GL1 Webinar Suppliers Not Attended =
VAR AllSuppliers =
    CALCULATETABLE(
        VALUES('GL1 Supplier Webinar Attendance'[Supplier Name]),
        REMOVEFILTERS(
            'GL1 Supplier Webinar Attendance'[Attendance Status]
        )
    )
VAR AttendedSuppliers =
    CALCULATETABLE(
        VALUES('GL1 Supplier Webinar Attendance'[Supplier Name]),
        REMOVEFILTERS(
            'GL1 Supplier Webinar Attendance'[Attendance Status]
        ),
        'GL1 Supplier Webinar Attendance'[Attendance Status] = "Attended"
    )
RETURN
    COUNTROWS(
        EXCEPT(AllSuppliers, AttendedSuppliers)
    )
