---
layout: post
title:  "VGA Controller for an FPGA"
date:   2020-08-15 05:00:00 +0530
categories: jekyll update
---


&emsp; Implementation of a VGA Controler using Verilog for an FPGA with both graphics and text mode.




## VGA Contoller
&emsp; VGA stands for Video Graphics Array. A VGA Controller is the main component of Video Signal generator responsible for video signal production. It helps in generating timing of video signals such as horizontal and vertical synchronization signals and blanking interval signals. It may be completely integrated into computing system (video ram on the CPU’s memory map) or as a separate co-processor and can manipulate video RAM independently. It uses analog singal for displaying frames onto the display


### VGA Modes
&emsp; Many different Modes are possible ranging from Standard Text Mode through Standard Graphics Mode to High Definition Graphics Mode

#### VGA Standard Graphics Mode
&emsp; VGA Standard Graphics Mode differ by their Resolution, Pixel Clock, their timings, etc. For timing refer [VGA Timings](http://www.tinyvga.com/vga-timing) or [here](https://github.com/narendiran1996/vga_controller/blob/main/vga_timing_specs.csv).


#### VGA Standard Text Mode
&emsp; VGA Standard Text Moder differ by their resolution, Pixel Clock, thier timing and also the character size. The most command mode is the 640x480 - 60Hz with Character size of either 8x16 or 8x8 giving a character display of 80x30 or 80x60 respectively. Text Mode can either be in Monochrome or Color depending on the attribute field of the 16-bit character fields.

<img src="https://raw.githubusercontent.com/narendiran1996/vga_controller/main/DocsResources/textMode16bitStructure.png" alt="VGA 16-bit TEXT mode structure"/>


Note: Bit 15 may be fourth Background color depending on mode.


### VGA Signal Format and Interfacing
&emsp; VGA singal consit of 5 major signals (2 sync signals and 3 video signals).

| Signals | Name | Voltage | Description |
|---|---|---|---|
| HSYNC | Horizontal Synchronization | +5V(+3.3V) | Negative pulse denotes the start and of a new line that is makes electron beam restart at next screen’s scanline |
| VSYNC | Vertical Synchronization | +5V(+3.3V) | Negative pulse denotes the start and of frame that is makes electron beam restart at first screen’s scanline |
| R | Red Video Signal | 0 to +0.7V | Red color intensity for current pixel |
| G | Green Video Signal | 0 to +0.7V | Green color intensity for current pixel |
| B | Blue Video Signal | 0 to +0.7V | Blue color intensity for current pixel |


<img src="https://raw.githubusercontent.com/narendiran1996/vga_controller/main/DocsResources/vgaConnector.png" alt="VGA Connector">


- RGB pins of VGA interface should have analog signal voltage range of 0 to 0.7V depending on the pixel intensity.
- But FPGA has only digital pins of output voltages(0 and 3.3V), a R-2R Digital-to-Analog converter is being used at the output pins for the required RGB pins.
- The cirucit along with 75Ω termination resistance of VGA display to produce analog signal levels for Red, Blue and Green Video signals.
- Here, the FPGA uses 5 bits for Red and Blue channel and 6 bits for Green channel with a possible total color of 65,536 (25 ∗25 ∗26) colors.
- Here, an integrated DAC is used in the FPGA for solving this issue.

<p style="text-align:center">
<img src="https://raw.githubusercontent.com/narendiran1996/vga_controller/main/DocsResources/vgaCircuits.png" alt="VGA DAC Circuit">
</p>



### Terminologies

* **Horizontal Visible area** is the duration or the pixel clock count during which the pixels are drawn inside a horizontal line.
* **Horizontal Front Porch**, **Sync Pulse** and **Back porch** are the duration or the pixel clock count during which no drawing of pixels takes places. These timing delays are used for synchronization inside a horizontal Line.
* **Horizontal Whole Line** is the overall duration in a horizontal line or the overal pixel clock count in a horizontal line. It is the sum of **Visible area + Front Porch + Sync Pulse + Back porch**.
* Hence the **Vertical Refresh Rate** or **Line Rate** is the rate at which each horizontal line gets updated. It is nothing but the inverse of duration of Horizontal **Whole Line**.
* **Vertical Visible area** is the duration or the line count during which the horizontal lines are drawn vertically on a frame.
* **Vertical Front Porch**, **Sync Pulse** and **Back porch** are the duration or lines during which no drawing of pixels takes places. These timing delays are used for synchronization.
* **Vertical Whole Frame** is the overall duration of a frame or the duration it takes to draw all the horizontal lines in a frame. It is the sum of **Visible area + Front Porch + Sync Pulse + Back porch**.
* Hence the **Screen Refresh Rate** or **Frames per second** is the rate at which all the horizontal lines are drawn throughout the frame or rate at which entier frames gets updated. It is nothing but the inverse of duration of Vertical Whole Frame.

### Example Timing
&emsp; Let’s see the example of VGA Standard 640x480 @ 60Hz Industrial Standard.


**Horizontal Timing (Line)**

| Scanline part | Pixels | Time(μs) |
|---|---|---|
| Visible Area | 640 | 25.422 |
| Front Porch | 16 | 0.635 |
| Sync Pulse | 96 | 3.813 |
| Back Porch | 48 | 1.906 |
| **One Horizontal Line** | 800 | 31.777 |

**Vertical Timing (Frame)**

| Frame part | Lines | Time(ms) |
|---|---|---|
| Visible Area | 480 | 15.2532 |
| Front Porch | 10 | 0.3177 |
| Sync Pulse | 2 | 0.0635 |
| Back Porch | 33 | 1.0486 |
| **Whole Frame** | 525 | 16.6832 |

<p style="text-align:left">
<img src="https://raw.githubusercontent.com/narendiran1996/vga_controller/main/DocsResources/IMG_BasicTerminology_Timing640x480.png" alt="640x480 timing">
</p>


- The pixel clock is 25.175MHz making the duration of each pixel drawn to be 39.721 ns (1/25.175 MHz).
25.175MHz = 39.721ns.
- The pixels are drawn only during the visible area.
- A single horizontal line of 800 pixels (640 + 16 + 96 + 48) takes 800 ∗ (1/25.175 MHz) = 31.777 μs which is about 31.468 kHz making the vertical Refresh Rate.
- A complete frame is made of 800 pixels x 525 lines (480 + 10 + 2 + 33) it would take 800 ∗ 525 ∗ (1/25.175 MHz) = 16.68 ms which is about 60 Hz making the Screen Refresh Rate or the frames per second.

| Pixel Frequency | 25.175MHz |
| Vertical Refresh | 31.468 kHz |
| Screen Refresh Rate | 60 Hz (fps) |

