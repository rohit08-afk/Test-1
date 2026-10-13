GL1 Webinar Completed =
CALCULATE(
    DISTINCTCOUNT('GL1 - Supplier Webinar'[Domain Name]),
    'GL1 - Supplier Webinar'[Attendee Duration] >= 30,
    'GL1 - Supplier Webinar'[Domain Name] <> BLANK()
) + 0


GL1 Webinar Not Attended =
VAR AttendedDomains =
    CALCULATETABLE(
        VALUES('GL1 - Supplier Webinar'[Domain Name]),
        'GL1 - Supplier Webinar'[Attendee Email] <> BLANK()
    )
VAR AllDomains =
    VALUES('GL1 Webinar Supplier lookup'[Domain Name])
RETURN
    COUNTROWS(
        EXCEPT(
            FILTER(AllDomains, NOT ISBLANK('GL1 Webinar Supplier lookup'[Domain Name])),
            AttendedDomains
        )
    )


GL1 Webinar Short Attendance =
VAR AttendedDomains =
    CALCULATETABLE(
        VALUES('GL1 - Supplier Webinar'[Domain Name]),
        'GL1 - Supplier Webinar'[Attendee Email] <> BLANK()
    )
VAR CompletedDomains =
    CALCULATETABLE(
        VALUES('GL1 - Supplier Webinar'[Domain Name]),
        'GL1 - Supplier Webinar'[Attendee Duration] >= 30
    )
RETURN
    COUNTROWS(
        EXCEPT(AttendedDomains, CompletedDomains)
    )


GL1 Webinar Completion % =
DIVIDE(
    [GL1 Webinar Completed],
    [GL1 Webinar Total Suppliers],
    0
)



    

    
