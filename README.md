# Dag's Anki Cards
This repository contains Anki cards in markdown format. The cards are organized in decks, one deck for each `.md` file. Each deck contains cards for a specific topic.

All cards are in English, except where otherwise specified.

Spread markdown, not word documents or pdfs. :heart:

## Disclaimer
All these cards are derivative works of:
- my personal notes
- papers
- websites
- public documents (e.g. Google Docs, pdf...)
- private documents (e.g. notes shared by other students)

The cards are provided as-is, without any warranty. Me and the original authors of the documents are not responsible for any damage caused by the cards or any improper use of the cards. We are not liable in case you fail to learn anything because you relied on these cards, or in case of misinterpretation of the cards, or in case of any other problem. **Use at your own risk**.
The cards are obviously not guaranteed to be correct, complete, up-to-date or fit for any purpose. 
Think of them as a starting point for your studies, not as a replacement.

Do not use these cards if you don't agree with the above.

## Content
- `Biometrics.md`: cards about biometric systems (e.g. fingerprint, iris, face recognition)
  - They are in Italian
  - Topics not covered (give a look by yourself)
    - Keystroke recognition
    - Gait recognition

- `Distributed Systems.md`: cards about distributed systems (e.g. paxos, consensus, fault tolerance...)
  - Topics not covered
    - Algorand: ♋
    - GDPR Seminar
    - BGP Seminar
    - some particular long or complicated exercises (never seen at the exam, but only on exercises pdf. See the pdf sent by Tommaso if you want the solutions or check GitHub "SapienzaStudents" repo)

- `Blockchain.md`: cards about blockchain (e.g. bitcoin, ethereum, smart contracts...)
  - Topics not covered
    - Algorand: Feel free to add it yourself.
    - Rug Pull - Defi and Dex: they're already covered by distributed systems cards
    - IPFS: that seminar was about IPFS cryptography, that is veery very long and complex. But in short IPFS is explained.

- `Big Data Computing.md`: cards about big data computing (e.g. hadoop, mapreduce, spark...)
  - Topics not covered: Hadoop and Spark syntax, algorithms too in-depth

- `Multimodal Interaction`: cards about multimodal interaction (e.g. speech recognition, gesture recognition, multimodal fusion...). Big thanks to [Riccardo](https://github.com/riccardoscuto).

- `Human Computer Interaction on the Web`: cards about human computer interaction. All the main topics are explained, excepts for voice interactions and chatbots. List of topics:
```
1 Wearable devices
  - Features
  - Common use-cases
  - Interruptions
  - Interactions
2 Internet of Things (IoT)
  - Distributed Functionality
  - IoT Design Stack
  - Beacons
  - Interface and Interactions for IoT
    - Physical Controls
    - Lights
    - Displays and Screens
    - Audio Output
    - Tangible and Tactile Interfaces
    - Gestural Input
    - Context-Sensitive Interaction
    - Computer Vision and Bar Codes
  - Ultra Wide Band (AirTag)
3 Context-Aware and Implicit Interaction
  - Keywords for Context-Aware interaction
  - Design Hints
  - Categories
  - Implicit Interaction
    - Main challenges
4 Tangible User Interfaces (TUIs)
  - Key Characteristics
    - Technologies used
    - Advantages
    - Limitations
5 Haptic Interaction
  - Tactual Perception
  - Touch vs. Sight
  - Wearable devices
  - Features
  - Haptic Symbols
  - Limitations of Tactile Perception
  - Haptic Feedback and Rendering
  - Applications
6 Gestural Interaction
  - Key Concepts
  - Types of Gestural Interaction
  - Technologies for Touchless Gestures
  - 3D User Interfaces
  - Virtual Reality (VR)
  - Augmented Reality (AR) and Mixed Reality (MR)
  - Challenges in Gestural Interaction
7 Zooming Interfaces
  - Comparison with Traditional GUIs
  - Key Features of ZUIs
  - Advantages over Traditional Interfaces
8 HCI in the Car
  - Interactive Systems in Cars
  - Unique Challenges of UI in Automotive Domain
  - Hands-free Interaction
  - Advanced Control Systems
  - Keywords for HCI in Cars 
```
- `Cloud computing`: These are the covered topics, more or less. (Starred ones are the not covered topics)
```
1 Introduction
  1.1 What is Cloud Computing?
  1.2 Service Models                                                
  1.3 Responsibilities
  1.4 Deployment models
  1.5 Cloud Roles                                          
2 Enabling Technologies
  2.1 Parallel vs Distributed
  2.2 Architectures
  2.3 Inter-Process Communication
  2.4 Service Oriented Architecture
  2.5 Microservices
  2.6 Virtualization

3 Autonomic Computing
  3.1 Self-* properties
  3.2 MAPE-K
  3.3 Models and Applications of Autonomic Computing 
  3.4 Planning
  *3.5 AC Adoption Model Levels
4 Automation and Orchestration
  *4.1 Automation
  *4.2 Ansible: tool for automation
  4.3 Orchestration
  *4.4 Kubernetes: most famous orchestrator

5 Autoscaling
  5.1 Threshold-based algorithms
  5.2 Autoscaling on AWS
  5.3 Autoscaling on Kubernetes
  5.4 Adaptive Model-Driven Autoscaling
  5.5 Online VM Auto-Scaling Algorithms

6 Cloud Storage
  6.1 Atomicity
  6.2 Storage models
  6.3 Distributed: Google File System
  6.4 Distributed: Hadoop File System
  6.5 NoSQL databases
  6.6 BigTable
  6.7 Amazon DynamoDB
  *6.8 S3 Object Storage
```
  
Feel free to add the cards you need or modify the existing ones on the markdown file.

## How to use (for Anki users)
1. Download the [Anki desktop app](https://apps.ankiweb.net/).
2. Clone this repository.
3. Import the `.apkg` files in the `decks` folder in Anki.
4. Done! You should now have all the cards in your Anki decks.

NOTE: for now, apkg files are not updated automatically. See last commit date. If you want to update them, you have to do it manually (see below).

## How to use (for Obsidian and Anki users)
1. Download the [Anki desktop app](https://apps.ankiweb.net/).
2. Download the [AnkiConnect](https://ankiweb.net/shared/info/2055492159) plugin.
3. Clone this repository.
4. Download [Obsidian](https://obsidian.md/) and open the Obsidian vault in this repository.
5. Download the [Obsidian_to_Anki](https://github.com/Pseudonium/Obsidian_to_Anki/) plugin and the follow the instructions.
6. Create decks in Anki for each of the `.md` files in this repository. Each deck should have the same name as the `.md` file (see each markdown file for the name of the deck).
7. Import the `.apkg` files in the `decks` folder in Anki.
8. Click on the button in the left sidebar with the "Anki" icon to sync Obisidian to Anki and wait.
9. Done! You should now have all the cards in your Anki decks.

## How to contribute
1. Fork this repository.
2. Edit or add cards in the `.md` files.
3. Create a pull request.
4. Done! I'll review your changes and merge them if they're good.

Do not remove the `<!-- -->` lines. They're used by the Obsidian_to_Anki plugin to generate the `.apkg` files. Removing them will result in the cards not being updated.

Also, if using Markdown, remember to import the `.apkg` files in Anki to update the decks, otherwise you'll have to do it manually (since in md files the comments are present, so the extension thinks the cards are already in the deck).

If you need it, use this regex to remove them: `<!--[\s\S]*?-->` and after you're done, undo the changes to the `.md` files so you won't lose tyour progress on Anki.

## Why
I use [Obsidian](https://obsidian.md/) to take notes. Obsidian is a markdown editor that allows you to create links between notes. It also has a wonderful plugin called [Obsidian_to_Anki] that allows you to export markdown notes to Anki cards. I use Anki to memorize things.

Markdown is a wonderful format for taking notes, but it's not very good for memorizing things. Anki is a wonderful tool for memorizing things, but it's not very good for taking notes. This repository is an attempt to combine the two.

## Credits
- The heroes, who wrote the original documents, from which I took some of the cards here. They helped and contributed in a significant way with their notes. Thank you! :heart: In no particular order:
  - [Riccardo](https://github.com/riccardoscuto) - Multimodal Interaction
  - [Lorenzo](https://github.com/Lorenzoantonelli) - Human Computer Interaction on the Web and Multimodal Interaction
  - [Simone](https://github.com/SimoneSestito) - Cloud Computing
  - [Tommaso](https://github.com/Tommaso-Sgroi/) - Distributed Systems


- My personal notes
- [Obsidian](https://obsidian.md/) and [Anki](https://apps.ankiweb.net/)
- [Pseudonium](https://github.com/Pseudonium) for the Obsidian_to_Anki plugin 

