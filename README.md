High Priority Not Attended =
VAR CurrentPersona =
    SELECTEDVALUE('GL1 Webinar Measures'[Persona])

VAR RegisterPersona =
    SWITCH(
        CurrentPersona,
        "Beeline - Identity Creation , Services",
        "Services, Beeline - Identity Creation",
        CurrentPersona
    )

VAR HighSuppliers =
    CALCULATETABLE(
        VALUES('Supplier Integration Register'[Name]),
        'Supplier Integration Register'[Persona] = RegisterPersona,
        'Supplier Integration Register'[Comms Priority] = "High"
    )

VAR AttendedHigh =
    SUMX(
        HighSuppliers,
        VAR CurrentSupplier =
            'Supplier Integration Register'[Name]
        RETURN
            IF(
                CALCULATE(
                    [GL1 Webinar Attended],
                    TREATAS(
                        {CurrentSupplier},
                        'GL1 Webinar Measures'[Supplier Name]
                    )
                ) > 0,
                1,
                0
            )
    )

RETURN
    COUNTROWS(HighSuppliers) - AttendedHigh



   Medium Priority Not Attended =
VAR CurrentPersona =
    SELECTEDVALUE('GL1 Webinar Measures'[Persona])

VAR RegisterPersona =
    SWITCH(
        CurrentPersona,
        "Beeline - Identity Creation , Services",
        "Services, Beeline - Identity Creation",
        CurrentPersona
    )

VAR MediumSuppliers =
    CALCULATETABLE(
        VALUES('Supplier Integration Register'[Name]),
        'Supplier Integration Register'[Persona] = RegisterPersona,
        'Supplier Integration Register'[Comms Priority] = "Medium"
    )

VAR AttendedMedium =
    SUMX(
        MediumSuppliers,
        VAR CurrentSupplier =
            'Supplier Integration Register'[Name]
        RETURN
            IF(
                CALCULATE(
                    [GL1 Webinar Attended],
                    TREATAS(
                        {CurrentSupplier},
                        'GL1 Webinar Measures'[Supplier Name]
                    )
                ) > 0,
                1,
                0
            )
    )

RETURN
    COUNTROWS(MediumSuppliers) - AttendedMedium 
