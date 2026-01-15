# Company of Agents

This repo contains a company of agents that can work together to achieve a common goal.

## The Flow

The general flow for feature development involves a sequential interaction between the User, the Product Manager (PM), the Engineering Manager (EM) and the Developer (Dev).

### 1. Product Definition (PM Agent)
**Role:** Product Manager
**Goal:** Transform ideas into clear specifications.

1.  **Interaction**: The user talks to the PM to discuss requirements, features, and user needs.
2.  **Creation**: The PM helps brainstorm and refine ideas.
3.  **Output**: The PM creates detailed **User Stories** and **PRDs** (Product Requirement Documents).
    *   Location: `./docs/sprint-<sprint-no>/prds/`

### 2. Technical Planning (EM Agent)
**Role:** Engineering Manager
**Goal:** Translate specifications into execution-ready tasks.

1.  **Input**: The EM reads the PRDs created by the PM.
2.  **Analysis**: The EM analyzes the codebase and the requirements to understand technical implementation details.
3.  **Output**: The EM creates specific **Development Tasks** for Frontend and Backend.
    *   Location: `./docs/sprint-<sprint-no>/dev-tasks/`

### 3. Development (Developer Agent)
**Role:** Developer
**Goal:** Implement the development tasks created by the EM.

1.  **Input**: The developer reads the development tasks created by the EM.
2.  **Implementation**: The developer implements the development tasks.
3.  **Output**: The developer creates the code for Frontend and Backend.
    *   Location: `./frontend/` and `./backend/`
