RETURN
COALESCE(
    CALCULATE(
        DISTINCTCOUNT('Supplier Integration Register'[Index]),
        REMOVEFILTERS(
            'Supplier Integration Register'[Comms Progress]
        ),
        TREATAS(
            {selectedstatus},
            'Supplier Integration Register'[Comms Progress]
        )
    ),
    0
)



Comms Progress Count Label =
FORMAT(
    COALESCE([Comms Progress Visual Count], 0),
    "#,0"
)
& " / " &
FORMAT([Suppliers in Scope], "#,0")
