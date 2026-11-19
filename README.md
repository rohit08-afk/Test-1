Test =
CALCULATE(
    DISTINCTCOUNT('GL1 RO Attendance Mapping'[RO]),
    'GL1 RO Attendance Mapping'[Attendance] = "Attended",
    TREATAS(
        VALUES('RO Topics'[Topic]),
        'GL1 RO Attendance Mapping'[Topic]
    )
)
