## SYSTEM DESIGN DOCUMENT

Introduction

Purpose of the Document

This document defines the system architecture, design approach and module-level planning for AgriQuest, a 3D educational farming simulation game that teaches CBC-aligned agriculture concepts through gameplay and AI interaction.

Scope of the System

The minimum viable product will entail the following:

Cultivating a crop that is clearing soil using either a hoe or by hand, planting and harvesting of either maize or beans.

Rearing of chicken by feeding them and collecting their eggs.

A static chatbot called AgriBot for learning support.

Saved user profiles; the name and grade.

A basic scoring system.

It is built for both Android and IOS.

In the near future we will expand our game to include:

Multiple crops and animals.

A dynamic AI chatbot.

A teacher dashboard.

Multiplayer mode.

Intended Audience

The different groups interacting with the game will be:

The development team who are the AgriQuest team members.

Instructors who are the CBC-trained teachers.

Pilot users who are the pupils in grade four to nine.

Glossary

CBC: Competency-Based Curriculum

MVP: Minimum Viable Product

AI: Artificial Intelligence which will be referring to our chatbot.

UI: User Interface

System Overview and Design Philosophy

High-Level description

AgriQuest is a 3D mobile farming simulation game developed using the Unity game engine. It is designed to support students in Kenya’s CBC by transforming agriculture learning into an interactive, gamified experience. The application empowers learners to virtually engage in soil preparation, planting, crop maintenance, harvesting and animal feeding while guided by an AI chatbot assistant named AgriBot.

The game simulates a smart farm where players take on the role of young digital farmers. They perform hands-on tasks aligned with the agriculture curriculum for Grades 4–9. These include weeding the land, planting CBC-relevant crops, watering, applying compost, harvesting and chicken farming.

Players interact with the game by tapping on different objects and tools such as a hoe, watering can, seeds and compost. As actions are performed correctly, the system provides feedback via AgriBot and awards points to reinforce learning. The AI chatbot helps explain farming concepts, clarify student questions and offer encouragement using a rules-based dialogue engine.

The game is optimized for Android and IOS mobile devices and is built with performance in mind, using lightweight 3D assets and modular scripts. It supports both offline play and potential WebGL deployment for browser-based access. All user interactions are local and do not require internet access, making the app suitable for low-resource environments.

Design Principles

These are the principles that will help manage the complexity of the design process, reduce errors and ensure high-quality software.

Modularity: Each game mechanic is its own script.

Scalability: Support for future crops and levels.

Performance: Lightweight models and textures for mobile.

Simplicity: Kid-friendly UI and UX.

Education-First: CBC alignment over realism.

Architectural Design

Architecture Diagram

Architecture Diagram

Architecture Style

AgriQuest AI is designed using a modular, component-based architecture following the principles of Unity’s MonoBehaviour scripting model. This architecture is well-suited for real-time, event-driven applications like 3D games and allows for high flexibility, reuse of components and clear separation of concerns.

The system primarily follows a layered and event-driven architecture composed of the following core layers:

## 1.     Presentation Layer (UI Layer):

This includes the user interface components such as buttons (“Plant”, “Use Hoe”, “Water”), score displays and the AgriBot dialogue box. All user interactions, like tapping on a soil tile or choosing a tool, are captured here and passed to the logic layer.

## 2.     Game Logic Layer (Gameplay Scripts):

This layer contains C# scripts attached to Unity GameObjects. It handles player actions such as soil preparation, crop growth timers and harvesting. GameObjects respond to events like user taps using Unity’s input system (e.g., OnMouseDown, OnPointerClick for mobile touch).

## 3.     AI Assistant Layer (AgriBot):

A rules-based logic layer that delivers predefined chatbot responses. This component operates in response to user-selected questions and offers feedback based on in-game actions. The current version is static, but the architecture allows for future integration of dynamic AI using cloud services. It is integrated with Botpress, a third-party AI chatbot platform. Unity acts as the frontend for triggering and displaying responses.

4.     Data/Service Layer (optional in MVP):

While the MVP does not require persistent data storage, the architecture leaves room for optional components like local save systems, in-memory session data and cloud integration for analytics or student tracking.

5.     Deployment Layer:

The game is designed for two deployment modes:

- Mobile (Android): built using Unity’s Android build system

- WebGL: exportable as a browser game for demo and showcase purposes

Communication between layers is event-based and primarily one-directional from the UI to the logic scripts. Unity’s Inspector interface allows for quick modular linking between components without hardcoding dependencies. This allows individual team members to work on separate modules (e.g., UI, soil logic, chatbot) without interfering with each other’s workflows.

The component-based approach ensures that core gameplay elements such as crops, soil and tools can be created as prefabs with scripts that can be reused or extended in future versions.

This architecture style enables:

Easy expansion such as add more crops or levels.

Reusability of scripts and UI elements

Clear testing and debugging pathways

Lightweight performance suitable for mobile devices

Component Description

Frontend vs backend Separation

The frontend platform is the Unity game which will handle game visuals, buttons, interactions, player inputs, the chat UI (AgriBot panel), sending and receiving chat messages from Botpress and the local scoring and logic.

The backend platform is Botpress which will handle Ai conversation logic, decision trees or intents, message flow and dynamic replies and later on add curriculum-specific AI skills. The API used will be the Botpress Converse API.

The table contains the different components of the game and what they do:

Detailed Design

Module Description

Each module includes: Functionality, Inputs/Outputs, Rules, Data Elements.

Soil Preparation

Functionality: Clear soil via hoe/hand.

Input: Player tap + tool selection.

Output: Visual soil state change.

Rule: Soil must be cleared before planting.

Data: soilState, isCleared, score

Planting & Crop Growth Module

Functionality: Maize growth stages (plant → harvest).

Input: Tap cleared soil.

Output: Crop stage progression.

Rule: Only grows in cleared soil.

Data: cropStage, growthTimer

Harvest Module

• Functionality: Collect mature crops.

• Input: Tap harvestable crop.

• Output: Crop disappears, score increases.

• Rule: Must be ready stage to harvest.

• Data: isHarvestable, score, harvestCount

Animal Interaction Module

• Functionality: Feed domestic animal (chicken).

• Input: Tap chicken to feed.

• Output: Animation, score, feedback.

• Rule: Can only be fed once per session.

• Data: animalFed, animalName, feedCount, score

AgriBot Chatbot Module

• Functionality: Provides educational responses.

• Input: Tap chatbot buttons.

• Output: Displays fixed message.

• Rule: Static Q&A, no typing input.

• Data: questionList [], responseList [], selectedQuestionIndex

Score Manager Module

• Functionality: Tracks total score.

• Input: Triggered by other scripts.

• Output: Updates score UI.

• Rule: Each action = fixed points.

• Data: score, maxScore, eventTriggered

Interface Design

User Interface Mockups

Splash Screen

Home Screen

Planting flow

API Interface Specifications

Botpress API Integration (AgriBot Chat)

## 1. Converse with AgriBot

Endpoint: /api/v1/bots/agriquest/converse/{userId}

Method: POST

Request Body:

{

"type": "text",

"text": "How do I clear soil with a hoe?"

}

Response:

{

"responses": [

{

"type": "text",

"text": "You can use a hoe to clear weeds quickly before planting."

}

]

}

Status: 200 OK

API Interface Specifications (for Firebase Integration)

Database Design

Entity Relationship Diagram

Data Dictionary

Normalization Level:

The user entity is normalized to 3NF:

Each field is atomic.

No redundant groups or repeating columns.

All non-key attributes are functionally dependent on the primary key.

There are no transitive dependencies.

Exceptions (Firebase-optimized design):

farm State and chatHistory include arrays and nested structures, which:

Intentionally violate 1NF (non-atomic values)

Are optimized for flat, fast-access JSON in Firebase

Allow efficient single-document reads/writes

Data Flow & Control Flow

Plants Sequence Diagram

Plants Data Flow Diagram

Animal Flowchart Diagram

Animal Data Flow Diagram

State Diagram for a plant in AgriQuest

Let’s use a maize crop as an example.

The Crop Can Be in These States:

## 1. Empty Soil.

## 2. Planted.

## 3. Growing

4. Ready to Harvest.

5. Harvested.

Each state changes when a player does something (like clicking a button), or when enough time has passed.

Text-Based State Diagram: Crop

Here’s how it works:

🟫 Empty Soil

↓ (Player plants seed)

🌱 Planted

↓ (Player waters OR time passes)

🌿 Growing

↓ (After a few seconds)

🌽 Ready to Harvest

↓ (Player taps harvest)

🧺 Harvested

↓ (Resets)

🟫 Back to Empty Soil

Events That Cause Changes (Transitions)

Player taps “Plant” > moves from Empty Soil > Planted.

Timer runs or player waters > moves from Planted > Growing.

Timer ends > Growing > Ready to Harvest.

Player taps “Harvest” > becomes Harvested.

System resets tile > returns to Empty.

Non-Functional Design Considerations

These are things we considered that don’t directly affect how the game looks, but help make sure it works well, is easy to use, and can grow in the future and inclusive of more interactivity.

Performance Optimization (Make it run smoothly)

We want AgriQuest to run well, even on low-end phones and school computers.

What we’re doing:

Using small, light 3D models (so the game loads faster).

Keeping the textures simple.

Turning off heavy Unity features we don’t need.

Using mobile-friendly settings in Unity, but still learning its functionality.

Importance: So, the game doesn’t lag or crash, especially on older devices.

Security Design (Keep users safe)

Since we’re building a school learning game, we don’t want to risk students’ personal data.

What we’re doing:

The student’s data is safeguarded through PlayProtect offered by Google, this is due to the fact that students are downloading the game through Google Play, hence safeguarding their data.

Importance: To keep things safe for schools and students.

Scalability Plans (Make it easy to expand later)

We want AgriQuest to grow in the future, more crops, more levels, more topics and more relevance to the current Curriculum by supplementing classroom teaching and learning.

What we intend to do:

Breaking the game into individual pieces (soil, planting, chatbot), so we can add more without starting all over.

Keeping AgriBot simple now, still AI but ready to connect to real AI later (like ChatGPT or Azure).

Making the design flexible for Grades 4–9 or even beyond.

Importance: So, we can easily improve the game after the MVP is done.

Availability & Fault Tolerance (Make it reliable and accessible)

We want learners to always be able to use the game regardless of the internet.

What we’re doing:

The whole game works offline (no need for Wi-Fi or data) and offline.

We plan to support three versions:

Android.

Web (WebGL for projectors/laptops).

iOS.

If the player makes a mistake, they get helpful feedback, not a crash.

Importance: So, it’s always available, even in schools with poor network access.

Usability & Accessibility Design (Make it easy and fair for all users)

We want all students to understand how to play, even younger ones or those with visual or reading challenges.

What we’re working on:

Using big buttons and large fonts.

Clear colors to show progress (e.g. green = growing, brown = cleared soil).

Simple, CBC-level messages.

Touch-based only (no keyboard).

Planning to add sound cues/ effects.

Importance: To make the game friendly and inclusive for every learner.

Deployment and Infrastructure

Platform

Our AgriQuest AI game will be primarily deployed on:

Android mobile devices via Unity's Android build system to allow wide access among learners with smartphones.

WebGL build hosted on a website for easy browser-based demos and testing, enabling access without installation.

The dual-platform approach ensures flexibility and accessibility for users with different devices and connectivity.

Version Control and Collaboration

The project codebase and assets will be stored and managed in GitHub.

Each team member will work on individual feature branches (e.g., prudence-mvp, mercy-ai, Roy-ml) to avoid conflicts and enable smooth integration.

Pull Requests (PRs) will be created for merging to the main branches after peer review.

Deployment Tools

Unity Editor for local builds and testing.

GitHub for source control and collaboration.

Netlify or GitHub Pages for hosting the WebGL version of the game.

Android Studio / Unity for packaging APKs for installation on Android devices.

Environments

## DEPLOYMENT ARCHITECTURE FLOWCHART

Push &pull code

## CI/ CD

Build Apk/ WebGL                                              Host WebGL

Testing Design

Testing Types

Test Data and Scenarios

Sample Crop Growth: Plant a seed, simulate growth stages, harvest, and verify score increments.

Soil Preparation: Confirm that soil can be cleared only when weeds are present.

AgriBot Responses: Check chatbot provides correct responses for selected questions.

Performance: Measure frame rates on typical mobile devices to ensure smooth gameplay.

Bug Tracking and Issue Management

Issues and bugs will be logged using GitHub Issues with labels such as bug, enhancement, and question.

Team members will assign issues to themselves or others and use milestones aligned with sprint schedules.

## TESTING FLOWCHART

Start testing

Feedback loop

Bugfixes

Improvements

New test cases

## RISKS AND MITIGATION PLANS

Appendices

GitHub Repository

URL: https://github.com/yourusername/AgriQuest-AI

Structure Highlights:

bash

CopyEdit

/Assets/Scripts/       # Unity C# scripts for gameplay logic

/Assets/Prefabs/       # Game objects and UI prefabs

/docs/                 # Project documentation including SDD, plans

/Ai-chatbot/           # Chatbot scripts and response data

/Mvp-plan/             # Sprint and MVP planning documents

Team Roles Document

Lists each member’s responsibilities, e.g.,

Prudence: Project lead and game developer

Mercy: Machine learning and AI chatbot integration

Roy: AI chatbot and machine learning integration

Kerry: Game design, animations, and 3D assets

Adrian: UI/UX designer

MVP Plan and Schedule

Contains the 8-week sprint plan, detailing which features will be implemented and tested each week.

AgriBot Chatbot Responses

A text file listing questions and answers for the static chatbot, aligned with CBC topics.

Unity Scripts Reference

A document or folder outlining key scripts, their responsibilities, and their interconnections.