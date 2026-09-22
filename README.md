--------------------------------------------------
-- 0. SUPPLIERS IN SCOPE
--------------------------------------------------

GL2 Total Suppliers =
DISTINCTCOUNT(
    'GL2 Supplier Integration Register'[Vendor_num]
)


--------------------------------------------------
-- PERSONA
--------------------------------------------------

GL2 Persona Assigned =
CALCULATE(
    [GL2 Total Suppliers],
    FILTER(
        'GL2 Supplier Integration Register',
        LEN(
            TRIM(
                COALESCE(
                    'GL2 Supplier Integration Register'[Persona],
                    ""
                )
            )
        ) > 0
    )
)


GL2 Persona Not Assigned =
[GL2 Total Suppliers] - [GL2 Persona Assigned]


GL2 Persona Assigned % =
DIVIDE(
    [GL2 Persona Assigned],
    [GL2 Total Suppliers],
    0
)


GL2 Persona Assigned Label =
FORMAT(
    [GL2 Persona Assigned],
    "#,0"
)
& " / " &
FORMAT(
    [GL2 Total Suppliers],
    "#,0"
)


--------------------------------------------------
-- BRT
--------------------------------------------------

GL2 BRT Assigned =
CALCULATE(
    [GL2 Total Suppliers],
    FILTER(
        'GL2 Supplier Integration Register',
        LEN(
            TRIM(
                COALESCE(
                    'GL2 Supplier Integration Register'[BRT Validator],
                    ""
                )
            )
        ) > 0
    )
)


GL2 BRT Not Assigned =
[GL2 Total Suppliers] - [GL2 BRT Assigned]


GL2 BRT Assigned % =
DIVIDE(
    [GL2 BRT Assigned],
    [GL2 Total Suppliers],
    0
)


GL2 BRT Assigned Label =
FORMAT(
    [GL2 BRT Assigned],
    "#,0"
)
& " / " &
FORMAT(
    [GL2 Total Suppliers],
    "#,0"
)


--------------------------------------------------
-- RELATIONSHIP OWNER
-- Contract Owner = Relationship Owner in GL2
--------------------------------------------------
