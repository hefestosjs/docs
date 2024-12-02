# Hefestos Framework Docs

Welcome! Hefestos is an MVC solution to develop your web application more easily and quickly. With a focus on productivity, Hefestos is splited in modules like authentication using jwt tokens or sessions, mail sending, periodic tasks and jobs, file upload to local driver or AWS S3 and much more. Hefestos was built on top of Bun, Typescript and Express.js.

## Summary

- [HefestosJS Docs](/README)

  - [Prerequisites](/README#prerequisites)
  - [Installation](/README#installation)
  - [Command Scripts](/README#command-scripts)
  - [Env](/README#env)
  - [Database](/pages/Database)
  - [Routes](/pages/Routes)
  - [Controllers](/pages/Controllers)
  - [Services](/pages/Services)
  - [Validation](/pages/Validation)
  - [ApiResponse](/pages/ApiResponse)
  - [Factories](/pages/Factories)
  - [Tests](/pages/Tests)
  - [Periodic Tasks and Jobs](/pages/Tasks)
  - [Security](/pages/Security)
  - [Performance](/pages/Performance)
  - [Static Assets](/pages/Assets)
  - [Middlewares](/pages/Middlewares/Page)
    - [Register a Server Middleware](/pages/Middlewares/Register)
    - [Boot Operations](/pages/Middlewares/Boot)
    - [Upload](/pages/Upload)
  - [Helpers and Hooks](/pages/Helpers)
    - [AppError](/pages/Helpers#apperror)
    - [File](/pages/Helpers#file)
    - [renderHtml](/pages/Helpers#renderhtml)
    - [useExclude](/pages/Helpers#useExclude)
    - [usePaginate](/pages/Helpers#usePaginate)
    - [useCache](/pages/Helpers#usecache)
  - [Logs](/pages/Logger)
  - [Generate files](/pages/Generator)
  - [Modules](/pages/Modules)
    - [Authentication](/pages/Authentication)
      - [API Session Strategy](/pages/Authentication#api-session-strategy)
      - [Full Stack Session Strategy](/pages/Authentication#full-stack-session-strategy)
      - [Token Strategy](/pages/Authentication#token-strategy)
    - [Mailer](/pages/Mailer)
    - [Layouts, views and partials](/pages/Views)
      - [Forms](/pages/Views#forms)
      - [Template Engine](/pages/Views#template-engine)
    - [Upload](/pages/Upload)
  - [References](/pages/References)
  - [Author](/README#author)

## Prerequisites:

- Bun (v1.1.20 or higher),
- Redis

## Installation

You can create a new project using the command:

```sh
bun install -g create-hefestos-app
```

```sh
bunx create-hefestos-app
```

## Command Scripts

- `start` - starts the server in production environment.

- `ms` - starts the server in a development environment, monitoring only changes to the server code.

- `mw` - starts the server in development environment, monitoring the code and tailwind changes (this command will be added when install views module).

- `g` - used to generate files, like controllers, services, views, validations and more.

- `module` - used to generate, install and configure modules, like authentication, views, mail sending, and more.

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

## Author

- [@lucasnjsilva](https://www.github.com/lucasnjsilva)
