# Guidelines for api.

## Prefix all the api's

All the api's should be prefixed with `/api`

## Prefix all the auth related api's with auth

`/api/auth`

## Versioning

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

#### Implementation in django-rest-framework

Reference: https://www.django-rest-framework.org/api-guide/versioning/

## Http methods and response status codes to use.

|Method|Explanation|Status code success|Status code failure|
|------|-----------|-------------------|-------------------|
| `POST` | When a resource is to be created. | 201 - Created | 400 - Bad request |
| `PUT` | When a resource needs complete update. | 200 - Ok | 400 - Bad request |
| `PATCH` | When a resource needs partial update. | 200 - Ok | 400 - Bad request |
| `DELETE` | When a resource needs to be deleted. (Use this for soft-delete's as well). | 204 - No content | 404 - Not found |

**Status code**

- 403 - Forbidden. (Use this when the user doesn't have access to the resource, even when the user is logged in.)
- 401 - Unauthoried. (Use this when a logged out user tries to access a restricted resource)

_**Note:**_
There is a lot of discussion over the meaning of 403 & 401. But we have chosen to use the above.

#### Unique together validation in DRF.

By default serializer doesn't handle unique together errors. We have to add a `UniqueTogetherValidator`.

Example:

```
from rest_framework.validators import UniqueTogetherValidator

class StudentSerializer(serializers.ModelSerializer):

    class Meta:
        model = Student
        fields = '__all__'

        validators = [
            UniqueTogetherValidator(
                queryset=Student.objects.all(),
                fields=("name", "age")
            )
        ]
```
