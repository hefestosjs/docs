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
