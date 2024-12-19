# Jina AI MCP Server

An MCP server that provides access to Jina AI's powerful web services through Claude. This server implements three main tools:

- Web page reading and content extraction
- Web search
- Fact checking/grounding

## Features

### Tools

#### `read_webpage`
- Extract content from web pages in a format optimized for LLMs
- Supports multiple output formats (Default, Markdown, HTML, Text, Screenshot, Pageshot)
- Options for including links and images
- Ability to generate alt text for images
- Cache control options

#### `search_web`
- Search the web using Jina AI's search API
- Configurable number of results (default: 5)
- Support for image retention and alt text generation
- Multiple return formats (markdown, text, html)
- Returns structured results with titles, descriptions, and content

#### `fact_check`
- Fact-check statements using Jina AI's grounding engine
- Provides factuality scores and supporting evidence 
- Optional deep-dive mode for more thorough analysis
- Returns references with key quotes and supportive/contradictory classification

## Setup

### Prerequisites

You'll need a Jina AI API key to use this server. Get one for free at https://jina.ai/

### Installation

There are two ways to use this server:

#### Option 1: NPX (Recommended)
Add this configuration to your Claude Desktop config file:

```json
{
  "mcpServers": {
    "jina-ai-mcp-server": {
      "command": "npx",
      "args": [
        "-y",
        "jina-ai-mcp-server"
      ],
      "env": {
        "JINA_API_KEY": "<YOUR_KEY>"
      }
    }
  }
}
```

#### Option 2: Local Installation
1. Clone the repository
2. Install dependencies:
```bash
npm install
```

3. Build the server:
```bash
npm run build
```

4. Add this configuration to your Claude Desktop config:
```json
{
  "mcpServers": {
    "jina-ai-mcp-server": {
      "command": "node",
      "args": [
        "/path/to/jina-ai-mcp-server/dist/index.js"
      ],
      "env": {
        "JINA_API_KEY": "<YOUR_KEY>"
      }
    }
  }
}
```

### Config File Location

On MacOS:
```bash
~/Library/Application Support/Claude/claude_desktop_config.json
```

On Windows:
```bash
%APPDATA%/Claude/claude_desktop_config.json
```

### Debugging

Since MCP servers communicate over stdio, debugging can be challenging. We recommend using the [MCP Inspector](https://github.com/modelcontextprotocol/inspector):

```bash
npm run inspector
```

The Inspector will provide a URL to access debugging tools in your browser.

## API Response Types

All tools return structured JSON responses that include:

- Status codes and metadata
- Formatted content based on the requested output type
- Usage information (token counts)
- When applicable: images, links, and additional metadata

For detailed schema information, see `schemas.ts`.
