# Date functions
Principais funções de data utilizadas dentro do Power Query. <br>

## Dia da semana
```M
Date.DayOfWeek()
```

## Dia de hoje
```M
Date.From(DateTime.LocalNow())
```

## Dia de hoje (data/hora)
```M
DateTime.LocalNow()
```

## Dia de ontem
```M
Date.From(DateTime.LocalNow()-#duration(1,0,0,0))
```

## Dia de ontem (data/hora)
```M
DateTime.LocalNow()-#duration(1,0,0,0)
```
