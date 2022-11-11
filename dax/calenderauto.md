# Create Date Table with calenderauto

## Create a simple table dimension

```
Date =
var mycalander = CALENDARAUTO()
return
ADDCOLUMNS(mycalander, 
    "Year", YEAR([Date]), 
    "Month", MONTH([Date]), 
    "Day", DAY([date])
    "WeekDay", Day
    )
```

## Full Table with fiscal year

```
Date = ADDCOLUMNS(

// Fiscal year starts in month 3 (March)
CALENDARAUTO(3),
"Calendar Year", YEAR([Date]),
"Calendar Quarter", "Qtr " & QUARTER([Date]) ,
"Calendar Month", MONTH([Date]),
"Calendar Month Name", FORMAT([Date], "mmmm"),
"Calendar Day", DAY([Date]),
"Calendar Weekday", WEEKDAY([Date],2),
"Calendar weekday name", FORMAT([Date], "dddd"),
"Financial Year", IF(
[Date] >= DATE(Year([Date]), 4, 1),
Year([Date]) & "/" & RIGHT(Year([Date]) +1,2),
Year([Date])-1 &"/" & RIGHT(Year([Date]),2)
),
"Financial Quarter", SWITCH(
TRUE(),
MONTH([Date]) IN {4,5,6},"Qtr 1",
MONTH([Date]) IN {7,8,9},"Qtr 2",
MONTH([Date]) IN {10,11,12},"Qtr 3",
"Qtr 4"
),

"Financial Month" , IF(
MONTH([Date]) >= 4,
MONTH([Date]) - 3,
MONTH([Date]) + 9

),
"Financial Month Name", FORMAT([Date], "mmmm")
)
```