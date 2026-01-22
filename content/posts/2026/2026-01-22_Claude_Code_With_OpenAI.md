---
title: "Use Claude Code with OpenAI compatible APIs"
date: 2026-01-22
categories: 
  - "general"
  - "AI"
tags: 
  - "LLMs"
  - "AIDE"
  - "Artificial"
  - "Intelligence"
  - "LocalAI"
  - "Claude"
  - "Code"
  - "OpenAI"
  - "cli"
  - "agent"
  - "ccr"
  - "router"
  - "claude2openai"
---

Happy New Year and welcome 2026. This is my first article of the year and I have embarked on a very interesting journey. And I am excited to share it with you. Keep reading.

[Claude code](https://claude.com/product/claude-code) is an AI coding tool operating within a terminal. It allows users to write, debug and manage code and/or AI tasks more efficiently, without going through an IDE. This typically enhances the AI interaction experience and is also quite light-weight. It also has a [in-built "Agentic Loop"](https://code.claude.com/docs/en/how-claude-code-works) where the 3 phases (contextualization, action and verification) happens in a loop to provide for the most optimum output without detailed repetitive prompting. It also supports MCP, subagents, hooks, plugins and what have you.

This is great BUT (yes, you know this was coming), one needs to shell out "mollahs" for the Claude Code subscription plans. Even after shelling out the dollars, the usage limits are applicable and there are extra charges if you are simply playing with it (or exploring/researching as I call it). Also what about all the locally hosted llms that I have been talking about in my previous articles.

It doesn't make sense to throw away all that local hosting, privacy, infrastructure setups, SW, model usage, etc. to just use an agentic tool; which by the way is amazingly cool and is a necessity. So people would generally say that use ollama-code (now with anthropic end-point support), LMStudio, AnythingLLM, etc. as they are "NOW" supporting anthropic end-points. Yes, you can do that for sure. But what if you have access to a hosted solution like Nvidia NIM (and yes, Nvidia does provide free hosted opensource NIM model access), but the server only supports OpenAI endpoints? And I am stubborn enough to use Claude Code instead of switching to something else like Aider, openwork, etc. I am also memerized by the [Auto-Claude](https://github.com/AndyMik90/Auto-Claude) multi-agent coding framework. More on Auto-Claude in my next article though.

So, given the limitations, there are 3 options for a person to use Claude Code.
1. Pay up to Anthropic to use their models and Claude Code (Cons: Costs/spending our hard-earned money)
2. Move to local hosting (as described in [previous article](https://naresh.se/en/posts/202425/2025-11-26_use_localai_server_langchain/)) that supports anthropic API endpoints (Cons: Hosted services like Nvidia NIM cannot be used. Also if you code, you will need to incorporate a switch which either talks to OpenAI endpoint or anthropic endpoint; which I would like to avoid). Also OpenAI endpoints are the most widely used endpoints across multiple providers so I don't want to deviate there.
3. Use an on the fly translator which intercepts the anthropic requests, converts it to OpenAI requests, gets the response from the OpenAI endpoint and converts the response back to anthropic response that will then be used by Claude Code

There is ofcourse a fourth option to not use it and move to other CLIs instead but hey, I am stubborn. So I select option 3. If you go the intercepter route, there are again 2 options (thanks opensource).
1. [Claude-Code-Router (ccr)](https://github.com/musistudio/claude-code-router) - CCR which does model routing.
- This one though does not support model mapping i.e. a configuration that allows for mapping of Claude models like Opus, Sonnet, Haiku, etc. to a customizable model.
- It has some additional options for adding [custom transformers](https://musistudio.github.io/claude-code-router/docs/server/config/transformers) to convert requests and responses between different formats, handle authentication, etc.
- It is very flexible but at the same time, comes with additional complexity. The [documentation](https://musistudio.github.io/claude-code-router/docs/category/cli) does a great job to explain the details.

I had some tough time to get ccr to work though because:
- Multitude of configuration options making it very complex
- No debug messages if anything goes weird (I guess there are options but I didn't delve deeper)
- A bit frustrating because of nodejs dependencies and runtime

Anyways, below is the config that helped me with the routing. Make sure to edit ~/claude-code-router/config.json to get something up and running.

````
{
  "LOG": true,
  "LOG_LEVEL": "debug",
  "CLAUDE_PATH": "/Users/nmehta/.local/bin/claude",
  "HOST": "127.0.0.1",
  "PORT": 8080,
  "APIKEY": "",
  "API_TIMEOUT_MS": "600000",
  "PROXY_URL": "",
  "transformers": [],
  "Providers": [
    {
      "name": "<name>",
      "api_base_url": "<server_URL>/chat/completions",
      "api_key": "<your_api_key>",
      "models": [
        "meta/llama-3.3-70b-instruct"
      ],
      "transformer": {
        "use": []
      }
    }
  ],
  "StatusLine": {
    "enabled": false,
    "currentStyle": "default",
    "default": {
      "modules": []
    },
    "powerline": {
      "modules": []
    }
  },
  "Router": {
    "default": "<name>,meta/llama-3.3-70b-instruct",
    "background": "<name>,meta/llama-3.3-70b-instruct",
    "think": "<name>,meta/llama-3.3-70b-instruct",
    "longContext": "<name>,meta/llama-3.3-70b-instruct",
    "longContextThreshold": 60000,
    "webSearch": "<name>,meta/llama-3.3-70b-instruct",
    "image": ""
  },
  "CUSTOM_ROUTER_PATH": ""
}
````

There can be multiple models listed. Also make sure that the router is prefixed by <name> of the provider followed by a , and the <model_name>. The api_base_url also needs /chat/completions suffixed. eg: Just providing http://localhost:1234/v1 will not work (as it does it VS extensions for instance, minor trouble but you need to know).

Restart the ccr server for the configuration to take effect. There is also a ccr ui command which allows to do visual settings. I suggest to use it after the actual settings.json has been edited.

Now for the most important part. Modify your claude settings (~/.claude/settings.json) to the following otherwise claude code will not work properly.

````
{
  "env": {
    "ANTHROPIC_API_KEY": "non-empty-string",
    "ANTHROPIC_BASE_URL": "http://127.0.0.1:8080/v1",
    "CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC": "1",
    "CLAUDE_CODE_ENABLE_TELEMETRY": "0"
  },
  "autoUpdatesChannel": "latest",
  "api_base_url": "http://127.0.0.1:8080/v1",
  "api_key": "any-non-empty-string",
  "apiBaseUrl": "http://127.0.0.1:8080/v1",
  "apiKey": "any-non-empty-string"
}
````

Adjust the port number if you have changed it to a different one. Once this is done, type in ccr code on the command line and the bypass will be active. I am sad to say though that sometimes it works but most of the times, either you get:
- API Error: 404 Route POST:/v1/v1/messages?beta=true not found
This is the route to Anthropic API endpoint. Not sure why that happens
- Input Validation WebSearch failed due to the following issues:
     The parameter `allowed_domains` type is expected as `array` but provided as `null`
     The parameter `blocked_domains` type is expected as `array` but provided as `null`

Also, if you just launch claude (instead of ccr code), the Claude Code "fails" to access the router. This would not be a big problem if you are just sticking to Claude Code but then you will loose out on the amazing Auto-Claude, Claude Cowork, etc. And man, I have become a fan of Auto-Claude. So the intercepter needs to be intercept any and all claude requests even if it is not started by ccr.

And here comes the 2nd contender! [Claude2OpenAI](https://github.com/wolverine2k/claude2openai) is a python server that runs silently in the background. It has only 1 job which is to intercept the Claude requests, convert it to OpenAI, send it to the OpenAI (compatible) endpoint, receive the response and convert it back to anthropic response. And this server works with any Claude (Claude CLI, Auto-Claude, etc) with minimal configuration and model mapping (instead of the static mapping in ccr). I am proud to say that I created this server yesterday (21st Jan 2026). I will do some code clean-up, generate documentation and open source the server under Apache license in a couple of days. And I am proud to say that the claude2openai server just works and is faster than ccr.

My next article will bring in the details of the claude2openai server and explain its usage. By that time, I will have open sourced the code on my github. Be on a lookout.

Happy Clauding!