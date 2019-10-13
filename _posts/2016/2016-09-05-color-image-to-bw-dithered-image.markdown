---
title: Color image to 1bit dithered image
layout: post
---

Hi all,

I'm trying to make myself more comfortable with blogging often. To do so, I wanted to publish a quick post about small project that I've done ~6 months ago. I'm basically revisiting the blog workflow while publishing this post :)

This is 'Floyd-Steinberg' dithering algorithm implementation in C++. Source code can be found at <https://github.com/kehribar/Dithering-OpenCV>

The algorithm is very useful if you have a black/white output capable only device (like thermal printers or monochrome displays) but want to have _some sort of_ detailed image.

### Results

![image](/img/dith_raw_image.png)

![image](/img/dith_dithered_image.png)

### References

See <https://en.wikipedia.org/wiki/Floyd%E2%80%93Steinberg_dithering> for additional details. 
