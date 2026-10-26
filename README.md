GL1 Webinar Total by Persona =
CALCULATE(
    [GL1 Total Suppliers],
    TREATAS(
        VALUES('GL1 Webinar Measures'[Persona]),
        'Supplier Integration Register'[Persona]
    )
)
