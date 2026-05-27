# Sessions

A session is defined by date and time, content, and, optionally, available capacity.

According to this definition, the same session can be shared by several tickets. The tickets "Adult Ticket", "Child Ticket", "Junior Ticket", "Senior Ticket" and "Disabled Ticket" can be associated with the same sessions during the current year (for example, 10 sessions per day during the 365 days of the year).

Because this situation can be common, we have tried to separate the session structure from the [product catalog](catalog.md) as much as possible. Following the previous example, if the sessions were defined in the product catalog, we would have 10 sessions x 365 days = 3650 sessions for each of the 5 tickets ("Adult Ticket", "Child Ticket", "Junior Ticket", "Senior Ticket" and "Disabled Ticket").

Therefore, the session structure is defined to minimize the data load and organize the session catalog as well as possible.

## Access method

**POST** activity/sessions

## Request structure

To obtain the sessions we can use different filters in the body of the method. Each filter will be considered an ***AND***.

- **`SessionsGroupProfileIds`**: (``list``). Array of session group profiles.
    - **``(string)``**: Session group profile identifier.
- **`SessionsGroupIds`**: (``list``). Array of session groups.
    - **``(string)``**: Session group identifier.
- **`SessionContentProfileIds`**: (``list``). Array of session content profiles.
    - **``(string)``**: Session content profile identifier.
- **`FromDate`**: (``string``). Filter by start date. Does not allow values earlier than today. The default value is the current day. *ISO 8601 format (yyyy-MM-dd)*.
- **`ToDate`**: (``string``). Filter by end date. Its default value is the date corresponding to one year from now. *ISO 8601 format (yyyy-MM-dd)*.
- **`Dates`**: (``list``). Array of dates to filter by. *ISO 8601 format (yyyy-MM-dd)*.
    - **``(date)``**: Date to filter by.
- **`LanguageCode`**: (``string``). Content language code.

### Request examples

--8<-- "includes/examples/activity/sessionsQueryExamples.md"

## Response structure

- **`SessionsGroupProfiles`**: (``list``). Array of session group profiles.
    - **`SessionsGroupProfileId`**: (``string``). Session group profile identifier.
    - **`SessionsGroupProfileName`**: (``string``). Session group profile name.
    - **`SessionTimeAvailabilityOffset`**: (``int``). Number of minutes before (if the value is negative) or after (if the value is positive) when the session can be on sale with respect to the session time.
    - **`SessionStartTimeType`**: (``int``). Numeric identifier that indicates the session access start type.
        - **`0`**: (``int``): Access at the indicated time.
        - **`1`**: (``int``): Access from the indicated time onwards.
    - **`SessionsGroups`**: (``list``). Array of session groups.
        - **`SessionsGroupId`**: (``string``). Session group identifier.
        - **`SessionsGroupName`**: (``string``). Session group name.
        - **`Sessions`**: (``list``). Array of sessions.
            - **`SessionId`**: (``string``). Session identifier.
            - **`SessionTime`**: (``date``). Session date and time.
            - **`AvailableCapacity`**: (``int``). Value that indicates the session capacity. If this field does not exist, there is no limited capacity. If you only want to check the capacity of a session, you can use the method described in [Obtaining available capacity](availability.md).
- **`SessionContentProfiles`**: (``list``). Array of session content profiles.
    - **`SessionContentProfileId`**: (``string``). Session content profile identifier.
    - **`SessionContentProfileName`**: (``string``). Session content profile name.
    - **`SessionContents`**: (``list``). Array of session contents.
        - **`SessionContentId`**: (``string``). Session content identifier.
        - **`SessionContentName`**: (``string``). Session content name.
        - **`SessionContentDescription`**: (``string``). Session content description.
--8<-- "includes/responseBaseDocumentation.en.md"

### Response example

As an example, suppose we have a default session group profile and a default session content profile.

Within the session group profile we can see that there are two session groups:

- Morning sessions, which group the 10:00 a.m. sessions.
- Afternoon sessions, which group the 5:00 p.m. sessions.

In the session content profile we have three session contents, which define movies (1, 2 and 3).

Seen from the reverse point of view, the most important entities are sessions on one side and contents on the other. Both entities have higher-level groupings (groups and profiles), with the sole purpose of organizing the structure.

!!! warning "Important"
    At this point we have only defined which sessions and contents exist, but we do not know the relationship between sessions and contents. That is the responsibility of the sessions section of the [product catalog](catalog.md).

--8<-- "includes/examples/activity/sessionResultExamples.md"
