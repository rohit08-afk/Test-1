RO High Priority Not Attended =
CALCULATE(
    [RO Not Attended],
    'GL1 RO Attendance Mapping'[Comms Priority] = "High"
)

RO Medium Priority Not Attended =
CALCULATE(
    [RO Not Attended],
    'GL1 RO Attendance Mapping'[Comms Priority] = "Medium"
)

RO Remaining % =
DIVIDE(
    [RO Not Attended],
    [Total ROs],
    0
)
