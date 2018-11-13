# General python guidelines

## Prefer absolute imports over relative imports.

This is recommended in PEP8, as they improve readability.

## Require or ignore 2 fields

If we want the user to send both the query parameters or ignore both of them we can use the below code.

`bool(query_param1) ^ bool(query_param2)`

If the parameters are integer use the below

`bool(query_param1 is not None) ^ bool(query_param2 is not None)`

because the default value for an integer is 0 (Which is false in bool).
