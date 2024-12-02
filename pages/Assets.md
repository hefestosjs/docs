## Static assets

Static assets can be divided into css, js, images and assets in general. Inside the public folder, you can create, if it doesn't already exist, the images and assets folders. The directory for js files is inside the `app/resources/js` folder. The urls are:

- `/css` - `/public/css` directory.
- `/assets` - `/public/assets` directory.

If DRIVE chosen in the .env file is "local", you can create the "uploads" folder inside the project root. This is where the files will be saved. To access the files saved in the "uploads" folder you can access the url `/files`.

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
