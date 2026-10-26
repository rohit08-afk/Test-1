GL1 Webinar Attended =
VAR CurrentSuppliers =
    VALUES('GL1 Supplier Webinar Attendance'[Supplier Name])

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
        REMOVEFILTERS('GL1 Supplier Webinar Attendance'),
        'GL1 Supplier Webinar Attendance'[Attendance Status] = "Attended"
    )

VAR MatchedSuppliers =
    FILTER(
        InvitedSuppliers,
        NOT ISBLANK([Domain])
            && CONTAINS(
                AttendedDomains,
                'GL1 Supplier Webinar Attendance'[Domain],
                [Domain]
            )
    )

RETURN
    COUNTROWS(
        INTERSECT(
            CurrentSuppliers,
            SELECTCOLUMNS(
                MatchedSuppliers,
                "Supplier Name",
                [Supplier Name]
            )
        )
    )
