---
layout: post
title: "Adjustable DC voltage/current source"
date: "2015-05-21 21:31"
category: build
---

Hi all,

I've recently built an adjustable voltage and current source to test various hardware I build. Normally I was using a potentiometer to generate an adjustable voltage when I need but having a dedicated tool for the job seemed better.

![image](/img/dc_source3.jpg)

I build this device by utilising a microcontroller, D/A converter, an op-amp + NPN transistor for constant current source and finally two optocouplers for serial communication.

![image](/img/ltc1448.jpg)
*R3: 1k*

For the D/A converter, I used LTC1448 12bit DAC. It is relatively expensive for such a build but I had this IC as a sample for couple of years; therefore price wasn't an issue. Moreover, since the battery voltage will vary with the milage and you can't know the voltage value precisely I used an LM4040 zener reference to generate 2048 mV to the DAC. Therefore 1 LSB of the DAC output will correspond to 0.5 mV.

![image](/img/constantCurrent.jpg)

DAC has two channels and I used the second channel as *constant current source*. R1 is just there to limit the base current of the NPN transistor. Constant current is calculated as `set_voltage/R2`. I used 100 ohms for R1, and (10kohm fixed // 100kohm trimpot) as an R2. Trimpot is used to fine tune the output current. For op-amp I used a LTC1152 which can work down to 2.7 volts but it is not the greatest low-power op-amp with 3mA supply current. However, the op-amp is choper stabilised therefore it has very little *low frequency noise* which is useful for such application.

![image](/img/dc_source1.jpg)

I used Attiny85 for microcontroller. Nothing specific about it, you can find the [firmware here](https://github.com/kehribar/adjustable-dc-reference). I used Elm-Chan's software serial library for basic I/O functionallity. I can set the voltage values over opto-isolated 9600 baud serial link and store them inside the microcontroller's EEPROM.

![image](/img/optoisolator.jpg)
*R1: 4.7kohm  R2: 470ohm   R3: 470ohm   R4: 4.7kohm*

When power-up, microcontroller sets initial values to DAC, therefore I don't need to configure the system each time I use. Also since I used optocouplers for isolation, I needed to invert TX & RX signals inside the firmware.

In conclusion,

System is not *that* accurate due to various reasons *(small inaccuracy of the voltage reference, DC offset of the DAC and etc.)* but it is highly stable. When I want to set the voltage channel to 250mV, I get around 250.45 mV of stable voltage out of it, which is enough for my needs.

![image](/img/dc_source2.jpg)

Also for a **much better** adjustable voltage reference build, you can check [Linear Technology App note 86](http://cds.linear.com/docs/en/application-note/an86f.pdf) called [*A Standards Lab Grade 20-Bit DAC with 0.1ppm/°C Drift*](http://cds.linear.com/docs/en/application-note/an86f.pdf)

ihsan.
