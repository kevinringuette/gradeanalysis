# Grade Analysis Dashboard

This repository hosts a static front-end dashboard for exploring student grade data. The app is built as a single HTML page that consumes Airtable and n8n webhook APIs directly from the browser.

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
