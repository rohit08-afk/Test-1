Supplier Drillthrough Row Filter =
VAR SelectedMetric =
    SELECTEDVALUE('Supplier Drillthrough Metrics'[Metric])

VAR CurrentSupplier =
    SELECTEDVALUE('GL1 Webinar Measures'[Supplier Name])

VAR IsHighTarget =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        REMOVEFILTERS('Supplier Integration Register'),
        'Supplier Integration Register'[Name] = CurrentSupplier,
        'Supplier Integration Register'[Comms Priority] = "High"
    ) > 0

VAR IsMediumTarget =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        REMOVEFILTERS('Supplier Integration Register'),
        'Supplier Integration Register'[Name] = CurrentSupplier,
        'Supplier Integration Register'[Comms Priority] = "Medium"
    ) > 0

VAR HasAttended =
    [GL1 Webinar Attended] > 0

RETURN
SWITCH(
    TRUE(),

    SelectedMetric = "Suppliers in scope",
        IF(IsHighTarget || IsMediumTarget, 1, 0),

    SelectedMetric = "Webinar Attended",
        IF(HasAttended, 1, 0),

    SelectedMetric = "High Priority Not Attended",
        IF(IsHighTarget && NOT HasAttended, 1, 0),

    SelectedMetric = "Medium Priority Not Attended",
        IF(IsMediumTarget && NOT HasAttended, 1, 0),

    SelectedMetric = "Remaining %",
        IF(
            (IsHighTarget || IsMediumTarget)
                && NOT HasAttended,
            1, 0
        ),

    0
)
