GL1 Check Medium Total =
CALCULATE(
    [GL1 Webinar Total by Persona],
    TREATAS(
        {"Medium"},
        'Supplier Integration Register'[Comms Priority]
    )
)


GL1 Check High Total =
CALCULATE(
    [GL1 Webinar Total by Persona],
    TREATAS(
        {"High"},
        'Supplier Integration Register'[Comms Priority]
    )
)
