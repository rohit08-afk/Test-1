
Webinar Done Tooltip =
VAR PersonaText =
    SELECTEDVALUE(
        'Supplier Integration Register'[Persona],
        ""
    )
VAR SelectedSupplier =
    SELECTEDVALUE(
        'Supplier Integration Register'[Supplier Name]
    )
VAR AttendedWebinars =
    CALCULATETABLE(
        VALUES(
            'GL1 Supplier Webinar Attendance'[Webinar Type]
        ),
        FILTER(
            ALL('GL1 Supplier Webinar Attendance'),
            'GL1 Supplier Webinar Attendance'[Supplier Name]
                = SelectedSupplier
            &&
            'GL1 Supplier Webinar Attendance'[Attendance Status]
                = "Attended"
        )
    )
RETURN
    "Done: "
        & COALESCE(
            CONCATENATEX(
                FILTER(
                    AttendedWebinars,
                    CONTAINSSTRING(
                        PersonaText,
                        'GL1 Supplier Webinar Attendance'[Webinar Type]
                    )
                ),
                'GL1 Supplier Webinar Attendance'[Webinar Type],
                ", "
            ),
            "None"
        )




Webinar Pending Tooltip =
VAR PersonaText =
    SELECTEDVALUE(
        'Supplier Integration Register'[Persona],
        ""
    )
VAR SelectedSupplier =
    SELECTEDVALUE(
        'Supplier Integration Register'[Supplier Name]
    )
VAR Personas =
    SELECTCOLUMNS(
        GENERATESERIES(
            1,
            MAX(
                1,
                LEN(PersonaText)
                    - LEN(SUBSTITUTE(PersonaText, ",", ""))
                    + 1
            )
        ),
        "PersonaName",
        TRIM(
            PATHITEM(
                SUBSTITUTE(PersonaText, ",", "|"),
                [Value],
                TEXT
            )
        )
    )
VAR AttendedWebinars =
    CALCULATETABLE(
        VALUES(
            'GL1 Supplier Webinar Attendance'[Webinar Type]
        ),
        FILTER(
            ALL('GL1 Supplier Webinar Attendance'),
            'GL1 Supplier Webinar Attendance'[Supplier Name]
                = SelectedSupplier
            &&
            'GL1 Supplier Webinar Attendance'[Attendance Status]
                = "Attended"
        )
    )
VAR PendingPersonas =
    FILTER(
        Personas,
        [PersonaName] <> ""
            &&
        NOT (
            [PersonaName]
                IN SELECTCOLUMNS(
                    AttendedWebinars,
                    "PersonaName",
                    'GL1 Supplier Webinar Attendance'[Webinar Type]
                )
        )
    )
RETURN
    "Pending: "
        & COALESCE(
            CONCATENATEX(
                PendingPersonas,
                [PersonaName],
                ", "
            ),
            "None"
        )
