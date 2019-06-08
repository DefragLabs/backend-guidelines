# General python guidelines

## Prefer absolute imports over relative imports.

This is recommended in PEP8, as they improve readability.

## Require or ignore 2 fields

If we want the user to send both the query parameters or ignore both of them we can use the below code.

`bool(query_param1) ^ bool(query_param2)`

If the parameters are integer use the below

`bool(query_param1 is not None) ^ bool(query_param2 is not None)`

because the default value for an integer is 0 (Which is false in bool).

## String to boolean

Convert a string representation of truth to true (1) or false (0)

https://docs.python.org/3/distutils/apiref.html#distutils.util.strtobool

## Install a python package from github directly

In `requirements.py` add this line instead of `django-rest-auth==0.9.3`

```
-e git+git://github.com/Tivix/django-rest-auth.git#egg=django-rest-auth
```
This will install from `master` branch.

## Formatting import statements

Import statements should be grouped into 3 levels.

1. Built-in libraries
2. Third party libraries (Include Django)
3. Custom imports

```
import os
import datetime

from django.db import models

from posts.view import PostListView
```

Also order the imports based on the line length.

**wrong**
```
import datetime
import os

from django.db import models

from utils.response import set_response
from posts.view import PostListView
```

**correct**

```
import os
import datetime

from django.db import models

from posts.view import PostListView
from utils.response import set_response
```
