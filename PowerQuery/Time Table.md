# Time Table


    Source = {0..1439},
    #"Converted to Table" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
    #"Changed Type" = Table.TransformColumnTypes(#"Converted to Table",{{"Column1", Int64.Type}}),
    #"Renamed Columns" = Table.RenameColumns(#"Changed Type",{{"Column1", "Minute Number"}}),
    #"Inserted Division" = Table.AddColumn(#"Renamed Columns", "Division", each [Minute Number] / 1440, type number),
    #"Changed Type1" = Table.TransformColumnTypes(#"Inserted Division",{{"Division", type time}}),
    #"Renamed Columns1" = Table.RenameColumns(#"Changed Type1",{{"Division", "Time to the Minute"}}),

    // Create 2 minute time slot
    #"Inserted Integer-Division2min" = Table.AddColumn(#"Renamed Columns1", "2min bucket", each Number.IntegerDivide([Minute Number], 2), Int64.Type),
    #"Added Custom2min" = Table.AddColumn(#"Inserted Integer-Division2min", "2min time slot", each [2min bucket] *2 / 1440),
    #"Changed Type2min" = Table.TransformColumnTypes(#"Added Custom2min",{{"2min time slot", type time}}),

    // Create 3 minute time slot
    #"Inserted Integer-Division3min" = Table.AddColumn(#"Changed Type2min", "Integer-Division", each Number.IntegerDivide([Minute Number], 3), Int64.Type),
    #"Renamed Columns3min" = Table.RenameColumns(#"Inserted Integer-Division3min",{{"Integer-Division", "3 min bucket"}}),
    #"Added Custom3min" = Table.AddColumn(#"Renamed Columns3min", "3min time slot", each [3 min bucket] * 3 / 1440),
    #"Changed Type3min" = Table.TransformColumnTypes(#"Added Custom3min",{{"3min time slot", type time}}),

    // Create 4 minute time slot
    #"Inserted Integer-Division4min" = Table.AddColumn(#"Changed Type3min", "Integer-Division", each Number.IntegerDivide([Minute Number], 4), Int64.Type),
    #"Renamed Columns4min" = Table.RenameColumns(#"Inserted Integer-Division4min",{{"Integer-Division", "4min bucket"}}),
    #"Added Custom4min" = Table.AddColumn(#"Renamed Columns4min", "4min time slot", each [4min bucket] * 4 / 14440),
    #"Changed Type4min" = Table.TransformColumnTypes(#"Added Custom4min",{{"4min time slot", type time}}),

    // Create 5 minute time slot
    #"Inserted Integer-Division5min" = Table.AddColumn(#"Changed Type4min", "Integer-Division", each Number.IntegerDivide([Minute Number], 5), Int64.Type),
    #"Renamed Columns5min" = Table.RenameColumns(#"Inserted Integer-Division5min",{{"Integer-Division", "5min bucket"}}),
    #"Added Custom5min" = Table.AddColumn(#"Renamed Columns5min", "5min time slot", each [5min bucket] * 5 / 1440),
    #"Changed Type5min" = Table.TransformColumnTypes(#"Added Custom5min",{{"5min time slot", type time}}),

    // Create 6 minute time slot
    #"Inserted Integer-Division6min" = Table.AddColumn(#"Changed Type5min", "Integer-Division", each Number.IntegerDivide([Minute Number], 6), Int64.Type),
    #"Renamed Columns6min" = Table.RenameColumns(#"Inserted Integer-Division6min",{{"Integer-Division", "6min bucket"}}),
    #"Added Custom6min" = Table.AddColumn(#"Renamed Columns6min", "6min time slot", each [6min bucket] * 6 / 1440),
    #"Changed Type6min" = Table.TransformColumnTypes(#"Added Custom6min",{{"6min time slot", type time}}),

    // Create 10 minute time slot
    #"Inserted Integer-Division10min" = Table.AddColumn(#"Changed Type6min", "Integer-Division", each Number.IntegerDivide([Minute Number], 10), Int64.Type),
    #"Renamed Columns10min" = Table.RenameColumns(#"Inserted Integer-Division10min",{{"Integer-Division", "10min bucket"}}),
    #"Added Custom10min" = Table.AddColumn(#"Renamed Columns10min", "10min time slot", each [10min bucket] * 10 / 1440),
    #"Changed Type10min" = Table.TransformColumnTypes(#"Added Custom10min",{{"10min time slot", type time}}),

    // Create 12 minute time slot
    #"Inserted Integer-Division12min" = Table.AddColumn(#"Changed Type10min", "Integer-Division", each Number.IntegerDivide([Minute Number], 12), Int64.Type),
    #"Renamed Columns12min" = Table.RenameColumns(#"Inserted Integer-Division12min",{{"Integer-Division", "12min bucket"}}),
    #"Added Custom12min" = Table.AddColumn(#"Renamed Columns12min", "12min time slot", each [12min bucket] * 12 / 1440),
    #"Changed Type12min" = Table.TransformColumnTypes(#"Added Custom12min",{{"12min time slot", type time}}),

    // Create 15 minute time slot
    #"Inserted Integer-Division15min" = Table.AddColumn(#"Changed Type12min", "Integer-Division", each Number.IntegerDivide([Minute Number], 15), Int64.Type),
    #"Renamed Columns15min" = Table.RenameColumns(#"Inserted Integer-Division15min",{{"Integer-Division", "15min bucket"}}),
    #"Added Custom15min" = Table.AddColumn(#"Renamed Columns15min", "15min time slot", each [15min bucket] * 15 / 1440),
    #"Changed Type15min" = Table.TransformColumnTypes(#"Added Custom15min",{{"15min time slot", type time}}),

    // Create 20 minute time slot
    #"Inserted Integer-Division20min" = Table.AddColumn(#"Changed Type15min", "Integer-Division", each Number.IntegerDivide([Minute Number], 20), Int64.Type),
    #"Renamed Columns20min" = Table.RenameColumns(#"Inserted Integer-Division20min",{{"Integer-Division", "20min bucket"}}),
    #"Added Custom20min" = Table.AddColumn(#"Renamed Columns20min", "20min time slot", each [15min bucket] * 20 / 1440),
    #"Changed Type20min" = Table.TransformColumnTypes(#"Added Custom20min",{{"20min time slot", type time}}),

    // Create 30 minute time slot
    #"Inserted Integer-Division30min" = Table.AddColumn(#"Changed Type20min", "Integer-Division", each Number.IntegerDivide([Minute Number], 30), Int64.Type),
    #"Renamed Columns30min" = Table.RenameColumns(#"Inserted Integer-Division30min",{{"Integer-Division", "30min bucket"}}),
    #"Added Custom30min" = Table.AddColumn(#"Renamed Columns30min", "30min time slot", each [30min bucket] * 30 / 1440),
    #"Changed Type30min" = Table.TransformColumnTypes(#"Added Custom30min",{{"30min time slot", type time}}),

    // Create 1h / 60 min time slot
    #"Inserted Integer-Division60min" = Table.AddColumn(#"Changed Type30min", "Integer-Division", each Number.IntegerDivide([Minute Number], 60), Int64.Type),
    #"Renamed Columns60min" = Table.RenameColumns(#"Inserted Integer-Division60min",{{"Integer-Division", "1h bucket"}}),
    #"Added Custom60min" = Table.AddColumn(#"Renamed Columns60min", "1h time slot", each [1h bucket] * 60 / 1440),
    #"Changed Type60min" = Table.TransformColumnTypes(#"Added Custom60min",{{"1h time slot", type time}}),

    // Create 2h / 120 min time slot
    #"Inserted Integer-Division120min" = Table.AddColumn(#"Changed Type60min", "Integer-Division", each Number.IntegerDivide([Minute Number], 120), Int64.Type),
    #"Renamed Columns120min" = Table.RenameColumns(#"Inserted Integer-Division120min",{{"Integer-Division", "2h bucket"}}),
    #"Added Custom120min" = Table.AddColumn(#"Renamed Columns120min", "2h time slot", each [2h bucket] * 120 / 1440),
    #"Changed Type120min" = Table.TransformColumnTypes(#"Added Custom120min",{{"2h time slot", type time}}),

    // Create 4h / 240 min time slot
    #"Inserted Integer-Division240min" = Table.AddColumn(#"Changed Type120min", "Integer-Division", each Number.IntegerDivide([Minute Number], 240), Int64.Type),
    #"Renamed Columns240min" = Table.RenameColumns(#"Inserted Integer-Division240min",{{"Integer-Division", "4h bucket"}}),
    #"Added Custom240min" = Table.AddColumn(#"Renamed Columns240min", "4h time slot", each [4h bucket] * 240 / 1440),
    #"Changed Type240min" = Table.TransformColumnTypes(#"Added Custom240min",{{"4h time slot", type time}}),

    // Create 6h / 360 min time slot
    #"Inserted Integer-Division360min" = Table.AddColumn(#"Changed Type240min", "Integer-Division", each Number.IntegerDivide([Minute Number], 360), Int64.Type),
    #"Renamed Columns360min" = Table.RenameColumns(#"Inserted Integer-Division360min",{{"Integer-Division", "6h bucket"}}),
    #"Added Custom360min" = Table.AddColumn(#"Renamed Columns360min", "6h time slot", each [6h bucket] * 360 / 1440),
    #"Changed Type360min" = Table.TransformColumnTypes(#"Added Custom360min",{{"6h time slot", type time}}),

     // Create 12h / 720 min time slot
    #"Inserted Integer-Division720min" = Table.AddColumn(#"Changed Type360min", "Integer-Division", each Number.IntegerDivide([Minute Number], 720), Int64.Type),
    #"Renamed Columns720min" = Table.RenameColumns(#"Inserted Integer-Division720min",{{"Integer-Division", "12h bucket"}}),
    #"Added Custom720min" = Table.AddColumn(#"Renamed Columns720min", "12h time slot", each [12h bucket] * 720 / 1440),
    #"Changed Type720min" = Table.TransformColumnTypes(#"Added Custom720min",{{"12h time slot", type time}})
in
    #"Changed Type720min"

