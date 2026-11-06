# Yixuan Song's personal website

Static migration of <https://yixuans.wixsite.com/home>, preserving its existing desktop and mobile designs, wording, photographs and portfolio structure.

Website: <https://yixuan-siren.github.io/>

## Editing and previewing

The deployable website lives in `site/`. There is no production build step and no Wix runtime. Edit the corresponding `index.html`, `site/migration.css`, or `site/site.js` and commit the changes. Small screens load the retained Wix mobile composition from `site/_mobile/` while keeping the normal page URL.

```sh
npm ci
npm run preview
npm run check
```

Open <http://127.0.0.1:4173/>. GitHub Actions validates and deploys `site/` when changes are pushed to `main`. Repository Settings → Pages must use **GitHub Actions** as the source.

The first browser upload stores the source in three `migration-part-*.zip` packages. The read-only workflow extracts these into its temporary build directory and publishes `site/`; it cannot push back to the repository. The full, uncompressed working source is retained locally in this project. Once ordinary Git upload is authorized, the packages can be replaced with the uncompressed files; the same workflow supports both forms.

## Migration record

- 13 routes: home, About, Publications, Research Blog, one blog article, one category, two tags, Portfolio and four project detail pages.
- Separate desktop and mobile layouts, with images, fonts, the existing CV PDF and available videos served locally.
- Navigation, contact anchors, image enlargement, portfolio navigation, blog search and share controls use the small local script.
- Existing Wix placeholder publication links were replaced with their displayed DOI destinations. The home page's template LinkedIn destination was replaced with the profile already used in the original footer.
- The contact form opens the visitor's email application. It does not send or store messages on the website. Its button and explanation state this clearly.
- Five unavailable Disaggregation tank videos retain their cover images with “Video coming soon,” as requested. Their identifiers are in `migration/deferred-media.json`; add the original MP4s when available.
- The initial migration retained the original content. On November 2, 2026, the publication page and home-page selections were updated from the current CV, with DOI-verified title and citation corrections. The public CV excludes the personal phone, references, and grants/funding; the master CV remains unchanged.
- The Wix advertising banner and hosting attribution are removed; the original site remains available at Wix.

`migration/manifest.json` records source URLs and locally retained assets. `scripts/migrate.mjs` generated the initial static copy from the captured public HTML; the raw captures remain local under the ignored `migration/source/` folder. Do not rerun migration after editing generated pages unless you intend to regenerate them from those captures.

The original site contains some template text and older information. These have been retained for later, deliberate revision.

## Publication, CV and media updates

- `content/home.json` contains the home-page introduction, academic profiles, and website contact email. Run `npm run home:update` after editing it.
- `content/publications.json` contains the published papers and separately labelled manuscripts. Run `npm run content:update` after editing it.
- The home page shows the three most recent published papers whose `authorRoles` include `first` or `corresponding`, followed by papers explicitly listed in `homepage.additionalDois` (currently the 2020 Physics of Fluids paper). Each selected paper needs a brief `homepageSummary`. Record `publishedDate` as `YYYY-MM-DD` when adding a paper; entries without a full date use the publication year for ordering. The full Publications page retains every published paper.
- `content/about.json` holds the awards shown on About. Run `npm run about:update` after editing it.
- `node scripts/build-public-cv.mjs /absolute/path/to/CV` builds the public download from the existing CV LaTeX source. It requires the source's `resume.cls` and a local LaTeX installation.
- The website links to `site/documents/Yixuan-Song-CV.pdf`.
- New private media goes in the local `素材库/01_原始素材/图片`, `视频`, or `文档` folders. Prepared web copies go in `素材库/02_网站版本/`. This library is ignored by Git; only explicitly selected website files are deployed.
