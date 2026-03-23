# Claude Builds Blueprints

A Claude skill for generating [WordPress Playground](https://playground.wordpress.net) Blueprint JSON files — automatically, intelligently, and correctly.

## What is a Blueprint?

A Blueprint is a JSON file that configures a WordPress Playground instance in seconds. It can install plugins and themes, set up demo content, configure site options, run PHP/WP-CLI commands, and navigate the user to the perfect starting page — all without any local setup.

```json
{
  "$schema": "https://playground.wordpress.net/blueprint-schema.json",
  "landingPage": "/wp-admin/",
  "login": true,
  "preferredVersions": { "php": "8.3", "wp": "latest" },
  "steps": [
    {
      "step": "installPlugin",
      "pluginData": { "resource": "wordpress.org/plugins", "slug": "gutenberg" },
      "options": { "activate": true }
    }
  ]
}
```

## What This Skill Does

The `blueprint-builder` Claude agent:

1. **Discovers your project** — scans for plugins, themes, and blocks in the current directory
2. **Asks smart questions** — only asks what it needs to know based on what it found
3. **Generates a valid Blueprint** — with correct structure, ordering, and resource references
4. **Provides a ready-to-use URL** — encoded playground.wordpress.net link

## Getting Started

### Use in Claude Code

The agent lives at `.claude/agents/blueprint-builder.md`. When invoked, it will:

1. Explore the current working directory for plugins, themes, and block.json files
2. Ask targeted questions based on what it discovers
3. Generate a complete, valid Blueprint JSON
4. Provide a shareable playground.wordpress.net URL

### Example Prompts

- "Create a Blueprint for my block plugin so I can share a demo link"
- "Set up a Playground with WooCommerce and some demo products"
- "Build a Blueprint that opens the site editor with my theme's starter content"
- "Generate a Blueprint for testing my plugin against WordPress 6.5 and PHP 8.0"
- "Create a full dev environment Blueprint with WP_DEBUG enabled"

## Examples

See the [`examples/`](./examples/) directory for ready-to-use Blueprints:

| File | Description |
|------|-------------|
| [plugin-demo.json](./examples/plugin-demo.json) | Demo a plugin from WordPress.org |
| [block-editor-demo.json](./examples/block-editor-demo.json) | Block editor with a custom block plugin |
| [theme-showcase.json](./examples/theme-showcase.json) | Showcase a theme with starter content |
| [dev-environment.json](./examples/dev-environment.json) | Full dev environment with WP_DEBUG |

## Blueprint API Reference

| Property | Description |
|----------|-------------|
| `$schema` | Validation schema URL |
| `landingPage` | Where to navigate after setup |
| `login` | Auto-login (`true` or `{username, password}`) |
| `preferredVersions` | PHP and WordPress version targets |
| `features.networking` | Enable HTTP requests |
| `siteOptions` | Set WordPress options |
| `steps` | Array of setup steps |

### Key Steps

| Step | What it does |
|------|-------------|
| `installPlugin` | Install plugin from WordPress.org or URL |
| `installTheme` | Install theme from WordPress.org or URL |
| `activatePlugin` | Activate an installed plugin |
| `activateTheme` | Activate an installed theme |
| `login` | Log in as a user |
| `importWxr` | Import demo content from XML |
| `setSiteOptions` | Set WordPress options |
| `defineWpConfigConsts` | Define wp-config.php constants |
| `runPHP` | Execute PHP code |
| `wp-cli` | Run WP-CLI commands |
| `writeFile` / `writeFiles` | Write files to the filesystem |
| `importThemeStarterContent` | Load theme starter content |

## Documentation Links

- [Blueprints Overview](https://wordpress.github.io/wordpress-playground/blueprints/)
- [Getting Started](https://wordpress.github.io/wordpress-playground/blueprints/getting-started)
- [All Steps Reference](https://wordpress.github.io/wordpress-playground/blueprints/steps)
- [Data Format](https://wordpress.github.io/wordpress-playground/blueprints/data-format)
- [Blueprint Gallery](https://github.com/WordPress/blueprints/blob/trunk/GALLERY.md)
- [JSON Schema](https://playground.wordpress.net/blueprint-schema.json)
- [API Reference](https://wordpress.github.io/wordpress-playground/api/blueprints)

## License

GPL-2.0-or-later
