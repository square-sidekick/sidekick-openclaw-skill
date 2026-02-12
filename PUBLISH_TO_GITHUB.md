# Publish To GitHub (First-Time Friendly)

This guide lets you publish this skill as a clean open-source repo.

## Option A: GitHub Web UI (no terminal)

1. In GitHub, click `New repository`.
2. Repository name suggestion:
   - `sidekick-openclaw-skill`
3. Set visibility:
   - `Public`
4. Add short description:
   - `OpenClaw skill for Sidekick outbound voice calling`
5. Click `Create repository`.
6. Upload the contents of this `openclaw-skill/` folder.
7. Commit message:
   - `Initial open-source skill package`
8. Add topics in repo settings:
   - `openclaw`
   - `ai-agent`
   - `voice-ai`
   - `twilio`
   - `elevenlabs`

## Option B: Terminal + Git CLI

Run from this project root:

```bash
mkdir -p /tmp/sidekick-openclaw-skill
cp -R openclaw-skill/* /tmp/sidekick-openclaw-skill/
cd /tmp/sidekick-openclaw-skill
git init
git branch -M main
git add .
git commit -m "Initial open-source skill package"
```

Create remote and push:

```bash
# Replace YOUR_GITHUB_USERNAME
git remote add origin git@github.com:YOUR_GITHUB_USERNAME/sidekick-openclaw-skill.git
git push -u origin main
```

If you use HTTPS remote instead of SSH:

```bash
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/sidekick-openclaw-skill.git
git push -u origin main
```

## Recommended Repo Settings

1. Add `README.md` as landing page (already included).
2. Add a license from GitHub UI:
   - `MIT` is common for skill templates.
3. Enable `Issues` so users can report setup problems.
4. Pin this section near top of README:
   - "Never commit real API keys."

## Security Notes

- Users must create their own `SIDEKICK_OUTBOUND_API_KEY`.
- Key is one-time reveal in Sidekick UI.
- Do not commit `.env` files with real keys.

