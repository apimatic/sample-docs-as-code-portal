# Sample docs-as-code portal

The `src/` directory on this branch is the starting point for projects made in
APIMatic's onboarding web app. The app clones this repository, replaces
`spec/petstore.json` with the user's own API description, and lets them download the
result. They then install version 2 of the
[APIMatic CLI](https://www.npmjs.com/package/@apimatic/cli) and run `apimatic quickstart`
with the project already in place, which records the SDK languages they choose and
builds the portal.

The `master` branch holds the version 1 sample, which APIMatic's hosted portal
generation builds.

## Layout

```
src/
  apimatic.json        the portal's brand and header links, and its SDK languages
  spec/
    petstore.json      the sample API; the onboarding app replaces it with the user's
  content/
    index.md           the home page
    nav.json           the order of the pages beside it
  static/
    images/            placeholder logos and favicon, copied to the site root
```

The portal takes its name and description from the spec, because `apimatic.json`
leaves `site` empty; a project with more than one spec has to set `site.name`. The
spec's file name becomes the URL segment: `spec/petstore.json` publishes the operation
pages under `/api/petstore/`.

Each language in the `languages` block gets a page on the SDKs tab with a download
link, and its own code sample on every operation page. C#, TypeScript and Python are
available today. A `plugin` block, which quickstart writes, adds a Context Plugin tab.
`apimatic.json` names its schema, so an editor such as VS Code completes and checks it
as you type.

## Changing the starter

Whatever is added under `src/` reaches every new project, so keep it free of anything
that belongs to one API. Use only settings that released 2.x CLIs read: the CLI refuses
keys it does not know, and the onboarding app clones this branch as it is at the time.

## Build it

You need Node 24 or newer and an APIMatic account with portal generation enabled.

```bash
npx @apimatic/cli@2 auth login
npx @apimatic/cli@2 portal generate --destination ./portal
```

`portal generate` sends `src/` to APIMatic, which generates the SDKs, their docs, the
code samples and, when there is a `plugin` block, the context plugin. The CLI then builds
the site on your machine. The `portal/` folder is the whole site. Serve it from any static
host: GitHub Pages, Netlify, Cloudflare Pages, S3 behind a CDN, or a plain web server.
Point unknown paths at `404.html` and nothing else needs configuring.

To edit with live reload:

```bash
npx @apimatic/cli@2 portal serve
```

It fetches the generated SDKs once, when it starts, so restart it after adding a
language or a `plugin` block.

## Automate it

`.github/workflows/DeployStaticPortal.yml` runs the same `portal generate` on GitHub
Actions and uploads the result as a workflow artifact. Add the `API_KEY` repository
secret with an APIMatic API key, then trigger the workflow by hand or push to this
branch. Deploying the artifact is left to the hosting platform of your choice.
