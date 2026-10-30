GL2 Comms Progress Count =
VAR SelectedStatus =
    SELECTEDVALUE(
        'Comms Progress Visual'[Comms Progress Display]
    )
RETURN
COALESCE(
    CALCULATE(
        DISTINCTCOUNT(
            'GL2 - Supplier Integration Register'[Vendor Number]
        ),
        REMOVEFILTERS(
            'GL2 - Supplier Integration Register'[Comms Progress]
        ),
        TREATAS(
            {SelectedStatus},
            'GL2 - Supplier Integration Register'[Comms Progress]
        )
    ),
    0
)


GL2 Comms Progress Remaining =
MAX(
    0,
    [GL2 Suppliers in Scope] -
    [GL2 Comms Progress Count]
)


GL2 Comms Progress % =
DIVIDE(
    [GL2 Comms Progress Count],
    [GL2 Suppliers in Scope],
    0
)


GL2 Comms Progress Count Label =
FORMAT([GL2 Comms Progress Count], "#,0")
& " / " &
FORMAT([GL2 Suppliers in Scope], "#,0")
