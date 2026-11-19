
Fix =
CALCULATE(
    DISTINCTCOUNT('GL1 RO Attendance Mapping'[RO]),
    'GL1 RO Attendance Mapping'[Attendance] = "Attended",
    REMOVEFILTERS('RO Topics')
)
