[![MseeP.ai Security Assessment Badge](https://mseep.net/pr/taxuspt-garmin-mcp-badge.png)](https://mseep.ai/app/taxuspt-garmin-mcp)

# Garmin MCP Server

This Model Context Protocol (MCP) server connects to Garmin Connect and exposes your fitness and health data to Claude and other MCP-compatible clients.

## Features

- List recent activities
- Get detailed activity information
- Access health metrics (steps, heart rate, sleep)
- View body composition data

## Setup

1. Install the required packages on a new environment:

```bash
uv sync
```

## Running the Server

### With Claude Desktop

1. Create a configuration in Claude Desktop:

Edit your Claude Desktop configuration file:

- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`

Add this server configuration:

```json
{
  "mcpServers": {
    "garmin": {
      "command": "uvx",
      "args": [
        "--python", "3.12",
        "--from", "git+https://github.com/Taxuspt/garmin_mcp",
        "garmin-mcp"
      ],
      "env": {
        "GARMIN_EMAIL": "YOUR_GARMIN_EMAIL",
        "GARMIN_PASSWORD": "YOUR_GARMIN_PASSWORD"
      }
    }
  }
}
```

Replace the path with the absolute path to your server file.

2. Restart Claude Desktop

### With MCP Inspector

For testing, you can use the MCP Inspector:

```bash
npx @modelcontextprotocol/inspector python /Users/adomingues/Documents/claude_filesystem/garmin_mcp/garmin_mcp_server.py
```

## Usage Examples

Once connected in Claude, you can ask questions like:

- "Show me my recent activities"
- "What was my sleep like last night?"
- "How many steps did I take yesterday?"
- "Show me the details of my latest run"

## Security Note

## Troubleshooting

If you encounter login issues:

1. Verify your credentials are correct
2. Check if Garmin Connect requires additional verification
3. Ensure the garminconnect package is up to date

For other issues, check the Claude Desktop logs at:
- macOS: `~/Library/Logs/Claude/mcp-server-garmin.log`
- Windows: `%APPDATA%\Claude\logs\mcp-server-garmin.log`
