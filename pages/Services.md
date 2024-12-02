## Services

Our code generator will generate 2 approaches for services: a single-file or a multiple-files approach. The service in a single file has each method as a functionality, but if you choose the multiple-files approach, each file will contain a single method. The service as a single file is a class and can have as many functions as you want, but if you generate the service using the command line, by default, the functions created alongside the service are:

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

You can import the AppError interface from within `@hefestos/core `to trigger specific errors, for example: `import { AppError } from "@hefestos/core";`.

An example of using AppError would be if a specific user was not found:
`if (!user) throw AppError.E_NOT_FOUND();`

Read more about [AppError](/docs/pages/Helpers#apperror).

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
