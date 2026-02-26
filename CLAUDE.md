# appcraft-tools — Claude Code Plugin Marketplace

## What This Is

appcraft-tools is a Claude Code plugin marketplace for Apple developers. It is a catalog repo — it contains no plugin code, only `.claude-plugin/marketplace.json` which references plugins hosted in their own GitHub repos.

## Repository Structure

```
.claude-plugin/marketplace.json   — marketplace catalog (the only essential file)
README.md                         — user-facing install instructions
CLAUDE.md                         — this file (agent context)
```

## How It Works

- Users add the marketplace: `/plugin marketplace add vishalvshekkar/appcraft-tools`
- Users install plugins by name: `/plugin install app-store-toolkit@appcraft-tools`
- Claude Code clones this repo to read the catalog, then fetches each plugin from its own GitHub repo

## Current Plugins

| Plugin | Repo | Description |
|--------|------|-------------|
| app-store-toolkit | `vishalvshekkar/app-store-toolkit` | AI-powered App Store Connect metadata management |

## Adding a New Plugin

Add an entry to the `plugins` array in `.claude-plugin/marketplace.json`:

```json
{
  "name": "new-plugin-name",
  "source": {
    "source": "github",
    "repo": "vishalvshekkar/new-plugin-repo"
  },
  "description": "What it does",
  "version": "0.1.0",
  "author": { "name": "Vishal V. Shekkar" },
  "homepage": "https://github.com/vishalvshekkar/new-plugin-repo",
  "repository": "https://github.com/vishalvshekkar/new-plugin-repo",
  "license": "MIT",
  "keywords": ["relevant", "tags"],
  "category": "developer-tools"
}
```

## Key Rules

### Version Authority
- The plugin's own `plugin.json` is the authority for version, not the version in this marketplace entry
- Keep marketplace version in sync with plugin version for clarity, but `plugin.json` always wins silently
- If two refs/commits have the same manifest version, Claude Code skips the update

### Source Types
All plugins use GitHub sources: `{"source": "github", "repo": "owner/repo"}`
- Can pin to a branch/tag with `"ref": "v1.0.0"`
- Can pin to exact commit with `"sha": "full-40-char-sha"`
- Without ref/sha, defaults to the repo's default branch

### Marketplace Schema
- `name`: marketplace identifier (kebab-case) — users see this in install commands
- `owner`: maintainer info (name, email)
- `metadata.description`: brief marketplace description
- `plugins[]`: array of plugin entries with `name` and `source` required

### What NOT to Put Here
- No plugin code — each plugin lives in its own repo
- No `.appstore/` directories — those are created in user projects by the plugins
- No credentials or secrets
