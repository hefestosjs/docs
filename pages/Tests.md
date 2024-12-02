## Tests

For test routes from the api, you can use the Supertest. You can import Supertest from: `import { Supertest } from "@hefestos/core";` and use like:

```typescript
import { describe, it, expect } from "bun:test";
import { Supertest } from "@hefestos/core";

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

We use Bun test module and Supertest. For more references about Supertest, access the official documentation at https://github.com/ladjs/supertest.

## Summary

- [HefestosJS Docs](/docs)

  - [Prerequisites](/docs#prerequisites)
  - [Installation](/docs#installation)
  - [Command Scripts](/docs#command-scripts)
  - [Env](/docs#env)
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
