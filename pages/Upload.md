## Upload

You can import the `upload` internal middleware from `core/middlewares` and pass it as middleware. The `upload` is a function that can receive an object with folder name. For example: `upload().single("file")` or `upload({ folder: 'images' }).single("file")`.

```typescript
import { Router } from "@hefestos/core";
import { upload } from "app/middlewares";

const routes = Router();

routes.post("/upload", upload().single("file"), (req, res) => {
  return res.json(req.file?.filename);
});

export default routes;
```

The `upload` internal middleware will upload to the local `uploads` directory. If you pass a folder as a parameter, this folder will be created within `uploads`. In the case of `upload({ folder: 'images' }).single("file")`, the "images" folder will be created within `uploads`, and the files sent via the "file" field will be stored within it.

To upload to an aws s3 bucket, you must import the `uploadTo` module from "modules/upload". For example:

```typescript
import { ApiResponse, AppError, Router } from "@hefestos/core";
import { upload } from "app/middlewares";
import { uploadTo } from "modules/upload";

const routes = Router();

routes.post("/media", upload().single("file"), async (request, response) => {
  try {
    if (!request.file) {
      throw AppError.E_VALIDATION_FAIL("The file is required.");
    }

    await uploadTo.s3({ fileName: request.file.filename, file: request.file });

    return ApiResponse.success(response, true);
  } catch (error: any) {
    return ApiResponse.error(response, error);
  }
});

export default routes;
```

### S3

Through the S3 module you can add or remove files from the s3 bucket. The S3 module has 2 functions `put` and `delete`.

`put` - expects to receive the parameters:

```typescript
key: string;
body: Buffer;
contentType: string;
```

Put example:

```typescript
const key = join(params.folder || "", params.fileName);
const body = await File.createBuffer(filePath);

const config = {
  key,
  body,
  contentType: "image/png",
};

await S3.put(config);
```

`delete` - expects to receive the parameters:

```typescript
fileName: string;
folder?: string;
```

Delete example:

```typescript
const media = {
  url: "file.jpg",
  userId: 2,
};

await S3.delete({ fileName: media.url, folder: media.userId });
```

PS: To upload files to S3, we recommend using the `uploadTo` module from "core/modules".

You can import the File module like this: `import { File } from 'core/modules';`.

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
