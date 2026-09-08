Test SAP Vendor Key =
VAR SelectedSupplier =
    SELECTEDVALUE(
        'Supplier Integration Register'[Name]
    )
RETURN
CALCULATE(
    SELECTEDVALUE(
        'Master File Supplier Integration D1 List'[SAP Vendor Key]
    ),
    TREATAS(
        {SelectedSupplier},
        'Master File Supplier Integration D1 List'[Vendor Name - Clean]
    )
)    )

RETURN
COALESCE(Result, "-")
