RO Session Detail Filter =
VAR SelectedMetric =
    SELECTEDVALUE('RO Session Metrics'[Metric])
VAR IsInvited =
    [Session RO Invited] > 0
VAR IsAttended =
    [Session RO Attended] > 0
VAR IsNotAttended =
    [Session RO Not Attended] > 0
RETURN
SWITCH(
    SelectedMetric,
    "Invited", IF(IsInvited, 1, 0),
    "Attended", IF(IsAttended, 1, 0),
    "Not Attended", IF(IsNotAttended, 1, 0),
    1
)
