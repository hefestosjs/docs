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
