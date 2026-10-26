GL1 Webinar Suppliers Attended =
VAR InvitedSuppliers =
    CALCULATETABLE(
        SUMMARIZE(
            'GL1 Supplier Webinar Attendance',
            'GL1 Supplier Webinar Attendance'[Supplier Name],
            'GL1 Supplier Webinar Attendance'[Domain]
        ),
        REMOVEFILTERS(
            'GL1 Supplier Webinar Attendance'[Invited Status],
            'GL1 Supplier Webinar Attendance'[Attendance Status]
        ),
        'GL1 Supplier Webinar Attendance'[Invited Status] = "Invited"
    )

VAR AttendedDomains =
    CALCULATETABLE(
        VALUES('GL1 Supplier Webinar Attendance'[Domain]),
        REMOVEFILTERS(
            'GL1 Supplier Webinar Attendance'[Invited Status],
            'GL1 Supplier Webinar Attendance'[Attendance Status]
        ),
        'GL1 Supplier Webinar Attendance'[Attendance Status] = "Attended"
    )

RETURN
    COUNTROWS(
        FILTER(
            InvitedSuppliers,
            NOT ISBLANK([Domain])
                && CONTAINS(
                    AttendedDomains,
                    'GL1 Supplier Webinar Attendance'[Domain],
                    [Domain]
                )
        )
    )



    GL1 Webinar Suppliers Not Attended =
VAR InvitedSuppliers =
    CALCULATETABLE(
        SUMMARIZE(
            'GL1 Supplier Webinar Attendance',
            'GL1 Supplier Webinar Attendance'[Supplier Name],
            'GL1 Supplier Webinar Attendance'[Domain]
        ),
        REMOVEFILTERS(
            'GL1 Supplier Webinar Attendance'[Invited Status],
            'GL1 Supplier Webinar Attendance'[Attendance Status]
        ),
        'GL1 Supplier Webinar Attendance'[Invited Status] = "Invited"
    )

VAR AttendedDomains =
    CALCULATETABLE(
        VALUES('GL1 Supplier Webinar Attendance'[Domain]),
        REMOVEFILTERS(
            'GL1 Supplier Webinar Attendance'[Invited Status],
            'GL1 Supplier Webinar Attendance'[Attendance Status]
        ),
        'GL1 Supplier Webinar Attendance'[Attendance Status] = "Attended"
    )

RETURN
    COUNTROWS(
        FILTER(
            InvitedSuppliers,
            ISBLANK([Domain])
                || NOT CONTAINS(
                    AttendedDomains,
                    'GL1 Supplier Webinar Attendance'[Domain],
                    [Domain]
                )
        )
    )
