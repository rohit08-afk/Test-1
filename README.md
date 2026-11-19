RO CFM List =
VAR CurrentRO =
    VALUES('GL1 RO CFM Mapping'[RO])

RETURN
CALCULATE(
    CONCATENATEX(
        FILTER(
            VALUES('GL1 RO CFM Mapping'[CFM]),
            NOT ISBLANK('GL1 RO CFM Mapping'[CFM])
                && TRIM('GL1 RO CFM Mapping'[CFM]) <> ""
        ),
        'GL1 RO CFM Mapping'[CFM],
        ", ",
        'GL1 RO CFM Mapping'[CFM],
        ASC
    ),
    REMOVEFILTERS('GL1 RO CFM Mapping'),
    TREATAS(
        CurrentRO,
        'GL1 RO CFM Mapping'[RO]
    )
)
