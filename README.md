RO Completion % Summary =
VAR SelectedCategories =
    VALUES(
        'GL1 Supplier Webinar Attendance'[Category Family]
    )
RETURN
CALCULATE(
    [RO Overall Completion %],
    REMOVEFILTERS('GL1 RO Attendance Mapping'[Category Family]),
    TREATAS(
        SelectedCategories,
        'GL1 RO Attendance Mapping'[Category Family]
    )
)
