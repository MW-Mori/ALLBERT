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

### Computing Architecture

ALLBERT uses both a Beaglebone Black and a Raspberry Pi 3B+, with each computer assigned a different role within the system. The BeagleBone Black serves as the primary hardware-control, handling direct interaction with the robot's motors and sensors through GPIO and PWM capabilities. The Raspberry Pi 3B+ serves as the higher-level interface computer, providing the foundation for ALLBERT's web dashboard and communication with the hardware-control system.

## Hardware

ALLBERT's hardware was selected and assembled with an emphasis on reliable control, modularity, safety, and the ability to troubleshoot or modify individual parts of the system. Many of these hardware decisions evolved as the robot was built and tested with each decision addressing a specific electrical, mechanical or control requirement.

ALLBERT did not begin as a robot designed entirely from a predetermined parts list. The project started with a robotics kit that was given to me. I soon realized that as the build developed, I would need different parts that the kit did not offer and that some of the original components did not fit my vision for ALLBERT. I chose to keep only a small number of the original kit's components and build the rest of the system around parts selected from different sources. I eventually purchased two additional robotics kits, different from the original, so I could use and combine specific pieces from them to construct the base I envisioned for ALLBERT.

As a result, ALLBERT became a custom combination of hardware that was never originally designed to work together as a single system. Building ALLBERT meant learning how to make these different components work together. Along the way, I had to solve compatibility and mounting problems, learn new methods of wiring and assembly, reconsider earlier decisions when something did not work as expected, and redesign portions of the robot as new challenges appeared. The hardware choices documented below reflect that process and explain not only what I used, but why I chose each solution.

### Hardware Decisions

#### Perfboard

One of my first hardware challenges was figuring out how the motor controller and its required wiring would become a secure part of ALLBERT. The motor controller needed to connect to several parts of the electrical system, but I also needed a way to organize those connections and securely mount the controller to the robot's base.

I initially considered using a solderless breadboard. However, as I learned more about its role in prototyping and testing, I decided that I wanted ALLBERT's final electrical system to use a more permanent construction method. This led me to using a Perfboard, even though I had never used one or soldered before and was initially uncomfortable with the idea of soldering.

The transition was not immediate. One of the first approaches I considered involved soldering wires directly to the motor controller's pins. In practice, the wires and solder were too cumbersome for the small pins, making the connections awkward, fragile, and difficult to secure. Rather than continuing with a connection method that did not work well physically, I reconsidered how the motor controller should interface with the rest of the electrical system.

Using Perfboard ultimately gave the motor controller a secure physical home, kept the electrical assembly organized, and made it easier to mount to ALLBERT's base. More importantly, it allowed the motor-control assembly to become a permanent part of the robot rather than remaining a temporary prototype.

#### Screw Terminal Blocks

As ALLBERT's electrical system grew, I realized that I needed a central location for connections that would be shared across multiple components. There were only so many connection points available directly on the individual boards, and although I understood that certain connections needed to be distributed throughout the robot, I initially could not visualize how to organize that distribution cleanly.

Screw terminal blocks provided the missing piece. They offered a secure central connection point where wiring that shared a common electrical connection could be brought together and then distributed to the components that needed it. I ultimately used two terminal blocks: one for ALLBERT's 3.3V logic power rail and another for the common ground rail.

Implementing the terminal blocks also presented another practical challenge. Some of the jumper wires from the BeagleBone Black and motor-control area were not long enough to reach the location of the terminal blocks. This required me to learn how to extend wiring by stripping insulation, preparing the conductors carefully, and creating secure crimped connections without leaving the wire strands frayed or exposed.

The terminal blocks ultimately made ALLBERT's electrical system cleaner, more organized, and easier to modify. Instead of connections appearing to be placed wherever space was available, each connection had a defined location and purpose. This supported a design approach that I continued throughout the build: keep the system clean, organized, understandable, and easy to readjust when changes are necessary.

#### Standoffs and Physical Mounting

Once the perfboard became the foundation for ALLBERT's motor-control and electrical assembly, I needed a way to securely mount it to the robot's base while keeping the electronics accessible. The selection of mounting hardware available to me was somewhat limited, so I focused on finding a solution that was practical, reliable, and appropriate for the design.

I chose plastic standoffs rather than metal ones. In addition to supporting and raising the perfboard from the robot's base, the nonconductive material eliminated an unnecessary conductive path near the electrical system. This was important to me because I wanted to remain conscious of future wiring changes and reduce the possibility of an exposed connection accidentally contacting conductive mounting hardware.

The standoffs allowed the perfboard to function as more than a board holding individual components. Once mounted, it became a secure physical platform for ALLBERT's electrical system, including the motor controller and its surrounding connections. Raising and securing the assembly also made it easier to access the motor controller, connect and adjust jumper wires, and route wiring without the perfboard moving around during changes.

This approach gave the electrical system a defined location within ALLBERT while keeping it accessible for future adjustments, supporting the same clean, organized, and serviceable design approach used throughout the build.



