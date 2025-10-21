# adk-pro  

A simple example project to explore the Google Agent Development Kit (ADK) and basic agent patterns.  

## Overview  

This repository contains a minimal agent built using the Google Agent Development Kit (ADK). ADK is a flexible, modular framework for developing and deploying AI agents. It can orchestrate multiple tools and models to accomplish tasks and is designed to make agent development feel like regular software development. The goal of this project is to demonstrate how to define a simple agent with custom tools and run it locally.  

The `chatbot_agent/agent.py` module defines two simple tools:  

- **`get_weather(city: str)`** – returns a hard‑coded weather report for New York or an error for other cities.  
- **`get_current_time(city: str)`** – returns the current time in the specified city (New York supported).  

These functions are exposed to a root agent (`weather_time_agent`) defined with ADK’s `Agent` class, which uses a LiteLLM model (`azure/gpt-4.1-mini`). The agent can answer questions about the weather or current time in supported cities.  

The `main.py` file currently prints a placeholder greeting. You can extend it to run the agent interactively.  

## Getting Started  

### Prerequisites  

- Python 3.12 or higher  
- A working installation of the Google Agent Development Kit (ADK) and its dependencies (see [`pyproject.toml`](./pyproject.toml) for a list of required packages).  

### Installation  

Clone the repository and install dependencies using `pip`:  

```bash  
git clone https://github.com/ArfiArfath21/adk-pro.git  
cd adk-pro  
python -m venv .venv  
source .venv/bin/activate  # on Windows use .venv\Scripts\activate  
pip install -e .  
```  

This will install `google-adk`, `litellm`, `openai`, `python-dotenv`, and any other dependencies specified in `pyproject.toml`.  

### Configuration  

The agent loads environment variables using `python-dotenv`. Create a `.env` file in the project root (or set environment variables in your shell) to configure credentials for the underlying model provider (e.g., OpenAI API keys or Azure credentials).  

Example `.env`:  

```
OPENAI_API_KEY=your-openai-key  
AZURE_ENDPOINT=your-azure-endpoint  
AZURE_API_KEY=your-azure-key  
```  

### Running the Example Agent  

To experiment with the simple weather/time agent:  

```python  
from chatbot_agent.agent import root_agent  

# Ask about the weather  
response = root_agent.run("What's the weather in New York?")  
print(response)  

# Ask about the time  
response = root_agent.run("What time is it in New York?")  
print(response)  
```  

When you run the above code, the agent will choose the appropriate tool (weather or time) based on your query and return a structured response.  

Alternatively, you can modify `main.py` to call the agent and interact through the terminal or integrate it into your own applications.  

## Extending This Project  

This repository is intentionally minimal to help you understand the core concepts of ADK. Here are a few ideas for extending it:  

- Add more tools (e.g., currency conversion, simple calculators) and include them in the `tools` list when constructing the agent.  
- Implement error handling and improved responses for unsupported cities.  
- Explore multi‑agent workflows by creating additional agents and orchestrating them with ADK’s session and runner APIs.  
- Deploy the agent to Vertex AI Agent Engine or integrate it into a web interface.  

## Learning More  

For more detailed tutorials and examples, refer to the official ADK documentation and sample repos:  

- **ADK Quickstarts and Tutorials** – guides to building agents and multi‑tool workflows.  
- **ADK Sample Agents Repository** – a collection of ready‑to‑use agents demonstrating various use cases.  

---  

This project is maintained by Arfi for educational purposes. Feel free to submit issues or pull requests if you have suggestions or improvements.
