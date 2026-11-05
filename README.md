
Supplier Session Detail Filter =
VAR SelectedMetric =
    SELECTEDVALUE('Supplier Session Metrics'[Metric])

VAR Invited =
    [Supplier Session Invited]

VAR Attended =
    [Supplier Session Attended]

VAR NotAttended =
    [Supplier Session Not Attended]

VAR HighNotAttended =
    [Supplier Session High Not Attended]

VAR MediumNotAttended =
    [Supplier Session Medium Not Attended]

RETURN
SWITCH(
    SelectedMetric,
    "Invited", IF(Invited > 0, 1, 0),
    "Attended", IF(Attended > 0, 1, 0),
    "Not Attended", IF(NotAttended > 0, 1, 0),
    "High Not Attended", IF(HighNotAttended > 0, 1, 0),
    "Medium Not Attended", IF(MediumNotAttended > 0, 1, 0),
    "Suppliers in Scope", 1,
    "Attendance Rate", 1,
    "Weekly Change", 1,
    0
)
