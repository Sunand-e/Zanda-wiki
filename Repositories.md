The LMS code is currently managed across two primary repositories, each serving a distinct purpose in the system. Below are details about each repository and their roles:

LMS API Repository
---
https://github.com/eLearning-Plus/MemberHub/

This repository contains the backend code for the LMS, built with Ruby on Rails. It is the core of the platform, managing essential functionalities such as user authentication, course management, and API endpoints. Previously referred to as "Memberhub", the name of this repository should be changed if possible as we no longer refer to the platform by this name. A suggestion: "Learning Platform API"? (It's not just an API...)

Key components include:

API Code: Implements the business logic and handles server-side operations.

Local Docker Setup: Includes configuration files and scripts (Dockerfile, docker-compose.yml, etc.) to streamline local development and testing.

### Branching
The core branching setup is relatively straightforward:

**main** - this is the branch containing the latest 'stable' version of the codebase

**production** - anything pushed to this branch will trigger the CI/CD workflow for deploying to the production environment.

**staging** - anything pushed to this branch will trigger the CI/CD workflow for deploying to the staging environment.

All other branches in the repo are either stale, or contain unfinished features. These branches can either be discarded, or kept for aiding in future developments relating to the branch names.

LMS Frontend Repository
---
https://github.com/eLearning-Plus/learning-platform-frontend/

This repository houses the frontend code for the LMS, responsible for delivering the user interface and experience. It includes:

#### **Key Features**

-   **Next.js for Page Routing and Static Exports:** Next.js is used to handle client-side routing and generate static exports during the CI/CD pipeline. This ensures the frontend is optimized for performance, with fast loading times and efficient content delivery, without relying on a server-rendered setup.
-   **Apollo Client for GraphQL Communication:** The frontend uses Apollo Client for efficient GraphQL query and mutation handling. It manages communication with the backend LMS API while leveraging caching mechanisms to minimize redundant network requests and improve data retrieval efficiency.
-   **State Management with Zustand:** Zustand is employed alongside Apollo Client for managing local state and handling UI-related logic that isn't directly tied to the API, offering lightweight and performant state management.
-   **React-based Responsive UI:** Built with React, the frontend delivers a clean, intuitive, and responsive interface that adapts seamlessly to various devices and screen sizes.
-   **Integration with LMS API:** The frontend interacts with the backend LMS API to dynamically fetch, display, and manipulate data, ensuring a smooth user experience and accurate data synchronization.
-   **Custom Design and Components:** Includes reusable design components and styling assets that define the LMS's visual identity and user interactions.

#### **Notes**

-   **Static Export Workflow:** During the CI/CD pipeline, Next.js generates a fully static version of the site, optimizing it for deployment to a static hosting environment. This approach eliminates the need for server-side rendering in production, ensuring scalability and simplified infrastructure.
-   **Apollo and Zustand Usage:** Apollo Client manages API-related state, while Zustand is used for lightweight, standalone state management needs like UI controls or session data.
