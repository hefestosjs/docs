### Logger

You can manage logging settings by editing the `active` property in the `app/config/logs.ts` file. The file will be generated in the `logs` folder, named with the current date and will have a `.log` extension.

#### Log Format Configuration

The `LogsConfig` object includes a `format` property that allows you to choose from several predefined logging formats:

- **combined**: Produces a standard Apache combined log output.
- **common**: Produces a standard Apache common log output.
- **dev**: Provides a concise, color-coded output ideal for development. The status code is colored according to its type:
  - Green: Successful responses
  - Red: Server errors
  - Yellow: Client errors
  - Cyan: Redirects
  - Uncolored: Informational responses
- **short**: A more compact format that also includes the response time.
- **tiny**: Minimal output for lightweight logging.

#### Custom Log Format

You can define a custom logging format using the `customFormat` property, allowing full customization based on the [Morgan documentation](https://github.com/expressjs/morgan).

> **Note**: This setup uses the `morgan` and `rotating-file-stream` libraries for logging and log file rotation.

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
