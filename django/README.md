## Django guidelines

### Use the name of the model, rather than the model object itself:
For models foreign keys use string format (`app.Model`) instead of actually importing the models. This will reduce
the probability of circular imports.

If the foreign key is in the same model file then mention the name of the model in string without app name (`Model`).
