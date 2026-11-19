RO CFM Selection Filter =
VAR CurrentRO =
    COALESCE(
        SELECTEDVALUE('GL1 RO CFM Display'[RO]),
        SELECTEDVALUE('GL1 RO Session Attendance unique'[RO])
    )

VAR SelectedCFMs =
    VALUES('GL1 RO CFM Mapping'[CFM])

VAR MatchingRows =
    CALCULATE(
        COUNTROWS('GL1 RO CFM Mapping'),
        REMOVEFILTERS('GL1 RO CFM Mapping'),
        'GL1 RO CFM Mapping'[RO] = CurrentRO,
        TREATAS(
            SelectedCFMs,
            'GL1 RO CFM Mapping'[CFM]
        )
    )

RETURN
IF(
    NOT ISBLANK(CurrentRO) &&
    MatchingRows > 0,
    1,
    0
)
