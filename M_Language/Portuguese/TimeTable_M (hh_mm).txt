let

    Source = List.Times(#time(0,0,0),24*60,#duration(0,0,1,0)),
    #"Converted to Table" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
    #"Renamed Columns" = Table.RenameColumns(#"Converted to Table",{{"Column1", "Time"}}),
    #"Changed Type" = Table.TransformColumnTypes(#"Renamed Columns",{{"Time", type time}}),

    //Remover segundos

    #"Removed Seconds" = Table.TransformColumns(#"Changed Type", {{"Time", each Time.FromText(Time.ToText(_, "hh:mm"))}}),

    //Coluna de horas

    #"Inserted Hour" = Table.AddColumn(#"Removed Seconds", "Hour", each Time.Hour([Time]), Int64.Type),

    //Coluna de minutos

    #"Inserted Minute" = Table.AddColumn(#"Inserted Hour", "Minute", each Time.Minute([Time]), Int64.Type),

    //Coluna de "AM/PM"

    #"Added Conditional Column" = Table.AddColumn(#"Inserted Minute", "AM/PM", each if [Hour] < 12 then "a.m." else "p.m."),
    #"Changed Type1" = Table.TransformColumnTypes(#"Added Conditional Column",{{"AM/PM", type text}}),

    //Coluna de turno

    #"Added Conditional Column1" = Table.AddColumn(#"Changed Type1", "Turno", each if [Hour] >= 0 and [Hour] < 6 then "3" else if [Hour] >= 6 and [Hour] < 15 then "1" else "2"),

    //Formatação da coluna time

    #"Tipo Alterado" = Table.TransformColumnTypes(#"Added Conditional Column1",{{"Time", type time}})

in

    #"Tipo Alterado"
