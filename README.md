GL2 Supplier Email Available? =
IF(
    ISBLANK('GL2 - Supplier Integration Register'[Supplier Email Contact])
        || TRIM('GL2 - Supplier Integration Register'[Supplier Email Contact]) = ""
        || TRIM('GL2 - Supplier Integration Register'[Supplier Email Contact]) = "--",
    "No",
    "Yes"
)
