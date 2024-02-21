## Flipt Test Corpus

There are many places in flipt where we need to synchronize functionality of evaluations for consistency purposes. The goal of this repository is to provide a single source of truth for evaluation request payloads and the expectation as those payloads are evaluated.

Currently, there are three repos that will benefit from this corpus:
- `flipt`
- `flipt-client-sdks`
- `flipt-server-sdks`

Flipt provides the amazing functionality of potentially sourcing its data from a git repository which means the server can just watch the `testdata` directory here.

Wherever this test corpus is being leveraged (probably in CI), it would have to download the `tests.json` and it would be up to the language of interest to make sense of the JSON file.

The structure of the `tests.json` is as follows:

```json
{
    "VARIANT": [
        {
            "request": {
                // Request information
            },
            "expectation": {
                // Expectation that the response should match
            }
        }
    ],
    "BOOLEAN": [
        ...
    ],
    "BATCH": [
        ...
    ]
}
```

`variant`, `boolean`, and `batch` are separated because they need to be deserialized differently, as you would imagine. So it should be as simple as deserializing the `tests.json`, and running through each array providing the `request` to the client, and asserting against the response with the `expectation`.
