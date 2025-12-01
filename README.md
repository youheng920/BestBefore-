# BestBefore
Simple static landing page for the BestBefore Android app.

This workspace contains a single-page website that introduces the app and provides a direct APK download link.

Files in this repo:
- `index.html` — Single-page landing page with Tailwind CSS (CDN) and APK download links.
- `assets/` — Placeholder folder to store `app-release.apk` (replace with your app binary).
- `.gitignore` — Ignores `*.apk` by default to avoid committing APKs to the repo.

Local preview
-------------
To preview the site locally, run a simple static server from the repo root:

```bash
python3 -m http.server 8000
# then open http://localhost:8000 in your browser
```

Notes
-----
- Replace `assets/README.txt` with your actual `app-release.apk` when available.
- For production distribution, host the APK as a release asset (GitHub Releases, S3, or CDN) instead of committing it to source control.
- When allowing direct APK downloads, remember to serve over HTTPS so users don't get warnings during downloads.

Publish to GitHub Pages
-----------------------

To publish this static site to GitHub Pages using GitHub Actions, the repo already contains a workflow at `.github/workflows/pages.yml` that will deploy the repository root to GitHub Pages whenever you push changes to the `main` branch.

Steps to publish:

1. Commit and push your changes to your remote `main` branch:

```bash
git add .
git commit -m "Add GitHub Pages deploy and release workflows"
git push origin main
```

2. After push completes, go to your repository on GitHub -> Settings -> Pages, or open the Actions tab to see the `Deploy to GitHub Pages` workflow run and the GitHub Pages site URL.

Uploading APK as a GitHub Release
---------------------------------

There is also a workflow at `.github/workflows/release.yml` that will automatically create a GitHub Release and upload `assets/app-release.apk` when you push a tag like `v1.0.0`.

To create a release with the APK (locally) you can run:

```bash
# Create a tag
git tag v1.0.0
git push origin v1.0.0
```

This will trigger `.github/workflows/release.yml` and attach `assets/app-release.apk` to the release (make sure `assets/app-release.apk` exists in the repo or is part of your CI build artifacts).

Important security note
-----------------------

- Avoid committing real APKs to a public repo. Instead, upload them directly from your CI job or use GitHub Releases via a CI build that produces the binary.
- Make sure releases and actions are configured with appropriate permissions and secrets if you add more complex pipelines (Android builds, signing keys, etc.).
