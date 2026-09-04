# Test-1

SAP BN Match =
VAR VendorKey =
    'Supplier Vendor Bridge'[SAP Vendor Key]
RETURN
    IF(
        CONTAINS(
            'SAP BN Onboarding',
            'SAP BN Onboarding'[SAP Vendor Key],
            VendorKey
        ),
        "Yes",
        "No"
    )
