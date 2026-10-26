Drilldown Category =
DATATABLE(
    "Category", STRING,
    {
        {"Webinar Attended"},
        {"Webinar Not Attended"},
        {"High Priority Not Attended"},
        {"Medium Priority Not Attended"}
    }
)


Drilldown Show Supplier =
VAR SelectedCategory =
    SELECTEDVALUE('Drilldown Category'[Category])

VAR Attended =
    [GL1 Webinar Attended] > 0

VAR Priority =
    SELECTEDVALUE('GL1 Webinar Measures'[Comms Priority])

RETURN
SWITCH(
    SelectedCategory,
    "Webinar Attended", IF(Attended, 1, 0),
    "Webinar Not Attended", IF(NOT Attended, 1, 0),
    "High Priority Not Attended",
        IF(NOT Attended && Priority = "High", 1, 0),
    "Medium Priority Not Attended",
        IF(NOT Attended && Priority = "Medium", 1, 0),
    0
)



