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
