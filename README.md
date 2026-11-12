SWITCH(
    SELECTEDVALUE('Supplier Drillthrough Metrics'[Metric]),
    "Remaining %", "0%",
    "#,0"
)
