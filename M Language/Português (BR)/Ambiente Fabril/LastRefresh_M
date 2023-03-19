let
    Fonte = DateTime.LocalNow(),
    #"Convertido para Tabela" = #table(1, {{Fonte}}),
    #"Tipo Alterado" = Table.TransformColumnTypes(#"Convertido para Tabela",{{"Column1", type datetime}}),
    #"Coluna Duplicada" = Table.DuplicateColumn(#"Tipo Alterado", "Column1", "Column1 - Copiar"),
    #"Coluna Duplicada1" = Table.DuplicateColumn(#"Coluna Duplicada", "Column1 - Copiar", "Column1 - Copiar - Copiar"),
    #"Tipo Alterado1" = Table.TransformColumnTypes(#"Coluna Duplicada1",{{"Column1", type datetime}}),
    #"Colunas Renomeadas" = Table.RenameColumns(#"Tipo Alterado1",{{"Column1", "DateTime.LocalNow"}, {"Column1 - Copiar", "LastRefresh.Date"}, {"Column1 - Copiar - Copiar", "LastRefresh.Hour"}}),
    #"Tipo Alterado2" = Table.TransformColumnTypes(#"Colunas Renomeadas",{{"LastRefresh.Date", type date}, {"LastRefresh.Hour", type time}}),
    #"Personalização Adicionada1" = Table.AddColumn(#"Tipo Alterado2", "LastRefresh.Week", each Date.WeekOfYear([DateTime.LocalNow])),

//Coluna de semana adicionada

    #"Personalização Adicionada" = Table.AddColumn(#"Personalização Adicionada1", "LastRefresh.Full", each Text.From([DateTime.LocalNow]) & " (CW" & 
Text.From([LastRefresh.Week]) & ")"),
    #"Tipo Alterado3" = Table.TransformColumnTypes(#"Personalização Adicionada",{{"LastRefresh.Full", type text}})
    
in
    #"Tipo Alterado3"
