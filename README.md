GL1 Webinar Not Attended Corrected =
VAR TotalSuppliers =
    CALCULATE(
        DISTINCTCOUNT('Supplier Integration Register'[Supplier Name]),
        TREATAS(
            VALUES('GL1 Webinar Measures'[Persona]),
            'Supplier Integration Register'[Persona]
        )
    )
RETURN
    TotalSuppliers - [GL1 Webinar Attended Corrected]
