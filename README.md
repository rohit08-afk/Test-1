--------------------------------------------
-- 1. PERSONA VERIFIED COUNT
--------------------------------------------

GL2 Persona Verified Count =
CALCULATE(
    [GL2 Total Suppliers],
    'GL2 Supplier Integration Register'[Persona Verified] = TRUE()
)


--------------------------------------------
-- 2. PERSONA NOT VERIFIED COUNT
--------------------------------------------

GL2 Persona Not Verified Count =
[GL2 Total Suppliers] - [GL2 Persona Verified Count]


--------------------------------------------
-- 3. PERSONA VERIFIED %
--------------------------------------------

GL2 Persona Verified % =
DIVIDE(
    [GL2 Persona Verified Count],
    [GL2 Total Suppliers],
    0
)


--------------------------------------------
-- 4. BRT VALIDATED COUNT
--------------------------------------------

GL2 BRT Validated Count =
CALCULATE(
    [GL2 Total Suppliers],
    'GL2 Supplier Integration Register'[BRT Verified] = TRUE()
)


--------------------------------------------
-- 5. BRT NOT VALIDATED COUNT
--------------------------------------------

GL2 BRT Not Validated Count =
[GL2 Total Suppliers] - [GL2 BRT Validated Count]


--------------------------------------------
-- 6. BRT VALIDATED %
--------------------------------------------

GL2 BRT Validated % =
DIVIDE(
    [GL2 BRT Validated Count],
    [GL2 Total Suppliers],
    0
)


--------------------------------------------
-- 7. RO VERIFIED COUNT
--------------------------------------------

GL2 RO Verified Count =
CALCULATE(
    [GL2 Total Suppliers],
    'GL2 Supplier Integration Register'[RO Data Verified] = TRUE()
)


--------------------------------------------
-- 8. RO NOT VERIFIED COUNT
--------------------------------------------

GL2 RO Not Verified Count =
[GL2 Total Suppliers] - [GL2 RO Verified Count]


--------------------------------------------
-- 9. RO VERIFIED %
--------------------------------------------

GL2 RO Verified % =
DIVIDE(
    [GL2 RO Verified Count],
    [GL2 Total Suppliers],
    0
)


--------------------------------------------
-- 10. SUPPLIER EMAIL PROVIDED COUNT
--------------------------------------------

GL2 Supplier Email Provided Count =
CALCULATE(
    [GL2 Total Suppliers],
    NOT(
        ISBLANK(
            'GL2 Supplier Integration Register'[Supplier Email]
        )
    )
)


--------------------------------------------
-- 11. SUPPLIER EMAIL MISSING COUNT
--------------------------------------------

GL2 Supplier Email Missing Count =
[GL2 Total Suppliers] - [GL2 Supplier Email Provided Count]


--------------------------------------------
-- 12. SUPPLIER EMAIL PROVIDED %
--------------------------------------------

GL2 Supplier Email Provided % =
DIVIDE(
    [GL2 Supplier Email Provided Count],
    [GL2 Total Suppliers],
    0
)
