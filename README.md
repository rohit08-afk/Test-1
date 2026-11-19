GL1 CFM Master =
DISTINCT(
    UNION(
        SELECTCOLUMNS(
            'GL1 RO CFM Mapping',
            "CFM", 'GL1 RO CFM Mapping'[CFM]
        ),
        SELECTCOLUMNS(
            'GL1 - Supplier Integration Register',
            "CFM", 'GL1 - Supplier Integration Register'[CFM]
        )
    )
)
