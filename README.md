GL1 Check High Attended =
CALCULATE(
    [GL1 Webinar Attended Corrected],
    'GL1 Webinar Measures'[Comms Priority] = "High"
)

GL1 Check Medium Attended =
CALCULATE(
    [GL1 Webinar Attended Corrected],
    'GL1 Webinar Measures'[Comms Priority] = "Medium"
)
