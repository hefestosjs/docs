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

  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Command Scripts](#command-scripts)
  - [Env](#env)
  - [Database](/docs/pages/Database)
  - [Routes](/docs/pages/Routes)
  - [Controllers](/docs/pages/Controllers)
  - [Services](/docs/pages/Services)
  - [Validation](/docs/pages/Validation)
  - [ApiResponse](/docs/pages/ApiResponse)
  - [Factories](/docs/pages/Factories)
  - [Tests](/docs/pages/Tests)
  - [Periodic Tasks and Jobs](/docs/pages/Tasks)
  - [Security](/docs/pages/Security)
  - [Performance](/docs/pages/Performance)
  - [Static Assets](/docs/pages/Assets)
  - [Middlewares](/docs/pages/Middlewares/Page)
    - [Register a Server Middleware](/docs/pages/Middlewares/Register)
    - [Boot Operations](/docs/pages/Middlewares/Boot)
    - [Upload](/docs/pages/Upload)
  - [Helpers and Hooks](/docs/pages/Helpers)
    - [AppError](/docs/pages/Helpers#apperror)
    - [File](/docs/pages/Helpers#file)
    - [renderHtml](/docs/pages/Helpers#renderhtml)
    - [useExclude](/docs/pages/Helpers#useExclude)
    - [usePaginate](/docs/pages/Helpers#usePaginate)
    - [useCache](/docs/pages/Helpers#usecache)
  - [Logs](/docs/pages/Logger)
  - [Generate files](/docs/pages/Generator)
  - [Modules](/docs/pages/Modules)
    - [Authentication](/docs/pages/Authentication)
      - [API Session Strategy](/docs/pages/Authentication#api-session-strategy)
      - [Full Stack Session Strategy](/docs/pages/Authentication#full-stack-session-strategy)
      - [Token Strategy](/docs/pages/Authentication#token-strategy)
    - [Mailer](/docs/pages/Mailer)
    - [Layouts, views and partials](/docs/pages/Views)
      - [Forms](/docs/pages/Views#forms)
      - [Template Engine](/docs/pages/Views#template-engine)
    - [Upload](/docs/pages/Upload)
  - [References](/docs/pages/References)
  - [Author](#author)
