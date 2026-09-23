Employee Initials =
VAR FirstName =
    SELECTEDVALUE('Employee Roster'[First Name])
VAR LastName =
    SELECTEDVALUE('Employee Roster'[Last Name])
RETURN
IF(
    ISBLANK(FirstName),
    "",
    UPPER(
        LEFT(FirstName,1) &
        LEFT(COALESCE(LastName,""),1)
    )
)

Selected Tenure Display =
VAR StartDate =
    SELECTEDVALUE('Employee Roster'[Current Employment Date])
VAR TotalMonths =
    DATEDIFF(StartDate, TODAY(), MONTH)
VAR Years =
    QUOTIENT(TotalMonths, 12)
VAR Months =
    MOD(TotalMonths, 12)
RETURN
IF(
    ISBLANK(StartDate),
    "--",
    Years & " " &
        IF(Years = 1, "year", "years")
        & " " &
    Months & " " &
        IF(Months = 1, "month", "months")
)

