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

Read more about [AppError](/pages/Helpers#apperror).

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
