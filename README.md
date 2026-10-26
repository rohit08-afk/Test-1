GL1 Webinar Total by Persona =
VAR CurrentPersona =
    SELECTEDVALUE('GL1 Webinar Measures'[Persona])

VAR RegisterPersona =
    SWITCH(
        CurrentPersona,
        "Beeline - Identity Creation , Services",
            "Services, Beeline - Identity Creation",
        CurrentPersona
    )

RETURN
    CALCULATE(
        [GL1 Total Suppliers],
        REMOVEFILTERS('Supplier Integration Register'[Persona]),
        'Supplier Integration Register'[Persona] = RegisterPersona
    )


    GL1 Summary Attendance Rate =
DIVIDE(
    [GL1 Webinar Attended Corrected],
    [GL1 Webinar Total by Persona],
    0
)



GL1 Summary Last Week Attended =
VAR LatestDate =
    CALCULATE(
        MAX('GL1 Webinar Measures'[Webinar Date]),
        REMOVEFILTERS('GL1 Webinar Measures'[Webinar Date])
    )

VAR PreviousDate =
    CALCULATE(
        MAX('GL1 Webinar Measures'[Webinar Date]),
        FILTER(
            ALL('GL1 Webinar Measures'[Webinar Date]),
            'GL1 Webinar Measures'[Webinar Date] < LatestDate
        )
    )

RETURN
    CALCULATE(
        [GL1 Webinar Attended Corrected],
        FILTER(
            ALL('GL1 Webinar Measures'[Webinar Date]),
            'GL1 Webinar Measures'[Webinar Date] <= PreviousDate
        )
    )


    GL1 Summary Last Week Rate =
DIVIDE(
    [GL1 Summary Last Week Attended],
    [GL1 Webinar Total by Persona],
    0
)


GL1 Summary Weekly Change PP =
(
    [GL1 Summary Attendance Rate]
    - [GL1 Summary Last Week Rate]
) * 100

