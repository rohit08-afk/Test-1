RO Topic Attended =
VAR SelectedROs =
    VALUES('GL1 RO Attendance Mapping'[RO])

VAR SelectedTopics =
    VALUES('RO Topics'[Topic])

RETURN
CALCULATE(
    DISTINCTCOUNT('GL1 RO Session Attendance unique'[RO]),

    TREATAS(
        SelectedROs,
        'GL1 RO Session Attendance unique'[RO]
    ),

    TREATAS(
        SelectedTopics,
        'GL1 RO Session Attendance unique'[Topic]
    ),

    'GL1 RO Session Attendance unique'[Attended] = 1
)
