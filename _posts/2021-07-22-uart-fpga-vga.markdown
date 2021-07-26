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


# Development
The System is developed in three stages as described below:

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