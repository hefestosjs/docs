# HefestosJS Docs

Welcome! HefestosJS is an MVC solution to develop your web application more easily and quickly. With a focus on productivity, HefestosJS is already configured for authentication using jwt tokens or sessions, sending emails, periodic tasks and jobs, uploading files to local driver or AWS S3 and much more.

## Summary

- [HefestosJS Docs](#hefestosjs-docs)
  - [Installation](#installation)
  - [Commands](#commands)
  - [Env](#env)
  - [Routes](#routes)
  - [Database](#database)
  - [Upload and Middlewares](#upload-and-middlewares)
  - [Layouts, views and partials](#layouts-views-and-partials)
  - [Validation](#validation)
  - [Tests](#tests)
  - [Tasks and Jobs](#tasks-and-jobs)
  - [Authentication](#authentication)
  - [Mailer](#mailer)
  - [References](#references)

## Installation

You can create a new project using the command:

```
npx hefestos-forge hello-world
```

## Commands

- `build` - delete the current dist folder (if exists), copy the resources files (views, partials, layouts) and transpile the typescript to the dist folder.

- `start` - starts the server in production environment.

- `dev` - starts the server in development environment, monitoring the code and tailwind changes.

- `test` - starts the tests

- `test:watch` - starts the tests while monitoring the changes.

- `coverage` - starts the coverage tests.

- `g` - used to generate files, like controllers, services, views, validations and more.

- `studio` - starts the prisma studio.

- `seed` - Populate your database with your data.

## Env

Create a .env file from .env.example and fill in the environment variables you will use.

```
# Application
PORT = 3000
NODE_ENV=development
SESSION_SECRET=<YOUR_SESSION_SECRET>
COOKIE_SECRET=<YOUR_COOKIE_SECRET>
LOG_ACTIVE=true
DRIVE_DISK=local

# Database
DB_USER=<YOUR_DB_USER>
DB_PASS=<YOUR_DB_PASS>
DB_PORT=<YOUR_DB_PORT>
DB_NAME=<YOUR_DB_NAME>
DB_HOST=<YOUR_DB_HOST>

DB_URL=postgresql://${DB_USER}:${DB_PASS}@${DB_HOST}:${DB_PORT}/${DB_NAME}

# Mailer
SMTP_HOST=<YOUR_SMTP_HOST>
SMTP_PORT=<YOUR_SMTP_PORT>
SMTP_USER=<YOUR_SMTP_USER>
SMTP_PASSWORD=<YOUR_SMTP_PASSWORD>
SMTP_SECURE=<IF_SHOULD_USE_SSL>

# Amazon S3
S3_KEY=<YOUR_S3_KEY>
S3_SECRET=<YOUR_S3_SECRET>
S3_BUCKET=<YOUR_S3_BUCKET>
S3_REGION=<YOUR_S3_REGION>
S3_ENDPOINT=https://s3.${S3_REGION}.amazonaws.com
S3_BUCKET_PATH=https://${S3_BUCKET}.s3.${S3_REGION}.amazonaws.com/projects

```

## Routes

You will often create resourceful routes to do CRUD operations on a resource.

`useRouter.resource` assigns CRUD routes to a controller using a single line of code:

```
// app/routes/index.ts

// This...
useRouter.resource('users', 'UsersController')

// ...equates to this:
useRouter.get('users', UserController.index);
useRouter.get('users/details/:id', UserController.show);
useRouter.get('users/create', UserController.create);
useRouter.post('users', UserController.store);
useRouter.get('users/edit/:id', UserController.edit);
useRouter.put('users/:id', UserController.update);
useRouter.delete('users/:id', UserController.destroy);
```

You can pass a middleware between the path and the Controller.
`useRouter.get('users', yourMiddleware, UserController.index);`

Default router file.

```
// app/routes/index.ts

import { Router } from "core/router";

const useRouter = Router();

useRouter.get("/", (req, res) => res.render("home"));

export default useRouter;
```

## Database

We use Prisma ORM to handle the database. You can create new models from the schema.prisma file located in the `app/database/schema.prisma` directory. You can also export the models, for easier use, from `app/database/index.ts`.

We recommend that you use https://prismabuilder.io to speed up the model development process.

## Upload and Middlewares

You can import the upload module and pass it as middleware, like:

```
import { Router } from "core/router";
import { upload } from "core/modules";

const useRouter = Router();

useRouter.post("/upload", upload.single("file"), (req, res) => {
  return res.json(req.file?.filename);
});

export default useRouter;
```

For register your own middlewares, you can use the `registerMiddleware` function. For example:

```
registerRouter("/", (req, res, next) => {
  console.log('Request Type:', req.method);
  next();
})
```

## Layouts, views and partials

We use Nunjucks as template engine. For more references about nunjucks, access the official documentation at https://mozilla.github.io/nunjucks/

Layouts, views, and partials must remain in their respective directories. Inside the resources directory we have layouts, views, partials and js. You can create folders inside these directories, but keep the .nj files inside these directories.

## Validation

We use Zod as validator. For more references about Zod, access the official documentation at https://zod.dev/

## Tests

We use Jest or automation testing. For more references about Jest, access the official documentation at https://jestjs.io/

## Tasks and Jobs

For create a new periodic task, you can use the command line, `yarn g`, select the "task" option and enter the task name. As the first argument of the `createSchedule` function, you will use the cron format. For the second argument, you must pass the task function.

We use the node-cron library under the hood, so for more information, visit the official documentation at https://github.com/node-cron/node-cron

Lastly, you must register the new task by going to app/tasks/index.ts, importing the new task and passing it to this.jobs, within the constructor, as shown in the example code present in the project.

## Authentication

## Mailer

## Author

- [@lucasnjsilva](https://www.github.com/lucasnjsilva)

## References

We use some libraries under the hood, so for more informations, visit the official documentation.

**Libraries:**

- Express.js
- Express Session
- Prisma
- Helmet
- Cookie parser
- Morgan
- Multer
- Nodemailer
- Passport
- Zod
- Jest
- Cors
- AWS SDK
- Nunjucks
- Tailwind
- DaisyUI
