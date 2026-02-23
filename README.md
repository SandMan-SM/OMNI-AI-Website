# Omni Leads — local dev & GitHub push notes

This repository was exported from Replit. These notes show how to push it to GitHub and run it from VS Code so you can use VS Code like Replit.

Prereqs
- Node 18+ and npm installed
- git installed
- (Optional) GitHub CLI `gh` for creating repos from the terminal
- (Optional) ngrok (for exposing your localhost publicly)

1) Create a GitHub repo and push

Option A — using GitHub CLI (recommended):

```bash
# from project root
git init
git add .
git commit -m "Import from Replit"
# create a public repo and push current directory
gh repo create YOUR_USERNAME/REPO_NAME --public --source=. --remote=origin --push
```

Option B — using the GitHub web UI:

```bash
git init
git add .
git commit -m "Import from Replit"
# create an empty repo on github.com and then run:
git remote add origin git@github.com:YOUR_USERNAME/REPO_NAME.git
git branch -M main
git push -u origin main
```

2) Do not commit secrets

Put API keys and secrets into a local `.env` file (example `.env.example` can be added and committed). `.gitignore` already excludes `.env`.

3) Run locally in VS Code (like Replit)

Open the repository in VS Code. In the integrated terminal:

```bash
npm ci
npm run dev
```

- `npm run dev` runs `tsx server/index.ts` (your server sets up Vite in dev). The server listens on `process.env.PORT` or defaults to 5000.
- If you prefer production flow:

```bash
npm ci
npm run build
npm run start
```

4) Expose your local site publicly (optional)

If you want a public URL like Replit provides, use `ngrok` or a similar tunnel:

```bash
# install (macOS)
brew install --cask ngrok

# run tunnel to the port your app uses (default 5000)
ngrok http 5000
```

Copy the HTTPS URL from ngrok and share it. Note: ngrok free plans rotate URLs.

5) Re-import to Replit from GitHub (optional)

- In Replit, choose Create → Import from GitHub and pick this repository. Replit will run your configured start command.

6) Useful VS Code tasks

Open the Command Palette → Run Task to run the tasks defined in `.vscode/tasks.json` (dev and prod tasks).

Troubleshooting
- If `npm run build` fails, check `script/build.ts` for expected output (should produce `dist/index.cjs` for `npm run start`).
- If the process fails to bind, confirm no other app is using the port and that `process.env.PORT` is set if required.

If you want, I can: push the repo for you (you'll need to give repo name or grant access), create a `.env.example` template, or add a GitHub Actions workflow for CI.
