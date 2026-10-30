GL2 Excluded from Comms =
CALCULATE(
    DISTINCTCOUNT(
        'GL2 - Supplier Integration Register'[Vendor Number]
    ),
    REMOVEFILTERS(
        'GL2 - Supplier Integration Register'[Comms Progress]
    ),
    'GL2 - Supplier Integration Register'[Comms Progress]
        = "7-Exclude from Comms"
)
