GL1 Lookup - Gap Flag =
VAR GapID =
    SELECTEDVALUE('Supplier Lookup Gap Items'[Gap ID])

VAR SupplierName =
    SELECTEDVALUE('Supplier Integration Register'[Name])

VAR SupplierNumber =
    SELECTEDVALUE('Supplier Integration Register'[SAP Vendor Key.1])

VAR Country =
    SELECTEDVALUE('Supplier SAP BN Mapping'[Supplier Country])

VAR AgreementNumber =
    SELECTEDVALUE('Supplier Integration Register'[Agreement Number])

VAR ExternalPartyType =
    SELECTEDVALUE('Supplier Integration Register'[EP Type - New])

VAR Procurement =
    SELECTEDVALUE('Supplier Integration Register'[Procurement or Non Procurement])

VAR CommsProgress =
    SELECTEDVALUE('Supplier Integration Register'[Comms Progress])

VAR RO =
    SELECTEDVALUE('Supplier Integration Register'[ExxonMobil Relationship Owner (RO)])

VAR ROVerified =
    SELECTEDVALUE('Supplier Integration Register'[RO Verified])

VAR Persona =
    SELECTEDVALUE('Supplier Integration Register'[Persona])

VAR PersonaVerified =
    SELECTEDVALUE('Supplier Integration Register'[Persona Verified])

VAR CategoryFamily =
    SELECTEDVALUE('Supplier Integration Register'[Category Family])

VAR SubCategory =
    SELECTEDVALUE('Supplier Integration Register'[Sub-Category])

VAR CategoryVerified =
    SELECTEDVALUE('Supplier Integration Register'[Category & Sub-Category Verified?])

VAR BRT =
    SELECTEDVALUE('Supplier Integration Register'[BRT Validator])

VAR BRTValidated =
    SELECTEDVALUE('Supplier Integration Register'[BRT Validated])

VAR SAPBN =
    SELECTEDVALUE('Supplier Integration Register'[SAP BN Status])


VAR SupplierNameMissing =
    ISBLANK(SupplierName)
        || TRIM(SupplierName) = ""
        || SupplierName = "--"
        || SupplierName = "-"

VAR SupplierNumberMissing =
    ISBLANK(SupplierNumber)
        || TRIM(SupplierNumber) = ""
        || SupplierNumber = "--"
        || SupplierNumber = "-"

VAR CountryMissing =
    ISBLANK(Country)
        || TRIM(Country) = ""
        || Country = "--"
        || Country = "-"

VAR AgreementMissing =
    ISBLANK(AgreementNumber)
        || TRIM(AgreementNumber) = ""
        || AgreementNumber = "--"
        || AgreementNumber = "-"

VAR ExternalPartyMissing =
    ISBLANK(ExternalPartyType)
        || TRIM(ExternalPartyType) = ""
        || ExternalPartyType = "--"
        || ExternalPartyType = "-"

VAR ProcurementMissing =
    ISBLANK(Procurement)
        || TRIM(Procurement) = ""
        || Procurement = "--"
        || Procurement = "-"

VAR CommsMissing =
    ISBLANK(CommsProgress)
        || TRIM(CommsProgress) = ""
        || CommsProgress = "--"
        || CommsProgress = "-"

VAR ROMissing =
    ISBLANK(RO)
        || TRIM(RO) = ""
        || RO = "--"
        || RO = "-"

VAR PersonaMissing =
    ISBLANK(Persona)
        || TRIM(Persona) = ""
        || Persona = "--"
        || Persona = "-"

VAR CategoryMissing =
    ISBLANK(CategoryFamily)
        || TRIM(CategoryFamily) = ""
        || CategoryFamily = "--"
        || CategoryFamily = "-"

VAR SubCategoryMissing =
    ISBLANK(SubCategory)
        || TRIM(SubCategory) = ""
        || SubCategory = "--"
        || SubCategory = "-"

VAR BRTMissing =
    ISBLANK(BRT)
        || TRIM(BRT) = ""
        || BRT = "--"
        || BRT = "-"

VAR SAPBNMissing =
    ISBLANK(SAPBN)
        || TRIM(SAPBN) = ""
        || SAPBN = "--"
        || SAPBN = "-"


RETURN
SWITCH(
    GapID,

    1, IF(SupplierNameMissing, 1, 0),

    2, IF(SupplierNumberMissing, 1, 0),

    3, IF(CountryMissing, 1, 0),

    4, IF(AgreementMissing, 1, 0),

    5, IF(ExternalPartyMissing, 1, 0),

    6, IF(ProcurementMissing, 1, 0),

    7, IF(CommsMissing, 1, 0),

    8, IF(ROMissing, 1, 0),

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
