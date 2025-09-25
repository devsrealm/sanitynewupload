# Sanitybase Release Management

This repository includes an automated workflow that manages releases with tags ending in "sanitybase".

## How it works

### Workflow Trigger
- The workflow runs automatically when a new GitHub release is published
- Only processes releases where the tag name ends with "sanitybase" (e.g., `v2.0.47-sanitybase`)

### What it does
1. **Checks the tag**: Only processes releases with tags ending in "sanitybase"
2. **Extracts release data**: Collects tag name, publication date, and all asset download URLs
3. **Updates JSON file**: Maintains `sanitybase-release.json` with the latest 5 releases
4. **Commits changes**: Automatically commits the updated JSON file back to the repository

### JSON File Structure

The `sanitybase-release.json` file contains an array of release objects, ordered from newest to oldest:

```json
[
  {
    "tag": "v2.0.47-sanitybase",
    "published_at": "2025-09-25T02:22:04Z",
    "download_urls": [
      {
        "name": "sanitybase.zip",
        "url": "https://github.com/devsrealm/sanitynewupload/releases/download/v2.0.47-sanitybase/sanitybase.zip",
        "size": 1986937
      }
    ]
  }
]
```

### Key Features
- **5-Release Limit**: Only keeps the 5 most recent sanitybase releases
- **No Duplicates**: Removes any existing entry for the same tag before adding the new one
- **All Assets**: Captures all release assets (zip files, etc.) with their download URLs
- **Automatic Updates**: Runs without manual intervention on every qualifying release

## Manual Usage

If you need to manually check which releases will be tracked, look for releases with tags ending in "sanitybase":

```bash
git tag -l "*sanitybase"
```

The workflow file is located at `.github/workflows/sanitybase-releases.yml`.