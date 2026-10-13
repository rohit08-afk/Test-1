GL1 Webinar High Priority Total =
CALCULATE(
    [GL1 Webinar Total Suppliers],
    'GL1 Webinar Supplier lookup'[Comms Priority] = "High"
)

GL1 Webinar High Priority Completed =
CALCULATE(
    [GL1 Webinar Completed],
    'GL1 Webinar Supplier lookup'[Comms Priority] = "High"
)

GL1 Webinar Medium Priority Total =
CALCULATE(
    [GL1 Webinar Total Suppliers],
    'GL1 Webinar Supplier lookup'[Comms Priority] = "Medium"
)

GL1 Webinar Medium Priority Completed =
CALCULATE(
    [GL1 Webinar Completed],
    'GL1 Webinar Supplier lookup'[Comms Priority] = "Medium"
)

GL1 Webinar High Completion % =
DIVIDE(
    [GL1 Webinar High Priority Completed],
    [GL1 Webinar High Priority Total],
    0
)

GL1 Webinar Medium Completion % =
DIVIDE(
    [GL1 Webinar Medium Priority Completed],
    [GL1 Webinar Medium Priority Total],
    0
)

