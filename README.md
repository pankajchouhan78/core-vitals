## Core Vitals – Git LFS Usage and Cloning Guide

A lightweight guide for contributors and users of this repository to correctly install, clone, and work with large files stored via Git LFS.

### What is Git LFS?
Git LFS (Large File Storage) is an extension for Git that stores large files (such as ZIPs, media, datasets) outside of your normal Git history and replaces them with small pointer files. This keeps the repository fast and under GitHub’s normal size limits while still allowing you to version large assets.

### Why do we use Git LFS in this repo?
This project includes large ZIP archives that exceed normal Git size best practices. They are tracked via Git LFS so cloning and pulling stays reliable and fast:
- `core-vitals-backend.zip`
- `core-vitals-fronted.zip`

If you clone without Git LFS (or don’t run the LFS fetch step), you may see small text “pointer” files instead of the actual ZIPs.

---

## Setup

### Prerequisites
- Git installed
- Internet access to GitHub and Git LFS endpoints

### Install Git LFS
- Download from the official site: `https://git-lfs.github.com/`

Or install via package managers:
- macOS (Homebrew):
```bash
brew install git-lfs
```
- Ubuntu / Debian:
```bash
curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash
sudo apt install git-lfs
```
- Windows (one of the following):
  - Download the installer from `https://git-lfs.github.com/` and run it
  - Or via winget: `winget install Git.GitLFS`
  - Or via Chocolatey: `choco install git-lfs`

Then initialize LFS (run once per machine):
```bash
git lfs install
```

---

## Cloning This Repository (with LFS files)
```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
# fetch actual large files stored in LFS
git lfs pull
```
- `git lfs pull` downloads the actual ZIPs from GitHub’s LFS storage.

### If You Already Cloned Without LFS
If you see small text pointer files instead of real ZIPs:
```bash
# install LFS if not already installed
git lfs install
# from inside the repository root
git lfs pull
```

---

## Adding New Large Files (for contributors)
If you need to add new `.zip` (or other large) files, track them with LFS before committing:
```bash
git lfs track "*.zip"
git add .gitattributes

git add your-large-file.zip
git commit -m "Add large file using Git LFS"
git push
```
Notes:
- `git lfs track` writes patterns to `.gitattributes`. Commit that file.
- Only patterns listed in `.gitattributes` will be stored via LFS on subsequent adds/commits.

---

## Verifying LFS
- See which patterns are tracked by LFS:
```bash
git lfs track
```
- See which files are currently managed by LFS:
```bash
git lfs ls-files
```

---

## GitHub LFS Limits (Free Tier)
- 1 GB total LFS storage
- 1 GB/month LFS bandwidth (downloads/uploads)
If you exceed these, you may need to purchase additional LFS data packs or optimize asset sizes.

---

## Quick Reference

| Task | Command(s) |
|---|---|
| Clone with LFS | `git clone … && cd … && git lfs pull` |
| Install Git LFS | `git lfs install` (after OS-specific install) |
| Track large files | `git lfs track "*.zip" && git add .gitattributes` |
| See tracked patterns | `git lfs track` |
| See LFS-managed files | `git lfs ls-files` |
| Download missing LFS files | `git lfs pull` |

---

## Troubleshooting
- Pointer file instead of real ZIP: Make sure Git LFS is installed and run `git lfs pull` in the repo root.
- New files not stored in LFS: Confirm the pattern is in `.gitattributes` via `git lfs track` and add/commit again.
- Auth or permission issues: Ensure you can authenticate to GitHub for this repo (SSH or HTTPS); try `git lfs env` for diagnostics.
- Corporate proxies/firewalls: Allow Git LFS endpoints and Git over HTTPS.

---

If you want this guide in Hindi, as a PDF, or embedded into another repo’s `README.md`, open an issue or request and we’ll generate it.