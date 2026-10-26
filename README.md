Target High Total =
CALCULATE(
    [GL1 Total Suppliers],
    REMOVEFILTERS('GL1 Webinar Measures'),
    REMOVEFILTERS('Supplier Integration Register'[Persona]),
    REMOVEFILTERS('Supplier Integration Register'[Comms Priority]),
    'Supplier Integration Register'[Comms Priority] = "High"
)


Target Medium Total =
CALCULATE(
    [GL1 Total Suppliers],
    REMOVEFILTERS('GL1 Webinar Measures'),
    REMOVEFILTERS('Supplier Integration Register'[Persona]),
    REMOVEFILTERS('Supplier Integration Register'[Comms Priority]),
    'Supplier Integration Register'[Comms Priority] = "Medium"
)


Target High Attended =
VAR HighSuppliers =
    CALCULATETABLE(
        VALUES('Supplier Integration Register'[Name]),
        REMOVEFILTERS('Supplier Integration Register'[Persona]),
        'Supplier Integration Register'[Comms Priority] = "High"
    )
RETURN
SUMX(
    HighSuppliers,
    VAR CurrentSupplier =
        'Supplier Integration Register'[Name]
    RETURN
        IF(
            CALCULATE(
                [GL1 Webinar Attended],
                REMOVEFILTERS('GL1 Webinar Measures'),
                TREATAS(
                    {CurrentSupplier},
                    'GL1 Webinar Measures'[Supplier Name]
                )
            ) > 0,
            1,
            0
        )
)




Target Medium Attended =
VAR MediumSuppliers =
    CALCULATETABLE(
        VALUES('Supplier Integration Register'[Name]),
        REMOVEFILTERS('Supplier Integration Register'[Persona]),
        'Supplier Integration Register'[Comms Priority] = "Medium"
    )
RETURN
SUMX(
    MediumSuppliers,
    VAR CurrentSupplier =
        'Supplier Integration Register'[Name]
    RETURN
        IF(
            CALCULATE(
                [GL1 Webinar Attended],
                REMOVEFILTERS('GL1 Webinar Measures'),
                TREATAS(
                    {CurrentSupplier},
                    'GL1 Webinar Measures'[Supplier Name]
                )
            ) > 0,
            1,
            0
        )
)


Target High Remaining =
[Target High Total] - [Target High Attended]

Target Medium Remaining =
[Target Medium Total] - [Target Medium Attended]


Target High Rate =
DIVIDE([Target High Attended], [Target High Total], 0)


Target Medium Rate =
DIVIDE([Target Medium Attended], [Target Medium Total], 0)


