---
layout: post
title: "Sensitive 'Loudness Detector'"
date: "2015-08-18 21:33"
---

Hi all,

I recently needed to build a sensitive 'loudness detector' for environment sound level sensing based project. I had the microphone part covered with my previous project [<http://kehribar.me/hardware/electretAmplifier/>] but level sensing part is left to do. I could use microcontroller to do the work in software but I wanted to have a relatively low power solution. Eventually, I had to build a single supply envelope detector.

![image](/img/loudness_detector_1.jpg)

Actually, that electret amplifier board itself have onboard diode + RC filter based passive envelope detector which can be used for level sensing purposes.

![image](/img/passive_envelope.png)

 On the other hand, it doesn't work good with low sound levels since the diode has ~0.6V drop. Standard solution is to use an op-amp as a *super diode* which all the examples on the web works quite OK if you have bipolar power supply rail. I wanted to have a single supply *precision rectifier* but couldn't find too much information on the web, therefore I'm sharing the solution that I've come up with.

![image](/img/loudness_detector_4.jpg)

Output of the electret amplifier board sit around ~1V generated from [mic bias voltage / 2]. Initially I set the DC level of the input signal to VREF via R1 and C1. The two basically creates a high pass filter. Values are R1: 47k, C1: 0.1uF After the signal properly biased to the half supply, it is applied to the *precision rectifier*. I used regular 1N4148 for D1. Only difference from the existing solution is that R2 and C2 is going to VREF line instead of GND. R2 and C2 decides the *responsiveness* of the level detection. I used C2: 47uF and R2: ~100k to get a slow and steady response. One can play with the values of R2 and C2 to get much faster attack time.

I used half of MCP6002 to do the rectification and other half for generating VREF = VCC/2 voltage. I used R3,R4: 47k and C3: 10uF.

Overall circuit consumes around ~0.8 mA of current with the electret amplifier board as well. It can be considered as low power for a particular application. You can see the board in action from the video below.

<iframe src="https://player.vimeo.com/video/136641666" width="740" height="420" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
*video*

I build the board on a perfboard which you can see the details below.

![image](/img/loudness_detector_3.jpg)

ihsan.
