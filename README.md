Suppliers in scope =
[Target High Total] + [Target Medium Total]


Webinar Not Attended =
[Suppliers in scope] - [Webinar Attended]


High Priority Not Attended =
[Target High Total] - [Target High Attended]



Medium Priority Not Attended =
[Target Medium Total] - [Target Medium Attended]


GL1 Webinar Attendance Rate =
DIVIDE(
    [Webinar Attended],
    [Suppliers in scope],
    0
)


Weekly Change PP =
(
    [GL1 Webinar Attendance Rate]
    - [GL1 Summary Last Week Rate]
) * 100


