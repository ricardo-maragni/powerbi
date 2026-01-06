# WeekDayTable
Código para modelo de tabela que converte os números da semana (0,1,2,3,4,5,6) em um formato amigável de texto.

```M
let

    Source = Table.FromColumns({{0..6},{"Domingo", "Segunda-feira", "Terça-feira", "Quarta-feira", "Quinta-feira", "Sexta-feira", "Sábado"}}),
    #"Renamed Columns" = Table.RenameColumns(Source,{{"Column1", "Number"}, {"Column2", "Day of Week"}}),
    #"Tipo Alterado" = Table.TransformColumnTypes(#"Renamed Columns",{{"Number", type number}, {"Day of Week", type text}})
    
in

    #"Tipo Alterado"
```
