<span data-ttu-id="ce7fb-101">Коллекция пользовательских измерений.</span><span class="sxs-lookup"><span data-stu-id="ce7fb-101">Collection of custom measurements.</span></span> <span data-ttu-id="ce7fb-102">Используйте этот tooreport коллекции с именем измерения, связанный с элементом телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="ce7fb-102">Use this collection tooreport named measurement associated with hello telemetry item.</span></span> <span data-ttu-id="ce7fb-103">Типичные случаи использования:</span><span class="sxs-lookup"><span data-stu-id="ce7fb-103">Typical use cases are:</span></span>
- <span data-ttu-id="ce7fb-104">Hello размер полезных данных телеметрии зависимости</span><span class="sxs-lookup"><span data-stu-id="ce7fb-104">hello size of Dependency Telemetry payload</span></span>
- <span data-ttu-id="ce7fb-105">Hello число обрабатываемых запросов телеметрии элементов очереди</span><span class="sxs-lookup"><span data-stu-id="ce7fb-105">hello number of queue items processed by Request Telemetry</span></span>
- <span data-ttu-id="ce7fb-106">время клиента заняло toocomplete hello шаг в этапе завершения работы мастера телеметрии события.</span><span class="sxs-lookup"><span data-stu-id="ce7fb-106">time that customer took toocomplete hello step in wizard step completion Event Telemetry.</span></span>

<span data-ttu-id="ce7fb-107">[Пользовательские измерения](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) можно запросить в аналитике приложений:</span><span class="sxs-lookup"><span data-stu-id="ce7fb-107">You can query [custom measurements](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) in Application Analytics:</span></span>

```
customEvents
| where customMeasurements != ""
| summarize avg(todouble(customMeasurements["Completion Time"]) * itemCount)
```

 > [!NOTE]
 > <span data-ttu-id="ce7fb-108">Пользовательские измерения связаны с hello телеметрии элемента, которому они принадлежат.</span><span class="sxs-lookup"><span data-stu-id="ce7fb-108">Custom measurements are associated with hello telemetry item they belong to.</span></span> <span data-ttu-id="ce7fb-109">Они являются toosampling тема с элементом hello телеметрии, содержащий эти измерения.</span><span class="sxs-lookup"><span data-stu-id="ce7fb-109">They are subject toosampling with hello telemetry item containing those measurements.</span></span> <span data-ttu-id="ce7fb-110">tootrack измерения со значением, независимо от других типов данных телеметрии, используйте [метрики телеметрии](../articles/application-insights/app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="ce7fb-110">tootrack a measurement that has a value independent from other telemetry types, use [Metric telemetry](../articles/application-insights/app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="ce7fb-111">Максимальная длина ключа: 150</span><span class="sxs-lookup"><span data-stu-id="ce7fb-111">Max key length: 150</span></span>
