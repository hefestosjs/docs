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
