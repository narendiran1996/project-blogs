---
layout: post
title:  "UART VGA System"
date:   2021-07-22 05:00:00 +0530
categories: jekyll update
---

&emsp;A system for sending image from PC to FPGA through Serial UART and display on a Monitor using VGA. The connection setup used can be seen below:

<center>
    <img src="https://raw.githubusercontent.com/narendiran1996/uart-fpga-vga/main/TexFileCreated/BlockDiagram.png" alt ="Block Diagram"/>
</center>

## Components Used
1. FPGA (Zybo Zynq-7000)
2. USB-UART Converter (FTDI FT232)
3. VGA Cable


## Development
&emsp;The System is developed in three stages as described below:

<ol>
<li>UART LED System</li>
<ol type='a'>
<li>Recieve data from PC and display them on the LED in the FPGA</li>
<li>Send the led status back to the PC</li>
<li>Application in python to check the working</li>
</ol>

<li>UART BRAM System</li>
<ol type='a'>
<li>Recieve BRAM Depth from PC and store it in the FPGA</li>
<li>Send the BRAM Depth back to the PC</li>
<li>Store the data from PC to FPGA through Serial UART</li>
</ol>


<li>UART VGA System</li>
<ol type='a'>
<li>Recieve BRAM Depth from PC and store it in the FPGA</li>
<li>Send the BRAM Depth back to the PC</li>
<li>Store the data from PC to FPGA through Serial UART</li>
<li>Display the BRAM memory as image onto the monitor using VGA</li>
</ol>
</ol>

# UART LED System
&emsp; The first stage  is where a simple data is transmitted and received between PC and FPGA through UART. A system where the led values are sent to the FPGA through UART and the LED's glow according to the value. And, also the current led status can be returned back. The source can be seen in [UART LED System github page](https://github.com/narendiran1996/uart-fpga-vga/tree/main/VivadoProjects/UARTLedSystem).


The result's can be seen below:
<p>
<!-- <center> -->
<img src="https://raw.githubusercontent.com/narendiran1996/uart-fpga-vga/main/Outputs/LedOutput1.png" alt="LED Output 1" style="horizontal-align:left">
<img src="https://raw.githubusercontent.com/narendiran1996/uart-fpga-vga/main/Outputs/LedOutput_1_FPGA.jpg" alt="LED Output 1 FPGA" style="horizontal-align:right" width="50%">
<!-- </center> -->
</p>

<p>
<img src="https://raw.githubusercontent.com/narendiran1996/uart-fpga-vga/main/Outputs/LedOutput2.png" alt="LED Output 2" style="horizontal-align:left">
<img src="https://raw.githubusercontent.com/narendiran1996/uart-fpga-vga/main/Outputs/LedOutput_2_FPGA.jpg" alt="LED Output 2 FPGA" style="horizontal-align:right" width="50%">
</p>


# UART BRAM System
&emsp; In the next stage, number of data values are sent. A system where the BRAM's is filled with values sent from PC through UART. The depth of BRAM is also sent. The source can be seen in [UART BRAM System github page](https://github.com/narendiran1996/uart-fpga-vga/tree/main/VivadoProjects/UARTBramSystem/UARTBramSystem.srcs).

The result's can be seen below:
<p>
<img src="https://raw.githubusercontent.com/narendiran1996/uart-fpga-vga/main/Outputs/UARTBRAMOutput1_Code.png" alt="UART BRAM Output 1" style="horizontal-align:left">
<img src="https://raw.githubusercontent.com/narendiran1996/uart-fpga-vga/main/Outputs/UARTBRAMOutput1.png" alt="UART BRAM Output 1 FPGA" style="horizontal-align:right" width="50%">
</p>

<p>
<img src="https://raw.githubusercontent.com/narendiran1996/uart-fpga-vga/main/Outputs/UARTBRAMOutput2_Code.png" alt="UART BRAM Output 2" style="horizontal-align:left">
<img src="https://raw.githubusercontent.com/narendiran1996/uart-fpga-vga/main/Outputs/UARTBRAMOutput2.png" alt="UART BRAM Output 2 FPGA" style="horizontal-align:right" width="50%">
</p>


# UART VGA System
&emsp; The final stage is where the BRAM's memory is used by VGA to display the output.Same as BRAM System with the addition of VGA Controller to display the BRAM memory containing an Image. The source can be seen in [UART BRAM System github page](https://github.com/narendiran1996/uart-fpga-vga/tree/main/VivadoProjects/UARTVGASystem/UARTVGASystem.srcs).

The result's can be seen below:
<p>
<img src="https://github.com/narendiran1996/uart-fpga-vga/raw/main/Outputs/UARTVGAOutput1.jpg" alt="UART VGA Output 1" style="horizontal-align:left" width="40%" style="padding-right:30px">
<img src="https://github.com/narendiran1996/uart-fpga-vga/raw/main/Outputs/UARTVGAOutput2.jpg" alt="UART VGA Output 2 FPGA" style="horizontal-align:right" width="40%">
</p>

Shown Below is an a by which the image is read from BRAM:
<p>
<img src="https://media.giphy.com/media/vFKqnCdLPNOKc/giphy.gif" width="400" height="400" />
</p>