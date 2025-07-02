---
layout: post
title: A Deep Researcher with Burr 
---

Recently I made my first significant [contribution](https://github.com/apache/burr/pull/530) to an open source project.  I added a substantial example to Burr, an open source framework from [DAGworks Inc](https://www.dagworks.io/). As of May 2025, Burr is an [Apache incubator project](https://incubator.apache.org/projects/burr.html). The goal of Burr is to facilitate managing the state of AI applications. 

The example I added implements an AI application called a reasoner; in particular, a "deep researcher."  Most people are familiar with AI chatbots like OpenAI's chatgpt. A deep researcher provides a more thorough and robust answer to research queries than a regular chatbot, and adds links to sources for the information it provides. Deep researcher reasoners are increasingly popular commercial products, with Google and OpenAI both offering one at a price to users.  This fact suggests the possibility of open source implementations.  

This example's particular research flow was adapted from LangChain's 
[Deep Researcher codebase](https://github.com/langchain-ai/local-deep-researcher). [LangChain](https://www.langchain.com/) offers a range of products to support AI applications, including an open source state-management framework called LangGraph.  In adapting the LangChain implementation, I replaced LangGraph with Burr.  

Why Burr?  For me, Burr's significant advantage over LangGraph is that its graphical user interface for observability is *also* self-hosted and open source.  Observability into the state of an AI application is essential for debugging it.   LangGraph's observability platform, [LangSmith](https://www.langchain.com/langsmith), requires an API key and its code is not open source.  AI agents and reasoners already require API integrations, often multiple ones, so minimizing them is both cost effective and time saving.  

The deep researcher flow is taken from the original LangGraph example. The following visualization shows the graph for the application.  
![my_graph]({{site.url}}/images/statemachine.png)  

In this simple case, the researcher uses a chatbot both to formulate a query and summarize information. In between these actions, for the search process itself, it employs a llm-friendly search engine.  This flow can be repeated multiple times in a reflective, self-improving fashion.The patterns in my code are basic Burr graph patterns, as described in the online documentation. Code to format queries and parse results is taken with attribution from the LangChain repository.

Burr's observability website also includes examples of applications written in the main framework.  The website uses python's [fastapi](https://fastapi.tiangolo.com/) on the backend and React on the frontend. It is non-trivial to integrate an AI application with a suitable API framework and a modern javascript frontend. However, that is what is need for a usable product. My application is also implemented as a Burr example.  Its code should help people looking to open source for guidance on putting deep researchers into production.  

Future developments to the workflow and the GUI could include adding
concurrency and streaming to the model. These additions would increase the deep researcher's power and to improve the user experience.  To build out the GUI for an enhanced researcher, one could consult other Burr examples that integrate streaming and concurrency with fastapi and React.  
