let

    Source = Table.FromColumns({{0..6},{"Domingo", "Segunda-feira", "Terça-feira", "Quarta-feira", "Quinta-feira", "Sexta-feira", "Sábado"}}),
    #"Renamed Columns" = Table.RenameColumns(Source,{{"Column1", "Number"}, {"Column2", "Day of Week"}}),
    #"Tipo Alterado" = Table.TransformColumnTypes(#"Renamed Columns",{{"Number", type number}, {"Day of Week", type text}})
    
in

    #"Tipo Alterado"
