- **``Activity``**: activity with which we want the package
    - **``PrePackageIds``**: activity prepackage identifier.
    - **``FromDate``**: date from which we want to use the activity.
    - **``ToDate``**: date until we want to make use of the activity.

- **``Accommodation``**: accommodation information.
    - **``CheckIn``**: access date to accommodation.
    - **``CheckOut``**: accommodation departure date.
    - **``Destination``**: coordinates of the destination, to search for nearby activities.
        - **``Latitude``**: latitude.
        - **``Longitude``**: longitude.
    - **``RoomDistribution``**: array of rooms.
        - **`People`**: array of people.
            - **``Type``**: kind of person.

                ??? example "Possible values"
                    - 0: Baby
                    - 1: Child
                    - 2: Adult
                    - 3: Senior
                    - 4: Generic

            - **``Age``**: person's age, mandatory in case of being a baby or child.
