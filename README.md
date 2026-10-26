GL1 Webinar Suppliers Not Attended =
VAR InvitedDomains =
    CALCULATETABLE(
        VALUES('GL1 Supplier Webinar Attendance'[Domain]),
        REMOVEFILTERS('GL1 Supplier Webinar Attendance'[Invited Status]),
        'GL1 Supplier Webinar Attendance'[Invited Status] = "Invited"
    )

VAR AttendedDomains =
    CALCULATETABLE(
        VALUES('GL1 Supplier Webinar Attendance'[Domain]),
        REMOVEFILTERS('GL1 Supplier Webinar Attendance'[Attendance Status]),
        'GL1 Supplier Webinar Attendance'[Attendance Status] = "Attended"
    )

RETURN
    COUNTROWS(
        EXCEPT(InvitedDomains, AttendedDomains)
    )


    GL1 Webinar Suppliers Attended =
VAR InvitedDomains =
    CALCULATETABLE(
        VALUES('GL1 Supplier Webinar Attendance'[Domain]),
        REMOVEFILTERS('GL1 Supplier Webinar Attendance'[Invited Status]),
        'GL1 Supplier Webinar Attendance'[Invited Status] = "Invited"
    )

VAR AttendedDomains =
    CALCULATETABLE(
        VALUES('GL1 Supplier Webinar Attendance'[Domain]),
        REMOVEFILTERS('GL1 Supplier Webinar Attendance'[Attendance Status]),
        'GL1 Supplier Webinar Attendance'[Attendance Status] = "Attended"
    )

RETURN
    COUNTROWS(
        INTERSECT(InvitedDomains, AttendedDomains)
    )
