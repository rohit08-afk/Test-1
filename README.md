Selected SAP BN Onboarding Status =
VAR SelectedSupplier =
    SELECTEDVALUE(
        'Supplier Integration Register'[Name]
    )

VAR VendorKey =
    CALCULATE(
        SELECTEDVALUE(
            'Master File Supplier Integration D1 List'[SAP Vendor Key]
        ),
        TREATAS(
            {SelectedSupplier},
            'Master File Supplier Integration D1 List'[Vendor Name - Clean]
        )
    )

VAR Result =
    CALCULATE(
        SELECTEDVALUE(
            'SAP BN Onboarding'[Onboarding Status]
        ),
        TREATAS(
            {VendorKey},
            'SAP BN Onboarding'[SAP Vendor Key]
        )
    )

RETURN
COALESCE(Result, "-")
