# Agentic-system-design
Detailed notes for 'Agentic system design' course on educative.io


# Agentic System Design Course - Chapter 1: Agent Design Fundamentals

**Course:** Agentic System Design (Educative.io)  
**Chapter:** Agent Design Fundamentals

---

## Table of Contents

1. [Introduction to AI Agents](#1-introduction-to-ai-agents)
2. [Agent Architecture: Core Agent Components](#2-agent-architecture-core-agent-components)
3. [Agent Architecture: Components Interaction and Agent Memory](#3-agent-architecture-components-interaction-and-agent-memory)
4. [Structuring Agent Behavior: Agent Orchestration Patterns](#4-structuring-agent-behavior-agent-orchestration-patterns)
5. [Building Trustworthy Agents: Guardrails and Human Oversight](#5-building-trustworthy-agents-guardrails-and-human-oversight)
6. [Key Challenges and Design Strategies in Agentic AI Systems](#6-key-challenges-and-design-strategies-in-agentic-ai-systems)

---

## 1. Introduction to AI Agents

### 1.1 Core Definition

**AI agents** are systems that can perceive their environment, make decisions, and act autonomously to achieve specific goals following the **'perceive-reason-act'** paradigm.

![AI Agent Perceive-Reason-Act Cycle](diagrams/perceive-reason-act.png)

### 1.2 Three Fundamental Capabilities

#### Perception
- Sensing and extracting meaningful information from the environment
- Sources: text, images, audio, sensor data

#### Reasoning and Planning
- Understanding context and selecting actions
- Planning steps toward goals using LLMs for language-based reasoning

#### Action Execution
- Taking concrete actions based on reasoning
- Examples: API calls, sending messages, controlling devices

### 1.3 Key Characteristics of AI Agents

| **Feature** | **Description** |
|------------|----------------|
| **Autonomy** | Acts independently without continuous human intervention |
| **Goal-Oriented Behavior** | Directs actions toward achieving predefined objectives |
| **Perception & Feedback Loop** | Observes environment and adjusts based on outcomes |
| **Continuity** | Maintains memory/context over time for multi-turn reasoning |
| **Flexibility** | Can revise plans when objectives or context change |

### 1.4 AI Models vs. AI Agents

![AI Model vs AI Agent Comparison](diagrams/model-vs-agent.png)

| **Feature** | **AI Model** | **AI Agent** |
|------------|-------------|--------------|
| **Scope** | Narrow task | Broader system of behavior |
| **Role** | Computes outputs from inputs | Chooses actions in pursuit of goals |
| **Context Awareness** | Limited to current inference window | Maintains and updates internal context |
| **Initiative** | Waits for input | Acts autonomously when triggered |
| **Tool Use** | No | Yes, often includes multiple tools and models |
| **Example** | Sentiment classifier | Customer support assistant that answers, escalates, and logs tickets |

**Key Difference:** AI models are passive components that wait for input and compute outputs. AI agents are active systems that use models as components, maintain context, take initiative, and operate over time in a perception-reason-action loop.

### 1.5 Three Categories of AI Agents

#### 1.5.1 Software-Based Agents (Sandbox Environment)

![Software-Based Agent](diagrams/software-agent.png)

**Description:** Operate entirely in digital spaces through APIs, web interfaces, databases

**Examples:**
- Chatbots providing customer service
- Email triage agents
- Trading bots monitoring financial news

**Key Characteristics:**
- No physical sensors or hardware
- Act through code, interfaces, and digital data
- Use tools like web search, file access, and language models

#### 1.5.2 Physical Agents (Embodied Systems)

![Physical Agent](diagrams/physical-agent.png)

**Description:** Interact with the real world using sensors and actuators

**Examples:**
- Domestic robots (vacuum cleaners, assistants)
- Autonomous vehicles
- Factory robotic arms

**Key Characteristics:**
- Sense physical world using embedded sensors
- Act using motors, arms, wheels, or other actuators
- Must handle uncertainty, delay, and safety in real environments

#### 1.5.3 Hybrid and Adaptive Agents

![Hybrid Agent](diagrams/hybrid-agent.png)

**Description:** Combine both digital and physical capabilities, adapting based on feedback

**Examples:**
- AI traffic systems analyzing live camera feeds
- Healthcare assistants monitoring wearables
- Warehouse robots using databases and physical movement

**Key Characteristics:**
- Operate across both digital and physical domains
- Integrate multi-modal data (text, images, sensor readings)
- Adapt and improve through real-world feedback loops

### 1.6 Evolution of AI Agents

![Evolution of AI Agents](diagrams/evolution-agents.png)

#### 1.6.1 Rule-Based Agents (1970s-1980s)

![Rule-Based Agent](diagrams/rule-based-agent.png)

**Characteristics:**
- Fixed "if-then" logic
- No generalization capability
- Human-defined rules

**Examples:** MYCIN, XCON

**Limitations:** Cannot infer new rules, struggle with edge cases and ambiguity

#### 1.6.2 Learning-Based Agents

![Learning-Based Agent](diagrams/learning-based-agent.png)

**Characteristics:**
- Data-driven optimization through ML
- Reinforcement Learning (RL) enables trial-and-error learning
- Learn complex behaviors without explicit programming

**Examples:** AlphaGo (RL), robot manipulation

**Limitations:** Require large-scale training, significant compute resources, carefully structured environments

#### 1.6.3 LLM-Powered Agents (Current)

![LLM-Powered Agent](diagrams/llm-powered-agent.png)

**Key Capabilities:**
- **Zero-shot generalization** through massive pretraining
- **Tool use and selection** - choosing and operating the right tool
- **Dynamic task planning** - decomposing complex goals
- **Conversational memory** - maintaining multi-turn context
- **Generalization without retraining** - handling novel tasks

**Examples:** GPT-4 agents, Claude-based systems, Gemini agents

### 1.7 When to Build an Agent

![Decision Framework for Building Agents](diagrams/when-to-build-agent.png)

Build agents when tasks involve:

#### 1. Contextual Decision-Making
- Nuanced judgment required
- Ambiguous input handling
- Behavior adjustment based on prior interactions

**Example:** Refund approval process considering customer history, tone, and reason

#### 2. Complex Rules
- Too many conditional branches
- Numerous exception cases
- Difficult maintenance

**Example:** Vendor security review with evolving compliance requirements

#### 3. Unstructured/Natural Language Data
- Parsing documents, emails, conversations
- Meaning extraction required

**Example:** Insurance claim intake where customers describe events in their own words

---

## 2. Agent Architecture: Core Agent Components

### 2.1 Three Core Components

![Core Agent Components](diagrams/core-components.png)

#### 2.1.1 The Model (Agent's Brain)

**Function:** Interprets inputs and reasons through decisions

**Why LLMs Work Well:**
- Flexible
- Compositional
- Adaptable

**Model Selection Factors:**

![Model Selection Factors](diagrams/model-selection-factors.png)

| **Factor** | **Consideration** |
|-----------|------------------|
| **Task Complexity** | Simple tasks → smaller models (Mistral, Gemma)<br>Complex reasoning → larger models (GPT-4, Claude Opus) |
| **Latency Requirements** | Fast responses → optimized models |
| **Cost Considerations** | Mix models: small for routine, large when needed |
| **Context Length** | Long conversations/documents → Claude 3 Sonnet, Gemini 1.5 |

#### 2.1.2 Tools (Acting in Environment)

**Function:** External functions, APIs, or environments for performing real-world tasks

**Types:**
- APIs (REST, GraphQL)
- Web search
- Code execution
- Databases
- Device interfaces

**Purpose:** Enable agents to go beyond text generation to actual interaction

#### 2.1.3 Instructions (Shaping Behavior)

**Function:** Guide what agent should do, how it should behave, which goals to prioritize

**Forms:**
- Natural language prompts
- System messages
- Examples (few-shot learning)
- Constraints
- Task definitions

**Purpose:**
- Align output with expectations
- Guide reasoning and tool use
- Control safety and constraints

### 2.2 Component Interaction Flow

![How Agent Components Work Together](diagrams/components-interaction.png)

**Flow:**
1. **Instructions set the stage** - Define role, goals, boundaries
2. **Model does the thinking** - Interprets, reasons, decides
3. **Tools handle the doing** - Retrieve data, send messages, trigger processes
4. **Steps may loop/repeat** as needed

### 2.3 Why Modular Design?

**Benefits:**
- ✅ Easily upgrade/swap models without system overhaul
- ✅ Integrate new tools to extend capabilities
- ✅ Adjust instructions for new domains/requirements
- ✅ Improve testing/debugging by isolating issues
- ✅ Enable fault isolation for system resilience
- ✅ Foster extensibility for diverse tasks

### 2.4 Example Workflow: Meeting Scheduling

**Step 1: Perceive and Plan** (Model + Instructions)
- Understand user request: "Schedule meeting with John next Tuesday"

**Step 2: Gather Information** (Calendar API Tool)
- Check availability for Tuesday
- Check John's calendar

**Step 3: Execute Action** (Email API Tool + Model)
- Format meeting invitation
- Send email to John

**Step 4: Confirm Completion** (Calendar API + Model)
- Add meeting to calendar
- Confirm with user

---

## 3. Agent Architecture: Components Interaction and Agent Memory

### 3.1 The Architecture Blueprint

![LLM-Based AI Agent Architecture](diagrams/agent-architecture.png)

#### Four Primary Elements:

1. **Input Interface**
   - Receives information from environment/user
   - Formats: text, sensor data, API signals, multimodal inputs

2. **Reasoning Core (Model)**
   - LLM interprets input
   - Plans steps
   - Determines tool/action use

3. **Tools and Actions**
   - Based on reasoning, calls APIs
   - Fetches documents
   - Sends responses
   - Triggers actions

4. **Memory and Context**
   - Stores/retrieves past information
   - Maintains conversational history
   - Stores documents and user preferences

### 3.2 The Agent Loop

