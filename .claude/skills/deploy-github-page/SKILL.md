---
name: deploy-github-page
description: Deploy the current project to GitHub Pages and return the live URL. Use when the user wants to publish their project online via GitHub Pages.
---

Deploy this project to GitHub Pages and return the live URL when done.

Follow these steps carefully, in order:

## Step 1 — Check prerequisites

Run these checks in parallel:
- `git --version` to confirm git is installed
- `gh --version` to confirm GitHub CLI is installed
- `gh auth status` to confirm the user is authenticated with GitHub

If `gh` is not installed or not authenticated, stop and tell the user to install it (`brew install gh`) and authenticate (`gh auth login`).

## Step 2 — Get GitHub username

Run `gh api user --jq '.login'` to get the authenticated GitHub username. Save this as `$GITHUB_USER`.

## Step 3 — Initialize git repo (if needed)

Check if `.git` exists. If not, run:
```
git init
git add .
git commit -m "Initial commit"
```

If `.git` already exists, check for uncommitted changes with `git status --porcelain`. If there are changes, stage and commit them:
```
git add .
git commit -m "Update before deploy"
```

## Step 4 — Create or connect GitHub remote repo

Run `gh repo view --json name 2>/dev/null` to check if a remote is already connected.

If no remote exists:
1. Determine the repo name from the project folder name (use the current directory basename, replace spaces with hyphens, lowercase)
2. Run: `gh repo create <repo-name> --public --source=. --remote=origin --push`

If a remote already exists, just run `git push origin main --force` (or `master` if that's the default branch).

## Step 5 — Set Vite base path

The repo name is needed for Vite's `base` config so assets load correctly on GitHub Pages.

Check `vite.config.ts`. If it does NOT already have a `base` field pointing to the repo name, add it:
- Edit `vite.config.ts` to add `base: '/<repo-name>/'` inside `defineConfig({ ... })`

Example:
```ts
export default defineConfig({
  base: '/my-repo-name/',
  plugins: [react()],
  ...
})
```

## Step 6 — Install gh-pages and add deploy script

Check if `gh-pages` is in `package.json` devDependencies. If not:
```
npm install --save-dev gh-pages
```

Check if `package.json` already has a `"deploy"` script. If not, add these two scripts:
- `"predeploy": "npm run build"`
- `"deploy": "gh-pages -d build"`

Use the Edit tool to update `package.json` if needed.

## Step 7 — Build and deploy

Run:
```
npm run deploy
```

This will build the project and push the `build/` folder to the `gh-pages` branch.

## Step 8 — Enable GitHub Pages (if needed)

Run:
```
gh api repos/$GITHUB_USER/<repo-name>/pages --method POST -f source='{"branch":"gh-pages","path":"/"}' 2>/dev/null || true
```

This enables GitHub Pages on the `gh-pages` branch. If it's already enabled, the error is suppressed.

## Step 9 — Commit config changes and push

If `vite.config.ts` or `package.json` were modified, commit and push:
```
git add vite.config.ts package.json package-lock.json
git commit -m "Configure GitHub Pages deployment"
git push origin main
```

## Step 10 — Return the live URL

The GitHub Pages URL will be:
```
https://<github-username>.github.io/<repo-name>/
```

Tell the user:
- The live URL
- That it may take 1–2 minutes for GitHub Pages to go live on first deploy
- They can check deployment status at: `https://github.com/<github-username>/<repo-name>/actions`
