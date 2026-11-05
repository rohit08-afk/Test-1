Session Attendance Change =
VAR CurrentDate =
    MAX('GL1 RO Attendance Mapping'[Session Date])

VAR PreviousDate =
    CALCULATE(
        MAX('GL1 RO Attendance Mapping'[Session Date]),
        ALL('GL1 RO Attendance Mapping'[Session Date]),
        'GL1 RO Attendance Mapping'[Session Date] < CurrentDate
    )

VAR PreviousCount =
    CALCULATE(
        [Session RO Attended],
        ALL('GL1 RO Attendance Mapping'[Session Date]),
        'GL1 RO Attendance Mapping'[Session Date] = PreviousDate
    )

RETURN
IF(
    ISINSCOPE('GL1 RO Attendance Mapping'[Session Date]),
    IF(
        ISBLANK(PreviousDate),
        0,
        [Session RO Attended] - PreviousCount
    ),
    BLANK()
)
