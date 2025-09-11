# Chapter 2: Routing

## Routing Pattern Overview

While sequential processing via prompt chaining is a foundational technique for executing deterministic, linear workflows with language models, its applicability is limited in scenarios requiring adaptive responses. Real-world agentic systems must often arbitrate between multiple potential actions based on contingent factors, such as the state of the environment, user input, or the outcome of a preceding operation. This capacity for dynamic decision-making, which governs the flow of control to different specialized functions, tools, or sub-processes, is achieved through a mechanism known as routing.

Routing introduces conditional logic into an agent's operational framework, enabling a shift from a fixed execution path to a model where the agent dynamically evaluates specific criteria to select from a set of possible subsequent actions. This allows for more flexible and context-aware system behavior.

For instance, an agent designed for customer inquiries, when equipped with a routing function, can first classify an incoming query to determine the user's intent. Based on this classification, it can then direct the query to a specialized agent for direct question-answering, a database retrieval tool for account information, or an escalation procedure for complex issues, rather than defaulting to a single, predetermined response pathway. Therefore, a more sophisticated agent using routing could:

1. Analyze the user's query.
2. Route the query based on its intent:
   - If the intent is "check order status", route to a sub-agent or tool chain that interacts with the order database.
   - If the intent is "product information", route to a sub-agent or chain that searches the product catalog.
   - If the intent is "technical support", route to a different chain that accesses troubleshooting guides or escalates to a human.
   - If the intent is unclear, route to a clarification sub-agent or prompt chain.

The core component of the Routing pattern is a mechanism that performs the evaluation and directs the flow. This mechanism can be implemented in several ways:

- LLM-based Routing
- Embedding-based Routing
- Rule-based Routing
- Machine Learning Model-Based Routing

Routing mechanisms can be implemented at multiple junctures within an agent's operational cycle: at the outset to classify a primary task, at intermediate points within a processing chain to determine a subsequent action, or during a subroutine to select the most appropriate tool from a given set.

## Practical Applications & Use Cases

The routing pattern is a critical control mechanism in the design of adaptive agentic systems, enabling them to dynamically alter their execution path in response to variable inputs and internal states. Its utility spans multiple domains by providing a necessary layer of conditional logic.

- Human-computer interaction: interpret user intent and select appropriate tools or escalation paths.
- Automated pipelines: classify and direct emails, tickets, or payloads to specialized workflows.
- Multi-agent systems: act as a dispatcher across search, summarize, analyze agents.

Ultimately, routing transforms an agent from a static executor of pre-defined sequences into a dynamic system that can make decisions about the most effective method for accomplishing a task under changing conditions.

## Hands-On Code Example (LangChain)

```python
# Requirements: pip install langchain langchain-google-genai
from langchain_google_genai import ChatGoogleGenerativeAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser
from langchain_core.runnables import RunnablePassthrough, RunnableBranch

# Initialize LLM (ensure GOOGLE_API_KEY is set)
llm = ChatGoogleGenerativeAI(model="gemini-2.5-flash", temperature=0)

# Router chain: decide destination
coordinator_router_prompt = ChatPromptTemplate.from_messages([
    ("system", """
Analyze the user's request and determine which specialist handler should process it.
- If the request is related to booking flights or hotels, output 'booker'.
- For general information questions, output 'info'.
- If unclear, output 'unclear'.
ONLY output one word: 'booker', 'info', or 'unclear'.
"""),
    ("user", "{request}")
])
coordinator_router_chain = coordinator_router_prompt | llm | StrOutputParser()

# Simulated handlers
def booking_handler(request: str) -> str:
    return f"Booking Handler processed: {request}"

def info_handler(request: str) -> str:
    return f"Info Handler processed: {request}"

def unclear_handler(request: str) -> str:
    return f"Coordinator could not delegate: {request}. Please clarify."

# Branching
branches = {
    "booker": RunnablePassthrough.assign(output=lambda x: booking_handler(x['request']['request'])),
    "info": RunnablePassthrough.assign(output=lambda x: info_handler(x['request']['request'])),
    "unclear": RunnablePassthrough.assign(output=lambda x: unclear_handler(x['request']['request'])),
}

delegation_branch = RunnableBranch(
    (lambda x: x['decision'].strip() == 'booker', branches["booker"]),
    (lambda x: x['decision'].strip() == 'info', branches["info"]),
    branches["unclear"]
)

coordinator_agent = {
    "decision": coordinator_router_chain,
    "request": RunnablePassthrough()
} | delegation_branch | (lambda x: x['output'])

# Example
if __name__ == "__main__":
    for req in ["Book me a flight to London.", "What is the capital of Italy?", "Tell me about quantum physics."]:
        print(coordinator_agent.invoke({"request": req}))
```

## Hands-On Code Example (Google ADK)

The Agent Development Kit (ADK) implements routing through tools and sub-agents. A Coordinator agent delegates to specialized agents based on instructions, leveraging the framework's auto-flow.

```python
# Pseudocode sketch (see official ADK docs for full runnable code)
from google.adk.agents import Agent
from google.adk.runners import InMemoryRunner
from google.adk.tools import FunctionTool

# Tools
booking_tool = FunctionTool(lambda request: f"Booking action for '{request}' simulated.")
info_tool = FunctionTool(lambda request: f"Information request for '{request}' simulated.")

# Sub-agentsooking_agent = Agent(name="Booker", model="gemini-2.0-flash", tools=[booking_tool])
info_agent = Agent(name="Info", model="gemini-2.0-flash", tools=[info_tool])

# Coordinator
autoflow_coordinator = Agent(
    name="Coordinator",
    model="gemini-2.0-flash",
    instruction=(
        "Analyze user requests and delegate: 'Booker' for booking, 'Info' for others."
    ),
    sub_agents=[booking_agent, info_agent]
)

# Runner usage omitted for brevity
```

## At a Glance

- Routing enables agents to make dynamic decisions about the next step in a workflow.
- Moves systems beyond linear execution to adaptive behavior.
- Implement with LLM prompts, rules, embeddings, or trained classifiers.
- LangGraph/ADK offer structured primitives for routing within agent workflows.

## References

1. LangGraph: https://www.langchain.com/
2. Google Agent Developer Kit (ADK): https://google.github.io/adk-docs/
