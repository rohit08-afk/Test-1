let
    Source = #"GL1 RO Attendance_Working",

    #"Removed Duplicates" =
        Table.Distinct(
            Source,
            {"RO", "Category Family", "Persona"}
        ),

    #"Lowercased Text" =
        Table.TransformColumns(
            #"Removed Duplicates",
            {{"RO", Text.Lower, type text}}
        ),

    #"Merged RO Priority" =
        Table.NestedJoin(
            #"Lowercased Text",
            {"RO", "Category Family", "Persona"},
            #"GL1 RO Priority Mapping",
            {"RO", "Category Family", "Persona"},
            "Priority Lookup",
            JoinKind.LeftOuter
        ),

    #"Expanded RO Priority" =
        Table.ExpandTableColumn(
            #"Merged RO Priority",
            "Priority Lookup",
            {"RO Comms Priority"},
            {"RO Comms Priority"}
        )

in
    #"Expanded RO Priority"
