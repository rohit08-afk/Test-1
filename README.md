GL1 Weekly Attendance Growth PP =
VAR LatestDate =
    CALCULATE(
        MAX('GL1 Webinar Measures'[Webinar Date]),
        REMOVEFILTERS('GL1 Webinar Measures'[Webinar Date])
    )

VAR CurrentAttended =
    CALCULATE(
        DISTINCTCOUNT('GL1 Webinar Measures'[Supplier Name]),
        'GL1 Webinar Measures'[Attendance Status] = "Attended",
        REMOVEFILTERS('GL1 Webinar Measures'[Webinar Date]),
        'GL1 Webinar Measures'[Webinar Date] <= LatestDate
    )

VAR PreviousAttended =
    CALCULATE(
        DISTINCTCOUNT('GL1 Webinar Measures'[Supplier Name]),
        'GL1 Webinar Measures'[Attendance Status] = "Attended",
        REMOVEFILTERS('GL1 Webinar Measures'[Webinar Date]),
        'GL1 Webinar Measures'[Webinar Date] <= LatestDate - 7
    )

VAR TotalSuppliers =
    [Suppliers in-scope]

RETURN
    DIVIDE(
        CurrentAttended - PreviousAttended,
        TotalSuppliers,
        0
    ) * 100



    GL1 Weekly Attendance Growth Display =
FORMAT(
    [GL1 Weekly Attendance Growth PP],
    "+0.0;-0.0;0.0"
) & " pp"
