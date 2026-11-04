Vendor Row Count =
CALCULATE(
    COUNTROWS('GL2 - Supplier Integration Register'),
    ALLEXCEPT(
        'GL2 - Supplier Integration Register',
        'GL2 - Supplier Integration Register'[Vendor_num]
    )
)
