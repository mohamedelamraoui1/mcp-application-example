# MCP Knowledge Base System

This is a Model Context Protocol (MCP) server that provides access to a company knowledge base through Groq's chat completions API.

## ✅ Current Status: WORKING!

The `client-simple.py` is now fully functional and successfully:
- Connects to the MCP server
- Communicates with Groq API (free tier)
- Retrieves information from the knowledge base
- Provides intelligent responses

**Quick Test**: Run `python client-simple.py` to see it in action!

## Understanding the Problem You Encountered

When you ran `python server.py` directly, the terminal hung because:

1. **MCP servers are designed to communicate via stdin/stdout** - they don't run as standalone applications
2. **The server waits for input** from a client that communicates using the MCP protocol
3. **Running it directly leaves it waiting** for messages that never come

## How the System Works

```
[Client] ←→ [MCP Server] ←→ [Knowledge Base (JSON)]
   ↓
[Groq API]
```

1. **Client** (`client-simple.py`) - Handles user queries and Groq communication
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

### 3. Set Up Groq API Key
Edit the `.env` file and add your Groq API key:
```
GROQ_API_KEY=your_actual_api_key_here
```

Get your API key from: https://console.groq.com/keys

## Running the System

### Option 1: Test Server Only (No Groq API Required)
```powershell
python test_server.py
```
This tests the MCP server functionality without requiring a Groq API key.

### Option 2: Full Demo with Groq Integration
```powershell
python client-simple.py
```
This runs the complete system with Groq integration - **Currently Working!**

### Option 3: Alternative Clients (if available)
```powershell
python client.py  # If you have other client implementations
```

## Files Explanation

- `server.py` - MCP server that provides knowledge base access
- `client-simple.py` - **Main working client** that integrates Groq with MCP tools
- `client.py` - Alternative client implementation (if available)
- `data/kb.json` - Knowledge base containing Q&A pairs
- `.env` - Environment variables (Groq API key)
- `requirements.txt` - Python dependencies

## Troubleshooting

### "Terminal hangs when running server.py"
- **Don't run `server.py` directly**
- Use `client-simple.py` instead
- The server is designed to be used by a client, not run standalone

### "Groq API errors"
- Check that your API key is set in `.env`
- Ensure you have credits in your Groq account (free tier available)
- Verify the API key is valid
- Check your internet connection

### "Import errors"
- Make sure virtual environment is activated
- Run `pip install -r ../requirements.txt`
- Install missing packages: `pip install groq python-dotenv nest-asyncio`

### "File not found errors"
- Ensure you're in the `ai-integration` directory
- Check that `data/kb.json` exists
- Verify `.env` file is in the parent directory (`../.env`)

## Example Usage

1. **Quick Start** (Currently Working):
   ```powershell
   python client-simple.py
   ```

2. The system will automatically:
   - Connect to the MCP server
   - Ask the predefined question: "What is our company's vacation policy?"
   - Use Groq AI to process the query
   - Retrieve information from the knowledge base
   - Provide an intelligent response

3. **Sample Questions** you can modify in the code:
   - "What is our company's vacation policy?"
   - "How do I request a new software license?"
   - "What is our remote work policy?"
   - "What are the company benefits?"

4. **To customize queries**: Edit the `main()` function in `client-simple.py` and change the `query` variable.

The system uses the MCP server to retrieve relevant information from the knowledge base and provides intelligent responses through Groq's LLM API (free tier available).
