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
- **Mid-Level Logic Layer:** Interprets sensor states and applies decision-making logic to determine appropriate actions, such as advancing, turning or escaping from a blocked path.
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

#### TB6612FNG Motor Controller

When I began working with ALLBERT's TT motors, one of the first problems I encountered was simply determining how the motors would connect to and be controlled by the rest of the system. The motors had their own wiring, but there was no appropriate place to connect them directly to the BeagleBone Black. Researching how DC motors are controlled led me to motor controllers and eventually to the TB6612FNG.

During my research, I compared the TB6612FNG with alternatives such as the L298N and found the TB6612FNG to be a better fit for the project. Another consideration at the time was soldering. I had never soldered before and was not yet comfortable doing it, so finding a motor controller with its pins already installed influenced my decision. Ironically, as ALLBERT developed, I eventually learned to solder and incorporated soldering extensively into the finished electrical assembly.

The TB6612FNG serves as the interface between ALLBERT's control computer and its motors. The BeagleBone Black determines how the robot should move and sends low-power direction and PWM control signals to the motor controller. The TB6612FNG then uses the separate motor power supply to drive the motors according to those commands.

ALLBERT uses four TT motors, while the TB6612FNG provides two motor-control channels. I organized the motors into left and right sides, with the two motors on each side operating together through one channel. This arrangement made sense because ALLBERT's wheels do not physically pivot left or right like the steering wheels of a conventional car. Instead, the robot changes direction by controlling the movement of its left and right sides differently. One side can move differently from, or opposite to, the other side to produce turning and pivoting behavior.

This configuration allowed a two-channel motor controller to provide the movement control needed for ALLBERT while keeping the motor-control architecture straightforward and consistent with the robot's physical design.

#### Power System

When I began designing ALLBERT's power system, I did not initially know that the motors and control electronics should be powered separately. Through research and development of the motor-control system, I learned that the motors and computing hardware have different electrical requirements and that separating their power supplies would provide a cleaner and more appropriate power architecture.

For the BeagleBone Black and Raspberry Pi 3B+, I chose an Anker power bank. My available options were limited, and I needed a portable power solution that could accommodate the different USB connections required by both computers. Using the appropriate USB cables allowed one portable power source to support the computing side of ALLBERT without relying on the motor power supply.

The four TT motors receive their power separately through the TB6612FNG motor controller. For the motor supply, I used a six-slot AA battery holder containing four AA batteries and two dummy cells. Although the holder could physically accommodate six batteries, I deliberately chose four active cells to provide approximately 6V rather than supplying the approximately 9V that six fresh 1.5V cells could produce. This allowed me to operate the motor system more conservatively while still using the battery holder that fit the physical design of the robot.

Separating the power sources did not mean completely separating the two electrical systems. As I developed the design, I learned that the BeagleBone Black and motor controller still needed a common ground. Sharing this ground provides a common electrical reference so that the motor controller can correctly interpret the control signals sent by the BeagleBone Black.

The resulting power architecture separates the computing and motor loads while still allowing both sides of ALLBERT to communicate through a shared electrical reference. It also gives each part of the robot a power source appropriate for its role rather than attempting to operate the entire system from a single supply.

#### Wiring and Connections

As ALLBERT's electrical system became more complex, I learned that different types of electrical connections did not necessarily require the same type or size of wire. Connections carrying power may need larger conductors because they can carry more current, while GPIO and other control signals carry much smaller currents and can use thinner wiring. I applied this distinction throughout the robot rather than attempting to use one type of wire for every connection.

The physical layout also required me to adapt some of the wiring. Several existing jumper wires were not long enough to reach their intended destinations, so I learned how to extend wiring by carefully stripping insulation, preparing the conductors, and creating secure crimped connections. In some cases, this also required joining wiring of different sizes when the available connections required it.

Another priority was keeping portions of ALLBERT's wiring removable. I did not want every connection permanently soldered in place because I wanted the robot to remain adaptable. If I later change the chassis, increase the robot's size, replace damaged wiring, change its physical design, or replace a component, I want to be able to reuse working portions of the existing electrical system rather than rebuilding the robot from the beginning.

This led me to use jumper wires, headers, connectors, and terminal connections where appropriate. Low-current sensor and control signals could use jumper-style connections between the sensors, BeagleBone Black, and motor-controller control inputs, while shared 3.3V power and ground connections were organized through the screw terminal blocks. Motor output connections from the TB6612FNG were also designed with serviceability in mind so that the motor wiring could be disconnected or changed without unnecessarily rebuilding the surrounding electrical assembly.

The resulting wiring system reflects an important principle behind ALLBERT's design: individual parts of the robot should be replaceable or modifiable without requiring the entire system to be rebuilt. Keeping the electrical system organized and modular allows future versions of ALLBERT to build upon working subsystems rather than always starting from the beginning.

#### Sensors

For ALLBERT's obstacle-detection system, I wanted the robot to be able to understand whether movement was possible in each of its four primary directions: front, rear, left, and right. Detecting an obstacle directly in front of the robot would not be enough for autonomous navigation. If the front is blocked, ALLBERT also needs information about the surrounding directions before deciding whether it can turn or back away safely.

I therefore equipped ALLBERT with four directional KY obstacle sensors, with one sensor responsible for each primary direction. I deliberately kept the sensing system relatively simple. For the current version of ALLBERT, the navigation system does not need to identify objects or build a detailed representation of its surroundings. It primarily needs to determine whether a direction is clear or blocked.

The digital output from each sensor can be interpreted by the software as a simple obstacle state. This provides the mid-level decision logic with the information it needs without introducing additional sensing complexity that the current navigation system does not require. More advanced sensors can be incorporated in future versions if ALLBERT eventually requires capabilities such as more precise distance measurement, mapping, or environmental recognition.

Physical placement was also important. Each sensor was positioned to maintain a clear view of the direction it monitors. Wiring and other components were arranged so that they would not unnecessarily obstruct the sensors' detection paths.

This sensor configuration reflects a principle I have followed throughout ALLBERT's development: complexity should serve a purpose. The current sensors provide the information required for the robot's navigation decisions while keeping the hardware and software straightforward and understandable.

#### Computing Hardware Integration

One of the early decisions in ALLBERT's development was determining what computer should control the robot. I was interested in both the Raspberry Pi and the BeagleBone Black, but I learned that the BeagleBone Black offered hardware capabilities that made it well suited for embedded control and timing-sensitive interaction with physical hardware.

Rather than choosing one platform and abandoning the other, I began exploring whether the Raspberry Pi and BeagleBone Black could be used together. This led to a larger architectural decision: instead of having one computer responsible for every part of ALLBERT, I could give each computer a dedicated role and allow them to operate together as parts of a larger system.

The BeagleBone Black became ALLBERT's hardware-control computer. It interfaces with the robot's sensors and sends the GPIO and PWM control signals required by the motor controller. The Raspberry Pi 3B+ was assigned the higher-level interface and network role, providing the foundation for ALLBERT's web dashboard and communication with the BeagleBone Black.

This separation reflects the same design philosophy I use when writing software. I prefer systems in which individual functions, classes, components, and subsystems have clearly defined responsibilities rather than having one part attempt to perform every task. The Raspberry Pi and BeagleBone Black therefore operate as separate subsystems with different responsibilities while contributing to the operation of the same robot.

For example, a movement command originating from ALLBERT's web dashboard can be received by the Raspberry Pi and communicated to the BeagleBone Black. The BeagleBone Black then translates the requested movement into the appropriate control signals for the TB6612FNG motor controller, which supplies the motor outputs that physically drive the robot.

Using two computing platforms gives ALLBERT a modular computing architecture in which the user-facing and network responsibilities can develop independently from the hardware-control system while still allowing both sides to work together as a complete robotic system.

#### Layered Software Architecture

ALLBERT's software did not begin as a layered system. The original program consisted primarily of a single Python class containing the GPIO pin assignments and functionality required to control the robot's wheels. At that stage of development, the immediate goal was simply to establish direct software control over the physical hardware.

As the robot developed, I realized that movement could not safely depend on hardware-control code alone. ALLBERT would eventually be making movement decisions based on information received from its sensors. If that information was missing, invalid, or incorrectly handled, the result would not be limited to a software error. The robot could move incorrectly and physically run into a wall or another obstacle.

This led me to begin separating the software into layers with different responsibilities. Rather than allowing one class to receive information, make decisions, and directly control the hardware, I wanted each part of the software to correspond to a specific responsibility within the robotic system.

The resulting architecture is divided into three primary layers:

- **Low-Level Hardware Layer:** Responsible for direct interaction with the physical hardware, including GPIO, PWM, and motor-control operations.
- **Mid-Level Logic Layer:** Evaluates sensor information and determines which movements are appropriate based on the robot's surroundings and safety conditions.
- **High-Level Autonomous Layer:** Coordinates the robot's larger autonomous behavior and determines what ALLBERT should attempt to do.

This architecture also reflects how I prefer to design software generally. I like systems and subsystems in which individual components have clearly defined responsibilities and work together rather than having one part of the program attempt to manage everything.

For ALLBERT, that separation has an additional safety purpose. Information can be evaluated before it ultimately results in physical movement, allowing safety and decision logic to exist between environmental input and hardware action.

The layered architecture therefore developed from both a software-design preference and a physical requirement: as ALLBERT became more autonomous, its software needed a structure that could organize responsibility while reducing the possibility that bad information would lead directly to unsafe movement.

#### Low-Level Hardware Control

ALLBERT's software began with its low-level hardware-control code. The original program was primarily a Python class containing the BeagleBone Black GPIO pin assignments required to control the robot's motors. As the code developed, I wanted to keep the individual GPIO operations organized rather than allowing hardware instructions to become scattered throughout the program.

I began placing the operations required for particular movements inside dedicated functions. Instead of other parts of the program needing to know which GPIO pins must be HIGH or LOW or how PWM should be configured, they could request a movement such as `move_forward()` and allow the hardware-control code to handle the individual operations required to produce that movement.

I also organized the motors into left and right wheel groups so that common movement operations could work with those groups rather than repeating nearly identical code for each motor. This followed a programming principle I already valued: Don't Repeat Yourself (DRY). When the same behavior is required in multiple places, I prefer to implement the underlying logic once and reuse it.

Motor speed introduced another low-level consideration. PWM duty-cycle values must remain within their valid range, so I created a `clamp_speed()` function that constrains requested speed values between 0 and 100 before returning them for use by the PWM system. This prevents an out-of-range value from being passed directly into the hardware-control library.

I also introduced a `@safe_method` decorator around low-level movement operations. Its purpose is to provide an additional layer of protection around GPIO-related operations so that incorrect data or an exception can be handled rather than allowing a hardware-control operation to fail without being accounted for.

The result is a low-level layer with a clearly defined responsibility: translate movement requests into the GPIO and PWM operations required by ALLBERT's physical hardware while keeping those hardware-specific details contained within one part of the software.

#### Mid-Level Decision Logic

As ALLBERT's software developed beyond direct hardware control, I wanted the decision-making process to remain simple and structured. Rather than allowing sensors to directly determine motor behavior, I separated sensing, decision-making, and physical movement into different responsibilities.

The sensors provide information about ALLBERT's surroundings, while the mid-level logic interprets that information and determines which movement is appropriate. The resulting movement request can then be passed to the low-level hardware layer, which is responsible for translating that request into the GPIO and PWM operations required by the motors.

This creates a structured progression of information through the system:

`Sensor State → Decision Logic → Movement Request → Hardware Control`

The mid-level can also evaluate multiple sensor states when making a decision. For example, detecting an obstacle in front of ALLBERT does not automatically mean that the robot should always turn in one predetermined direction. The surrounding sensor states can be evaluated to determine which available movement is appropriate.

Mid-level functions receive the existing robot-control object as a parameter. This allows the decision logic to use capabilities such as `move_forward()` or `pivot_turn_left()` without creating or owning another hardware-control object. The mid-level therefore determines which action should occur while the low-level remains responsible for how that action is physically performed.

I also created an `escape()` behavior for situations where the normal movement process should not continue. Rather than continuing to evaluate increasingly complicated movement conditions, the fallback behavior can stop the robot, back it away from the immediate situation, and end the current process.

The purpose of the mid-level layer is therefore not to directly control ALLBERT's hardware, but to provide a clear transition between environmental information and physical action. Each subsystem performs its own responsibility, allowing data and control to progress through the program in a structured and understandable way.














