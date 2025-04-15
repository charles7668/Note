# Ubuntu Manual Upgrade

Sometimes, Ubuntu's upgrade tools cannot be used when the version is too old, so a manual upgrade is required.

## 1. Download the Target Version Upgrade Tool (Recommended: Upgrade Version by Version)

Download it from:  
https://changelogs.ubuntu.com/meta-release

## 2. Run the Upgrade Script

The script name corresponds to the Ubuntu version (e.g., `focal`, `bionic`).

## 3. Optional (If the Release File Cannot Be Found)

Edit the `/etc/apt/sources.list` file:

- Replace `archive.ubuntu.com` with `old-releases.ubuntu.com`
- Replace `security.ubuntu.com` with `old-releases.ubuntu.com`
