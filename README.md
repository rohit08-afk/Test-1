RO Total Invited =
COUNTROWS('RO Attendance Summary')


RO Attended Session 1 =
CALCULATE(
    COUNTROWS('RO Attendance Summary'),
    'RO Attendance Summary'[1st Session_Aug 7] = "Joined"
)

RO Attended Session 2 =
CALCULATE(
    COUNTROWS('RO Attendance Summary'),
    'RO Attendance Summary'[2nd Session_Aug 11] = "Joined"
)

RO Attended Session 3 =
CALCULATE(
    COUNTROWS('RO Attendance Summary'),
    'RO Attendance Summary'[3rd Session_Sep 3] = "Joined"
)

RO Did Not Attend Any Session =
CALCULATE(
    COUNTROWS('RO Attendance Summary'),
    'RO Attendance Summary'[1st Session_Aug 7] <> "Joined",
    'RO Attendance Summary'[2nd Session_Aug 11] <> "Joined",
    'RO Attendance Summary'[3rd Session_Sep 3] <> "Joined"
)

RO Attended At Least One Session =
[RO Total Invited] - [RO Did Not Attend Any Session]


RO Onboarding Coverage % =
DIVIDE(
    [RO Attended At Least One Session],
    [RO Total Invited],
    0
)




Orientation Total Invitees =
CALCULATE(
    DISTINCTCOUNT('RO Orientation Summary'[Email - Invited]),
    NOT ISBLANK('RO Orientation Summary'[Email - Invited])
)


Orientation Attended Session =
CALCULATE(
    DISTINCTCOUNT('RO Orientation Summary'[Email - Invited]),
    'RO Orientation Summary'[Attended - Supplier Impacts for RO/AO 09-15] = "Yes"
)


Orientation Missed Session =
CALCULATE(
    DISTINCTCOUNT('RO Orientation Summary'[Email - Invited]),
    'RO Orientation Summary'[Attended - Supplier Impacts for RO/AO 09-15] = "No"
)

Orientation Coverage % =
DIVIDE(
    [Orientation Attended Session],
    [Orientation Total Invitees],
    0
)
