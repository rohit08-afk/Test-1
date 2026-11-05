
-- 1. SESSION RO INVITED

Session RO Invited =
CALCULATE(
    DISTINCTCOUNT('GL1 RO Attendance_Working'[RO]),
    'GL1 RO Attendance_Working'[Invitation Status] = "Invited"
)


-- 2. SESSION RO ATTENDED

Session RO Attended =
CALCULATE(
    DISTINCTCOUNT('GL1 RO Attendance_Working'[RO]),
    'GL1 RO Attendance_Working'[Attendance] = "Attended"
)


-- 3. SESSION RO NOT ATTENDED

Session RO Not Attended =
VAR InvitedROs =
    CALCULATETABLE(
        VALUES('GL1 RO Attendance_Working'[RO]),
        'GL1 RO Attendance_Working'[Invitation Status] = "Invited"
    )
VAR AttendedROs =
    CALCULATETABLE(
        VALUES('GL1 RO Attendance_Working'[RO]),
        'GL1 RO Attendance_Working'[Attendance] = "Attended"
    )
RETURN
    COUNTROWS(
        EXCEPT(InvitedROs, AttendedROs)
    )


-- 4. CHANGE VS PREVIOUS SESSION

Session Attendance Change =
VAR CurrentDate =
    SELECTEDVALUE('GL1 RO Attendance_Working'[Session Date])

VAR PreviousDate =
    CALCULATE(
        MAX('GL1 RO Attendance_Working'[Session Date]),
        REMOVEFILTERS('GL1 RO Attendance_Working'[Session Date]),
        'GL1 RO Attendance_Working'[Session Date] < CurrentDate
    )

VAR PreviousAttendance =
    CALCULATE(
        [Session RO Attended],
        REMOVEFILTERS('GL1 RO Attendance_Working'[Session Date]),
        'GL1 RO Attendance_Working'[Session Date] = PreviousDate
    )

RETURN
    IF(
        ISBLANK(CurrentDate) || ISBLANK(PreviousDate),
        BLANK(),
        [Session RO Attended] - PreviousAttendance
    )


-- 5. FINAL MATRIX VALUE

RO Session Drillthrough Value =
SWITCH(
    SELECTEDVALUE('RO Session Metrics'[Metric]),
    "Total ROs", [Total ROs],
    "Invited", [Session RO Invited],
    "Attended", [Session RO Attended],
    "Not Attended", [Session RO Not Attended],
    "Change vs Previous", [Session Attendance Change],
    BLANK()
)
