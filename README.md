
-- 1. HIGH PRIORITY NOT ATTENDED

Supplier Session High Not Attended =
CALCULATE(
    [Supplier Session Not Attended],
    'GL1 Webinar Measures'[Comms Priority] = "High"
)


-- 2. MEDIUM PRIORITY NOT ATTENDED

Supplier Session Medium Not Attended =
CALCULATE(
    [Supplier Session Not Attended],
    'GL1 Webinar Measures'[Comms Priority] = "Medium"
)


-- 3. WEEKLY CHANGE (COUNT)

Supplier Session Weekly Change Count =
VAR CurrentDate =
    SELECTEDVALUE('GL1 Webinar Measures'[Webinar Date])

VAR PreviousDate =
    CALCULATE(
        MAX('GL1 Webinar Measures'[Webinar Date]),
        REMOVEFILTERS('GL1 Webinar Measures'[Webinar Date]),
        'GL1 Webinar Measures'[Webinar Date] < CurrentDate
    )

VAR PreviousAttended =
    CALCULATE(
        [Supplier Session Attended],
        REMOVEFILTERS('GL1 Webinar Measures'[Webinar Date]),
        'GL1 Webinar Measures'[Webinar Date] = PreviousDate
    )

RETURN
IF(
    ISINSCOPE('GL1 Webinar Measures'[Webinar Date]),
    IF(
        ISBLANK(PreviousDate),
        0,
        COALESCE([Supplier Session Attended], 0)
            - COALESCE(PreviousAttended, 0)
    ),
    BLANK()
)
