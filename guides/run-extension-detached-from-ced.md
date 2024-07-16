# Run extension detached from CED core

This tutorial applies to all kind of extensions.

CED extensions need to run inside CED. This is not convenient for the first stages of local development of extensions. To overcome this requirement you can mock the `core` object obtained from the `attachToCore` function.

## Create a mocked core

Create a mocked core implementing `CoreInterface`. The implementation will depend on the type of extension.

```typescript
import { CoreInterface } from '@ced/example-extension';

export const coreMock: CoreInterface = {
  getUser: async () => ({
    email: 'user@ced.com',
  }),
  isUserAdmin: async () => true,
  getAccessToken: async () => '1234567890',
  getOrganization: async () => 'MyOrganization',
  getCoreApiBaseUrl: async () => 'https://core-api.ced-dev.merthin.systems',
  goToRoute: async (url: string) => console.log(`Requested core route: ${url}`),
  setLoading: async (value: boolean) =>
    console.log(`Changed core loading state: ${value}`),
  unload: async () => console.log(`Unloaded extension`),
};
```

## Use the mocked core

Change the call to `attachToCore` so it receives the mock.

```typescript
const core = await attachToCore({
  coreInterfaceMock: coreMock, //Use mocked core
});
```

## Run the extension locally

Run the extension in local development environment with whatever script you defined for that. For instance `npm run start`.

You should be able to see the extension working with the mocked data. A message in the JavaScript console "Running extension with mocked core interface." will indicate that the extension is effectively running with the mocked core.
