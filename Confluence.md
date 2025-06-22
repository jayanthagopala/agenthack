# Google Agenthack


## Hackathon Overview

**Google Agenthack** was a specialized hackathon at Google designed for fintech companies. The event focused on **Agentic AI** - using  agents to automate previously manual financial processes. The hackathon provided hands-on experience with Google's Agent Development Kit (ADK) and showcased the potential of multi-agent systems in financial services.

### Key Statistics
- **Focus**: Agentic AI and financial automation
- **Platform**: Google Cloud AI Platform with ADK
- **Challenge**: Build AI agents for Moneypenny's Bank

---

## What Google Has to Offer

Google provided access to AI agent development and deployment:

### 1. Agent Development Kit (ADK)
> **Official Docs**: [google.github.io/adk-docs](https://google.github.io/adk-docs/)

**ADK** is Google's flexible and modular framework for developing AI agents. Key features include:

#### Core Agent Types
- **LLM Agents**: Intelligent reasoning with Large Language Models (Gemini)
- **Workflow Agents**: Structured execution flow (Sequential, Parallel, Loop)
- **Custom Agents**: Specialized business logic and integrations

#### Key Capabilities
- ✅ **Multi-Agent Orchestration**: Hierarchical agent coordination
- ✅ **Rich Tool Ecosystem**: Built-in tools + custom functions
- ✅ **Session Management**: Persistent conversations and state
- ✅ **Deployment Flexibility**: Local, Cloud Run, GKE, Agent Engine
- ✅ **Built-in Evaluation**: Performance assessment framework
- ✅ **Enterprise Security**: Trustworthy agent patterns

#### Technology Stack
- **AI Platform**: Google Cloud Vertex AI
- **Models**: Gemini 2.5 Flash
- **Languages**: Python 3.8+ (v1.0.0), Java (v0.1.0)
- **Deployment**: Google Cloud Agent Engine

---

## The Hackathon Challenge: Moneypenny's Bank Agent System

The hackathon provided a **comprehensive starter codebase** for **Moneypenny's Bank** - a fictional bank requiring AI automation across three critical areas. This codebase was shared with participants at the start of the hackathon, complete with detailed README files and inline comments explaining the challenge requirements and implementation guidance.

### Setup Requirements

**Important**: To run this codebase, participants needed to configure several API keys:

- **Google Cloud Project ID**: For Vertex AI and Gemini model access
- **Google Maps API Key**: Required for geographic risk assessment in the AML agent
- **Moneypenny's Bank API**: Provided by hackathon organizers (`https://api.agenthack.uk/api`)

The codebase came with detailed setup instructions and configuration templates, with comments throughout explaining the challenge objectives and implementation approach.

### Challenge Documentation

The provided codebase included extensive documentation:
- **README files**: Detailed explanations of each agent's purpose and sub-components
- **Inline comments**: Step-by-step guidance on what needed to be implemented
- **Configuration examples**: Template files showing required environment variables
- **API integration patterns**: Examples of how to connect to banking and external services

### System Architecture

```
Moneypenny's Bank AI System
├── Financial Concierge Agent (Customer Service)
├── Underwriting Agent (Loan Processing)
└── AML Agent (Anti-Money Laundering)
```

### 1. Financial Concierge Agent 
**Purpose**: Customer service and financial guidance

**Key Capabilities**:
- Account balance and transaction history
- Spending pattern analysis and budgeting advice
- Credit card eligibility assessment
- Savings goals management
- General banking FAQ support

**Sub-Agent Architecture**:
- `account_data_agent`: Account details and transaction history
- `credit_eligibility_agent`: Credit card product recommendations
- `spending_advisor_agent`: Personalized budgeting advice
- `savings_goal_advisor_agent`: Savings goal management
- `faq_agent`: Banking knowledge base

**Example Queries**:
- "What's my account balance?"
- "Help me create a savings goal for a vacation"
- "Am I eligible for a credit card?"
- "Analyze my spending patterns"

### 2. Underwriting Agent 
**Purpose**: Automated loan application processing

**Supported Loan Types**:
- Personal home loans
- Mortgages
- Business loans

**Process Flow**:
1. **Application Intake**: Identity verification and KYC
2. **Financial Analysis**: Income, expenses, DTI ratio calculation
3. **Credit Risk Assessment**: External credit reports, fraud checks
4. **Loan Structuring**: Final approval decision and terms

**Sub-Agent Architecture**:
- `application_intake_agent`: KYC and application creation
- `financial_analysis_agent`: Financial health assessment
- `credit_risk_assessment_agent`: Credit and fraud evaluation
- `loan_structuring_agent`: Loan terms and approval decisions

**Integration Points**:
- External credit reporting APIs
- Fraud detection services
- Property valuation systems
- Business risk assessment tools

### 3. AML Agent 
**Purpose**: Anti-Money Laundering compliance and monitoring

**Analysis Capabilities**:
- **Transaction Pattern Analysis**: Structuring, unusual volumes
- **Geographic Risk Assessment**: High-risk jurisdictions
- **Entity Linkage Analysis**: Sanctions screening
- **Policy Alignment**: Risk scoring and recommendations

**Risk Assessment Levels**:
- **Low**: No action required
- **Medium**: Enhanced monitoring
- **High**: Enhanced Due Diligence (EDD)
- **Critical**: Consider SAR filing

**Sub-Agent Architecture**:
- `transaction_pattern_analysis_agent`: Suspicious pattern detection
- `geographic_risk_assessment_agent`: Country risk evaluation
- `entity_linkage_analysis_agent`: Sanctions and watchlist screening
- `aml_policy_alignment_agent`: Policy compliance and risk scoring

---

## Technical Implementation

### Multi-Agent System Design

The hackathon challenge showcased **hierarchical multi-agent orchestration**:

```
Main Coordinators (LLM Agents)
├── Financial Concierge Agent
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
- **Dynamic Routing**: LLM agents decide which sub-agents to call
- **Sequential Processing**: AML agent processes through analysis stages
- **Parallel Execution**: Multiple risk assessments run simultaneously
- **Tool Integration**: Banking APIs, external services, custom functions

### Development Experience

#### Getting Started
```bash
# Install ADK and dependencies
pip install google-adk
pip install -r requirements.txt

# Launch ADK web interface
adk web

# Or run from command line
adk run financial_concierge
adk run underwriting_agent
adk run aml_agent
```

#### Key Development Tools
- **ADK Web Interface**: Interactive agent testing at `http://localhost:8000`
- **Multi-Agent Testing**: Test individual agents or full workflows
- **Mock API Integration**: Realistic banking API simulation
- **Real-time Debugging**: Built-in evaluation and performance assessment

---

## Key Learnings and Insights

### 1. Multi-Agent Orchestration
- **Coordinator Pattern**: Main agents orchestrate specialized sub-agents
- **Context Passing**: Seamless data flow between agent layers
- **Parallel Processing**: Efficiency gains through concurrent agent execution

### 2. Fintech-Specific Challenges
- **Regulatory Compliance**: AML and KYC requirements built into agent logic
- **Data Sensitivity**: Proper handling of PII and financial data
- **Risk Assessment**: Multi-dimensional risk evaluation across agents

### 3. ADK Capabilities
- **Rapid Prototyping**: Quick agent development and testing
- **Production Ready**: v1.0.0 with enterprise deployment options
- **Flexible Architecture**: Support for LLM, Workflow, and Custom agents

### 4. Enterprise Integration
- **API-First Design**: Clean separation between agent logic and data access
- **Scalable Architecture**: Ready for cloud deployment
- **Security Patterns**: Built-in trustworthy agent behavior

---

## Future Opportunities

### Immediate Next Steps
1. **Production Deployment**: Scale with Google Cloud Agent Engine
2. **Enterprise Integration**: Connect to real banking systems and APIs
3. **Advanced Analytics**: Enhanced risk models and pattern detection

### Enterprise Expansion
- **Agentspace Enterprise**: Deploy as company-wide AI platform
- **Multi-tenant Architecture**: Support multiple business units
- **Advanced Connectors**: Integration with existing enterprise systems

### Industry Applications
- **Regulatory Reporting**: Automated compliance documentation
- **Customer Experience**: 24/7 intelligent financial assistance
- **Risk Management**: Real-time fraud and AML monitoring

---

## Google Contact Information

**For Enterprise Inquiries**:
- **Email**: fintech@google.com
- **Team**: Google Cloud UKI Fintech Team
- **Lead**: Arham Khan

**Learning Resources**:
- [ADK Documentation](https://google.github.io/adk-docs/)
- [Agentspace Enterprise](https://cloud.google.com/agentspace/agentspace-enterprise/docs/overview)
- [Vertex AI Agent Builder](https://cloud.google.com/blog/products/ai-machine-learning/rag-and-grounding-on-vertex-ai)

---
