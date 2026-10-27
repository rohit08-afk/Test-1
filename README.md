RO High Priority Not Attended =
CALCULATE(
    [RO Not Attended],
    KEEPFILTERS(
        'GL1 RO Attendance Mapping'[RO Comms Priority] = "High"
    )
)

RO Medium Priority Not Attended =
CALCULATE(
    [RO Not Attended],
    KEEPFILTERS(
        'GL1 RO Attendance Mapping'[RO Comms Priority] = "Medium"
    )
)
