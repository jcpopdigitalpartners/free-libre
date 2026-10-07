# The Learning Library

An Astro course library for JC Choi, with topic filters, text search, and links to independently hosted learning objects. No database or server is needed.

Course titles and Open buttons trigger a diagonal pixelated wipe lasting about 0.7 seconds, then open the learning object in the same tab. Browser Back returns to the library. Reduced-motion preferences skip the animation; Ctrl/Cmd-click and other modified clicks keep their usual browser behavior. Source links still open in a new tab. With JavaScript disabled, courses open directly in a new tab.

## Run in VS Code

Install Node.js 22.12 or newer, open this folder in VS Code, and run:

```bash
npm ci
npm run dev
```

Open the localhost address Astro prints. The local site uses `/course-library/` as its base path by default.

## Publish on GitHub Pages

1. Create a **public** repository at https://github.com/new. Suggested name: `course-library`. Do not initialize it with a README, license, or gitignore.
2. Extract this archive and open the `course-library` folder in VS Code. The repository root must contain `package.json`, `astro.config.mjs`, `src`, and `.github` directly, not another enclosing folder.
3. In the VS Code terminal, run:

```bash
git init -b main
git add .
git commit -m "Create Astro learning library"
git remote add origin https://github.com/jcpopdigitalpartners/course-library.git
git push -u origin main
```

If you chose another repository name, change the remote URL above. The workflow automatically uses the actual repository name and account for Astro's base path and site URL.

4. Open the repository on GitHub. Go to **Settings → Pages → Build and deployment → Source**, and choose **GitHub Actions**.
5. Open **Actions → Deploy course library to GitHub Pages**. If the initial run failed before Pages was enabled, choose **Run workflow → main → Run workflow**.
6. Wait for both the build and deploy jobs to succeed. The deployment link appears in the workflow summary and Settings → Pages. With the suggested repository name, the address is `https://jcpopdigitalpartners.github.io/course-library/`.

The deployment workflow is included at `.github/workflows/deploy-pages.yml`. In Windows File Explorer, enable hidden items if needed. Do not use “Deploy from a branch” for the Astro source.

## Add or change a learning object

Edit `src/data/courses.json`. Each entry creates one card. Duplicate an entry, assign a unique ID, and update its text and URLs:

```json
{
  "id": "your-course",
  "title": "Your learning object title",
  "description": "What learners will explore or practice.",
  "topic": "Astro",
  "format": "Interactive lab",
  "level": "Intermediate",
  "url": "https://jcpopdigitalpartners.github.io/your-course/",
  "repository": "https://github.com/jcpopdigitalpartners/your-course",
  "outcome": "The practical skill learners will take away.",
  "visual": "boundary"
}
```

Choose a visual style: `frameworks`, `boundary`, or `cloud`. Topic buttons and counts update automatically; search includes the title, description, topic, format, and outcome. Keep the file valid JSON (no trailing commas).

The three initial links are taken from your shared project URLs. External pages could not be fetched in this environment; confirm their availability before sharing publicly. Their source links use the corresponding GitHub repository paths.

Commit and push edits to `main`; GitHub Actions rebuilds the library. Your learning objects stay in their own repositories and are linked, not copied or embedded.

## Local production check

```bash
npm run build
npm run preview
```

`dist/` is generated output. The Pages workflow builds it and uploads it automatically. The lockfile is included for repeatable installation.
