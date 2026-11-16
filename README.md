RO Completion % Summary =
VAR SelectedCategories =
    VALUES(
        'GL1 Supplier Webinar Attendance'[Category Family]
    )

VAR FilteredROs =
    CALCULATETABLE(
        VALUES('GL1 RO Attendance Mapping'[RO]),
        REMOVEFILTERS('GL1 RO Attendance Mapping'[Category Family]),
        TREATAS(
            SelectedCategories,
            'GL1 RO Attendance Mapping'[Category Family]
        )
    )

VAR CompletedTopics =
    SUMX(
        FilteredROs,
        VAR CurrentRO =
            'GL1 RO Attendance Mapping'[RO]
        RETURN
            CALCULATE(
                DISTINCTCOUNT(
                    'GL1 RO Session Attendance unique'[Topic]
                ),
                'GL1 RO Session Attendance unique'[Attended] = 1,
                TREATAS(
                    { CurrentRO },
                    'GL1 RO Session Attendance unique'[RO]
                )
            )
    )

RETURN
    DIVIDE(
        CompletedTopics,
        COUNTROWS(FilteredROs) * 4,
        0
    )
