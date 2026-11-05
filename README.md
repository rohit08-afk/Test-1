
Supplier Session Detail Filter =
VAR SelectedMetric =
    SELECTEDVALUE('Supplier Session Metrics'[Metric])

VAR IsInvited =
    CALCULATE(
        COUNTROWS('GL1 Webinar Measures'),
        'GL1 Webinar Measures'[Invited Status] = "Invited"
    ) > 0

VAR IsAttended =
    CALCULATE(
        COUNTROWS('GL1 Webinar Measures'),
        'GL1 Webinar Measures'[Invited Status] = "Invited",
        'GL1 Webinar Measures'[Attendance Status] = "Attended"
    ) > 0

VAR IsHigh =
    CALCULATE(
        COUNTROWS('GL1 Webinar Measures'),
        'GL1 Webinar Measures'[Invited Status] = "Invited",
        'GL1 Webinar Measures'[Comms Priority] = "High"
    ) > 0

VAR IsMedium =
    CALCULATE(
        COUNTROWS('GL1 Webinar Measures'),
        'GL1 Webinar Measures'[Invited Status] = "Invited",
        'GL1 Webinar Measures'[Comms Priority] = "Medium"
    ) > 0

RETURN
SWITCH(
    TRUE(),
    SelectedMetric = "Invited" && IsInvited, 1,
    SelectedMetric = "Attended" && IsAttended, 1,
    SelectedMetric = "Not Attended"
        && IsInvited && NOT IsAttended, 1,
    SelectedMetric = "High Not Attended"
        && IsHigh && NOT IsAttended, 1,
    SelectedMetric = "Medium Not Attended"
        && IsMedium && NOT IsAttended, 1,
    SelectedMetric IN {
        "Suppliers in Scope",
        "Attendance Rate",
        "Weekly Change"
    }, 1,
    0
)
