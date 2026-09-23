Selected City =
COALESCE(
    SELECTEDVALUE('Employee Roster'[City]),
    "--"
)

Selected Geographic Region =
COALESCE(
    SELECTEDVALUE('Employee Roster'[Geographic Region]),
    "--"
)

Selected Preferred Name =
COALESCE(
    SELECTEDVALUE('Employee Roster'[Preferred Name]),
    "--"
)

Selected GPN =
COALESCE(
    SELECTEDVALUE('Employee Roster'[GPN]),
    "--"
)

Selected GUI =
COALESCE(
    SELECTEDVALUE('Employee Roster'[GUI]),
    "--"
)

Selected Current Project =
COALESCE(
    SELECTEDVALUE('Employee Roster'[Current Project]),
    "--"
)

Selected Core Skills =
COALESCE(
    SELECTEDVALUE('Employee Roster'[Core Skills]),
    "--"
)
