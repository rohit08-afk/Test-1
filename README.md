Target Medium Attended =
VAR MediumSuppliers =
    CALCULATETABLE(
        VALUES('Supplier Integration Register'[Name]),
        'Supplier Integration Register'[Comms Priority] = "Medium"
    )
RETURN
CALCULATE(
    [Webinar Attended],
    KEEPFILTERS(
        TREATAS(
            MediumSuppliers,
            'GL1 Webinar Measures'[Supplier Name]
        )
    )
)
