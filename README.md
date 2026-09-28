GL2 Supplier Email Available? =
VAR Email =
    TRIM(
        'GL2 - Supplier Integration Register'[Supplier Email Contact] & ""
    )
RETURN
IF(
    Email = "" || Email = "--",
    "No",
    "Yes"
)
