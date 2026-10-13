let
    emails = if [Attendance Supplier] = "Attended"
        and [Email Address_Webinar] <> null
        and [#"Duration (minutes)"] <> null
        then Text.Split([Email Address_Webinar], ";")
        else {},
    durations = if [Attendance Supplier] = "Attended"
        and [Email Address_Webinar] <> null
        and [#"Duration (minutes)"] <> null
        then Text.Split([#"Duration (minutes)"], ";")
        else {}
in
    List.Zip({emails, durations})

    
