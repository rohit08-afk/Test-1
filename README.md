Webinar Detail People Attended =
CALCULATE(
    DISTINCTCOUNT('GL1 Webinar Measures'[Supplier Contact]),
    'GL1 Webinar Measures'[Attendance Status] = "Attended",
    'GL1 Webinar Measures'[Supplier Contact] <> BLANK()
)
