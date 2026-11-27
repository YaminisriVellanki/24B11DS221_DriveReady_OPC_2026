# Day 4 – Tools, Structured Output, Google Sheets and Agent Tracing

## Objective

To understand how AI agents interact with external functions using tools, extract structured information from unstructured text, store information in external applications, select tools based on their descriptions, and analyze agent execution traces.

## Case Study

**Sweet Crumbs Home Bakery**

Sweet Crumbs Home Bakery is used as the business scenario to demonstrate the implementation of LangChain tools, structured customer-order extraction, Google Sheets integration, tool selection, and agent execution.

---

# Task 1: Creating Custom Tools Using `@tool`

## 1.1 What Are Tools?

Tools are functions that an AI agent can use to perform specific tasks beyond generating text responses.

An LLM can understand questions and generate answers, but it cannot directly interact with external systems or execute business operations unless it is provided with the necessary capabilities.

Tools enable an agent to perform actions such as:

- Retrieving product prices.
- Checking business policies.
- Performing calculations.
- Accessing databases.
- Saving customer information.
- Interacting with external applications.

A tool connects the reasoning capability of an LLM with the functionality of an external Python program or service.

## 1.2 What Is the `@tool` Decorator?

The `@tool` decorator is provided by LangChain to convert a normal Python function into a tool that an AI agent can use.

When a function is decorated with `@tool`, LangChain uses its function name, type hints, and docstring to create information about the tool.

This information helps the agent understand:

- What the tool is called.
- What the tool does.
- What input arguments it requires.
- What type of input it accepts.

The converted tool can be invoked directly or provided to an AI agent.

## 1.3 Role of Type Hints

Type hints specify the expected data types of function parameters and return values.

For example, `item: str` indicates that the item argument is expected to be a string.

Type hints help LangChain identify the tool's input structure and generate an appropriate input schema. They also improve code readability and reduce ambiguity.

## 1.4 Role of Docstrings

A docstring is a description written inside a Python function to explain its purpose.

When a function is converted into a LangChain tool, its docstring becomes an important part of the tool description.

The LLM uses this description to understand when the tool should be selected. A clear and specific description improves the agent's ability to identify the correct tool for a task.

## 1.5 Tool Invocation Using `.invoke()`

The `invoke()` method is used to execute a LangChain tool with the required input.

It accepts the input in the form of a dictionary whose keys correspond to the tool's input parameters.

For example, a pricing tool can receive an item name and return its price. A tool without input parameters can be invoked using an empty dictionary.

Tool invocation executes the function and returns its result.

## 1.6 Implementation

Two custom tools were created for Sweet Crumbs Home Bakery:

- `get_price` – Retrieves the price of a bakery item.
- `check_advance_notice` – Returns the advance-order requirement.

Both functions were converted into LangChain tools using the `@tool` decorator and tested using `.invoke()`.

## 1.7 Outcome

Successfully converted normal Python functions into LangChain tools and verified their execution. This demonstrates how business functions can be made available to an AI agent as callable capabilities.

---

# Task 2: Structured Output Using Pydantic

## 2.1 What Is Structured Output?

Structured output refers to information organized in a predefined format rather than free-form text.

Customer messages are generally unstructured because customers communicate naturally using different sentence patterns, abbreviations, incomplete details, and informal language.

For example:

"I am Ravi, need 2 plum cakes on Dec 24, eggless please."

This message contains multiple pieces of information, but they are not explicitly organized into separate fields.

Structured output converts this type of message into a predictable format that an application can process.

## 2.2 What Is Pydantic?

Pydantic is a Python library used to define data models, validate data, and enforce expected data structures.

A Pydantic model defines the fields that an object should contain along with their expected data types.

In this task, the `BakeryOrder` model defines the structure of a customer order.

The fields include:

- Customer name
- Item
- Quantity
- Order date
- Eggless preference

Instead of receiving an unpredictable paragraph, the application receives information organized into predefined fields.

## 2.3 What Is a Pydantic Model?

A Pydantic model is a class that defines the structure of data using typed attributes.

Each field specifies the expected type of information. Pydantic can validate data against these definitions and help identify invalid data.

For example:

- Customer name should be text.
- Item should be text.
- Quantity should be an integer.
- Eggless preference should be a Boolean value.

The model makes data more consistent and easier to use in other parts of the application.

## 2.4 What Are Optional Fields?

Some customer messages may not contain all the information required for an order.

Optional fields allow a field to contain `None` when the information is unavailable.

For example, if a customer mentions the item and quantity but not their name, the name field can remain unavailable instead of forcing the model to invent a value.

Optional fields are useful when processing incomplete or ambiguous real-world messages.

## 2.5 What Is `Field()`?

`Field()` is used in Pydantic to configure model fields.

It can provide additional information about a field, such as its description, constraints, default values, and other metadata.

Field descriptions explain the meaning of each attribute and can help the LLM understand what information should be extracted into that field.

## 2.6 What Is `with_structured_output()`?

`with_structured_output()` is a LangChain method that configures an LLM to return its response according to a specified structure or schema.

Instead of generating an unrestricted text response, the model is instructed to produce output matching the defined Pydantic model.

The schema guides the model in organizing the extracted information into the expected fields.

This is particularly useful when the response must be consumed by another Python function, database, spreadsheet, or application.

## 2.7 Unstructured-to-Structured Data Extraction

Customer messages are supplied to the LLM in their original informal form.

The model identifies relevant details from the message and organizes them according to the `BakeryOrder` schema.

The same schema is used for all five customer messages, making the results consistent even when the customers use different wording.

## 2.8 What Is `model_dump()`?

`model_dump()` is a Pydantic method that converts a model instance into a Python dictionary.

The extracted order can therefore be represented as key-value pairs, making it easier to display, process, save, or pass to another function.

## 2.9 Implementation

A Pydantic model named `BakeryOrder` was created to define the structure of customer-order information.

The LLM was configured using `with_structured_output(BakeryOrder)` and tested with five informal customer messages.

The extracted results were displayed using `model_dump()`.

## 2.10 Outcome

Successfully extracted customer information from unstructured messages into a predefined data structure.

This demonstrates how LLMs and Pydantic can be combined to transform natural-language information into application-ready data.

---

# Task 3: Google Sheets Integration

## 3.1 What Is Google Sheets Integration?

Google Sheets integration allows a Python application to interact with a Google spreadsheet programmatically.

Instead of manually entering records into a spreadsheet, Python can create, retrieve, update, and append data through supported APIs and libraries.

This enables a spreadsheet to act as a simple external data store for business records.

## 3.2 What Is API Integration?

An API (Application Programming Interface) provides a defined way for different software applications to communicate with each other.

An application can use an API to request information or perform operations on another application without manually interacting with its interface.

In this task, Python communicates with Google Sheets through its integration libraries and Google authentication mechanisms.

## 3.3 What Is Authentication?

Authentication is the process of verifying the identity of a user or application before allowing access to a resource.

Google authentication is required to access or modify spreadsheets associated with a Google account.

In Google Colab, authentication allows the notebook to obtain the credentials required to interact with Google services on behalf of the authorized user.

Authentication is different from authorization:

- Authentication verifies who the user is.
- Authorization determines what the authenticated user is allowed to access or modify.

## 3.4 What Is `gspread`?

`gspread` is a Python library that provides an interface for working with Google Sheets.

It simplifies operations such as:

- Opening spreadsheets.
- Creating spreadsheets.
- Accessing worksheets.
- Reading cell data.
- Retrieving records.
- Appending rows.
- Updating cell values.

It reduces the amount of code needed to interact with Google Sheets APIs.

## 3.5 What Is a Spreadsheet and Worksheet?

A spreadsheet is the complete Google Sheets document.

A worksheet is an individual tab inside that spreadsheet.

A spreadsheet can contain multiple worksheets, each storing a different category of information.

In this implementation, the spreadsheet is used as a bakery order register, and its worksheet contains customer-order records.

## 3.6 What Is a Header Row?

A header row contains the column names describing the information stored in each column.

For example:

- Customer Name
- Item
- Quantity
- Order Date
- Eggless

Headers make records understandable and help organize the data into a consistent structure.

## 3.7 What Is `append_row()`?

`append_row()` is a `gspread` method that adds a new row of values to the worksheet.

The supplied values are placed into the next available row according to the spreadsheet's append behavior.

This is useful for maintaining a register in which new customer orders are added without overwriting existing records.

## 3.8 What Is a Logging Tool?

A logging tool is a function used to record information or events in a persistent destination.

In this task, `log_bakery_order` is created as a tool that saves order details into Google Sheets.

The function accepts order details as input and writes them to the worksheet.

The spreadsheet serves as the external record of the submitted order.

## 3.9 What Is Persistent Storage?

Persistent storage means data remains available after the current program execution ends.

Unlike a normal Python variable, which generally exists only during the program's execution, data stored in Google Sheets remains saved in the spreadsheet until it is changed or deleted.

This makes it possible to retrieve order records in later sessions.

## 3.10 Implementation

Google authentication was performed in Colab, and the `gspread` library was used to connect to Google Sheets.

A spreadsheet named `Sweet Crumbs Bakery Orders` was opened or created, and the worksheet was prepared with column headers.

A tool named `log_bakery_order` was implemented to append customer-order information to the worksheet.

A sample record was submitted and the saved data was retrieved to verify that the integration worked.

## 3.11 Outcome

Successfully connected Python with Google Sheets and stored customer-order records externally.

This demonstrates how an AI agent's tools can interact with external applications and maintain persistent business information.

---

# Task 4: Tool Naming and Description Experiment

## 4.1 What Is Tool Selection?

Tool selection is the process through which an AI agent determines which available tool is appropriate for a given user request.

An agent may have access to multiple tools, each designed for a different purpose.

When a user asks a question, the LLM evaluates the request and the available tool information to determine whether a tool is required and which tool should be called.

The agent's selection depends on factors such as the request, tool name, tool description, and available input schema.

## 4.2 Why Are Tool Names Important?

A tool name communicates its intended functionality.

Descriptive names such as `get_price` or `check_advance_notice` make the purpose of a tool easier to understand.

Poorly chosen names such as `tool1` provide little information about the function's purpose.

Clear names help the LLM distinguish between tools and select the one that matches the user's request.

## 4.3 Why Are Tool Descriptions Important?

Tool descriptions explain what a tool does and when it should be used.

The LLM uses the available tool descriptions as context when deciding which tool is relevant to a request.

A descriptive docstring helps the model understand the tool's purpose, inputs, and intended use.

A vague description such as `does stuff` does not provide meaningful information about the functionality of the tool.

## 4.4 What Is a Tool Schema?

A tool schema describes the structure of a tool's inputs, including parameter names and data types.

The schema helps the LLM understand what information must be provided when calling the tool.

For example, a pricing tool may require an item name as a string.

The model must provide an input that matches the expected schema when requesting the tool's execution.

## 4.5 What Is an AI Agent?

An AI agent is a system that uses an LLM to interpret a request, decide what steps to take, and use available tools when necessary to complete a task.

Unlike a basic LLM interaction that directly generates text, a tool-enabled agent can request the execution of functions and use their returned results in its response.

A typical tool-enabled agent workflow is:

1. Receive the user's request.
2. Analyze the request.
3. Identify whether a tool is required.
4. Select an appropriate tool.
5. Generate a tool call with the required inputs.
6. Receive the tool result.
7. Use the result to generate a response.

## 4.6 What Is `create_agent()`?

`create_agent()` is a LangChain function used to create an agent with a model and a set of tools.

The model acts as the reasoning component, while the tools provide capabilities that the model can request during execution.

The agent manages the interaction between the model and the tools according to the agent workflow.

## 4.7 What Is the Tool-Calling Mechanism?

Tool calling is the process in which the model generates a structured request to invoke a tool instead of directly answering the user.

The model does not directly execute the Python function itself. It produces a tool-call request, and the agent framework executes the requested tool, returns the result to the model, and continues the interaction.

This separation between the model's decision and the tool's execution is a key part of tool-enabled agent architecture.

## 4.8 Experiment: Descriptive Name vs. Poor Name

The same business question was tested using a descriptive tool and a poorly named tool.

The descriptive tool used a meaningful name and docstring.

The experimental tool was renamed to `tool1` and its description was changed to `does stuff`.

The agent was asked the same pricing question in both scenarios, and its tool calls were inspected.

This experiment helps demonstrate the importance of providing clear tool metadata to the LLM.

## 4.9 Outcome

Observed the relationship between tool metadata and the agent's tool-selection process.

This experiment demonstrates why tools should have meaningful names, clear descriptions, and well-defined input schemas when building reliable AI agents.

---

# Task 5: Agent Trace Analysis

## 5.1 What Is an Agent Trace?

An agent trace is a record of the messages and interactions generated during an agent's execution.

It helps developers understand how the agent processed a request, which tools it selected, what inputs it supplied, what results it received, and how it generated its final response.

Agent traces are useful for debugging, monitoring, understanding execution behavior, and analyzing agent workflows.

## 5.2 What Is an Agent Message?

An agent interaction can contain different types of messages.

These messages represent different stages of the interaction, including user input, AI responses, tool requests, and tool results.

By inspecting the message sequence, developers can understand the flow of execution.

## 5.3 What Is `AIMessage`?

`AIMessage` represents a message generated by the AI model.

It may contain ordinary text, a tool-call request, or both, depending on the interaction.

When the model requests a tool, the `AIMessage` can contain structured tool-call information, including the tool name and arguments.

Counting AI messages in a trace helps examine the number of AI message entries present in the recorded interaction.

## 5.4 What Is `ToolMessage`?

`ToolMessage` represents the response returned after a tool has been executed.

It contains the result of the tool execution, which is made available to the agent for further processing.

The model can use this result to continue reasoning or prepare its final response.

## 5.5 What Is `tool_calls`?

`tool_calls` is a property of an AI message that contains tool-call requests made by the model.

Each tool call identifies the requested tool and includes the arguments to be supplied to it.

A single AI message can contain multiple tool calls, so counting AI messages alone is not sufficient to determine the total number of tool calls.

The number of tool calls can be calculated by counting the entries in the `tool_calls` collection of each AI message.

## 5.6 What Is `pretty_print()`?

`pretty_print()` is a message method used to display message information in a readable format.

It makes it easier to inspect the content and structure of messages in the agent trace, including AI responses and tool interactions.

It is useful when examining the execution sequence of an agent without manually accessing every message field.

## 5.7 What Is Trace Analysis?

Trace analysis involves examining recorded execution information to understand how a system behaved.

In an AI agent, trace analysis can help identify:

- How many AI messages were generated in the captured trace.
- How many tool calls were requested.
- Which tools were selected.
- What inputs were provided to the tools.
- What results were returned.
- How the agent arrived at its final response.

Trace analysis is useful for debugging unexpected behavior, evaluating tool usage, and improving agent design.

## 5.8 Counting AI Messages and Tool Calls

The captured trace was inspected by iterating through the messages.

The number of `AIMessage` instances was counted to determine the AI message entries.

For each AI message, the number of entries in `tool_calls` was added to the total tool-call count.

`ToolMessage` instances were counted separately to identify the tool responses present in the trace.

These counts represent the recorded message and tool-call information, not necessarily the provider's complete internal execution or billing-level model-call count.

## 5.9 Implementation

An agent was created with the bakery tools and supplied with a question requiring business information.

The execution trace was captured and displayed using `pretty_print()`.

The trace was then inspected to calculate the number of AI messages, tool calls, and tool responses.

## 5.10 Outcome

Successfully inspected an agent's execution trace and identified AI messages, tool calls, and tool responses.

This demonstrates how execution traces can be used to understand and analyze an agent's behavior.

---

# Overall Workflow

The five tasks demonstrate how different LangChain and Python concepts work together to build tool-enabled AI applications.

1. Python functions are converted into tools using the `@tool` decorator.
2. Pydantic defines a structured schema for customer-order information.
3. `with_structured_output()` extracts information from natural-language messages into the defined schema.
4. Google Sheets integration provides an external destination for storing business records.
5. Logging tools enable information to be written to an external application.
6. An agent uses an LLM to select tools according to the user's request.
7. Tool names, descriptions, and schemas provide context for tool selection.
8. Agent traces provide a record of messages, tool calls, and tool responses.
9. Trace analysis helps developers understand, inspect, and debug agent execution.

## Technologies Used

- **Python** – Programming language used to implement functions, tools, and data-processing logic.
- **LangChain** – Framework for building LLM applications, creating tools, structured-output workflows, and agents.
- **Groq** – LLM inference platform used to run the selected language model.
- **Pydantic** – Library used to define and validate structured data models.
- **Google Colab** – Cloud-based notebook environment used for implementation and testing.
- **gspread** – Python library used to interact with Google Sheets.
- **Google Authentication** – Used to authenticate access to Google services.

## Conclusion

Day 4 explored the core mechanisms used to extend LLMs into tool-enabled AI agents.

The implementation demonstrated custom tool creation, structured information extraction, external data storage, tool selection, and agent trace inspection.

These concepts form an important foundation for developing agentic AI systems capable of interacting with external tools, handling structured information, and performing multi-step tasks beyond basic text generation.
