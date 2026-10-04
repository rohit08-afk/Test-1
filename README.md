GL1 Lookup - Gap Flag =

VAR GapID =
    SELECTEDVALUE(
        'Supplier Lookup Gap Items'[Gap ID]
    )

-- =====================================================
-- CORE FIELD PRESENCE CHECKS
-- =====================================================

VAR SupplierNamePresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        FILTER(
            'Supplier Integration Register',
            NOT ISBLANK('Supplier Integration Register'[Name])
                && TRIM('Supplier Integration Register'[Name]) <> ""
                && TRIM('Supplier Integration Register'[Name]) <> "-"
                && TRIM('Supplier Integration Register'[Name]) <> "--"
        )
    ) > 0


VAR SupplierNumberPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        FILTER(
            'Supplier Integration Register',
            NOT ISBLANK('Supplier Integration Register'[SAP Vendor Key.1])
                && TRIM('Supplier Integration Register'[SAP Vendor Key.1]) <> ""
                && TRIM('Supplier Integration Register'[SAP Vendor Key.1]) <> "-"
                && TRIM('Supplier Integration Register'[SAP Vendor Key.1]) <> "--"
        )
    ) > 0


VAR CountryPresent =
    CALCULATE(
        COUNTROWS('Supplier SAP BN Mapping'),
        FILTER(
            'Supplier SAP BN Mapping',
            NOT ISBLANK('Supplier SAP BN Mapping'[Supplier Country])
                && TRIM('Supplier SAP BN Mapping'[Supplier Country]) <> ""
                && TRIM('Supplier SAP BN Mapping'[Supplier Country]) <> "-"
                && TRIM('Supplier SAP BN Mapping'[Supplier Country]) <> "--"
        )
    ) > 0


VAR AgreementPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        FILTER(
            'Supplier Integration Register',
            NOT ISBLANK('Supplier Integration Register'[Agreement Number])
                && TRIM('Supplier Integration Register'[Agreement Number]) <> ""
                && TRIM('Supplier Integration Register'[Agreement Number]) <> "-"
                && TRIM('Supplier Integration Register'[Agreement Number]) <> "--"
        )
    ) > 0


VAR ExternalPartyTypePresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        FILTER(
            'Supplier Integration Register',
            NOT ISBLANK('Supplier Integration Register'[EP Type - New])
                && TRIM('Supplier Integration Register'[EP Type - New]) <> ""
                && TRIM('Supplier Integration Register'[EP Type - New]) <> "-"
                && TRIM('Supplier Integration Register'[EP Type - New]) <> "--"
        )
    ) > 0


VAR ProcurementPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        FILTER(
            'Supplier Integration Register',
            NOT ISBLANK('Supplier Integration Register'[Procurement or Non Procurement])
                && TRIM('Supplier Integration Register'[Procurement or Non Procurement]) <> ""
                && TRIM('Supplier Integration Register'[Procurement or Non Procurement]) <> "-"
                && TRIM('Supplier Integration Register'[Procurement or Non Procurement]) <> "--"
        )
    ) > 0


VAR CommsProgressPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        FILTER(
            'Supplier Integration Register',
            NOT ISBLANK('Supplier Integration Register'[Comms Progress])
                && TRIM('Supplier Integration Register'[Comms Progress]) <> ""
                && TRIM('Supplier Integration Register'[Comms Progress]) <> "-"
                && TRIM('Supplier Integration Register'[Comms Progress]) <> "--"
        )
    ) > 0


VAR ROPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        FILTER(
            'Supplier Integration Register',
            NOT ISBLANK(
                'Supplier Integration Register'[ExxonMobil Relationship Owner (RO)]
            )
                && TRIM(
                    'Supplier Integration Register'[ExxonMobil Relationship Owner (RO)]
                ) <> ""
                && TRIM(
                    'Supplier Integration Register'[ExxonMobil Relationship Owner (RO)]
                ) <> "-"
                && TRIM(
                    'Supplier Integration Register'[ExxonMobil Relationship Owner (RO)]
                ) <> "--"
        )
    ) > 0


VAR PersonaPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        FILTER(
            'Supplier Integration Register',
            NOT ISBLANK('Supplier Integration Register'[Persona])
                && TRIM('Supplier Integration Register'[Persona]) <> ""
                && TRIM('Supplier Integration Register'[Persona]) <> "-"
                && TRIM('Supplier Integration Register'[Persona]) <> "--"
        )
    ) > 0


VAR CategoryPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        FILTER(
            'Supplier Integration Register',
            NOT ISBLANK('Supplier Integration Register'[Category Family])
                && TRIM('Supplier Integration Register'[Category Family]) <> ""
                && TRIM('Supplier Integration Register'[Category Family]) <> "-"
                && TRIM('Supplier Integration Register'[Category Family]) <> "--"
        )
    ) > 0


VAR SubCategoryPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        FILTER(
            'Supplier Integration Register',
            NOT ISBLANK('Supplier Integration Register'[Sub-Category])
                && TRIM('Supplier Integration Register'[Sub-Category]) <> ""
                && TRIM('Supplier Integration Register'[Sub-Category]) <> "-"
                && TRIM('Supplier Integration Register'[Sub-Category]) <> "--"
        )
    ) > 0


VAR BRTPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        FILTER(
            'Supplier Integration Register',
            NOT ISBLANK('Supplier Integration Register'[BRT Validator])
                && TRIM('Supplier Integration Register'[BRT Validator]) <> ""
                && TRIM('Supplier Integration Register'[BRT Validator]) <> "-"
                && TRIM('Supplier Integration Register'[BRT Validator]) <> "--"
        )
    ) > 0


VAR SAPBNPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        FILTER(
            'Supplier Integration Register',
            NOT ISBLANK('Supplier Integration Register'[SAP BN Status])
                && TRIM('Supplier Integration Register'[SAP BN Status]) <> ""
                && TRIM('Supplier Integration Register'[SAP BN Status]) <> "-"
                && TRIM('Supplier Integration Register'[SAP BN Status]) <> "--"
        )
    ) > 0


-- =====================================================
-- VERIFICATION / VALIDATION CHECKS
-- =====================================================

VAR ROVerifiedYes =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        FILTER(
            'Supplier Integration Register',
            UPPER(
                TRIM(
                    COALESCE(
                        'Supplier Integration Register'[RO Verified],
                        ""
                    )
                )
            ) = "YES"
        )
    ) > 0


VAR PersonaVerifiedYes =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        FILTER(
            'Supplier Integration Register',
            UPPER(
                TRIM(
                    COALESCE(
                        'Supplier Integration Register'[Persona Verified],
                        ""
                    )
                )
            ) = "YES"
        )
    ) > 0


VAR CategoryVerifiedYes =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        FILTER(
            'Supplier Integration Register',
            UPPER(
                TRIM(
                    COALESCE(
                        'Supplier Integration Register'[Category & Sub-Category Verified?],
                        ""
                    )
                )
            ) = "YES"
        )
    ) > 0


VAR BRTValidatedYes =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        FILTER(
            'Supplier Integration Register',
            UPPER(
                TRIM(
                    COALESCE(
                        'Supplier Integration Register'[BRT Validated],
                        ""
                    )
                )
            ) = "YES"
        )
    ) > 0


-- =====================================================
-- GAP OUTPUT
-- =====================================================

RETURN

SWITCH(
    GapID,

    1,
        IF(
            NOT SupplierNamePresent,
            1,
            0
        ),

    2,
        IF(
            NOT SupplierNumberPresent,
            1,
            0
        ),

    3,
        IF(
            NOT CountryPresent,
            1,
            0
        ),

    4,
        IF(
            NOT AgreementPresent,
            1,
            0
        ),

    5,
        IF(
            NOT ExternalPartyTypePresent,
            1,
            0
        ),

    6,
        IF(
            NOT ProcurementPresent,
            1,
            0
        ),

    7,
        IF(
            NOT CommsProgressPresent,
            1,
            0
        ),

    8,
        IF(
            NOT ROPresent,
            1,
            0
        ),

    9,
        IF(
            ROPresent
                && NOT ROVerifiedYes,
            1,
            0
        ),

    10,
        IF(
            NOT PersonaPresent,
            1,
            0
        ),

    11,
        IF(
            PersonaPresent
                && NOT PersonaVerifiedYes,
            1,
            0
        ),

    12,
        IF(
            NOT CategoryPresent,
            1,
            0
        ),

    13,
        IF(
            NOT SubCategoryPresent,
            1,
            0
        ),

    14,
        IF(
            CategoryPresent
                && SubCategoryPresent
                && NOT CategoryVerifiedYes,
            1,
            0
        ),

    15,
        IF(
            NOT BRTPresent,
            1,
            0
        ),

    16,
        IF(
            BRTPresent
                && NOT BRTValidatedYes,
            1,
            0
        ),

    17,
        IF(
            NOT SAPBNPresent,
            1,
            0
        ),

    0
)
