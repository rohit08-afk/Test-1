
-- TOPIC 1: PAYABLES & INVOICING

T1 Completion % =
CALCULATE(
    [RO Attendance Rate],
    'GL1 RO Attendance Mapping'[Topic] = "Payables & Invoicing"
)

T1 Attended =
CALCULATE(
    [RO Attended],
    'GL1 RO Attendance Mapping'[Topic] = "Payables & Invoicing"
)

T1 Invited =
CALCULATE(
    [RO Invited],
    'GL1 RO Attendance Mapping'[Topic] = "Payables & Invoicing"
)

T1 Not Attended =
CALCULATE(
    [RO Not Attended],
    'GL1 RO Attendance Mapping'[Topic] = "Payables & Invoicing"
)

T1 Attendance Label =
"Attended: " & FORMAT([T1 Attended], "0")
& " / " & FORMAT([T1 Invited], "0")

T1 Remaining Label =
"Remaining: " & FORMAT([T1 Not Attended], "0")


-- TOPIC 2: PO's & PO CONVERSION

T2 Completion % =
CALCULATE(
    [RO Attendance Rate],
    'GL1 RO Attendance Mapping'[Topic] = "PO's & PO Conversion"
)

T2 Attended =
CALCULATE(
    [RO Attended],
    'GL1 RO Attendance Mapping'[Topic] = "PO's & PO Conversion"
)

T2 Invited =
CALCULATE(
    [RO Invited],
    'GL1 RO Attendance Mapping'[Topic] = "PO's & PO Conversion"
)

T2 Not Attended =
CALCULATE(
    [RO Not Attended],
    'GL1 RO Attendance Mapping'[Topic] = "PO's & PO Conversion"
)

T2 Attendance Label =
"Attended: " & FORMAT([T2 Attended], "0")
& " / " & FORMAT([T2 Invited], "0")

T2 Remaining Label =
"Remaining: " & FORMAT([T2 Not Attended], "0")


-- TOPIC 3: FIELDGLASS/SERVICES SES

T3 Completion % =
CALCULATE(
    [RO Attendance Rate],
    'GL1 RO Attendance Mapping'[Topic] = "Fieldglass/Services SES"
)

T3 Attended =
CALCULATE(
    [RO Attended],
    'GL1 RO Attendance Mapping'[Topic] = "Fieldglass/Services SES"
)

T3 Invited =
CALCULATE(
    [RO Invited],
    'GL1 RO Attendance Mapping'[Topic] = "Fieldglass/Services SES"
)

T3 Not Attended =
CALCULATE(
    [RO Not Attended],
    'GL1 RO Attendance Mapping'[Topic] = "Fieldglass/Services SES"
)

T3 Attendance Label =
"Attended: " & FORMAT([T3 Attended], "0")
& " / " & FORMAT([T3 Invited], "0")

T3 Remaining Label =
"Remaining: " & FORMAT([T3 Not Attended], "0")


-- TOPIC 4: PROFESSIONAL SERVICES/SOW/IDENTITY CREATION

T4 Completion % =
CALCULATE(
    [RO Attendance Rate],
    'GL1 RO Attendance Mapping'[Topic] = "Professional Services/SOW/Identity Creation"
)

T4 Attended =
CALCULATE(
    [RO Attended],
    'GL1 RO Attendance Mapping'[Topic] = "Professional Services/SOW/Identity Creation"
)

T4 Invited =
CALCULATE(
    [RO Invited],
    'GL1 RO Attendance Mapping'[Topic] = "Professional Services/SOW/Identity Creation"
)

T4 Not Attended =
CALCULATE(
    [RO Not Attended],
    'GL1 RO Attendance Mapping'[Topic] = "Professional Services/SOW/Identity Creation"
)

T4 Attendance Label =
"Attended: " & FORMAT([T4 Attended], "0")
& " / " & FORMAT([T4 Invited], "0")

T4 Remaining Label =
"Remaining: " & FORMAT([T4 Not Attended], "0")
