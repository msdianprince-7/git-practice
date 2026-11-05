# Precedence for capability settings

Once "unknown" became its own state, a reviewer pointed out a second source of
truth: a provider can declare a capability for all of its models.

The order I settled on, most specific first:

1. the model's own catalog entry, if it says true or false
2. the provider-wide setting, if the model has no opinion
3. otherwise keep the behaviour that does not silently drop user input

```python
def disabled(model, provider) -> bool:
    from_model = model_map_value(model)
    if from_model is not None:
        return not from_model
    return provider.info.get("supports_function_calling") is False
```

## Test every combination

Model (true, false, unknown) times provider (true, false, unset) is small enough to
parametrize. Seven cases covered every branch, including "model says yes, provider
says no".
