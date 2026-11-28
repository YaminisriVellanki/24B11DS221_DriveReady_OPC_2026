# Day 5 — Memory and RAG: An Agent That Remembers and Looks Things Up

## 1. Objective

The objective of Day 5 is to build an AI agent that can remember previous conversations, maintain separate memory for different customers, retrieve information from a knowledge base, and answer questions using relevant stored information.

The project uses **Sweet Crumbs Home Bakery** as the case study to demonstrate Memory, Embeddings, Vector Databases, Retrieval-Augmented Generation (RAG), and integration of these concepts into an AI agent.

---

## 2. Case Study — Sweet Crumbs Home Bakery

Sweet Crumbs Home Bakery is a fictional bakery that uses an AI assistant to answer customer questions, provide menu information, retrieve bakery policies, remember customer conversations, and assist with orders.

The assistant should be able to:
- Answer questions about bakery products and prices.
- Retrieve information about ingredients, delivery, payment, and policies.
- Remember customer preferences within a conversation.
- Maintain separate conversation histories for different customers.
- Handle order modifications using conversation context.
- Avoid making up answers when information is unavailable.

---

## 3. Concepts Covered

### 3.1 Types of Memory in AI Agents

AI agents can use different kinds of memory depending on the information they need to retain.

**Conversation Memory**
- Stores messages exchanged between the user and agent.
- Maintains conversational context.
- Helps the agent understand follow-up questions.
- Allows the conversation to continue without starting from scratch.

**Customer Memory**
- Maintains customer-specific information.
- Can include customer preferences, names, interests, and relevant details.
- Allows the agent to provide personalized responses.

**Knowledge Memory**
- Stores business information, facts, policies, FAQs, and other reference information.
- Allows the agent to retrieve information when answering questions.
- Provides access to information beyond the current conversation.

---

### 3.2 Conversation Memory

Conversation memory allows an AI agent to remember earlier messages within a conversation.

For example, when a customer says they want two plum cakes and later asks to change the quantity to three, the agent should understand the previous order and update the quantity instead of asking the customer to repeat everything.

Conversation memory helps with:
- Follow-up questions.
- Order modifications.
- Maintaining conversational context.
- Understanding references to earlier messages.

---

### 3.3 Checkpointer

A checkpointer stores the state of an agent's conversation so that the agent can continue from its previous state.

In LangGraph, a checkpointer can preserve conversation state across multiple interactions.

The checkpointer is used together with a thread ID to identify a conversation.

**Benefits:**
- Retains conversation state.
- Supports continuing previous conversations.
- Allows multiple independent conversations.
- Prevents conversations from starting with an empty state every time.

---

### 3.4 Thread ID

A thread ID is a unique identifier used to associate messages with a particular conversation.

For example:
- `customer_A` identifies Customer A's conversation.
- `customer_B` identifies Customer B's conversation.

Messages submitted using the same thread ID belong to the same conversation. Different thread IDs maintain separate conversation states.

---

### 3.5 Customer Memory Isolation

Customer memory isolation ensures that one customer cannot access another customer's conversation information.

For example:
- Customer A likes plum cake.
- Customer B likes chocolate cake.

When each customer asks about their preference, the agent should retrieve the correct information from their respective conversation.

This is important for privacy, personalization, and avoiding the mixing of customer data.

---

### 3.6 Context Window

The context window is the amount of information an AI model can process during a particular interaction.

It includes information such as:
- System instructions.
- Conversation history.
- User messages.
- Tool results.
- Retrieved knowledge.
- Agent responses.

When the conversation becomes too long, the context window may become insufficient to accommodate all information.

---

### 3.7 Token Budget

Tokens are units used by language models to process text. A token may represent a word, part of a word, punctuation, or another text unit.

The token budget refers to the available tokens that can be used within a model's context window.

Managing the token budget is important because:
- Long conversations consume more tokens.
- Large prompts increase processing requirements.
- Too much irrelevant information reduces efficiency.
- Relevant information should be selected instead of sending everything to the model.

---

### 3.8 Embeddings

Embeddings are numerical representations of text that capture semantic meaning.

Texts with similar meanings can have similar vector representations, even if they use different words.

Embeddings are used to:
- Represent text mathematically.
- Compare semantic similarity.
- Search for relevant information.
- Retrieve knowledge based on meaning rather than exact keyword matching.

For example, a query about whether cakes can be delivered may retrieve information stored as "Delivery is available within 5 km."

---

### 3.9 Vector Database

A vector database stores and manages vector representations of information and enables similarity-based retrieval.

In this project, **ChromaDB** is used as the vector database.

It is used to:
- Store bakery knowledge.
- Organize information into a collection.
- Retrieve relevant documents.
- Perform similarity searches using natural-language queries.

---

### 3.10 ChromaDB Collection

A collection in ChromaDB is used to organize related stored documents.

The project uses a bakery knowledge collection to store information about:
- Menu prices.
- Products.
- Ingredients.
- Payment methods.
- Order requirements.
- Delivery policies.
- Cancellation policies.
- Product storage and freshness.

The collection allows the agent to search stored bakery knowledge when answering questions.

---

### 3.11 Similarity Search

Similarity search retrieves documents that are semantically related to a query.

Instead of searching only for exact matching words, the database compares vector representations to identify relevant information.

For example:

**Query:** How long should I keep the cake?

The database can retrieve information about refrigeration and freshness even if the stored document does not contain the exact wording of the question.

---

### 3.12 Document Chunking

Document chunking is the process of dividing large documents into smaller pieces of text.

Chunking helps:
- Reduce the amount of information retrieved at one time.
- Improve relevance of retrieval.
- Avoid sending entire documents to the model.
- Manage context-window and token-budget limitations.

The project demonstrates how knowledge can be divided into smaller chunks for retrieval.

---

### 3.13 Retrieval-Augmented Generation (RAG)

Retrieval-Augmented Generation combines information retrieval with language-model generation.

Instead of depending entirely on the model's pre-trained knowledge, the agent retrieves relevant information from an external knowledge base and uses it to generate an answer.

**RAG workflow:**

1. The user asks a question.
2. The question is used to search the knowledge base.
3. Relevant documents are retrieved.
4. The retrieved information is provided to the AI model.
5. The model generates an answer grounded in the retrieved information.

RAG improves the relevance and reliability of answers for business-specific information.

---

### 3.14 RAG Pipeline

The RAG pipeline consists of the following stages:

**Ingestion**
- Collect business knowledge and FAQs.

**Chunking**
- Divide information into manageable text chunks when required.

**Embedding**
- Convert the stored text into vector representations.

**Storage**
- Store the text and its vectors in ChromaDB.

**Retrieval**
- Search for relevant information using the user's query.

**Augmentation**
- Provide the retrieved information as context to the language model.

**Generation**
- Generate an answer based on the retrieved information.

---

### 3.15 Custom Retrieval Tool — `search_faq`

A custom tool named `search_faq` is created to retrieve information from the bakery's knowledge base.

The tool:
- Accepts a natural-language question.
- Queries the ChromaDB collection.
- Retrieves relevant documents.
- Returns the retrieved information to the agent.
- Provides a fallback response when relevant information is unavailable.

The tool is integrated into the agent so that it can be invoked when bakery-related questions require knowledge retrieval.

---

### 3.16 Tool Integration

Tools extend the capabilities of AI agents by allowing them to perform specific tasks beyond generating text.

The Day 5 agent integrates tools for:
- Menu price lookup.
- Order advance requirement checking.
- Order logging.
- FAQ and policy retrieval using RAG.

The agent decides when to use an available tool based on the user's request.

---

### 3.17 Memory and RAG Integration

Memory and RAG solve different problems and work together.

| Memory | RAG |
|---|---|
| Stores conversation context | Retrieves external knowledge |
| Remembers customer information | Retrieves business information |
| Uses conversation threads | Uses knowledge-base search |
| Helps with follow-up questions | Helps answer factual questions |
| Maintains customer-specific context | Provides relevant stored documents |

Combining memory and RAG allows the agent to remember what a customer said while also retrieving accurate information from the bakery's knowledge base.

---

### 3.18 Hallucination Prevention

Hallucination occurs when an AI model generates information that is incorrect, unsupported, or not present in its available knowledge.

The project implements safeguards by:
- Retrieving relevant information from ChromaDB.
- Using stored information to answer business questions.
- Avoiding invented prices and policies.
- Checking whether relevant documents are available.
- Returning an appropriate fallback response for unsupported questions.

For example, if a customer asks for the bakery's Wi-Fi password and it is not stored in the knowledge base, the agent should state that the information is unavailable rather than inventing a password.

---

### 3.19 Retrieval Relevance and Distance Threshold

Similarity search may return documents even when they are not sufficiently relevant to the user's question.

A retrieval relevance threshold is used to filter results based on the database's similarity or distance score.

The purpose is to:
- Avoid using unrelated documents.
- Reduce incorrect answers.
- Improve unsupported-query handling.
- Allow fallback responses when retrieval is insufficient.

The threshold must be calibrated using the actual retrieval scores rather than chosen blindly.

---

### 3.20 Agent Testing and Evaluation

The agent is tested using different scenarios to verify its functionality.

Testing includes:
- Price lookup.
- Payment-policy retrieval.
- Product freshness questions.
- Conversation memory.
- Customer memory isolation.
- Order modifications.
- Order requirements.
- Unsupported questions.
- Order logging.

The test results are used to calculate the pass rate.

\[
\text{Pass Rate}=\frac{\text{Tests Passed}}{\text{Tests Executed}}\times100
\]

A target pass rate of at least 80% is used for evaluation.

---

## 4. Knowledge Base

The bakery knowledge base contains business facts stored in ChromaDB.

| Category | Stored Information |
|---|---|
| Menu | Plum cake, chocolate cake, cupcakes |
| Pricing | Product prices |
| Payments | Cash and UPI |
| Order requirements | Advance notice required |
| Custom orders | Photo cake advance requirement |
| Add-ons | Free candles |
| Customization | Message length limit |
| Ingredients | Product ingredient information |
| Product safety | Nut information |
| Storage | Refrigeration |
| Freshness | Best-consumption period |
| Delivery | Delivery radius |
| Delivery charges | Delivery fee |
| Free delivery | Minimum order amount |
| Payment policy | Advance payment for high-value orders |
| Cancellation | Cancellation time requirements |

---

## 5. Tools Implemented

| Tool | Purpose |
|---|---|
| `get_bakery_price` | Retrieves the price of a bakery item |
| `check_order_requirement` | Checks advance notice requirements |
| `log_bakery_order` | Records confirmed orders in Google Sheets |
| `search_faq` | Retrieves relevant bakery knowledge using ChromaDB |

---

## 6. Agent Workflow

1. Customer sends a message.
2. The agent identifies the customer's request.
3. Conversation memory is retrieved using the thread ID.
4. The agent determines whether a tool is required.
5. If necessary, the appropriate tool is called.
6. For FAQ and business-policy queries, relevant information is retrieved from ChromaDB.
7. Retrieved information is provided to the language model.
8. The agent generates a response using the conversation context and available information.
9. The response is returned to the customer.
10. Conversation state is maintained for subsequent interactions.

---

## 7. Technologies Used

- Python
- Google Colab
- LangChain
- LangGraph
- Groq API
- ChromaDB
- Vector embeddings
- Retrieval-Augmented Generation
- Google Sheets
- Pydantic

---

## 8. Practical Tasks Completed

- Implemented different types of memory.
- Demonstrated conversation memory.
- Implemented checkpointer-based conversation state.
- Created separate thread IDs for customers.
- Demonstrated context-window limitations.
- Explored token-budget management.
- Studied embedding concepts.
- Created a ChromaDB collection.
- Stored bakery facts in a vector database.
- Implemented semantic similarity search.
- Demonstrated document chunking.
- Built a custom FAQ retrieval tool.
- Integrated RAG into the AI agent.
- Implemented customer memory isolation.
- Tested unsupported-query handling.
- Evaluated agent responses.
- Calculated the test pass rate.

---

## 9. Testing Scenarios

| Test | Expected Behavior |
|---|---|
| Price query | Retrieve the correct menu price |
| Payment query | Retrieve supported payment methods |
| Freshness query | Retrieve storage and freshness information |
| Delivery query | Retrieve delivery policies |
| Customer memory | Remember information from previous messages |
| Memory isolation | Keep different customers' memories separate |
| Order modification | Understand changes using conversation context |
| Order requirement | Provide the correct advance notice |
| Unsupported query | Avoid inventing information |
| Order logging | Record confirmed order details correctly |

---

## 10. Learning Outcomes

After completing Day 5, the following concepts and skills were practiced:

- Understanding short-term conversational memory.
- Understanding customer-specific memory.
- Understanding knowledge memory.
- Maintaining agent state using a checkpointer.
- Using thread IDs for conversations.
- Understanding memory isolation.
- Understanding context windows and token budgets.
- Understanding embeddings and vector representations.
- Using ChromaDB as a vector database.
- Performing semantic similarity searches.
- Understanding document chunking.
- Building a RAG pipeline.
- Creating custom retrieval tools.
- Integrating retrieval with an AI agent.
- Grounding responses in stored knowledge.
- Handling unsupported queries.
- Testing and evaluating agent performance.

---

## 11. Conclusion

Day 5 focused on enabling AI agents to remember conversations and retrieve external information.

By integrating conversational memory, thread-based state management, ChromaDB, semantic search, and Retrieval-Augmented Generation, the Sweet Crumbs Home Bakery assistant becomes capable of maintaining conversational context and answering business-related questions using stored knowledge.

This demonstrates how memory and retrieval can make AI agents more context-aware, useful, and reliable.
