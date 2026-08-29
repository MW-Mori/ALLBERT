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
- **Low-Level Hardware Logic:** This layer interfaces directly with the physical hardware, translating movement commands into GPIO and PWM signals used to control the motors
