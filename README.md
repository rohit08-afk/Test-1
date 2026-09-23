Selected Employee Name =
SELECTEDVALUE(
    'Employee Roster'[Full Name],
    "--"
)

Selected Rank =
COALESCE(
    SELECTEDVALUE('Employee Roster'[Rank Desc]),
    "--"
)

Selected EY Grade =
COALESCE(
    SELECTEDVALUE('Employee Roster'[Experience Level / EY Grade]),
    "--"
)

Selected Email =
COALESCE(
    SELECTEDVALUE('Employee Roster'[Email Address]),
    "--"
)

Selected Hire Date =
VAR d =
    SELECTEDVALUE('Employee Roster'[Current Employment Date])
RETURN
    IF(
        ISBLANK(d),
        "--",
        FORMAT(d, "dd MMM yyyy")
    )

    Selected Tenure =
VAR t =
    SELECTEDVALUE('Employee Roster'[Tenure Years])
RETURN
    IF(
        ISBLANK(t),
        "--",
        FORMAT(t, "0.0") & " years"
    )


    Selected Counselor =
COALESCE(
    SELECTEDVALUE('Employee Roster'[Counselor Name]),
    "--"
)

Selected Counselor Connect Leader =
COALESCE(
    SELECTEDVALUE('Employee Roster'[Counselor Connect Leader Name]),
    "--"
)

Selected Counselee Count =
VAR x =
    SELECTEDVALUE('Employee Roster'[Counselee Count])
RETURN
    COALESCE(x, 0)
