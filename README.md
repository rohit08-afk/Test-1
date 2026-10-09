if [Is for Material ONLY?] = null or Text.Trim(Text.From([Is for Material ONLY?])) = "" then "Open"
else if Text.Upper(Text.Trim(Text.From([Is for Material ONLY?]))) = "YES" then "Validated - Yes"
else if Text.Upper(Text.Trim(Text.From([Is for Material ONLY?]))) = "NO" then "Validated - No"
else "Other"

Open Validation Items =
CALCULATE(
    COUNTROWS('Material Supplier Validation'),
    'Material Supplier Validation'[Validation Status] = "Open"
)
