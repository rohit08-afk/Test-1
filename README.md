GL1 High Priority Not Attended =
CALCULATE(
    [GL1 Summary Not Attended],
    'GL1 Webinar Measures'[Comms Priority] = "High"
)


GL1 Medium Priority Not Attended =
CALCULATE(
    [GL1 Summary Not Attended],
    'GL1 Webinar Measures'[Comms Priority] = "Medium"
)

