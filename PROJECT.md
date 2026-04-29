Introduction
Welcome! Imagine yourself as a trusted and seasoned consultant specialized in building smart, efficient, and powerful agent-based workflows. Businesses rely on you to solve their complex operational challenges with cutting-edge solutions. Your latest client, the Beaver's Choice Paper Company, urgently requires your expertise to revolutionize their inventory management and quoting system. Your role? Develop a multi-agent system that streamlines their operations, enabling quick quote generation, accurate inventory tracking, and ultimately driving increased sales.

The Challenge
The Beaver's Choice Paper Company is struggling with managing their paper supplies, responding promptly to customer inquiries, and generating competitive quotes. They're overwhelmed and losing potential sales due to inefficiencies. Your challenge is to design and implement a multi-agent solution, restricted to at most five agents, capable of handling inquiries, checking inventory status, providing accurate quotations, and completing transactions seamlessly. Your solution must ensure responsiveness, accuracy, and reliability in managing requests and maintaining optimal stock levels.

Core Components of the Multi-agent System
In this project, you must ensure that the Beaver's Choice Paper Company's needs are met through a multi-agent system implementation. To maintain simplicity and effectiveness, the system should involve at most five agents. Your solution will handle strictly text-based inputs and outputs, and you will verify its performance using a provided set of sample requests. Begin your project by creating a diagram that clearly outlines your intended workflow. You may choose among three Python frameworks for your agent implementation: smolagents, pydantic-ai, or npcpy. Your completed program should contain agents that can:

Answer questions regarding current inventory and manage the reordering of supplies when necessary, demonstrating your agents' ability to use database information effectively and to make purchase decisions.
Provide accurate and intelligent quotes for potential customers by considering historical quote data and pricing strategies.
Efficiently finalize sales transactions based on the available inventory and delivery timelines.
Your submission must include:

The workflow diagram (an image file)
Your source code (only one python file should be submitted)
A detailed document that thoroughly explains the system you've built and describes how you ensured it meets all specified requirements.
You'll utilize the knowledge that you gained about multi-agent systems along with your skills in Python programming, database management (sqlite3), and an agent orchestration framework of your choice to execute this project.

Project Summary
This exciting 6-hour project is divided into key steps:

Diagramming & Planning: Create a detailed flow diagram outlining your multi-agent system.
Implementation: Develop your multi-agent system using Python and your chosen agent framework.
Testing & Debugging: Thoroughly test your agents using provided sample inputs to ensure robust performance.
Documentation: Write a comprehensive report explaining your system, your design decisions, and how your solution meets the project requirements.
Ready to revolutionize inventory and quoting management for the Beaver's Choice Paper Company? Let's get started!

What Are Vocareum OpenAI API Keys?
OpenAI API keys provide access to paid OpenAI services. Vocareum is a provider that Udacity uses to grant learners access to these keys as part of enrolling in a Udacity program.

Unlike API keys that come directly from OpenAI, Vocareum OpenAI API keys must be routed through Vocareum servers, allowing Udacity to manage API usage budgets.

Finding Your Vocareum OpenAI API Key
You will find this on the “Cloud Resources” button on the navigation pane. By clicking into the “Cloud Resources” button, you will be provided with a OpenAI API key along with the budget assigned to that key.

Under the "OpenAI Key" header, there is a value starting with "voc" as well as an info panel showing "You have $4.9757645 left of your $5 budget for this program"
Your Budget
As you use up the credits, you can come back to that screen to see how much budget you have left. Note that while the key may appear at the lesson level, this budget may be shared across the broader Udacity program (course or Nanodegree program).

The budgets are set to align with the demos, exercises, and projects in the program. To avoid prematurely running out of your budgeted credits, do not use models or endpoints beyond those indicated in the program content.

Using Vocareum OpenAI API Keys
Code that uses Vocareum OpenAI API keys must include the appropriate configuration so the requests are routed to the Vocareum server.

The Python code for this configuration depends on the version of the openai package being used. The following examples use a placeholder example API key, which must be replaced with your actual key.

OpenAI Python Package Version 0
import openai
openai.api_base = "https://openai.vocareum.com/v1"
openai.api_key = "voc-00000000000000000000000000000000abcd.12345678"
OpenAI Python Package Version 1
from openai import OpenAI
client = OpenAI(
base_url = "https://openai.vocareum.com/v1",
api_key = "voc-00000000000000000000000000000000abcd.12345678"
)
REST API Calls
If using curl or another client to access the OpenAI API, build the URLs using https://openai.vocareum.com/v1 in place of https://api.openai.com/v1

Re-Issuing API Keys
Udacity will not reissue the Vocareum API key. Treat this key as highly sensitive and store it securely at all times. Exercise extreme caution when sharing or uploading the key, especially to large language models or third-party tools, as it may be exposed or compromised.

Project Instructions
Step 1: Draft Your Agent Workflow
Begin by drafting a diagram illustrating the interactions and data flows between the agents in your multi-agent system. Your diagram should demonstrate the sequence of operations for handling customer inquiries, inventory management, quote generation, and order fulfillment. Some recommended agents for your multi-agent system are as follows:

An orchestrator agent for handling customer inquiries and delegating tasks to different agents
Answer inventory queries accurately, including deciding when to reorder supplies
Generate quotes efficiently, applying bulk discounts strategically to encourage sales
Finalize sales transactions, considering inventory levels and delivery timelines
These agents should also have access to tools that allow them to interact with the system database and the outside world. Some recommended tools that might help you flesh out your system are:

A tool that checks inventory for different paper types
A tool that gets quote history related to a customer's request
A tool that checks the timeline for delivery of an item from the supplier
A tool that fulfills orders by updating the system database
Note that these recommendations for agents and tools are only recommendations. You may want to design the architecture of your multi-agent system differently. To understand more about the context of this project, you may want to do some reading on inventory and sales management in companies selling physical products.

You can use diagramming tools like Diagrams.net(opens in a new tab) or Mermaid(opens in a new tab) to create your diagrams.

Step 2: Review the Starter Code
Carefully examine the provided starter code (project_starter.py) in your workspace. This code includes essential functionalities such as:

Initializing and managing an SQLite database
Managing inventory stock levels
Generating and tracking financial transactions
Utility functions to estimate supplier delivery dates and current cash balance
At the bottom of the project_starter.py file, you'll find a provided code stub designed to help you evaluate your agent implementation. You can use this stub to test and refine your system effectively.

Spend at least 30 minutes reviewing the starter file. Write brief descriptions for each function provided to ensure you thoroughly understand their purpose and usage within your system.

Once you complete your review, revisit your agent flow draft from Step 1. Update the tools you initially outlined, replacing hypothetical tools with tools defined using the helper functions provided in the starter code based on your newfound understanding.

Step 3: Select Your Agent Framework
Decide on the agent orchestration framework you will use for this project. Your options include:

smolagents: Link to documentation(opens in a new tab)
pydantic-ai: Link to documentation(opens in a new tab)
npcsh: Link to documentation(opens in a new tab)
Make sure you are comfortable with your chosen framework and that it aligns well with the requirements and your intended agent interactions.

Step 4: Implement Your System
Using the framework you have selected, implement the agents based on the updated flow you refined in Step 2. Ensure your system follows the agent workflow diagram you drafted in step 1. Feel free to update the diagram based on changes to your approach if any hiccups arise during the implementation.

You can get started by creating different agents which accomplish each of these tasks and an orchestration agent that orchestrates the flow of control and data between the different agents. Use the helper functions provided in the starter file to aid the definition of tools for the different worker agents. Additionally, refer to the project rubric to thoroughly understand the requirements and criteria for successful completion of your system.

Step 5: Test and Evaluate Your Implementation
Test your multi-agent system thoroughly using the provided dataset (quote_requests_sample.csv). Ensure:

Your agents correctly handle various customer inquiries and orders
Orders are accommodated effectively to optimize inventory use and profitability
The quoting agent consistently provides competitive and attractive pricing
Refer to the project rubric at the end of this step to evaluate the results documented in the test_results.csv file.

Step 6: Reflect and Document
After evaluating your system, prepare a clear and concise report detailing:

A comprehensive explanation of your multi-agent system
Evaluation results (test_results.csv generated by the evaluation code) highlighting strengths and areas for improvement
Suggestions for further improvements to the system based on the areas of improvement.
Your final submission should include:

Your updated agent flow diagram
Your completed implementation script
Your reflective report with evaluations
Ensure that you check the project rubric to understand the requirements from the different parts of the project before submitting it. You submission will be reviewed against the project rubric.

Local setup instructions
Install dependencies
Make sure you have Python 3.8+ installed.

You can install all required packages using the provided requirements.txt file:

pip install -r requirements.txt

If you're using smolagents, install it separately:

pip install smolagents

For other options like pydantic-ai or npcsh[lite], refer to their documentation.

Create .env File
Add your OpenAI-compatible API key:

UDACITY_OPENAI_API_KEY=your_openai_key_here

This project uses a custom OpenAI-compatible proxy hosted at https://openai.vocareum.com/v1(opens in a new tab).

Rubric
Use this project rubric to understand and assess the project criteria.

Agent Workflow Diagram
Criteria Submission Requirements
Illustrate the architecture of the multi-agent system, including agent responsibilities and orchestration.

The workflow diagram includes all of the agents in the multi-agent system (maximum of five agents as per project constraints).
Each agent has explicitly defined responsibilities that do not overlap with other systems.
The orchestration logic and data flow between agents is clear.
Illustrate the interactions between agents and their tools, specifying the purpose of each tool.

The workflow diagram depicts tools associated with specific agents.
For each tool depicted, its purpose and the specific helper function(s) from the starter code it intends to use is specified in the diagram.
The diagram shows interactions (e.g., data input/output) between agents and their respective tools.
Multi-Agent System Implementation
Criteria Submission Requirements
Implement the multi-agent system with distinct orchestrator and worker agent roles as per their diagram.

The implemented multi-agent system architecture (agents, their primary roles) matches the submitted agent workflow diagram.
The system includes an orchestrator agent that manages task delegation to other agents.
The system implements distinct worker agents (or clearly separated functionalities within agents) for different tasks such as:
Inventory management (e.g., checking stock, assessing reorder needs)
Quoting (e.g., generating prices, considering discounts)
Sales finalization (e.g., processing orders, updating database).
The student selects and utilizes one of the recommended agent orchestration frameworks (smolagents, pydantic-ai, or npcsh) for the implementation.
Implement tools for agents using the provided helper functions, ensuring all required functions are utilized.

Tools for different agents are defined in the code according to the conventions of the selected agent orchestration framework.
All of the following helper functions from the starter code are used in at least one tool definition within the implemented system: create_transaction, get_all_inventory, get_stock_level, get_supplier_delivery_date, get_cash_balance, generate_financial_report, search_quote_history.
Evaluation and Reflection
Criteria Submission Requirements
Evaluate the multi-agent system using the provided dataset and document the results.

The multi-agent system is evaluated using the full set of requests provided in quote_requests_sample.csv and the results of the evaluation are submitted in test_results.csv.
The test_results.csv file (or equivalent documented output) demonstrates that:
At least three requests result in a change to the cash balance.
At least three quote requests are successfully fulfilled.
Not all requests from quote_requests_sample.csv are fulfilled, with reasons provided or implied for unfulfilled requests (e.g., insufficient stock).
Reflect on the architecture, implementation, and performance evaluation of the multi-agent system.

The reflection report:

contains an explanation of the agent workflow diagram, detailing the roles of the agents and the decision-making process that led to the chosen architecture. The student may refer to their diagram file, but the explanation must be in this text report.
discusses the evaluation results from test_results.csv, identifying specific strengths of the implemented system. The student may refer to their test_results.csv file, but the discussion must be in this text report.
includes at least two distinct suggestions for further improvements to the system, based on the identified areas of improvement or new potential features.
Industry Best Practices
Criteria Submission Requirements
Provide transparent and explainable outputs for customer-facing interactions.

Outputs generated by the system (e.g., quotes, responses to inquiries) for the "customer" contain all the information directly relevant to the customer's request.
Outputs provided to the "customer" include a rationale or justification for key decisions or outcomes, where appropriate (e.g., why a quote is priced a certain way if discounts are applied, why an order cannot be fulfilled).
Customer-facing outputs do not reveal sensitive internal company information (e.g., exact profit margins, internal system error messages) or any personally identifiable information (PII) beyond what's essential for the transaction.
Write code that is readable, well-commented, and modular.

Variable and function names in the Python code are descriptive and consistently follow a discernible naming convention (e.g., snake_case for functions and variables, PascalCase for classes, if applicable).
The code consists of comments and docstrings at appropriate places.
Logic within the code has been broken down sufficiently into individual modules.
Suggestions to Make Your Project Stand Out
Create a customer agent that uses the customer context from the sample requests to then can negotiate with the team multi-agent system here.
Make a terminal animation that builds on top of outputs from various agents in the multi-agent system to show the customer how their request is being processed.
Add a business advisor agent that analyses all the transactions being handled by the multi-agent system and proactively recommends changes to the business operations in order to improve its efficiency and revenue.
