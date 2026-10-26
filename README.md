Target Medium Total =
VAR SelectedSuppliers =
    VALUES('GL1 Webinar Measures'[Supplier Name])

VAR TeamFiltered =
    ISFILTERED('GL1 Webinar Measures'[Persona])
    || ISFILTERED('GL1 Webinar Measures'[Category Family])
    || ISFILTERED('GL1 Webinar Measures'[Category Manager])
    || ISFILTERED('GL1 Webinar Measures'[Procurement Leadership Team])
    || ISFILTERED('GL1 Webinar Measures'[Comms Priority])

RETURN
IF(
    TeamFiltered,
    CALCULATE(
        [Total Suppliers],
        'Supplier Integration Register'[Comms Priority] = "Medium",
        TREATAS(
            SelectedSuppliers,
            'Supplier Integration Register'[Name]
        )
    ),
    CALCULATE(
        [Total Suppliers],
        'Supplier Integration Register'[Comms Priority] = "Medium"
    )
)


Target High Total =
VAR SelectedSuppliers =
    VALUES('GL1 Webinar Measures'[Supplier Name])

VAR TeamFiltered =
    ISFILTERED('GL1 Webinar Measures'[Persona])
    || ISFILTERED('GL1 Webinar Measures'[Category Family])
    || ISFILTERED('GL1 Webinar Measures'[Category Manager])
    || ISFILTERED('GL1 Webinar Measures'[Procurement Leadership Team])
    || ISFILTERED('GL1 Webinar Measures'[Comms Priority])

RETURN
IF(
    TeamFiltered,
    CALCULATE(
        [Total Suppliers],
        'Supplier Integration Register'[Comms Priority] = "High",
        TREATAS(
            SelectedSuppliers,
            'Supplier Integration Register'[Name]
        )
    ),
    CALCULATE(
        [Total Suppliers],
        'Supplier Integration Register'[Comms Priority] = "High"
    )
)
