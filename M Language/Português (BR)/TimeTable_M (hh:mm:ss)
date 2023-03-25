let

    Source = List.Times(#time(0,0,0),24*60*60,#duration(0,0,0,1)),
    #"Converted to Table" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
    #"Renamed Columns" = Table.RenameColumns(#"Converted to Table",{{"Column1", "Tempo"}}),
    #"Changed Type" = Table.TransformColumnTypes(#"Renamed Columns",{{"Tempo", type time}}),

    //Coluna de horas

    #"Inserted Hour" = Table.AddColumn(#"Changed Type", "Horas", each Time.Hour([Tempo]), Int64.Type),

    //Coluna de minutos

    #"Inserted Minute" = Table.AddColumn(#"Inserted Hour", "Minutos", each Time.Minute([Tempo]), Int64.Type),
    #"Inserted Second" = Table.AddColumn(#"Inserted Minute", "Segundos", each Time.Second([Tempo]), type number),

    //Coluna de "AM/PM"

    #"Added Conditional Column" = Table.AddColumn(#"Inserted Second", "AM/PM", each if [Horas] < 12 then "a.m." else "p.m."),

    //Coluna de turno

    #"Added Conditional Column1" = Table.AddColumn(#"Added Conditional Column", "Turno", each if [Horas] >= 0 and [Horas] < 6 then "3" else if [Horas] >= 6 and [Horas] < 15 then "1" else "2")

in

    #"Added Conditional Column1"
