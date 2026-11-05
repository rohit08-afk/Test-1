Selected RO Topic =
SELECTEDVALUE(
    'GL1 RO Attendance Mapping'[Topic],
    "All Topics"
)

Selected RO Session =
VAR SessionDate =
    SELECTEDVALUE('GL1 RO Attendance Mapping'[Session Date])
RETURN
    IF(
        NOT ISBLANK(SessionDate),
        FORMAT(SessionDate, "dd MMM yyyy"),
        "All Sessions"
    )
