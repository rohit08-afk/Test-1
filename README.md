Selected Primary Sector =
COALESCE(
    SELECTEDVALUE('Employee Roster'[Primary Sector Name]),
    "--"
)

Selected Secondary Sector =
COALESCE(
    SELECTEDVALUE('Employee Roster'[Secondary Sector Name]),
    "--"
)

Selected OCG Sector Team =
COALESCE(
    SELECTEDVALUE('Employee Roster'[Include in OCG Sector Team?]),
    "--"
)


Employee Selected =
IF(
    HASONEVALUE('Employee Roster'[Full Name]),
    1,
    0
)

