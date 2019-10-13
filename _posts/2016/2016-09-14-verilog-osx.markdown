---
title: OSX Based Minimal Verilog Simulation Toolchain
layout: post
---

Hi All,

I recently tried to make myself more comfortable to Verilog world with minimum **big** software tools. Then, I created a small solution for myself and put it on to GitHub. Below, you can find the Readme file that I prepared for the codebase.

You can check the repository from <https://github.com/kehribar/verilog-osx>

### About

One can say VHDL is second class citizen in open source software / hardware world. For example, [IceStrom](http://www.clifford.at/icestorm) project only supports Verilog. Furthermore, easy to use and FOSS simulators like [Icarus Verilog](http://iverilog.icarus.com/) and [Verilator](http://www.veripool.org/wiki/verilator) also (in stable sense) only support Verilog.

[Here](https://github.com/kehribar/verilog-osx) you can find a bare-bones, OSX based Verilog simulation toolchain that I created using several different tools. Everything should be working under Linux as well (expect [Scansion](http://www.logicpoet.com/scansion)) though I haven't tested yet.

### Description

There are four different Verilog source files:

* `up_counter.v`: 8bit unsigned up counter with clock, reset and enable inputs.
* `clken_gen.v`: Clock enable pulse generator module with clock and reset inputs. Division ratio is parameterised.
* `top.v`: Main top module that instantiates an up_counter and clken_gen module.
* `top_tb.v`: Testbench module that instantiates the top module and feeds the neccessary test signals to the module.

If you want to change the example structure, see the `Makefile` then:

* Change `SRCS` variable with new source file names ...
* Change `TESTBENCH` variable for another test bench file name ...

Also, if you want to change the resulting waveform file:

* Modify `$dumpfile("top_tb.vcd");` line in the testbench code.

### Commands

- Hit `make simulate` to simulate the codebase and run the testbench using Icarus Verilog.
	- Testbench's output stream ($display, $monitor function outputs and also any error/log messages) directed to $TESTBENCHNAME_log.txt file to make later analysis more convenient.
- Hit `make lint` to trigger linting using Verilator.
- Hit `make scansion` to open up the Scansion application with recently created signal file. Only works under OSX.
- Hit `make gtkwave` to open up the GTKWave application with recently created signal file. Not suggested for OSX.
- Hit `make clean` to delete any generated files.

### Prerequisites

* **Icarus Verilog**
	- Run `brew install icarus-verilog` to install on OSX system.

* **Verilator**
	- Even though verilator itself also supports simulation, I'm only using it to 'lint' the codebase for any syntax / logical errors.
	- Run `brew install verilator` to install on OSX system.

* **GTKWave**
	- This application can be used to investigate .vcd waveform files. It was not very stable under OSX, so I moved on to other tool. Under Linux, this probably runs better.
	- Run `brew install gtkwave` to install on OSX system.

* **Scansion**
	- This application is used to investigate .vcd waveform files. It is OSX only. It works much better (more stable) than gtkwave under OSX.
	- Visit <http://www.logicpoet.com/scansion/> webpage to download the application. Makefile assumes that you put the OSX executable under **/Applications/** folder. You can change it if you want.

* **Sublime Text**
	- Sublime Text doesn't support Verilog language as valid syntax extension. You should install <https://packagecontrol.io/packages/Verilog> package from package manager to have basic syntax coloring and couple of extra features for Verilog inside Sublime Text.
	- You can, of course, use any other text editor as well. :)

### Tips for analog waveform inspection

Scansion and GTKWave support visualising ports as analog waveforms. This feature is **very useful** in signal processing applications. Below you can see an example screenshot from *Scansion*:

![image](/img/analog_waveform.png)

Hit `⌘ + 2` to open `Trace Inspector` menu and select the desired signal. First, change the `Style` to **Analog** then adjust `Height Scaling` parameter to some high value to have bigger headroom in the display.

### References

You should check these short but dense documents about Verilog:

* "Summary of Synthesisable Verilog 2001"
	* <https://www.cl.cam.ac.uk/teaching/0910/ECAD+Arch/files/verilogcheatsheet.pdf>
* "Verilog Tips, Pitfalls to Avoid"
	*  <http://retroactive.be/verilog_tips.pdf>
