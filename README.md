VAR AttendedHigh =
    SUMX(
        HighSuppliers,
        VAR SupplierName =
            'Supplier Integration Register'[Name]
        RETURN
            IF(
                CALCULATE(
                    [GL1 Webinar Attended],
                    TREATAS(
                        {SupplierName},
                        'GL1 Webinar Measures'[Supplier Name]
                    )
                ) > 0,
                1,
                0
            )
    )
