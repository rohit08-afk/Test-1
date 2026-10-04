GL1 Lookup - Gap Flag =
VAR GapID =
    SELECTEDVALUE('Supplier Lookup Gap Items'[Gap ID])

VAR SupplierNamePresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        'Supplier Integration Register'[Name] <> BLANK(),
        'Supplier Integration Register'[Name] <> "",
        'Supplier Integration Register'[Name] <> "--"
    ) > 0

VAR SupplierNumberPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        'Supplier Integration Register'[SAP Vendor Key.1] <> BLANK(),
        'Supplier Integration Register'[SAP Vendor Key.1] <> "",
        'Supplier Integration Register'[SAP Vendor Key.1] <> "--"
    ) > 0

VAR CountryPresent =
    CALCULATE(
        COUNTROWS('Supplier SAP BN Mapping'),
        'Supplier SAP BN Mapping'[Supplier Country] <> BLANK(),
        'Supplier SAP BN Mapping'[Supplier Country] <> "",
        'Supplier SAP BN Mapping'[Supplier Country] <> "--"
    ) > 0

VAR AgreementPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        'Supplier Integration Register'[Agreement Number] <> BLANK(),
        'Supplier Integration Register'[Agreement Number] <> "",
        'Supplier Integration Register'[Agreement Number] <> "--"
    ) > 0

VAR EPPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        'Supplier Integration Register'[EP Type - New] <> BLANK(),
        'Supplier Integration Register'[EP Type - New] <> "",
        'Supplier Integration Register'[EP Type - New] <> "--"
    ) > 0

VAR ProcurementPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        'Supplier Integration Register'[Procurement or Non Procurement] <> BLANK(),
        'Supplier Integration Register'[Procurement or Non Procurement] <> "",
        'Supplier Integration Register'[Procurement or Non Procurement] <> "--"
    ) > 0

VAR CommsPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        'Supplier Integration Register'[Comms Progress] <> BLANK(),
        'Supplier Integration Register'[Comms Progress] <> "",
        'Supplier Integration Register'[Comms Progress] <> "--"
    ) > 0

VAR ROPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        'Supplier Integration Register'[ExxonMobil Relationship Owner (RO)] <> BLANK(),
        'Supplier Integration Register'[ExxonMobil Relationship Owner (RO)] <> "",
        'Supplier Integration Register'[ExxonMobil Relationship Owner (RO)] <> "--"
    ) > 0

VAR ROVerifiedYes =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        'Supplier Integration Register'[RO Verified] = "Yes"
    ) > 0

VAR PersonaPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        'Supplier Integration Register'[Persona] <> BLANK(),
        'Supplier Integration Register'[Persona] <> "",
        'Supplier Integration Register'[Persona] <> "--"
    ) > 0

VAR PersonaVerifiedYes =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        'Supplier Integration Register'[Persona Verified] = "Yes"
    ) > 0

VAR CategoryPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        'Supplier Integration Register'[Category Family] <> BLANK(),
        'Supplier Integration Register'[Category Family] <> "",
        'Supplier Integration Register'[Category Family] <> "--"
    ) > 0

VAR SubCategoryPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        'Supplier Integration Register'[Sub-Category] <> BLANK(),
        'Supplier Integration Register'[Sub-Category] <> "",
        'Supplier Integration Register'[Sub-Category] <> "--"
    ) > 0

VAR CategoryVerifiedYes =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        'Supplier Integration Register'[Category & Sub-Category Verified?] = "Yes"
    ) > 0

VAR BRTPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        'Supplier Integration Register'[BRT Validator] <> BLANK(),
        'Supplier Integration Register'[BRT Validator] <> "",
        'Supplier Integration Register'[BRT Validator] <> "--"
    ) > 0

VAR BRTValidatedYes =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        'Supplier Integration Register'[BRT Validated] = "Yes"
    ) > 0

VAR SAPBNPresent =
    CALCULATE(
        COUNTROWS('Supplier Integration Register'),
        'Supplier Integration Register'[SAP BN Status] <> BLANK(),
        'Supplier Integration Register'[SAP BN Status] <> "",
        'Supplier Integration Register'[SAP BN Status] <> "--"
    ) > 0

RETURN
SWITCH(
    GapID,

    1,  IF(NOT SupplierNamePresent, 1, 0),
    2,  IF(NOT SupplierNumberPresent, 1, 0),
    3,  IF(NOT CountryPresent, 1, 0),
    4,  IF(NOT AgreementPresent, 1, 0),
    5,  IF(NOT EPPresent, 1, 0),
    6,  IF(NOT ProcurementPresent, 1, 0),
    7,  IF(NOT CommsPresent, 1, 0),

    8,  IF(NOT ROPresent, 1, 0),
    9,  IF(ROPresent && NOT ROVerifiedYes, 1, 0),

    10, IF(NOT PersonaPresent, 1, 0),
    11, IF(PersonaPresent && NOT PersonaVerifiedYes, 1, 0),

    12, IF(NOT CategoryPresent, 1, 0),
    13, IF(NOT SubCategoryPresent, 1, 0),

    14,
        IF(
            CategoryPresent &&
            SubCategoryPresent &&
            NOT CategoryVerifiedYes,
            1,
            0
        ),

    15, IF(NOT BRTPresent, 1, 0),
    16, IF(BRTPresent && NOT BRTValidatedYes, 1, 0),

    17, IF(NOT SAPBNPresent, 1, 0),

    0
)
