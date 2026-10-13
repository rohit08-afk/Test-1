GL1 Webinar Completed =
VAR CompletedDomains =
    CALCULATETABLE(
        VALUES('GL1 - Supplier Webinar'[Domain Name]),
        'GL1 - Supplier Webinar'[Attendee Duration] >= 30
    )
RETURN
    CALCULATE(
        DISTINCTCOUNT('GL1 Webinar Supplier lookup'[Supplier Name]),
        TREATAS(
            CompletedDomains,
            'GL1 Webinar Supplier lookup'[Domain Name]
        )
    ) + 0


    GL1 Webinar Not Attended =
VAR AttendedDomains =
    VALUES('GL1 - Supplier Webinar'[Domain Name])
VAR NotAttendedSuppliers =
    FILTER(
        'GL1 Webinar Supplier lookup',
        NOT (
            'GL1 Webinar Supplier lookup'[Domain Name]
                IN AttendedDomains
        )
    )
RETURN
    COUNTROWS(NotAttendedSuppliers) + 0


   GL1 Webinar Short Attendance =
VAR AttendedDomains =
    VALUES('GL1 - Supplier Webinar'[Domain Name])
VAR CompletedDomains =
    CALCULATETABLE(
        VALUES('GL1 - Supplier Webinar'[Domain Name]),
        'GL1 - Supplier Webinar'[Attendee Duration] >= 30
    )
RETURN
    CALCULATE(
        DISTINCTCOUNT('GL1 Webinar Supplier lookup'[Supplier Name]),
        TREATAS(
            EXCEPT(AttendedDomains, CompletedDomains),
            'GL1 Webinar Supplier lookup'[Domain Name]
        )
    ) + 0 
