# The Pardo Family Archive

A responsive family-history site for the Pardo, Bibi, Safdieh, Massry, and connected family lines. It includes a generational tree, searchable relatives and surnames, historical stories, and a timeline. The interactive photo gallery starts with one approved portrait per relative, and visitors can search names, browse the complete collection, and move between images in an accessible viewer.

## Run locally

For local development, start the privacy-filtering server from this folder:

```sh
python3 server.py
```

Open `http://localhost:4173`. The checked-in `export-Ancestors.ged 3` is already redacted to the site's public privacy rules; the local server serves its normalized data at `/api/family-data`, and GEDCOM paths are blocked over HTTP. Keep any full, unredacted source GEDCOM outside the repository. Browser GEDCOM import is local to that browser session and does not upload the file.

## Deploy with GitHub Pages

The `Deploy family archive to GitHub Pages` workflow builds the static site on pushes to `main` and on manual runs. It reads the already-redacted GEDCOM from the repository checkout, embeds sanitized family data in a content-addressed JavaScript bundle, and also publishes the same bundled app as `app.js` so cached copies of the original homepage continue to work. It also writes `_site/family-data.json`, copies the approved local archival images from `assets/`, and adds `.nojekyll` so GitHub Pages serves the artifact files directly. It deploys only `_site`—the GEDCOM itself is not copied into the Pages artifact.

The build also publishes `family-archive.html` as an alternate entry point to the same site. Use it if a browser or CDN continues serving a cached copy of the root homepage after deployment.

The gallery uses the approved public portrait set stored in `featured-photos.json`. The public GEDCOM keeps every person and family relationship, but for living people not reliably established as 90 or older it retains only initials and surname plus family links; other personal facts and photos are removed. A living person reliably established as 90 or older may retain their name, birth date, and birthplace. Photos are published only for deceased people. The browser's local GEDCOM import applies the same age-based name, date, place, role, and photo restrictions. The public timeline omits recent household events. Review the generated site data and artifact before publishing.

To enable deployment:

1. In the repository, open **Settings → Pages** and set **Build and deployment → Source** to **GitHub Actions**.
2. Push the workflow and site changes to `main`, or run the workflow from **Actions → Deploy family archive to GitHub Pages → Run workflow**.
3. Open the deployment URL shown in the completed workflow or in **Settings → Pages**.

GitHub Pages is publicly accessible unless the repository’s GitHub plan and Pages settings support access restrictions. A private source repository does not by itself make the published site private. Treat all deployed names, relationships, photos, and historical details as public.