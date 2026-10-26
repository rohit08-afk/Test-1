GL1 High Priority Not Attended =
VAR CurrentPersona =
    SELECTEDVALUE('GL1 Webinar Measures'[Persona])

VAR RegisterPersona =
    IF(
        CurrentPersona = "Beeline - Identity Creation , Services",
        "Services, Beeline - Identity Creation",
        CurrentPersona
    )

VAR TotalHigh =
    CALCULATE(
        [GL1 Total Suppliers],
        REMOVEFILTERS('Supplier Integration Register'[Persona]),
        'Supplier Integration Register'[Persona] = RegisterPersona,
        'Supplier Integration Register'[Comms Priority] = "High"
    )

VAR AttendedHigh =
    CALCULATE(
        [GL1 Webinar Attended Corrected],
        'GL1 Webinar Measures'[Comms Priority] = "High"
    )

RETURN
    TotalHigh - AttendedHigh



    GL1 Medium Priority Not Attended =
VAR CurrentPersona =
    SELECTEDVALUE('GL1 Webinar Measures'[Persona])

VAR RegisterPersona =
    IF(
        CurrentPersona = "Beeline - Identity Creation , Services",
        "Services, Beeline - Identity Creation",
        CurrentPersona
    )

VAR TotalMedium =
    CALCULATE(
        [GL1 Total Suppliers],
        REMOVEFILTERS('Supplier Integration Register'[Persona]),
        'Supplier Integration Register'[Persona] = RegisterPersona,
        'Supplier Integration Register'[Comms Priority] = "Medium"
    )

VAR AttendedMedium =
    CALCULATE(
        [GL1 Webinar Attended Corrected],
        'GL1 Webinar Measures'[Comms Priority] = "Medium"
    )

RETURN
    TotalMedium - AttendedMedium
