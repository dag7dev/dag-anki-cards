TARGET DECK: HCIW
START
Basic
Describe wearable devices, the features and common use cases
Back: 
Inventing, designing, building, or using body-borne computational and sensory devices

## Features
* **Intertwined**: No separated human and computer entities
* **Constancy**: it is not necessary to turn on the device before interacting
* **Multi-tasking**

Example: Forget-me-not

## Common use-cases
* Smartwatch
* AR/VR devices
* Body-worn sensors, such as activity trackers (not only on the wrist)
* Health and medical devices
<!--ID: 1721143899164-->
END

---

START
Basic
What's the meaning of interruptions? What's the difference between interruptions and interactions?
Back: 
**Interruptions** that wearables can cause the user, can distract the user from the actions the user is performing.

Interruptions can be:
* **Immediate**: force the user to take action (a continuous vibration to notify a call)
* **Negotiated**: announce the interruption and allow the user to decide when to deal with it (notifications)
* **Scheduled**
* **Mediated**: the context is used to decide **when** to interrupt the use

The difference is that interactions describes how the user interact with the system and can react to an interruption.

Interactions can be:
* **Eyes-free hand gestures**: open and close the hand wearing the device
* **Head gestures**: shaking the head to ignore a call while wearing AirPods
* **Wrist gestures**: raise-to-wake in smartwatches and smartbands.
<!--ID: 1721143899166-->
END

---

START
Basic
What is IoT? Tell me more about it.
Back: 
IoT (Internet of Things) devices are **physical objects embedded with sensors, software, and network connectivity** that enable them to **collect and exchange data**. These smart devices can range from household appliances to industrial equipment, allowing for remote monitoring, control, and automation in various applications.
>[!info] In IoT devices, the service is as critical as the device.

> IoT is all about data

Embedded devices capture data from the real world and the data are used to **provide a specific service to the user**. The service can be provided using traditional UIs on other devices: imagine a weather station where it is possible to check the results on a smartphone or with a web app.

Some IoT devices work **asynchronously** to save power.
>[!info] Remember that the computing part could run on other devices or in the cloud and not on-device.
<!--ID: 1721143899168-->
END

---

START
Basic
Is IoT fault tolerant by default? Why? Is it a distributed system?
Back: 
A failure in one service's component can compromise the device's functionality, even if it is working perfectly, so it is not "fault tolerant" by default.

> Designers should clarify the system model while ensuring operation to keep users in control.

One important aspect of IoT devices is **interusability**: the experience of an IoT device is **distributed** across multiple devices.
<!--ID: 1721143899169-->
END

---

START
Basic
Describe the IoT stack
Back: 
![[Pasted image 20240713180932.png]]
>[!info] This design stack is based on the idea of **integrated thinking**: the components should be designed together to achieve the best possible integration.
* **UI/Visual Design**: Design the layout and aesthetic
* **Interaction Design**: Designing the sequence of actions the user should perform to complete a task.
* **[[#Distributed Functionality|Interusability]]**: Design the **cross-device** user flow.
* **Industrial Design**: Design the product in terms of physical hardware.
* **Service Design**: Design the services **around the product**: software updates, customer support, and in-store experience.
* **Conceptual Model**: Design how the user will figure out how to use the service.
* **Productisation**: Creation of the final appealing product to sell.
* **Platform Design**: Developing a software framework that enables developers to integrate IoT devices with other services or create custom applications for the product. This typically includes tools like Software Development Kits (SDKs), APIs, and documentation to facilitate seamless connectivity and functionality expansion.
<!--ID: 1721143899171-->
END

---

START
Basic
What are beacons? Is it something related to bluetooth? Give some examples
Back: 
**BLE** (Bluetooth Low Energy) beacons are **small wireless transmitters** that broadcast signals using Bluetooth Low Energy technology. 

These devices periodically emit unique identifiers which can be detected by nearby smartphones or other BLE-enabled devices. 

Beacons are typically used for **location-based services, proximity marketing, indoor navigation, and asset tracking** due to their low power consumption and ability to provide accurate micro-location data.
<!--ID: 1721143899172-->
END

---

START
Basic
Describe Interface and Interactions for IoT
Back: 
- **physical controls**: buttons, switches, sliders, knobs
	- **pros**: direct, fast, good for fine adjustements, accessible for the visually impaired
	- **cons**: less suitable for frequently updated products, since the interface is not upgradable
- **lights**: color coding, blink patterns
	- **pros**: glanceable, non intrusive information output
	- **cons**: not suitable for complex information
- **displays and screens**: segment displays, monochrome displays, e-ink...
	- **pros**: makes objets dynamic, and keeps products flexible
	- **cons**: can complicate the user experience and potential **feature creep**
- **audio output**: sounds, tts
	- **pros**: pervasive, emotional, no visual attention eeded
	- **cons**: issues with pronunciation, localization costs
- haptics: vibration, object manipulation
	* **Pros**: Easier to learn, less computer-like interaction, good for educational purposes.
	* **Cons**: Not ideal when the reliability of keeping parts together is crucial.
* **Gestural Input**: Swipe, pinch, mid-air gestures.
	* **Pros**: Good for video games, wearables, and short interactions.
	* **Cons**: Not suitable for precision or lengthy interactions
- **Context-Sensitive Interaction**: Based on location or proximity to products.
	* **Pros**: Manages complexity with little interaction.
	* **Cons**: May be perceived as patronizing if it limits user control.
- **Computer Vision and Bar Codes**: Facial recognition, biometrics, QR Codes, OCR.
	* **Pros**: Can replace cumbersome manual input.
	* **Cons**: May require more complex interaction than alternatives.
<!--ID: 1721143899174-->
END

---

START
Basic
Describe AirTag
Back: 
Technology for transmitting information across a wide bandwidth. 

Used for real-time location and peer-to-peer fine ranging, which allows many applications based on relative distance between two entities.
<!--ID: 1721143899175-->
END

---

START
Basic
What's the difference between context-aware and implicit interaction? Can you tell about some features and examples? 
Back: 
Context-aware systems use sensors and perception algorithms to understand the environment and take appropriate actions.

Examples:
- **Automatic lights**: current light condition, motion
- **Car display dims in tunnels**: location
- **Brightness of smartphone display**: external light intensity
- **Temperature sensor-based cooling management**: temperature

ABS is a good example too: it anticipates the user need and doesn't require too much active attention.

Some general concepts includes:
- **Context Information**: Includes location, time, temperature, light, user activity and more.
* **Feature Space**: Hierarchical structure of factors influencing system behaviour.
* **Awareness Mismatch**: Discrepancy between system behavior and user expectation.
* **Mental Models**: User's understanding of how the system works.


On the other hand, **implicit interaction** focuses on interpreting user actions not primarily intended as computer input. Aims to seamlessly integrate output with the environment and user tasks.

* Implicit input
	> Actions and behaviours of humans which are done to **achieve a goal,** and which are not primarily regarded as interaction with a computer, but **captured, recognised, and interpreted by a computer system as input**.
* Implicit output
	> Output of a computer **not directly related to an explicit input**, and which is **seamlessly integrated** with the environment and the task of the user.

Implicit interaction **is not an alternative** to explicit interaction.

<!--ID: 1721143899177-->
END

---

START
Basic
What is ubiquitous computing?
Back: 
**Ubiquitous computing** aims to integrate technology seamlessly into everyday life
<!--ID: 1721143899178-->
END

---

START
Basic
How to design a context-aware system?
Back: 
1. Create a hierarchical feature space for system behavior.
2. Provide information about sensory input to minimize [[#Keywords for Context-Aware interaction|awareness mismatch]].
3. Identify characteristic features and appropriate sensors for **context detection**
4. Consider presenting options rather than anticipating a single user's need.
5. Use UI adaptation carefully to maintain stability and memorability.
<!--ID: 1721143899179-->
END

---

START
Basic
What are TUI? Give some examples
Back: 
**Tangible user interaction** emerged in the 90s as a response to WIMP (Windows, Icons, Menus, Pointers) interfaces.

The main idea is to **give physical form to digital information**, using physical artifacts as both representations and controls.

Examples include:
* Augmented Reality
* Tabletop Interaction
* Ambient Displays
* RFID
* Computer vision
* Microcontrollers, sensors and actuators

## Key Characteristics
* **Computational coupling**: Tangible objects linked to digital data.
* **Interactive control**: Moving and manipulating objects is the primary form of interaction.
* **Perceptual coupling**: Objects coupled with digital representations, such as audio or visuals.
* **Representation significance**: The physical state of the objects reflects the system state.

Pros:
* Intuitive interaction through physical manipulation.
* Utilizes natural spatial and motor skills.
* Can enhance collaborative working and learning.

Cons:
* **Scalability issues**: limited to small datasets.
* **Single-purpose** or **task-specific** (limited).
* **Limited malleability**: physical objects are rigid and static.
* **Potential for user fatigue**: object weight and size.
* **Lack of "undo" functionality**.
<!--ID: 1721143899180-->
END

---

START
Basic
What haptic interactions are? Why are they useful?

Back: 
**Haptic interaction** combines movement and touch to enable manipulation of physical and virtual objects.

Haptic interaction is particularly **useful when visual interaction is impractical or impossible**, such as for individuals with **visual impairments** or in situations requiring **eyes-free operation**.

Cons:
* Spatial and temporal resolution constraints
* Perceptual integration challenges
* Limited attention capacity
<!--ID: 1721143899182-->
END

---

START
Basic
Describe tactual perception (haptic)
Back: 
Haptic perception involves both cutaneous and kinesthetic senses, providing a rich sensory experience.

Three kinds:
* **Cutaneous sense**: Awareness of skin stimulation
* **Kinesthetic sense**: Awareness of body positioning
* **Tactual modes**: Range from passive to active perception
<!--ID: 1721143899183-->
END

---

START
Basic
Touch vs. Sight: what's the difference?
Back: 
* No dominant sense in case of conflict
* Touch excels in perceiving substance dimensions (e.g., hardness, texture)
* Sight is faster for processing structural information
<!--ID: 1721143899184-->
END

---

START
Basic
What are the haptic symbols?
Back: 
1. **Line symbols**: Raised lines as tactile substitutes for visual ones
2. **Point symbols**: Explored with minimal fingertip movement
3. **Areal symbols**: Use of texture or tactile patterns

The effectiveness of haptic symbols depends on factors such as traceability, distinguishability, and perceptual integration.
<!--ID: 1721143899186-->
END

---

START
Basic
What is Haptic Feedback and Rendering?

Back: 
* Force feedback interfaces (1DOF to 7DOF)
* Compute and generate forces based on virtual object interactions
* Requires high processing speed (at least 1000 Hz)

Haptic rendering can be conceptualized as pushing the device out of a virtual object when it attempts to move inside, creating the sensation of a solid surface.

Applications are:
1. **Medical**: Tissue modeling, training, remote surgeries.
2. **Three-dimensional modeling**: Virtual prototyping, sculpting.
<!--ID: 1721143899187-->
END

---

START
Basic
What are gestures? How many kinds exist? Give some usage examples  
Back: 
**Gesture** is a Non-verbal/non-vocal communication using visible bodily actions to convey messages.

It may Include movements of hands, face, or other body parts

Gesture recognition uses mathematical algorithms to interpret human gestures

There are two kinds of gestures:
1. **Touch gestures**
2. **Touchless gestures**

Examples:
- **Leap Motion**: Uses monochromatic IR cameras and infrared LEDs
- **Kinect**: Combines depth sensor, spatial microphone array, video camera, and orientation sensor
<!--ID: 1721143899188-->
END

---

START
Basic
What are touchless gestures?
Back: 
The **touchless** ones, allow interaction with devices **without physical contact**, using technologies like **computer vision, image processing, and inertial measurement units**.

Some Technologies for Touchless Gestures
- Stereoscopic cameras
- Infrared sensors
- Inertial motion capture gloves
- Wired gloves
- Laser-scanners
<!--ID: 1721143899190-->
END

---

START
Basic
What are the open challenges in gestural interaction?
Back: 
1. **Interaction fidelity**: Balancing natural and "magic" (hyper-natural) interactions
2. **Precision in spatial input**:
    - Lack of physical support
    - Natural hand tremor
    - Amplification of errors in ray-casting interactions

However, precision issues could be solved by:
-  Filtering tracker output
- Modifying control/display ratio
- Designing for necessary precision
- Using progressive refinement techniques
<!--ID: 1721143899191-->
END

---
START
Basic
Describe the differences between 3D User Interfaces, Virtual Reality, Aumented Reality and Mixed Reality
Back: 
- **3DUI**:  performed directly in a 3D spatial context, on large displays, and requires spatial tracking / additional inputs (aircraft simulator)
- **VR**: Immersive environments created by software, providing sensory feedback (auditory, visual, haptic). You typically access it by using headsets. It is used in a wide range of applications: healthcare, engineering, museums, entertainment... 
- **AR**: Enhances real-world environments with computer-generated information
- **MR**: Merges real-world objects into virtual worlds (e.g., Microsoft HoloLens)
<!--ID: 1721143899192-->
END

---

START
Basic
What are zooming interfaces?
Back: 
A **Zooming User Interface (ZUI)** is based on an **infinite plane with infinite resolution**, allowing users to pan, zoom in, and zoom out.

Since traditional GUIs are based on views, navigation often involves buttons and tabs and can be **difficult to backtrack or remember information locations**.

Pros:
- Users can **change the scale** of the viewing area
- **Encourages memory based** on landmarks and relative positions
- Allows for **associations** based on proximity
- Establishes **hierarchical relationships** through zooming
- Users can **organize objects as they prefer**
<!--ID: 1721143899194-->
END

---

START
Basic
HCI in the car
Back: 
Modern cars are **equipped with CPUs, sensors, actuators, and various interaction devices**, making them connected and capable of advanced functionalities.

Examples:
* Navigation systems
* Entertainment systems
* Cell phones
* HVAC systems (Heating, Ventilation, and Air Conditioning)

However, these interactive systems **can lead to potential distractions**, affecting **visual attention and cognitive load**.

Keywords for HCI in Cars
* **Visual Attention**: The focus required on the road vs. in-car systems
* **Cognitive Load**: Mental effort required to operate car systems while driving
* **Context Restoration**: Process of refocusing on driving after interacting with car systems
* **Hands-free Interaction**: Methods of interacting with car systems without manual input
* **Driver in the Loop**: Concept of keeping the driver engaged in semi-autonomous systems
<!--ID: 1721143899195-->
END

---

START
Basic
What are the challenges of ui in automotive domain? 
Back: 
* Different from desktop and mobile environments
* Touch-sensitive screens can become safety hazards
* Position of controls affects driver's focus

**Shifting eyes** from road to device requires **context restoration**, impacting driving safety.

The challenge lies in **designing systems** that **enhance driving experience and safety** without overwhelming or disengaging the driver.
<!--ID: 1721143899196-->
END

---

START
Basic
What hands-free interactions are? Where are they used?
Back: 
These are the kinds:
* Audio output
* Speech recognition
* Gesture recognition

They are used especially in cars, to avoid context-break.
<!--ID: 1721143899198-->
END

---

START
Basic
Describe some advanced control systems.
Back: 
* Automatic transmission
* **Anti-skid braking**
* Stability controls
* Active cruise control
* **Lane-keeping assistance**
* **Automatic parking**
* Overtaking vehicles detection
* **Automatic payment for tolls and parking**

The integration of advanced control systems raises questions about the driver's role and the balance between automation and human control.
<!--ID: 1721143899200-->
END

---
