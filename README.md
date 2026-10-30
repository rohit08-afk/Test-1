RO Topic Completion Contribution =
VAR CurrentRO =
    SELECTEDVALUE('GL1 RO Attendance Mapping'[RO])

VAR CurrentTopic =
    SELECTEDVALUE('RO Topics'[Topic])

VAR AttendedSessions =
    CALCULATE(
        COUNTROWS('GL1 RO Session Attendance unique'),
        REMOVEFILTERS('GL1 RO Session Attendance unique'),
        TREATAS(
            {CurrentRO},
            'GL1 RO Session Attendance unique'[RO]
        ),
        TREATAS(
            {CurrentTopic},
            'GL1 RO Session Attendance unique'[Topic]
        ),
        'GL1 RO Session Attendance unique'[Attended] = 1
    )

RETURN
IF(
    NOT ISBLANK(CurrentRO)
        && NOT ISBLANK(CurrentTopic),
    IF(AttendedSessions > 0, 0.25, 0),
    BLANK()
)


RO Session Completion Contribution =
VAR CurrentRO =
    SELECTEDVALUE('GL1 RO Session Attendance unique'[RO])

VAR CurrentTopic =
    SELECTEDVALUE('GL1 RO Session Attendance unique'[Topic])

VAR AttendedSessions =
    CALCULATE(
        COUNTROWS('GL1 RO Session Attendance unique'),
        REMOVEFILTERS('GL1 RO Session Attendance unique'[Session Date]),
        'GL1 RO Session Attendance unique'[RO] = CurrentRO,
        'GL1 RO Session Attendance unique'[Topic] = CurrentTopic,
        'GL1 RO Session Attendance unique'[Attended] = 1
    )

RETURN
IF(
    ISINSCOPE('GL1 RO Session Attendance unique'[Topic])
        && NOT ISINSCOPE('GL1 RO Session Attendance unique'[Session Date]),
    IF(AttendedSessions > 0, 0.25, 0),
    BLANK()
)
