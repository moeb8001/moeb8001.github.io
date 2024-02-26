---
title: "Talking to drones "
excerpt: "Voice command based flying of a nano-UAV. Focused on onboard Voice Command Recognition for Crazyflie.<br/>
![image](https://github.com/moeb8001/moeb8001.github.io/assets/112695184/99a9ecae-e9b7-4a9d-b96d-953cb4facb60)"
collection: portfolio
---
# CrazyAudio Project: Enabling Voice Command for the Crazyflie Nano-UAV

Authors: Hanqiu Li Cai and Mohammad Ebrahimi  
Supervisor: Suryansh Sharma  
Project Duration: October 2023 - Present  
Cover: A Crazyflie drone. Photo from SNSF Scientific Image Competition

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

## Interfacing and Onboard Processing

This section covers the physical interface between the XIAO ESP32S3 module and the Crazyflie, including the deployment of an Edge Impulse keyword detection model and the communication framework established for autonomous operation.

### Hardware

Details the pin schematics and the UART serial communication setup between the ESP32 module and the Crazyflie, facilitating command transmission for drone actions.

### Software

Describes the custom application developed for the Crazyflie, allowing for onboard control without external devices. The application initiates UART serial communication and performs actions based on received commands.

### Initial Prototype

Presents the current prototype capable of detecting basic keywords and executing commands under conditions of ambient noise.

## Next Steps

Outlines future directions, including noise filtering improvements, keyword sample collection for a robust detection model, hardware adjustments for power supply issues, and the potential expansion of voice commands to drone swarms.

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
