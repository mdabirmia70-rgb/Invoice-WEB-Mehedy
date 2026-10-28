# Google Sheets invoice backup setup

The browser page cannot change a Google Apps Script deployment by itself. Deploy the included `Code.gs` once, then point `index.html` at the new deployment.

1. Open the target spreadsheet and choose **Extensions → Apps Script**.
2. Replace the editor contents with [`Code.gs`](./Code.gs) and save.
3. Select `setupInvoiceBackup` in the function list and click **Run**. Review and grant the requested Sheets and Drive permissions. This keeps existing invoice rows, renames `Sheet1` to `Invoices`, adds the invoice detail headers, and creates `Invoice Items` and `Invoice PDF Backups` as needed.
4. Choose **Deploy → New deployment → Web app**. Set **Execute as** to your account and **Who has access** to **Anyone**, then deploy and copy the URL ending in `/exec`.
5. In `index.html`, replace `PASTE_DEPLOYED_WEB_APP_URL_HERE` in `GOOGLE_SCRIPT_URL` with the copied deployment URL.
6. Publish the updated site and test with a sample invoice. Confirm the summary appears in `Invoices`, each product line in `Invoice Items`, and the PDF link opens from the authorized Google account.

The `Invoices` tab stores one row per invoice. `Invoice Items` stores one row per product and repeats the invoice number so the detail rows can be filtered or joined back to the summary. The PDF files are kept in the private `Invoice PDF Backups` Drive folder; the script does not make customer invoices public.

The web app must be accessible to anyone for a static GitHub Pages site to call it. Treat its URL as public and do not store secrets in the page.
