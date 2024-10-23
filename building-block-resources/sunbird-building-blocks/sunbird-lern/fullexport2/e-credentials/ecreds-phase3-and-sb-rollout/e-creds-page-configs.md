---
icon: elementor
---

# E-Creds Page Configs

* [Problem](https://project-sunbird.atlassian.net/wiki/spaces/UM/pages/1290502242/E-Creds+Page+Configs#Problem)
* [Solution](https://project-sunbird.atlassian.net/wiki/spaces/UM/pages/1290502242/E-Creds+Page+Configs#Solution)
* [Setting Up Header and Footer](https://project-sunbird.atlassian.net/wiki/spaces/UM/pages/1290502242/E-Creds+Page+Configs#Setting-Up--Header-and-Footer)

### Problem <a href="#problem" id="problem"></a>

Generated Certificate has a page number and a file path displayed at footer if CSS not configured properly.

Ticket Ref: [SB- 17835](https://project-sunbird.atlassian.net/browse/SB-17835)

### Solution <a href="#solution" id="solution"></a>

If using [print-service](https://project-sunbird.atlassian.net/wiki/spaces/UM/pages/1284997145/Print-Service) above problem is not reproducible, the only change required is to give `"displayHeaderFooter": false` as an args while generating pdf.

### Setting Up Header and Footer <a href="#setting-up-header-and-footer" id="setting-up-header-and-footer"></a>

If the consumer explicitly wants to **show** page number in Header/Footer then below is the configuration provided for the same in print-service.

`await page.pdf({path: pdfFilePath, format: 'A4',printBackground: true, "displayHeaderFooter": true, "headerTemplate":"<div class=\"page-footer\" style=\"width:100%; text-align:right; font-size:12px;\">Page <span class=\"pageNumber\"></span> of <span class=\"totalPages\"></span></div>", "footerTemplate": "<div class=\"page-footer\" style=\"width:100%; text-align:center; font-size:12px;\">Page <span class=\"pageNumber\"></span> of <span class=\"totalPages\"></span></div>" });`

headerTemplate 0r footerTemplate key can be used with the above-provided value, which will display the page number or required Header/Footer in the certificate.

Open Screenshot 2020-03-09 at 6.10.57 PM.png![](blob:https://project-sunbird.atlassian.net/9ce8b3d5-046b-47c0-a961-204d09b20c1e#media-blob-url=true\&id=917990c7-b6a3-4566-9c7f-ccab00d16c53\&collection=contentId-1290502242\&contextId=1290502242\&mimeType=image%2Fpng\&name=Screenshot%202020-03-09%20at%206.10.57%20PM.png\&size=855532\&width=1440\&height=793\&alt=)

Margins can also be set explicitly while generating pdf.

`await page.pdf({path: pdfFilePath, format: 'A4',printBackground: true, "displayHeaderFooter": true, "footerTemplate": "<div class=\"page-footer\" style=\"width:100%; text-align:center; font-size:12px;\">Page <span class=\"pageNumber\"></span> of <span class=\"totalPages\"></span></div>", margin: { bottom: 70, // minimum required for footer msg to display left: 25, right: 35, top: 30, } });`

&#x20;

Source

[https://www.api2pdf.com/print-header-footer-page-numbers-on-pdf-with-headless-chrome](https://www.api2pdf.com/print-header-footer-page-numbers-on-pdf-with-headless-chrome/)
