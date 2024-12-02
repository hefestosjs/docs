### Authentication Configuration

This application supports two authentication strategies: **Session-based** and **Token-based**. You can configure options such as the database table, unique sign-in column, strategy type, and more in the `app/config/auth.ts` file.

```typescript
const auth: AuthConfig = {
  option: "session", // Choose "session" or "token"
  table: "users",
  uniqueColumn: "email",
  strategy: {
    token: {
      secret: process.env.JWT_SECRET || "secret",
      expiresIn: "30d",
      useRedis: true,
    },
    session: {
      genid: () => randomUUI(),
      useRedis: true,
      prefix: "myapp:", // Prefix for RedisStore keys
      secret: process.env.SESSION_SECRET || "secret",
      resave: false, // Forces session persistence even if unmodified
      saveUninitialized: false, // Saves session only if data exists
      cookie: {
        secure: SecurityPolicy.ssl,
        httpOnly: true, // Prevents client-side access to the cookie
        maxAge: 90 * 24 * 60 * 60 * 1000, // 3 months in milliseconds
        sameSite: "lax",
      },
    },
  },
};
```

---

### API Session Strategy

To enable session-based authentication, set `option` to `"session"` in `app/config/auth.ts`.

**Login Example:**

```typescript
static async store(request: Request, response: Response, next: Next) {
  try {
    const { email, password } = request.body;
    const user = await SessionService.getUser(email, password); // Validate credentials

    const userSession = await useAuth.login({
      session: { request, response, next, user },
    });

    return ApiResponse.success(response, { session: userSession });
  } catch (error: any) {
    return ApiResponse.error(response, error);
  }
}
```

**Route Authentication:**

```typescript
useRouter.get("/", isAuthenticated, (req, res) => res.send("Authenticated"));
```

**Logout Example:**

```typescript
static async destroy(request: Request, response: Response, next: Next) {
  try {
    await useAuth.logout({ session: { request, session } });
    return ApiResponse.success(response, { message: "Logged out" });
  } catch (error: any) {
    return ApiResponse.error(response, error);
  }
}
```

---

### Full Stack Session Strategy

To enable session-based authentication for full-stack applications, set the `option` to `"session"` in `app/config/auth.ts`.

#### **Login Example:**

```typescript
static async store(request: Request, response: Response, next: Next) {
  try {
    const { email, password } = request.body;
    const user = await SessionService.getUser(email, password); // Validate credentials

    // Initiates login and redirects to the specified path
    useAuth.login({ request, response, next, user, redirectPath: "/dashboard" });
  } catch (error: any) {
    console.log(error);

    // Handle errors here...
  }
}
```

#### **Route Authentication:**

Use the `isAuthenticated` middleware to protect routes.

```typescript
useRouter.get("/dashboard", isAuthenticated, (req, res) =>
  res.send("Authenticated")
);
```

#### **Logout Example:**

```typescript
static async destroy(request: Request, response: Response, next: Next) {
  try {
    // Logs the user out and redirects to the specified path
    useAuth.logout({ request, response, next, redirectPath: "/" });
  } catch (error: any) {
    console.log(error);

    // Handle errors here...
  }
}
```

### Notes:

- `redirectPath` specifies where to redirect users after login or logout.
- Customize error handling as needed to fit your application's logic.

---

### Token Strategy

To enable token-based authentication, set `option` to `"token"` in `app/config/auth.ts`.

**Login Example:**

```typescript
static async store(request: Request, response: Response, next: Next) {
  try {
    const { email, password } = request.body;
    const user = await SessionService.getUser(email, password); // Validate credentials

    const userToken = await useAuth.login({
      token: { userId: user.id },
    });

    return ApiResponse.success(response, { token: userToken });
  } catch (error: any) {
    return ApiResponse.error(response, error);
  }
}
```

**Route Authentication:**

```typescript
useRouter.get("/", isAuthenticated, (req, res) => res.render("home"));
```

**Logout Example:**

```typescript
static async destroy(request: Request, response: Response, next: Next) {
  try {
    const result = await useAuth.logout({
      token: { request, response },
    });

    return ApiResponse.success(response, result);
  } catch (error: any) {
    return ApiResponse.error(response, error);
  }
}
```

> **Note:** For token-based authentication, use the `Authorization` header:  
> `Authorization: Bearer {{token}}`, replacing `{{token}}` with the token returned by `Auth.login`.

---

### Redis Integration

Both **session** and **token** strategies support Redis for storing authentication data. To use Redis:

1. Set `useRedis` to `true` in `app/config/auth.ts`.
2. Ensure Redis is enabled in `app/config/performance.ts`.

You can further customize Redis-related behavior in the `module/auth` directory if needed.

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
