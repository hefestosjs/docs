### ApiResponse

ApiResponse is a utility class designed to standardize the responses from the controller in an API. It provides structured methods to handle various types of responses, including:

- Successful operations, such as redirecting the user after a new post is registered or displaying a single post.
- Paginated data responses for displaying lists of posts or other items.
- Error handling, both for general errors and specific application errors, typically used within the catch blocks of try-catch statements.

You can find the ApiResponse.ts in `app/utils/ApiResponse.ts`.

Example usage scenarios include registering a new user, paginating a list of posts, or managing errors encountered during API requests.

**ApiResponse examples**:

```typescript
// Used when you successfully complete a request
// Example 1: When you successfully register a new post and then want to redirect the user to the listing screen.
// Example 2: When you want to display only 1 post.
ApiResponse.success(response, data, path_for_redirect);

// Used to display paginated data.
// PS: Recommended to use ResponseUtils.paginate
ApiResponse.pagination(response, posts);

// Used to display an error
// Recommended to use in the catch block of a try catch
ApiResponse.error(response, error);

// Used when you want to display an error like the AppError mentioned above
// Recommended to use in the catch block of a try catch
ApiResponse.appError(response, error);
```

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
