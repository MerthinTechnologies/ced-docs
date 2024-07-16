# Signin to CED localhost

CED always uses `Merthin` organization in localhost. You'll need to have an active session in `Merthin` organization within CED Dev in order to run CED in localhost.

Make sure you have both, [SPA](../../spa/) and [Core API](../../backend/core-api/) running locally before continuing.

## Signin in CED from localhost

1. Go to [Product Central Dev using Merthin organization](https://product-central-dev.merthin.systems/login?org=Merthin)
1. Authenticate with your credentials. It'll take you to CED Dev, notice the url, you're not in local-dev yet.
1. Navigate to CED local-dev http://localhost:4200/

## Change user

1. Navigate to CED local-dev http://localhost:4200/ and logout if there's an active session.
1. Navigate to CED Dev https://ced-dev.merthin.systems/ and logout if there's an active session.
1. Follow the instructions from above to signin from localhost
