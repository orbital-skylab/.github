# Getting Started

### Tech stack and platforms:

###### Frontend
- [Next.js](https://nextjs.org/)
- [Material UI](https://mui.com/)

###### Backend
- [Express](https://expressjs.com/)
- [Prisma with Postgresql](https://www.prisma.io/) 

###### Testing
- [Jest](https://jestjs.io/)
- [Cypress](https://www.cypress.io/)
- [Faker.js](https://fakerjs.dev/)

###### Deployment
- [Nginx](https://www.nginx.com/)
- [Pm2](https://pm2.keymetrics.io/)

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
1. Install [Node.js (version LTS Fermium)](https://nodejs.org/download/)
2. Install [Postgresql (version 14)](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads)
3. Install [Postman Desktop App](https://www.postman.com/)

## Initial Setup for Local Development

### Frontend

#### 1. Clone Git Repository

Open your terminal and clone the frontend repository into a directory of your choice.

```
cd <path to directory of choice>
git clone https://github.com/orbital-skylab/skylab-frontend
```

#### 2. Install Dependencies

Ensure that you have installed and are using the **LTS Fermium** version of Node.js. If you have a different version of Node.js installed, you can make use of nvm for [Windows](https://github.com/coreybutler/nvm-windows) or [macOS/unix/WSL](https://github.com/nvm-sh/nvm) to change it to LTS Fermium.

```
cd skylab-frontend
npm install
```

#### 3. Set up .env.local File

We have a `.env.local` file in the root of the `skylab frontend` repository to contain project secrets. If you wish to add more secrets, ensure to prefix the name of the secret variable with `NEXT_PUBLIC_` for it to be exposed to the browser as described [here](https://nextjs.org/docs/basic-features/environment-variables).

```
touch .env.local
echo NEXT_PUBLIC_BASE_DEV_API_URL="http://localhost:4000/api" >> .env.local
```

### Postgres Database

#### 1. Install psql

The download archive for psql version 14.X can be found [here](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads).

pgAdmin, which is a GUI for Postgresql, will not be necessary but you can choose to install it if you want to use it.

If you are using **Windows**, you can follow [this](https://www.enterprisedb.com/docs/supported-open-source/postgresql/installer/02_installing_postgresql_with_the_graphical_installation_wizard/01_invoking_the_graphical_installer/) installation guide. Otherwise, the installation should be straightforward for other platforms.

#### 2. **(Windows)** Add psql to PATH

In order to find out where psql was installed on your computer, you can open **command prompt** and key in `where psql`. This command will print out the path to your installed psql, which should by default look similar to this:
```
C:\Program Files\PostgreSQL\14\bin\psql.exe
```

Copy this address **excluding** `\psql.exe`. In other words, copy the address of the bin folder. For the above example, this is what should be copied:

```
C:\Program Files\PostgreSQL\14\bin
```

Next, use the shortcut `Windows Key` + `s` to bring up the Windows search menu, then key in the word **system**

You should see the option to `Edit the system environmental variables` under **Control Panel** pop up in the search results. Click on it to bring up the **System Properties** menu.

![Search](/profile/images/search.jpg)

At the bottom of this menu, you should see an `Environmental Variables...` button. Click on it to bring up the **Environmental Variables** menu.

![System Properties](/profile/images/system_properties.jpg)

In the bottom half of this menu, under **System Variables**, Select `Path` then click on the `Edit...` button below it to bring up the **Edit Environmental Variable** menu.

![PATH](/profile/images/system_variables.jpg)

Click on the `New` button at the top right of this menu then paste the **address to the psql bin folder** that we copied earlier into the new input highlighted in blue.

![Add](/profile/images/new.jpg)

Once completed, click on the `OK` button at the bottom of this menu, then restart your terminal and/or code editor for the change to the system environmental variables to take effect. If the changes are still not recognized, you can restart your computer.

#### 3. Connect to psql

Postgresql comes with a default super user named `postgres`. We will be connecting to the psql interactive terminal using this super user.

**macOS**:

_macOS does not require password authentication for the default `postgres` super user_.
```
sudo -u postgres psql // sudo -u <username> psql
```

**Windows**: 

_You will be prompted to enter the password for `postgres` which you would have set up during installation_.
```
psql -U postgres // psql -U <username>
```

#### 2. Create Development Databases

We will be creating and using a new database for development. By default we set the name of the database to be `skylab`, but you can name it anything that you want.

If you do rename the database, ensure to update the environment variables for the backend application (which we will be setting up later on)  accordingly.

```
CREATE DATABASE skylab;
```

#### 3. (Optional) Create New Super User

You can create your own super user to use in place of the default `postgres` super user.

```
CREATE USER <your_super_user_username> WITH SUPERUSER PASSWORD '<your_super_user_password>';
```

#### 4. Exit psql

If there is nothing else for you to do within psql, you can shut down the psql interactive terminal.

````
\q
````

### Backend

#### 1. Clone the Repository

Open your terminal and clone the backend repository into a directory of your choice.

```
cd <path to directory of choice>
git clone https://github.com/orbital-skylab/skylab-backend
```

#### 2. Install Dependencies

Ensure that you have installed and are using the **LTS Fermium** version of Node.js. If you have a different version of Node.js installed, you can make use of nvm for [Windows](https://github.com/coreybutler/nvm-windows) or [macOS/unix/WSL](https://github.com/nvm-sh/nvm) to change it to LTS Fermium.

```
cd skylab-backend
npm install
```

#### 3. Set up .env File

We have a `.env` file in the root of the `skylab backend` repository to contain project secrets. Ensure to replace all the values encapsulated in angle brackets: `<replace_these_values>`.

```
touch .env
echo DATABASE_URL="postgresql://postgres:<your_postgres_super_user_password>@localhost:5432/skylab" >> .env 
echo JWT_SECRET="<any_value>" >> .env
echo ADMIN_PASSWORD="<your_chosen_password>" >> .env
echo SALT_ROUNDS=<any_number> >> .env
```

The format of the `DATABASE_URL` is `postgresql://<username>:<password>@<domain>:<port>/<database_name>`. 

You can make use of another postgres user if you choose to do so in place of the `postgres` super user. The default port used by psql is `5432`. If you chose a different name instead of `skylab` for your development database, ensure to update the database name in `DATABASE_URL`.

If your postgres super user account is not password protected, use `...postgres@localhost...` instead of `...postgres:<password>@localhost...`.

`JWT_SECRET` is used for user authentication and authorization via JSON web tokens. For development, this secret can take any value. We recommend a 32-digit random hex number which you can generate [here](https://www.browserling.com/tools/random-hex). These tokens are cryptographically signed and contain verifiable user information in a standard format which we use to verify the identity of an entity making a request to the server. Unauthenticated and unauthorized users will be rejected with HTTP error `401` or `403` respectively.

#### 4. Run Migration

Run a migration to create the necessary tables in the development database.

```
npx prisma generate
npx prisma migrate dev
```

The database can also be reset at any time if you run into any issues/
```
npx prisma migrate reset
```

More information about migration with Prisma ORM can be found [here](https://www.prisma.io/docs/concepts/components/prisma-migrate)

## Seeding Mock Data

Mock data can be seeded directly using the command `npx prisma db seed`. You can change the data that is seeded if you wish to do so by altering the files in `prisma/seed`

## Booting up the Development Environment

Open two different terminals to start up the frontend and backend applications.

```
cd <path_to_skylab_frontend>
npm run dev

cd <path_to_skylab_backend>
npm run dev
```

The frontend application can be accessed at `localhost:3000` while the backend application can be accessed at `localhost:4000`.

## Testing API with Postman

The [Postman Desktop App](https://www.postman.com/) can be used to test backend routes

You can create a new **personal workspace** to contain all your requests to test for Skylab V2 by clicking on the `Create Workspace` button in the Postman Desktop App menu.

![Menu](/profile/images/menu.jpg)

![Create Workspace](/profile/images/create_workspace.jpg)

You can then create a new **environment** for local development. You can name the environment anything that you like. In this example, we call it `Localhost`

![Environments](/profile/images/environment.jpg)

In this new environment, you can add an environmental variable for the URL of the Skylab V2 api. In this example, we call this environmental variable `api_url`.

![Environmental Variable](/profile/images/environmental_variable.jpg)

Ensure to save this new environment and variable with the shortcut `Ctrl` + `s`**(Windows)** or `cmd` + `s`**(macOS)**

Now we can move on to creating test requests. Postman allows us to create **collections**, which are essentially groups of requests. 

We will be trying our two requests in this example. The first request is to seed mock data for our development database. The second request that we will want to test is the login request because this will embed the response with a verified **HTTP only cookie**, making our future requests authenticated. You can read more about our method of authentication [here]()**[Work in Progresss]**

Let's first create a new collection to contain the login request. For this example, we will call the new collection `Auth`

![New Collection](/profile/images/new_collection.jpg)

We will then add the login request. The request body can be added by selecting the `Body` tab below the address bar, clicking on the `raw` radio button and then selecting the `JSON` option in the type selector on the right. Note that in Postman, JSON object keys **must be strings**.

![New Collection](/profile/images/auth_request.jpg)

**Note:** Postman requests can only be authenticated by our backend server if it is run in development environment (`npm run dev`). This is because in development environment, our cookies are **not** secure, which is necessary for usage with Postman. The routes which require authentication are specified in our [Backend Wiki](https://github.com/orbital-skylab/skylab-backend/wiki).

You can use the above-mentioned steps to create more collections and requests for your testing needs. 

## Using Admin Account

After seeding the mock data, an admin account with the following credentials will be available for you to use.

```
email: admin@skylab.com
password: Password123
```
In the frontend application, you can log in using these credentials.

If you wish to create another admin account, you will need to make a `POST` request while the backend application is running as outlined [here](https://github.com/orbital-skylab/skylab-backend/wiki/Administrators-Endpoints#create-a-new-account-with-administrator-role).

## Directly Interacting with Database

After migration is compelted, there are two ways to directly view and interact with data in the skylab database.

### PSQL
1. Connect to psql as the postgres super user via the command `psql -U postgres`**(Windows)** or `sudo -u postgres psql`**(macOS)** and key in your postgres super user password if applicable.
2. Connect to the development database via the command `\c skylab`
3. Shut down psql after you are done via the command `\q`

### Prisma Studio
1. Boot up prisma studio via the command `npx prisma studio`
2. By default, prisma studio can then be accessed at `localhost:5555`

## How Authentication and Authorization Work

We make use of [JSON Web Tokens](https://jwt.io/) and [HTTP cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies) for authentication and authorization in Skylab V2.

The Skylab API is very extensive and there are some requests which require authentication or authorization. Authentication means that the host sending the request but be logged into the platform. Authorization means that the host sending the request must have a specific identity or role, depending on the authorization middleware that is securing that particular route.

When users log in to the platform, the server will first verify the user's credentials. If verification is successful, a new JSON web token is generated with the user's account information (excluding password) as the signed payload. This token is then stored in a secure HTTP cookie which is sent back to the client in the login response. 
This token will persist in the user's browser and be used to authenticate future requests. 

As for authorization, there are several levels of permissions in Skylab V2 as mentioned earlier. These can be seen [here](https://github.com/orbital-skylab/skylab-backend/tree/staging/src/middleware). The gist of authorization is that the payload (containing account information) of the JSON web token in the HTTP cookie embedded in the request will be decrypted and verified against the permissions required for the route. The authorization required for each route is detailed in our [Backend Wiki Endpoints Documentation](https://github.com/orbital-skylab/skylab-backend/wiki)


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
3. `npm ci` to update dependencies with lockfile frozen
4. `npm run build` to rebuild the static files for production
5. `pm2 restart skylab-frontend` to restart the frontend on production

### Backend

1. `cd Desktop/skylab-backend` to move to the backend repository
2. `git pull` to update the repository with the latest changes
3. `npm ci` to update dependencies with lockfile frozen
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
