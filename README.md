GL1 Webinar Suppliers Not Attended =
VAR AllSuppliers =
    CALCULATETABLE(
        VALUES('GL1 Supplier Webinar Attendance'[Supplier Name]),
        REMOVEFILTERS(
            'GL1 Supplier Webinar Attendance'[Attendance Status],
            'GL1 Supplier Webinar Attendance'[Webinar Date]
        )
    )
VAR AttendedSuppliers =
    CALCULATETABLE(
        VALUES('GL1 Supplier Webinar Attendance'[Supplier Name]),
        REMOVEFILTERS(
            'GL1 Supplier Webinar Attendance'[Attendance Status],
            'GL1 Supplier Webinar Attendance'[Webinar Date]
        ),
        'GL1 Supplier Webinar Attendance'[Attendance Status] = "Attended"
    )
RETURN
    COUNTROWS(
        EXCEPT(AllSuppliers, AttendedSuppliers)
    )


    GL1 Webinar Attendance Rate =
DIVIDE(
    [GL1 Webinar Suppliers Attended],
    [Your Existing Total Suppliers Measure],
    0
)


GL1 Webinar Previous Week Attended =
VAR LatestDate =
    MAXX(
        ALL('GL1 Supplier Webinar Attendance'),
        'GL1 Supplier Webinar Attendance'[Webinar Date]
    )
VAR PreviousCutoff = LatestDate - 7
RETURN
    CALCULATE(
        DISTINCTCOUNT('GL1 Supplier Webinar Attendance'[Supplier Name]),
        'GL1 Supplier Webinar Attendance'[Attendance Status] = "Attended",
        REMOVEFILTERS('GL1 Supplier Webinar Attendance'[Webinar Date]),
        'GL1 Supplier Webinar Attendance'[Webinar Date] <= PreviousCutoff
    )


    GL1 Webinar Weekly Change PP =
VAR CurrentRate = [GL1 Webinar Attendance Rate]
VAR PreviousRate =
    DIVIDE(
        [GL1 Webinar Previous Week Attended],
        [Your Existing Total Suppliers Measure],
        0
    )
RETURN
    (CurrentRate - PreviousRate) * 100



    Webinar Status =
DATATABLE(
    "Status", STRING,
    {
        {"Attended"},
        {"Not Attended"}
    }
)

GL1 Webinar Status Count =
SWITCH(
    SELECTEDVALUE('Webinar Status'[Status]),
    "Attended", [GL1 Webinar Suppliers Attended],
    "Not Attended", [GL1 Webinar Suppliers Not Attended]
)

