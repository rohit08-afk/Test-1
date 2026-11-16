
Webinar Completed Count =
VAR PersonaText =
    SELECTEDVALUE(
        'Supplier Integration Register'[Persona],
        ""
    )
VAR SelectedSupplier =
    SELECTEDVALUE(
        'Supplier Integration Register'[Supplier Name]
    )
RETURN
    CALCULATE(
        DISTINCTCOUNT(
            'GL1 Supplier Webinar Attendance'[Webinar Type]
        ),
        FILTER(
            ALL('GL1 Supplier Webinar Attendance'),
            'GL1 Supplier Webinar Attendance'[Supplier Name]
                = SelectedSupplier
            &&
            'GL1 Supplier Webinar Attendance'[Attendance Status]
                = "Attended"
            &&
            CONTAINSSTRING(
                PersonaText,
                'GL1 Supplier Webinar Attendance'[Webinar Type]
            )
        )
    ) + 0



Webinar Attendance KPI =
VAR Completed = [Webinar Completed Count]
VAR Required = [Webinar Required Count]
RETURN
    Completed & " / " & Required & " Complete"
