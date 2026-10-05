GL2 Supplier Email Provided =
CALCULATE(
    DISTINCTCOUNT(
        'GL2 - Supplier Integration Register'[Vendor_num]
    ),
    FILTER(
        ALLSELECTED('GL2 - Supplier Integration Register'),
        LEN(
            TRIM(
                'GL2 - Supplier Integration Register'[Supplier Email Contact] & ""
            )
        ) > 0
        &&
        TRIM(
            'GL2 - Supplier Integration Register'[Supplier Email Contact] & ""
        ) <> "--"
    )
)


.
