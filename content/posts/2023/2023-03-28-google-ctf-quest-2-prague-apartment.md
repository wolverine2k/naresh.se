---
title: "Google CTF - Quest 2 (Prague Apartment)"
date: 2023-03-28
categories: 
  - "general"
---

Quest 2 is even easier than Quest 1 (if you have studied logic gates). Basically, the idea is to go through the circuit given and arrive at the code which will provide for a 1 on the final output. The combination of gates that are TRUE needs to be mentioned in CTF{<answer>}. The rest of the gates can be ignored.

There is a very simple way to solve it. We do a reverse traversal from the final gate to the input gates. The idea is to basically have the final value as true and then look at the gates input. Determine the input values so that the final value is true. Do the reverse traversal in an iterative fashion until one reaches the inputs defined.

Another option is to draw the circuit in a logic gate simulator like logic.ly and then toggle the switches to get the final output (true) on the end gate. This is brute force method but again can be cracked quite easily. I suggest doing the reverse traversal first before doing the brute force method. The logic diagram looks like below:

> [
> 
> View this post on Instagram
> 
> ](https://www.instagram.com/p/CqU7-GCrajV/?utm_source=ig_embed&utm_campaign=loading)
> 
> [A post shared by Naresh Mehta (@wolverine2k)](https://www.instagram.com/p/CqU7-GCrajV/?utm_source=ig_embed&utm_campaign=loading)

<script async src="//www.instagram.com/embed.js"></script>

I have deliberately turned off some switches so as to hide the real answer. But there you are, it should be very easy to solve. Do write in your comments if you have done it or not. Next would be the 3rd one if I get some time this week. Keep the fun rolling in :).
