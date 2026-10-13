GL1 Webinar Supplier Status =
VAR SupplierDomain =
    SELECTEDVALUE(
        'GL1 Webinar Supplier lookup'[Domain Name]
    )
VAR AttendanceRows =
    CALCULATE(
        COUNTROWS('GL1 - Supplier Webinar'),
        TREATAS(
            {SupplierDomain},
            'GL1 - Supplier Webinar'[Domain Name]
        )
    )
VAR CompletedRows =
    CALCULATE(
        COUNTROWS('GL1 - Supplier Webinar'),
        'GL1 - Supplier Webinar'[Attendee Duration] >= 30,
        TREATAS(
            {SupplierDomain},
            'GL1 - Supplier Webinar'[Domain Name]
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
