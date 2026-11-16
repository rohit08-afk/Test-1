
Webinar Required Count =
VAR PersonaText =
    TRIM(
        SELECTEDVALUE(
            'Supplier Integration Register'[Persona],
            ""
        )
    )
RETURN
    IF(
        PersonaText = "",
        0,
        LEN(PersonaText)
            - LEN(SUBSTITUTE(PersonaText, ",", ""))
            + 1
    )
