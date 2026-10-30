RO Session Invited Display =
IF(
    ISINSCOPE('GL1 RO Session Attendance unique'[Session Date]),
    IF(
        MAX('GL1 RO Session Attendance unique'[Invited]) = 1,
        "Yes",
        "No"
    ),
    BLANK()
)

RO Session Attended Display =
IF(
    ISINSCOPE('GL1 RO Session Attendance unique'[Session Date]),
    IF(
        MAX('GL1 RO Session Attendance unique'[Attended]) = 1,
        "Yes",
        "No"
    ),
    BLANK()
)
