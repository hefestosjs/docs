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
