GL1 High Priority Not Attended =
VAR RegisterPersona =
    SWITCH(
        SELECTEDVALUE('GL1 Webinar Measures'[Persona]),
        "Beeline - Identity Creation , Services",
        "Services, Beeline - Identity Creation",
        SELECTEDVALUE('GL1 Webinar Measures'[Persona])
    )

VAR HighSuppliers =
    CALCULATETABLE(
        VALUES('Supplier Integration Register'[Supplier Name]),
        'Supplier Integration Register'[Persona] = RegisterPersona,
        'Supplier Integration Register'[Comms Priority] = "High"
    )

VAR AttendedHigh =
    CALCULATE(
        [GL1 Webinar Attended Corrected],
        TREATAS(
            HighSuppliers,
            'GL1 Webinar Measures'[Supplier Name]
        )
    )

RETURN
    COUNTROWS(HighSuppliers) - AttendedHigh



GL1 Medium Priority Not Attended =
VAR RegisterPersona =
    SWITCH(
        SELECTEDVALUE('GL1 Webinar Measures'[Persona]),
        "Beeline - Identity Creation , Services",
        "Services, Beeline - Identity Creation",
        SELECTEDVALUE('GL1 Webinar Measures'[Persona])
    )

VAR MediumSuppliers =
    CALCULATETABLE(
        VALUES('Supplier Integration Register'[Supplier Name]),
        'Supplier Integration Register'[Persona] = RegisterPersona,
        'Supplier Integration Register'[Comms Priority] = "Medium"
    )

VAR AttendedMedium =
    CALCULATE(
        [GL1 Webinar Attended Corrected],
        TREATAS(
            MediumSuppliers,
            'GL1 Webinar Measures'[Supplier Name]
        )
    )

RETURN
    COUNTROWS(MediumSuppliers) - AttendedMedium
    
