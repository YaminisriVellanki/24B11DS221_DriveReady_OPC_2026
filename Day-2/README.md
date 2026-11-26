# Day 2 – Prompts, Memory and Python Agents

## 1. Introduction

Day 2 focuses on prompt engineering, conversation memory and Python concepts used to build AI agents.

In this session, I learned how to control LLM responses using system prompts, provide examples, generate JSON responses and manage conversation history.

I also practiced Python dictionaries, functions, decorators and exception handling using the Groq API.

## 2. Concepts Learned

### 2.1 Messages and Roles

An LLM conversation consists of messages with different roles.

- **System:** Defines the chatbot's behaviour and instructions.
- **User:** Contains the user's questions or messages.
- **Assistant:** Contains the chatbot's responses.

These roles help organize conversations and control chatbot behaviour.

### 2.2 System Prompt

A system prompt provides instructions to the AI assistant.

The four important parts are:

- **Role:** Defines who the assistant is.
- **Facts:** Provides business information.
- **Rules:** Defines what the assistant should and should not do.
- **Format:** Controls how the response should be presented.

### 2.3 Few-Shot Examples

Few-shot prompting means providing examples to an LLM before asking it to perform a task.

It helps the model understand the expected response pattern.

For example, a customer message can be classified into categories such as Order, Question or Complaint.

### 2.4 Asking for JSON

JSON stands for JavaScript Object Notation.

It is a structured format used to represent and exchange data.

An AI assistant can return information in JSON format with fields such as:

- Name
- Item
- Quantity
- Date
- Eggless

In Python, `json.loads()` converts a JSON string into a Python dictionary.

### 2.5 Memory by Hand

LLMs do not automatically remember previous independent API calls.

Conversation history can be maintained manually using a Python list.

The previous messages are passed to the API along with the current user message.

`MAX_TURNS` is used to limit the number of messages included in the conversation context.

### 2.6 Dictionaries and JSON in Python

A Python dictionary stores information in key-value pairs.

Example:

```python
MENU = {
    "plum cake": 500,
    "chocolate cake": 650,
    "cupcake": 80
}
```

The `json.dumps()` function converts Python objects into JSON strings.

### 2.7 Functions and Type Hints

Functions are reusable blocks of code that perform specific tasks.

Type hints indicate the expected data types of function parameters and return values.

Example:

```python
def get_price(item: str, qty: int = 1) -> int:
    """
    Calculate the total price of an item.
    """
    return qty * 100
```

### 2.8 Decorators

A decorator is a function that adds extra functionality to another function without changing its original code.

The `@` symbol is used to apply a decorator.

Example:

```python
from functools import wraps

def log_call(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print("Function called:", func.__name__)
        return func(*args, **kwargs)
    return wrapper
```

### 2.9 Try and Except

Exception handling prevents a program from stopping unexpectedly when an error occurs.

- `try`: Contains code that may produce an error.
- `except`: Handles the error.

Example:

```python
try:
    number = int("abc")
except ValueError:
    print("Invalid number")
```

## 3. Practical Tasks – Your 10%

### Task 1: Prompt Parts

- Created a system prompt with business rules.
- Tested the chatbot after removing the RULES section.
- Restored the RULES section and compared the responses.
- Observed how instructions influence AI responses.

### Task 2: Few-Shot Classifier

- Created a classifier for a business using three examples.
- Tested the classifier with five new customer messages.
- Observed how examples guide the model's responses.

### Task 3: JSON Extraction

- Asked the chatbot to extract customer order details in JSON format.
- Used the fields Name, Item, Quantity, Date and Eggless.
- Parsed the response using `json.loads()`.
- Used `try-except` for error handling.

### Task 4: Memory Testing

- Set `MAX_TURNS = 2`.
- Stored conversation messages in a Python list.
- Tested whether the chatbot could remember a customer's name after multiple messages.
- Observed how limiting conversation history affects memory.

### Task 5: Build a Chatbot for My Own Business – DemandPulse AI

- Created a service catalogue using a Python dictionary.
- Implemented a price calculation function.
- Used type hints and a docstring.
- Created a custom system prompt for DemandPulse AI.
- Tested the chatbot using customer queries.

## 4. Additional Implementation – DemandPulse AI

DemandPulse AI is my additional business example.

I created a service catalogue containing:

- Sales Forecasting
- Demand Analysis
- Inventory Planning
- Business Report

I implemented a Python function to calculate service prices and tested the chatbot using the Groq API.

This additional implementation helped me apply Python dictionaries, functions and system prompting to a practical business example.

## 5. Tools and Technologies Used

- Python
- Google Colab
- Groq API
- OpenAI Python SDK
- JSON
- LLM Prompt Engineering

## 6. Learning Outcomes

After completing Day 2, I learned:

1. How message roles work in LLM conversations.
2. How to create structured system prompts.
3. How to guide AI responses using few-shot examples.
4. How to generate and parse JSON responses.
5. How to maintain conversation history manually.
6. How to use Python dictionaries and JSON.
7. How to create functions with type hints and docstrings.
8. How to use decorators.
9. How to handle errors using try-except.

## 7. Conclusion

Day 2 helped me understand prompt engineering, conversation memory and essential Python concepts for building AI agents. I implemented the instructor's practical tasks and created an additional DemandPulse AI chatbot to apply the concepts to my own business example.
