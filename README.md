Webinar Detail Max Duration =
MAX('GL1 Webinar Measures'[Attendance Duration])

Webinar Detail Attended =
IF(
    CALCULATE(
        COUNTROWS('GL1 Webinar Measures'),
        'GL1 Webinar Measures'[Attendance Status] = "Attended"
    ) > 0,
    "Attended",
    "Not Attended"
)


Webinar Detail Invited =
IF(
    CALCULATE(
        COUNTROWS('GL1 Webinar Measures'),
        'GL1 Webinar Measures'[Invited Status] = "Invited"
    ) > 0,
    "Invited",
    "Not Invited"
)
