---
title: "Google CTF – Quest 3 (High-Speed Chase)"
date: 2023-05-04
categories: 
  - "general"
---

This is the first quest where you are told to write code in JavaScript. It is a very easy challenge to clear and tests the basics of conditional statements. The problem is that after breaking away from the [Prague Apartment (Quest 2)](https://www.naresh.se/2023/03/28/google-ctf-quest-2-prague-apartment/), you are being followed by adversaries. Luckily you get your hands on a self-driving car and you can break-in into the self-driving module and write your own code to get it to move faster than the pursuers. You are also helped by data points which are collected from satellites and sent to you for use. You can use JavaScript to write the code and get away from the pursuers.

So the background story is good but the main question is are you really going to write a self-driving module code? No, you are not. Basically, you are going to code a small function that is called multiple times per second, and depending on the value returned from the function, your car will either move 1 unit left, keep going straight or 1 unit to the right. So your function returns an integer, -1 meaning move 1 unit left, 0 meaning keep going straight, and 1 meaning move 1 unit right. The array of 17 data points is passed as input to the function. The more value of a particular data point, the more is the distance of an obstacle from that data point.

So basically your data will look like something below.

arr\[0\] = 10, arr\[1\] = 11..... arr\[16\]=3

The values at a particular point indicate the distance from the obstacle up ahead. There is also a picture IIRC to show how the data points might plot out. More information is in the quest of course. The real question is how will you interpret this data and move the car around so you don't hit any obstacles and go ahead safely.

Your algorithm needs to make sure that the center point of the car is always pointing to the longest distance possible in the array values. Since there are 17 markers, if the center point of the car is the longest at the center, keep going straight, if it is less than half (i.e. 8) go left otherwise go right. Pretty easy right? This is a typically find min/max in an array problem.

So basically we keep tracking a center point to the maximum value of the array and note down the index. If the index is less than 8, go left, if 8, go straight, and if more than 8, go right. This simple logic works because the function is called multiple times in a second (i.e. at a higher frequency). If it would only be called once per move, the logic will fail and we will need more advanced techniques but for this quest, the simple algo suffices.

Below is the code for the same. As usual, I will not provide direct answers. I have some deliberate easy errors in the code which you can fix to get through this module.

```
    var maxDist = scanArray[0];
    var center = 0;
    for (let i = 1; i <= 16; i++) {
        if (scanArray[i] >= maxDist) {
            maxDist = scanArray[i];
        }
            center = i - 1;
    }

    if (center == 8) {
        return 0;
    } else if (center < 8) {
        return 0;
    } else {
        return 0;
    }
```

Enjoy and don't forget to leave your comments below. See you for the next quest.
