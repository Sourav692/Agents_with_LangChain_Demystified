# MLflow ResponseAgent Tutorial - Complete Package

## 📦 Package Contents

This package contains 4 comprehensive Jupyter notebooks covering MLflow ResponseAgent with LangGraph integration:

### Notebooks Included:

1. **01_mlflow_installation_mac.ipynb** (6.5 KB)
   - Complete installation guide for macOS
   - Environment setup
   - Dependency management
   - Verification steps

2. **02_responses_agent_basics.ipynb** (15 KB)
   - ResponseAgent fundamentals
   - Why it's needed
   - Basic implementations
   - Request/Response patterns

3. **03_langgraph_integration.ipynb** (20 KB)
   - Building LangGraph agents
   - Wrapping with ResponseAgent
   - Deployment strategies
   - Multi-turn conversations

4. **04_tool_calling_agent.ipynb** (27 KB)
   - Production tool-calling patterns
   - Weather and calculator tools
   - Iterative agent loop
   - Full tracing implementation

5. **README.md** (9.2 KB)
   - Complete documentation
   - Quick start guide
   - Troubleshooting
   - Resources

## 🎯 Key Concepts Covered

### What is ResponseAgent?

ResponseAgent is MLflow's **framework-agnostic** interface for serving AI agents with:
- **OpenAI API compatibility** - Works with any OpenAI-compatible client
- **Tool calling support** - Built-in function execution framework
- **Multi-agent orchestration** - Support for complex agent workflows
- **Full tracing** - Integrated MLflow observability
- **Easy deployment** - Log once, deploy anywhere

### Why Use ResponseAgent?

#### Traditional Approach Problems:
- ❌ Framework lock-in (can't switch between LangGraph, LangChain easily)
- ❌ No standard API (each agent has custom input/output)
- ❌ Difficult deployment (complex serialization)
- ❌ Poor observability (hard to debug multi-step agents)
- ❌ No multi-agent support

#### ResponseAgent Solutions:
- ✅ Framework independence (wrap any implementation)
- ✅ Standard OpenAI-compatible API
- ✅ Models-from-Code deployment
- ✅ Built-in tracing and monitoring
- ✅ Multi-agent ready

## 🚀 Quick Start

### Prerequisites
```bash
# Required
- macOS
- Python 3.8+
- OpenAI API key
```

### Installation (5 minutes)
```bash
# Install MLflow and dependencies
pip install mlflow[genai] pydantic>=2.0.0 langgraph>=0.2.27 \
    langchain>=0.3.0 langchain-openai>=0.2.0 openai \
    python-dotenv backoff

# Create .env file
echo "OPENAI_API_KEY=your_key_here" > .env

# Start MLflow UI (optional)
mlflow ui
```

### Run Notebooks
1. Open Jupyter: `jupyter notebook`
2. Follow notebooks in order (01 → 04)
3. Execute cells sequentially

## 📊 ResponseAgent Benefits for LangGraph

### Why Wrap LangGraph with ResponseAgent?

| Challenge | Without ResponseAgent | With ResponseAgent |
|-----------|----------------------|-------------------|
| **Deployment** | Custom serialization logic | Log with mlflow.pyfunc |
| **API Format** | LangGraph-specific | OpenAI-compatible |
| **Observability** | Manual tracing setup | Auto tracing |
| **Versioning** | Git only | Full MLflow tracking |
| **Serving** | Custom server code | MLflow models serve |
| **Multi-framework** | Lock-in to LangGraph | Switch frameworks easily |

### Real-World Use Cases

1. **Production Chatbots**
   - Deploy to Databricks Model Serving
   - OpenAI SDK compatibility
   - Automatic scaling

2. **Tool-Calling Agents**
   - API integrations (weather, databases, etc.)
   - Function execution tracking
   - Error handling and retries

3. **Multi-Agent Systems**
   - Research agent + writer agent + reviewer agent
   - Coordinated workflows
   - Intermediate result storage

4. **Enterprise Applications**
   - Standardized deployment across teams
   - Version control and rollback
   - Audit trails and compliance

## 💡 Code Examples

### Basic ResponseAgent
```python
from mlflow.pyfunc import ResponsesAgent
from mlflow.types.responses import ResponsesAgentRequest, ResponsesAgentResponse

class SimpleAgent(ResponsesAgent):
    @mlflow.trace(span_type=SpanType.AGENT)
    def predict(self, request: ResponsesAgentRequest) -> ResponsesAgentResponse:
        user_msg = request.input[-1].content
        return ResponsesAgentResponse(
            output=[self.create_text_output_item(
                text=f"Echo: {user_msg}",
                id="msg_1"
            )]
        )
```

### LangGraph Wrapper
```python
class LangGraphResponsesAgent(ResponsesAgent):
    def __init__(self, agent: CompiledStateGraph):
        self.agent = agent
    
    def predict_stream(self, request):
        cc_msgs = to_chat_completions_input([i.model_dump() for i in request.input])
        for _, events in self.agent.stream({"messages": cc_msgs}):
            for node_data in events.values():
                yield from output_to_responses_items_stream(node_data["messages"])
```

### Tool-Calling Agent
```python
class ToolCallingAgent(ResponsesAgent):
    def __init__(self, model, tools):
        self.model = model
        self.tools = {t.name: t for t in tools}
    
    @mlflow.trace(span_type=SpanType.TOOL)
    def execute_tool(self, tool_name, args):
        return self.tools[tool_name].exec_fn(**args)
    
    # ... agent loop implementation
```

## 📁 File Structure

```
mlflow_responseagent_notebooks/
├── README.md                              # Complete documentation
├── 01_mlflow_installation_mac.ipynb      # Installation guide
├── 02_responses_agent_basics.ipynb       # Fundamentals
├── 03_langgraph_integration.ipynb        # LangGraph wrapper
└── 04_tool_calling_agent.ipynb           # Production patterns
```

## 🔧 Installation Commands

### Mac Installation
```bash
# Using pip
pip install mlflow[genai] --upgrade

# Core dependencies for ResponseAgent
pip install pydantic>=2.0.0  # Required for ResponseAgent
pip install openai           # For LLM calls

# LangGraph integration
pip install langgraph>=0.2.27
pip install langchain>=0.3.0
pip install langchain-openai>=0.2.0

# Utilities
pip install backoff          # Retry logic
pip install python-dotenv    # Environment variables
```

### Start MLflow Server
```bash
# Local file-based tracking
mlflow ui --backend-store-uri file://~/mlflow_experiments

# Access UI at http://localhost:5000
```

## 🎓 Learning Path

### Beginner (Notebook 01-02)
- Install MLflow and dependencies
- Understand ResponseAgent basics
- Create simple agents
- Log and load models

### Intermediate (Notebook 03)
- Build LangGraph agents
- Wrap with ResponseAgent
- Handle multi-turn conversations
- View execution traces

### Advanced (Notebook 04)
- Implement tool calling
- Build production workflows
- Handle complex tool chains
- Deploy to production endpoints

## 🔍 Key Features Demonstrated

### 1. Framework Independence
✅ Use any agent framework (LangGraph, LangChain, custom)
✅ Switch frameworks without changing deployment

### 2. Standard API
✅ OpenAI Responses API compatibility
✅ Works with OpenAI SDK and UIs

### 3. Tool Calling
✅ Function calling support
✅ Automatic tool execution
✅ Full tracing of tool invocations

### 4. Observability
✅ MLflow tracing integration
✅ Token usage tracking
✅ Execution time monitoring

### 5. Production Ready
✅ Models-from-Code deployment
✅ Easy serving with MLflow
✅ Version control and rollback

## 📚 Additional Resources

### Official Documentation
- [MLflow ResponseAgent](https://mlflow.org/docs/latest/genai/serving/responses-agent/)
- [LangGraph Guide](https://langchain-ai.github.io/langgraph/)
- [MLflow Tracing](https://mlflow.org/docs/latest/genai/tracing/)

### Community
- [MLflow GitHub](https://github.com/mlflow/mlflow)
- [Databricks Community](https://community.databricks.com/)

## ⚠️ Important Notes

### Requirements
- **Pydantic v2+** is required for ResponseAgent
- **OpenAI API key** needed for examples
- **Python 3.8+** for compatibility

### Costs
- OpenAI API calls incur costs
- Examples use `gpt-4o-mini` (cost-effective)
- Can substitute with local models

### Mac-Specific
- Installation tested on macOS
- Should work on Linux with minor adjustments
- Windows may need WSL

## 🎯 What You'll Learn

By completing these notebooks, you will:

1. ✅ Install and configure MLflow for agent development
2. ✅ Understand ResponseAgent architecture and benefits
3. ✅ Build and deploy LangGraph agents
4. ✅ Implement production tool-calling patterns
5. ✅ Use MLflow tracing for observability
6. ✅ Deploy agents with standard APIs

## 🚀 Next Steps After Tutorial

1. **Build Your Own Agent**
   - Start with notebook templates
   - Add your custom tools
   - Deploy to MLflow server

2. **Explore Advanced Patterns**
   - Multi-agent systems
   - Streaming responses
   - Custom tool frameworks

3. **Production Deployment**
   - Deploy to Databricks Model Serving
   - Set up monitoring and alerts
   - Implement A/B testing

## 📞 Support

For questions or issues:
1. Review notebook comments and markdown cells
2. Check [MLflow documentation](https://mlflow.org/docs/)
3. Visit [GitHub issues](https://github.com/mlflow/mlflow/issues)

---

**Created**: January 2026
**MLflow Version**: Latest (2.x+)
**Target Audience**: Data Scientists, ML Engineers, Solution Architects

**Ready to build production AI agents! 🤖**
