---
title: "How to get Started with AI?"
date: 2025-11-20
categories: 
  - "general"
  - "AI"
tags: 
  - "LLMs"
  - "AIDE"
  - "Artificial"
  - "Intelligence"
---

AI has expanded into multiple territories. The pace of expansion has been exponential after 2022 when the first "free" LLMs were exposed to the general public for use. Suddenly overnight we have a variety of demography using AI for a variety of purposes. The chat interface offered by companies such as OpenAI, Google, ChatGPT, etc. provides for the most basic usage. People from all walks of life, all age groups and all professions use the chat interface to use the power of AI. Natural Language Processing (NLP) is a game changer in that context. I work in a multi-cultural environment with customers spread across the globe speaking different languages. Just about 5 years ago, a customer email in a local language had to be translated manually. And the quality of translation left a lot to be desired. Fast forward to today and language barriers seem almost non-existent! Most of the linked-in job postings now talk about practical AI usage experience rather than proficiency in certain language as a key skill. Language though comes as an added skillset. With the development of headsets that do on the fly translation, I guess it would be pushed further down in priority, all thanks to NLP and LLMs.

As an aside, just recently, my 10 year old asked me to read her a story that was created by ChatGPT based on the prompts given by her. And frankly, I was positively surprised at the quality of prompt given by her. She had almost a full page of text describing in detail the following:
1. Topic & description of the story - The details here were fantastic which allows the LLM to understand the context
2. Characters & relationship between those characters - These allows LLM to establish a bounded box needed to reduce hallucination and/or going off into a totally unrelated topic
3. Details on chapters - Her prompt was sophisticated in the sense that the story writing was "out-sourced" to the LLM but the progress of the story was still controlled by my daughter. She made sure that the LLM knows the chapters and what should be in each chapter. She also made sure that the LLM doesn't pick up some topic too early in progression and that the story does not loose its continuity.
4. Language to be used - In her prompt, she also mentioned the language and the complexity of the language to be used. She also mentioned that the story should be written in a way that it can be read by a child of her age sprinkling some advanced vocabulary and sentence formations to make the story very interesting.
5. Proof read the story - She also mentioned that the story should be proof read to make sure there are no grammatical errors and the story is free of any typos. This was something very interesting to me. I never thought of asking the LLM to proof read the story. I was always under the impression that LLMs output needs a Human-In-Loop to ensure the quality of output and proof reading was something that was done by a human.

But her prompt made me wonder as to how many people are good at prompting AI? An AI will generate an output based on the quality of prompt given to it. A high quality prompt will yield a better output. TO get the best out of AI, one needs to understand how to engage them in the best possible way to get the best results. I get a question lot of times from friends and family members as to how to use the AI properly. Because asking simple questions will give them the necessary answers. But when things get more complicated, they are not able to get the correct answers and they go on a totally incorrect path because of the hallucination aspect. Sometimes the replies from the LLMs are outright incorrect and easy to spot, at other times the replies are not incorrect but are not what was expected and can lead down a wrong path. Most visible aspect of a bad output is when the user is using models to generate images or videos. Try it yourself on DALL-E or Midjourney and you would see exception results. As an example, I wanted to generate a photorealistic image of a moon in the background and a unicorn flying in the foreground in dreamshaper hosted on my local machine. I used the following prompt: "Create a photorealistic image of a moon in the background and a unicorn flying in the foreground."

![Bad Image](https://live.staticflickr.com/65535/54935185427_debe21eb72_b.jpg)

As you can see, the output is not what I expected. I was expecting a photorealistic image of a moon in the background and a (single) unicorn flying in the foreground. The output is not photorealistic and the unicorn is not flying in the foreground. Also other artifacts like clouds, 2 moons, 2 unicorns, a princess with 3 legs and the front unicorn missing a leg were never expected. I know I chose a bad model to show an example but it pretty much remains the same. Now lets compare it with a good prompt as below.

Prompt: "extreme macro photograph of a ladybug on a green leaf covered in morning dew drops, shallow depth of field, soft natural lighting, intricate details, bokeh background, National Geographic quality"

![Good Image](https://live.staticflickr.com/65535/54935202882_c85b2469f5_b.jpg)

You can see the difference! It is the same model but with a better prompt. The output is photorealistic and the ladybug is in the foreground. The background is a bokeh background and the lighting is soft natural lighting. The image is also in National Geographic quality. Lets see if I can have a good prompt for the moon and the unicorn. Since unicorn is not a real animal, maybe the model doesn't understand how it might look for real. Lets try with a horse instead.

Prompt: "photograph of a single horse with 4 legs and a horn on the head in the night forest with a single photorealistic big moon in the background, wide angle shot, soft natural lighting, intricate details, bokeh background, National Geographic quality"

![A bit better?](https://live.staticflickr.com/65535/54936101386_dd3e29ac89_b.jpg)

We got a very different result with that prompt. The moment I use the word Unicorn, I would get a cartoon style image. So I changed the prompt to describe the a horse, brought it down to a real background. The creature is still a creep though and I either get 2 horns (like in the picture) or I get the proper horse but with a cartoon style horn on a disproportionate body. In any case, improving the prompt improved the image. Another aspect is that improving prompts is not an easy job. One needs to understand how the model works and behaves and how to control it to get the best results.

So hang on with me as I explore the techniques of using the proper prompts to get the best results from the LLMs. We will go together, experiment and learn from each other.

Happy Prompting!
