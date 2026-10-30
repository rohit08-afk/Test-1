RO Drillthrough Row Filter =
VAR SelectedMetric =
    SELECTEDVALUE('RO Drillthrough Metrics'[Metric])
VAR CurrentRO =
    SELECTEDVALUE('GL1 RO Attendance Mapping'[RO])
VAR IsInvited =
    CALCULATE(
        MAX('GL1 RO Session Attendance unique'[Invited]),
        TREATAS(
            {CurrentRO},
            'GL1 RO Session Attendance unique'[RO]
        )
    )
VAR IsAttended =
    CALCULATE(
        MAX('GL1 RO Session Attendance unique'[Attended]),
        TREATAS(
            {CurrentRO},
            'GL1 RO Session Attendance unique'[RO]
        )
    )
RETURN
    SWITCH(
        SelectedMetric,
        "Total ROs", 1,
        "RO Invited", IF(IsInvited = 1, 1, 0),
        "Attended", IF(IsAttended = 1, 1, 0),
        "Not Attended", IF(COALESCE(IsAttended, 0) = 0, 1, 0),
        "Remaining %", IF(COALESCE(IsAttended, 0) = 0, 1, 0),
        0
    )
