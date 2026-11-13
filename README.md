GL2 Email Availability - All =
DATATABLE(
    "Email Availability", STRING,
    "Email Sort", INTEGER,
    {
        {"Yes", 1},
        {"No", 2}
    }
)

GL2 Communication Outcome - All =
DISTINCT(
    SELECTCOLUMNS(
        'GL2 - Supplier Integration Registerp',
        "Communication Outcome",
        'GL2 - Supplier Integration Registerp'[Comms Outcome]
    )
)

GL2 Comms Progress - All =
DISTINCT(
    SELECTCOLUMNS(
        'GL2 - Supplier Integration Registerp',
        "Comms Progress",
        'GL2 - Supplier Integration Registerp'[Comms Progress]
    )
)
