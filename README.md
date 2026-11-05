Supplier Session Attended =
VAR InvitedSuppliers =
    CALCULATETABLE(
        VALUES('GL1 Webinar Measures'[Supplier Name]),
        'GL1 Webinar Measures'[Invited Status] = "Invited"
    )
VAR AttendedSuppliers =
    CALCULATETABLE(
        VALUES('GL1 Webinar Measures'[Supplier Name]),
        'GL1 Webinar Measures'[Attendance Status] = "Attended"
    )
RETURN
    COUNTROWS(
        INTERSECT(InvitedSuppliers, AttendedSuppliers)
    )


    Supplier Session Not Attended =
VAR InvitedSuppliers =
    CALCULATETABLE(
        VALUES('GL1 Webinar Measures'[Supplier Name]),
        'GL1 Webinar Measures'[Invited Status] = "Invited"
    )
VAR AttendedSuppliers =
    CALCULATETABLE(
        VALUES('GL1 Webinar Measures'[Supplier Name]),
        'GL1 Webinar Measures'[Attendance Status] = "Attended"
    )
RETURN
    COUNTROWS(
        EXCEPT(InvitedSuppliers, AttendedSuppliers)
    )
