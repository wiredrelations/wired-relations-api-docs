# wired-relations-api-docs
Wired Relations API documentation

To access the Wired Relation API you need 
1. The name of your tenant (tenantName aka org aka site)
2. The id of your tenant (tenantId aka orgId)
3. User-name and password for an api-access user (please contace Wired Relation Customer Support to get this)

# Authentication

With very few exceptions the Wired Relations API is accessed through a Graph-QL interface, but before you can access that you need an access token.
To get that make a POST request on https://{tenantName}.wiredrelations.com/user-management/org/{tenantId}/token2 with user-name and password in the
request body, like this:

POST https://apidemo.wiredrelations.com/user-management/org/af6d0e70-18f5-41ce-b5bb-df709358d523/token2
```json
{
    "grant_type": "Bearer",
    "usernameOrEmail": "api-read-only-user",
    "password": "RWd8!777A$vL%@9f60"
}
```

# Graph QL

TODO: graphiql and schema browsing has been disabled for the prod environment -why? And shouldn't we enable that?

The GraphQL schema is available at https://x.wiredrelations.dk/graphql2-service/graphql/schema

You can use GraphiQL to browse the schema and access the API. It is available at https://x.wiredrelations.dk/graphql2-service/graphiql
