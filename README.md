Supplier Lookup Gap Items =
DATATABLE(
    "Gap ID", INTEGER,
    "Gap Area", STRING,
    {
        {1,  "Supplier Name Missing"},
        {2,  "Supplier Number Missing"},
        {3,  "Country Missing"},
        {4,  "Agreement Number Missing"},
        {5,  "External Party Type Missing"},
        {6,  "Procurement / Non-Procurement Missing"},
        {7,  "Comms Progress Missing"},
        {8,  "Relationship Owner Missing"},
        {9,  "Relationship Owner Not Verified"},
        {10, "Persona Missing"},
        {11, "Persona Not Verified"},
        {12, "Category Family Missing"},
        {13, "Sub-Category Missing"},
        {14, "Category / Sub-Category Not Verified"},
        {15, "BRT Validator Missing"},
        {16, "BRT Not Validated"},
        {17, "SAP BN Status Missing"}
    }
)



GL1 Lookup - Gap Flag =
VAR GapID =
    SELECTEDVALUE('Supplier Lookup Gap Items'[Gap ID])

VAR SupplierName =
    SELECTEDVALUE('Supplier Integration Register'[Supplier Name])

VAR SupplierNumber =
    SELECTEDVALUE('Supplier Integration Register'[SAP Vendor Key])

VAR Country =
    SELECTEDVALUE('Supplier Integration Register'[Country])

VAR AgreementNumber =
    SELECTEDVALUE('Supplier Integration Register'[Agreement Number])

VAR ExternalPartyType =
    SELECTEDVALUE('Supplier Integration Register'[External Party Type])

VAR Procurement =
    SELECTEDVALUE('Supplier Integration Register'[Procurement or Non-Procurement])

VAR CommsProgress =
    SELECTEDVALUE('Supplier Integration Register'[Comms Progress])

VAR RO =
    SELECTEDVALUE('Supplier Integration Register'[Relationship Owner])

VAR ROVerified =
    SELECTEDVALUE('Supplier Integration Register'[Relationship Owner Verified])

VAR Persona =
    SELECTEDVALUE('Supplier Integration Register'[Persona])

VAR PersonaVerified =
    SELECTEDVALUE('Supplier Integration Register'[Persona Verified])

VAR CategoryFamily =
    SELECTEDVALUE('Supplier Integration Register'[Category Family])

VAR SubCategory =
    SELECTEDVALUE('Supplier Integration Register'[Sub Category])

VAR CategoryVerified =
    SELECTEDVALUE('Supplier Integration Register'[Cat & Sub Cat Verified])

VAR BRT =
    SELECTEDVALUE('Supplier Integration Register'[BRT Validator])

VAR BRTValidated =
    SELECTEDVALUE('Supplier Integration Register'[BRT Validated])

VAR SAPBN =
    SELECTEDVALUE('Supplier Integration Register'[SAP BN Status])

VAR SupplierNameMissing =
    ISBLANK(SupplierName) || TRIM(SupplierName) = "" || SupplierName = "--"

VAR SupplierNumberMissing =
    ISBLANK(SupplierNumber) || TRIM(SupplierNumber) = "" || SupplierNumber = "--"

VAR CountryMissing =
    ISBLANK(Country) || TRIM(Country) = "" || Country = "--"

VAR AgreementMissing =
    ISBLANK(AgreementNumber) || TRIM(AgreementNumber) = "" || AgreementNumber = "--"

VAR ExternalPartyMissing =
    ISBLANK(ExternalPartyType) || TRIM(ExternalPartyType) = "" || ExternalPartyType = "--"

VAR ProcurementMissing =
    ISBLANK(Procurement) || TRIM(Procurement) = "" || Procurement = "--"

VAR CommsMissing =
    ISBLANK(CommsProgress) || TRIM(CommsProgress) = "" || CommsProgress = "--"

VAR ROMissing =
    ISBLANK(RO) || TRIM(RO) = "" || RO = "--"

VAR PersonaMissing =
    ISBLANK(Persona) || TRIM(Persona) = "" || Persona = "--"

VAR CategoryMissing =
    ISBLANK(CategoryFamily) || TRIM(CategoryFamily) = "" || CategoryFamily = "--"

VAR SubCategoryMissing =
    ISBLANK(SubCategory) || TRIM(SubCategory) = "" || SubCategory = "--"

VAR BRTMissing =
    ISBLANK(BRT) || TRIM(BRT) = "" || BRT = "--"

VAR SAPBNMissing =
    ISBLANK(SAPBN) || TRIM(SAPBN) = "" || SAPBN = "--"

RETURN
SWITCH(
    GapID,

    1,  IF(SupplierNameMissing, 1, 0),
    2,  IF(SupplierNumberMissing, 1, 0),
    3,  IF(CountryMissing, 1, 0),
    4,  IF(AgreementMissing, 1, 0),
    5,  IF(ExternalPartyMissing, 1, 0),
    6,  IF(ProcurementMissing, 1, 0),
    7,  IF(CommsMissing, 1, 0),

    8,  IF(ROMissing, 1, 0),

    9,
        IF(
            NOT ROMissing
                && UPPER(TRIM(COALESCE(ROVerified, ""))) <> "YES",
            1,
            0
        ),

    10, IF(PersonaMissing, 1, 0),

    11,
        IF(
            NOT PersonaMissing
                && UPPER(TRIM(COALESCE(PersonaVerified, ""))) <> "YES",
            1,
            0
        ),

    12, IF(CategoryMissing, 1, 0),

    13, IF(SubCategoryMissing, 1, 0),

    14,
        IF(
            NOT CategoryMissing
                && NOT SubCategoryMissing
                && UPPER(TRIM(COALESCE(CategoryVerified, ""))) <> "YES",
            1,
            0
        ),

    15, IF(BRTMissing, 1, 0),

    16,
        IF(
            NOT BRTMissing
                && UPPER(TRIM(COALESCE(BRTValidated, ""))) <> "YES",
            1,
            0
        ),

    17, IF(SAPBNMissing, 1, 0),

    0
)
