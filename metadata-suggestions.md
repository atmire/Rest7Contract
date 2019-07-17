# Metadata suggestions from live import
[Back to the index](README.md)

**Contents:**

* [Introduction](#introduction)
* [Adding metadata](#adding-metadata)
* [Replacing metadata](#replacing-metadata)

## Introduction

TODO: list of live import sources
perform a query or reference a bitstream. Different query syntax depending on the sources. Query syntax could be shared for some sources
search results: should display all metadata from the suggestions, not just the change to the metadata. Preferably similar to the discovery results to reuse that component
actual suggestions: can we reuse the details from the search results?
 
The live import can suggest metadata from various sources.
The user should be given the choice to apply or ignore the metadata changes.

The suggestions will be presented in a format compatible with the [Metadata Patch](metadata-patch.md)
to allow the user-interface to easily apply the suggested changes.

The examples in each section below build on each other, assuming an initial metadata state of:

```json
{
  "metadata": {
    "dc.title": [
      { "value": "Initial Title", "language": null, "authority": null, "confidence": -1 }
    ]
  }
}
```

The user interface can display the suggested metadata, and request the user to accept or reject the changes.
If accepted, the user interface can perform a PATCH based on the suggested metadata changes to apply the suggestions.

## Adding metadata

With the `add` operation, the live import suggests to add metadata new values.

The `add` can also be used to effectively _replace_ all values for a given metadata key, by specifying
an already-present key as the `path`, and an array of replacement values as the `value`.
This use of the add operation to replace a list of values may be counter-intiutive, but it
is done according to the [RFC section 4.1](https://tools.ietf.org/html/rfc6902#section-4.1)

> If the target location specifies an object member that does exist, that member's value is replaced.

Note:

* According to the [JSON Patch specification](https://tools.ietf.org/html/rfc6902), to initialize the first
  value for any array, the `add` operation must receive an array of values. Therefore, in the first operation
  below, since it is not possible to add a single value to the not yet initialized `/metadata/dc.description`
  array, we initialize it with an array with one value.
* When values already exist for a metadata key, as in the second operation below, it is necessary to specify
  the new value's position at the end of the `path` (`/0` means first position, `/-` means last).
* When creating new metadata values, if unspecified, the `language` and `authority` properties
  default to `null`, and `confidence` defaults to `-1`.

Example response, suggestion the addition of three values:

```json
[
  {
    "op": "add",
    "path": "/metadata/dc.description",
    "value": [ { "value": "Some description" } ]
  },
  {
    "op": "add",
    "path": "/metadata/dc.title/0",
    "value": { "value": "Zeroth Title" }
  },
  {
    "op": "add",
    "path": "/metadata/dc.title/-",
    "value": { "value": "Final Title", "language": "en_US" }
  }
]
```

If this patch is applied hereafter, the new metadata state is:

```json
{
  "metadata": {
    "dc.description": [
      { "value": "Some description", "language": null, "authority": null, "confidence": -1 }
    ],
    "dc.title": [
      { "value": "Zeroth Title", "language": null, "authority": null, "confidence": -1 },
      { "value": "Initial Title", "language": null, "authority": null, "confidence": -1 },
      { "value": "Final Title", "language": "en_US", "authority": null, "confidence": -1 }
    ]
  }
}
```

## Replacing metadata

With `replace`, the live import suggests to overwrite any of the following within a single operation
of a PATCH request:

* The entire set of all object metadata (`path="/metadata"`)
* All metadata values for an existing key (e.g. `path="/metadata/dc.title"`)
* A single existing metadata value (e.g. `path="/metadata/dc.title/0"`)
* A single property of an existing value (e.g. `path="/metadata/dc.title/0/language"`)

Example response, replacing the `value` and `language` of the first `dc.title`:

```json
[
  {
    "op": "replace",
    "path": "/metadata/dc.title/0",
    "value": { "value": "最後のタイトル", "language": "ja_JP" }
  }
]
```

If this patch is applied hereafter, the new metadata state is:

```json
{
  "metadata": {
    "dc.title": [
      { "value": "最後のタイトル", "language": "ja_JP", "authority": null, "confidence": -1 },
      { "value": "Initial Title", "language": null, "authority": null, "confidence": -1 },
      { "value": "Final Title", "language": "en_US", "authority": null, "confidence": -1 }
    ]
  }
}
```
