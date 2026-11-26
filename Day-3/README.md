# Day 3 – Your First Agent: What an Agent Is and LangChain

## 1. Introduction

Day 3 focuses on understanding AI agents and learning how to build a basic AI application using LangChain.

We learned the difference between a chatbot and an AI agent, the components of an agent, the agent loop, and how LangChain connects an LLM with prompts and memory.

We implemented a customer-support assistant for Sweet Crumbs Home Bakery and then customized it for our own business example, DemandPulse AI.

## 2. Concepts Learned

### 2.1 Chatbot vs Agent
- A chatbot responds to user questions.
- An AI agent can perform multiple steps to complete a task.
- An agent can use tools, make decisions, and observe results.

### 2.2 Four Parts of an AI Agent
1. **Brain:** The language model that processes information.
2. **Instructions:** The system prompt that defines the agent's role and rules.
3. **Tools:** Functions that allow the agent to perform actions.
4. **Memory:** Stores previous conversation information.

### 2.3 Agent Loop
An AI agent follows a continuous process:

1. Think – Understand the task.
2. Act – Perform an action or use a tool.
3. Observe – Check the result.
4. Repeat – Continue until the task is completed.

This is also associated with the ReAct approach.

### 2.4 Three Levels of AI
- **Traditional Software:** Performs predefined operations using code.
- **Generative AI:** Generates responses using an LLM.
- **Agentic AI:** Uses reasoning and tools to complete multi-step tasks.

### 2.5 Why LangChain?
LangChain is a framework used to build applications powered by language models. It helps connect prompts, models, memory, and tools.

### 2.6 LangChain Basics
- **Model:** Processes the input and generates a response.
- **Prompt Template:** Defines the instructions and structure of the input.
- **Chain:** Connects components together to process a request.

### 2.7 Conversation Memory
Conversation history can be maintained using a Python list and passed to the model with each new question.

### 2.8 CSV Testing
CSV files can store test questions and expected keywords. The assistant's responses can be checked automatically using Python.

## 3. Practical Implementation

### Sweet Crumbs Home Bakery
Implemented a customer-support assistant using:
- LangChain
- ChatGroq
- ChatPromptTemplate
- MessagesPlaceholder
- StrOutputParser
- Conversation history
- CSV-based testing

Created a basic LangChain agent using `create_agent()`.

### DemandPulse AI – My Own Business Example
Customized the system prompt for DemandPulse AI with four services:

| Service | Price |
|---|---:|
| Sales Forecasting | Rs 500 |
| Demand Analysis | Rs 300 |
| Inventory Planning | Rs 400 |
| Business Report | Rs 200 |

Implemented:
- A customized system prompt.
- Ten customer questions in a CSV file.
- Automated keyword-based response testing.
- Prompt improvement and comparison.
- Temperature experiment using temperature 1.0.
- Classification of business jobs as Plain Code, One LLM Call, and Agent.

## 4. Python Functions for Day 4 Preparation

Created two Python functions with type hints and docstrings.

**1. get_service_price(service: str) -> int**
- Retrieves the price of a DemandPulse AI service.
- Raises a ValueError for an unknown service.

**2. check_service_available(service: str) -> bool**
- Checks whether a service is provided by DemandPulse AI.
- Returns True or False.

These functions prepare us to understand how Python functions can be converted into tools for an AI agent.

## 5. Technologies Used

- Python
- Google Colab
- LangChain
- LangChain-Groq
- Groq API
- CSV
- JSON
- LLMs

## 6. Learning Outcomes

After completing Day 3, I learned:

1. The difference between chatbots and AI agents.
2. The four main components of an AI agent.
3. How the agent loop works.
4. The basic concepts of LangChain.
5. How to create prompts and chains.
6. How to maintain conversation history.
7. How to test AI responses using CSV files.
8. How to create a basic agent using LangChain.
9. How to write reusable Python functions with type hints and docstrings.
10. How to prepare Python functions for use as agent tools.

## 7. Conclusion

Day 3 helped me understand the fundamentals of AI agents and LangChain. I implemented a basic customer-support assistant, customized it for DemandPulse AI, tested its responses, and created Python functions as preparation for building agents with tools in Day 4.
