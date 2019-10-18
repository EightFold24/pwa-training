# Lighthouse

Lighthouse is an open-source, automated tool for improving the quality of web pages. You can run it against any web page, public or requiring authentication. It has audits for performance, accessibility, progressive web apps, and more.

![Lighthouse Logo](https://developers.google.com/web/progressive-web-apps/images/pwa-lighthouse.png)

You can run Lighthouse in Chrome DevTools, from the command line, or as a Node module. You give Lighthouse a URL to audit, it runs a series of audits against the page, and then it generates a report on how well the page did. From there, use the failing audits as indicators on how to improve the page. Each audit has a reference doc explaining why the audit is important, as well as how to fix it.

## Run Lighthouse in Chrome DevTools
Lighthouse now powers the Audits panel of Chrome DevTools. To run a report:

1. Download Google Chrome for Desktop.
2. In Google Chrome, go to the URL you want to audit. You can audit any URL on the web.
3. [Open Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/#open).
4. Click the **Audits** tab.

![Open Lighthouse in Google Chrome](https://developers.google.com/web/tools/lighthouse/images/audits.png)
*Figure 1. To the left is the viewport of the page that will be audited. To the right is the Audits panel of Chrome DevTools, which is now powered by Lighthouse*

5. Click Perform an audit. DevTools shows you a list of audit categories. Leave them all enabled.
6. Click Run audit. After 60 to 90 seconds, Lighthouse gives you a report on the page.

![Run Lighthouse Audit](https://developers.google.com/web/tools/lighthouse/images/cdt-report.png)
*Figure 2. A Lighthouse report in Chrome DevTools*

### TODO
* Run a lighthouse audit on your webapp and take note of the progressive webapp analytics
* In the next section we are going to fix these

## More Resources
* https://codelabs.developers.google.com/codelabs/pwa-offline-quickstart/index.html#2

***Content from this document is adapted from https://developers.google.com/web/tools/lighthouse#devtools***

### [Next Section >>>](../02-serviceworker)