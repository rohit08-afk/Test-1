RO Topic Completion Contribution =
VAR CurrentRO =
    SELECTEDVALUE('GL1 RO Attendance Mapping'[RO])

VAR CurrentTopic =
    SELECTEDVALUE('RO Topics'[Topic])

VAR HasAttended =
    CALCULATE(
        COUNTROWS('GL1 RO Session Attendance unique'),
        'GL1 RO Session Attendance unique'[Attended] = 1,
        TREATAS(
            {CurrentRO},
            'GL1 RO Session Attendance unique'[RO]
        ),
        TREATAS(
            {CurrentTopic},
            'GL1 RO Session Attendance unique'[Topic]
        )
    )

RETURN
IF(
    NOT ISBLANK(CurrentRO)
        && NOT ISBLANK(CurrentTopic),
    IF(HasAttended > 0, 0.25, 0),
    BLANK()
)



RO Session Completion Contribution =
VAR CurrentRO =
    SELECTEDVALUE('GL1 RO Session Attendance unique'[RO])

VAR CurrentTopic =
    SELECTEDVALUE('GL1 RO Session Attendance unique'[Topic])

VAR HasAttended =
    CALCULATE(
        COUNTROWS('GL1 RO Session Attendance unique'),
        REMOVEFILTERS('GL1 RO Session Attendance unique'[Session Date]),
        'GL1 RO Session Attendance unique'[Attended] = 1,
        'GL1 RO Session Attendance unique'[RO] = CurrentRO,
        'GL1 RO Session Attendance unique'[Topic] = CurrentTopic
    )

RETURN
IF(
    ISINSCOPE('GL1 RO Session Attendance unique'[Topic])
        && NOT ISINSCOPE('GL1 RO Session Attendance unique'[Session Date])
        && HasAttended > 0,
    0.25,
    BLANK()
)



