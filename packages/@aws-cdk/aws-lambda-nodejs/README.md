## Amazon Lambda Node.js Library
<!--BEGIN STABILITY BANNER-->

---

![Stability: Experimental](https://img.shields.io/badge/stability-Experimental-important.svg?style=for-the-badge)

> **This is a _developer preview_ (public beta) module. Releases might lack important features and might have
> future breaking changes.**
>
> This API is still under active development and subject to non-backward
> compatible changes or removal in any future version. Use of the API is not recommended in production
> environments. Experimental APIs are not subject to the Semantic Versioning model.

---
<!--END STABILITY BANNER-->

This library provides constructs for Node.js Lambda functions.

To use this module, you will need to add a dependency on `parcel-bundler` in your
`package.json`:

```
yarn add parcel-bundler@^1
# or
npm install parcel-bundler@^1
```

### Node.js Function
Define a `NodejsFunction`:

```ts
new lambda.NodejsFunction(this, 'my-handler');
```

By default, the construct will use the name of the defining file and the construct's id to look
up the entry file:
```
.
├── stack.ts # defines a 'NodejsFunction' with 'my-handler' as id
├── stack.my-handler.ts # exports a function named 'handler'
```

This file is used as "entry" for [Parcel](https://parceljs.org/). This means that your code is
automatically transpiled and bundled whether it's written in JavaScript or TypeScript.

Alternatively, an entry file and handler can be specified:
```ts
new lambda.NodejsFunction(this, 'MyFunction', {
  entry: '/path/to/my/file.ts'
  handler: 'myExportedFunc'
});
```

All other properties of `lambda.Function` are supported, see also the [AWS Lambda construct library](https://github.com/aws/aws-cdk/tree/master/packages/%40aws-cdk/aws-lambda).

### Configuring Parcel
The `NodejsFunction` construct exposes some [Parcel](https://parceljs.org/) options via properties: `minify`, `sourceMaps`,
`buildDir` and `cacheDir`.

Parcel transpiles your code (every internal module) with [@babel/preset-env](https://babeljs.io/docs/en/babel-preset-env) and uses the
runtime version of your Lambda function as target.

Configuring Babel with Parcel is possible via a `.babelrc` or a `babel` config in `package.json`.
