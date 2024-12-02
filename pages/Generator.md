### Generator

Using the `bun g` command, you can generate one or multiple files simultaneously. The available file types are:

- **Validation**
- **Service**
- **Controller**
- **Factory**
- **Test**
- **Task**
- **Layout**
- **View**

---

#### Validation

Choose between generating a validation set or a single validation file.

- **set**: Creates a folder containing templates for both `create` and `update` validations.
- **single file**: Generates a single validation file using a predefined example template.

#### Service

Two options are available for generating service files:

- **single file**: Creates a single class file with each service method defined within it.
- **multiple files**: Generates a separate file for each service method.

#### Controller

You can generate controllers for either an API or a Full Stack application.

- **API Controller**: Includes methods for `index`, `show`, `store`, `update`, and `destroy`.
- **Full Stack Controller**: Includes additional methods for `create` and `edit` alongside the API methods.

#### Factory

Generates a factory file based on the specified model name. You’ll need to define the fields to be included in the factory output.

#### Test

Creates a test file using **Supertest** and **Bun test** frameworks.

#### Task

Generates a file for periodic tasks using **node-cron**.

#### Layout

Creates a layout file using **Nunjucks**.

> **Note**: The **views** module must be installed.

#### View

Generates a view file using **Nunjucks**.

> **Note**: The **views** module must be installed.

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
