Target Medium Total =
VAR PersonaFiltered =
    ISFILTERED('GL1 Webinar Measures'[Persona])

VAR SelectedPersonas =
    SELECTCOLUMNS(
        VALUES('GL1 Webinar Measures'[Persona]),
        "PersonaName",
        SWITCH(
            'GL1 Webinar Measures'[Persona],
            "Beeline - Identity Creation , Services",
            "Services, Beeline - Identity Creation",
            'GL1 Webinar Measures'[Persona]
        )
    )

RETURN
IF(
    PersonaFiltered,
    CALCULATE(
        [Total Suppliers],
        KEEPFILTERS(
            'Supplier Integration Register'[Comms Priority] = "Medium"
        ),
        TREATAS(
            SelectedPersonas,
            'Supplier Integration Register'[Persona]
        )
    ),
    CALCULATE(
        [Total Suppliers],
        KEEPFILTERS(
            'Supplier Integration Register'[Comms Priority] = "Medium"
        )
    )
)
