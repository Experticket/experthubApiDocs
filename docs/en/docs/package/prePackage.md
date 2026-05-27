# Prepackages

With this method we can obtain the available activity prepackages.

Prepackages are structures that exist before creating a package and can be composed of one or more enclosures (e.g. "Oceanogràfic + Bioparc"). Each prepackage, in turn, will have one or more product groups (`ProductPaxGroupings`).

It is important to take the suggested geolocation into account. This is used in the different catalog methods to locate an area from which hotels will be searched.

## Access method

**POST** /Activity/Prepackages

## Request structure

All request parameters are optional.

- **``ProviderIds``**: (``list``) ``Optional``. List of providers to filter.
    - **``(string)``**: ``Optional``. Provider identifier.
- **``PrePackageIds``**: (``list``) ``Optional``. List of prepackages to filter.
    - **``(string)``**: ``Optional``. Prepackage identifier.
- **``FromDate``**: (``date``) ``Optional``. Initial date to filter prepackages. Default value: current day. ISO 8601 format (YYYY-MM-DD).
- **``ToDate``**: (``date``) ``Optional``. Final date to filter prepackages. Default value: one year in the future. ISO 8601 format (YYYY-MM-DD).
- **``PeopleDistributions``**: (``list``) ``Optional``. List with the distribution of people in the different rooms.
    - **``PeopleDistribution``**: (``object``) ``Optional``. Information about the distribution in the corresponding room.
        - **``NumberOfAdults``**: (``int``) ``Optional``. Number of adults.
        - **``NumberOfChildren``**: (``int``) ``Optional``. Number of children.
        - **``NumberOfSeniors``**: (``int``) ``Optional``. Number of seniors.
        - **``NumberOfBabies``**: (``int``) ``Optional``. Number of babies.
        - **``ChildrenAges``**: (``list``) ``Optional``. List with the ages of babies and children.
            - **``(int)``**: ``Optional``. Age of the baby or child.

!!! caution "Age of babies/children"
    The age must be requested for all people who are 17 years old or younger.

### Request example

--8<-- "includes/examples/package/prepackageQueryExamples.md"

## Response structure

- **`Timestamp`**: (``dateTime``). Time at which the request was processed. ISO 8601 format (yyyy-MM-ddThh\:mm\:ss.fffffff).
- **``PrePackages``**: (``list``). List of available prepackages.
    - **``PrePackage``**: (``object``). Prepackage information.
        - **``Id``**: (``string``). Prepackage identifier.
        - **``Order``**: (``int``). Display order.
        - **``Image``**: (``string``). URL of the prepackage promotional image.
        - **``Description``**: (``string``). Prepackage description.
        - **``Name``**: (``string``). Prepackage name.
        - **``CommercialName``**: (``string``). Prepackage commercial name.
        - **``ProductPaxGroupings``**: (``list``). List of product groupings.
            - **``ProductPaxGrouping``**: (``object``). Product grouping information.
                - **``ProviderId``**: (``string``). Provider identifier.
                - **``ProviderName``**: (``string``). Provider name.
                - **``ProviderLocation``**: (``string``). Provider location.
                    - **`Lat`**: (``decimal``). Latitude coordinates.
                    - **`Lng`**: (``decimal``). Longitude coordinates.
                - **``DatePolicyKey``**: (``int``). Date policy key. All products with the same key must share the access date.
                - **``TicketEnclosures``**: (``list``). List of enclosures.
                    - **``TicketEnclosure``**: (``object``). Enclosure information.
                        - **``Id``**: (``string``). Enclosure identifier.
                        - **``Name``**: (``string``). Enclosure name.
                        - **``Logo``**: (``string``). URL of the image with the enclosure logo.
                - **``ValidDays``**: (``int``). Validity days.
                - **``ValidDaysType``**: (``int``). Type of validity days.

                    ??? example "Possible values"
                        --8<-- "includes/enum/validDayType.md"

                - **``ProductPaxGroupingId``**: (``string``). Grouped product identifier.
                - **``ProductPaxGroupingName``**: (``string``). Grouped product name.

            - **``SuggestedLocation``**: (``object``). Suggested location for accommodation search. It is usually a set of central coordinates calculated between all prepackage enclosures.
                - **`Lat`**: (``decimal``). Latitude coordinates.
                - **`Lng`**: (``decimal``). Longitude coordinates.

--8<-- "includes/experthubResponseBaseDocumentation.en.md"

### Response example

--8<-- "includes/examples/package/prepackageResponseExamples.md"
