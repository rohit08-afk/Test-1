RO Completion % for Matrix =
VAR CurrentCategories =
    VALUES('GL1 Supplier Webinar Attendance'[Category Family])
RETURN
    CALCULATE(
        [RO Overall Completion %],
        TREATAS(
            CurrentCategories,
            'GL1 RO Attendance Mapping'[Category Family]
        )
    )
