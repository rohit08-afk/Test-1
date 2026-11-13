GL2 Total Suppliers - Comms =
DISTINCTCOUNT(
    'GL2 - Supplier Integration Registerp'[SAP Vendor Key]
)

GL2 Total Suppliers - Overall Comms =
VAR SelectedProgress =
    VALUES('GL2 Comms Progress - All'[Comms Progress])

VAR SelectedOutcome =
    VALUES('GL2 Communication Outcome - All'[Communication Outcome])

VAR SelectedEmail =
    VALUES('GL2 Email Availability - All'[Email Availability])

RETURN
CALCULATE(
    [GL2 Total Suppliers - Comms],

    REMOVEFILTERS(
        'GL2 - Supplier Integration Registerp'[Comms Progress]
    ),

    REMOVEFILTERS(
        'GL2 - Supplier Integration Registerp'[EP Type]
    ),

    TREATAS(
        SelectedProgress,
        'GL2 - Supplier Integration Registerp'[Comms Progress]
    ),

    TREATAS(
        SelectedOutcome,
        'GL2 - Supplier Integration Registerp'[Comms Outcome]
    ),

    TREATAS(
        SelectedEmail,
        'GL2 - Supplier Integration Registerp'[GL2 Supplier Email Available?]
    )
)
