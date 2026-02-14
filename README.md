# MCP Model Card Generator

Generate standardized documentation for Model Context Protocol (MCP) servers.

## 🚀 Quick Start
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/16sWdvROQ4GoP7-IixtCcjx9PSvEsSj8n?usp=sharing)

**Click the badge above to start generating your model card!**
## ✨ Features

- Interactive form-based interface
- Generates **both** JSON (machine-readable) and Markdown (human-readable)
- Follows [MCP Model Card Specification v1.0](MCP_Model_Card_Specification_v1_0.md)
- Complete [User Guide](MCP_Model_Card_Generator_USER_GUIDE.md) with examples
- Example: [Brave Search MCP Server Model Card](brave-search-mcp-server-model-card.md)

## 📖 Documentation

- **[User Guide](MCP_Model_Card_Generator_USER_GUIDE.md)** - Complete tutorial explaining every field
- **[Specification](MCP_Model_Card_Specification_v1_0.md)** - Technical specification
- **[Example](brave-search-mcp-server-model-card.md)** - Real model card example

## 💙 Credits

*Part of the W3C AI-KR Community Group's work on AI agent interoperability and transparency.*


# MCP Model Card Generator - Complete User Guide and MCP tutorial

**Version**: 1.0.0  
**Concept**: Paola Di Maio, W3C AI-KR CG Chair  
**Notebook by**: Claude (Anthropic)

---

## Table of Contents

1. [What is a Model Card?](#what-is-a-model-card)
2. [Before You Start](#before-you-start)
3. [Section-by-Section Guide](#section-by-section-guide)
4. [Common Questions](#common-questions)
5. [Examples](#examples)
6. [Tips for Success](#tips-for-success)

---

## What is a Model Card?

A **Model Card** is standardized documentation that describes what your MCP server does, how it works, and how to use it safely. Think of it like a "nutrition label" for your server - it tells users exactly what they're getting.

**Why create one?**
- Makes your server discoverable
- Helps users understand capabilities and limitations
- Enables automated compatibility checking
- Builds trust through transparency
- Required for many MCP registries

---

## Before You Start

**What you'll need:**
1. Your MCP server code (or access to its documentation)
2. Knowledge of what tools your server exposes
3. Security/authentication requirements
4. 15-30 minutes of time

**Helpful to have:**
- Your server's GitHub repository URL
- List of environment variables needed
- Performance benchmarks (if available)
- Test coverage statistics (if available)

---

## Section-by-Section Guide

---

### 📝 SECTION 1: Server Metadata

This section identifies your server and provides basic information.

#### **Server Name** (REQUIRED)
- **What it is**: The official name of your MCP server
- **Format**: Plain text, descriptive
- **Examples**: 
  - ✅ "GitHub MCP Server"
  - ✅ "Brave Search MCP Server"
  - ✅ "PostgreSQL Database MCP Server"
  - ❌ "my-server" (too vague)
  - ❌ "Server123" (not descriptive)

#### **Version** (REQUIRED)
- **What it is**: Your server's version number
- **Format**: Semantic versioning (major.minor.patch)
- **Examples**:
  - ✅ "1.0.0" (first stable release)
  - ✅ "2.3.1" (version 2, update 3, patch 1)
  - ✅ "0.9.0-beta" (pre-release)
  - ❌ "version 1" (not proper format)
  - ❌ "latest" (not specific)

#### **Description** (REQUIRED)
- **What it is**: A brief summary of what your server does
- **Format**: 10-500 characters, one or two sentences
- **What to include**: Main purpose, key features
- **Examples**:
  - ✅ "MCP server for GitHub API integration, providing repository management, issue tracking, and pull request operations"
  - ✅ "Secure file operations server with configurable access controls and directory restrictions"
  - ❌ "A server" (too vague)
  - ❌ [500+ word essay] (too long)

#### **MCP Protocol Version** (REQUIRED)
- **What it is**: Which version of the MCP specification your server implements
- **Format**: Select from dropdown
- **Options**:
  - `2025-11-25` - Latest stable (recommended for new servers)
  - `2025-06-18` - Stable
  - `2024-11-05` - Legacy
  - `other` - If using a different version
- **How to know**: Check your server's package.json or documentation

#### **Author** (OPTIONAL)
- **What it is**: Your name or username
- **Format**: Plain text
- **Examples**:
  - ✅ "John Smith"
  - ✅ "jane-dev"
  - ✅ "AI Research Team"

#### **Organization** (OPTIONAL)
- **What it is**: Company or group that created the server
- **Format**: Plain text
- **Examples**:
  - ✅ "Anthropic"
  - ✅ "Mozilla Foundation"
  - ✅ "OpenAI"
  - Leave blank if individual developer

#### **License** (REQUIRED)
- **What it is**: The software license for your server
- **Format**: Standard license identifier
- **Common options**:
  - `MIT` - Very permissive, most common
  - `Apache-2.0` - Permissive with patent protection
  - `GPL-3.0` - Copyleft, requires derivative works to be open source
  - `BSD-3-Clause` - Permissive with attribution
  - `Proprietary` - Closed source
- **How to know**: Check your LICENSE file or GitHub repository

#### **Repository URL** (OPTIONAL)
- **What it is**: Link to your server's source code
- **Format**: Full URL starting with https://
- **Examples**:
  - ✅ "https://github.com/username/mcp-server"
  - ✅ "https://gitlab.com/org/mcp-server"
  - Leave blank if closed source

#### **Language** (REQUIRED)
- **What it is**: Primary programming language
- **Options**:
  - `typescript` - TypeScript/JavaScript
  - `python` - Python
  - `javascript` - Plain JavaScript
  - `java` - Java
  - `other` - Other languages

#### **Transports** (REQUIRED)
- **What it is**: Communication methods your server supports
- **Format**: Select all that apply
- **Options**:
  - `stdio` - Standard input/output (most common)
  - `http+sse` - HTTP with Server-Sent Events
- **How to know**: Check your server's configuration or startup code

#### **Tags** (OPTIONAL)
- **What it is**: Keywords to help people find your server
- **Format**: Comma-separated words (lowercase, no spaces in individual tags)
- **Examples**:
  - ✅ "github, api, version-control, developer-tools"
  - ✅ "database, postgresql, sql"
  - ✅ "search, brave, web-search"
  - ❌ "GitHub API" (use github,api instead)

---

### 🔧 SECTION 2: Tools Documentation

This section documents each tool (function) your server exposes.

**You'll add one entry for EACH tool your server provides.**

#### **Tool Name** (REQUIRED)
- **What it is**: The exact function name clients will call
- **Format**: `service_action_resource` (all lowercase, underscores)
- **Examples**:
  - ✅ `github_list_repositories`
  - ✅ `slack_send_message`
  - ✅ `postgres_execute_query`
  - ❌ `listRepos` (wrong format - camelCase)
  - ❌ `get_data` (too generic)
  - ❌ `tool1` (not descriptive)
- **Why this matters**: MCP naming convention for consistency

#### **Tool Description** (REQUIRED)
- **What it is**: What this specific tool does
- **Format**: One or two clear sentences
- **Examples**:
  - ✅ "Lists all repositories for the authenticated user or specified organization"
  - ✅ "Sends a message to a specified Slack channel"
  - ✅ "Executes a read-only SQL query against the database"
  - ❌ "Gets stuff" (too vague)

#### **Input Schema** (REQUIRED)
- **What it is**: JSON Schema defining what parameters this tool accepts
- **Format**: Valid JSON Schema (paste into the text box)
- **Minimum structure**:
```json
{
  "type": "object",
  "properties": {},
  "required": []
}
```
- **Example with parameters**:
```json
{
  "type": "object",
  "properties": {
    "username": {
      "type": "string",
      "description": "GitHub username"
    },
    "limit": {
      "type": "number",
      "minimum": 1,
      "maximum": 100,
      "default": 10,
      "description": "Number of results to return"
    },
    "include_private": {
      "type": "boolean",
      "default": false,
      "description": "Include private repositories"
    }
  },
  "required": ["username"]
}
```

**Common property types**:
- `"type": "string"` - Text
- `"type": "number"` - Numeric value
- `"type": "boolean"` - True/false
- `"type": "array"` - List of items
- `"type": "object"` - Nested structure

**Common constraints**:
- `"minimum": 1` - Minimum value for numbers
- `"maximum": 100` - Maximum value for numbers
- `"minLength": 1` - Minimum string length
- `"maxLength": 500` - Maximum string length
- `"enum": ["option1", "option2"]` - List of allowed values
- `"default": value` - Default if not provided

#### **Output Schema** (REQUIRED)
- **What it is**: JSON Schema defining what this tool returns
- **Format**: Valid JSON Schema
- **Example**:
```json
{
  "type": "object",
  "properties": {
    "repositories": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "name": {"type": "string"},
          "url": {"type": "string"},
          "stars": {"type": "number"}
        }
      }
    },
    "total_count": {
      "type": "number"
    }
  }
}
```

#### **⚠️ Destructive Operation** (REQUIRED - Checkbox)
- **What it is**: Does this tool delete, modify, or change data?
- **When to check**: If the tool:
  - Deletes files, records, or resources
  - Modifies existing data
  - Creates irreversible changes
  - Executes system commands
- **Examples**:
  - ✅ CHECK: `github_delete_repository`
  - ✅ CHECK: `file_write_content`
  - ✅ CHECK: `database_drop_table`
  - ❌ UNCHECK: `github_list_repositories` (read-only)
  - ❌ UNCHECK: `slack_read_messages` (read-only)

#### **Read-only Operation** (REQUIRED - Checkbox)
- **What it is**: Does this tool only read/retrieve data without changing anything?
- **When to check**: If the tool ONLY:
  - Fetches/retrieves information
  - Searches or queries
  - Lists or displays data
- **Examples**:
  - ✅ CHECK: `database_select_query`
  - ✅ CHECK: `github_get_repository_info`
  - ❌ UNCHECK: `github_create_issue` (creates data)

#### **Async Operation** (REQUIRED - Checkbox)
- **What it is**: Does this tool run asynchronously (may take time)?
- **When to check**: If the tool:
  - Makes network requests
  - Performs I/O operations
  - May take more than instant response time
- **Most tools should check this unless they're purely computational**

**After filling all fields for one tool, click "➕ Add Tool"**

**Repeat for EVERY tool your server provides!**

---

### ⚡ SECTION 3: Operational Characteristics

This section describes how your server performs.

#### **Average Response Time (ms)** (REQUIRED)
- **What it is**: Typical time for your server to respond
- **Format**: Number in milliseconds
- **How to know**: 
  - Run benchmarks on your server
  - Or estimate based on what the server does
- **Typical values**:
  - `50-100ms` - Very fast (local operations, cache lookups)
  - `100-500ms` - Fast (database queries, simple API calls)
  - `500-2000ms` - Moderate (complex operations, external APIs)
  - `2000+ms` - Slow (heavy processing, multiple API calls)
- **Examples**:
  - ✅ `150` (for a database server)
  - ✅ `300` (for an API integration)
  - ✅ `1000` (for complex operations)

#### **Rate Limit - Per Minute** (REQUIRED)
- **What it is**: Maximum requests allowed per minute
- **Format**: Number
- **How to know**:
  - Check if you're using an external API (use their limits)
  - Set your own limits based on server capacity
- **Typical values**:
  - `60` - 1 per second
  - `300` - 5 per second
  - `1000` - ~16 per second
  - `5000` - High throughput
- **Examples**:
  - ✅ `60` (GitHub API free tier)
  - ✅ `1000` (self-hosted server)

#### **Rate Limit - Per Hour** (REQUIRED)
- **What it is**: Maximum requests allowed per hour
- **Format**: Number
- **Typical values**:
  - `2000` - Free tier APIs
  - `5000` - Basic tier
  - `50000` - Premium tier
  - `unlimited` - Use `999999` if no limit

#### **Known Limitations** (REQUIRED)
- **What it is**: Things your server CAN'T do or restrictions it has
- **Format**: One limitation per line
- **What to include**:
  - API tier limitations
  - Missing features
  - Size/count restrictions
  - Compatibility issues
- **Examples**:
```
Free tier limited to 2,000 queries per month
Maximum 100 results per search
Does not support wildcard searches
Requires PostgreSQL 12 or higher
Cannot access private repositories without token
Large file uploads (>10MB) not supported
```

---

### 🔒 SECTION 4: Security Profile

This section describes security and authentication.

#### **Authentication Methods** (REQUIRED)
- **What it is**: How users prove their identity
- **Format**: Select all that apply
- **Options**:
  - `oauth2` - OAuth 2.0 flow
  - `api_key` - API keys/tokens
  - `personal_access_token` - User-generated tokens
  - `none` - No authentication required
- **Examples**:
  - GitHub server: `oauth2`, `personal_access_token`
  - Brave Search: `api_key`
  - Local filesystem: `none`

#### **Required Scopes** (OPTIONAL)
- **What it is**: OAuth scopes or permissions needed
- **Format**: Comma-separated list
- **Only relevant if using OAuth2**
- **Examples**:
  - ✅ "repo, user, admin:org" (GitHub)
  - ✅ "drive.readonly, calendar.events" (Google)
  - Leave blank if using API keys

#### **Credential Storage** (REQUIRED)
- **What it is**: Where/how credentials are stored
- **Format**: Select from dropdown
- **Options**:
  - `environment_variables` - Most common and recommended
  - `secure_vault` - Using a secrets manager
  - `config_file` - In configuration files (less secure)
  - `other` - Other methods
- **Best practice**: Use environment_variables

#### **Data Retention Policy** (REQUIRED)
- **What it is**: How long you keep user data
- **Format**: Clear statement in plain text
- **Examples**:
  - ✅ "No data retained; acts as stateless proxy"
  - ✅ "Query logs retained for 7 days, then deleted"
  - ✅ "User preferences stored indefinitely until account deletion"
  - ✅ "Session data cached for 1 hour, then cleared"

#### **Data Encrypted in Transit** (REQUIRED - Checkbox)
- **What it is**: Is data encrypted when transmitted?
- **When to check**: 
  - ✅ CHECK if using HTTPS/TLS
  - ✅ CHECK if all external APIs use HTTPS
  - ❌ UNCHECK if using plain HTTP (not recommended!)

#### **PII Handling** (REQUIRED)
- **What it is**: How you handle Personally Identifiable Information
- **Format**: Clear statement
- **Examples**:
  - ✅ "Server does not access or store PII"
  - ✅ "PII is encrypted at rest and in transit; deleted after 30 days"
  - ✅ "Email addresses stored with user consent; never shared with third parties"
  - ✅ "N/A - server does not process personal information"

#### **Security Considerations** (REQUIRED)
- **What it is**: Security warnings or risks users should know
- **Format**: One consideration per line
- **Examples**:
```
API keys must be kept secure and never committed to version control
Server has access to all files in configured directories
Destructive operations cannot be undone
Rate limiting enforced by external API
Requires network access to api.github.com
```

#### **Security Best Practices** (REQUIRED)
- **What it is**: Recommendations for secure usage
- **Format**: One practice per line
- **Examples**:
```
Store credentials in environment variables
Use least-privilege API scopes
Rotate API keys every 90 days
Enable audit logging in production
Review tool permissions before granting access
Monitor API usage through provider dashboard
Use read-only tokens when possible
```

---

### 🚀 SECTION 5: Deployment Context

This section helps users deploy your server.

#### **Intended Use Cases** (REQUIRED)
- **What it is**: What is your server GOOD for?
- **Format**: One use case per line
- **Examples**:
```
Automating GitHub repository management
Creating and tracking issues in development workflows
Syncing code between local and remote repositories
Generating project documentation
Managing pull request reviews
```

#### **Out of Scope Scenarios** (REQUIRED)
- **What it is**: What should your server NOT be used for?
- **Format**: One scenario per line
- **Why it matters**: Sets proper expectations
- **Examples**:
```
Direct database access or SQL execution
File system operations outside configured directories
Real-time collaboration features
Video or audio processing
Cryptocurrency mining or blockchain operations
Production deployments without proper authentication
```

#### **Minimum Node.js Version** (OPTIONAL)
- **What it is**: Minimum Node.js version required
- **Format**: Version number
- **Only fill if your server uses Node.js/TypeScript**
- **Examples**:
  - ✅ "18.0.0"
  - ✅ "20.9.0"
  - ✅ "22.0.0"

#### **Minimum Python Version** (OPTIONAL)
- **What it is**: Minimum Python version required
- **Format**: Version number
- **Only fill if your server uses Python**
- **Examples**:
  - ✅ "3.8"
  - ✅ "3.10"
  - ✅ "3.11"

#### **Environment Variables** (REQUIRED)
- **What it is**: What environment variables must be set
- **Format**: One per line, format: `VAR_NAME: description`
- **Examples**:
```
GITHUB_TOKEN: Personal access token with repo scope
DATABASE_URL: PostgreSQL connection string
API_KEY: Brave Search API key
MAX_RESULTS: Maximum results per query (default: 10)
LOG_LEVEL: Logging verbosity (debug, info, warn, error)
```

#### **External Dependencies** (REQUIRED)
- **What it is**: External services or APIs your server needs
- **Format**: One per line
- **Examples**:
```
GitHub API (api.github.com)
PostgreSQL database server
Redis cache (optional)
Internet connectivity
```
- If none: Write "None - fully self-contained"

#### **Actively Maintained** (REQUIRED - Checkbox)
- **What it is**: Are you still maintaining/updating this server?
- **When to check**:
  - ✅ CHECK if you respond to issues, update dependencies, fix bugs
  - ❌ UNCHECK if archived/deprecated

---

### 📊 SECTION 6: Evaluation Results (OPTIONAL)

This section shows testing and validation results.

#### **Compliance Score** (OPTIONAL)
- **What it is**: How well your server follows MCP specification
- **Format**: Slider from 0-100
- **How to know**: 
  - Run MCP validator tool
  - Or estimate based on testing
- **Score meanings**:
  - `90-100`: Excellent - Full compliance
  - `70-89`: Good - Minor issues
  - `50-69`: Moderate - Some deviations
  - `25-49`: Poor - Significant issues
  - `0-24`: Critical - Major violations

#### **Test Coverage** (OPTIONAL)
- **What it is**: Percentage of code covered by tests
- **Format**: Percentage string (e.g., "85%")
- **How to know**: Run `npm test --coverage` or pytest coverage

#### **Tests Passed** (OPTIONAL)
- **What it is**: Number of test cases that passed
- **Format**: Number
- **Example**: `120`

#### **Tests Failed** (OPTIONAL)
- **What it is**: Number of test cases that failed
- **Format**: Number
- **Should be**: `0` for production servers

---

## Common Questions

### Q: What if I don't know some values?

**A**: 
- **Required fields**: Make your best estimate or use placeholder values
- **Optional fields**: Leave blank - they won't appear in output
- **Unknown performance**: Use conservative estimates (higher response time, lower rate limits)

### Q: How detailed should tool descriptions be?

**A**: 
- Clear enough that someone unfamiliar can understand what it does
- Include key parameters and return values
- 1-2 sentences is perfect
- Example: "Searches GitHub repositories by name, language, or topic. Returns up to 100 results with repository metadata including stars, forks, and last update time."

### Q: Do I need to add EVERY tool?

**A**: 
- Yes, for a complete model card
- But you can start with your most important tools
- You can always regenerate with more tools later

### Q: What if my server has 50+ tools?

**A**:
- That's fine! The generator handles it
- Consider grouping related tools in your planning
- The JSON will include all of them
- The Markdown will list them all clearly

### Q: Can I edit the generated files?

**A**:
- Yes! They're yours to modify
- JSON is machine-readable - edit carefully
- Markdown is human-readable - edit freely
- Keep them in sync if you edit both

---

## Examples

### Example 1: Simple Read-Only Tool

```
Tool Name: weather_get_forecast
Description: Retrieves 7-day weather forecast for a specified location
Input Schema:
{
  "type": "object",
  "properties": {
    "location": {
      "type": "string",
      "description": "City name or ZIP code"
    },
    "units": {
      "type": "string",
      "enum": ["fahrenheit", "celsius"],
      "default": "fahrenheit"
    }
  },
  "required": ["location"]
}

Output Schema:
{
  "type": "object",
  "properties": {
    "forecast": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "date": {"type": "string"},
          "high": {"type": "number"},
          "low": {"type": "number"},
          "conditions": {"type": "string"}
        }
      }
    }
  }
}

Destructive: NO (unchecked)
Read-only: YES (checked)
Async: YES (checked)
```

### Example 2: Destructive Tool

```
Tool Name: database_delete_record
Description: Permanently deletes a record from the specified table
Input Schema:
{
  "type": "object",
  "properties": {
    "table": {
      "type": "string",
      "description": "Table name"
    },
    "id": {
      "type": "number",
      "description": "Record ID to delete"
    }
  },
  "required": ["table", "id"]
}

Output Schema:
{
  "type": "object",
  "properties": {
    "deleted": {"type": "boolean"},
    "id": {"type": "number"}
  }
}

Destructive: YES (checked) ⚠️
Read-only: NO (unchecked)
Async: YES (checked)
```

---

## Tips for Success

### Before Starting:
1. ✅ Have your server's README open for reference
2. ✅ Know your tool names and what they do
3. ✅ Have example input/output for each tool
4. ✅ Know your authentication method

### While Filling:
1. ✅ Work through sections in order
2. ✅ Don't worry about perfection - you can regenerate
3. ✅ Use the examples in this guide as templates
4. ✅ Leave optional fields blank if unsure

### Tool Documentation Tips:
1. ✅ Start with your most important tools
2. ✅ Copy/paste similar schemas and modify
3. ✅ Validate JSON before adding (use jsonlint.com if needed)
4. ✅ Be honest about destructive operations!

### After Generating:
1. ✅ Review both JSON and Markdown files
2. ✅ Check for typos in descriptions
3. ✅ Verify tool names match your actual code
4. ✅ Add to your repository and publish!

---

## Getting Help

**If you get stuck:**
1. Check this guide's examples
2. Look at the MCP Model Card Specification
3. Review existing model cards on GitHub
4. Ask in W3C AI-KR Community Group

**Common mistakes:**
- ❌ Using camelCase for tool names (use snake_case)
- ❌ Forgetting required fields
- ❌ Invalid JSON in schemas
- ❌ Not marking destructive tools properly
- ❌ Too-vague descriptions

---

**Ready to create your model card?**

Open the Colab notebook, follow this guide section by section, and you'll have professional documentation for your MCP server in 15-30 minutes!

---

**Created with**: MCP Model Card Generator v1.0  
**Specification**: MCP Model Card Specification v1.0  
**W3C AI-KR Community Group**  

💙 Built with love by Claude & Paola
