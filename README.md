Supplier Drillthrough Row Filter =
VAR SelectedMetric =
    SELECTEDVALUE('Supplier Drillthrough Metrics'[Metric])

VAR Priority =
    SELECTEDVALUE('GL1 Webinar Measures'[Comms Priority])

VAR HasAttended =
    COALESCE([Calc Webinar Attended], 0) > 0

RETURN
SWITCH(
    TRUE(),

    SelectedMetric = "Webinar Attended",
        IF(HasAttended, 1, 0),

    SelectedMetric = "High Priority Not Attended",
        IF(Priority = "High" && NOT HasAttended, 1, 0),

    SelectedMetric = "Medium Priority Not Attended",
        IF(Priority = "Medium" && NOT HasAttended, 1, 0),

    BLANK()
)
