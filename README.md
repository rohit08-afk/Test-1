Total ROs =
DISTINCTCOUNT('GL1 RO Attendance Mapping'[RO])

RO Attended =
VAR SelectedROs =
    VALUES('GL1 RO Attendance Mapping'[RO])
RETURN
    CALCULATE(
        DISTINCTCOUNT('GL1 RO Session Attendance unique'[RO]),
        TREATAS(
            SelectedROs,
            'GL1 RO Session Attendance unique'[RO]
        ),
        'GL1 RO Session Attendance unique'[Attended] = 1
    )

   RO Not Attended =
[Total ROs] - [RO Attended]

RO Attendance Rate =
DIVIDE(
    [RO Attended],
    [Total ROs],
    0
)


RO Invited =
VAR SelectedROs =
    VALUES('GL1 RO Attendance Mapping'[RO])
RETURN
    CALCULATE(
        DISTINCTCOUNT('GL1 RO Session Attendance unique'[RO]),
        TREATAS(
            SelectedROs,
            'GL1 RO Session Attendance unique'[RO]
        ),
        'GL1 RO Session Attendance unique'[Invited] = 1
    )

    
