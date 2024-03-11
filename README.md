# HefestosJS Docs

Welcome! HefestosJS is an MVC solution to develop your web application more easily and quickly. With a focus on productivity, HefestosJS is already configured for authentication using jwt tokens or sessions, sending emails, periodic tasks and jobs, uploading files to local driver or AWS S3 and much more.

## Summary

- [HefestosJS Docs](#hefestosjs-docs)
  - [Installation](#installation)
  - [Command Scripts](#command-scripts)
  - [Env](#env)
  - [Database](#database)
  - [Routes](#routes)
  - [Controllers](#controllers)
  - [Services](#services)
  - [Upload and Middlewares](#upload-and-middlewares)
  - [Layouts, views and partials](#layouts-views-and-partials)
  - [Validation](#validation)
  - [Tests](#tests)
  - [Tasks and Jobs](#tasks-and-jobs)
  - [Security](#security)
  - [Performance](#performance)
  - [Static Assets](#static-assets)
  - [Generate files](#generate-files)
  - [Logs](#logs)
  - [Authentication](#authentication)
  - [Mailer](#mailer)
  - [References](#references)

## Installation

You can create a new project using the command:

```
npx hefestos-forge hello-world
```

## Command Scripts

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
DRIVE_DISK=local
SSL=false
JWT_SECRET=secret
SESSION_SECRET=secret

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

## Database

We use Prisma ORM to handle the database. You can create new models from the schema.prisma file located in the `app/database/schema.prisma` directory. You can also export the models, for easier use, from `app/database/index.ts`.

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

## Controllers

Responsible for handling requests and directing them to the appropriate action, the controller is a class and can have as many and as many functions as you want, but if you use the `.resources` method or if you generate the controller using the command line, by default, the functions that must exist in the controller are:

- index
- show
- create
- store
- edit
- update
- destroy

You can import the Request and Response interfaces from within "core", for example: `import { Request, Response } from "core";`. If you are building an api, you can also import and use ApiResponse which contains the functions:

- success,
- pagination,
- error
- appError

In the example file "UserController.ts", it uses ApiResponse, Request and Response.

## Services

The service is a class and can have as many functions as you want, but if you generate the Service using the command line, by default, the functions that are created next to the service are:

- index
- show
- store
- update
- destroy

You can import the AppError interface from within "core" to trigger specific errors, for example: `import { AppError } from "core";`. If necessary, you can also import the ResponseUtils file, which has functions that help with pagination, deleting data, such as a password, an object or an array of objects. The functions are:

- page,
- exclude,
- excludeFromList

In the example file "UserService.ts", AppError and ResponseUtils are used.

An example of using AppError would be if a specific user was not found:

`if (!user) throw AppError.E_NOT_FOUND();`

## Validation

We use Zod as validator. For more references about Zod, access the official documentation at https://zod.dev/

## Upload and Middlewares

In direct routes, you can pass a middleware to a route after the path, for example:
`useRouter.get('/users', isAuthenticated, (req, res) => res.render('users));`

In resource routes, you can pass a middleware within an array after the Controller, for example:
`useRouter.resources("users", "UsersController", [isAuthenticated]);`

You can import the upload module and pass it as middleware, for example:

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

## Tests

We use Jest or automation testing. For more references about Jest, access the official documentation at https://jestjs.io/

## Tasks and Jobs

For create a new periodic task, you can use the command line, `yarn g`, select the "task" option and enter the task name. As the first argument of the `createSchedule` function, you will use the cron format. For the second argument, you must pass the task function.

We use the node-cron library under the hood, so for more information, visit the official documentation at https://github.com/node-cron/node-cron

Lastly, you must register the new task by going to app/tasks/index.ts, importing the new task and passing it to this.jobs, within the constructor, as shown in the example code present in the project.

## Security

By default, following the Content Security Policy directives, you cannot use in-line javascript or display images from unregistered urls, so within `app/config/security.ts` you can change the directives you want to, for example, For example, allow the creation and use of <scripts></scripts> within the view. If you don't change anything, the images and assets used in the views must be in some static assets folder; The javascript codes must be in files within the `app/resources/js` folder and called within the view in question.

## Performance

To improve our application performance, we can use some strategies like cache, cluster and compression.
Inside the `app/config/performance.ts` file, you can active cluster server, cache strategy and define cache life time in seconds. If cache is active, we'll use redis to store the cache.

We can cache our query results like:

```
  // app/services/UserService.ts

  static async index(currentPage: number = 1) {
    const perPage = 10;
    const page = currentPage ? currentPage : 1;
    const skip = (page - 1) * perPage;

    // Cache
    const key = `users.list.params=${skip}_${perPage}`;
    const cached = await useCache.get(key);

    if (cached) {
      return JSON.parse(cached);
    }

    // Queries
    const totalUsers = await User.count();
    const query = await User.findMany({ take: perPage, skip });
    const users = ResponseUtils.excludeFromList(query, ["password"]);

    const response = ResponseUtils.paginate({
      data: users,
      totalData: totalUsers,
      page,
      perPage,
    });

    await useCache.set(key, JSON.stringify(response));

    return response;
  }
```

From 100kb the response will be compressed with gzip. If you don't want to compress some page, you can pass `x-no-compression`header.

## Static assets

Static assets can be divided into css, js, images and assets in general. Inside the public folder, you can create, if it doesn't already exist, the images and assets folders. The directory for js files is inside the `app/resources/js` folder. The urls are:

- /css
- /js
- /images
- /assets

If DRIVE chosen in the .env file is "local", you can create the "uploads" folder inside the project root. This is where the files will be saved. To access the files saved in the "uploads" folder you can access the url `/files`.

## Generate files

Using the `npm run g` command line you can generate:

- controller
- service
- validation
- task
- test
- layout
- view

You can abbreviate the command using the command line, generator and file name, for example: `npm run g controller Post`. The "PostController.ts" file will be created inside the `app/controllers` folder.

## Logs

You can enable or disable logs in the `app/config/logs.ts` file by changing the value of active property. If the NODE_ENV is development, a log file will be created within the `app/logs` folder with the name of the day of the log and the file extension ".log". If NODE_ENV is production, a log file will be created daily and compressed at the end of the day. The file will be compressed if the file reaches 5mb. You can create a task to send the log files that were compressed to a bucket in AWS.

## Authentication

We have 2 strategies, session and token. You can configure your authentication options like table and unique column used to sign in, strategy and more inside `app/config/auth.ts`.

```
const auth: AuthConfig = {
  strategy: "web",
  table: "users",
  uniqueColumn: "email",
  tokenStrategy: {
    secret: process.env.JWT_SECRET || "secret",
    expiresIn: "30d",
    useRedis: true,
  },
};
```

### Session Strategy

Inside `app/config/auth.ts` set strategy to "web".

- To make login is like:

  ```
    static async store(request: Request, response: Response, next: Next) {
      try {
        const { email, password } = request.body;
        const user = await SessionService.getUser(email, password);

        Auth.login({
          session: {
            request,
            response,
            next,
            user,
            redirectPath: "/logout",
          },
        });
      } catch (error: any) {
        return ApiResponse.error(response, error);
      }
    }
  ```

- To check if a user is authenticated to access a route you can use the middleware isAuthenticated like:

  `useRouter.get("/", isAuthenticated, (req, res) => res.render("home"));`

- To make logout is like:
  ```
  static async destroy(request: Request, response: Response, next: Next) {
    try {
      Auth.logout({
        session: {
          request,
          response,
          next,
          redirectPath: "/login",
        },
      });
    } catch (error: any) {
      return ApiResponse.error(response, error);
    }
  }
  ```

### Token Strategy

Inside `app/config/auth.ts` set strategy to "token".

- To make login is like:

  ```
  static async store(request: Request, response: Response, next: Next) {
    try {
      const { email, password } = request.body;
      const user = await SessionService.getUser(email, password);

      const result = await Auth.login({
        token: {
          request,
          response,
          next,
          userId: user.id,
        },
      });

      return ApiResponse.success(response, result, "/");
    } catch (error: any) {
      return ApiResponse.error(response, error);
    }
  }
  ```

- To check if a user is authenticated to access a route you can use the middleware isAuthenticated like:

  `useRouter.get("/", isAuthenticated, (req, res) => res.render("home"));`

PS: remember that if you're using token strategy, you must use the Authorization header, like `Authorization: Bearer {{token}}` replacing "{{token}}" by the token returned in `Auth.login`.

- To make logout is like:

  ```
  static async destroy(request: Request, response: Response, next: Next) {
    try {
      const result = await Auth.logout({
        token: {
          request,
          response,
        },
      });

      return ApiResponse.success(response, result, "/");
    } catch (error: any) {
      return ApiResponse.error(response, error);
    }
  }
  ```

Both the session and the tokens are stored within redis. If, when using token strategy, you do not want to store the token in redis or if you want to make any changes, you can modify in `vendor/auth/token.ts`.

## Mailer

## Author

- [@lucasnjsilva](https://www.github.com/lucasnjsilva)

## References

We use some libraries under the hood, so for more informations, visit the official documentation.

**Libraries:**

- Express.js
- Express Session
- JsonWebToken
- Compression
- Redis
- Connect Reddis
- UUID
- Prisma
- Helmet
- Cookie parser
- Morgan
- Multer
- Nodemailer
- Zod
- Jest
- Cors
- AWS SDK
- Nunjucks
- Tailwind
