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
