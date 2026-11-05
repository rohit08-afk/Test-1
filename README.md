RO Session Drillthrough Value =
SWITCH(
    SELECTEDVALUE('RO Session Metrics'[Metric]),
    "Invited", [Session RO Invited],
    "Attended", [Session RO Attended],
    "Not Attended", [Session RO Not Attended],
    "Change vs Previous", 999,
    BLANK()
)
