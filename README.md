# Wired Relations API documentation

To access the Wired Relations API you need 
1. The name of your tenant (aka tenantName, org or site)
2. The id of your tenant (tenantId aka orgId)
3. Username and password for an api-access user (please contact Wired Relations Customer Support to request this)

With that in hand you can [Authenticate](#authentication) to get an access token, and then you can access the [API](#api).


# Authentication

The Wired Relations API is accessed through REST resources, but before you can access those, you need an access token.
You get that by either authenticating, or, if you already did that, by using a refresh token to get a new set of tokens.


## Log In / Authentication

To log in, make a POST request on https://api2.wiredrelations.com/org/{{orgId}}/auth/token with username and password in the
request body, like this:

`POST https://api2.wiredrelations.com/org/af6d0e70-18f5-41ce-b5bb-df709358d523/auth/token`
```json
{
    "grant_type": "Bearer",
    "usernameOrEmail": "api-read-only-user",
    "password": "RWd8!777A$vL%@9f60"
}
```

You can use the above url and credentials to get read-only access to a demo tenant.
The response will be like this:
```json
{
    "accessToken": "eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJvcmciOiJhcGlkZW1vIiwibmFtZSI6IkFQSSBVc2VyIiwiZXhwIjoxNzExNTMyODA2LCJ1c2VySWQiOiJlNTljN2MzNy1kOWViLTQ4MGUtYWUxZi1mYmU1MzE2MDQ2ZjYiLCJpYXQiOjE3MTE1MjkyMDYsIm9yZ0lkIjoiYWY2ZDBlNzAtMThmNS00MWNlLWI1YmItZGY3MDkzNThkNTIzIiwiZW1haWwiOiJhcGktcmVhZC1vbmx5LXVzZXIiLCJhdXRob3JpdGllcyI6W3siYXV0aG9yaXR5IjoiUkVBRF9PTkxZIn1dLCJtb2R1bGVzIjoie1wic3ViRG9tYWluXCI6XCJhcGlkZW1vXCIsXCJiZXRhRmVhdHVyZXNcIjpbXSxcIm1vZHVsZXNFbmFibGVkXCI6W1wiQVNTRVNTTUVOVFwiLFwiUFJPQ0VTU0lOR19BQ1RJVklUSUVTXCIsXCJSSVNLU19WMlwiLFwiVEFTS19UWVBFU1wiLFwiV1JfTE9HSU5cIixcIkdNQUlMXCJdLFwicXVlc3Rpb25uYWlyZVwiOntcInZlcnNpb25cIjoyfSxcImN1c3RvbWVyc1wiOntcImVuYWJsZWRcIjpmYWxzZX0sXCJyaXNrc1wiOntcImVuYWJsZWRcIjpmYWxzZX0sXCJyaXNrc1YyXCI6e1wiZW5hYmxlZFwiOnRydWV9LFwicHJlbWl1bVwiOntcImxhYmVsc1wiOmZhbHNlfSxcImF6dXJlXCI6e1wiZW5hYmxlZFwiOmZhbHNlfSxcImFkdmFuY2VkQ29udHJvbHNcIjp7XCJlbmFibGVkXCI6ZmFsc2V9LFwiZ29vZ2xlXCI6e1wiZ3N1aXRlXCI6ZmFsc2UsXCJnbWFpbFwiOnRydWUsXCJzc29cIjpmYWxzZX0sXCJncm91cE9yZ2FuaXphdGlvblwiOntcImVuYWJsZWRcIjpmYWxzZX0sXCJraXRvc1wiOntcImVuYWJsZWRcIjpmYWxzZX0sXCJjdXN0b21RdWVzdGlvbm5haXJlXCI6e1wiZW5hYmxlZFwiOmZhbHNlfSxcImdvdmVybmFuY2VcIjp7XCJlbmFibGVkXCI6dHJ1ZSxcImN1c3RvbVwiOmZhbHNlLFwiaXNvMjcwMDJcIjpmYWxzZSxcImlzbzI3NzAxXCI6ZmFsc2UsXCJpc2FlMzAwMFwiOmZhbHNlLFwiaXNvMjcwMDJfMjAyMlwiOmZhbHNlfSxcImNvbnRyYWN0c1wiOntcImVuYWJsZWRcIjpmYWxzZX0sXCJzdWJwcm9jZXNzb3JcIjp7XCJlbmFibGVkXCI6ZmFsc2V9LFwiYXNzZXNzbWVudFwiOntcImVuYWJsZWRcIjp0cnVlfSxcInRvZG9UYXNrRXZhbHVhdGlvblwiOntcImVuYWJsZWRcIjpmYWxzZX0sXCJ1dWlkXCI6XCJhZjZkMGU3MC0xOGY1LTQxY2UtYjViYi1kZjcwOTM1OGQ1MjNcIn0iLCJ1c2VybmFtZSI6bnVsbH0.9C46phmQ0acQu0fSO5YMLYaHeQHpYQHWiJuD4Ay0dRdFM_LIF2x9myOT7Tml2kKwCDDjMiqnlkjuT56fqAqz8g",
    "refreshToken": "4f7d09a1-46cf-42ee-8783-00f1f3d43d33",
    "expiresInSeconds": 86400,
    "tokenType": "Bearer"
}
```
__`accessToken`__ and __`tokenType`__ is what you need to provide as bearer token on requests.
Ie. send a HTTP header named "Authorization" with the value constructed by concatenating tokenType and accessToken with a space between.

The access token is a JWT (JSON Web Token). When you decode it (you can do that on eg. https://jwt.io), you will see that it has these properties (and more):
```json
{
  "org": "apidemo",
  "name": "API User",
  "exp": 1711532806,
  "userId": "e59c7c37-d9eb-480e-ae1f-fbe5316046f6",
  "iat": 1711529206,
  "orgId": "af6d0e70-18f5-41ce-b5bb-df709358d523",
  ... (other properties removed for brevity)
}
```
JWTs are described in great detail in [RFC 7519](https://datatracker.ietf.org/doc/html/rfc7519), but the only thing you really need to use is the
expiry time (the `exp` property). It is a Unix timestamp, and it tells when the token expires.
Please do not make any requests with expired tokens. Before each request, check if the token is still valid, and if not, use the `refreshToken`
to get a new one, as described below.

__`refreshToken`__ is for refreshing tokens as described in the next section.

__`expiresInSeconds`__ tells for how long the refresh token is valid.

## Refreshing tokens

Access tokens have a relatively short validity period. When one expires you will need to get a fresh one using the `refreshToken` you received with
the access token. Refresh tokens can be used only once. When you use one, you get both a new access token and a new refresh token.

Token refresh is done using the same endpoint as authentication, but with `"grant_type": "token_refresh"`, so a request could look like this:
`POST https://api2.wiredrelations.com//org/af6d0e70-18f5-41ce-b5bb-df709358d523/auth/token`
```json
{
    "grant_type": "token_refresh",
    "refresh_token": "c5011b3f-b8e6-4a5e-b395-59c7a0c7329a"
}
```
The response is identical to the authentication response:
```json
{
    "accessToken": "eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJvcmciOiJhcGlkZW1vIiwibmFtZSI6IkFQSSBVc2VyIiwiZXhwIjoxNzExNTM5NTU5LCJ1c2VySWQiOiJlNTljN2MzNy1kOWViLTQ4MGUtYWUxZi1mYmU1MzE2MDQ2ZjYiLCJpYXQiOjE3MTE1MzU5NTksIm9yZ0lkIjoiYWY2ZDBlNzAtMThmNS00MWNlLWI1YmItZGY3MDkzNThkNTIzIiwiZW1haWwiOiJhcGktcmVhZC1vbmx5LXVzZXIiLCJhdXRob3JpdGllcyI6W3siYXV0aG9yaXR5IjoiUkVBRF9PTkxZIn1dLCJtb2R1bGVzIjoie1wic3ViRG9tYWluXCI6XCJhcGlkZW1vXCIsXCJiZXRhRmVhdHVyZXNcIjpbXSxcIm1vZHVsZXNFbmFibGVkXCI6W1wiQVNTRVNTTUVOVFwiLFwiUFJPQ0VTU0lOR19BQ1RJVklUSUVTXCIsXCJSSVNLU19WMlwiLFwiVEFTS19UWVBFU1wiLFwiV1JfTE9HSU5cIixcIkdNQUlMXCJdLFwicXVlc3Rpb25uYWlyZVwiOntcInZlcnNpb25cIjoyfSxcImN1c3RvbWVyc1wiOntcImVuYWJsZWRcIjpmYWxzZX0sXCJyaXNrc1wiOntcImVuYWJsZWRcIjpmYWxzZX0sXCJyaXNrc1YyXCI6e1wiZW5hYmxlZFwiOnRydWV9LFwicHJlbWl1bVwiOntcImxhYmVsc1wiOmZhbHNlfSxcImF6dXJlXCI6e1wiZW5hYmxlZFwiOmZhbHNlfSxcImFkdmFuY2VkQ29udHJvbHNcIjp7XCJlbmFibGVkXCI6ZmFsc2V9LFwiZ29vZ2xlXCI6e1wiZ3N1aXRlXCI6ZmFsc2UsXCJnbWFpbFwiOnRydWUsXCJzc29cIjpmYWxzZX0sXCJncm91cE9yZ2FuaXphdGlvblwiOntcImVuYWJsZWRcIjpmYWxzZX0sXCJraXRvc1wiOntcImVuYWJsZWRcIjpmYWxzZX0sXCJjdXN0b21RdWVzdGlvbm5haXJlXCI6e1wiZW5hYmxlZFwiOmZhbHNlfSxcImdvdmVybmFuY2VcIjp7XCJlbmFibGVkXCI6dHJ1ZSxcImN1c3RvbVwiOmZhbHNlLFwiaXNvMjcwMDJcIjpmYWxzZSxcImlzbzI3NzAxXCI6ZmFsc2UsXCJpc2FlMzAwMFwiOmZhbHNlLFwiaXNvMjcwMDJfMjAyMlwiOmZhbHNlfSxcImNvbnRyYWN0c1wiOntcImVuYWJsZWRcIjpmYWxzZX0sXCJzdWJwcm9jZXNzb3JcIjp7XCJlbmFibGVkXCI6ZmFsc2V9LFwiYXNzZXNzbWVudFwiOntcImVuYWJsZWRcIjp0cnVlfSxcInRvZG9UYXNrRXZhbHVhdGlvblwiOntcImVuYWJsZWRcIjpmYWxzZX0sXCJ1dWlkXCI6XCJhZjZkMGU3MC0xOGY1LTQxY2UtYjViYi1kZjcwOTM1OGQ1MjNcIn0iLCJ1c2VybmFtZSI6bnVsbH0.IQ9TCweNXnbvJhm0RAxgg57-J6QfMAcRWRPVUYpZlccm-cBTmlNWL9ewaV8B7W4qASLulYMExRFFI3a8UZRCiQ",
    "refreshToken": "30262ac2-1332-411d-9bee-3fa5c54ef875",
    "expiresInSeconds": 86400,
    "tokenType": "Bearer"
}
```

## Changing password

When you request API access Wired Relations will send you a username and password. The first thing you should do, when you receive this, is to change the password.

You can do that with the `setMyPassword` operation.:

`POST https://api2.wiredrelations.com/org/{{orgId}}/auth/setMyPassword`
```json
{
  "newPassword": "string"
}
```

# API

The API is a basic REST API documented with OpenAPI (Swagger). For an introduction to Swagger please refer to [swagger.io/specification/v3](https://swagger.io/specification/v3/).

The OpenAPI file (yaml) is available at https://api2.wiredrelations.com/api-service/api-docs.yaml

You can use the Swagger Editor to browse our API. Import our OpenAPI file here: [Swagger Editor](https://editor-next.swagger.io/).
The Swagger Editor can also help you generate client code in various languages. 

Another good tool for working with REST APIs is Postman.

You can either:
- import the OpenAPI file into Postman, and then you can use the Postman collection to make requests to the API, or
- use the Postman collection directly from: [Postman Collection](./postman/WiredRelationsPublicAPI_prod.postman_collection_2_1.json)

Regardless which tool you use, you need to first get an access token as described in the [Authentication](#authentication) section, and provide that in the `Authorization` header on all requests.

## Pagination and ordering


Key elements for pagination and sorting:

__`page`__:
Zero-based page index (0..N). The page to be returned.

__`size`__:
The size of the page to be returned

__`sort`__:
Sorting criteria in the format: property,(asc|desc). Default sort order is ascending. Multiple sort criteria are supported.



## Reference Documentation

- JWT (rfc7519): https://datatracker.ietf.org/doc/html/rfc7519
- Swagger OpenAPI Specification: https://swagger.io/specification/v3/
- Pagination (Spring): https://docs.spring.io/spring-data/rest/reference/paging-and-sorting.html
- JSON Patch (rfc6902): https://datatracker.ietf.org/doc/html/rfc6902



