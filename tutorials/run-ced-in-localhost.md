# Run CED in localhost

Follow these steps to run CED in localhost. Make sure to have [access to Merthin NPM Registry](./authenticate-to-merthin-npm-registry.md) before continuing.

## Run Core API

Run these commands in the [Core API folder](../../backend/core-api/).

Install dependencies

```bash
$ npm install
```

Build project

```bash
$ npm run build
```

Create `CED_ENCRYPTION_KEY` environment variable for CED data access encryption key.

```
CED_ENCRYPTION_KEY=DEV12345678901234567890123456789
```

Run Core API

```bash
$ npm run start
```

## Run SPA

Run these commands in the [SPA folder](../../spa/).

Install dependencies

```bash
$ npm install
```

Run the SPA in dev mode

```bash
$ npm run start
```

Navigate to http://localhost:4200/ and [signin to CED in localhost](./sign-in-to-ced-localhost.md).
