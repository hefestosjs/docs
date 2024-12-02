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
