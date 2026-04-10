# GitHub Setup Instructions for VERIFIQ

## Step 1 — Create GitHub Repository

1. Go to **github.com/bbmw96** (already logged in)
2. Click **New repository**
3. Fill in:
   - **Repository name:** `verifiq`
   - **Description:** `IFC Compliance Checker for Singapore CORENET-X and Malaysia NBeS`
   - **Visibility:** Public (for GitHub Pages) or Private
   - **Do NOT** initialise with README (you already have one)
4. Click **Create repository**

## Step 2 — Push Source Code

From a terminal in the VERIFIQ project folder:

```bash
cd VERIFIQ
git init
git add .
git commit -m "feat: VERIFIQ v1.2.0 initial release"
git branch -M main
git remote add origin https://github.com/bbmw96/verifiq.git
git push -u origin main
```

## Step 3 — Create v1.2.0 Release Tag

```bash
git tag -a v1.2.0 -m "VERIFIQ v1.2.0 — 3D viewer, 89 SG rules, health score dashboard"
git push origin v1.2.0
```

This triggers the GitHub Actions workflow at `.github/workflows/release.yml` which:
- Builds VERIFIQ.Desktop in Release mode
- Zips the output as `VERIFIQ-v1.2.0-win-x64.zip`
- Creates a GitHub Release with download link

## Step 4 — Enable GitHub Pages for Website

1. In the GitHub repo, go to **Settings → Pages**
2. Under **Source**, select **Deploy from a branch**
3. Branch: `main`, Folder: `/docs` (or root)
4. Click **Save**

The website files in this folder go into the `/docs` folder of the repository:

```bash
mkdir docs
cp index.html docs/
cp _config.yml docs/
git add docs/
git commit -m "docs: add VERIFIQ product website"
git push
```

Your site will be live at: **https://bbmw96.github.io/verifiq**

## Step 5 — Custom Domain (bbmw0.com/verifiq)

In GitHub Pages settings, add custom domain: `bbmw0.com`

Then in your DNS provider, add:
```
CNAME  www  bbmw96.github.io
A      @    185.199.108.153
A      @    185.199.109.153
A      @    185.199.110.153
A      @    185.199.111.153
```

## Licence Keys Summary

| Tier | Keys | Range |
|---|---|---|
| Trial | 1 | VRFQ-TRIAL-DEMO0-0000-00000001 |
| Individual | 250 | VRFQ-IND1-0001 to 0250 |
| Practice | 250 | VRFQ-PRAC-0251 to 0500 |
| Enterprise | 250 | VRFQ-ENT1-0501 to 0750 |
| Site Licence | 251 | VRFQ-ENTX-0751 to 1001 |

All 1,001 keys are embedded in `VERIFIQ.Security/LicenceValidator.cs`.
