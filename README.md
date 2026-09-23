# Sample docs-as-code portal

A developer portal for the Swagger Petstore API, built on your own machine by the
[APIMatic CLI](https://www.npmjs.com/package/@apimatic/cli) from the files in this
repository. Nothing is uploaded to generate it: the CLI reads `src/`, builds a static
site, and writes it to a folder you can host anywhere.

This branch uses the input layout of CLI version 2. The `master` branch holds the
layout of version 1, which sends the same files to APIMatic's hosted portal
generation API instead.

## Layout

```
src/
  apimatic.json            the portal's name, logo, colours, fonts and layout, and the
                           SDK languages the project ships
  spec/
    petstore.json          the OpenAPI document; one page per operation, grouped by tag
    APIMATIC-META.json     settings for SDK generation
  content/
    nav.json               the order of the pages below, and of the portal's tabs
    index.md               the home page
    authentication.md      a guide, written in Markdown with front matter
    what-apimatic-offers.md
  static/
    images/                copied to the site root; the logo lives here
  APIMATIC-BUILD.json      used by the SDK commands only
```

The spec's file name becomes the URL segment: `spec/petstore.json` publishes the
operation pages under `/api/petstore/`.

`src/apimatic.json` names its schema, so an editor such as VS Code completes and checks
the `portal` block as you type. The `languages` block lists the SDKs the project ships;
a portal needs at least one.

## Build it

You need Node 24 or newer and an APIMatic account with portal generation enabled.

```bash
npx @apimatic/cli@2 auth login
npx @apimatic/cli@2 portal generate --destination ./portal
```

The `portal/` folder is the whole site. Serve it from any static host: GitHub Pages,
Netlify, Cloudflare Pages, S3 behind a CDN, or a plain web server. Point unknown paths
at `404.html` and nothing else needs configuring.

To edit with live reload:

```bash
npx @apimatic/cli@2 portal serve
```

## Automate it

`.github/workflows/DeployStaticPortal.yml` runs the same `portal generate` on GitHub
Actions and uploads the result as a workflow artifact. Add the `API_KEY` repository
secret with an APIMatic API key, then trigger the workflow by hand or push to this
branch. Deploying the artifact is left to the hosting platform of your choice.
