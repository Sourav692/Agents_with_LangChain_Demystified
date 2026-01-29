# MLflow ResponsesAgent - Complete Tutorial Guide

This repository contains comprehensive Jupyter notebooks demonstrating MLflow's ResponsesAgent for building production-ready AI agents.

## Overview

**ResponsesAgent** is MLflow's framework-agnostic interface for serving generative AI models with advanced capabilities including:
- Tool calling and function execution
- Multi-agent orchestration
- OpenAI API compatibility
- Full MLflow tracing and observability
- Framework independence (works with LangGraph, LangChain, custom implementations)

## Why ResponsesAgent?

Traditional approaches to deploying AI agents face several challenges:

### Problems:
- ❌ Framework lock-in (hard to switch between LangGraph, LangChain, etc.)
- ❌ No standardized input/output formats
- ❌ Complex tool calling implementations
- ❌ Difficult deployment and scaling
- ❌ Poor observability and debugging
- ❌ No multi-agent support

### Solutions with ResponsesAgent:
- ✅ **Framework Independent**: Wrap any agent implementation
- ✅ **Standard Interface**: OpenAI Responses API compatibility
- ✅ **Built-in Tool Support**: Native function calling
- ✅ **Easy Deployment**: Log once, deploy anywhere
- ✅ **Full Tracing**: Integrated MLflow observability
- ✅ **Multi-agent Ready**: Support for complex workflows

## Notebooks

### 1. MLflow Installation on Mac
**File**: `01_mlflow_installation_mac.ipynb`

Complete setup guide covering:
- Python environment verification
- MLflow and dependencies installation
- Local tracking server setup
- MLflow UI configuration
- Environment variable setup
- Installation verification

### 2. ResponsesAgent Basics
**File**: `02_responses_agent_basics.ipynb`

Understanding the fundamentals:
- What is ResponsesAgent?
- Why it's needed
- Key features and advantages
- Basic implementation patterns
- Request/Response schemas
- Helper methods
- Logging and loading models

### 3. LangGraph Integration
**File**: `03_langgraph_integration.ipynb`

Wrapping LangGraph agents:
- Building basic LangGraph agents
- Wrapping with ResponsesAgent
- Format conversion utilities
- Logging and deployment
- Multi-turn conversations
- Full tracing integration

### 4. Tool Calling Agent
**File**: `04_tool_calling_agent.ipynb`

Production-ready tool-calling:
- Tool specification (OpenAI format)
- Tool execution framework
- Iterative agent loop
- Multiple tool support
- Error handling
- Full observability

### 5. Streaming Responses
**File**: `05_streaming_responses.ipynb`

Real-time response streaming:
- Why streaming matters
- Streaming interface overview
- Basic text streaming
- OpenAI streaming integration
- Streaming with tool calls
- Reasoning/chain-of-thought streaming
- Production streaming patterns

### 6. ChatCompletions API Integration
**File**: `06_chat_completions_integration.ipynb`

Using OpenAI ChatCompletions API:
- ChatCompletions vs Responses API
- Basic integration patterns
- Format conversion utilities
- Multi-turn conversations
- Context-aware agents
- Production deployment

### 7. Responses API Integration
**File**: `07_responses_api_integration.ipynb`

Using OpenAI Responses API:
- Direct Responses API integration
- Native format compatibility
- Streaming with Responses API
- Tool calling with Responses API
- Production-ready patterns
- Best practices

### 8. Serving and Deployment
**File**: `08_serving_and_deployment.ipynb`

Complete deployment guide:
- Local model serving
- Docker deployment
- Databricks Model Serving
- Testing deployed models
- Production best practices
- Troubleshooting guide

## Quick Start

### Prerequisites
- macOS (or Linux/Windows with minor adjustments)
- Python 3.8+
- OpenAI API key

### Installation Steps

1. **Install MLflow and dependencies**:
```bash
pip install "mlflow[genai]" pydantic>=2.0.0 langgraph>=0.2.27 langchain>=0.3.0 langchain-openai>=0.2.0 openai python-dotenv backoff
```

2. **Set up environment variables**:
Create a `.env` file:
```bash
OPENAI_API_KEY=your_api_key_here
MLFLOW_TRACKING_URI=file://~/mlflow_experiments
```

3. **Start MLflow UI** (optional):
```bash
mlflow ui
```
Then open http://localhost:5000

4. **Run the notebooks in order**:
- Start with `01_mlflow_installation_mac.ipynb`
- Follow through to `08_serving_and_deployment.ipynb`

## ResponsesAgent vs Alternatives

| Feature | ChatModel | ChatAgent | ResponseAgent |
|---------|-----------|-----------|---------------|
| Basic Chat | ✅ | ✅ | ✅ |
| Tool Calling | ❌ | ✅ | ✅ |
| Multi-agent | ❌ | ❌ | ✅ |
| OpenAI Compatible | ❌ | Partial | Full |
| Intermediate Outputs | ❌ | Limited | Full |
| Streaming | ✅ | ✅ | ✅ |
| Custom Outputs | ❌ | ❌ | ✅ |
| Annotations | ❌ | ❌ | ✅ |

## Key Helper Methods

ResponsesAgent provides these helper methods for creating outputs:

| Method | Purpose |
|--------|---------|
| `create_text_output_item()` | Create text response |
| `create_function_call_item()` | Create tool invocation |
| `create_function_call_output_item()` | Create tool result |
| `create_reasoning_item()` | Create chain-of-thought |
| `create_text_delta()` | Stream text chunks |
| `create_annotation_added()` | Add annotations |

## Deployment Options

| Method | Command | Best For |
|--------|---------|----------|
| **Local** | `mlflow models serve -m <uri>` | Development |
| **Docker** | `mlflow models build-docker` | Containerized |
| **Databricks** | `client.create_endpoint()` | Production |

### Local Serving Example
```bash
# Log your model, then serve
mlflow models serve -m runs:/<run_id>/agent -p 5001

# Test with curl
curl -X POST http://localhost:5001/invocations \
  -H 'Content-Type: application/json' \
  -d '{"input": [{"role": "user", "content": "Hello!"}]}'
```

## Architecture

### ResponsesAgent Structure

```python
class MyResponsesAgent(ResponsesAgent):
    @mlflow.trace(span_type=SpanType.AGENT)
    def predict(self, request: ResponsesAgentRequest) -> ResponsesAgentResponse:
        # Your agent logic
        return ResponsesAgentResponse(output=[...])
    
    @mlflow.trace(span_type=SpanType.AGENT)
    def predict_stream(self, request: ResponsesAgentRequest) -> Generator:
        # Streaming logic
        yield ResponsesAgentStreamEvent(...)
```

### LangGraph Wrapper Pattern

```python
class LangGraphResponsesAgent(ResponsesAgent):
    def __init__(self, agent: CompiledStateGraph):
        self.agent = agent
    
    def predict_stream(self, request):
        # Convert formats
        cc_msgs = to_chat_completions_input(request.input)
        
        # Stream through LangGraph
        for _, events in self.agent.stream({"messages": cc_msgs}):
            yield from output_to_responses_items_stream(events)
```

## Troubleshooting

### Common Issues

**1. Import Errors**
```bash
pip install "pydantic>=2.0.0"
```

**2. OpenAI API Errors**
```bash
export OPENAI_API_KEY=your_key_here
```

**3. MLflow Tracking Issues**
```python
mlflow.set_tracking_uri("file://~/mlflow_experiments")
```

**4. Long-Running Agents Timeout**
```python
os.environ["MLFLOW_DEPLOYMENT_PREDICT_TIMEOUT"] = "900"
os.environ["MLFLOW_DEPLOYMENT_PREDICT_TOTAL_TIMEOUT"] = "1200"
```

## Additional Resources

### Official Documentation
- [MLflow ResponsesAgent Docs](https://mlflow.org/docs/latest/genai/serving/responses-agent/)
- [LangGraph Documentation](https://langchain-ai.github.io/langgraph/)
- [MLflow Tracing](https://mlflow.org/docs/latest/genai/tracing/)

### Related Guides
- [Models from Code](https://mlflow.org/docs/latest/models.html#models-from-code)
- [MLflow Deployment](https://mlflow.org/docs/latest/models.html#built-in-deployment-tools)
- [OpenAI Responses API](https://platform.openai.com/docs/api-reference/responses)

## Learning Path

**Recommended order**:
1. ✅ Complete installation (Notebook 01)
2. ✅ Understand ResponsesAgent basics (Notebook 02)
3. ✅ Learn LangGraph integration (Notebook 03)
4. ✅ Build tool-calling agents (Notebook 04)
5. ✅ Master streaming responses (Notebook 05)
6. ✅ Explore ChatCompletions integration (Notebook 06)
7. ✅ Use Responses API directly (Notebook 07)
8. ✅ Deploy to production (Notebook 08)
9. 🚀 Build your own production agent!

---

**Happy Agent Building! 🤖**

For more information:
- [Databricks MLflow](https://docs.databricks.com/mlflow/index.html)
- [Mosaic AI Agent Framework](https://docs.databricks.com/generative-ai/agent-framework/)
