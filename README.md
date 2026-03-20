# CodeQR Plugin

Official [CodeQR](https://codeqr.io) plugin for Claude Code and AI agents. Create short links, generate QR codes, track analytics, and manage domains directly from your AI workflow.

## Installation

### Claude Code

```bash
claude plugin install codeqr
```

Or install from the repository directly:

```bash
claude plugin install --from https://github.com/codeqr-io/codeqr-plugin
```

### Manual Setup

1. Clone this repository
2. Set your API key: `export CODEQR_API_KEY=your_key_here`
3. Load the plugin: `claude --plugin-dir ./codeqr-plugin`

## Setup

You need a CodeQR API key. Get one at [app.codeqr.io/settings/tokens](https://app.codeqr.io/settings/tokens).

Set it as an environment variable:

```bash
export CODEQR_API_KEY=your_api_key_here
```

## Usage

### Slash Command

```
/codeqr shorten https://example.com/my-long-url
/codeqr create qr code for https://example.com
/codeqr show analytics for last 7 days
```

### Natural Language (via Skills)

The plugin's skills are automatically triggered by context. Just ask Claude naturally:

- "Shorten this URL: https://example.com/very-long-path"
- "Create a QR code for my website"
- "How many clicks did my links get this week?"
- "List all my short links"
- "Add a custom domain link.mysite.com"

## Skills

| Skill | Description |
|-------|-------------|
| `create-link` | Create shortened links with custom slugs, domains, tags, and expiration |
| `create-qrcode` | Generate QR codes with custom colors and sizes |
| `analytics` | Query click analytics by country, device, browser, referrer, and more |
| `manage-links` | List, update, delete, and search existing links |
| `manage-domains` | Add, configure, and manage custom domains |
| `manage-tags` | Create and organize tags for link categorization |
| `track-conversions` | Track leads and sales attributed to your links |

## MCP Server

This plugin bundles the [`@codeqr/ts-mcp`](https://www.npmjs.com/package/@codeqr/ts-mcp) server, which provides two MCP tools:

- **`execute`** — Run TypeScript code against the CodeQR API with a pre-authenticated client
- **`search_docs`** — Search SDK documentation for methods, parameters, and examples

## Cross-Platform Compatibility

The skills in this plugin follow the [Agent Skills](https://agentskills.io) open standard and are compatible with:

- **Claude Code** — Full plugin support with MCP server
- **VS Code Copilot** — Via Agent Skills
- **OpenAI Codex** — Via Agent Skills
- **Cursor** — Via Agent Skills

## API Resources

The CodeQR API provides:

- **Links** — Create, update, list, delete, and bulk create short links
- **QR Codes** — Create, update, list, delete, and bulk create QR codes
- **Analytics** — Click analytics with grouping by country, device, browser, OS, referrer
- **Events** — Event log for your workspace
- **Domains** — Custom domain management
- **Tags** — Link organization with tags
- **Track** — Lead and sale conversion tracking
- **Projects** — Workspace project management

## Development

```bash
# Test the plugin locally
claude --plugin-dir ./codeqr-plugin

# Reload after changes
/reload-plugins
```

## License

MIT - [CodeQR](https://codeqr.io)
