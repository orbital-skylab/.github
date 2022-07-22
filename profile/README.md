# Getting Started

### Repositories:
- [Skylab Frontend](https://github.com/orbital-skylab/skylab-frontend)
- [Skylab Backend](https://github.com/orbital-skylab/skylab-backend)

### Important Reads:
- [Git Workflow](https://github.com/orbital-skylab/skylab-frontend/wiki/Git-Workflow)
- [Issue Tracking](https://github.com/orbital-skylab/skylab-frontend/wiki/Issue-Tracking)

## Initial Setup
1. Install the [LTS/Fermium version of node.js](https://nodejs.org/download/release/latest-fermium/) on your computer.
2. Open your terminal, clone the frontend repository into a directory of your choice and install dependencies.
    - `cd <path to directory of choice>`
    - `git clone https://github.com/orbital-skylab/skylab-frontend`
    - `cd skylab-frontend`
    - `npm install`
3. Create a new `.env.local` file in the project root and add the following contents into it:
    ```
    NEXT_PUBLIC_BASE_DEV_API_URL=http://localhost:4000/api
    ```
5. Run the frontend development server with the command `npm run dev`. It can be accessed at `localhost:3000`.
6. Open another terminal instance, clone the backend repository into a directory of your choice and install dependencies.
    - `cd <path to directory of choice>`
    - `git clone https://github.com/orbital-skylab/skylab-backend`
    - `cd skylab-backend`
    - `npm install`
7. Create a new `.env.local` file in the project root and add the following contents into it:
    ```
    DATABASE_URL=<contact the developers for the API key>
    SHADOW_DATABASE_URL=<contact the developers for the API key>
    ```
8. Run the backend development server with the command `npm run dev`. It can be accessed at `localhost:4000`.

## Glossary

|Term|What It Refers To|
|-|-|
|Cohort|The Orbital program runs once per academic year, from May to Auguest. Each run is referred to as a cohort.|
|User|Someone who is able to sign in to the Skylab platform with their email and password. Users can have up to one role per cohort.|
|Role|Student, Adviser, Mentor or Administrator. The role a user has during a particular cohort will determine what pages they can access and what actions they can carry out in that time period. For example, a particular user could be a student in the 2020 cohort then an adviser in the 2021 cohort.|
|Team|All orbitees are split into teams, which are groups of students (typically 2 students per team).|
|Project|Refers to the software project undertaken by a team for Orbital|
|Milestone|A checkpoint for students to submit their preliminary work and documentation. Evaluations also happen after each milestone. There are typically 5 milestones per Orbital cohort (Liftoff, Milestone 1, Milestone 2, Milestone 3 and Splashdown).|
|Deadline|A general term for set of questions that requires a submission by a specified due date.|
|Submission|A general term for a set of answers to a deadline.|
|Evaluation|A specific type of deadline where teams and advisers review other teams' projects. **Note:** evaluations are team-level submissions, not individual, so only 1 student from each team is required to submit each evaluation.|
|Evaluation Relationship|A unidirectional relationship which determine who evaluates what. For example, there could be an evaluation relationship whereby Team A evaluates Team B's project, but it is not necessary for there to also be an evaluation relationship whereby Team B evaluates Team A's project. Typically, Artemis teams will be assigned more projects to review.|


