GL1 Webinar Not Attended Corrected =
VAR CurrentPersona =
    SELECTEDVALUE('GL1 Webinar Measures'[Persona])

VAR RegisterPersona =
    IF(
        CurrentPersona = "Beeline - Identity Creation, Services",
        "Services, Beeline - Identity Creation",
        CurrentPersona
    )

VAR TotalSuppliers =
    CALCULATE(
        DISTINCTCOUNT('Supplier Integration Register'[Supplier Name]),
        REMOVEFILTERS('Supplier Integration Register'[Persona]),
        'Supplier Integration Register'[Persona] = RegisterPersona
    )

RETURN
    TotalSuppliers - [GL1 Webinar Attended Corrected]
