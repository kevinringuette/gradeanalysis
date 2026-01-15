# Grade Analysis Dashboard

This repository hosts a static front-end dashboard for exploring student grade data. The app is built as a single HTML page that consumes Airtable and n8n webhook APIs directly from the browser.

## Using the dashboard

1. **Pick a section.** The landing screen queries the Master Sections table and lets you search by section name, teacher, block, or Section ID. The roster size is shown so you can confirm you have the right class before drilling in.
2. **Choose a student.** After selecting a section you’ll see only the students linked to that record in the Student Roster. Search is scoped to the roster and matches both names and email addresses.
3. **Review grades and attendance.** The progress chart and stat cards reflect the categories returned by the n8n webhook. Attendance pulled from the Airtable Attendance table is plotted beneath the x-axis so absences, tardies, and early departures line up with the assignment timeline. Tooltips show both assignment details and any attendance events recorded for that day.

If a student is missing the numeric **ID** field or a section is missing the numeric **Section ID**, the app surfaces a validation error before making webhook or attendance requests so you can correct the data in Airtable.

## Local development

You can open the `index.html` file directly in a browser for local testing. No build step is required.

```bash
# macOS Finder / Windows Explorer
open index.html
```

Because the page makes requests to Airtable and an external webhook, ensure that the API key and webhook are accessible from your network.

## Deployment

The project is ready to deploy as a static site on Vercel:

1. Create a new Vercel project pointing at this repository.
2. Choose the **Other** framework preset so Vercel serves the repository as static content.
3. Deploy; Vercel will automatically serve `index.html` from the project root.

If you need to keep the Airtable API key private, consider migrating the data requests to a Vercel serverless function or a secure API proxy.

## Webhook troubleshooting

The grade view now includes a **Webhook debug details** panel under the chart. The panel automatically opens after the first request and displays the payload, status code, headers, and a compact preview of the JSON returned from your n8n workflow. Use the toggle button to collapse or expand the history.

If a request fails (for example due to a `404` or JSON parse error) the panel highlights in red, expands automatically, and lists the most recent stages so you can confirm whether the webhook responded and what the server returned without digging through the browser console. The last status label in the panel header mirrors the most recent stage so it is easy to spot problems such as `parse error` or `empty result`.

> **Note:** Some browsers currently warn about a `Permissions-Policy` header that includes the `browsing-topics` feature. That header is emitted by n8n; the warning is benign, and you can inspect the raw headers inside the debug panel to verify the response you received.
