# Crisp MCP Server

An MCP (Model Context Protocol) server that provides tools for interacting with the Crisp customer support platform.

## Installation

```bash
cd mcp-servers/crisp-mcp
npm install
npm run build
```

## Configuration

The server requires the following environment variables:

| Variable | Description |
|----------|-------------|
| `CRISP_IDENTIFIER` | Your Crisp plugin identifier |
| `CRISP_KEY` | Your Crisp API key |
| `CRISP_WEBSITE_ID` | Your Crisp website ID |

You can get these credentials from the Crisp Marketplace by creating a plugin, or from your Crisp dashboard settings.

## Usage with Claude Code

Add the following to your Claude Code MCP settings (`.claude/settings.json` or global settings):

```json
{
  "mcpServers": {
    "crisp": {
      "command": "node",
      "args": ["/path/to/mcp-servers/crisp-mcp/dist/index.js"],
      "env": {
        "CRISP_IDENTIFIER": "your-identifier",
        "CRISP_KEY": "your-key",
        "CRISP_WEBSITE_ID": "your-website-id"
      }
    }
  }
}
```

## Available Tools

### Conversation Management

| Tool | Description |
|------|-------------|
| `list_conversations` | List conversations with optional filtering (page, search, unresolved, unread) |
| `get_unresolved_conversations` | Get all unresolved conversations (paginated) |
| `get_conversation` | Get detailed info about a specific conversation |
| `search_conversations` | Search conversations by text query |

### Messages

| Tool | Description |
|------|-------------|
| `get_messages` | Get messages from a conversation |
| `get_conversation_with_messages` | Get conversation and messages formatted for analysis |
| `send_message` | Send a message (text or internal note) to a conversation |

### Conversation State

| Tool | Description |
|------|-------------|
| `set_conversation_state` | Change state (pending, unresolved, resolved) |
| `update_conversation_meta` | Update metadata (email, nickname, subject, segments) |
| `add_segments` | Add tags/segments to a conversation |
| `remove_segments` | Remove tags/segments from a conversation |

### Conversation Actions

| Tool | Description |
|------|-------------|
| `assign_conversation` | Assign to a specific operator |
| `block_conversation` | Block a conversation |
| `unblock_conversation` | Unblock a conversation |
| `delete_conversation` | Permanently delete a conversation |

### Team & Visitors

| Tool | Description |
|------|-------------|
| `get_operators` | Get list of support team operators |
| `get_visitors` | Get list of current website visitors |

## Available Resources

| URI | Description |
|-----|-------------|
| `crisp://conversations/unresolved` | List of all unresolved support conversations |

## Examples

### List unresolved conversations

```
Use the list_conversations tool with unresolved_only: true
```

### Get a support ticket with full context

```
Use the get_conversation_with_messages tool with the session_id
```

### Reply to a customer

```
Use the send_message tool with session_id and content
```

### Mark a ticket as resolved

```
Use the set_conversation_state tool with state: "resolved"
```

## Development

```bash
# Watch mode for development
npm run dev

# Build for production
npm run build

# Run the server
npm start
```

## License

MIT
