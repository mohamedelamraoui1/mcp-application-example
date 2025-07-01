# MCP Knowledge Base System

This is a Model Context Protocol (MCP) server that provides access to a company knowledge base through OpenAI's chat completions API.

## Understanding the Problem You Encountered

When you ran `python server.py` directly, the terminal hung because:

1. **MCP servers are designed to communicate via stdin/stdout** - they don't run as standalone applications
2. **The server waits for input** from a client that communicates using the MCP protocol
3. **Running it directly leaves it waiting** for messages that never come

## How the System Works

```
[Client] ←→ [MCP Server] ←→ [Knowledge Base (JSON)]
   ↓
[OpenAI API]
```

1. **Client** (`client.py`) - Handles user queries and OpenAI communication
2. **MCP Server** (`server.py`) - Provides tools to access the knowledge base
3. **Knowledge Base** (`data/kb.json`) - Contains Q&A data

## Setup Instructions

### 1. Ensure Virtual Environment is Active
```powershell
# If not already activated
.\.venv\Scripts\Activate.ps1
```

### 2. Install Dependencies
```powershell
pip install -r ../requirements.txt
```

### 3. Set Up OpenAI API Key
Edit the `.env` file and add your OpenAI API key:
```
OPENAI_API_KEY=your_actual_api_key_here
```

Get your API key from: https://platform.openai.com/api-keys

## Running the System

### Option 1: Test Server Only (No OpenAI Required)
```powershell
python test_server.py
```
This tests the MCP server functionality without requiring an OpenAI API key.

### Option 2: Full Demo with OpenAI Integration
```powershell
python demo.py
```
This runs the complete system with OpenAI integration.

### Option 3: Use Client Directly
```powershell
python client.py
```
This runs the main client application.

## Files Explanation

- `server.py` - MCP server that provides knowledge base access
- `client.py` - Main client that integrates OpenAI with MCP tools
- `demo.py` - Demonstration script showing how to use the system
- `test_server.py` - Simple test script for the MCP server only
- `data/kb.json` - Knowledge base containing Q&A pairs
- `.env` - Environment variables (OpenAI API key)

## Troubleshooting

### "Terminal hangs when running server.py"
- **Don't run `server.py` directly**
- Use `test_server.py` or `demo.py` instead
- The server is designed to be used by a client, not run standalone

### "OpenAI API errors"
- Check that your API key is set in `.env`
- Ensure you have credits in your OpenAI account
- Verify the API key is valid

### "Import errors"
- Make sure virtual environment is activated
- Run `pip install -r ../requirements.txt`

### "File not found errors"
- Ensure you're in the `ai-integration` directory
- Check that `data/kb.json` exists

## Example Usage

1. Start with testing the server:
   ```powershell
   python test_server.py
   ```

2. If that works, try the full demo:
   ```powershell
   python demo.py
   ```

3. Ask questions like:
   - "What is our company's vacation policy?"
   - "How do I request a new software license?"
   - "What is our remote work policy?"

The system will use the MCP server to retrieve relevant information from the knowledge base and provide intelligent responses through OpenAI.
