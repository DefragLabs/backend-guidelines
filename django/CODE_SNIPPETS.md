## Useful code snippets in django.

### Query parameters in django-rest-swagger

Using django-rest-swagger doesn't give option in the ui for the user to enter the query parameters.
Use the below decorator to bring it up in the ui.

**Usage:**
```
@additional_query_schema(
    [
        {'name': 'archived'},
        {'name': 'sort'},
        {'name': 'search'}
    ]
)
class JobPostView(GenericAPIView):

```

**Code for the decorator.**
```
def additional_query_schema(params):
    """
    rest framework does not provide a way to override the schema on
    a per endpoint basis.  this is a cheap way to get the fields to
    appear on the swagger web interface through the filter_backends
    """
    class SwaggerFilterBackend(object):
        def get_schema_fields(self, view):
            schema_list = []
            for param in params:
                # required = requred.get('required') if 'required' in param else False
                schema_list.append(
                    (param.get('name'), {
                        'name': param.get('name'),
                        'required': param.get('required') if 'required' in param else False,
                        'location': param.get('location') if 'location' in param else 'query',
                        'type': param.get('type') if 'type' in param else 'string',
                        'description': param.get('desc') if 'desc' in param else param.get('name')
                    })
                )

            schema = OrderedDict(schema_list)
            keys = ('name', 'required', 'location', 'type', 'description')
            return [
                coreapi.Field(**{
                    key: val for key, val in field.items() if key in keys})
                for field in schema.values()
                ]

        def filter_queryset(self, request, queryset, view):
            # do nothing
            return queryset

    def wrapper(cls):
        cls.filter_backends = [SwaggerFilterBackend]
        return cls

    return wrapper
```
