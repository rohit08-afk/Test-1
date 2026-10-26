RETURN
COUNTROWS(
    DISTINCT(
        SELECTCOLUMNS(
            FILTER(
                MatchedSuppliers,
                NOT ISBLANK([Supplier Name])
            ),
            "Supplier", [Supplier Name]
        )
    )
)
