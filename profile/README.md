# Getting Started

### Repositories:
- [Skylab Frontend](https://github.com/orbital-skylab/skylab-frontend)
- [Skylab Backend](https://github.com/orbital-skylab/skylab-backend)

### Important Reads:
- [Git Workflow](https://github.com/orbital-skylab/skylab-frontend/wiki/Git-Workflow)
- [Issue Tracking](https://github.com/orbital-skylab/skylab-frontend/wiki/Issue-Tracking)
- [Style Guide](https://github.com/orbital-skylab/skylab-frontend/wiki/Style-Guide)
- [Code Review Rubrics](https://github.com/orbital-skylab/skylab-frontend/wiki/Code-Review-Rubrics)
- [Contribution Guide](https://github.com/orbital-skylab/.github/blob/main/CONTRIBUTING.md)

## Prerequisites
1. [LTS/Fermium version of node.js](https://nodejs.org/download/release/latest-fermium/)
2. [Postgresql version 14.X](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads)

## Initial Setup for Local Development
1. Open your terminal, clone the frontend repository into a directory of your choice and install dependencies.
    - `cd <path to directory of choice>`
    - `git clone https://github.com/orbital-skylab/skylab-frontend`
    - `cd skylab-frontend`
    - `npm install`
2. Create a new `.env.local` file in the project root and add the following contents into it:
    ```
    NEXT_PUBLIC_BASE_DEV_API_URL=http://localhost:4000/api
    ```
3. Run the frontend development server with the command `npm run dev`. It can be accessed at `localhost:3000`.
4. Open another terminal instance and connect to psql as the postgres super user via the command `psql -U postgres` and key in your postgres super user password if applicable.
5. Create two new databases for skylab development.
    -  `CREATE DATABASE skylab;`
    -  `CREATE DATABASE skylab_shadow;`
6. Open another terminal instance, clone the backend repository into a directory of your choice and install dependencies.
    - `cd <path to directory of choice>`
    - `git clone https://github.com/orbital-skylab/skylab-backend`
    - `cd skylab-backend`
    - `npm install`
7. Create a new `.env.local` file in the project root and add the following contents into it:
    ```
    DATABASE_URL=postgresql://postgres:<your_postgres_super_user_password>@localhost:5432/skylab
    SHADOW_DATABASE_URL=postgresql://postgres:<your_postgres_super_user_password>@localhost:5432/skylab_shadow
    
    ```
    - If your postgres super user account is not password protected, use `...postgres@localhost...` instead.
    - You can also use a different user apart from the postgres super user, just ensure that this user has all permissions for the `skylab` and `skylab_shadow` databases.
8. Run a migration to create the necessary tables in the development databases.
    - `npx prisma generate`
    - `npx prisma migrate dev`
9. Run the backend development server with the command `npm run dev`. It can be accessed at `localhost:4000`.

## Directly Interacting with Database

After migration is compelted, there are two ways to directly view and interact with data in the skylab database

### PSQL
1. Connect to psql as the postgres super user via the command `psql -U postgres` and key in your postgres super user password if applicable.
2. Connect to the development database via the command `\c skylab`

### Prisma Studio
1. Boot up prisma studio via the command `npx prisma studio`
2. By default, prisma studio can then be accessed at `localhost:5555`

## Deployment on SoC VM

The front and back end of Skylab V2 are deployed and running on SoC VM. When changes are made to either repository, the corresponding applications on the VM will need to be restarted.

Please contact prof for the hostname and password of the VM, then ssh into it via `ssh <hostname>` and key in the password.

Both applications are hosted via [pm2](https://pm2.keymetrics.io/). The frontend application is named `skylab-frontend` and the backend application is named `skylab-frontend`.

`skylab-frontend` is a standard [Next.js](https://nextjs.org/) application.

`skylab-backend` is an [Express.js](https://expressjs.com/) server supported by [Prisma ORM](https://www.prisma.io/).
- A local instance of psql running on port 5432 is being used to host the database for Prisma.
- The database can be managed directly by connecting to psql by simply using the `sudo -u postgres psql`, then, connecting to the production database via the command `\c skylab`.
    - You can also connect to psql with our skylab super user, more information can be found in the `.env` file in the `skylab-backend` repository.
- There is also a development database and shadow development database called `skykab_dev` and `skylab_dev_shadow` respectively, which can be used if necessary. The development database should contain mock data seeded via [faker.js](https://fakerjs.dev/).

### Frontend

1. `cd Desktop/skylab-frontend` to move to the frontend repository
2. `git pull` to update the repository with the latest changes
3. `npm install` to update dependencies
4. `npm run build` to rebuild the static files for production
5. `pm2 restart skylab-frontend` to restart the frontend on production

### Backend

1. `cd Desktop/skylab-backend` to move to the backend repository
2. `git pull` to update the repository with the latest changes
3. `npm install` to update dependencies
4. `npm run build` to rebuild the static files for production
5. `pm2 restart skylab-backend` to restart the backend on production

### Other useful information

- The frontend and backend applications were started using the following steps
    - Frontend
        - ssh into VM
        - `cd Desktop/skylab-frontend`
        - `npm run build`
        - `pm2 start npm --name skylab-frontend -- run start`
    - Backend
        - ssh into VM
        - `cd Desktop/skylab-backend`
        - `npm run build`
        - `pm2 start npm --name skylab-backend -- run start`
- The applications can be stopped/reloaded or even deleted via `pm2 <stop/reload/delete> <skylab-frontend/skylab-backend>`
    - eg; `pm2 reload skylab-backend` to reload the backend application
- The status of both applications can be monitored via `pm2 monit`

## Glossary

|Term|What It Refers To|
|-|-|
|Cohort|The Orbital program runs once per academic year, during the summmer break from May to August. Each run is referred to as a cohort.|
|User|Someone who is able to sign in to the Skylab platform with their email and password.|
|Role|Student, Adviser, Mentor or Administrator. The role a user has during a particular cohort will determine what pages they can access and what actions they can carry out in that time period. For example, a particular user could be a student in the 2020 cohort then an adviser in the 2021 cohort.|
|Team|Groups of students (typically 2 students per team).|
|Project|Refers to the software project undertaken by a team for Orbital|
|Milestone|A checkpoint for students to submit their preliminary work and documentation. Evaluations also happen after each milestone. There are typically 5 milestones per Orbital cohort (Liftoff, Milestone 1, Milestone 2, Milestone 3 and Splashdown).|
|Deadline|A general term for set of questions that requires a submission by a specified due date.|
|Submission|A general term for a set of answers to a deadline.|
|Evaluation|A specific type of deadline where teams and advisers review other teams' projects. **Note:** evaluations are team-level submissions, not individual, so only 1 student from each team is required to submit each evaluation.|
|Evaluation Relationship|A unidirectional relationship which determines who evaluates what. For example, there could be an evaluation relationship whereby Team A evaluates Team B's project, but it is not necessary for there to also be an evaluation relationship whereby Team B evaluates Team A's project. Typically, Artemis teams will be assigned more projects to review.|


