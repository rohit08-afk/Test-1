RO Drillthrough Value =
SWITCH(
    SELECTEDVALUE('RO Drillthrough Metrics'[Metric]),
    "Total ROs", [Total ROs],
    "RO Invited", [RO Invited],
    "Attended", [RO Attended],
    "Not Attended", [RO Not Attended],
    "Remaining %", DIVIDE([RO Not Attended], [Total ROs], 0),
    BLANK()
)
