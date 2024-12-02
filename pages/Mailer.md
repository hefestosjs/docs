## Mailer

First you need to set the `SMTP_HOST, SMTP_PORT, SMTP_USER and SMTP_PASSWORD` environment variables.

To send emails, we will use the sendMail function of the Mailer class, which is located in the vendor/mail directory.

**Example:**

```typescript
await Mailer.sendMail({
  from: "your_email@email.com",
  to: "user_email@email.com",
  subject: "E-mail Subject",
  text: "E-mail message",
  html: "HTML code in string format",
});
```

We recommend using the renderHtml function that you can import from `@hefestos/core` to turn your HTML email template into a string. We also recommend that you always send the email message in text in addition to HTML.

In renderHtml you will pass the file path with extension, for example: `renderHtml("mails/contact.nj");`

We recommend keeping email templates in the mails directory.

**Complete Example:**

```typescript
import { ApiResponse, renderHtml } from "@hefestos/core";

const routes = Router();

routes.post("/mail", async (request, response) => {
  try {
    const htmlString = renderHtml("mails/contact.nj");

    await Mailer.sendMail({
      from: "your_email@email.com",
      to: "user_email@email.com",
      subject: "E-mail Subject",
      text: "E-mail message",
      html: htmlString,
    });

    return ApiResponse.success(response);
  } catch (error: any) {
    return ApiResponse.error(response, error);
  }
});

export default routes;
```

_We use the nodemailer library, for more information visit its official documentation._

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
