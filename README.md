# MCP Application Examples

A comprehensive collection of examples demonstrating the **Model Context Protocol (MCP)** - a universal protocol for integrating AI models with external tools, data sources, and services.

## 🤖 What is MCP (Model Context Protocol)?

The **Model Context Protocol (MCP)** is an open-source standard that enables AI assistants to securely access external tools and data sources. Think of it as a bridge that allows AI models to:

- **Execute tools**: Run calculations, API calls, file operations, etc.
- **Access data**: Query databases, knowledge bases, files, and more
- **Integrate services**: Connect with external APIs, cloud services, and applications
- **Maintain security**: Controlled access with proper permissions and authentication

### Key Benefits:
- 🔌 **Universal Integration**: One protocol for all external integrations
- 🛡️ **Security First**: Controlled access with proper authentication
- 🚀 **Easy Development**: Simple APIs for both servers and clients
- 🌐 **Transport Flexibility**: Works with stdio, SSE, and other transports
- 📦 **Modular Design**: Add/remove capabilities as needed

### How MCP Works:
```
AI Assistant ←→ MCP Client ←→ MCP Server ←→ External Services
                    ↑              ↑
               Your App      Tools/Data Sources
```

## 📁 Project Structure

This repository contains multiple examples showing different aspects of MCP:

### 🧮 [`simple-server-step/`](./simple-server-step/)
**Basic MCP Server with Calculator Tool**
- Simple calculator server with add function
- Demonstrates basic MCP server setup
- Shows both stdio and SSE transport options
- Perfect starting point for understanding MCP basics

**Files:**
- `server.py` - Basic MCP server with calculator tool
- `client-stdio.py` - Client using stdio transport
- `client-see.py` - Client using SSE transport

### 🧠 [`ai-integration/`](./ai-integration/)
**Advanced AI-Powered Knowledge Base**
- MCP server with Groq AI integration
- Knowledge base querying with natural language
- Demonstrates real-world AI application
- Shows how to integrate external AI services

**Files:**
- `server.py` - MCP server with AI-powered knowledge base
- `client.py` - Full-featured client
- `client-simple.py` - Simplified client for quick testing
- `data/kb.json` - Sample knowledge base

### 🐳 [`run-with-docker/`](./run-with-docker/)
**Dockerized MCP Server**
- Complete Docker setup for MCP server
- Production-ready containerization
- Easy deployment and scaling
- Includes comprehensive Docker documentation

**Files:**
- `server.py` - MCP server optimized for containers
- `client.py` - Client for connecting to containerized server
- `Dockerfile` - Docker configuration
- `requirements.txt` - Python dependencies

## 🚀 Quick Start

### Prerequisites
- Python 3.11+
- Docker (for containerized examples)
- Git

### 1. Clone and Setup
```bash
git clone <repository-url>
cd mcp-application
pip install -r requirements.txt
```

### 2. Choose Your Adventure

#### 🔰 **Beginner**: Start with Simple Calculator
```bash
cd simple-server-step
python server.py  # In one terminal
python client-stdio.py  # In another terminal
```

#### 🧠 **Intermediate**: Try AI Integration
```bash
cd ai-integration
# Set up your Groq API key in ../.env
python client-simple.py
```

#### 🐳 **Advanced**: Run with Docker
```bash
cd run-with-docker
docker build -t mcp-server .
docker run -p 8050:8050 mcp-server
python client.py  # In another terminal
```

## 🛠️ Development Guide

### Creating Your Own MCP Server

1. **Install FastMCP**:
   ```bash
   pip install mcp[cli]
   ```

2. **Basic Server Template**:
   ```python
   from mcp.server.fastmcp import FastMCP
   
   mcp = FastMCP(name="MyServer")
   
   @mcp.tool()
   def my_tool(param: str) -> str:
       """Your tool description"""
       return f"Processed: {param}"
   
   if __name__ == "__main__":
       mcp.run(transport="stdio")
   ```

3. **Add More Features**:
   - Resources (data access)
   - Prompts (reusable prompt templates)
   - Multiple tools
   - Error handling

### Transport Options

#### **STDIO Transport** (Standard)
- Communication via stdin/stdout
- Perfect for command-line tools
- Used by most MCP clients

#### **SSE Transport** (Server-Sent Events)
- HTTP-based communication
- Great for web applications
- Easier debugging and testing

## 📚 Learning Path

1. **Start Here**: [`simple-server-step/`](./simple-server-step/) - Learn MCP basics
2. **Add AI**: [`ai-integration/`](./ai-integration/) - Integrate AI services
3. **Deploy**: [`run-with-docker/`](./run-with-docker/) - Production deployment
4. **Build Your Own**: Create custom MCP servers for your use cases

## 🔧 Configuration

### Environment Variables
Create a `.env` file in the root directory:
```env
GROQ_API_KEY=your_groq_api_key_here
# Add other API keys as needed
```

### Common Issues & Solutions

#### "Server hangs when run directly"
- ✅ **Solution**: MCP servers communicate via stdin/stdout, use a client to connect
- ✅ **For testing**: Use SSE transport or run the provided client

#### "Connection refused"
- ✅ **Check**: Server is running and listening on correct port
- ✅ **Verify**: Firewall settings allow the connection
- ✅ **Docker**: Ensure port mapping is correct (`-p 8050:8050`)

#### "Import errors"
- ✅ **Install**: `pip install -r requirements.txt`
- ✅ **Virtual env**: Use a virtual environment for isolation

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Add examples or improvements
4. Test thoroughly
5. Submit a pull request

## 📖 Additional Resources

- [MCP Official Documentation](https://modelcontextprotocol.io/)
- [FastMCP Documentation](https://github.com/jlowin/fastmcp)
- [MCP Specification](https://spec.modelcontextprotocol.io/)
- [Community Examples](https://github.com/modelcontextprotocol)

## 📄 License

This project is open source. See individual files for specific license information.

---

**Happy Building with MCP! 🚀**

*Start with the simple examples and work your way up to building powerful AI-integrated applications.*