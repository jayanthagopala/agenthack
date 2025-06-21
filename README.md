# Moneypenny's Bank Agent System

*A comprehensive AI-powered banking system built for the hackathon*

## Overview

This project implements a multi-agent banking system for Moneypenny's Bank, featuring three specialized AI agents that handle different aspects of financial services:

- **Financial Concierge Agent**: Personal financial assistant for customer queries
- **Underwriting Agent**: Automated loan application processing and approval
- **AML Agent**: Anti-Money Laundering detection and compliance monitoring

## System Architecture

The system is built using Google's [Agent Development Kit (ADK)](https://google.github.io/adk-docs/), a flexible and modular framework for developing and deploying AI agents. Our implementation follows a **hierarchical multi-agent system** with specialized agent types:

### ADK Agent Types Used

- **LLM Agents**: Use Large Language Models (Gemini) for reasoning, natural language processing, and dynamic decision making
- **Workflow Agents**: Control execution flow of other agents in predictable patterns (Sequential, Parallel, Loop)
- **Custom Agents**: Implement specialized business logic and integrations unique to banking operations

### Multi-Agent Hierarchy

```
Main Coordinators (LLM Agents)
├── Financial Concierge Agent (Customer Service)
│   ├── Account Data Agent (Custom)
│   ├── Credit Eligibility Agent (LLM + Custom)
│   ├── Spending Advisor Agent (LLM)
│   ├── Savings Goal Advisor Agent (LLM + Custom)
│   └── FAQ Agent (LLM)
├── Underwriting Agent (Workflow + LLM)
│   ├── Application Intake Agent (LLM + Custom)
│   ├── Financial Analysis Agent (LLM + Custom)
│   ├── Credit Risk Assessment Agent (Custom)
│   └── Loan Structuring Agent (LLM + Custom)
└── AML Agent (Sequential Workflow)
    ├── Transaction Pattern Analysis Agent (Custom + LLM)
    ├── Geographic Risk Assessment Agent (Custom)
    ├── Entity Linkage Analysis Agent (Custom)
    └── AML Policy Alignment Agent (LLM)
```

### Agent Orchestration Patterns

- **Dynamic Routing**: LLM agents decide which sub-agents to call based on user queries
- **Sequential Processing**: AML agent processes through analysis stages in order
- **Parallel Execution**: Multiple risk assessments run simultaneously
- **Tool Integration**: Agents equipped with banking APIs, external services, and custom functions

## Technology Stack

- **Agent Framework**: [Google Agent Development Kit (ADK) v1.0.0](https://google.github.io/adk-docs/) - Production-ready agent development
- **AI Platform**: Google Cloud Vertex AI with ADK integration
- **AI Models**: Gemini 2.5 Flash (via Vertex AI) - Advanced reasoning and function calling
- **Agent Engine**: Google Cloud Agent Engine for deployment and scaling
- **APIs**: Google Maps API, Moneypenny's Bank API, Vertex AI APIs
- **Languages**: Python 3.8+ (Java ADK v0.1.0 also available)
- **Dependencies**: See `requirements.txt`

### ADK Key Features Used

- **Multi-Agent Orchestration**: Hierarchical agent coordination and delegation
- **Tool Integration**: Rich ecosystem of built-in tools and custom functions  
- **Session Management**: Persistent conversations and state management
- **Deployment Flexibility**: Local development, Cloud Run, GKE, or Agent Engine
- **Enterprise Integration**: Can be deployed with Agentspace Enterprise for organization-wide agent access
- **Built-in Evaluation**: Systematic assessment of agent performance
- **Safety & Security**: Built-in patterns for trustworthy agent behavior

## Quick Start

### Prerequisites

1. **Python 3.8+** installed
2. **Google Cloud Account** with Vertex AI enabled
3. **Google Cloud CLI** installed and configured
4. **Google Maps API Key** (for geographic risk assessment)
5. **Moneypenny's Bank API Access** (provided by hackathon organizers)

### Installation & ADK Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd agenthack
   ```

2. **Set up Google Cloud authentication**
   ```bash
   # Install/update gcloud CLI
   gcloud components update
   
   # Authenticate with Google Cloud
   gcloud auth application-default login
   ```

3. **Create and activate virtual environment**
   ```bash
   # Create virtual environment
   python -m venv .venv
   
   # Activate (choose based on your OS)
   # macOS/Linux:
   source .venv/bin/activate
   # Windows CMD:
   .venv\Scripts\activate.bat
   # Windows PowerShell:
   .venv\Scripts\Activate.ps1
   ```

4. **Install dependencies**
   ```bash
   # Install ADK and other dependencies
   pip install google-adk
   pip install -r requirements.txt
   ```

5. **Configure environment variables**
   
   Create `.env` files in each agent directory with:
   ```bash
   # Google Cloud Configuration
   GOOGLE_CLOUD_PROJECT="your-project-id"
   GOOGLE_CLOUD_LOCATION="us-central1"  # or your preferred region
   GOOGLE_GENAI_USE_VERTEXAI="True"
   
   # Project Configuration
   MONEYPENNY_API_BASE_URL="https://api.agenthack.uk/api"
   GOOGLE_MAPS_API_KEY="your-google-maps-api-key"
   ADK_SERVER_URL="http://localhost:8000"
   ```

6. **Update configuration files**
   - Edit `config.py` to add your Google Maps API key
   - Update team credentials in `submit_aml_agent.py` (lines 8-9)
   - Ensure your Google Cloud project ID is set correctly

### Running the System

#### Option 1: ADK Web Interface (Recommended for Development)

Launch the ADK developer web interface to interact with agents:

```bash
# From the project root directory
adk web
```

Then open your browser to `http://localhost:8000` and select the agent you want to test.

#### Option 2: ADK Command Line Interface

Run agents directly from the command line:

```bash
# Test individual agents
adk run financial_concierge
adk run underwriting_agent  
adk run aml_agent
```

#### Option 3: Deploy Individual Agents

Each agent can be deployed separately:

```bash
# Deploy Financial Concierge
cd financial_concierge/deployment
python deploy.py

# Deploy Underwriting Agent
cd underwriting_agent
python agent.py

# Deploy AML Agent
cd aml_agent
python agent.py
```

#### Option 4: Submit Tasks (Hackathon Mode)

For hackathon task submission:

```bash
python submit_aml_agent.py
```

#### Option 5: Enterprise Deployment (Future)

For enterprise deployment, this system can be integrated with [Google Agentspace Enterprise](https://cloud.google.com/agentspace/agentspace-enterprise/docs/overview):

- **Company-wide Access**: Deploy as organization-branded multimodal search agents
- **Data Integration**: Connect to enterprise systems (Salesforce, Jira, Confluence, SharePoint)
- **Access Control**: SSO authentication with user-level permissions
- **Custom Agents**: Use Agentspace Enterprise Plus for specialized banking workflows

## Agent Capabilities

### Financial Concierge Agent

**Purpose**: Customer service and financial guidance

**Key Features**:
- Account balance and transaction history
- Spending pattern analysis and budgeting advice
- Credit card eligibility assessment
- Savings goals management
- General banking FAQ support

**Example Queries**:
- "What's my account balance?"
- "Help me create a savings goal for a vacation"
- "Am I eligible for a credit card?"
- "Analyze my spending patterns"

### Underwriting Agent

**Purpose**: Automated loan application processing

**Key Features**:
- Personal, mortgage, and business loan processing
- Identity verification and KYC
- Financial health analysis
- Credit risk assessment
- Loan structuring and approval decisions

**Supported Loan Types**:
- Personal home loans
- Mortgages
- Business loans

**Process Flow**:
1. Application intake and identity verification
2. Financial analysis (income, expenses, DTI ratio)
3. Credit risk assessment (external credit reports, fraud checks)
4. Loan structuring and final decision

### AML Agent

**Purpose**: Anti-Money Laundering compliance and monitoring

**Key Features**:
- Transaction pattern analysis (structuring, unusual volumes)
- Geographic risk assessment (high-risk jurisdictions)
- Entity linkage analysis (sanctions screening)
- Policy alignment and risk scoring

**Risk Assessment Levels**:
- **Low**: No action required
- **Medium**: Enhanced monitoring
- **High**: Enhanced Due Diligence (EDD)
- **Critical**: Consider SAR filing

## Configuration

### Google Cloud Setup

Before running the agents, ensure your Google Cloud project is properly configured:

1. **Enable required APIs**:
   - Vertex AI API
   - Generative AI API (if using Gemini)

2. **Set up billing** for your Google Cloud project

3. **Configure IAM permissions** for Vertex AI access

### API Endpoints

The system integrates with various APIs:

- **Vertex AI**: Gemini 2.5 Flash model via Google Cloud
- **Bank API**: `https://api.agenthack.uk/api`
- **External Services**: Credit reports, fraud checks, property valuation
- **Google Maps**: Geographic risk assessment

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `MONEYPENNY_API_BASE_URL` | Base URL for bank API | `https://api.agenthack.uk/api` |
| `GOOGLE_MAPS_API_KEY` | Google Maps API key | *Required* |
| `ADK_SERVER_URL` | ADK server URL | `http://localhost:8000` |

## Testing

Run the test suite:

```bash
pytest
```

For async tests:
```bash
pytest-asyncio
```

## Development Notes

### Current Status

- All agents are fully implemented using ADK v1.0.0
- Multi-agent system with LLM, Workflow, and Custom agents
- Sub-agent orchestration working with dynamic routing
- Mock API responses available for testing
- ADK web interface for development and debugging
- **Note**: Some backend endpoints return mock data
- **Note**: Google Maps API key needs to be configured

### Known Limitations

1. **Mock Data**: Some external service calls return mock responses
2. **API Keys**: Google Maps API key needs to be configured
3. **Backend Services**: Some endpoints are not fully implemented on the backend

### Team Credentials

Update these in `submit_aml_agent.py`:
- **Team Name**: "Algo Avengers"
- **Password**: "kR8sL2fP"
- **Task Number**: 3

## Contributing

For teammates working on this project:

1. **Code Structure**: Each agent follows the coordinator-sub-agent pattern
2. **API Client**: All HTTP calls go through `bank_api_client.py`
3. **Prompts**: Agent behavior is defined in `prompt.py` files
4. **Documentation**: Each agent has its own README with detailed documentation

### Key Files to Know

- `config.py`: Global configuration
- `submit_aml_agent.py`: Hackathon submission script
- `*/agent.py`: Main agent implementations
- `*/bank_api_client.py`: API integration layer
- `*/prompt.py`: Agent prompts and behavior

## Hackathon Submission

This system is designed for hackathon task submission. The `submit_aml_agent.py` script:

1. Fetches tasks from the hackathon API
2. Creates ADK sessions for each task
3. Processes tasks through the AML agent
4. Submits results back to the evaluation system

## Troubleshooting

### Common Issues

1. **API Connection**: Check `MONEYPENNY_API_BASE_URL` is correct
2. **Google Maps**: Ensure API key is valid and has Geocoding API enabled
3. **Dependencies**: Run `pip install -r requirements.txt` again
4. **ADK Server**: Ensure ADK server is running on configured port

### Debug Mode

Enable verbose logging by setting environment variable:
```bash
export DEBUG=1
```

---

## Hackathon Context

This project was developed during the **Google AgentHack hackathon** - a day of innovation and exploration into Agentic AI. The event focused on automating previously manual tasks using AI agents and showcased the power of Google Cloud's Agent Development Kit (ADK).

### Learning Resources

The Google Cloud team provided these valuable resources for continued learning:

**Core ADK Resources:**
- [**ADK & Agentspace Complete Guide**](./ADK_AND_AGENTSPACE_GUIDE.md) - **Comprehensive platform comparison and integration guide**
- [ADK Introduction](https://developers.googleblog.com/en/agent-development-kit-easy-to-build-multi-agent-applications) - Getting started with Agent Development Kit
- [ADK Quickstart](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-development-kit/quickstart) - Step-by-step setup guide
- [ADK Documentation](https://google.github.io/adk-docs/) - Complete technical documentation (v1.0.0 Python, v0.1.0 Java)
- [Agent Types Guide](https://google.github.io/adk-docs/agents/) - LLM, Workflow, and Custom agents explained

**Google Cloud AI Platform:**
- [Vertex AI Colab Enterprise](https://cloud.google.com/blog/products/ai-machine-learning/vertex-ai-colab-enterprise-and-mlops) - MLOps and collaboration
- [Vertex AI Agent Builder](https://cloud.google.com/blog/products/ai-machine-learning/rag-and-grounding-on-vertex-ai) - RAG and grounding techniques
- [Vertex AI Search](https://cloud.google.com/generative-ai-app-builder/docs/enterprise-search-introduction) - Enterprise search capabilities

**Development Tools:**
- [Google AI Studio](https://ai.google.dev/gemini-api/docs/ai-studio-quickstart) - Gemini API development
- [Agentspace Enterprise](https://cloud.google.com/agentspace/agentspace-enterprise/docs/overview) - Enterprise AI agents and search platform

### Next Steps

For productionalizing this solution or exploring AI Agents further:

**Enterprise Deployment Options:**
- **ADK + Agent Engine**: Scale individual agents with Google Cloud Agent Engine
- **Agentspace Enterprise**: Deploy as company-wide AI search and agent platform
- **Custom Integration**: Build on Google Cloud with Vertex AI and custom infrastructure

**Contact Information:**
- **Email**: fintech@google.com
- **Team**: Google Cloud UKI Fintech team
- **Lead**: Arham Khan

**Enterprise Features Available:**
- Multi-tenant agent deployment
- Enterprise data connectors (Salesforce, Jira, etc.)
- SSO and access control integration
- Blended RAG over multiple data sources
- Real-time feedback and analytics

## Team Contact

For questions or issues, reach out to the team:
- **Team**: Algo Avengers
- **Project**: Moneypenny's Bank Agent System
- **Hackathon**: Google AgentHack (Google Cloud)

*Built with care using Google Cloud AI Platform and ADK*
