RO Completion % TREATAS =
VAR SelectedCategories =
    VALUES('GL1 Webinar Measures'[Category Family])
RETURN
    CALCULATE(
        [RO Overall Completion %],
        REMOVEFILTERS('GL1 RO Attendance Mapping'[Category Family]),
        TREATAS(
            SelectedCategories,
            'GL1 RO Attendance Mapping'[Category Family]
        )
    )
