# Tags

Tags are used to categorize providers according to the type of leisure they offer, for example: *Theme parks*, *Shows*, *Museums*, *Concerts*, etc.

The identifiers of the assigned tags can be seen in the [catalog](catalog.md) at provider level.

## Access method

**GET** /activity/tags

## Request structure

- **``LanguageCode``** (`string`): identifier of the language in which we want to obtain the tags. *ISO 639-1 format*.

### Request examples

--8<-- "includes/examples/activity/tagsQueryExamples.md"

## Response structure

- **``Tags``** (`list`): array of tags.
    - **`Tag`** (`object`): tag.
        - **``Id``** (``string``): tag identifier. 13-character alphanumeric.
        - **``Key``** (``int``): tag key. Unique integer value across all tags.
        - **``Name``** (``string``): tag name (for example "*Theaters and shows*").
        - **``PathName``** (``string``): tag path separated by "/" if it has child tags (for example "Theaters and shows / Concerts").
        - **``Children``** (``list``): child tags of the current tag. The nesting level is infinite, so there may be tags with a depth of N children. The child tag structure is the same as the parent tag structure.

--8<-- "includes/responseBaseDocumentation.en.md"

### Response example

--8<-- "includes/examples/activity/tagsResponseExamples.md"
