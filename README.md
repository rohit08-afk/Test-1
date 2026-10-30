RO Session Completion Contribution =
VAR CurrentRO =
    SELECTEDVALUE('GL1 RO Session Attendance unique'[RO])

VAR CurrentTopic =
    SELECTEDVALUE('GL1 RO Session Attendance unique'[Topic])

VAR HasAttended =
    CALCULATE(
        COUNTROWS('GL1 RO Session Attendance unique'),
        REMOVEFILTERS('GL1 RO Session Attendance unique'),
        'GL1 RO Session Attendance unique'[RO] = CurrentRO,
        'GL1 RO Session Attendance unique'[Topic] = CurrentTopic,
        'GL1 RO Session Attendance unique'[Attended] = 1
    )

RETURN
IF(
    ISINSCOPE('GL1 RO Session Attendance unique'[Topic])
        && NOT ISINSCOPE('GL1 RO Session Attendance unique'[Session Date]),
    IF(HasAttended > 0, 0.25, 0),
    BLANK()
)
