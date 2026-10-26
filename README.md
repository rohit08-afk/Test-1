GL1 Selected Total Suppliers =
VAR SelectedPersonas =
    SELECTCOLUMNS(
        VALUES('GL1 Webinar Measures'[Persona]),
        "Persona",
        SWITCH(
            'GL1 Webinar Measures'[Persona],
            "Beeline - Identity Creation , Services",
            "Services, Beeline - Identity Creation",
            'GL1 Webinar Measures'[Persona]
        )
    )
RETURN
    CALCULATE(
        [GL1 Total Suppliers],
        TREATAS(
            SelectedPersonas,
            'Supplier Integration Register'[Persona]
        )
    )
