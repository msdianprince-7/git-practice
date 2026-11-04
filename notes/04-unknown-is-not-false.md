# "Unknown" is not the same as "false"

A capability check like `supports_function_calling(model)` returned `False` in two
different situations:

- the catalog says the model does not support tools
- the model is not in the catalog at all

The caller treated both as "remove the tools from the request". So every new model,
exactly the kind that is not catalogued yet, silently lost tool calling.

## Better shape

Return three states instead of two:

```python
def model_map_value(model: str) -> bool | None:
    try:
        value = lookup(model).get("supports_function_calling")
    except ModelNotFound:
        return None
    return value if isinstance(value, bool) else None
```

`None` means "nobody said". Only an explicit `False` should take something away
from the request.
