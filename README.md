Onboarding Status =
IF(
    'RO Attendance Summary'[1st Session_Aug 7] = "Joined"
        || 'RO Attendance Summary'[2nd Session_Aug 11] = "Joined"
        || 'RO Attendance Summary'[3rd Session_Sep 3] = "Joined",
    "Attended",
    "Missed"
)


Orientation Status =
VAR OrientationAttendance =
    LOOKUPVALUE(
        'RO Orientation Summary'[Attended - Supplier Impacts for RO/AO 09-15],
        'RO Orientation Summary'[Email - Invited],
        'RO Attendance Summary'[Email]
    )
RETURN
SWITCH(
    TRUE(),
    OrientationAttendance = "Yes", "Attended",
    OrientationAttendance = "No", "Missed",
    "Not Invited / No Record"
)


Current Readiness =
IF(
    'RO Attendance Summary'[Onboarding Status] = "Attended"
        && 'RO Attendance Summary'[Orientation Status] = "Attended",
    "Completed",
    "Pending"
)
