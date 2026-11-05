Session RO Attended =
VAR InvitedROs =
    CALCULATETABLE(
        VALUES('GL1 RO Attendance Mapping'[RO]),
        'GL1 RO Attendance Mapping'[Invitation Status] = "Invited"
    )
VAR AttendedROs =
    CALCULATETABLE(
        VALUES('GL1 RO Attendance Mapping'[RO]),
        'GL1 RO Attendance Mapping'[Attendance] = "Attended"
    )
RETURN
    COUNTROWS(INTERSECT(InvitedROs, AttendedROs))


  Session Attendance Change =
VAR CurrentDate =
    SELECTEDVALUE('GL1 RO Attendance Mapping'[Session Date])

VAR PreviousDate =
    CALCULATE(
        MAX('GL1 RO Attendance Mapping'[Session Date]),
        REMOVEFILTERS(
            'GL1 RO Attendance Mapping'[Session Date],
            'GL1 RO Attendance Mapping'[Session ID]
        ),
        'GL1 RO Attendance Mapping'[Session Date] < CurrentDate
    )

VAR PreviousAttendance =
    CALCULATE(
        [Session RO Attended],
        REMOVEFILTERS(
            'GL1 RO Attendance Mapping'[Session Date],
            'GL1 RO Attendance Mapping'[Session ID]
        ),
        'GL1 RO Attendance Mapping'[Session Date] = PreviousDate
    )

RETURN
    IF(
        ISINSCOPE('GL1 RO Attendance Mapping'[Session Date]),
        IF(
            ISBLANK(PreviousDate),
            0,
            COALESCE([Session RO Attended], 0)
                - COALESCE(PreviousAttendance, 0)
        ),
        BLANK()
    )  
