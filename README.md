= Table.AddColumn(
    #"Expanded GL1 RO Priority Source",
    "Priority Rank",
    each
        let
            Priority =
                if [Comms Priority] = null then ""
                else Text.Upper(Text.Trim(Text.From([Comms Priority])))
        in
            if Priority = "HIGH" then 3
            else if Priority = "MEDIUM" then 2
            else if Priority = "LOW" then 1
            else 0,
    Int64.Type
)
