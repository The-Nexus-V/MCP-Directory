# PowerHub MCP Directory

The official MCP (Model Context Protocol) server directory for **PowerHub Store** in Nexus-V.

This repository serves as the central registry for MCP servers that can be installed and managed through the PowerHub Store interface.

## 📦 Structure

```
MCP-Directory/
├── registry.json          # Main registry file with all MCP servers
├── servers/               # Individual server configuration files
│   ├── github.json
│   ├── notion.json
│   └── ...
├── [server-name]/         # Legacy server directories (for icons/assets)
│   ├── server.json
│   ├── icon.svg
│   └── README.md
└── README.md
```

## 🚀 How the PowerHub Store Works

The Nexus-V app automatically fetches MCP servers from this repository:

1. **Primary Source**: `registry.json` - Contains the full list of available MCP servers
2. **Secondary Source**: `servers/` directory - Individual JSON files for each server
3. **Fallback**: Built-in sample servers if network is unavailable

The app refreshes the registry periodically and caches the data locally for offline access.

---

## 📝 Adding a New MCP Server

### Option 1: Add to registry.json (Recommended)

Add your server entry to the `servers` array in `registry.json`:

```json
{
  "id": "mcp-server-your-service",
  "packageName": "your-package-name",
  "name": "Your Service Name",
  "description": "Short description of your MCP server",
  "longDescription": "Detailed description with features...",
  "author": {
    "name": "Author Name",
    "url": "https://your-website.com",
    "verified": false
  },
  "version": "1.0.0",
  "versions": [
    { "version": "1.0.0", "releaseDate": "2024-01-01", "minProtocolVersion": "2024-11-05" }
  ],
  "category": "api-integration",
  "tags": ["tag1", "tag2", "tag3"],
  "repositoryUrl": "https://github.com/your/repo",
  "license": "MIT",
  "installSource": "npm",
  "installCommand": "@your-org/mcp-server",
  "transportType": "stdio",
  "permissions": [],
  "capabilities": {
    "tools": { "listChanged": true }
  },
  "tools": [],
  "resources": [],
  "prompts": [],
  "requiredEnvVars": [],
  "optionalEnvVars": [],
  "minProtocolVersion": "2024-11-05",
  "downloads": 0,
  "rating": 0,
  "ratingCount": 0,
  "reviews": [],
  "lastUpdated": "2024-01-01T00:00:00Z",
  "createdAt": "2024-01-01T00:00:00Z",
  "isVerified": false,
  "isFeatured": false
}
```

### Option 2: Create Individual Server File

Create a new JSON file in the `servers/` directory:

```bash
servers/your-service.json
```

---

## 📋 Server Configuration Schema

### Required Fields

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Unique identifier (e.g., `mcp-server-github`) |
| `packageName` | string | NPM package name or Docker image |
| `name` | string | Display name |
| `description` | string | Short description (max 150 chars) |
| `author` | object | Author information |
| `version` | string | Current version (semver) |
| `versions` | array | Version history |
| `category` | string | Server category |
| `tags` | array | Search tags |
| `license` | string | License identifier |
| `installSource` | string | `npm`, `docker`, `url`, or `git` |
| `installCommand` | string | Installation command/URL |
| `transportType` | string | `stdio`, `http`, or `streamable-http` |
| `minProtocolVersion` | string | Minimum MCP protocol version |
| `downloads` | number | Download count |
| `rating` | number | Average rating (0-5) |
| `ratingCount` | number | Number of ratings |
| `lastUpdated` | string | ISO 8601 timestamp |
| `createdAt` | string | ISO 8601 timestamp |
| `isVerified` | boolean | Verified by maintainers |
| `isFeatured` | boolean | Featured in store |

### Optional Fields

| Field | Type | Description |
|-------|------|-------------|
| `longDescription` | string | Detailed description (markdown supported) |
| `repositoryUrl` | string | Source code repository |
| `homepageUrl` | string | Project homepage |
| `documentationUrl` | string | Documentation link |
| `permissions` | array | Required permissions |
| `capabilities` | object | Server capabilities |
| `tools` | array | Available tools |
| `resources` | array | Available resources |
| `prompts` | array | Available prompts |
| `requiredEnvVars` | array | Required environment variables |
| `optionalEnvVars` | array | Optional environment variables |
| `reviews` | array | User reviews |
| `screenshots` | array | Screenshot URLs |
| `securityWarnings` | array | Security warnings |
| `dependencies` | array | Dependencies |

---

## 🏷️ Categories

Use one of these categories:

| Category | Description |
|----------|-------------|
| `file-system` | File and storage operations |
| `database` | Database integrations |
| `api-integration` | Third-party API integrations |
| `development` | Development tools |
| `productivity` | Productivity tools |
| `communication` | Messaging and communication |
| `ai-ml` | AI/ML tools |
| `security` | Security tools |
| `monitoring` | Monitoring and observability |
| `data-processing` | Data processing tools |
| `cloud-services` | Cloud platform integrations |
| `version-control` | Version control systems |
| `documentation` | Documentation tools |
| `testing` | Testing frameworks |
| `other` | Other tools |

---

## 🔧 Environment Variables

Define required and optional environment variables:

```json
{
  "requiredEnvVars": [
    {
      "name": "API_KEY",
      "description": "Your API key for authentication",
      "isSecret": true,
      "example": "sk-xxxxxxxxxxxx"
    }
  ],
  "optionalEnvVars": [
    {
      "name": "API_BASE_URL",
      "description": "Custom API base URL",
      "defaultValue": "https://api.example.com"
    }
  ]
}
```

---

## 🛠️ Tools Definition

Define the tools your server provides:

```json
{
  "tools": [
    {
      "name": "tool_name",
      "description": "What this tool does",
      "isReadOnly": true,
      "isDestructive": false
    }
  ]
}
```

- `isReadOnly`: Tool only reads data, doesn't modify anything
- `isDestructive`: Tool can delete or permanently modify data

---

## 🔒 Permissions

Define required permissions:

```json
{
  "permissions": [
    {
      "type": "read",
      "scope": "resource-name",
      "description": "What this permission allows",
      "required": true,
      "warning": "Optional security warning"
    }
  ]
}
```

Permission types: `read`, `write`, `execute`, `admin`

---

## ✅ Submission Checklist

Before submitting a PR:

- [ ] Unique `id` that doesn't conflict with existing servers
- [ ] Valid `packageName` that can be installed
- [ ] Clear and concise `description`
- [ ] Correct `category` from the list above
- [ ] At least 3 relevant `tags`
- [ ] Valid `transportType` (`stdio`, `http`, or `streamable-http`)
- [ ] All `requiredEnvVars` documented with descriptions
- [ ] All `tools` listed with descriptions
- [ ] Valid `license` identifier
- [ ] `repositoryUrl` points to accessible repository
- [ ] Tested installation and basic functionality

---

## 🔄 Updating an Existing Server

1. Update the version number
2. Add new version to `versions` array
3. Update `lastUpdated` timestamp
4. Update any changed fields (tools, env vars, etc.)

---

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/The-Nexus-V/MCP-Directory/issues)
- **Discussions**: [GitHub Discussions](https://github.com/The-Nexus-V/MCP-Directory/discussions)

---

## 📄 License

This directory is licensed under MIT. Individual MCP servers may have their own licenses.
