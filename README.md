RO Session Completion Contribution =
VAR Contribution =
    CALCULATE(
        MAX('GL1 RO Session Attendance unique'[Attended]),
        ALLEXCEPT(
            'GL1 RO Session Attendance unique',
            'GL1 RO Session Attendance unique'[RO],
            'GL1 RO Session Attendance unique'[Topic]
        )
    )
RETURN
IF(
    ISINSCOPE('GL1 RO Session Attendance unique'[Session Date]),
    BLANK(),
    IF(
        ISINSCOPE('GL1 RO Session Attendance unique'[Topic]),
        IF(Contribution = 1, 0.25, 0),
        BLANK()
    )
)
