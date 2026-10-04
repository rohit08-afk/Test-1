GL2 Lookup - Gap Areas =

VAR SupplierName =
    [GL2 Lookup - Supplier Name]

VAR SupplierNumber =
    [GL2 Lookup - Supplier Number]

VAR Country =
    [GL2 Lookup - Country]

VAR Agreement =
    [GL2 Lookup - Agreement Number]

VAR EPType =
    [GL2 Lookup - External Party Type]

VAR Procurement =
    [GL2 Lookup - Procurement]

VAR CommsProgress =
    [GL2 Lookup - Comms Progress]

VAR RO =
    [GL2 Lookup - Relationship Owner]

VAR Persona =
    [GL2 Lookup - Persona]

VAR Category =
    [GL2 Lookup - Category Family]

VAR SubCategory =
    [GL2 Lookup - Sub-Category]

VAR BRT =
    [GL2 Lookup - BRT Validator]

VAR SAPBN =
    [GL2 Lookup - SAP BN Status]


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
        "• Relationship Owner Not Verified" & UNICHAR(10)
    )

VAR GapPersona =
    IF(
        PersonaMissing,
        "• Persona Missing" & UNICHAR(10),
        "• Persona Not Verified" & UNICHAR(10)
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
            && NOT SubCategoryMissing,
        "• Category / Sub-Category Not Verified" & UNICHAR(10),
        ""
    )

VAR GapBRT =
    IF(
        BRTMissing,
        "• BRT Validator Missing" & UNICHAR(10),
        "• BRT Not Validated" & UNICHAR(10)
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
