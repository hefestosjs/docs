## Performance

To improve our application performance, we can use some strategies like cache, redis and compression.

Inside the `app/config/performance.ts` file, you can active redis, cache strategy and define cache life time in seconds. If cache and redis are active, we'll use redis to store the cache.

We can cache our query results like:

```typescript
  // app/services/UserService.ts

  static async index(currentPage: number = 1) {
    const perPage = 10;
    const page = currentPage ? currentPage : 1;
    const skip = (page - 1) * perPage;

    // Cache
    const key = `users.list.params=${skip}_${perPage}`;
    const cached = await useCache.get(key);

    if (cached) {
      return JSON.parse(cached);
    }

    // Queries
    const totalUsers = await User.count();
    const query = await User.findMany({ take: perPage, skip });
    const users = ResponseUtils.excludeFromList(query, ["password"]);

    const response = ResponseUtils.paginate({
      data: users,
      totalData: totalUsers,
      page,
      perPage,
    });

    await useCache.set(key, JSON.stringify(response));

    return response;
  }
```

From 100kb the response will be compressed with gzip. If you don't want to compress some page, you can pass `x-no-compression`header.

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
