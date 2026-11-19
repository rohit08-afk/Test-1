GL1 RO CFM Display =
ADDCOLUMNS(
    DISTINCT(
        SELECTCOLUMNS(
            'GL1 RO CFM Mapping',
            "RO", 'GL1 RO CFM Mapping'[RO]
        )
    ),
    "CFM List",
    VAR CurrentRO = [RO]
    RETURN
        CONCATENATEX(
            FILTER(
                'GL1 RO CFM Mapping',
                'GL1 RO CFM Mapping'[RO] = CurrentRO
                    && NOT ISBLANK('GL1 RO CFM Mapping'[CFM])
                    && TRIM('GL1 RO CFM Mapping'[CFM]) <> ""
            ),
            'GL1 RO CFM Mapping'[CFM],
            ", ",
            'GL1 RO CFM Mapping'[CFM],
            ASC
        )
)
