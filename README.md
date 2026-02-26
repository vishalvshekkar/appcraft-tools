# appcraft-tools

A Claude Code plugin marketplace for Apple developers.

## Available Plugins

| Plugin | Description |
|--------|-------------|
| [app-store-toolkit](https://github.com/vishalvshekkar/app-store-toolkit) | AI-powered App Store Connect metadata management — ASO copywriting, changelogs, localization, and two-way sync |

## Installation

```bash
# Add the marketplace
/plugin marketplace add vishalvshekkar/appcraft-tools

# Install a plugin
/plugin install app-store-toolkit@appcraft-tools
```

## Adding Plugins

To add a new plugin to this marketplace, add an entry to `.claude-plugin/marketplace.json`:

```json
{
  "name": "your-plugin-name",
  "source": {
    "source": "github",
    "repo": "vishalvshekkar/your-plugin-repo"
  },
  "description": "What your plugin does"
}
```

## License

MIT
