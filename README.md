# UBC ELEC391 Laser Drawing Machine: PCB Design

<p align="center">
  <img src="https://github.com/jaydenguo832/ELEC391_2DOFLASER_PCB/assets/31781644/56ebe6e6-a0f5-4987-8362-cf99c41b7c2d" width="900">
</p>

<p align="center">
  Project Demo is shown at the end.
</p>

## Project Detail
The project is to build a machine that can rapidly draw with a laser to project geometric shapes. The system features a custom-designed PCB using Altium with useful features based on the user's needs determined through RCGs and the electrical demand from the different sub-systems (Digital Circuit, RT Controls, System ID). All the components are selected to satisfy the RCGs and soldered by hand.

<p align="center">
  <img src="https://github.com/jaydenguo832/ELEC391_2DOFLASER_PCB/assets/31781644/598a1ff2-2256-4187-83cb-036b023c169f" width="600">
</p>
<p align="center">
  Designed in Altium.
</p>

## PCB Key Features
1. Modular design
2. Integrated motor driver (L298N)
3. ESP32 Microcontroller
4. Dual Power Supply Solution for Power Jack and Battery
5. 5V and 12V Split Power Planes
6. Via Test Points

<p align="center">
  <img src="https://github.com/jaydenguo832/ELEC391_2DOFLASER_PCB/assets/31781644/4d83616e-36e0-4ccf-b9a9-dba3a79ef689" width="600">
</p>

## The RCGs:
The overall system RCGs are what set the design of the PCB and are an evaluation tool to assess the design.

### Requirements:
1. The circuit must be capable of DC motor bi-directional and speed control to reflect the laser with the mirrors in any orientation and speed.
2. The PCB must support two DC motors with encoders operating at 12V.
3. No temporary mounting methods for the PCB to mitigate board freeplay, and component damages, and provide a secure platform to function.

### Constraints:
1. The PCB must not exceed a 13cm x 13cm footprint to best fit within the casing design.
2. The system must not exceed a maximum of 12V VS and 2A from the power supply to protect components from excessive voltage and current damage. 
3. Component choices and PCB manufacturing costs must be within the $800 budget.

### Goals:
1. The PCB footprint should be as small as possible to reduce manufacturing costs.
2. Have a reliable 12V power source that can also be portable to be used in any location.
3. The system should be modular, and simple to interface such as plug-and-play connections, and provide test points for debugging.

## Components
### ESP32 MCU
The ESP32 is chosen for the MCU of the system due to its versatility and processing power. It can be powered by a 5V or 3.3V VSS and allows it to be easily integrated with the rest of the lower-voltage components of the system. It has 25 general-purpose I/O pins available to be configured to peripheral duties to meet Requirement 1 of having pin access to control the bi-directional and speed of the motors. The 11 pins will be assigned to the I/O duties of interfacing with the L298N motor driver, reading the decoder, controlling dual motor direction, laser control, and motor homing control.

<p align="center">
  <img src="https://github.com/jaydenguo832/ELEC391_2DOFLASER_PCB/assets/31781644/341f03b1-b7a8-49e0-9d27-7c812146a296" width="200">
</p>

### L298N Motor Driver
The L298N motor driver is chosen to satisfy Requirements 1, 2, and Constraint 2 for its integrated dual H-bridge, dual independent motor support, up to 2A per channel, and accessible inputs for speed and direction interface for the MCU. It can handle a supply voltage of up to 46V and a total DC current of up to 4A. In this project’s application, the L298N will be supplied with a maximum of 12V from the power source, 5V for the chip logic, and draws ~600mA for the 12V DC motors. 

<p align="center">
  <img src="https://github.com/jaydenguo832/ELEC391_2DOFLASER_PCB/assets/31781644/0403be56-feab-4331-974e-60b2a4245d5c" width="200">
</p>

### Portable and Stationary Power Supply
With reliability and portability in mind for Goal 2, the system is designed to run off of two 9V batteries for portability, or 12V from the barrel jack for a reliable wall plug power source. The power supply schematic and the breadboard prototype shows the design that allows for the integration of the barrel jack and batteries together in the same system. 

The principle of the barrel jack design has an insertion-detection pin that allows it to determine whether a power supply is inserted into the barrel jack, thus allowing the device to bypass the battery and run off external power. Additionally, the simple plug-and-play connection port of the barrel jack will satisfy the modularity of Goal 3 and allow the user to supply power to the system with ease. (https://learn.sparkfun.com/tutorials/connector-basics/power-connectors) 

<p align="center">
  <img src="https://github.com/jaydenguo832/ELEC391_2DOFLASER_PCB/assets/31781644/2c01e2d4-fb3b-4714-8af7-1258686ad827" width="200">
</p>

### 12V and 5V Regulation
To meet Constraint 2 of a maximum 12V power supply into the system, voltage regulators are needed to control the amount of voltage and current that runs through the system. The circuit contains the LM7812ACT 12V regulator and the L7805CV 5V regulator chosen for their low cost, and small footprint to satisfy Constraint 3 and Goal 1. 

<p align="center">
  <img src="https://github.com/jaydenguo832/ELEC391_2DOFLASER_PCB/assets/31781644/b5c77263-db0f-4864-bbe8-6d70e5ddd382" width="700">
</p>

The voltage regulators are connected in a cascade to step down the voltage output in two stages. The first stage is the 12V output for the DC motors and motor driver, and the second stage is the 5V output for the remaining lower voltage components such as the MCU, laser, and decoder IC. 100nF bypass capacitors are placed nearest to the input and output terminals of the regulators to prevent noise from entering the system by bypassing it to the ground. 

## PCB Design
### Layout
This is a 2-layered design for Vs and GND. The Vs layer is split into a 12V polygon and a 5V polygon for the high and low-level components that help to reduce routes, simplify the layout, and the overall footprint to 99.7mm x 123.19mm, satisfying Constraints 1 and 3 and meeting Goal 1. (Red: Top layer, Blue: Bottom layer)

<p align="center">
  <img src="https://github.com/jaydenguo832/ELEC391_2DOFLASER_PCB/assets/31781644/f4b4eb11-f235-4063-acd0-10521f71f315"  width="400">
  <img src="https://github.com/jaydenguo832/ELEC391_2DOFLASER_PCB/assets/31781644/10ff9e9f-375c-4cd7-8ca0-2a087b0e09ef" width="400">
  
</p>

<p align="center">
  <img src="https://github.com/jaydenguo832/ELEC391_2DOFLASER_PCB/assets/31781644/b3337917-0a71-4f93-9753-375ea6fd5dfb"  width="300">
</p>


### Interfacing
Components are arranged strategically to meet Goal 3 which aims for modularity and ease of interfacing for the user. All connection interfaces are grouped by category and placed on the edges for ease of accessibility. The power input terminal blocks are placed on the right edge, and the motor inputs and push buttons are placed on the left edge, allowing the user to easily interface the modular connection to configure the connections to meet Goal 3.

![02236](https://github.com/jaydenguo832/ELEC391_2DOFLASER_PCB/assets/31781644/ba25fb4d-5de0-4187-8d18-81875e7961fb)

## Schematic
![Screenshot 2024-04-30 214637](https://github.com/jaydenguo832/ELEC391_2DOFLASER_PCB/assets/31781644/ac2afd80-b05e-4018-aa13-c7777afcd9b6)


# Project Demo

https://github.com/jaydenguo832/ELEC391_2DOFLASER_PCB/assets/31781644/3c2735a0-2163-408a-a3d2-0086cca8f556

https://github.com/jaydenguo832/ELEC391_2DOFLASER_PCB/assets/31781644/7eb3b969-6d3f-4a60-a3ef-d48b0aa8dd46




















