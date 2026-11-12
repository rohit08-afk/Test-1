Supplier Drillthrough Row Filter =
VAR SelectedMetric =
    SELECTEDVALUE('Supplier Drillthrough Metrics'[Metric])

VAR CurrentPriority =
    SELECTEDVALUE('GL1 Webinar Measures'[Comms Priority])

VAR HasAttended =
    [GL1 Webinar Attended] > 0

RETURN
SWITCH(
    TRUE(),

    SelectedMetric = "Webinar Attended",
        IF(HasAttended, 1, 0),

    SelectedMetric = "High Priority Not Attended",
        IF(CurrentPriority = "High" && NOT HasAttended, 1, 0),

    SelectedMetric = "Medium Priority Not Attended",
        IF(CurrentPriority = "Medium" && NOT HasAttended, 1, 0),

    BLANK()
)
