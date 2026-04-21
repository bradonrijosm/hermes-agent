# Hermes Agent

A fork of [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) — an autonomous AI agent framework powered by Hermes models with tool-use and function-calling capabilities.

## Features

- 🤖 **Hermes Model Integration** — Optimized for NousResearch Hermes series models
- 🛠️ **Tool Use & Function Calling** — Structured JSON tool calls with automatic execution
- 🔄 **Agentic Loop** — Multi-step reasoning with tool feedback
- 🐳 **Docker Support** — Containerized deployment ready
- 🔧 **Extensible** — Easy to add custom tools and integrations

## Quick Start

### Prerequisites

- Python 3.10+
- An OpenAI-compatible API endpoint (e.g., Ollama, vLLM, OpenRouter, or OpenAI)

### Installation

```bash
# Clone the repository
git clone https://github.com/your-org/hermes-agent.git
cd hermes-agent

# Install dependencies
pip install -r requirements.txt

# Copy and configure environment variables
cp .env.example .env
# Edit .env with your API keys and settings
```

### Configuration

Copy `.env.example` to `.env` and configure the following key variables:

```env
# API Configuration
OPENAI_API_KEY=your_api_key_here
OPENAI_BASE_URL=https://api.openai.com/v1  # or your custom endpoint

# Model Selection
MODEL_NAME=NousResearch/Hermes-3-Llama-3.1-70B

# Agent Settings
MAX_ITERATIONS=10
TEMPERATURE=0.7
```

### Running the Agent

```bash
# Run interactively
python main.py

# Run with a specific prompt
python main.py --prompt "Research the latest developments in quantum computing"

# Run with Docker
docker compose up
```

## Usage

### Basic Example

```python
from hermes_agent import HermesAgent
from hermes_agent.tools import WebSearchTool, CodeExecutionTool

agent = HermesAgent(
    model="NousResearch/Hermes-3-Llama-3.1-70B",
    tools=[WebSearchTool(), CodeExecutionTool()],
)

result = agent.run("Write and test a Python function to calculate fibonacci numbers")
print(result)
```

### Adding Custom Tools

```python
from hermes_agent.tools import BaseTool
from pydantic import BaseModel

class MyToolInput(BaseModel):
    query: str

class MyCustomTool(BaseTool):
    name = "my_custom_tool"
    description = "Does something useful"
    input_schema = MyToolInput

    def execute(self, query: str) -> str:
        # Your tool logic here
        return f"Result for: {query}"
```

## Project Structure

```
hermes-agent/
├── hermes_agent/          # Core agent package
│   ├── __init__.py
│   ├── agent.py           # Main agent loop
│   ├── client.py          # LLM API client
│   ├── tools/             # Built-in tools
│   └── utils/             # Utility functions
├── tests/                 # Test suite
├── docker-compose.yml     # Docker configuration
├── Dockerfile
├── requirements.txt
└── main.py                # CLI entry point
```

## Contributing

Contributions are welcome! Please open an issue first to discuss what you'd like to change.

1. Fork the repository
2. Create a feature branch (`git checkout -b feat/amazing-feature`)
3. Commit your changes (`git commit -m 'feat: add amazing feature'`)
4. Push to the branch (`git push origin feat/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the Apache 2.0 License — see the [LICENSE](LICENSE) file for details.

## Acknowledgements

- [NousResearch](https://nousresearch.com/) for the original hermes-agent and Hermes model series
- The open-source AI community
