# AgriQuest: 3D Educational Farming Game

##  Table of Contents
1. [Project Overview](#project-overview)  
2. [Features](#features)  
3. [Gameplay Mechanics](#gameplay-mechanics)  
4. [Technology Stack](#technology-stack)  
5. [Getting Started](#getting-started)  
   - [Prerequisites](#prerequisites)  
   - [Installation](#installation)  
6. [Contributing](#contributing)  
7. [Acknowledgement](#acknowledgement)  

## Project Overview
**AgriQuest** is a 3D mobile farming simulation game developed using **Unity** to support Kenya’s Competency-Based Curriculum (CBC).  
The game transforms agriculture lessons into an interactive experience where students prepare soil, plant crops, rear chickens, and harvest produce, guided by an AI chatbot called **AgriBot**.  

## Features
- Interactive **soil preparation, planting, and harvesting** (maize and beans).  
- **Chicken rearing**: feeding and egg collection.  
- **AgriBot chatbot** for guided learning and feedback (powered by DialogFlow).  
- User profiles with name and grade.  
- Basic scoring system to track progress.  
- Works on **Android, iOS, and WebGL** (for browser demos).  

## Gameplay Mechanics
- **Soil Preparation:** Clear soil using a hoe or by hand.  
- **Planting & Growth:** Plant seeds on cleared soil → progress through growth stages.  
- **Harvesting:** Collect crops once ready → score increases.  
- **Animal Interaction:** Feed chickens once per session → feedback + points.  
- **AgriBot Chatbot:** Provides fixed educational responses to selected questions.  
- **Scoring System:** Awards points for correct actions to encourage progress.  

## Technology Stack
- **Game Engine:** Unity (C# scripts using MonoBehaviour).  
- **Frontend:** Unity UI (buttons, score display, AgriBot dialogue box).  
- **Backend / AI:** DialogFlow (chatbot integration).   
- **Deployment Platforms:** Android APK, iOS, WebGL.  
- **Version Control & Collaboration:** GitHub & Plastic SCM.  

## Getting Started

### Prerequisites
- Unity **2022.3 LTS** or later installed.  
- Android Build Support module (for APKs).  
- WebGL Build Support (for browser demos).  
- Firebase account (optional for persistence).  
- GitHub account for version control.  

### Installation
1. Clone the repo:  
   ```bash
   git clone https://github.com/<username>/<repo>.git
   cd <repo>
   ```
2. Open the project in **Unity Hub**.  
3. Switch build platform to **Android** or **WebGL** via Unity Build Settings.  
4. Run the game in Unity Editor or build an APK/WebGL version.  

## Contributing
1. Fork the repo.  
2. Create a feature branch:  
   ```bash
   git checkout -b feature-new
   ```  
3. Commit changes:  
   ```bash
   git commit -m "Add new feature"
   ```  
4. Push to your branch:  
   ```bash
   git push origin feature-new
   ```  
5. Submit a Pull Request.  


## Acknowledgement
- CBC curriculum mentors and teachers for guidance.  
- DialogFlow team for chatbot tools.   
- Unity community for open-source resources.  
