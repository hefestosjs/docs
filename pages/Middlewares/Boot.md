## Boot Operations

Boot operations allow you to execute custom logic **before the server initialization**. Unlike middlewares, boot operations are not tied to handling specific requests but are used to perform tasks like setting up configurations, initializing services, or running pre-start logic. To define a boot operation, add it to `app/middlewares/boot.ts`.

### Structure of a Boot Operation

Each boot operation is an object that contains:

- **function**: The logic to be executed.
- **params**: An array of parameters passed to the function.

All boot operations listed in `bootOperations` are executed sequentially.

### 1. Boot Operation Without Parameters

A simple boot operation that doesn't require parameters:

```typescript
export const bootOperations: OperationsType[] = [
  {
    function: () => {
      console.log("Server initialization started.");
    },
    params: [], // No parameters needed
  },
];
```

### 2. Boot Operation With Parameters

You can pass parameters to the function using the `params` array:

```typescript
export const bootOperations: OperationsType[] = [
  {
    function: (name, environment) => {
      console.log(`Initializing ${name} in ${environment} mode.`);
    },
    params: ["Server", "Production"],
  },
];
```

### 3. Executing Multiple Boot Operations

You can define multiple boot operations to be executed in sequence:

```typescript
export const bootOperations: OperationsType[] = [
  {
    function: () => {
      console.log("Connecting to the database...");
    },
    params: [],
  },
  {
    function: (service) => {
      console.log(`Initializing service: ${service}`);
    },
    params: ["AuthService"],
  },
  {
    function: (message) => {
      console.log(message);
    },
    params: ["Server is ready to start!"],
  },
];
```

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
