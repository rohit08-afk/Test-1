if [Vendor Key Split] = null or Text.Trim([Vendor Key Split]) = "" then
    if [#"SAP System / Supplier Number"] = null or Text.Trim([#"SAP System / Supplier Number"]) = "" then
        "Keep"
    else
        "Remove"
else
    "Keep"
