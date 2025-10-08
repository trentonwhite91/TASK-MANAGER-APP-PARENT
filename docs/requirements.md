# Software Requirements Specification (SRS)

## 1. Introduction

### 1.1 Purpose
The purpose of this document is to ensure that all stakeholders have a clear and shared understanding of the Task Manager system's expected behavior by defining the functional and non-functional requirements.

### 1.2 Scope
This system will allow small distributed teams (1–15 people) to create, assign, and track tasks. It will support real-time synchronization and AI-powered workload balancing suggestions

### 1.3 Definitions, Acronyms, Abbreviations
- CRUD: Create, Read, Update, Delete
- AI Recommendation Engine: Module that suggests optimal task assignments
- JWT: JSON Web Token

### 1.4 References
- Vision Document (VISION.md)

## 2. Overall Description

### 2.1 Product Perspective
The system is a standalone web and mobile PWA (Progressive Web App) with a Spring Boot backend, PostgreSQL database, and AI microservice.

### 2.2 Product Functions
- Create, assign, and update tasks
- Real-time collaboration with sync across devices
- AI recommendations for task assignment and prioritization

### 2.3 User Classes and Characteristics
- Team Lead: Assign tasks, view workload, manage project settings
- Team Member: Create, view, and update tasks
- Admin: Administrator of the system

### 2.4 Operating Environment
- Web browser (Chrome, Edge, Firefox, Safari)
- Mobile devices (iOS/Android via PWA)
- Backend server (Spring Boot on cloud, PostgreSQL database)

### 2.5 Constraints
- Must support at least 15 concurrent users per team
- AI recommendations must complete within 2 seconds

## 3. Functional Requirements 

- FR1: The system shall allow users to create, edit, and delete tasks
- FR2: The syswtem shall allow users to create, edit, and delete projects
- FR3: The system shall support assigning tasks to team members
- FR4: The system shall allow team members to update task status (To Do, In Progress, Done)
- FR5: The system shall provide AI-based priority prediction
- FR6: The system shall allow team members to view overall team progress in a dashboard
- FR7: The system shall allow team leads to add team members to a project
- FR8: The system shall only allow users who are a part of a project to view or edit tasks which are a part of that project

## 4. Non-Functional Requirements

- NFR1 (Performance): The system shall support at least 100 tasks per user with no noticeable lag.
- NFR2 (Availability): The system shall be available 99.5% of the time.
- NFR3 (Security): All data shall be encrypted in transit (TLS) and at rest.
- NFR4 (Usability): New users shall be able to complete core tasks within 5 minutes of onboarding.
- NFR5 (Portability): The system shall run as a PWA across modern browsers and mobile devices.

## 5. Acceptance Criteria

- AI recommendations appear in under 2 seconds and improve workload balance.
- Usability test participants rate onboarding ≥ 8/10.

## 6. Future Enhancements

- Integration with Slack or Teams for notifications
- Advanced analytics dashboards
- Role-based access control
