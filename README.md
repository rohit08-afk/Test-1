RO Session Completion Contribution =
VAR HasAttended =
    CALCULATE(
        MAX('GL1 RO Session Attendance unique'[Attended]),
        ALLEXCEPT(
            'GL1 RO Session Attendance unique',
            'GL1 RO Session Attendance unique'[RO],
            'GL1 RO Session Attendance unique'[Topic]
        )
    )
RETURN
    IF(HasAttended = 1, 0.25, 0)
