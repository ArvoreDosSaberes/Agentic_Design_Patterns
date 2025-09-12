# Chapter 3: Parallelization

## Parallelization Pattern Overview

In the previous chapters, we've explored Prompt Chaining for sequential workflows and Routing for dynamic decision-making and transitions between different paths. While these patterns are essential, many complex agentic tasks involve multiple sub-tasks that can be executed simultaneously rather than one after another. This is where the Parallelization pattern becomes crucial.

Parallelization involves executing multiple components, such as LLM calls, tool usages, or even entire sub-agents, concurrently. Instead of waiting for one step to complete before starting the next, parallel execution allows independent tasks to run at the same time, significantly reducing the overall execution time for tasks that can be broken down into independent parts.

Consider an agent designed to research a topic and summarize its findings.

A sequential approach might:

1. Search for Source A.
2. Summarize Source A.
3. Search for Source B.
4. Summarize Source B.
5. Synthesize a final answer from summaries A and B.

A parallel approach could instead:

1. Search for Source A and Search for Source B simultaneously.
2. Once both searches are complete, Summarize Source A and Summarize Source B simultaneously.
3. Synthesize a final answer from summaries A and B (this step is typically sequential, waiting for the parallel steps to finish).

The core idea is to identify parts of the workflow that do not depend on the output of other parts and execute them in parallel. This is particularly effective when dealing with external services (like APIs or databases) that have latency, as you can issue multiple requests concurrently.

Implementing parallelization often requires frameworks that support asynchronous execution or multi-threading/multi-processing. Modern agentic frameworks are designed with asynchronous operations in mind, allowing you to easily define steps that can run in parallel.

Frameworks like LangChain, LangGraph, and Google ADK provide mechanisms for parallel execution. In LangChain Expression Language (LCEL), you can achieve parallel execution by combining runnable objects using operators and structures like `RunnableParallel`. LangGraph, with its graph structure, allows you to define multiple nodes that can be executed from a single state transition, effectively enabling parallel branches in the workflow. Google ADK also facilitates parallel execution through multi-agent delegation and primitives like `ParallelAgent`.

## Practical Applications & Use Cases

Parallelization optimizes performance across scenarios such as:

1. Information Gathering and Research: Search news, stocks, social media, DBs at once.
2. Data Processing and Analysis: Run sentiment, keywords, categorization concurrently.
3. Multi-API or Tool Interaction: Check flights, hotels, events, restaurants in parallel.
4. Content Generation with Multiple Components: Subject, body, image selection, CTA generation together.
5. Validation and Verification: Validate email, phone, address, profanity simultaneously.
6. Multi-Modal Processing: Analyze text and image of a post concurrently.
7. A/B Testing or Options Generation: Produce multiple variations concurrently and select the best.

## Hands-On Code Example (LangChain)

```python
# Requirements: pip install langchain langchain-community langchain-openai
import os
import asyncio
from typing import Optional
from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser
from langchain_core.runnables import Runnable, RunnableParallel, RunnablePassthrough

# Initialize LLM (ensure OPENAI_API_KEY is set)
llm: Optional[ChatOpenAI] = ChatOpenAI(model="gpt-4o-mini", temperature=0.7)

# Independent chains
summarize_chain: Runnable = (
    ChatPromptTemplate.from_messages([
        ("system", "Summarize the following topic concisely:"),
        ("user", "{topic}")
    ])
    | llm
    | StrOutputParser()
)

questions_chain: Runnable = (
    ChatPromptTemplate.from_messages([
        ("system", "Generate three interesting questions about the following topic:"),
        ("user", "{topic}")
    ])
    | llm
    | StrOutputParser()
)

terms_chain: Runnable = (
    ChatPromptTemplate.from_messages([
        ("system", "Identify 5-10 key terms from the following topic, separated by commas:"),
        ("user", "{topic}")
    ])
    | llm
    | StrOutputParser()
)

# Execute in parallel and pass through original topic
map_chain = RunnableParallel(
    {
        "summary": summarize_chain,
        "questions": questions_chain,
        "key_terms": terms_chain,
        "topic": RunnablePassthrough(),
    }
)

synthesis_prompt = ChatPromptTemplate.from_messages([
    ("system", """Based on the following information:\nSummary: {summary}\nRelated Questions: {questions}\nKey Terms: {key_terms}\nSynthesize a comprehensive answer."""),
    ("user", "Original topic: {topic}")
])

full_parallel_chain = map_chain | synthesis_prompt | llm | StrOutputParser()

async def run_parallel_example(topic: str) -> None:
    if not llm:
        print("LLM not initialized.")
        return
    print(f"\n--- Running Parallel LangChain Example for Topic: '{topic}' ---")
    response = await full_parallel_chain.ainvoke(topic)
    print("\n--- Final Response ---")
    print(response)

if __name__ == "__main__":
    test_topic = "The history of space exploration"
    asyncio.run(run_parallel_example(test_topic))
```

Note: `asyncio` provides concurrency on a single thread via an event loop; true parallelism may require multi-processing or threads for CPU-bound workloads.

## Hands-On Code Example (Google ADK)

Below is a conceptual outline using ADK primitives where three researcher agents run in parallel and a merger agent synthesizes results.

```python
from google.adk.agents import LlmAgent, ParallelAgent, SequentialAgent
from google.adk.tools import google_search

GEMINI_MODEL = "gemini-2.0-flash"

researcher_agent_1 = LlmAgent(
    name="RenewableEnergyResearcher",
    model=GEMINI_MODEL,
    instruction=(
        "Research 'renewable energy sources' using google_search and output a 1-2 sentence summary."
    ),
    tools=[google_search],
    output_key="renewable_energy_result"
)

researcher_agent_2 = LlmAgent(
    name="EVResearcher",
    model=GEMINI_MODEL,
    instruction=(
        "Research 'electric vehicle technology' using google_search and output a 1-2 sentence summary."
    ),
    tools=[google_search],
    output_key="ev_technology_result"
)

researcher_agent_3 = LlmAgent(
    name="CarbonCaptureResearcher",
    model=GEMINI_MODEL,
    instruction=(
        "Research 'carbon capture methods' using google_search and output a 1-2 sentence summary."
    ),
    tools=[google_search],
    output_key="carbon_capture_result"
)

parallel_research_agent = ParallelAgent(
    name="ParallelWebResearchAgent",
    sub_agents=[researcher_agent_1, researcher_agent_2, researcher_agent_3],
)

merger_agent = LlmAgent(
    name="SynthesisAgent",
    model=GEMINI_MODEL,
    instruction=(
        "Synthesize the three input summaries into a structured report with sections and an overall conclusion."
    )
)

root_agent = SequentialAgent(
    name="ResearchAndSynthesisPipeline",
    sub_agents=[parallel_research_agent, merger_agent]
)
```

## At a Glance

- Parallelization executes independent tasks concurrently to improve efficiency.
- Useful when tasks involve waiting for external resources (APIs, DBs).
- Adds complexity in design, debugging, and logging; use judiciously.
- LCEL `RunnableParallel` and ADK `ParallelAgent` help structure concurrent execution.

## References

1. LCEL Parallelism: https://python.langchain.com/docs/concepts/lcel/
2. Google ADK Multi-Agents: https://google.github.io/adk-docs/agents/multi-agents/
3. Python asyncio: https://docs.python.org/3/library/asyncio.html

<!-- nav-prev-next -->
| Anterior | Próximo |
| --- | --- |
| [Chapter 2: Routing](chapter-02-routing.md) | [Chapter 4: Reflection](chapter-04-reflection.md) |
