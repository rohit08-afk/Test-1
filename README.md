- Supplier Count Validation: Identified that some suppliers are mapped to multiple personas (e.g., Materials and Materials, Services), resulting in overlapping counts at the persona level. The dashboard correctly shows 58 unique suppliers for Chemical Products, while persona-level counts total 79. Attached screenshot for reference.

- Supplier Drillthrough Metrics =
DATATABLE(
    "Metric", STRING,
    "Sort Order", INTEGER,
    {
        {"Suppliers in scope", 1},
        {"Webinar Attended", 2},
        {"High Priority Not Attended", 3},
        {"Medium Priority Not Attended", 4},
        {"Remaining %", 5}
    }

)

Supplier Drillthrough Value =
SWITCH(
    SELECTEDVALUE('Supplier Drillthrough Metrics'[Metric]),
    "Suppliers in scope", [Suppliers in scope],
    "Webinar Attended", [Webinar Attended],
    "High Priority Not Attended", [High Priority Not Attended],
    "Medium Priority Not Attended", [Medium Priority Not Attended],
    "Remaining %", [Remaining (as a % of total)],
    BLANK()
)


Selected Supplier Metric =
SELECTEDVALUE(
    'Supplier Drillthrough Metrics'[Metric],
    "No metric selected"
)

