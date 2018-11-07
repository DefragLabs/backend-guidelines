## Guidelines for api.

### Prefix all the api's

All the api's should be prefixed with `/api`

### Versioning

There are 3 ways of implementing versioning

1. Mention the version in the headers.
2. In query parameter
3. In url path

#### Version in header

An api request can include `Accept` header. This is how github api works.

`Accept: application/vnd.github.v3+json`

The format is `application/vnd.yourcompany.version+json`

Reference: https://developer.github.com/v3/

#### Query parameter 

Version number can be included in the query param. `?v=1.0`

#### Url path

Version number can be included in the url as a path parameter.

/api/{version-number}/resource
