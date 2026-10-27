RO Completion % for Matrix =
VAR CurrentCategory =
    SELECTEDVALUE(
        'GL1 Supplier Webinar Attendance'[Category Family]
    )
RETURN
    IF(
        NOT ISBLANK(CurrentCategory),
        CALCULATE(
            [RO Overall Completion %],
            REMOVEFILTERS('GL1 RO Attendance Mapping'),
            'GL1 RO Attendance Mapping'[Category Family] = CurrentCategory
        ),
        [RO Overall Completion %]
    )
