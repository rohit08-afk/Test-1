GL1 Lookup - Gap Areas =

VAR SupplierName =
    [Selected Supplier Name Display]

VAR SupplierNumber =
    [Selected Supplier Number]

VAR Country =
    [Selected Country]

VAR Agreement =
    [Selected Agreement Number]

VAR EPType =
    [Selected EP Type]

VAR Procurement =
    [Selected Procurement Non Procurement]

VAR CommsProgress =
    [Selected Comms Progress]

VAR RO =
    [Selected RO]

VAR ROVerified =
    [Selected RO Verified]

VAR Persona =
    [Selected Persona]

VAR PersonaVerified =
    [Selected Persona Verified]

VAR Category =
    [Selected Category Family]

VAR SubCategory =
    [Selected Sub-Category]

VAR CatSubCatVerified =
    [Selected Cat & Sub-Cat Verified]

VAR BRT =
    [Selected BRT Validator]

VAR BRTValidated =
    [Selected BRT Validation]

VAR SAPBN =
    [Selected SAP BN Status]


-- ==========================
-- MISSING VALUE CHECKS
-- ==========================

VAR SupplierNameMissing =
    ISBLANK(SupplierName)
        || TRIM(SupplierName) = ""
        || TRIM(SupplierName) = "-"
        || TRIM(SupplierName) = "--"

VAR SupplierNumberMissing =
    ISBLANK(SupplierNumber)
        || TRIM(SupplierNumber) = ""
        || TRIM(SupplierNumber) = "-"
        || TRIM(SupplierNumber) = "--"

VAR CountryMissing =
    ISBLANK(Country)
        || TRIM(Country) = ""
        || TRIM(Country) = "-"
        || TRIM(Country) = "--"

VAR AgreementMissing =
    ISBLANK(Agreement)
        || TRIM(Agreement) = ""
        || TRIM(Agreement) = "-"
        || TRIM(Agreement) = "--"

VAR EPTypeMissing =
    ISBLANK(EPType)
        || TRIM(EPType) = ""
        || TRIM(EPType) = "-"
        || TRIM(EPType) = "--"

VAR ProcurementMissing =
    ISBLANK(Procurement)
        || TRIM(Procurement) = ""
        || TRIM(Procurement) = "-"
        || TRIM(Procurement) = "--"

VAR CommsMissing =
    ISBLANK(CommsProgress)
        || TRIM(CommsProgress) = ""
        || TRIM(CommsProgress) = "-"
        || TRIM(CommsProgress) = "--"

VAR ROMissing =
    ISBLANK(RO)
        || TRIM(RO) = ""
        || TRIM(RO) = "-"
        || TRIM(RO) = "--"

VAR PersonaMissing =
    ISBLANK(Persona)
        || TRIM(Persona) = ""
        || TRIM(Persona) = "-"
        || TRIM(Persona) = "--"

VAR CategoryMissing =
    ISBLANK(Category)
        || TRIM(Category) = ""
        || TRIM(Category) = "-"
        || TRIM(Category) = "--"

VAR SubCategoryMissing =
    ISBLANK(SubCategory)
        || TRIM(SubCategory) = ""
        || TRIM(SubCategory) = "-"
        || TRIM(SubCategory) = "--"

VAR BRTMissing =
    ISBLANK(BRT)
        || TRIM(BRT) = ""
        || TRIM(BRT) = "-"
        || TRIM(BRT) = "--"

VAR SAPBNMissing =
    ISBLANK(SAPBN)
        || TRIM(SAPBN) = ""
        || TRIM(SAPBN) = "-"
        || TRIM(SAPBN) = "--"


-- ==========================
-- GAP TEXT
-- ==========================

VAR GapSupplierName =
    IF(
        SupplierNameMissing,
        "• Supplier Name Missing" & UNICHAR(10),
        ""
    )

VAR GapSupplierNumber =
    IF(
        SupplierNumberMissing,
        "• Supplier Number Missing" & UNICHAR(10),
        ""
    )

VAR GapCountry =
    IF(
        CountryMissing,
        "• Country Missing" & UNICHAR(10),
        ""
    )

VAR GapAgreement =
    IF(
        AgreementMissing,
        "• Agreement Number Missing" & UNICHAR(10),
        ""
    )

VAR GapEPType =
    IF(
        EPTypeMissing,
        "• External Party Type Missing" & UNICHAR(10),
        ""
    )

VAR GapProcurement =
    IF(
        ProcurementMissing,
        "• Procurement / Non-Procurement Missing" & UNICHAR(10),
        ""
    )

VAR GapComms =
    IF(
        CommsMissing,
        "• Comms Progress Missing" & UNICHAR(10),
        ""
    )

VAR GapRO =
    IF(
        ROMissing,
        "• Relationship Owner Missing" & UNICHAR(10),
        IF(
            UPPER(TRIM(COALESCE(ROVerified, ""))) <> "YES",
            "• Relationship Owner Not Verified" & UNICHAR(10),
            ""
        )
    )

VAR GapPersona =
    IF(
        PersonaMissing,
        "• Persona Missing" & UNICHAR(10),
        IF(
            UPPER(TRIM(COALESCE(PersonaVerified, ""))) <> "YES",
            "• Persona Not Verified" & UNICHAR(10),
            ""
        )
    )

VAR GapCategory =
    IF(
        CategoryMissing,
        "• Category Family Missing" & UNICHAR(10),
        ""
    )

VAR GapSubCategory =
    IF(
        SubCategoryMissing,
        "• Sub-Category Missing" & UNICHAR(10),
        ""
    )

VAR GapCatVerification =
    IF(
        NOT CategoryMissing
            && NOT SubCategoryMissing
            && UPPER(TRIM(COALESCE(CatSubCatVerified, ""))) <> "YES",
        "• Category / Sub-Category Not Verified" & UNICHAR(10),
        ""
    )

VAR GapBRT =
    IF(
        BRTMissing,
        "• BRT Validator Missing" & UNICHAR(10),
        IF(
            UPPER(TRIM(COALESCE(BRTValidated, ""))) <> "YES",
            "• BRT Not Validated" & UNICHAR(10),
            ""
        )
    )

VAR GapSAPBN =
    IF(
        SAPBNMissing,
        "• SAP BN Status Missing" & UNICHAR(10),
        ""
    )


VAR Result =
      GapSupplierName
    & GapSupplierNumber
    & GapCountry
    & GapAgreement
    & GapEPType
    & GapProcurement
    & GapComms
    & GapRO
    & GapPersona
    & GapCategory
    & GapSubCategory
    & GapCatVerification
    & GapBRT
    & GapSAPBN


RETURN
IF(
    Result = "",
    "✓ No gaps identified",
    Result
)
