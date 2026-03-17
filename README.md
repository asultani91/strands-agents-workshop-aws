# 🤖 Strands Agents Workshop: Building Production-Ready AI Agents on AWS

A comprehensive, hands-on workshop covering the **Strands Agents SDK** - an open-source framework for building model-driven AI agents with minimal code. This project demonstrates how to create intelligent agents from simple chatbots to complex multi-agent systems deployed on AWS.

> **Duration:** Multi-day workshop (8 fundamental labs + 3 multi-agent labs + 2 deployment labs)
> **Target Audience:** Solution Architects, Software Designers, Developers
> **Prerequisites:** Python 3.10+, AWS Account, Amazon Bedrock access

---

## 📖 What is Strands Agents?

**Strands Agents** is an open-source SDK that takes a **model-driven approach** to building AI agents in just a few lines of code. Like the two strands of DNA, Strands connects two core pieces together: **the model and the tools**.

### Core Philosophy

The simplest agent consists of three components:
1. **A Model** (LLM for reasoning and decision-making)
2. **Tools** (Functions the agent can execute)
3. **A Prompt** (Instructions defining agent behavior)

The agent uses these components in an **agentic loop** - continuously reasoning, selecting tools, and executing actions until the task is complete.

---

## 🎯 Key Features

### 1️⃣ **Simplified Agent Development**
- Create fully functional agents with minimal code
- Rapid prototyping and iteration
- Focus on business logic, not infrastructure

### 2️⃣ **Flexible Tool Integration**
- **Built-in tools**: Calculator, current_time, retrieve (RAG), HTTP requests
- **Custom tools**: Use any Python function with `@tool` decorator
- **MCP (Model Context Protocol)**: Connect to external services and APIs

### 3️⃣ **Multi-Model Support**
- **Amazon Bedrock**: Claude, Nova, Llama models
- **Anthropic API**: Direct Claude access
- **Ollama**: Local model deployment
- **LiteLLM**: Unified interface for OpenAI, Mistral, Gemini
- **Custom Providers**: Build your own

### 4️⃣ **Advanced Multi-Agent Architectures**
- **Agent as Tool**: Hierarchical orchestration
- **Swarm**: Parallel processing with emergent intelligence
- **Graph**: Structured networks with explicit communication
- **Workflow**: Sequential/parallel task orchestration

### 5️⃣ **Enterprise-Ready Capabilities**
- AWS Lambda & Fargate deployment examples
- Streaming responses for real-time interactions
- OpenTelemetry (OTEL) integration for observability
- Amazon Bedrock Guardrails for content filtering
- Persistent memory with Mem0

---

## 🧪 Workshop Labs

### **FUNDAMENTALS (Labs 1-8)**

#### **Lab 1: Quick Start - Your First Agent**
**What I Built:**
- Simple conversational agent
- Custom tools using `@tool` decorator
- Calculator and weather forecast tools
- RecipeBot with web search capability

**Key Concepts:**
```python
from strands import Agent, tool

@tool
def weather():
    """Get weather"""
    return "sunny"

agent = Agent(
    tools=[calculator, weather],
    system_prompt="You're a helpful assistant."
)

response = agent("What is the weather today?")

Lab 2: Model Providers
What I Built:

Ollama agent running locally (Llama 3.2)
File operations agent (read, write, list directory)
OpenAI/Azure integration via LiteLLM

Supported Providers:
| Provider | Use Case |
|----------|----------|
| Amazon Bedrock | Managed AWS service with multiple models |
| Anthropic | Direct Claude API access |
| Ollama | Privacy-focused local deployment |
| LiteLLM | Unified interface for 100+ providers |
| Custom | Build your own provider |

Lab 3: Connecting with AWS Services
What I Built:

Restaurant booking assistant
DynamoDB integration for bookings
Amazon Bedrock Knowledge Base (RAG) for menu queries
Custom tools: create_booking, get_booking_details, delete_booking
Architecture:

User → Agent → Tools:
                ├── retrieve (Knowledge Base - restaurant menus)
                ├── current_time
                ├── create_booking (DynamoDB)
                ├── get_booking_details (DynamoDB)
                └── delete_booking (DynamoDB)
Lab 4: Model Context Protocol (MCP)
What I Built:

Agent connected to AWS Documentation MCP Server
Perplexity MCP Server integration for web search
Custom MCP server with calculator tools
MCP Transport Types:

stdio: Local integrations, command-line tools
Streamable HTTP: Stateless, server-based, supports SSE
Lab 5: Advanced Response Processing
What I Built:

Async iterators for streaming responses
Custom callback handlers for event processing
FastAPI integration with streaming endpoints
Method 1: Async Iterators

async def process_streaming_response():
    async for event in agent.stream_async("Calculate 2+2"):
        if "data" in event:
            print(event["data"])

Method 2: Callback Handlers

def custom_callback_handler(event_type, **kwargs):
    if "data" in kwargs:
        print(f"MODEL OUTPUT: {kwargs['data']}")

agent = Agent(callback_handler=custom_callback_handler)

Lab 6: Guardrails & Responsible AI
What I Built:

Solar Panels customer support agent
Amazon Bedrock Guardrails integration
Content filtering (PII, financial advice blocking)
Topic blocking and word filters
Guardrail Features:

Topic Policy (deny investment advice)
Content Policy (hate, violence, sexual content)
Word Policy (profanity blocking)
PII Protection (redact sensitive data)
Lab 7: Memory Persistent Agents
What I Built:

Personal agent with long-term memory
Mem0 integration (OpenSearch Serverless backend)
Web search tool with DuckDuckGo
Context-aware conversations across sessions
Memory Operations:
from strands_tools import mem0_memory

# Store information
memory_agent.tool.mem0_memory(
    action="store",
    content="The user's name is Ahmad.",
    user_id="ABC"
)

# Retrieve information
memory_agent.tool.mem0_memory(
    action="retrieve",
    query="What is the user's name?",
    user_id="ABC"
)

Lab 8: Observability & Evaluation
What I Built:

Restaurant assistant with Langfuse integration
RAGAS evaluation metrics
Trace collection and analysis
Score feedback loops
Observability Stack:

Agent → OpenTelemetry → Langfuse → Ragas Evaluation
         ↓                ↓            ↓
      Traces          Monitoring    Quality Scores
RAGAS Metrics Used:

AspectCritic: Binary evaluation (request completeness, brand tone)
RubricsScore: Multi-level scoring (food recommendations)
ContextRelevance: RAG retrieval quality
ResponseGroundedness: Factual accuracy
MULTI-AGENT SYSTEMS (Labs 9a-9c)
Lab 9a: Agent as Tool (Hierarchical)
What I Built:

Orchestrator agent managing 3 specialized agents:
Research Assistant: Factual information gathering
Product Recommendation Assistant: Personalized suggestions
Trip Planning Assistant: Travel itineraries
Architecture Pattern:

User → Orchestrator Agent → Research Assistant
                          → Product Recommender
                          → Trip Planner
Key Advantage: Clear separation of concerns with hierarchical delegation

Lab 9b: Swarm Intelligence
What I Built:

Native Swarm with 4 specialized agents:
Research Agent
Creative Agent
Critical Agent
Summarizer Agent
Swarm Features:

Self-organizing agent teams
Shared working memory
Autonomous handoffs between agents
Emergent collective intelligence
Configuration Parameters:
| Parameter | Default | Purpose |
|-----------|---------|---------|
| `max_handoffs` | 20 | Limit agent transfers |
| `max_iterations` | 20 | Cap total execution cycles |
| `execution_timeout` | 900s | Total runtime limit |
| `node_timeout` | 300s | Per-agent timeout |

Lab 9c: Agent Graph (DAG-Based)
What I Built:

Sequential pipeline (Team Lead → Analyst → Expert)
Parallel processing (Finance → Tech → Market → Risk)
Branching with conditions (Classifier → Technical/Business Report)
Graph Topologies:

Sequential Pipeline:
Agent A → Agent B → Agent C
Parallel Processing:
        ┌─→ Analyst ─┐
Lead ─→ │            ├─→ Summarizer
        └─→ Expert ──┘
Conditional Branching:
               ┌─→ Technical Report
Classifier ─→ ?
               └─→ Business Report
DEPLOYMENT (Labs 10a-10b)
Lab 10a: AWS Lambda Deployment
What I Deployed:

Restaurant booking agent as Lambda function
DynamoDB backend for bookings
Bedrock Knowledge Base integration
Session management with S3
CDK Stack Components:

Lambda function with Python 3.12
IAM roles for Bedrock and DynamoDB access
S3 bucket for session state
API Gateway integration
Lab 10b: AWS Fargate Deployment
What I Deployed:

Containerized agent on ECS Fargate
Application Load Balancer
Two endpoints:
/invoke - Standard responses
/invoke-streaming - Real-time streaming
Infrastructure:

Docker container with Strands agent
VPC with public/private subnets
ECS cluster with Fargate launch type
CloudWatch logging
🛠️ Technologies & Services Used
AWS Services
Amazon Bedrock (Claude, Nova models)
Amazon Bedrock Guardrails (content filtering)
Amazon Bedrock Knowledge Bases (RAG)
AWS Lambda (serverless functions)
AWS Fargate (containerized deployment)
Amazon DynamoDB (NoSQL database)
Amazon S3 (object storage)
Amazon OpenSearch Serverless (vector search)
AWS IAM (identity and access)
Amazon CloudWatch (monitoring)
Frameworks & Tools
Strands Agents SDK (core framework)
Strands Tools (pre-built tool library)
Mem0 (persistent memory)
Langfuse (observability platform)
RAGAS (evaluation framework)
MCP Protocol (Model Context Protocol)
OpenTelemetry (distributed tracing)
AWS CDK (infrastructure as code)
Foundation Models
Claude 3.5 Sonnet / Claude 4 Haiku (Anthropic)
Amazon Nova Pro/Premier (multimodal)
Llama 3.2 (Meta, via Ollama)
Titan Embeddings (vector embeddings)
📊 Use Cases Demonstrated
1. Restaurant Assistant (Single Agent)
Features:

Table reservations across multiple restaurants
Menu inquiries via RAG
Booking management (create, retrieve, delete)
Time-aware scheduling
2. Personal Assistant (Multi-Agent)
Features:

Calendar management with SQLite
Web search via Perplexity MCP
Development assistance (Python REPL, editor, shell)
Journal management
Agent Hierarchy:

Orchestrator: Routes tasks
Calendar Agent: Appointments, agendas
Coding Agent: Code execution, file editing
Search Agent: Real-time web information
🎯 When to Use Each Pattern
| Pattern | Best For | Example Use Cases |
|---------|----------|-------------------|
| **Single Agent** | Simple, focused tasks | Calculator, weather bot, FAQ chatbot |
| **Agent as Tool** | Hierarchical specialization | Customer service with escalation, content creation with editing |
| **Swarm** | Parallel brainstorming | Research analysis, problem exploration, consensus building |
| **Graph** | Structured workflows | Multi-level review, project management, layered processing |
| **Workflow** | Sequential/parallel pipelines | ETL operations, multi-stage document processing, data validation |

🎓 Learning Outcomes
By completing this workshop, I gained expertise in:

✅ Agent Fundamentals - Building agents from scratch with tools ✅ Multi-Model Integration - Working with Bedrock, Anthropic, Ollama, OpenAI ✅ AWS Service Integration - DynamoDB, Knowledge Bases, S3, Lambda ✅ MCP Protocol - Connecting to external services and APIs ✅ Responsible AI - Implementing guardrails and content filtering ✅ Advanced Processing - Streaming, async, callback handlers ✅ Persistent Memory - Long-term agent memory with Mem0 ✅ Observability - Tracing, logging, evaluation with Langfuse + RAGAS ✅ Multi-Agent Patterns - Swarm, Graph, Agent-as-Tool, Workflow ✅ Production Deployment - Lambda, Fargate, containerization ✅ Performance Evaluation - RAG metrics, agent quality scoring

📸 Screenshots & Diagrams
The project includes comprehensive diagrams for:

Agentic Loop (Model, tools, and prompt interaction cycle)
Calculator Agent (Local environment with AWS Bedrock LLM)
Customer Support Agent (Multi-tool system with guardrails)
Memory Agent (Mem0 integration with OpenSearch)
Restaurant Assistant (Knowledge Base + DynamoDB architecture)
Swarm Architecture (Mesh topology with 4 specialized agents)
Sequential Communication (Research → Summary → Response)
Orchestrator Pattern (Hierarchical agent delegation)
Parallel Processing Graph (Finance/Tech/Market/Risk analysts)
Conditional Branching (Classifier routing to specialized reporters)
Lambda Deployment (Serverless agent with S3 session management)
Fargate Deployment (Containerized agent with ALB)
All diagrams are stored in the /images folder.

🚀 Setup Requirements
AWS Prerequisites
# Enable Bedrock models
- Claude 3.5 Sonnet / Claude 4 Haiku
- Amazon Nova Pro / Premier
- Titan Embeddings

# IAM Permissions Required
- AmazonBedrockFullAccess
- AmazonSageMakerFullAccess
- DynamoDB full access
- S3 read/write access
- Lambda execution
- CloudFormation deployment

Local Environment
# Install Strands
pip install strands-agents strands-agents-tools

# Install dependencies
pip install boto3 duckduckgo-search nest-asyncio

# For Ollama (optional)
ollama pull llama3.2:latest
ollama serve

📚 Additional Resources
Strands Documentation
API Reference
GitHub Repository
Model Context Protocol
Amazon Bedrock Documentation
Langfuse Platform
RAGAS Evaluation Framework
🏁 Summary
This comprehensive workshop demonstrates how Strands Agents SDK provides everything needed to build AI agents from simple chatbots to sophisticated multi-agent systems. By combining:

Model flexibility (Bedrock, Anthropic, Ollama, OpenAI)
Tool extensibility (custom tools, MCP, built-in functions)
Multi-agent patterns (Swarm, Graph, Agent-as-Tool, Workflow)
AWS integration (DynamoDB, Knowledge Bases, Lambda, Fargate)
Enterprise features (Guardrails, observability, evaluation, memory)
I created production-ready, responsible, and observable agentic systems suitable for real-world enterprise deployments.
