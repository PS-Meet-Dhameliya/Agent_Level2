# Weekend Wizard 🎉

An intelligent AI agent that orchestrates multiple MCP (Model Context Protocol) tools to provide interactive weekend assistance through natural language conversations.

## Features

- **Multi-tool orchestration**: Handles complex requests requiring multiple sequential tool calls
- **Natural language interface**: Ask questions in plain English
- **5 integrated tools**:
  - 🌤️ Weather data (Open-Meteo API)
  - 📚 Book recommendations (Open Library)
  - 😄 Random jokes (JokeAPI)
  - 🐕 Random dog pictures (Dog CEO API)
  - 🧠 Trivia questions (Open Trivia DB)
- **Robust error handling**: Automatic JSON parsing recovery and comprehensive debugging
- **ReAct reasoning**: Step-by-step decision making with full visibility

## Architecture

```
┌─────────────┐         ┌──────────────┐         ┌─────────────┐
│             │         │              │         │             │
│  agent_fun  │ ◄─────► │  MCP Server  │ ◄─────► │  External   │
│  (Client)   │  stdio  │ (server_fun) │   HTTP  │    APIs     │
│             │         │              │         │             │
└─────────────┘         └──────────────┘         └─────────────┘
      │
      └─► Ollama (Mistral 7B)
```

## Prerequisites

- Python 3.8+
- [Ollama](https://ollama.ai/) installed with Mistral 7B model
- Internet connection for API calls

## Installation

1. **Clone or download this project**

2. **Install Ollama and pull the Mistral model:**
   ```bash
   ollama pull mistral:7b
   ```

3. **Install Python dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

## Usage

### Start the agent:
```bash
python agent_fun.py
```

### Example interactions:

**Single tool request:**
```
You: tell me a joke
Agent: Here's a joke for you: Why did the scarecrow win an award? Because he was outstanding in his field!
```

**Multi-tool request:**
```
You: tell me a joke and recommend books about history
Agent: Here's a joke: [joke content]. And here are some great history books: [book recommendations]
```

**Available commands:**
- Type your question and press Enter
- Type `exit` or `quit` to stop the agent

## How It Works

1. **User input**: You ask a question in natural language
2. **LLM reasoning**: Mistral 7B analyzes the request and decides which tool(s) to call
3. **Sequential execution**: Agent calls tools one at a time, seeing each result
4. **Response synthesis**: Final answer combines all tool results into a coherent response

### Debug Output

The agent provides detailed debug information:
- `[DEBUG]` - Shows LLM decisions and tool calls
- `[ERROR]` - Displays any errors encountered
- Full visibility into the reasoning process

## Project Structure

```
weekend-wizard/
├── agent_fun.py        # Main agent with multi-tool orchestration
├── server_fun.py       # MCP server with 5 tool implementations
├── requirements.txt    # Python dependencies
└── README.md          # This file
```

## Technical Details

- **LLM**: Mistral 7B via Ollama
- **Protocol**: MCP (Model Context Protocol) over stdio
- **Pattern**: ReAct (Reasoning + Acting)
- **Max iterations**: 6 sequential tool calls per request
- **Temperature**: 0.2 for consistent outputs


