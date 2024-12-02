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
