# Tags

The tags are used to categorize providers according to the type of entertainment they offer, for example: *Theme Parks*, *Shows*, *Museums*, *Concerts*, etc.

The identifiers of the assigned labels can be seen in the [catalog](catalog.md) at the supplier level.

## Access method

**GET** /activity/tags

## Response structure

- **``Tags``**: tag array.
    - **``Id``**: tag identifier. 13 character alphanumeric.
    - **``Key``**: tag key. Unique integer value among all tags.
    - **``Name``**: tag name (for example "*Theaters and Shows*").
    - **``PathName``**: tag path separated by "/" in case it has child tags (for example "Theaters and shows / Concerts").
    - **``Children``**: child tags of the current tag. The nesting level is infinite, there can be labels with depth of N children. The structure of child tags is the same as parent tags.

--8<-- "includes/responseBaseDocumentation.en.md"

### Response example

--8<-- "includes/examples/activity/catalogResponseExamples.md"
