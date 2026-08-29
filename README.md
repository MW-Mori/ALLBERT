# ALLBERT
A custom autonomous mobile robot built from the ground up using python, a BeagleBone Black and a Raspberry Pi, with layered hardware control, decision logic and safety systems.

## Project Overview

ALLBERT began from my interest in programming and the idea that software can bring a physical machine to life. I wanted to take the logic I was used to creating in code and apply it to something physical-a robot that could sense its environment, make decisions and act on those through movement.

The goal for ALLBERT is to explore how software and hardware work together in a complete robotic system. Rather than relying on a prebuilt robotics framework, I am developing the control system myself, from direct motor and sensor interaction to decision-making and autonomous behavior.

## Project Goals

The primary goal of ALLBERT is to operate autonomously by navigating its environment, detecting obstacles, and making decisions about how to move around them without requiring constant human control.

To accomplish this, ALLBERT is being developed to:

- Sense obstacles from multiple directions using onboard sensors.
- Interpret sensor information and make movement decisions based on the robot's current surroundings.
- Translate those decisions into controlled physical movement through the motor-control system.
- Respond safely to sensor failures and other conditions where movement may be unsafe.
- Maintain a clear separation between hardware control, decision-making and autonomous behavior through layered software architecture.
- Use a control system developed from the ground up rather than relying on a prebuilt robotics framework such as ROS.

## System Architecture

ALLBERT uses a layered architecture that separates high-level autonomous behavior, mid-level decision logic, and low-level hardware control. This separation allows each layer to have a clearly defined responsibility while still working together as a complete robotic system.

The software architecture is divided into three primary layers:

- **High-level Autonomous Layer:** Coordinates ALLBERT's overall autonomous behavior and determines what the robot should attempt to do.
- -**Mid-Level Logic Layer:** Interprets sensor states and applies decision-making logic to determine appropriate actions, such as advancing, turning or escaping from a blocked path.
- **Low-Level Hardware Logic:** This layer interfaces directly with the physical hardware, translating movement commands into GPIO and PWM signals used to control the motors.

###Computing Architecture

ALLBERT uses both a Beaglebone Black and a Raspberry Pi 3B+, with each computer assigned a different role within the system. The BeagleBone Black serves as the primary hardware-control, handling direct interaction with the robot's motors and sensors through GPIO and PWM capabilities. The Raspberry Pi 3B+ serves as the higher-level interface computer, providing the foundation for ALLBERT's web dashboard and communication with the hardware-control system.

##Hardware

ALLBERT's hardware was selected and assembled with an emphasis on reliable control, modularity, safety, and the ability to troubleshoot or modify individual parts of the system. Many of the hardware evolved as the robot was built and tested with each decision addressing a specific electrical, mechanical or control requirement.

ALLBERT did not begin as a robot designed entirely from a predetermined parts list. The project started with a robotics kit that was given to me. I soon realized that as the build developed, I would need different parts that the kit did not offer nor fit my vision. I chose to keep only a small number of the original kit's components and build the rest of the system around parts selected from different sources. I even purchased a second kit twice to construct the base layer that I wanted.

As a result, ALLBERT became a custom combination of hardware that was never originally designed to work together as a single system. Building it required me to learn how to integrate those components, solve compatibility and mounting problems, revise earlier decisions, and sometimes redesign portions of the robot as new challenges appeared. The hardware choices documented below reflect that process and explain not only what I used, but why I chose each solution.





