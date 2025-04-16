---
title: "Google CTF (Beginners Quest)!"
date: 2023-03-27
categories: 
  - "general"
---

I have been doing reverse engineering (RE) since my childhood days and that always helps freshen up my technical skills as well as understand the intrinsic working details of a particular piece of code and/or software. I have used tools such as IDA, x64dbg/Ollydbg, hiew, and more recently Ghidra. In the past I had also used SoftICE and quite a few other things. Those were the golden days when one can play around and I had all the time to learn stuff.

But these days, it is hard to find time to indulge into the RE scene. In the weekend, I was getting bored and didn't have anything to do. So just took a shot at Google CTF (https://capturetheflag.withgoogle.com/). It is a good resource to have fun and learn stuff. Click on the BeginnersQuest ((https://capturetheflag.withgoogle.com/beginners-quest)) and you would be presented with a (complex) map. There is a 1 on Side B top right corner. Click on it and you should be taken to the first challenge (https://cctv-web.2021.ctfcompetition.com/). The first challenge is to crack the password for getting access to those CCTV cameras!

The idea is to hack the password. If done properly, you should see 4 CCTV cameras and a CTF{<string>}. This is the string that you need to submit to finish the challenge. I will not paste the CTF string here so don't ask for it. But this first challenge is pretty easy to solve. Right-click on the page and view the source of the page. Look at the checkPassword() function in Javascript embedded in the HTML page.

The function is pretty easy to understand. There are a bunch of unicode characters compared for the password. It is a byte by byte comparison. And I have given the solution now. It is very easy to implement in Javascript and get the password.

If you are still confused, have a look at the solution here: https://onecompiler.com/javascript/3z3vj2v9n

BTW: Could have been solved with python, C and a host of other languages. I just chose JS as it was hosted and pretty easy to script in there.

Hope you all got started on Google CTF. I will hopefully find time for the next challenge and will put a write-up soon.
