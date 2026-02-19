---
title: "How many MCPs have you enabled in your LLM?"
date: 2026-02-19
categories: 
  - "general"
  - "AI"
tags: 
  - "Model Context Protocol"
  - "MCP"
  - "LLM" 
  - "Context"
---

Context is the lifeline of LLM. Without context (or with invalid context) an LLM is nothing but a gibberish word generating machine. Context allows for the LLM to personalize, reason, provide coherence and grounding for any response it generates. The Context Window is the model's active memory. Claude Opus-4 for instance has a 200K token context window. It is huge and suffices for most of the tasks. But efficient use of the context window is also needed to improve coherence and dept in responses.

One more thing to take care of besides the context window size utilization is relevance of information in the context being used. Claude for instance has commands to clear & compact context window contents whenever an overflow occurs. Context size has a direct impact on the costs incurred as increased context size usage also means higher computation cost and potential performance issues (including hallucination - where the model promotes attention on the wrong aspect thus going off-track). The response times also increases a lot with LLM responses becoming slow and confusing.

Context window size limiations are constraints resulting from the self-attention mechanism, KV cache memory and GPU memory bandwidth. [LLM context windows: Understanding and optimizing working memory](https://redis.io/blog/llm-context-windows/) goes into a lot more details on optimizing the context window usage and how to make efficient use of smaller & larger context window management during development & production scenarios.

So where does Model Context Protocol (MCP) fit into all these? MCP allows the applications/LLMs to connect and communicate with external tools and data. MCP provides a standard interface that allows LLMs to access data spread across various data providers without worrying about API specifics, data formats, etc. Most of the LLMs/AI Agents support MCP. In my organization, we have almost 20-30 MCP servers for all the internal tools that are being used. These MCP servers allows a user to get data from various sources and give a well-formulated, coherent response to a query. One of my colleagues had all the MCP servers enabled by default in his AI agent. And he was always complaining of the slow LLM response as well as hallucinations.

And my experience is totally different on the same LLM server. So I looked at the context window and the contents of that and surprise, surprise! Just loading about 5-10 MCP clients eats up almost 50% of the context window size (200K window size). And that is just starting up the agent. One still hasn't initiated the conversation at all. So we are already halving the size of the usable context window by enabling all the different MCP clients that are available.

The more MCP clients that you have enabled, the more context size you eat up even before sending in your query to LLM. So there are 2 disadvantages here:
1. Increased cost as the context window is already filled-up with tools/MCP clients irrelevant to the current function.
2. Less space to fit any additional conversation/history that might provide accurate context to the LLMs for generating responces.

So in general, disable all the MCPs that are not needed for the current task. MCPs which are not intrinsic to ones current task are just noise and will lead to hallucinations and increased costs. Useless MCPs like the ones checking for a weather forecast or email are not needed (use OpenClaw for that kind of tasks). And enabling an MCP to update the documentation while fixing bugs or grepping a bug database can be done separately outside of the current context window thus freeing up more space for the relevant conversation with LLM (as well as reducing token usage cost).

I generally disable all MCPs for my main sessions. If there is a need to enable an MCP, I use a separate session, get that particular granular task done and then return to my main session. What approach do you suggest WRT MCP and LLM token usage?