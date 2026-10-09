# Daily Auto Commit

This repo automatically commits once a day using GitHub Actions, so your
contribution graph stays green without you doing anything manually.

## How it works

- `.github/workflows/auto-commit.yml` runs on a schedule (default: every day
  at 09:00 UTC).
- Each run appends a timestamp line to `logs/activity.log` and pushes the
  commit using the repo's built-in `GITHUB_TOKEN` — no personal access token
  needed.
- You can also trigger it manually anytime from the **Actions** tab
  ("Run workflow" button), since `workflow_dispatch` is enabled.

## Setup (2 minutes)

1. Create a new **public** repo on GitHub (private repos also work, but only
   public repo commits show as green squares on your public profile unless
   you've enabled "private contributions" in your profile settings).
2. Upload/push these files (this whole folder) to that repo:
   ```bash
   cd auto-commit-repo
   git init
   git add .
   git commit -m "initial commit"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo>.git
   git push -u origin main
   ```
3. Go to your repo → **Settings → Actions → General → Workflow permissions**,
   and make sure "Read and write permissions" is selected. (This lets the
   workflow push commits.)
4. That's it. The workflow will now run daily on its own.

## Changing the schedule

Edit the `cron` line in `.github/workflows/auto-commit.yml`. Cron is in UTC.
Examples:
- `'0 9 * * *'` → every day at 09:00 UTC
- `'30 14 * * *'` → every day at 14:30 UTC
- `'0 */12 * * *'` → every 12 hours

You can test cron expressions at https://crontab.guru

## Note

GitHub only counts a commit toward your contribution graph if it's on the
repo's default branch and (for private repos) if you've turned on "Include
private contributions" in your profile settings. This workflow doesn't
represent real project work — it's just a way to keep the graph active.
If you want, I can also help you find small real side-projects to commit to
instead, which looks better to anyone actually reviewing your GitHub.
