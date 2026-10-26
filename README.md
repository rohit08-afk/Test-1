GL1 Check Attendance Overlap =
VAR HighSuppliers =
    CALCULATETABLE(
        VALUES('GL1 Webinar Measures'[Supplier Name]),
        'GL1 Webinar Measures'[Comms Priority] = "High",
        FILTER(
            VALUES('GL1 Webinar Measures'[Supplier Name]),
            [GL1 Webinar Attended Corrected] > 0
        )
    )

VAR MediumSuppliers =
    CALCULATETABLE(
        VALUES('GL1 Webinar Measures'[Supplier Name]),
        'GL1 Webinar Measures'[Comms Priority] = "Medium",
        FILTER(
            VALUES('GL1 Webinar Measures'[Supplier Name]),
            [GL1 Webinar Attended Corrected] > 0
        )
    )

RETURN
    COUNTROWS(
        INTERSECT(HighSuppliers, MediumSuppliers)
    )
