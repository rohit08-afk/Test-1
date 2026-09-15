let
    t = [#"SAP System / Supplier Number"],
    s1 = Text.Replace(t, "AMP ", "|AMP "),
    s2 = Text.Replace(s1, "G3P ", "|G3P "),
    s3 = Text.Replace(s2, "EUP ", "|EUP "),
    s4 = Text.Replace(s3, "PNR ", "|PNR "),
    s5 = Text.Replace(s4, "S8P ", "|S8P "),
    s6 = Text.Replace(s5, "XTP ", "|XTP "),
    s7 = Text.Replace(s6, "GEP ", "|GEP "),
    s8 = Text.Replace(s7, "G9P ", "|G9P ")
in
    s8
