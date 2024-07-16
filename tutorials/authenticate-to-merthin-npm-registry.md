---
title: "Authenticate to Merthin NPM Registry" 
description: "Steps to authenticate to the Merthin NPM registry."
---

# Authenticate to Merthin NPM registry

This will give you access to all packages under `@ced`, `@merthin` and `@product-central` scopes.

```bash
$ npm config set "@ced:registry" https://npm.merthin.net/
$ npm config set "@merthin:registry" https://npm.merthin.net/
$ npm config set "@product-central:registry" https://npm.merthin.net/
```

Authenticate

```bash
npm login --registry https://npm.merthin.net/ --auth-type legacy
```

Get in touch with the team to get your credentials.
