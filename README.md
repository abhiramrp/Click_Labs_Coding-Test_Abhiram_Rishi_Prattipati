# Click_Labs_Coding-Test_Abhiram_Rishi_Prattipati

## Part 1 — Diagnose and Fix a Bug

The error is happening with this console message. 

```
breezy-fulltime-test.html:917 Uncaught SyntaxError: Failed to execute 'querySelector' on 'Document': 'file:////Documents/Click_Labs_Coding-Test_Abhiram_Rishi_Prattipati/breezy-fulltime-test.html#pricing' is not a valid selector.
    at HTMLAnchorElement.<anonymous> (breezy-fulltime-test.html:917:31)
(anonymous) @ breezy-fulltime-test.html:917
```

and this line of code. 

``` const target = document.querySelector(a.href); ```

It is returning the absolute HTML path instead of the id. To fix this, set the value of target to the section id ONLY if it exists. To prevent console errors, I added a toast message that displays a message. 

```
const hrefId = a.getAttribute('href');
const target = hrefId.length > 1 ? document.querySelector(hrefId) : null;

if (target) {
    target.scrollIntoView({ behavior: 'smooth', block: 'start' });
} else {
    showToast("Section is not implemented");
}
```

## Part 2 — Redesign a Section

```
  .steps { display: flex; gap: 32px; margin-top: 56px; flex-wrap: nowrap; justify-content: center; }
  .step {
    flex: 1; min-width: 220px; max-width: 300px; text-align: center;
    position: relative; padding: 0 12px;
    transition: transform 0.5s ease, box-shadow 0.5s ease;
  }
  .step:hover { box-shadow: 0 8px 24px rgba(24, 177, 247, 0.4); transform: scale(1.1); padding-top: 3px;}

  /* connector line — now on .step, sized relative to .step's responsive width */
  .step:not(:last-child)::after {
    content: "";
    position: absolute;
    top: 28px; /* half of step-num's 56px height = its vertical center */
    left: 50%;
    width: calc(100% + 32px); /* 32px matches .steps { gap: 32px } */
    height: 2px;
    background: linear-gradient(90deg, var(--sky-100), var(--sky-400));
    z-index: 0;
  }

  .step:hover::after,
  .step:has(+ .step:hover)::after {
    opacity: 0;
  }
  
  @media (max-width: 768px) {
    .steps {flex-direction: column; align-items: center;}
    .step::after {opacity: 0;}
  }
```

I changed the CSS. For the connector line, I implemented `::after` and drew a line. For responsive screen size, I edited the steps class to column orientation. To hover with transition, I scaled it to a larger size and also remove the connecting line when hovered. 

## Part 3 - README Questions
1.	Deployed on GitHub Pages since this site is fully static without backend. It is integrated with GitHub repo. 
2.  Currently, a non-technical person needs to edit the raw HTML to make changes. In the future, the content can be moved to a JSON or MD files so they could edit through an UI instead. 
3.  Being static with no backend/database eliminates most attack surface, and everything's served over HTTPS by default; for production I'd add server-side input validation on the signup endpoint, and rate limiting once a real backend exists. I would also convert the repo to private and change the hosting provider.  
4.	Currently, it's only three HTML files with duplicate line code. For better code maintenance ina. team environment, I would implement shared components and moved styles and scripts to external files. I would document it in an markdown file.
5.	Since the website is framework free without backend, it is mostly fast. To optimize performance more, I would implement lazy loading for image files and content that is not visible on the screen. I wo
6.	I added real-time email validation on the newsletter form using a debounced regex check with visual feedback (border, icon, message) and a disabled submit button until valid; with more time I'd connect it to a real email service and add server-side validation as a backup.
