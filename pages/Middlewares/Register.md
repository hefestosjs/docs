## Register a Server Middleware

Middlewares allow you to execute custom logic on incoming requests before they reach your defined routes. You can apply them globally, to specific routes, or to groups of routes based on a common path. Define your middlewares in `app/middlewares/index.ts` as shown below.

### 1. Apply Middleware to a Specific Route

To apply middleware to a single route, specify the `path` field. This example logs the request time for requests to `/health`:

```typescript
export const middlewareList: MiddlewareType[] = [
  {
    function: (request, response, next) => {
      console.log("Request received at:", new Date().toISOString());
      next(); // Passes control to the next middleware or route handler
    },
    path: "/health", // Middleware applies only to "/health"
  },
];
```

### 2. Apply Middleware Globally

To apply middleware to **all routes**, leave the `path` field empty. This ensures the middleware executes on every incoming request:

```typescript
export const middlewareList: MiddlewareType[] = [
  {
    function: (request, response, next) => {
      console.log("Global Middleware: Request received");
      next();
    },
    path: "", // Applies to all routes
  },
];
```

### 3. Apply Middleware to a Group of Routes

If you want middleware to apply to a group of routes under a shared path, such as `/admin`, define the `path` accordingly. This ensures the middleware runs for all `/admin` routes:

```typescript
export const middlewareList: MiddlewareType[] = [
  {
    function: (request, response, next) => {
      console.log("Hello from Admin!", request.url);
      next();
    },
    path: "/admin", // Applies to all routes under "/admin"
  },
];
```

This approach ensures middleware execution on any request matching the `/admin` path and its subpaths.

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
