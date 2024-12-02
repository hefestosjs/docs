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
