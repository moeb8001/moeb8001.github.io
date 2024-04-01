---
title: "Talking to drones "
excerpt: "Voice command based flying of a nano-UAV. Focused on onboard Voice Command Recognition for Crazyflie.<br/>
![image](https://github.com/moeb8001/moeb8001.github.io/assets/112695184/99a9ecae-e9b7-4a9d-b96d-953cb4facb60)"
collection: portfolio
---


# Project: Enabling Voice Command for the Crazyflie Nano-UAV
(this is more of a place for dumping pics etc as of now)
Authors: Hanqiu Li Cai and Mohammad Ebrahimi  
Supervisor: Suryansh Sharma  
Project Duration: October 2023 - Present  
Cover: A Crazyflie drone. 

## Introduction

The CrazyAudio project aims to enable onboard voice control for the Crazyflie, an open-source nano-UAV widely used in robotics research. This initiative seeks to enhance human-quadcopter collaboration, potentially leading to innovative IoT applications for nano-UAVs and their swarms in real-life scenarios.

This document provides a preliminary progress report up to November 21, 2023, detailing methodologies, work done, technical challenges, and future work to be addressed.

## System Design

The Crazyflie nano-quadcopter's capabilities are expanded using external modules, despite its power and weight limitations. This project proposes a lightweight, power-efficient system capable of real-time audio processing for command-based flying using voice control. The chosen component for this task is the Seeed Studio XIAO ESP32S3 Sense, noted for its size, integrated digital microphone, and processing capacity.

## Noise Sampling and Characterization

### Approach

The methodology involves collecting noise data from the propellers at various thrust levels to analyze and characterize the noise spectrum. This data is crucial for developing a keyword spotting model that can effectively filter out propeller noise.

### Setup

The experimental setup includes attaching the ESP32 module to the drone's body, reflecting the final design's real scenarios.
![image](https://github.com/moeb8001/moeb8001.github.io/assets/112695184/70b17cd2-4887-49e5-83b1-90726f2a2777)
![image](https://github.com/moeb8001/moeb8001.github.io/assets/112695184/012b19ad-7c2d-4e51-8130-604860241501)



Additionally, a modified version of the Open Gimbal was used to facilitate and speed up the recording process.
![image](https://github.com/moeb8001/moeb8001.github.io/assets/112695184/b6f523ef-fc5f-4567-ba1a-c17184257e0e)


The set-up for the recording with the ESP board si shown below: 
![image](https://github.com/moeb8001/moeb8001.github.io/assets/112695184/7c90b489-db0f-421a-b8e6-b48d3305a043)



### Spectral Analysis

Initial spectral analysis confirms that propeller noise is harmonic and directly proportional to the RPM of the motor, aligning with expectations and existing literature.
![image](https://github.com/moeb8001/moeb8001.github.io/assets/112695184/777d5f97-9793-4641-b33e-05ba74606ca8)

### Pic dump
![image](https://github.com/moeb8001/moeb8001.github.io/assets/112695184/1da81e20-8f9f-44f4-a5ed-94f21c6fac37)


![image](https://github.com/moeb8001/moeb8001.github.io/assets/112695184/d18598f4-405c-4edd-a5d0-69c53979402e)


![image](https://github.com/moeb8001/moeb8001.github.io/assets/112695184/31fa257c-0fde-482d-a5d3-47b95ff596e3)


![image](https://github.com/moeb8001/moeb8001.github.io/assets/112695184/70300e8a-7e4e-4122-bc52-f0258ed4e310)


![image](https://github.com/moeb8001/moeb8001.github.io/assets/112695184/84bef0ba-d971-4d15-8d98-92308f6c66c6)

![image](https://github.com/moeb8001/moeb8001.github.io/assets/112695184/0c7794af-58ce-4857-9f5d-55acf35fd73b)


![image](https://github.com/moeb8001/moeb8001.github.io/assets/112695184/0c04cd20-ccee-4359-a39e-c330b5650f26)


diff heights: ![image](https://github.com/moeb8001/moeb8001.github.io/assets/112695184/482abc02-3cad-4b28-b843-494e572f3cb2)


## Interfacing and Onboard Processing

This section covers the physical interface between the XIAO ESP32S3 module and the Crazyflie, including the deployment of 

## References

- [1] Bitcraze AB. Crazyflie PWM to Thrust. URL: https://www.bitcraze.io/documentation/repository/crazyflie-firmware/master/functional-areas/pwm-to-thrust/ (visited on 11/21/2023).
- [2] Crazyflie 2.1 Datasheet. 114991551. Rev. 3. Bitcraze. 2020.
- ...

## CrazyAudio Source Code

```c
#define DEBUG_MODULE "CrazyAudio"

#include <stdint.h>
#include <string.h>
#include "FreeRTOS.h"
#include "task.h"
#include "system.h"
#include "config.h"
#include "debug.h"
#include "app.h"
#include "uart2.h"
#include "motors.h"
#include "param_logic.h"
#include "led.h"

void appMain() {
    systemWaitStart();
    uart2Init(19200);
    DEBUG_PRINT("UART2 initialized\n");
    ...
}
