RO Session Invited Display =
IF(
    MAX('GL1 RO Session Attendance unique'[Invited]) = 1,
    "Yes",
    "No"
)


RO Session Attended Display =
IF(
    MAX('GL1 RO Session Attendance unique'[Attended]) = 1,
    "Yes",
    "No"
)



RO Session Breakdown Filter =
VAR CurrentRO =
    SELECTEDVALUE('GL1 RO Session Attendance unique'[RO])

VAR EligibleROs =
    FILTER(
        VALUES('GL1 RO Attendance Mapping'[RO]),
        CALCULATE([RO Drillthrough Row Filter]) = 1
    )

RETURN
    IF(
        NOT ISBLANK(CurrentRO)
            && CONTAINS(
                EligibleROs,
                'GL1 RO Attendance Mapping'[RO],
                CurrentRO
            ),
        1,
        0
    )
