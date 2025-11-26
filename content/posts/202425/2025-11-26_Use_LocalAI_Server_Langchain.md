---
title: "Use LocalAI server with Langchain"
date: 2025-11-26
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
  - "OpenAI"
  - "LMStudio"
  - "Ollama"
  - "GPT4All"
  - "Huggingface"
  - "server"
---

Now you might have used gemini, chatgpt, deepseek, claude, etc. for your daily activities or asking a question here and there. And most of these services ask for a subscription to use their services. And if you are not tech sauvy, you might not be aware that it is very easy to run local AI servers on your local machine. No need to have a subscription or pay for cloud services. The best part is that your normal PC/Mac will work just fine. Of course depending on your HW, there will be limits on the type of models that can be used. But running an SLM (Small Language Model) or a smaller LLM (Large Language Model) is a piece of cake.

There are quite a few options available to run LLMs on your local machine. Some of the popular options are:
1. [LocalAI](https://localai.io/)
2. [LMStudio](https://lmstudio.ai/)
3. [Ollama](https://ollama.com/)
4. [GPT4All](https://gpt4all.io/)

There is a whole ecosystem of tools and services that allow you to run LLMs on your local machine. I have used the ones I listed above and they all work great. My personal favorite though is LMStudio. LMStudio provides access to a host of models including but not limited to DeepSeek, gpt-oss, seed-oss, qwen3, phi-4, gemma-3, llama, etc. Even huggingface models, Vision Language Models (VLMs), Code Language Models (CLMs) and Audio Language Models (ALMs) are available. LMStudio is available as a desktop app for Linux, Windows & Mac and comes out of box with a very good user interface. It also has command line interface for those who prefer to use it that way. The best part is that you can start/stop the local AI server by just a push of a button without going through any other complications. You can also decide on the model to interact with on the server using OpenAI compatible API endpoints. One can also load multiple models and switch between them but loading multiple models will demand higher resources. In any case, the UI provides a nice chat interface + ability to load/unload a model at runtime + an openAI compatible API endpoint for the server interaction. The best feature is that when one tries to download a model, depending on your HW and the model size, it will show if the model is compatible and will work with your HW or not. This is a pretty neat feature I would say.

Once you have got LMStudio setup to use it like a completely offline free service, we can move on to the most important part. And that is to use LangChain to interact with the local AI server. LangChain is a framework that allows you to interact with LLMs in a very easy way. It provides a lot of flexibility and allows you to use different LLMs in a very easy way. It also provides a lot of features like caching, streaming, etc. LangChain is available as a python package and can be installed using pip. It is also available as a docker image and can be run using docker. 

So setup your python environment and install langchain using pip. I would recommend using a virtual environment for this. You can use venv or conda for this. I would recommend using uv as it is much easier to manage and use and is incredibly fast. Once the necessary packages are installed, you can use the following code to interact with the local AI server.

```python
import os
from dotenv import load_dotenv
from langchain_core.prompts import PromptTemplate
from langchain_openai import ChatOpenAI


load_dotenv()

def main():
    print("Hello from code-langchain!")
    print(os.environ.get("OPENAI_API_KEY"))

    information = """
Elon Reeve Musk[b] (born June 28, 1971) is a businessman and entrepreneur known for his leadership of Tesla, SpaceX, Twitter, and xAI. Musk has been the wealthiest person in the world since 2021; as of October 2025, Forbes estimates his net worth to be around $500 billion.

Born into a wealthy family in Pretoria, South Africa, Musk emigrated in 1989 to Canada; his Canadian citizenship is congenital, his mother having been born there. He received bachelor's degrees in 1997 from the University of Pennsylvania in Philadelphia, United States, before moving to California to pursue business ventures. In 1995, Musk co-founded the software company Zip2. Following its sale in 1999, he co-founded X.com, an online payment company that later merged to form PayPal, which was acquired by eBay in 2002. That year, Musk also became an American citizen.

In 2002, Musk founded the space technology company SpaceX, becoming its CEO and chief engineer; the company has since led innovations in reusable rockets and commercial spaceflight. Musk joined the automaker Tesla as an early investor in 2004 and became its CEO and product architect in 2008; it has since become a leader in electric vehicles. In 2015, he co-founded OpenAI to advance artificial intelligence (AI) research, but later left; growing discontent with the organization's direction and their leadership in the AI boom in the 2020s led him to establish xAI. In 2022, he acquired the social network Twitter, implementing significant changes, and rebranding it as X in 2023. His other businesses include the neurotechnology company Neuralink, which he co-founded in 2016, and the tunneling company the Boring Company, which he founded in 2017. In November 2025, a Tesla pay package worth $1 trillion for Musk was approved, which he is to receive over 10 years if he meets specific goals.

Musk was the largest donor in the 2024 U.S. presidential election, where he supported Donald Trump. After Trump was inaugurated as president in early 2025, Musk served as Senior Advisor to the President and as the de facto head of DOGE. After a public feud with Trump, Musk left the Trump administration and returned to managing his companies.

Musk is a supporter of global far-right figures, causes, and political parties. His political activities, views, and statements have made him a polarizing figure. Musk has been criticized for COVID-19 misinformation, promoting conspiracy theories, and affirming antisemitic, racist, and transphobic comments. His acquisition of Twitter was controversial due to a subsequent increase in hate speech and the spread of misinformation on the service. His role in the second Trump administration attracted considerable public backlash, particularly in response to DOGE.
    """

    summary_template = """
given the information {information}, about a person, I want you to create:
1. A short summary
2. two interesting facts about them
    """

    summary_prompt_template = PromptTemplate(input_variables=["information"], template=summary_template)
    llm = ChatOpenAI(openai_api_base=os.environ.get("OPENAI_API_BASE"),openai_api_key=os.environ.get("OPENAI_API_KEY"),
                     model_name="openai/gpt-oss-20b", temperature=0)
    chain = summary_prompt_template | llm
    response = chain.invoke(input={"information": information})
    print(response.content)


if __name__ == "__main__":
    main()
```

Keep an eye on the invocation of the ChatOpenAI() call where the OPENAI_API_BASE and OPENAI_API_KEY are explicitly passed. The variables are defined in the .env file as below:

```bash
OPENAI_API_KEY="openai/gpt-oss-20b"
OPENAI_API_BASE="http://127.0.0.1:1234/v1"
OPENAI_API_VERSION="v1"
# MODEL_API_IDENTIFIER = openai/gpt-oss-20b

```

The OPENAI_API_KEY is the same as the model identifier in the LMStudio UI for the server tab. When the server is started in LMStudio, it starts a local server at http://127.0.0.1:1234/v1. You can also access the server from outside by using tailscale for instance. But that is a topic for another post.

A sample run of the above code gives the below output:

```bash
3:10:12 (code-langchain) code_langChain ±|master ✗|→ python main.py 
Hello from code-langchain!
openai/gpt-oss-20b
**Short Summary**

Elon Reeve Musk (born June 28 1971) is a South‑African‑born entrepreneur who has built a global portfolio of high‑profile tech companies—Tesla, SpaceX, Twitter/X, xAI, Neuralink, and the Boring Company. A serial founder and CEO, he became the world’s richest person in 2021, with Forbes estimating his net worth at roughly $500 billion as of October 2025. Musk has also been deeply involved in politics: he was the largest donor in the 2024 U.S. presidential election (supporting Donald Trump), briefly served as a senior advisor to the Trump administration, and has been a vocal supporter of far‑right causes—an activity that has drawn widespread criticism for promoting misinformation and hateful rhetoric.

**Two Interesting Facts**

1. **$1 Trillion Pay Package:** In November 2025, Tesla approved an unprecedented compensation plan worth $1 trillion, payable over ten years if Musk meets specific performance targets. This is the largest single‑company pay package ever authorized in corporate history.

2. **Dual Citizenship from Birth:** Musk holds both South African and Canadian citizenship by birth—his mother was born in Canada—before later acquiring U.S. citizenship in 2002. This tri‑national status has enabled him to navigate regulatory environments across three major economies while running his multinational ventures.

```

The code is available on my github repo [code-langchain](https://github.com/learn-ai-101/code-langchain/commit/46de40a20e873eaf49ca2c0e712d6176fd21ae2d).

Do post your comments and experience with localAI server and langchain.