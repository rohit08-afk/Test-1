Supplier Session Detail Filter =
VAR MetricSelected =
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

VAR Priority =
    SELECTEDVALUE('GL1 Webinar Measures'[Comms Priority])

RETURN
SWITCH(
    TRUE(),
    MetricSelected = "Invited" && IsInvited, 1,
    MetricSelected = "Attended" && IsAttended, 1,
    MetricSelected = "Not Attended"
        && IsInvited && NOT IsAttended, 1,
    MetricSelected = "High Not Attended"
        && IsInvited && NOT IsAttended && Priority = "High", 1,
    MetricSelected = "Medium Not Attended"
        && IsInvited && NOT IsAttended && Priority = "Medium", 1,
    MetricSelected IN {
        "Suppliers in Scope",
        "Attendance Rate",
        "Weekly Change"
    }, 1,
    0
)


Selected Supplier Persona =
SELECTEDVALUE(
    'GL1 Webinar Measures'[Persona],
    "All Personas"
)


Selected Supplier Webinar Date =
VAR SelectedDate =
    SELECTEDVALUE('GL1 Webinar Measures'[Webinar Date])
RETURN
IF(
    ISBLANK(SelectedDate),
    "All Sessions",
    FORMAT(SelectedDate, "dd MMM yyyy")
)


