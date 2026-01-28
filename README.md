# cchistory-site

Web app to view and compare Claude Code version prompts with side-by-side diff visualization.

This fork is configured for **GitHub Pages** deployment with automated updates.

## Live Site

Visit: https://cchistory.prismalabs.dev

## How It Works

1. **GitHub Actions** check for new Claude Code versions daily
2. New prompts are automatically fetched and committed to `data/`
3. Site is built and deployed to GitHub Pages

## Setup (for your own fork)

### 1. Fork this repository

### 2. Add your Anthropic API Key

Go to **Settings → Secrets → Actions** and add:
- `ANTHROPIC_API_KEY`: Your Anthropic API key

### 3. Enable GitHub Pages

Go to **Settings → Pages**:
- Source: **GitHub Actions**

### 4. Run initial update

Go to **Actions → Update Prompts → Run workflow**:
- Check "Fetch all versions from 1.0.0 to latest"
- Click "Run workflow"

This will fetch all ~200+ versions (takes ~30 minutes).

## Manual Updates

To fetch a specific version manually:

```bash
cd data
npx @mariozechner/cchistory <version>
# or fetch latest
npx @mariozechner/cchistory <current-latest> --latest
```

Then commit and push - GitHub Actions will deploy automatically.

## Local Development

```bash
npm install
npm run build
# Copy data to dist
mkdir -p dist/data && cp data/* dist/data/
# Serve locally
npx serve dist -l 3000
```

## Project Structure

```
cchistory-site/
├── .github/workflows/
│   ├── deploy.yml           # Build & deploy to GitHub Pages
│   └── update-prompts.yml   # Fetch new Claude Code versions
├── src/frontend/            # Frontend app (Lit + Monaco Editor)
├── data/                    # Prompt files (committed to git)
│   ├── versions.json        # Version metadata
│   └── prompts-*.md         # Prompt files per version
├── dist/                    # Build output (git ignored)
└── infra/                   # Build scripts
```

## Tech Stack

- **Frontend**: Lit Elements, Monaco Editor (VS Code's diff editor)
- **Styling**: Tailwind CSS v4
- **Build**: tsup bundler
- **Deployment**: GitHub Pages + GitHub Actions

## Original Project

This is a fork of [badlogic/cchistory-site](https://github.com/badlogic/cchistory-site) by Mario Zechner.

The original runs with Docker and a server-side update service. This fork is modified for static GitHub Pages hosting.
