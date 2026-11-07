# socialshields.org

Homepage for Social Shields. A single static page, `index.html`, with no build step.

- Project icons come from the Iso Icons API at icons.socialshields.org.
- The sheep mascot is rendered by open-bot-avatar (MIT) loaded from jsDelivr; a static SVG fallback is inlined.
- `brand.css` is the shared stylesheet for all `*.socialshields.org` sites, served at https://socialshields.org/brand.css. `STYLE_GUIDE.md` explains the tokens and rules behind it.

## Deploy on Cloudflare Pages

Connect this repository in Cloudflare Pages with framework preset "None", build command empty, and output directory `/`.
