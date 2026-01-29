# MLflow ResponseAgent with LangGraph - Complete Guide

This repository contains comprehensive Jupyter notebooks demonstrating MLflow's ResponseAgent with LangGraph integration for building production-ready AI agents.

## 📚 Overview

**ResponseAgent** is MLflow's framework-agnostic interface for serving generative AI models with advanced capabilities including:
- Tool calling and function execution
- Multi-agent orchestration
- OpenAI API compatibility
- Full MLflow tracing and observability
- Framework independence (works with LangGraph, LangChain, custom implementations)

## 🎯 Why ResponseAgent?

Traditional approaches to deploying AI agents face several challenges:

### Problems:
- ❌ Framework lock-in (hard to switch between LangGraph, LangChain, etc.)
- ❌ No standardized input/output formats
- ❌ Complex tool calling implementations
- ❌ Difficult deployment and scaling
- ❌ Poor observability and debugging
- ❌ No multi-agent support

### Solutions with ResponseAgent:
- ✅ **Framework Independent**: Wrap any agent implementation
- ✅ **Standard Interface**: OpenAI Responses API compatibility
- ✅ **Built-in Tool Support**: Native function calling
- ✅ **Easy Deployment**: Log once, deploy anywhere
- ✅ **Full Tracing**: Integrated MLflow observability
- ✅ **Multi-agent Ready**: Support for complex workflows

## 📖 Notebooks

### 1. MLflow Installation on Mac
**File**: `01_mlflow_installation_mac.ipynb`

Complete setup guide covering:
- Python environment verification
- MLflow and dependencies installation
- Local tracking server setup
- MLflow UI configuration
- Environment variable setup
- Installation verification

**Key installations**:
```bash
pip install mlflow[genai]
pip install pydantic>=2.0.0
pip install langgraph>=0.2.27
pip install langchain>=0.3.0
pip install langchain-openai>=0.2.0
```

### 2. ResponseAgent Basics
**File**: `02_responses_agent_basics.ipynb`

Understanding the fundamentals:
- What is ResponseAgent?
- Why it's needed
- Key features and advantages
- Basic implementation patterns
- Request/Response schemas
- Helper methods
- Logging and loading models

**Key concepts**:
- Framework-agnostic design
- Structured I/O handling
- OpenAI compatibility
- Models-from-Code approach

### 3. LangGraph Integration
**File**: `03_langgraph_integration.ipynb`

Wrapping LangGraph agents:
- Building basic LangGraph agents
- Wrapping with ResponseAgent
- Format conversion utilities
- Logging and deployment
- Multi-turn conversations
- Full tracing integration

**LangGraph benefits**:
- Cycles and branching
- State persistence
- Human-in-the-loop
- Streaming support

### 4. Tool Calling Agent
**File**: `04_tool_calling_agent.ipynb`

Production-ready tool-calling:
- Tool specification (OpenAI format)
- Tool execution framework
- Iterative agent loop
- Multiple tool support
- Error handling
- Full observability

**Tools demonstrated**:
- Weather API (mock)
- Calculator operations
- Custom tool creation

## 🚀 Quick Start

### Prerequisites
- macOS
- Python 3.8+
- OpenAI API key

### Installation Steps

1. **Clone or download this repository**

2. **Install MLflow and dependencies**:
```bash
pip install mlflow[genai] pydantic>=2.0.0 langgraph>=0.2.27 langchain>=0.3.0 langchain-openai>=0.2.0 openai python-dotenv backoff
```

3. **Set up environment variables**:
Create a `.env` file:
```bash
OPENAI_API_KEY=your_api_key_here
MLFLOW_TRACKING_URI=file://~/mlflow_experiments
```

4. **Start MLflow UI** (optional, for viewing experiments):
```bash
mlflow ui
```
Then open http://localhost:5000

5. **Run the notebooks in order**:
- Start with `01_mlflow_installation_mac.ipynb`
- Follow through to `04_tool_calling_agent.ipynb`

## 💡 Use Cases for LangGraph Agents

### When to Use ResponseAgent with LangGraph:

1. **Production Deployment**
   - Need standardized API for multiple agents
   - Require OpenAI-compatible interfaces
   - Want framework flexibility

2. **Multi-Agent Systems**
   - Coordinating multiple specialized agents
   - Complex workflow orchestration
   - Agent-to-agent communication

3. **Tool-Calling Applications**
   - Agents that interact with external APIs
   - Database query agents
   - Automation workflows

4. **Observability Requirements**
   - Need detailed execution traces
   - Debugging complex agent behavior
   - Performance monitoring

## 📊 ResponseAgent vs Alternatives

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

## 🏗️ Architecture

### ResponseAgent Structure

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

## 🔧 Common Patterns

### 1. Simple Chatbot
```python
agent = SimpleResponsesAgent()
response = agent.predict({
    "input": [{"role": "user", "content": "Hello!"}]
})
```

### 2. Tool-Calling Agent
```python
agent = ToolCallingAgent(model="gpt-4o", tools=[weather_tool, calc_tool])
response = agent.predict({
    "input": [{"role": "user", "content": "What's the weather?"}]
})
```

### 3. LangGraph Integration
```python
graph = create_langgraph_agent()
agent = LangGraphResponsesAgent(graph)
response = agent.predict(request)
```

## 📦 Deployment

### Local Serving
```bash
# Log model
with mlflow.start_run():
    mlflow.pyfunc.log_model(python_model="agent.py", artifact_path="agent")

# Serve model
mlflow models serve -m runs:/<run-id>/agent -p 5001
```

### Testing Endpoint
```bash
curl -X POST http://localhost:5001/invocations \
  -H 'Content-Type: application/json' \
  -d '{
    "input": [{"role": "user", "content": "Hello!"}]
  }'
```

### Databricks Deployment
For Databricks Model Serving, the logged model works seamlessly:
1. Log model to MLflow
2. Register in Model Registry
3. Deploy to Databricks serverless endpoint
4. Use with OpenAI SDK or Databricks SDK

## 🔍 Observability

### MLflow Tracing
Every agent execution is automatically traced:
- Input/output at each step
- Tool executions
- Token usage
- Execution time
- Error tracking

**View traces**:
1. Start MLflow UI: `mlflow ui`
2. Navigate to your experiment
3. Click "Traces" tab
4. Explore detailed execution

## 🛠️ Troubleshooting

### Common Issues

**1. Import Errors**
```bash
# Ensure Pydantic v2+
pip install "pydantic>=2.0.0"
```

**2. OpenAI API Errors**
```bash
# Check environment variable
echo $OPENAI_API_KEY
```

**3. MLflow Tracking Issues**
```python
# Set tracking URI explicitly
mlflow.set_tracking_uri("file://~/mlflow_experiments")
```

**4. Long-Running Agents Timeout**
```python
# Increase timeout
os.environ["MLFLOW_DEPLOYMENT_PREDICT_TIMEOUT"] = "900"  # 15 minutes
```

## 📚 Additional Resources

### Official Documentation
- [MLflow ResponseAgent Docs](https://mlflow.org/docs/latest/genai/serving/responses-agent/)
- [LangGraph Documentation](https://langchain-ai.github.io/langgraph/)
- [MLflow Tracing](https://mlflow.org/docs/latest/genai/tracing/)

### Related Guides
- [Models from Code](https://mlflow.org/docs/latest/models.html#models-from-code)
- [MLflow Deployment](https://mlflow.org/docs/latest/models.html#built-in-deployment-tools)
- [OpenAI Responses API](https://platform.openai.com/docs/api-reference/responses)

## 🤝 Contributing

Suggestions and improvements welcome! Key areas:
- Additional agent patterns
- More tool examples
- Advanced LangGraph workflows
- Production deployment guides

## 📄 License

This educational material is provided as-is for learning purposes.

## 🙋 Support

For issues or questions:
1. Check MLflow documentation
2. Review notebook comments
3. Check MLflow GitHub issues
4. Consult Databricks community forums

## 🎓 Learning Path

**Recommended order**:
1. ✅ Complete installation (Notebook 01)
2. ✅ Understand ResponseAgent basics (Notebook 02)
3. ✅ Learn LangGraph integration (Notebook 03)
4. ✅ Build tool-calling agents (Notebook 04)
5. 🚀 Build your own production agent!

---

**Happy Agent Building! 🤖**

For more information about Databricks and MLflow, visit:
- [Databricks MLflow](https://docs.databricks.com/mlflow/index.html)
- [Mosaic AI Agent Framework](https://docs.databricks.com/generative-ai/agent-framework/)
