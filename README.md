# Agentic AI - MCP Calculator Example

This project demonstrates a minimal Model Context Protocol (MCP) setup where a lightweight calculator server exposes a tool and an Express client connects it to a Groq-backed LLM.

## What this project does

- Runs an MCP server in `server.js`
- Exposes a `addition` tool that adds two numbers
- Starts the MCP server from the client using `@modelcontextprotocol/client`
- Uses `@langchain/groq` to let the LLM call the MCP tool when prompted
- Exposes a simple Express API at `/chat` for sending prompts

## Project structure

- `server.js` - MCP server implementation
- `client.js` - Express API client that connects to the MCP server and invokes Groq
- `package.json` - Node project configuration and scripts

## Prerequisites

- Node.js 18 or newer
- A Groq API key

## Setup

1. Install dependencies:

   ```bash
   npm install
   ```

2. Create a `.env` file in the project root and add your Groq API key:

   ```env
   GROQ_API_KEY=your_api_key_here
   ```

3. Start the app:

   ```bash
   npm run client
   ```

This command runs the Express app on port `5000` by default and automatically starts the MCP server process.

## API usage

Send a POST request to:

```http
POST http://localhost:5000/chat
Content-Type: application/json
```

Example body:

```json
{
  "prompt": "Add 12 and 30 using the calculator tool"
}
```

Example response:

```json
"sum using this mcp tool is 12 & 30 = 42"
```

## Notes

- The MCP tool is named `addition`.
- The LLM is configured with the model `openai/gpt-oss-120b`.
- The app uses a generated tool call from the LLM to invoke the MCP server function and return the result.
