## Helpers and Hooks

You can import the helpers from `@hefestos/core`.

#### AppError

AppError is a utility class designed to throw predefined exceptions in an API. It provides a standardized way to handle various types of errors, making error management consistent and predictable.

You can import it like this: `import { AppError } from '@hefestos/core';`.

**AppError examples:**

```typescript
// Example: used when an unexpected error occurs
throw AppError.E_BAD_REQUEST();

// Example: used when a route is prohibited for a user's role
throw AppError.E_FORBIDDEN();

// Used for generic errors
throw AppError.E_GENERIC_ERROR();

// Example: used when trying to log in with invalid credentials
throw AppError.E_INVALID_CREDENTIALS();

// Used for logic errors
throw AppError.E_LOGIC_ERROR();

// Example: used when a user tries to access data that does not exist
throw AppError.E_NOT_FOUND();

// Example: used when an unauthenticated user try access a private route
throw AppError.E_UNAUTHORIZED();

// Example: used when a registration fails form validation
throw AppError.E_VALIDATION_FAIL();
```

### useExclude

`.fromObject` - Excluding specific fields from an object, such as removing sensitive information like passwords or phone numbers before returning a user object.
`.fromList` - Excluding specific fields from an array of objects, useful for scenarios like returning a list of users without exposing their passwords.

You can import it like this: `import { useExclude } from '@hefestos/core';`.

Example:

```typescript
// import { useExclude } from '@hefestos/core';

// Used when you want to delete data from an object.
// Example: when you access a user's show method and don't want the password to appear in the user object.
useExclude.fromObject(user, ["password", "phone"]);

// Used when you want to delete data from an array of objects.
// Example: when you access the user list and do not want passwords to appear on objects in that list.
useExclude.fromList(users, ["password"]);
```

### usePaginate

- Paginating data, to efficiently handle and return large datasets in manageable chunks.

You can import it like this: `import { usePaginate } from '@hefestos/core';`.

Example:

```typescript
import { useExclude, usePaginate } from "@hefestos/core";

class UserService {
  static async index(currentPage: number = 1) {
    const perPage = 10;
    const page = currentPage ? currentPage : 1;
    const totalUsers = await User.count();
    const users = useExclude.fromList(query, ["password"]);

    return usePaginate({
      data: users,
      totalData: totalUsers,
      page,
      perPage,
    });
  }
}
```

### useCache

useCache is a utility module designed for managing cache operations in an application. It provides methods to interact with the cache, enabling efficient data retrieval and storage.

You can import it like this: `import { useCache } from '@hefestos/core';`.

```typescript
// Used to check whether a given key exists in the cache.
await useCache.get(key);

// Stores data in the cache, passing the identification key and the data in string format
await useCache.set(key, JSON.stringify(data));
```

### renderHtml

renderHtml is a utility function designed for rendering email templates with dynamic content. By passing variables to the email template, you can customize the content based on specific data.

You can import it like this: `import { renderHtml } from '@hefestos/core';`.

Example usage scenario for renderHtml:

Rendering a marketing email template with a user's name

```typescript
renderHtml("mails/marketing.nj", userName);
```

We recommend keeping email templates in the mails directory for better organization and maintainability.

You can import it like this: `import { renderHtml } from '@hefestos/core';`.

### File

The File module provides various utilities for handling file and directory operations. You can import the File module like this: `import { File } from '@hefestos/core';`.

```typescript
// Used to check if a file or directory exists.
// Return a boolean value.
File.exists("/file_path");

// User to rename a file or directory.
File.rename("/file_path/file_name", "/file_path/new_file_name");

// User to move a file to a new directory.
File.move("/old_path", "/new_path");

// User to delete a file or directory.
File.remove("/file_path");

// Used to load a stream and return a buffer.
// Expect a stream value.
// If you want to get a buffer from a file, use the File.createBuffer.
await File.loadStream(stream);

// Used to create a buffer from a file path.
// Return the buffer.
await File.createBuffer("/file_path");
```

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
