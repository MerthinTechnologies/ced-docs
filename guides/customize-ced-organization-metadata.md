# Customize CED organization metadata

Navigate to Product Central GraphQL

Development:

```
https://api.product-central-dev.merthin.systems/graphql
```

Production:

```
https://api.product.merthin.com/graphql
```

Run the following mutation as a `TenantAdmin` after replacing placeholders:

- `<organization-id>`: Id of the organization to customize.
- `<organization-icon-url>`: Optional. Custom icon of the organization.
- `<display-name>`: Optional. Display name of the organization
- `<stripe-customer-id>`: Stripe customer id associated to the organization.

```graphql
mutation {
  setOrganizationMetadata(
    id: "<organization-id>"
    metadata: [
      { key: "iconUrl", value: "<organization-icon-url>" }
      { key: "displayName", value: "<display-name>" }
      { key: "stripeCustomerId", value: "<stripe-customer-id>" }
    ]
  )
}
```

Run this query to check existing metadata in an organization:

- `<organization-name>`: Name of the organization to customize.

```graphql
{
  organizationByName(name: "<organization-name>") {
    id
    name
    metadata {
      key
      value
    }
  }
}
```
