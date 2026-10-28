= Table.AddColumn(#"Changed Type", "Topic", each Text.Trim(Text.BeforeDelimiter([Session ID], "_")), type text)

= Table.AddColumn(#"Added Custom", "Session Date", each
    let
        DateText = Text.Trim(Text.AfterDelimiter([Session ID], "_")),
        ParsedDate = try Date.FromText(DateText & " 2026", [Culture="en-US"]) otherwise null
    in
        ParsedDate,
    type date)
