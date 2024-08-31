# HefestosJS Docs

Welcome! HefestosJS is an MVC solution to develop your web application more easily and quickly. With a focus on productivity, HefestosJS is already configured for authentication using jwt tokens or sessions, sending emails, periodic tasks and jobs, uploading files to local driver or AWS S3 and much more. HefestosJS can be used with Node.js or Bun.

## Summary

- [HefestosJS Docs](#hefestosjs-docs)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Command Scripts](#command-scripts)
  - [Env](#env)
  - [Database](#database)
  - [Routes](#routes)
  - [Controllers](#controllers)
  - [Services](#services)
  - [Upload and Middlewares](#upload-and-middlewares)
  - [Helpers and Hooks](#helpers-and-hooks)
    - [AppError](#apperror)
    - [ResponseUtils](#responseutils)
    - [ApiResponse](#apiresponse)
    - [useCache](#usecache)
    - [renderHtml](#renderhtml)
    - [File](#file)
    - [S3](#s3)
    - [useRequest](#userequest)
  - [Layouts, views and partials](#layouts-views-and-partials)
  - [Validation](#validation)
  - [Tests](#tests)
  - [Factories](#factories)
  - [Tasks and Jobs](#tasks-and-jobs)
  - [Security](#security)
  - [Performance](#performance)
  - [Static Assets](#static-assets)
  - [Generate files](#generate-files)
  - [Logs](#logs)
  - [Authentication](#authentication)
    - [Session Strategy](#session-strategy)
    - [Token Strategy](#token-strategy)
  - [Mailer](#mailer)
  - [References](#references)

## Prerequisites:

- Node (v16.x or higher) or Bun (v1.1.20 or higher),
- Redis

## Installation

You can create a new project using the command:

```javascript
npx hefestos-forge

// or

bunx hefestos-forge
```

## Command Scripts

- `build` - delete the current dist folder (if exists), copy the resources files (views, partials, layouts) and transpile the typescript to the dist folder (available only in node.js runtime).

- `start` - starts the server in production environment.

- `dev` - starts the server in development environment, monitoring the code and tailwind changes.

- `ms` - starts the server in a development environment, monitoring only changes to the code.

- `test` - starts the tests

- `g` - used to generate files, like controllers, services, views, validations and more.

- `studio` - starts the prisma studio.

- `seed` - Populate your database with your data.

## Env

Create a .env file from .env.example.

See below an example of a complete .env, with database, mailer and amazon s3 variables to configure.

```
# Application
PORT = 3000
NODE_ENV=development
DRIVE_DISK=local
JWT_SECRET=secret
SESSION_SECRET=secret
COOKIE_SECRET=secret

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

In the .env file, the DB_URL variable changes according to the bank you choose, being:

- PostgreSQL: `DB_URL=postgresql://${DB_USER}:${DB_PASS}@${DB_HOST}:${DB_PORT}/${DB_NAME}`
- MySQL: `DB_URL=mysql://${DB_USER}:${DB_PASS}@${DB_HOST}:${DB_PORT}/${DB_NAME}`
- SQLite: `DB_URL="file:./dev.db"`

If you want to do a raw query, you can use the Database handler located in the `app/database/database.ts` directory. This handler is just an abstraction of Prisma's native functions, so instead of doing:

```typescript
const [posts, totalPosts] = await prisma.$transaction([
  prisma.post.findMany({ where: { title: { contains: "prisma" } } }),
  prisma.post.count(),
]);
```

You will be able to do:

```typescript
import { Database } from "app/database/database";
import { Post } from "app/database";

const [posts, totalPosts] = await Database.transaction([
  Post.findMany({ where: { title: { contains: "prisma" } } }),
  Post.count(),
]);
```

For more information, visit the official documentation.

## Routes

You will often create resourceful routes to do CRUD operations on a resource.

`useRouter.resource` assigns CRUD routes to a controller using a single line of code:

```typescript
// app/routes/index.ts

// This...
useRouter.resource("users", "UsersController");

// ...equates to this:
useRouter.get("users", UserController.index);
useRouter.get("users/details/:id", UserController.show);
useRouter.get("users/create", UserController.create);
useRouter.post("users", UserController.store);
useRouter.get("users/edit/:id", UserController.edit);
useRouter.put("users/:id", UserController.update);
useRouter.delete("users/:id", UserController.destroy);
```

You can pass a middleware between the path and the Controller.
`useRouter.get('users', yourMiddleware, UserController.index);`

Default router file.

```typescript
// app/routes/index.ts

import { Router } from "core/router";

const useRouter = Router();

useRouter.get("/", (req, res) => res.render("home"));

export default useRouter;
```

## Controllers

Responsible for handling requests and directing them to the appropriate action, the controller is a class and can have as many functions as you want, but if you use the `.resources` method or if you generate the controller using the command line, by default, the functions that must exists in the controller are:

- index
- show
- create
- store
- edit
- update
- destroy

```typescript
const useRouter = Router();

useRouter.resources("path", "ControllerName", [
  middleware,
  { method: "store", middleware: customMiddleware },
]);
```

To better understand how middleware works, read the [middleware](#upload-and-middlewares) section.

You can import the Request and Response interfaces from within "core", for example: `import type { Request, Response } from "core";`. If you are building an api, you can also import and use [ApiResponse](#apiresponse) which contains the functions:

- success,
- pagination,
- error
- appError

## Services

Our code generator will generate 2 approaches for services: a single-file approach or a multiple-files approach. The service in a single file has each method as a functionality, but if you choose the multiple-files approach, each file will contain a single method. The service as a single file is a class and can have as many functions as you want, but if you generate the service using the command line, by default, the functions created alongside the service are:

For the single-file approach, the command line will generate file with a class that can have as many functions as you want, and by default, the functions created alongside the service are:

- index
- show
- store
- update
- destroy

For the multiple-files approach, the command line will generate a folder with the name you chose, containing the files:

- index.ts
- Create.ts
- Update.ts
- List.ts
- Show.ts
- Delete.ts

You can import the AppError interface from within "core" to trigger specific errors, for example: `import { AppError } from "core";`. If necessary, you can also import the ResponseUtils file, which has functions that help with pagination, deleting data, such as a password, an object or an array of objects. The functions are:

- page,
- exclude,
- excludeFromList

An example of using AppError would be if a specific user was not found:

`if (!user) throw AppError.E_NOT_FOUND();`

## Validation

We use Zod as validator. For more references about Zod, access the official documentation at https://zod.dev/

## Upload and Middlewares

In direct routes, you can pass a middleware to a route after the path, for example:

```typescript
useRouter.get('/users', isAuthenticated, (req, res) => res.render('users));
```

In resource routes, you can pass a middleware within an array after the Controller to execute for all resource methods, for example:

```typescript
useRouter.resources("users", "UsersController", [isAuthenticated]);
```

But if you want to use a middleware in a specific resource method, you can pass an object with the method and middleware, for exemple:

```typescript
useRouter.resources("users", "UsersController", [
  isAuthenticated,
  { method: "store", middleware: upload().single("file") },
]);
```

You can import the `upload` internal middleware from `core/middlewares` and pass it as middleware. The `upload` is a function that can receive an object with folder name. For example: `upload().single("file")` or `upload({ folder: 'images' }).single("file")`.

```typescript
import { Router } from "core/router";
import { upload } from "core/middlewares";

const useRouter = Router();

useRouter.post("/upload", upload().single("file"), (req, res) => {
  return res.json(req.file?.filename);
});

export default useRouter;
```

The `upload` internal middleware will upload to the local `uploads` directory. If you pass a folder as a parameter, this folder will be created within `uploads`. In the case of `upload({ folder: 'images' }).single("file")`, the "images" folder will be created within `uploads`, and the files sent via the "file" field will be stored within it.

To upload to an aws s3 bucket, you must import the `uploadTo` module from "core/modules". For example:

```typescript
import { ApiResponse, AppError } from "core";
import { Router } from "core/router";
import { upload } from "core/middlewares";
import { uploadTo } from "core/modules";

const useRouter = Router();

useRouter.post("/media", upload().single("file"), async (request, response) => {
  try {
    if (!request.file) {
      throw AppError.E_VALIDATION_FAIL("The file is required.");
    }

    await uploadTo.s3({ fileName: request.file.filename, file: request.file });

    return ApiResponse.success(response, true);
  } catch (error: any) {
    return ApiResponse.error(response, error);
  }
});

export default useRouter;
```

For register your own middlewares, you can use the `registerMiddleware` function. For example:

```typescript
registerRouter("/", (req, res, next) => {
  console.log("Request Type:", req.method);
  next();
});
```

## Helpers and Hooks

You can import the helpers from "core/helpers".

#### AppError

AppError is a utility class designed to throw predefined exceptions in an API. It provides a standardized way to handle various types of errors, making error management consistent and predictable.

You can import it like this: `import { AppError } from 'core/helpers';`.

AppError examples:

```typescript
// Example: used when an unexpected error occurs
throw AppError.E_BAD_REQUEST();

// Example: used when a route is prohibited for a user's role
throw AppError.E_FORBIDDEN();

// Used for generic errors
throw AppError.E_GENERIC_ERROR();

// Example: used when trying to log in with invalid credentials
throw AppError.E_INVALID_CREDENTIALS();

// Used for logic errors
throw AppError.E_LOGIC_ERROR();

// Example: used when a user tries to access data that does not exist
throw AppError.E_NOT_FOUND();

// Example: used when an unauthenticated user try access a private route
throw AppError.E_UNAUTHORIZED();

// Example: used when a registration fails form validation
throw AppError.E_VALIDATION_FAIL();
```

### ResponseUtils

ResponseUtils is a utility class designed to refine and format method responses in an API. It provides methods for various common tasks, including:

- Excluding specific fields from an object, such as removing sensitive information like passwords or phone numbers before returning a user object.
- Excluding specific fields from an array of objects, useful for scenarios like returning a list of users without exposing their passwords.
- Paginating data, to efficiently handle and return large datasets in manageable chunks.

Example usage includes cleaning up user data before sending it in a response or paginating a list of users for easier navigation.

You can import it like this: `import { ResponseUtils } from 'core/helpers';`.

ResponseUtils examples:

```typescript
// Used when you want to delete data from an object.
// Example: when you access a user's show method and don't want the password to appear in the user object.
ResponseUtils.exclude(user, ["password", "phone"]);

// Used when you want to delete data from an array of objects.
// Example: when you access the user list and do not want passwords to appear on objects in that list.
ResponseUtils.excludeFromList(users, ["password"]);

// ResponseUtils.paginate - used to paginate data
class UserService {
  static async index(currentPage: number = 1) {
    const perPage = 10;
    const page = currentPage ? currentPage : 1;
    const totalUsers = await User.count();
    const users = ResponseUtils.excludeFromList(query, ["password"]);

    return ResponseUtils.paginate({
      data: users,
      totalData: totalUsers,
      page,
      perPage,
    });
  }
}
```

### ApiResponse

ApiResponse is a utility class designed to standardize the responses from the controller in an API. It provides structured methods to handle various types of responses, including:

- Successful operations, such as redirecting the user after a new post is registered or displaying a single post.
- Paginated data responses for displaying lists of posts or other items.
- Error handling, both for general errors and specific application errors, typically used within the catch blocks of try-catch statements.

Example usage scenarios include registering a new user, paginating a list of posts, or managing errors encountered during API requests.

ApiResponse examples:

```typescript
// Used when you successfully complete a request
// Example 1: When you successfully register a new post and then want to redirect the user to the listing screen.
// Example 2: When you want to display only 1 post.
ApiResponse.success(response, data, path_for_redirect);

// Used to display paginated data.
// PS: Recommended to use ResponseUtils.paginate
ApiResponse.pagination(response, posts);

// Used to display an error
// Recommended to use in the catch block of a try catch
ApiResponse.error(response, error);

// Used when you want to display an error like the AppError mentioned above
// Recommended to use in the catch block of a try catch
ApiResponse.appError(response, error);
```

### useCache

useCache is a utility module designed for managing cache operations in an application. It provides methods to interact with the cache, enabling efficient data retrieval and storage.

```typescript
// Used to check whether a given key exists in the cache.
await useCache.get(key);

// Stores data in the cache, passing the identification key and the data in string format
await useCache.set(key, JSON.stringify(data));
```

### renderHtml

renderHtml is a utility function designed for rendering email templates with dynamic content. By passing variables to the email template, you can customize the content based on specific data.

Example usage scenario for renderHtml:

Rendering a marketing email template with a user's name

```typescript
renderHtml("mails/marketing.nj", userName);
```

We recommend keeping email templates in the mails directory for better organization and maintainability.

You can import it like this: `import { renderHtml } from 'core/helpers';`.

### File

The File module provides various utilities for handling file and directory operations. You can import the File module like this: `import { File } from 'core/modules';`.

```typescript
// Used to check if a file or directory exists.
// Return a boolean value.
File.exists("/file_path");

// User to rename a file or directory.
File.rename("/file_path/file_name", "/file_path/new_file_name");

// User to move a file to a new directory.
File.move("/old_path", "/new_path");

// User to delete a file or directory.
File.remove("/file_path");

// Used to load a stream and return a buffer.
// Expect a stream value.
// If you want to get a buffer from a file, use the File.createBuffer.
await File.loadStream(stream);

// Used to create a buffer from a file path.
// Return the buffer.
await File.createBuffer("/file_path");
```

### S3

Through the S3 module you can add or remove files from the s3 bucket. The S3 module has 2 functions `put` and `delete`.

`put` - expects to receive the parameters:

```typescript
key: string;
body: Buffer;
contentType: string;
```

Put example:

```typescript
const key = join(params.folder || "", params.fileName);
const body = await File.createBuffer(filePath);

const config = {
  key,
  body,
  contentType: "image/png",
};

await S3.put(config);
```

`delete` - expects to receive the parameters:

```typescript
fileName: string;
folder?: string;
```

Delete example:

```typescript
const media = {
  url: "file.jpg",
  userId: 2,
};

await S3.delete({ fileName: media.url, folder: media.userId });
```

PS: To upload files to S3, we recommend using the `uploadTo` module from "core/modules".

You can import the File module like this: `import { File } from 'core/modules';`.

### useRequest

useRequest is a utility module designed to facilitate handling HTTP requests. It provides a set of methods for making various types of requests to external APIs or services, including GET, POST, PUT, PATCH, and DELETE.

Example usage scenarios for useRequest include:

```typescript
// Sending a GET request:
await useRequest.GET({ url: "https://api.example.com", path: "endpoint" });

// Sending a POST request with a request body:
await useRequest.POST({
  url: "https://api.example.com/",
  path: "endpoint",
  body: { key: "value" },
  headers: { "Custom-Header": "value" },
});

// Sending a PUT request to update data:
await useRequest.PUT({
  url: "https://api.example.com",
  path: "endpoint",
  body: { key: "updatedValue" },
});

// Sending a PATCH request to partially update data:
await useRequest.PATCH({
  url: "https://api.example.com",
  path: "endpoint",
  body: { key: "newValue" },
});

// Sending a DELETE request:
await useRequest.DELETE({ url: "https://api.example.com", path: "endpoint" });
```

The useRequest module simplifies making requests and handling responses by abstracting the details of the HTTP methods and request setup. The useRequest accepts json and formData in its body. By default, Content-Type: application/json is already implemented in the header, but this changes if you decide to use formData.

You can import it like this: `import { useRequest } from 'core/helpers';`

## Layouts, views and partials

We use Nunjucks as template engine. For more references about nunjucks, access the official documentation at https://mozilla.github.io/nunjucks/

Layouts, views, and partials must remain in their respective directories. Inside the resources directory we have layouts, views, partials and js. You can create folders inside these directories, but keep the .nj files inside these directories.

## Tests

For test routes from the api, you can use the Supertest. You can import Supertest from: `import { Supertest } from "core/modules";` and use like:

```typescript
import { describe, it, expect } from "@jest/globals";
import { Supertest } from "core/modules";

descript("List posts", () => {
  it("Successfully list the posts", async () => {
    // Creating some posts for the list
    // ...

    // Main request
    const { body, status } = await Supertest.get("/posts");

    expect(status).toBe(200);
    expect(body).toEqual(
      expect.objectContaining({
        status: "OK",
        error: null,
        // result: ...
      })
    );
  });
});
```

We use Jest and Supertest. For more references about Jest, access the official documentation at https://jestjs.io/ and https://github.com/ladjs/supertest.

## Factories

Factories are used to define a blueprint of a data structure and then using that blueprint to generate dummy data. You can create a Factory using our generator with the command `yarn g` and selecting the factory option, or just using `yarn g factory ModelName`. Let’s check out this example.

First, we'll use the command `yarn g factory ContentCreator` and the file will be generated in `/app/database/factories/ContentCreatorFactory.ts`. Inside the ContentCreatorFactory file, we'll set the properties like this.

```typescript
import { Factory } from "core/modules";
import { ContentCreator } from "..";

export default new Factory().define(ContentCreator, (faker) => {
  return {
    name: faker.person.fullName(),
    biography: faker.lorem.sentence(4),
  };
});
```

The factories uses the @faker-js library. For more references about @faker-js, access the official documentation at https://fakerjs.dev/

## Tasks and Jobs

For create a new periodic task, you can use the command line, `yarn g`, select the "task" option and enter the task name. As the first argument of the `createSchedule` function, you will use the cron format. For the second argument, you must pass the task function.

We use the node-cron library under the hood, so for more information, visit the official documentation at https://github.com/node-cron/node-cron

Lastly, you must register the new task by going to app/tasks/index.ts, importing the new task and passing it to this.jobs, within the constructor, as shown in the example code present in the project.

## Security

By default, following the Content Security Policy directives, you cannot use in-line javascript or display images from unregistered urls, so within `app/config/security.ts` you can change the directives you want to, for example, For example, allow the creation and use of <scripts></scripts> within the view. If you don't change anything, the images and assets used in the views must be in some static assets folder; The javascript codes must be in files within the `app/resources/js` folder and called within the view in question.

## Performance

To improve our application performance, we can use some strategies like cache, redis, cluster and compression.

Inside the `app/config/performance.ts` file, you can active cluster server, redis, cache strategy and define cache life time in seconds. If cache and redis are active, we'll use redis to store the cache.

We can cache our query results like:

```typescript
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

Using the `npm run g` or `bun g` command line you can generate:

- controller
- service
- validation
- task
- test
- layout
- view

## Logs

You can enable or disable logs in the `app/config/logs.ts` file by changing the value of active property. If the NODE_ENV is development, a log file will be created within the `app/logs` folder with the name of the day of the log and the file extension ".log". If NODE_ENV is production, a log file will be created daily and compressed at the end of the day. The file will be compressed if the file reaches 5mb. You can create a task to send the log files that were compressed to a bucket in AWS.

## Authentication

We have 2 strategies, session and token. You can configure your authentication options like table and unique column used to sign in, strategy and more inside `app/config/auth.ts`.

```typescript
const auth: AuthConfig = {
  strategy: "web",
  table: "users",
  uniqueColumn: "email",
  tokenStrategy: {
    secret: process.env.JWT_SECRET || "secret",
    expiresIn: "30d",
    useRedis: true,
  },
  sessionStrategy: {
    useRedis: true,
    prefix: "myapp:", // RedisStore prefix
    secret: process.env.SESSION_SECRET || "secret",
    resave: false, // Required: force lightweight session keep alive (touch)
    saveUninitialized: false, // Recommended: only save session when data exists
    cookie: {
      httpOnly: true, // If true prevent client side JS from reading the cookie
      maxAge: 90 * 24 * 60 * 60 * 1000, // Session max age in miliseconds (3 months in this case)
    },
  },
};
```

### Session Strategy

Inside `app/config/auth.ts` set strategy to "web".

- To make login is like:

  ```typescript
    static async store(request: Request, response: Response, next: Next) {
      try {
        const { email, password } = request.body;

        // Check if the credentials are valid and if user exists
        const user = await SessionService.getUser(email, password);

        // You can import it from vendor/auth
        await Auth.login({
          session: {
            request,
            response,
            next,
            user,
            redirectPath: "/",
          },
        });
      } catch (error: any) {
        console.log(error);
      }
    }
  ```

- To check if a user is authenticated to access a route you can use the middleware isAuthenticated like:

  `useRouter.get("/", isAuthenticated, (req, res) => res.render("home"));`

- To make logout is like:

  ```typescript
  static async destroy(request: Request, response: Response, next: Next) {
    try {
      // You can import it from vendor/auth
      await Auth.logout({
        session: {
          request,
          response,
          next,
          redirectPath: "/",
        },
      });
    } catch (error: any) {
      console.log(error);
    }
  }
  ```

  **PS:** If you are using session strategy, do not use ApiResponse or an error will be thrown, for example:

  ```typescript
  const result = await Auth.login({
    session: {
      request,
      response,
      next,
      user,
      redirectPath: "/",
    },
  });

  return ApiResponse.success(response, result, "/");
  ```

  The error:

  ```
  uncaughtException signal received.
  Error [ERR_HTTP_HEADERS_SENT]: Cannot set headers after they are sent to the client
  ```

### Token Strategy

Inside `app/config/auth.ts` set strategy to "token".

- To make login is like:

  ```typescript
  static async store(request: Request, response: Response, next: Next) {
    try {
      const { email, password } = request.body;

      // Check if the credentials are valid and if user exists
      const user = await SessionService.getUser(email, password);

      // You can import it from vendor/auth
      const result = await Auth.login({
        token: {
          request,
          response,
          next,
          userId: user.id,
        },
      });

      return ApiResponse.success(response, result);
    } catch (error: any) {
      return ApiResponse.error(response, error);
    }
  }
  ```

- To check if a user is authenticated to access a route you can use the middleware isAuthenticated like:

  `useRouter.get("/", isAuthenticated, (req, res) => res.render("home"));`

PS: remember that if you're using token strategy, you must use the Authorization header, like `Authorization: Bearer {{token}}` replacing "{{token}}" by the token returned in `Auth.login`.

- To make logout is like:

  ```typescript
  static async destroy(request: Request, response: Response, next: Next) {
    try {
      // You can import it from vendor/auth
      const result = await Auth.logout({
        token: {
          request,
          response,
        },
      });

      return ApiResponse.success(response, result);
    } catch (error: any) {
      return ApiResponse.error(response, error);
    }
  }
  ```

Both the session and the tokens can be stored in redis. If, when using token strategy, you do not want to store the token in redis or if you want to make any changes, you can modify in `vendor/auth/token.ts`.

To use redis for authentication, useRedis in the `app/config/auth.ts` must be true, and redis in `app/config/performance.ts` must be true.

## Mailer

First you need to set the `SMTP_HOST, SMTP_PORT, SMTP_USER and SMTP_PASSWORD` environment variables.

To send emails, we will use the sendMail function of the Mailer class, which is located in the vendor/mail directory.

**Example:**

```typescript
await Mailer.sendMail({
  from: "your_email@email.com",
  to: "user_email@email.com",
  subject: "E-mail Subject",
  text: "E-mail message",
  html: "HTML code in string format",
});
```

We recommend using the renderHtml function that you can import from "core" to turn your HTML email template into a string. We also recommend that you always send the email message in text in addition to HTML.

In renderHtml you will pass the file path with extension, for example: `renderHtml("mails/contact.nj");`

We recommend keeping email templates in the mails directory.

**Complete Example:**

```typescript
import { ApiResponse, renderHtml } from "core";

const useRouter = Router();

useRouter.post("/mail", async (request, response) => {
  try {
    const htmlString = renderHtml("mails/contact.nj");

    await Mailer.sendMail({
      from: "your_email@email.com",
      to: "user_email@email.com",
      subject: "E-mail Subject",
      text: "E-mail message",
      html: htmlString,
    });

    return ApiResponse.success(response);
  } catch (error: any) {
    return ApiResponse.error(response, error);
  }
});

export default useRouter;
```

_We use the nodemailer library, for more information visit its official documentation._

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
- Supertest
- Cors
- AWS SDK
- Nunjucks
- Tailwind
- FakerJS
- BiomeJS
