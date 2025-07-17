# LangGraph Introduction Tutorial

A comprehensive introduction to LangGraph with practical examples using OpenAI's GPT models.

## Overview

This repository contains code examples and tutorials for getting started with LangGraph, a library for building stateful, multi-actor applications with LLMs. LangGraph is particularly useful for creating complex workflows, agent systems, and multi-step reasoning applications.

## What is LangGraph?

LangGraph is a library built on top of LangChain that allows you to create cyclical graphs of LLM calls and other operations. It's designed for building:

- **Agent workflows**: Complex reasoning chains with multiple steps
- **Multi-agent systems**: Coordinated interactions between different AI agents
- **Stateful applications**: Applications that maintain state across interactions
- **Human-in-the-loop systems**: Workflows that can pause for human input

## Features Demonstrated

- Basic LangGraph setup and configuration
- Creating simple linear workflows
- Building conditional flows with decision points
- State management across nodes
- Integration with OpenAI's GPT models
- Error handling and retry mechanisms
- Human-in-the-loop examples

## Repository Structure

```
langgraph-introduction/
├── README.md
├── requirements.txt
├── .env.example
├── .gitignore
├── notebooks/
│   ├── 01_langgraph_basics.ipynb
│   ├── 02_conditional_flows.ipynb
│   └── 03_advanced_examples.ipynb
├── src/
│   ├── __init__.py
│   ├── basic_agent.py
│   ├── conditional_agent.py
│   └── utils.py
└── examples/
    ├── simple_workflow.py
    ├── research_agent.py
    └── chat_with_tools.py
```

## Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/genai-lab-business/langgraph-introduction.git
cd langgraph-introduction
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Set Up Environment Variables

```bash
cp .env.example .env
# Edit .env and add your OpenAI API key
```

### 4. Run the Jupyter Notebook

```bash
jupyter notebook notebooks/01_langgraph_basics.ipynb
```

## Prerequisites

- Python 3.8+
- OpenAI API key
- Basic understanding of Python and LangChain concepts

## Installation

Install the required packages:

```bash
pip install langgraph langchain-openai python-dotenv jupyter
```

## Usage Examples

### Basic Linear Workflow

```python
from langgraph.graph import StateGraph
from langchain_openai import ChatOpenAI

# Create a simple workflow that processes text through multiple steps
def create_basic_workflow():
    workflow = StateGraph(AgentState)
    
    workflow.add_node("analyze", analyze_text)
    workflow.add_node("summarize", summarize_text)
    workflow.add_node("format", format_output)
    
    workflow.add_edge("analyze", "summarize")
    workflow.add_edge("summarize", "format")
    
    workflow.set_entry_point("analyze")
    workflow.set_finish_point("format")
    
    return workflow.compile()
```

### Conditional Flow

```python
def create_conditional_workflow():
    workflow = StateGraph(AgentState)
    
    workflow.add_node("classifier", classify_input)
    workflow.add_node("technical_response", technical_handler)
    workflow.add_node("general_response", general_handler)
    
    workflow.add_conditional_edges(
        "classifier",
        decide_path,
        {
            "technical": "technical_response",
            "general": "general_response"
        }
    )
    
    return workflow.compile()
```

## Key Concepts

### State Management
LangGraph uses a state object that gets passed between nodes, allowing you to maintain context throughout your workflow.

### Nodes and Edges
- **Nodes**: Individual functions or operations in your graph
- **Edges**: Connections between nodes that define the flow
- **Conditional Edges**: Dynamic routing based on state or conditions

### Compilation
Workflows must be compiled before execution, which optimizes the graph and prepares it for running.

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Related Resources

- [LangGraph Documentation](https://langchain-ai.github.io/langgraph/)
- [LangChain Documentation](https://docs.langchain.com/)
- [OpenAI API Documentation](https://platform.openai.com/docs/)

## Medium Article

This repository accompanies the Medium article: "Getting Started with LangGraph: Building Intelligent Workflows with LLMs"

## Support

If you have questions or need help:
1. Check the [Issues](https://github.com/genai-lab-business/langgraph-introduction/issues) section
2. Create a new issue if your question isn't already addressed
3. Join the LangChain Discord community

---

**Happy coding with LangGraph!** 🚀
