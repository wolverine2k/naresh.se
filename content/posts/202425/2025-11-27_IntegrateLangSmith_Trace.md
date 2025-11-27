---
title: "Integrate LangSmith with Langchain"
date: 2025-11-27
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
  - "LangSmith"
  - "OpenAI"
  - "LMStudio"
  - "Ollama"
  - "GPT4All"
  - "Huggingface"
  - "server"
---

LangSmith is a platform that allows you to track and analyze the performance of your LLMs. It provides a lot of features like tracing, debugging, etc. LangSmith is available as a python package and can be installed using pip and also as a docker image. But the best way to start using LangSmith is pretty simple.

If you have followed my previous article on [Use LocalAI server with Langchain](https://naresh.se/en/posts/202425/2025-11-26_use_localai_server_langchain/), you should have a localAI server running and a langchain setup to interact with it. You can download the example code that I have pasted in the previous article and run it to interact with the localAI server.

So now is the time to understand how our LLM is performing, how many tokens is it consuming, etc. It allows for tracing and debugging of your langchain application. The best part is that it is amazingly simple to setup. All you need to do is go to [LangSmith](https://smith.langchain.com/) and create an account. Login and create a new tracing project. Follow the instructions on the website to setup the tracing project. Generate an API key and add it to your environment variables. Add the other variables like project, tracing, etc. to your environment variables. Use your .env file to add the variables as shown below.

```bash
LANGSMITH_TRACING=true
LANGSMITH_ENDPOINT=https://eu.api.smith.langchain.com # Replace with your endpoint shown during project creation
LANGSMITH_TRACING=true
LANGSMITH_API_KEY=xxxxxxxxxxx # Replace with your API key
LANGSMITH_PROJECT=xxxxxxxxxxx # Replace with your project name
```

And voila! You are all set to use LangSmith with Langchain. Nothing else to do to start using LangSmith to trace your LLM calls! Yes, it is that simple. Simply run your code and it will start tracing your LLM calls. You can then view the traces in the LangSmith UI. You can also view the traces in the LangSmith UI and analyze the performance of your LLMs.

Checkout how my first run looks like in the LangSmith UI.

![LangSmith Tracing Project Page](https://live.staticflickr.com/65535/54950034980_91a53daa3c_b.jpg)

Click on the project to see more details. It shows the start time, stop time, status (success/fail) of the call, total number of tokens used, latency, etc. It also shows the input and output of the call. Checkout the image below.

![LangSmith Tracing Details Page](https://live.staticflickr.com/65535/54949739946_5d4f39fbf4_b.jpg)

Check the metadata tab while you are at it. Change to a different model and see how it affects the latency and the number of tokens used. The IO can also be compared using different models. Use a model with model parameters in millions instead of the 20 billion parameter model that I am using and see the difference. This is an amazing tool to optimize your LLM calls and LLM Usage. If you have not checked it out, look at my [LLM comparison article](https://naresh.se/en/posts/202425/2025-08-28_llm_parameters/) to see how different models perform and what they are good for, their training data size, training data sources, context size, strengths & weaknesses, etc. That should help you with an idea on what model to use for what purposes. Sometimes the current model you are using is not the best for the job that you are throwing at it.

Do post your comments and experience with LangSmith tracing and see if you can achieve better results. Please do share it with me and our readers.

Happy LLMing!