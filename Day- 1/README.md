# Day 1 – How LLMs Work and Your First API Call

## 1. Introduction

Day 1 introduces the fundamentals of Large Language Models (LLMs) and explains how to communicate with an AI model using an API.

In this session, we learned how LLMs process text, generate responses, use tokens, handle conversation context, and connect with Python applications.

### Topics Covered

1. Why AI is suddenly everywhere?
2. What an LLM really does
3. Tokens
4. Temperature
5. The model has no memory
6. Context window
7. How it learned and hallucination
8. AI engineer role
9. First API call

---

## 2. Concepts Learned

### 2.1 Why AI Is Suddenly Everywhere?

**What is it?**

Artificial Intelligence (AI) is a technology that enables computers to perform tasks that normally require human intelligence.

Examples include understanding language, recognizing images, generating content, and answering questions.

**Why is AI becoming popular?**

- AI can automate repetitive tasks.
- It can process large amounts of information.
- It helps users get answers quickly.
- It can generate text, images, and code.
- It can be integrated into different applications.

**Example:**

A bakery can use an AI assistant to answer customer questions about cake prices, eggless options, and order requirements.

**Application in DemandPulse AI:**

AI can help a shopkeeper understand customer requests and identify possible unmet-demand opportunities.

### 2.2 What an LLM Really Does

**What is an LLM?**

LLM stands for Large Language Model.

It is an AI model trained on large amounts of text data to understand and generate human-like language.

**How does an LLM work?**

1. It receives text as input.
2. It processes the input as tokens.
3. It uses the provided context to understand the request.
4. It predicts the next token.
5. It generates a response token by token.

**Example:**

Input:

"What is Artificial Intelligence?"

The LLM processes the question and generates an appropriate explanation.

**Why is it useful?**

LLMs allow applications to communicate with users using natural language instead of fixed commands.

**Application in DemandPulse AI:**

An LLM can explain repeated product requests and summarize demand patterns for a shopkeeper.

### 2.3 Tokens

**What are tokens?**

Tokens are the small units of text processed by an LLM.

A token can be:
- A complete word.
- A part of a word.
- A punctuation mark.

A sentence is divided into tokens before it is processed by the model.

**Why are tokens important?**

- Models process input and output using tokens.
- API usage can depend on the number of tokens.
- Token limits affect how much information can be processed.
- Longer prompts generally consume more input tokens.

**Important API terms:**

- `prompt_tokens`: Tokens used in the input.
- `completion_tokens`: Tokens generated in the response.
- `total_tokens`: Total tokens used.

**Example:**

When asking the same question in English and Telugu, the token usage may differ.

**Application in DemandPulse AI:**

When sending many customer demand records to an LLM, token usage must be considered to manage API usage efficiently.

### 2.4 Temperature

**What is temperature?**

Temperature is a parameter that controls the randomness of the model's response.

It influences how predictable or varied the generated answers are.

**Low Temperature:**
- More focused responses.
- More consistent outputs.
- Useful for factual and rule-based tasks.

**High Temperature:**
- More varied responses.
- More creative outputs.
- Useful for brainstorming and creative writing.

**Example:**

For Sweet Crumbs Home Bakery:
- Temperature 0.2 can produce more consistent customer-support answers.
- Temperature 1.2 can produce more varied taglines.

**Application in DemandPulse AI:**

A lower temperature is suitable for consistent demand summaries and business recommendations.

### 2.5 The Model Has No Memory

**What does it mean?**

A normal independent API request does not automatically remember previous requests.

The model can use the messages included in the current request, but it does not automatically retain the previous request's conversation.

**Example:**

First API request:

"My name is Ravi."

Second separate API request:

"What is my name?"

The model may not know the name because the earlier message was not included.

**How can we provide memory?**

We can include previous conversation messages in the next API request.

For example:

- System message: Defines the assistant's role.
- User message: Provides the question.
- Assistant message: Contains the previous response.
- New user message: Provides the next question.

This allows the model to use the supplied conversation history.

**Application in DemandPulse AI:**

The system may need to retain previous demand records and shopkeeper decisions. This requires storing and providing relevant information rather than assuming the LLM remembers it automatically.

### 2.6 Context Window

**What is a context window?**

A context window is the amount of information a model can process during a single interaction.

It includes the information provided in the request, such as:

- System instructions.
- User messages.
- Conversation history.
- Other supplied context.

**Why is it important?**

- It limits the amount of information processed at once.
- Large inputs consume more tokens.
- Very long conversations may exceed the model's context limit.
- Relevant information must be selected carefully.

**Example:**

If a shopkeeper provides hundreds of customer requests, all the information may not fit into a single model request.

**Application in DemandPulse AI:**

We can summarize or organize demand records before sending relevant information to the LLM.

### 2.7 How It Learned and Hallucination

**How does an LLM learn?**

An LLM is trained using large amounts of text data.

During training, it learns patterns in language and relationships between words and concepts. It uses these learned patterns to generate responses.

**What is hallucination?**

Hallucination occurs when an AI model generates information that sounds correct but is incorrect or unsupported by the available information.

**Example:**

Suppose a bakery assistant is given only these facts:

- Orders require 24 hours' notice.
- All cakes have eggless versions.
- Plum cake costs Rs 500.

If a customer asks whether delivery is available in Kakinada, the model should not invent a delivery policy.

It should say:

"I'll check with the owner."

**How can hallucination be reduced?**

1. Provide accurate information.
2. Write clear system instructions.
3. Give rules for handling unknown information.
4. Avoid unsupported assumptions.
5. Verify important information.

**Application in DemandPulse AI:**

The system must not invent supplier prices, product availability, customer demand, or expected profits. Business recommendations must be based on available evidence.

### 2.8 AI Engineer Role

**Who is an AI engineer?**

An AI engineer develops applications and systems that use Artificial Intelligence to solve real-world problems.

**Important responsibilities:**

- Working with AI and LLM models.
- Writing effective prompts.
- Connecting applications with AI APIs.
- Using Python for AI development.
- Processing and managing data.
- Testing and improving AI applications.
- Integrating AI into practical solutions.

**Example:**

Developing an AI-powered customer-support assistant for a bakery.

**Application in DemandPulse AI:**

An AI engineer can combine Python, LLM APIs, data analysis, and other AI technologies to build a system that helps shopkeepers make informed business decisions.

### 2.9 First API Call

**What is an API?**

API stands for Application Programming Interface.

It allows two software applications to communicate with each other.

In this session, we used Python to communicate with an AI model through the Groq API using an OpenAI-compatible client.

**Technologies used:**

- Python
- Google Colab
- OpenAI Python library
- Groq API
- `openai/gpt-oss-20b` model

**Steps involved in making an API call:**

1. Install the required Python library.
2. Retrieve the API key securely.
3. Configure the API client.
4. Select the AI model.
5. Provide messages to the model.
6. Send the API request.
7. Receive and display the response.
8. Check token usage.

**Important API components:**

| Component | Purpose |
|---|---|
| `OpenAI()` | Creates the API client |
| `api_key` | Authenticates the API request |
| `base_url` | Specifies the API service endpoint |
| `model` | Specifies the model to use |
| `messages` | Contains instructions and conversation input |
| `temperature` | Controls response randomness |
| `chat.completions.create()` | Sends a chat completion request |
| `response.choices[0].message.content` | Retrieves the generated response |
| `response.usage` | Retrieves token usage information |

**Understanding the API workflow:**

1. Python creates the API client.
2. The client sends the request to the API service.
3. The API service processes the request using the selected model.
4. The model generates a response.
5. The response is returned to Python.
6. Python displays the response and usage information.

**Application in DemandPulse AI:**

The API connects the DemandPulse AI Python application with an LLM so that it can analyze and explain customer demand information.

---

## 3. Instructor Example – Sweet Crumbs Home Bakery

The instructor demonstrated the first API call using a bakery customer-support assistant.

### Business facts

- The bakery prepares cakes to order.
- Orders require 24 hours' notice.
- All cakes have eggless versions.
- Plum cake costs Rs 500.
- Chocolate cake costs Rs 650.
- Cupcake costs Rs 80.

### System prompt concepts

The system prompt defines:

- **Role:** The assistant works for Sweet Crumbs Home Bakery.
- **Facts:** Provides accurate bakery information.
- **Rules:** Prevents unsupported promises.
- **Format:** Keeps responses friendly and under 50 words, in English or Telugu according to the customer.

### Example customer question

"Can I get an eggless cake today evening?"

### Expected response behaviour

The assistant should explain that eggless cakes are available, but orders require 24 hours' notice.

It should not promise same-evening availability.

### What we learned from this example

- How to define an AI assistant's role.
- How to provide business information.
- How to write system instructions.
- How to control the response format.
- How to connect an LLM through an API.

---

## 4. Practical Exercises – Your 10%

The following exercises were assigned by the instructor.

### Task 1 – Temperature

Generate a tagline for Sweet Crumbs Home Bakery:

- Three times using temperature 0.2.
- Three times using temperature 1.2.

Compare the responses and observe the differences in creativity and consistency.

### Task 2 – Hallucination

Remove the FACTS information from the system prompt.

Ask:

"Do you deliver to Kakinada?"

Observe whether the model generates information that was not provided.

### Task 3 – No Memory

First send:

"My name is Ravi."

Then, in a separate request, ask:

"What is my name?"

Next, include both messages in the same conversation context and compare the responses.

### Task 4 – Tokens

Ask the same question in English and Telugu.

Compare the prompt token usage returned by the API.

### Task 5 – Your Business

Create a system prompt for your own business.

Include:
- Five business facts.
- Three assistant rules.
- Three real customer questions.

Observe how the assistant responds using the information and rules provided.

---

## 5. Additional Learning – DemandPulse AI

### Project Name

**DemandPulse AI – Autonomous Unmet-Demand Discovery & Business Decision Agent**

### Problem Statement

Small retail shops may lose sales when customers request products that are unavailable.

Shopkeepers may not systematically record repeated requests or investigate whether introducing those products would be profitable.

### Proposed Solution

DemandPulse AI aims to collect unmet customer requests, identify repeated demand, investigate product opportunities, evaluate risks, and provide evidence-based recommendations.

### Day 1 Concepts Applied

| Concept | Application |
|---|---|
| LLM | Explains customer demand patterns |
| System prompt | Defines the DemandPulse AI assistant's role and rules |
| Tokens | Helps monitor API usage |
| Temperature | Helps generate consistent analysis |
| No memory | Shows the need to provide or store previous demand records |
| Context window | Determines how much demand information can be supplied |
| Hallucination | Helps prevent unsupported business claims |
| API | Connects the Python application to an LLM |

### Basic Example Scenario

Simulated customer requests:

- Sugar-free biscuits – 3 requests.
- Oat milk – 1 request.
- Almond cookies – 1 request.

Python counts the requests, and the LLM explains the demand pattern.

### Important Business Rule

Repeated requests alone do not prove that a product will be profitable.

Before recommending a purchase, the system must eventually consider:

- Supplier availability.
- Purchase cost.
- Expected selling price.
- Profitability.
- Purchasing risk.
- Uncertainty in customer demand.

**Current implementation:** This is a basic demand-analysis prototype, not a complete autonomous agentic system.

Advanced features will be added progressively as the corresponding concepts are taught in the course.

---

## 6. Day 1 Learning Outcomes

After completing Day 1, I learned:

1. The meaning and importance of Artificial Intelligence.
2. What Large Language Models are and how they generate responses.
3. What tokens are and why token usage matters.
4. How temperature affects generated responses.
5. Why separate API requests do not automatically share memory.
6. What a context window is.
7. How LLM training works at a basic level.
8. What hallucination means and how to reduce it.
9. The responsibilities of an AI engineer.
10. How to configure an API client and make the first API call.
11. How to apply basic LLM concepts to a practical business problem.
---

## 8. Conclusion

Day 1 provided the foundation for understanding Large Language Models and connecting Python applications with AI models through APIs.

The concepts learned in this session will help in developing more advanced AI applications, including DemandPulse AI, in the upcoming course sessions.
