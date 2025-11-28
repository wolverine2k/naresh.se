---
title: "Integrate Tavily Search with Langchain"
date: 2025-11-28
categories: 
  - "general"
  - "AI"
tags: 
  - "LLMs"
  - "AIDE"
  - "Artificial"
  - "Intelligence"
  - "LocalAI"
  - "Langchain"
  - "Tavily"
  - "OpenAI"
---

Something amazingly simple turned out to be amazingly weird! I was trying to create a react agent that uses tavily search to fetch relevant articles and then uses openai (on localai server) to generate a response based on the articles. I was following the [Langchain docs](https://js.langchain.com/docs/integrations/tools/tavily_search) and the [tavily search docs](https://tavily.ai/docs) to create the agent. 

The code is available on [github](https://github.com/learn-ai-101/code-langchain/commit/fe40dffdf1b867a94434556662ca17ef57d263dc). If I use the TavilyClient directly as a tool in my agent, it works fine. But if I use the TavilySearch tool, it truncates the query in a weird way and sends the result back. The LLM (gpt-oss) then goes into an infinite loop trying to get the correct information from the tool. The tool in turn gives back invalid responses which do not match the query and the whole cycle is repeated again.

So, lets look at the good case first. Using TavilyClient inside a search function that is designated as a tool (@tool decorator) in my code. This works fine. Below is the Langsmith trace for the tool.

[TavilyClientLangsmith trace](https://eu.smith.langchain.com/public/adcd4b4b-088f-4c73-b592-daf183c42593/r)

As can be seen, the LLM nicely uses the tool to get the relevant results. The tool is called 4 times by the LLM for the queries which unfortunately got profile links and unrelated posts. Now comes the interesting part. The TavilyClient went ahead and did a google search instead of linkedin only search and came up with 3 relevant results. You can check the output from the trace and view the result in a markdwon viewer. The salary/compensation part looks a bit weird as it lists the range in Euros but hey, we got some nice results.

And now we come to TavilySearch tool which is a part of langchain_tavily. Check the code in langChaintavily_search_agent.py. The search tool now adds 2 new parameters to the query which are "include_domains" and "search_depth". This creates a big issue for the LLM. Below is the Langsmith trace for the same.

[TavilySearchLangsmith trace](https://eu.smith.langchain.com/public/6c35516a-cdcb-4dd8-8583-3e300ae62838/r)

The search returns 3 profiles instead of 3 job postings that have been asked for in the query. LLM looks at the output and sees that it did not get the information it was looking for and hence retries the search again. And this keeps on happening forever! Basically I used up almost half of my free credits (500 of those) before I stopped the infinite loop. Now who is to blame: the LLM or the tool or both? I guess part of the problem lies with the langchain_tavily wrapper which added a couple of parameters to the query and never informed the LLM of the same. LLM quickly notices this and retries the search again and again.

So what is the moral of the story? Wrappers and hidden parameters/changes are not a good idea. I am pretty sure that the LLM would recognize the issue if the tool had provided the parameters used as a part of the result instead of just the query. The hidden params created a havoc for the LLM and since it was not getting the expected results, it kept on retrying.

Imagine if I had been using the paid cloud services instead of my local server. I would have wasted almost 290.2k tokens for nothing (yes, it utilized 290213 tokens). Another reason why one should use local servers for LLMs hosting and experimentation. Once the app is productised, token usage is optimized and comprehensive testing has happened, then it is a good idea to use paid cloud services. Until then, use local services for hosting LLMs and experimentation.

Happy LLMing!