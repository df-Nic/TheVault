---
title: Project Notes
Date Created: 2025-08-21
Last Updated: 2025-09-28
tags:
  - CS3219
---
# Project Description
---
**Topic**: Peer collaboration & communication for technical interview

**Background**: A user who is keen to prepare for their technical interviews **visits the PeerPrep site**. They **create an account and then log** in After logging in, the user selects the question **difficulty level ( medium, or hard) and a topic** they want to attempt today The user then waits until they are **matched with another online user** who has selected the same difficulty level and topic choice as them **If they are not successfully matched after a specific duration, they time out**. If they are successfully matched, the users are **provided with an appropriate question and a collaborative space to develop their solution in real time**. The application should allow the users to **terminate the collaborative session gracefully**.

>[!important] This project strongly recommends following the microservice atchitecture
# Features
---
## Critical Features

1) A service for users to manage their profile
	- Authentication Feature
	- 2FA
	- Email verification
	- Reset Password
	- Change profile picture (*Extra*)

2) Service matching
	- Match 2 users in the queue based on criteria's like question difficulty or topic
	- Timeout if cannot find within a set threshold

3) Question Service
	- Maintain a question bank with indexed based on certain factors (*difficulty, topic*)
	- Support images
	- Community base question collaboration

4) Collaboration services
	- Real time communication
	- Real time code editing
	- Real time video sharing

5) GUI for application

6) Deployment
	- Containers
	- Kubernetes
## Nice to have Features

1) Service enhancement
	- Enhanced code editor
	- Code translation*
	- Improved communication tools
	- Question attempt history
	- Code execution

2) AI features
	- AI assisted explanations
	- AI assisted problem solving
	- Conceptual expansion
	- Open ended innovation

3) Integration, testing, and deployment
	- Automated tests
	- Coverage target
	- Cross browser/app testing
	- Non functional tests
	- CI/CD
	- Infrastructure as code

# Deadlines
---

|             Description              |       Marks       |                            Due                             |                              Remarks                               |
| :----------------------------------: | :---------------: | :--------------------------------------------------------: | :----------------------------------------------------------------: |
|      Requirement Specification       |         5         |               End of week 5, **Sep 12 2025**               | Product backlog for critical features 1 - 4<br>Refined to 2 levels |
|            Progress Check            | 5 checks * 4 = 20 |              End of week 11, **Oct 24, 2025**              |             Design Decisions<br>There will be 5 checks             |
| Project Demonstration & Presentation |        25         | End of **week 13**<br>Slides submission on **Nov 13 2025** |                     30 Min Demo + Presentation                     |
# To Do List
---
- [x] Figure out what features we need
- [ ] What will be our front end
- [ ] What will be our back end + tech stack

# Tech Stack
---
## Front End

Frameworks:
- React + Next.js
- Angular
- Vue.js + Nuxt

UI Library (*depends on which framework we are using*):
- PrimeNG (*Angular*)
- Ng-Zorro (*Angular*)
- MUI (*React*)
- Material UI (*React*)
- PrimeVue (*Vue*)
- Vuetify (*Vue*)
- Naive UI (*Vue*)
## Backend