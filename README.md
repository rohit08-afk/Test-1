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
    [GL2 Lookup - EP Type]

VAR Procurement =
    [GL2 Lookup - Proc Non-Proc]

VAR RO =
    [GL2 Lookup - Relationship Owner]

VAR Persona =
    [GL2 Lookup - Persona]

VAR Category =
    [GL2 Lookup - Category]

VAR CategoryManager =
    [GL2 Lookup - Category Manager]

VAR BRT =
    [GL2 Lookup - BRT Validator]


-- =====================================================
-- MISSING CHECKS
-- =====================================================

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

VAR CategoryManagerMissing =
    ISBLANK(CategoryManager)
        || TRIM(CategoryManager) = ""
        || TRIM(CategoryManager) = "-"
        || TRIM(CategoryManager) = "--"

VAR BRTMissing =
    ISBLANK(BRT)
        || TRIM(BRT) = ""
        || TRIM(BRT) = "-"
        || TRIM(BRT) = "--"


-- =====================================================
-- GAP OUTPUT
-- =====================================================

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
        "• Category Missing" & UNICHAR(10),
        "• Category Not Verified" & UNICHAR(10)
    )

VAR GapCategoryManager =
    IF(
        CategoryManagerMissing,
        "• Category Manager Missing" & UNICHAR(10),
        ""
    )

VAR GapBRT =
    IF(
        BRTMissing,
        "• BRT Validator Missing" & UNICHAR(10),
        "• BRT Not Validated" & UNICHAR(10)
    )


VAR Result =
      GapSupplierName
    & GapSupplierNumber
    & GapCountry
    & GapAgreement
    & GapEPType
    & GapProcurement
    & GapRO
    & GapPersona
    & GapCategory
    & GapCategoryManager
    & GapBRT


RETURN
IF(
    Result = "",
    "✓ No gaps identified",
    Result
)
