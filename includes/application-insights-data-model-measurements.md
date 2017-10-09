Коллекция пользовательских измерений. Используйте этот tooreport коллекции с именем измерения, связанный с элементом телеметрии hello. Типичные случаи использования:
- Hello размер полезных данных телеметрии зависимости
- Hello число обрабатываемых запросов телеметрии элементов очереди
- время клиента заняло toocomplete hello шаг в этапе завершения работы мастера телеметрии события.

[Пользовательские измерения](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) можно запросить в аналитике приложений:

```
customEvents
| where customMeasurements != ""
| summarize avg(todouble(customMeasurements["Completion Time"]) * itemCount)
```

 > [!NOTE]
 > Пользовательские измерения связаны с hello телеметрии элемента, которому они принадлежат. Они являются toosampling тема с элементом hello телеметрии, содержащий эти измерения. tootrack измерения со значением, независимо от других типов данных телеметрии, используйте [метрики телеметрии](../articles/application-insights/app-insights-api-custom-events-metrics.md).

Максимальная длина ключа: 150
