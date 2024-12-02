## Database

We use Prisma ORM to handle the database. You can create new models from the schema.prisma file located in the `app/database/schema.prisma` directory. You can also export the models, for easier use, from `app/database/index.ts`.

In the .env file, the DB_URL variable changes according to the bank you choose, being:

- PostgreSQL: `DB_URL=postgresql://${DB_USER}:${DB_PASS}@${DB_HOST}:${DB_PORT}/${DB_NAME}`
- MySQL: `DB_URL=mysql://${DB_USER}:${DB_PASS}@${DB_HOST}:${DB_PORT}/${DB_NAME}`
- SQLite: `DB_URL="file:./dev.db"`

### Raw Queries

If you need to execute raw queries, you can use the Database handler located in `app/database/database.ts`. This handler provides an abstraction over Prisma's native functions, making it easier to work with database operations.

For example, instead of doing:

```typescript
const [posts, totalPosts] = await prisma.$transaction([
  prisma.post.findMany({ where: { title: { contains: "prisma" } } }),
  prisma.post.count(),
]);
```

You can use the Database handler like this:

```typescript
const [posts, totalPosts] = await Database.transaction([
  Post.findMany({ where: { title: { contains: "prisma" } } }),
  Post.count(),
]);
```

This abstraction allows you to interact with your models in a more streamlined way, making your code cleaner and easier to maintain.

The Database handler provides the following methods for interacting with the database:

- `transaction`: Executes multiple Prisma operations in a transaction.
- `queryRaw`: Executes a raw SQL query (returns data).
- `queryRawUnsafe`: Executes a raw SQL query with potentially unsafe queries (use with caution).
- `executeRaw`: Executes a raw SQL command (does not return data).
- `executeRawUnsafe`: Executes a raw SQL command with potentially unsafe queries (use with caution).

Each of these methods is bound to Prisma's corresponding functions, allowing for consistent use across your application.

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
