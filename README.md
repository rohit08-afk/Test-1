each try
    let
        Tokens =
            List.Select(
                Text.Split(Text.Trim([Vendor List]), " "),
                each _ <> ""
            ),

        Pairs =
            List.Split(Tokens, 2),

        FormattedKeys =
            List.Transform(
                Pairs,
                each
                    if List.Count(_) = 2 then
                        Text.Upper(_{0}) & "-" & _{1}
                    else
                        Text.Upper(_{0})
            )
    in
        Text.Combine(FormattedKeys, " ")
otherwise null
