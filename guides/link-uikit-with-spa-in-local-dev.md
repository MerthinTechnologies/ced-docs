# Link UIKit with SPA in local development environment

This will allow you to test changes in UIKit without having to deploy them.

## Build UIKit

Run from the root folder:

```bash
$ cd libs/internal/extensibility/ced-ui-kit
$ npm run build
```

## Use local build in SPA

From the root folder:

```bash
$ cd spa
$ npm run uikit:copy-local-build
$ npm run start
```

## Restore released UIKit

From the root folder:

```bash
$ cd spa
$ npm run uikit:remove-local-build
```
