GL1 Webinar Session Invited =
VAR SupplierDomain =
    SELECTEDVALUE('GL1 Webinar Supplier lookup'[Domain Name])
RETURN
    CALCULATE(
        CONCATENATEX(
            VALUES('GL1 Raw - Supplier Webinar'[Session Invited]),
            'GL1 Raw - Supplier Webinar'[Session Invited],
            ", "
        ),
        TREATAS(
            {SupplierDomain},
            'GL1 Raw - Supplier Webinar'[Domain Name]
        )
    )


    GL1 Webinar Attendee Count =
VAR SupplierDomain =
    SELECTEDVALUE('GL1 Webinar Supplier lookup'[Domain Name])
RETURN
    CALCULATE(
        DISTINCTCOUNT('GL1 - Supplier Webinar'[Attendee Email]),
        TREATAS(
            {SupplierDomain},
            'GL1 - Supplier Webinar'[Domain Name]
        )
    ) + 0



    
