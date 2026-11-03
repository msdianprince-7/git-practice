# Proving an API proxy fix without provider keys

A bug fix in a proxy is best shown end to end, but I did not have a key for the
provider involved. What worked instead:

1. Run the real proxy with the model's `api_base` pointed at `http://127.0.0.1:8765`
2. Run a tiny HTTP server on that port that logs the JSON body it receives and
   answers with a canned chat completion
3. Send the same curl request with the old code and with the fix
4. Compare what the "provider" received

Everything between the curl and the outgoing request is the real code path. Only
the provider at the end is fake.

## Example result

Before the fix the upstream body had `"tools": null`. After, it carried the tool
definition and `"tool_choice": "auto"`. Both runs returned HTTP 200, which is
exactly why the bug was silent.

Say clearly in the PR that no billed call was made.
