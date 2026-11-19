RO CFM List =
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
)
