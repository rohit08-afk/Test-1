Supplier Detail Invitation Status =
IF(
    CALCULATE(
        COUNTROWS('GL1 Webinar Measures'),
        'GL1 Webinar Measures'[Invited Status] = "Invited"
    ) > 0,
    "Invited",
    "Not Invited"
)


Supplier Detail Attendance Status =
IF(
    CALCULATE(
        COUNTROWS('GL1 Webinar Measures'),
        'GL1 Webinar Measures'[Invited Status] = "Invited",
        'GL1 Webinar Measures'[Attendance Status] = "Attended"
    ) > 0,
    "Attended",
    "Not Attended"
)
