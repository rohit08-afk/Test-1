Target High Total =
CALCULATE(
    [Total Suppliers],
    KEEPFILTERS(
        'Supplier Integration Register'[Comms Priority] = "High"
    ),
    TREATAS(
        VALUES('GL1 Webinar Measures'[Persona]),
        'Supplier Integration Register'[Persona]
    )
)


Target High Attended =
VAR HighSuppliers =
    CALCULATETABLE(
        VALUES('Supplier Integration Register'[Name]),
        KEEPFILTERS(
            'Supplier Integration Register'[Comms Priority] = "High"
        )
    )
RETURN
CALCULATE(
    [Webinar Attended],
    KEEPFILTERS(
        TREATAS(
            HighSuppliers,
            'GL1 Webinar Measures'[Supplier Name]
        )
    )
)
