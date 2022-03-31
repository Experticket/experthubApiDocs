# Prepackages

With this method we can obtain the prepackages of available activities.

## Access method

**POST** activity/prepackages

## Request structure

- **``ProviderIds``**: array of providers to filter.
- **``PrePackageIds``**: array of prepackets to filter.
- **``FromDate``**: date from to filter prepackages. By default the current day is taken. *ISO 8601 format (yyyy-MM-dd)*.
- **``ToDate``**: date until to filter pre-packages. By default it will be the date within a year. *ISO 8601 format (yyyy-MM-dd)*.
- **``PeopleDistributions``**: type of people to filter prepackages.
    - **``NumberOfAdults``**: number of adults.
    - **``NumberOfChildren``**: number of children.
    - **``NumberOfSeniors``**: number of seniors.
    - **``NumberOfBabies``**: number of babies.
    - **``ChildrenAges``**: array of ages of children and babies.

### Request example

--8<-- "includes/examples/package/prepackageQueryExamples.md"

## Response structure

- **``PrePackages``**: prepackage array.
    - **``Id``**: prepackage identifier.
    - **``Order``**: order to be displayed.
    - **``Image``**: prepackage promotional image.
    - **``Description``**: prepackage description.
    - **``Name``**: prepackage name.
    - **``CommercialName``**: commercial name of the prepackage.
    - **``ProductPaxGroupings``**: product grouping.
        - **``ProviderId``**: provider identifier.
        - **``ProviderName``**: provider name.
        - **``ProviderLocation``**: provider location.
            - **`Lat`**: latitude coordinates.
            - **`Lng`**: longitude coordinates.
        - **``DatePolicyKey``**: date policies key.
        - **``TicketEnclosures``**: array of enclosures.
            - **``Id``**: enclosure identifier.
            - **``Name``**: enclosure name.
            - **``Logo``**: image with the enclosure logo.
        - **``ValidDays``**: days of validity.
        - **``ValidDaysType``**: type of validity days.
    - **``SuggestedLocation``**: suggested location to search for accommodation. It is usually a calculated central coordinates between all the prepackage enclosures.
        - **`Lat`**: latitude coordinates.
        - **`Lng`**: longitude coordinates.
--8<-- "includes/responseBaseDocumentation.es.md"

### Response example

--8<-- "includes/examples/package/prepackageResponseExamples.md"
