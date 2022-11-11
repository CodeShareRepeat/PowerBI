# Create Date Table with calenderaut

```
Date =
var mycalander = CALENDARAUTO()
return
ADDCOLUMNS(mycalander, 
    "Year", YEAR([Date]), 
    "Month", MONTH([Date]), 
    "Day", DAY([date]))
```