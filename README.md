RO Topic Session Summary =
VAR CurrentRO =
    SELECTEDVALUE('GL1 RO Attendance Mapping'[RO])
VAR CurrentTopic =
    SELECTEDVALUE('RO Topics'[Topic])
VAR InvitedCount =
    CALCULATE(
        DISTINCTCOUNT('GL1 RO Session Attendance unique'[Session Date]),
        'GL1 RO Session Attendance unique'[Invited] = 1,
        TREATAS(
            {CurrentRO},
            'GL1 RO Session Attendance unique'[RO]
        ),
        TREATAS(
            {CurrentTopic},
            'GL1 RO Session Attendance unique'[Topic]
        )
    )
VAR AttendedCount =
    CALCULATE(
        DISTINCTCOUNT('GL1 RO Session Attendance unique'[Session Date]),
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
    FORMAT(COALESCE(InvitedCount, 0), "0")
        & " Invited | "
        & FORMAT(COALESCE(AttendedCount, 0), "0")
        & " Attended"



RO Topics =
DISTINCT(
    SELECTCOLUMNS(
        'GL1 RO Session Attendance unique',
        "Topic", 'GL1 RO Session Attendance unique'[Topic]
    )
)
        
