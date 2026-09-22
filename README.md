RELATIONSHIP OWNER
-- Contract Owner = Relationship Owner in GL2
--------------------------------------------------

GL2 RO Assigned =
CALCULATE(
    [GL2 Total Suppliers],
    FILTER(
        'GL2 Supplier Integration Register',
        LEN(
            TRIM(
                COALESCE(
                    'GL2 Supplier Integration Register'[Contract Owner],
                    ""
                )
            )
        ) > 0
    )
)


GL2 RO Not Assigned =
[GL2 Total Suppliers] - [GL2 RO Assigned]


GL2 RO Assigned % =
DIVIDE(
    [GL2 RO Assigned],
    [GL2 Total Suppliers],
    0
)


GL2 RO Assigned Label =
FORMAT(
    [GL2 RO Assigned],
    "#,0"
)
& " / " &
FORMAT(
    [GL2 Total Suppliers],
    "#,0"
)


--------------------------------------------------
-- SUPPLIER EMAIL
--------------------------------------------------

GL2 Supplier Email Provided =
CALCULATE(
    [GL2 Total Suppliers],
    FILTER(
        'GL2 Supplier Integration Register',
        LEN(
            TRIM(
                COALESCE(
                    'GL2 Supplier Integration Register'[Supplier Email Contact],
                    ""
                )
            )
        ) > 0
    )
)


GL2 Supplier Email Missing =
[GL2 Total Suppliers] - [GL2 Supplier Email Provided]


GL2 Supplier Email Provided % =
DIVIDE(
    [GL2 Supplier Email Provided],
    [GL2 Total Suppliers],
    0
)


GL2 Supplier Email Label =
FORMAT(
    [GL2 Supplier Email Provided],
    "#,0"
)
& " / " &
FORMAT(
    [GL2 Total Suppliers],
    "#,0"
)
