= Table.AddColumn(Source, "Invited Status", each
    if [Invitation Status] <> null
       and Text.Lower(Text.Trim(Text.From([Invitation Status]))) = "invited"
    then 1
    else 0,
    Int64.Type)


    = Table.AddColumn(#"Added Custom", "Attendance Status", each
    if [Attendance] <> null
       and Text.Lower(Text.Trim(Text.From([Attendance]))) = "attended"
    then 1
    else 0,
    Int64.Type)
