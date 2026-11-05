Supplier Session Metrics =
DATATABLE(
    "Metric", STRING,
    "Sort Order", INTEGER,
    {
        {"Suppliers in Scope", 1},
        {"Invited", 2},
        {"Attended", 3},
        {"Not Attended", 4},
        {"Attendance Rate", 5},
        {"High Not Attended", 6},
        {"Medium Not Attended", 7},
        {"Weekly Change", 8}
    }
)


Supplier Session Drillthrough Value =
SWITCH(
    SELECTEDVALUE('Supplier Session Metrics'[Metric]),
    "Suppliers in Scope", [Suppliers in-scope],
    "Invited", [Supplier Session Invited],
    "Attended", [Supplier Session Attended],
    "Not Attended", [Supplier Session Not Attended],
    "Attendance Rate", [Webinar Attendance Rate],
    "High Not Attended", [Supplier Session High Not Attended],
    "Medium Not Attended", [Supplier Session Medium Not Attended],
    "Weekly Change", [Supplier Session Weekly Change Count],
    BLANK()
)



