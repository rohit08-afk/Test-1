try
    let
        RawText = Text.From([#"SAP System / Supplier Number"]),

        NormalizedText =
            Text.Trim(
                Text.Replace(
                    Text.Replace(
                        Text.Replace(RawText, "#(cr)", " "),
                        "#(lf)", " "
                    ),
                    "#(tab)", " "
                )
            ),

        Parts =
            List.Select(
                Text.Split(NormalizedText, " "),
                each Text.Trim(_) <> ""
            ),

        PairCount =
            Number.RoundDown(List.Count(Parts) / 2),

        Vendors =
            List.Transform(
                List.Numbers(0, PairCount),
                each Parts{_ * 2} & " " & Parts{_ * 2 + 1}
            )
    in
        Vendors
otherwise
    {}


    try
    Text.Upper(
        Text.Remove(
            Text.Trim([Vendor List]),
            {" "}
        )
    )
otherwise
    null
