Target High Total =
VAR SelectedSuppliers =
    VALUES('GL1 Webinar Measures'[Supplier Name])
RETURN
IF(
    ISCROSSFILTERED('GL1 Webinar Measures'[Supplier Name]),
    CALCULATE(
        [Total Suppliers],
        KEEPFILTERS(
            'Supplier Integration Register'[Comms Priority] = "High"
        ),
        TREATAS(
            SelectedSuppliers,
            'Supplier Integration Register'[Name]
        )
    ),
    CALCULATE(
        [Total Suppliers],
        KEEPFILTERS(
            'Supplier Integration Register'[Comms Priority] = "High"
        )
    )
)



Target Medium Total =
VAR SelectedSuppliers =
    VALUES('GL1 Webinar Measures'[Supplier Name])
RETURN
IF(
    ISCROSSFILTERED('GL1 Webinar Measures'[Supplier Name]),
    CALCULATE(
        [Total Suppliers],
        KEEPFILTERS(
            'Supplier Integration Register'[Comms Priority] = "Medium"
        ),
        TREATAS(
            SelectedSuppliers,
            'Supplier Integration Register'[Name]
        )
    ),
    CALCULATE(
        [Total Suppliers],
        KEEPFILTERS(
            'Supplier Integration Register'[Comms Priority] = "Medium"
        )
    )
)

