T1 Completion % =
CALCULATE(
    [RO Attendance Rate],
    'GL1 RO Attendance Mapping'[Topic] = "Payables & Invoicing"
)


T2 Completion % =
CALCULATE(
    [RO Attendance Rate],
    'GL1 RO Attendance Mapping'[Topic] = "PO's & PO Conversion"
)

T3 Completion % =
CALCULATE(
    [RO Attendance Rate],
    'GL1 RO Attendance Mapping'[Topic] = "Fieldglass/Services SES"
)


T4 Completion % =
CALCULATE(
    [RO Attendance Rate],
    'GL1 RO Attendance Mapping'[Topic] = "Professional Services/SOW/Identity Creation"
)



T1 Attended =
CALCULATE(
    [RO Attended],
    'GL1 RO Attendance Mapping'[Topic] = "Payables & Invoicing"
)


T1 Not Attended =
CALCULATE(
    [RO Not Attended],
    'GL1 RO Attendance Mapping'[Topic] = "Payables & Invoicing"
)


T1 Invited =
CALCULATE(
    [RO Invited],
    'GL1 RO Attendance Mapping'[Topic] = "Payables & Invoicing"
)


T1 Attendance Label =
"Attended: "
    & FORMAT([T1 Attended], "0")
    & " / "
    & FORMAT([T1 Invited], "0")


    T1 Remaining Label =
"Remaining: "
    & FORMAT([T1 Not Attended], "0")



    
