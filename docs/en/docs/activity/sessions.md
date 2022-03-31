# Sessions

A session is defined by date and time, content, and, optionally, available capacity.

Under this definition, we understand a given session can be shared by multiple products. E.g. products "Adult Ticket", "Children’s Ticket", "Junior Ticket", "Senior Ticket" and "Special Needs Ticket” can be associated with the same sessions in the present year, e.g. 10 sessions per day, 365 days of the year.

As this series may be common, we have sought to separate the sessions’ structure from the [products catalog](catalog.md) structure as much as possible. Using the above example, if we define the session in the products catalog, we would have 10 sessions x 365 days = 3650 sessions for each one of the 5 products ("Adult Ticket", "Children’s Ticket", "Junior Ticket", "Senior Ticket" and "Special Needs Person’s Ticket")... and we are talking about just an example of products from a single provider.

Therefore, to minimize the uploading of data, and to prioritize the best possible sessions catalog, we will define the sessions’ structure in the units presented below.

## Access method

**POST** activity/sessions

## Request structure

To obtain the sessions we can use different filters in the body of the method. Each filter will be considered an ***AND***.

The following data structure must be specified in the method body.

- **`SessionsGroupProfileIds`**: profile of session groups.
- **`SessionsGroupIds`**: session groups.
- **`SessionContentProfileIds`**: sessions content profile.
- **`FromDate`**: filtering by starting date. It does not allow earlier date values other than the one of today . Its value is by default today’s date. *ISO 8601 formt (yyyy-MM-dd)*.
- **`ToDate`**: filtering by ending date. The default value is the corresponding date within a year. *ISO 8601 format (yyyy-MM-dd)*.
- **`Dates`**: list of dates to filter by. *ISO 8601 format (yyyy-MM-dd)*.
- **`LanguageCode`**: contents language code.

### Request examples

--8<-- "includes/examples/activity/sessionsQueryExamples.md"

## Response structure

- **`SessionsGroupProfiles`**: array of session groups profile.
    - **`SessionsGroupProfileId`**: identifier of session groups profile.
    - **`SessionsGroupProfileName`**: name of the session groups profile.
    - **`SessionTimeAvailabilityOffset`**: amount of minutes before (negative value) or after (positive value) the session time when the session can be available to purchase.
    - **`SessionsGroups`**: array of session groups.
        - **`SessionsGroupId`**: the session’s group identifier.
        - **`SessionsGroupName`**: name of the sessions group.
        - **`Sessions`**: array of sessions.
            - **`SessionId`**: session identifier.
            - **`SessionTime`**: date and time of the session.
            - **`AvailableCapacity`**: value that indicates the session’s capacity. If this field does not exist it is because there is no limited capacity. If one only wants to see a session’s capacity, use the method described in the unit on [obtaining available capacity](availability.md).
- **`SessionContentProfiles`**: array of session contents profile.
    - **`SessionContentProfileId`**: session contents profile identifier.
    - **`SessionContentProfileName`**: name of session contents profile.
    - **`SessionContents`**: Session contents.
        - **`SessionContentId`**: the session’s content identifier.
        - **`SessionContentName`**: session content name.
        - **`SessionContentDescription`**: session content description.
--8<-- "includes/responseBaseDocumentation.en.md"

### Response example

See the example below. The "Provider with sessions" has a default session groups profile, and a default session contents profile.

Therefore, within the session groups profile there will be two session groups:

- Morning sessions, which groups the 10:00 a.m. sessions.
- Afternoon sessions, which groups the 5:00 p.m. sessions.

Within the session contents profile we see that there will be three session contents, which define movies (1, 2 and 3).

Seen from a reverse point of view, the most important entities are the sessions on the one hand, and the contents on the other. Both entities have upper clusters (groups and profiles), with the sole purpose ranking the structure.

!!! warning "Important note"
    At this point we have only defined which sessions and contents there are, but we do not know the relationship existing between sessions and content. That is treated in the [products catalog](catalog.md) section.

--8<-- "includes/examples/activity/sessionResultExamples.md"
