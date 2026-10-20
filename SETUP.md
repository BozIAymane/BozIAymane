# Setup Guide — GitHub Profile README

Step-by-step instructions to deploy your professional GitHub Profile README.

---

## Prerequisites

- A GitHub account ([BozIAymane](https://github.com/BozIAymane))
- Git installed locally
- A text editor for any customizations

---

## Step 1: Create the Profile Repository

GitHub displays a special README on your profile when you have a **public repository** whose name **exactly matches your username**.

1. Go to [github.com/new](https://github.com/new)
2. Set **Repository name** to: `BozIAymane`
3. Set visibility to **Public**
4. Check **Add a README file** (we'll replace it)
5. Click **Create repository**

> **Note:** If the repository `BozIAymane/BozIAymane` already exists, skip this step.

---

## Step 2: Push the Files

Clone the profile repository and copy all files from this project:

```bash
# Clone the profile repository
git clone https://github.com/BozIAymane/BozIAymane.git
cd BozIAymane

# Copy all files from this project into the cloned repo
# (adjust the source path to where you have the my_git folder)
cp -r /path/to/my_git/* .
cp -r /path/to/my_git/.github .

# Stage, commit, and push
git add -A
git commit -m "feat: add professional profile README"
git push origin main
```

### Files to Include

```
BozIAymane/
├── README.md                          # The profile README
├── assets/
│   ├── header.svg                     # Animated header
│   └── footer.svg                     # Animated footer
├── .github/
│   └── workflows/
│       ├── metrics.yml                # GitHub Metrics workflow
│       └── snake.yml                  # Contribution snake workflow
└── SETUP.md                           # This file (optional to include)
```

---

## Step 3: Create a Personal Access Token (PAT) for Metrics

The `lowlighter/metrics` action requires a Personal Access Token to read your GitHub data.

1. Go to **[github.com/settings/tokens](https://github.com/settings/tokens)**
2. Click **Generate new token (classic)**
3. Set a descriptive name: `Profile Metrics`
4. Set expiration (recommended: 90 days, then renew)
5. Select these scopes:
   - ✅ `repo` — Required for repository statistics and private repo metrics
   - ✅ `read:user` — Required for profile information
6. Click **Generate token**
7. **Copy the token immediately** — you won't see it again

### Why These Scopes?

| Scope | Purpose |
|-------|---------|
| `repo` | Allows the action to read repository data, language statistics, and commit history |
| `read:user` | Allows reading profile information for the metrics card |

> **Security:** The token is stored as an encrypted secret and is never exposed in logs. Use the minimum scopes needed. You do **not** need `write:packages`, `admin:org`, or any destructive permissions.

---

## Step 4: Add the Token as a Repository Secret

1. Go to your profile repo: **[github.com/BozIAymane/BozIAymane/settings/secrets/actions](https://github.com/BozIAymane/BozIAymane/settings/secrets/actions)**
2. Click **New repository secret**
3. Name: `METRICS_TOKEN`
4. Value: Paste the PAT you generated in Step 3
5. Click **Add secret**

---

## Step 5: Configure Repository Permissions for Actions

The snake animation workflow needs write permissions to push to the `output` branch.

1. Go to **[github.com/BozIAymane/BozIAymane/settings/actions](https://github.com/BozIAymane/BozIAymane/settings/actions)**
2. Scroll to **Workflow permissions**
3. Select **Read and write permissions**
4. Click **Save**

---

## Step 6: Run the Workflows Manually

After pushing all files, trigger both workflows for the first time:

### Metrics Workflow

1. Go to the **[Actions tab](https://github.com/BozIAymane/BozIAymane/actions)**
2. Select **Metrics** from the left sidebar
3. Click **Run workflow** → **Run workflow**
4. Wait for completion (~2-3 minutes)
5. The workflow will generate `github-metrics.svg` and commit it to the repo

### Snake Workflow

1. In the **[Actions tab](https://github.com/BozIAymane/BozIAymane/actions)**
2. Select **Contribution Snake** from the left sidebar
3. Click **Run workflow** → **Run workflow**
4. Wait for completion (~1-2 minutes)
5. The workflow will create an `output` branch containing the snake SVGs

---

## Step 7: Verify

1. Visit **[github.com/BozIAymane](https://github.com/BozIAymane)**
2. You should see:
   - ✅ Animated SVG header
   - ✅ Social badges (GitHub, LinkedIn, Email)
   - ✅ About Me section
   - ✅ Technology stack table
   - ✅ Featured projects grid
   - ✅ GitHub stats cards (GitHub Readme Stats)
   - ✅ Streak stats
   - ✅ Metrics SVG (after first workflow run)
   - ✅ Snake animation (after first workflow run)
   - ✅ Animated footer

---

## Workflow Schedules

| Workflow | Schedule | Description |
|----------|----------|-------------|
| **Metrics** | Daily at 00:00 UTC | Regenerates the GitHub metrics SVG card |
| **Contribution Snake** | Every 12 hours | Updates the contribution snake animation |

Both workflows also support **manual dispatch** from the Actions tab.

---

## Troubleshooting

### Metrics SVG is broken / not appearing
- Confirm the `METRICS_TOKEN` secret is set correctly
- Check the Actions tab for error logs
- Ensure the PAT has `repo` and `read:user` scopes
- Verify the PAT has not expired

### Snake animation is not appearing
- Verify the `output` branch exists (created after the first successful workflow run)
- Check that **Workflow permissions** are set to "Read and write"
- Ensure the README references the correct URL:
  ```
  https://raw.githubusercontent.com/BozIAymane/BozIAymane/output/github-snake-dark.svg
  ```

### GitHub Stats cards not loading
- These use the free [github-readme-stats](https://github.com/anuraghazra/github-readme-stats) API
- They may occasionally be slow due to rate limiting
- No configuration is required — they work out of the box

### Workflow creates an infinite loop
- The snake workflow uses `[skip ci]` in commit messages to prevent re-triggering
- The metrics workflow commits directly and only runs on `schedule` / `workflow_dispatch`, not on `push`

---

## Customization Tips

### Change the color palette
- Edit `assets/header.svg` and `assets/footer.svg` — modify the hex colors (`#00d4ff`, `#0099ff`, `#0a0e27`)
- Update the `bg_color`, `title_color`, `border_color` parameters in the GitHub Stats URLs in `README.md`

### Add or remove featured projects
- Edit the projects table in `README.md`
- Each project is a `<td>` block — copy the structure and update the content

### Adjust metrics plugins
- Edit `.github/workflows/metrics.yml`
- See available plugins: [lowlighter/metrics — Plugin List](https://github.com/lowlighter/metrics#-plugins)

---

## Required Secrets Summary

| Secret Name | Where to Create It | Required By |
|-------------|-------------------|-------------|
| `METRICS_TOKEN` | Repository Settings → Secrets → Actions | `metrics.yml` workflow |

> The `GITHUB_TOKEN` used by the snake workflow is **automatically provided** by GitHub Actions — no manual setup needed.

---

## Files Checklist

| File | Purpose | Status |
|------|---------|--------|
| `README.md` | Profile README displayed on GitHub | ✅ Created |
| `assets/header.svg` | Animated header banner | ✅ Created |
| `assets/footer.svg` | Animated footer banner | ✅ Created |
| `.github/workflows/metrics.yml` | GitHub Metrics generation | ✅ Created |
| `.github/workflows/snake.yml` | Contribution snake animation | ✅ Created |
| `SETUP.md` | This setup guide | ✅ Created |
| `github-metrics.svg` | Generated metrics card | ⏳ Generated after first workflow run |
| `output` branch (snake SVGs) | Snake animation assets | ⏳ Created after first workflow run |

---

## What Requires Manual Action

1. **Create the `BozIAymane` repository** on GitHub (if it doesn't exist)
2. **Generate a Personal Access Token** and add it as `METRICS_TOKEN`
3. **Set workflow permissions** to "Read and write"
4. **Push these files** to the `BozIAymane` repository
5. **Trigger both workflows** manually for the first time
6. **Verify** the profile page looks correct
