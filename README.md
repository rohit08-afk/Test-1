RO Session Completion Contribution =
VAR CompletedTopics =
    COUNTROWS(
        FILTER(
            VALUES('GL1 RO Session Attendance unique'[Topic]),
            CALCULATE(
                MAX('GL1 RO Session Attendance unique'[Attended]),
                REMOVEFILTERS(
                    'GL1 RO Session Attendance unique'[Session Date]
                )
            ) = 1
        )
    )

RETURN
SWITCH(
    TRUE(),

    ISINSCOPE('GL1 RO Session Attendance unique'[Session Date]),
        BLANK(),

    ISINSCOPE('GL1 RO Session Attendance unique'[Topic]),
        IF(CompletedTopics > 0, 0.25, 0),

    ISINSCOPE('GL1 RO Session Attendance unique'[RO]),
        CompletedTopics * 0.25,

    BLANK()
)
