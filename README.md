Webinar Attendance Status =
VAR SupplierDomain =
    'GL1 Webinar Supplier lookup'[Domain Name]

VAR AttendanceRows =
    CALCULATE(
        COUNTROWS('GL1 - Supplier Webinar'),
        FILTER(
            ALL('GL1 - Supplier Webinar'),
            'GL1 - Supplier Webinar'[Domain Name] = SupplierDomain
                && NOT ISBLANK('GL1 - Supplier Webinar'[Attendee Email])
        )
    )

VAR CompletedRows =
    CALCULATE(
        COUNTROWS('GL1 - Supplier Webinar'),
        FILTER(
            ALL('GL1 - Supplier Webinar'),
            'GL1 - Supplier Webinar'[Domain Name] = SupplierDomain
                && 'GL1 - Supplier Webinar'[Attendee Duration] >= 30
        )
    )

RETURN
    SWITCH(
        TRUE(),
        ISBLANK(SupplierDomain), BLANK(),
        CompletedRows > 0, "Completed",
        AttendanceRows > 0, "Short Attendance",
        "Not Attended"
    )
