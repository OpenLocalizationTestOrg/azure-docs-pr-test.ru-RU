<span data-ttu-id="5ae4a-101">Коллекция пользовательских измерений.</span><span class="sxs-lookup"><span data-stu-id="5ae4a-101">Collection of custom measurements.</span></span> <span data-ttu-id="5ae4a-102">Используйте эту коллекцию для создания отчета с именем измерения, связанного с элементом телеметрии.</span><span class="sxs-lookup"><span data-stu-id="5ae4a-102">Use this collection to report named measurement associated with the telemetry item.</span></span> <span data-ttu-id="5ae4a-103">Типичные случаи использования:</span><span class="sxs-lookup"><span data-stu-id="5ae4a-103">Typical use cases are:</span></span>
- <span data-ttu-id="5ae4a-104">Размер полезных данных телеметрии зависимостей.</span><span class="sxs-lookup"><span data-stu-id="5ae4a-104">the size of Dependency Telemetry payload</span></span>
- <span data-ttu-id="5ae4a-105">Число элементов очереди, обрабатываемых телеметрией запросов.</span><span class="sxs-lookup"><span data-stu-id="5ae4a-105">the number of queue items processed by Request Telemetry</span></span>
- <span data-ttu-id="5ae4a-106">Время, требуемое клиенту для завершения шага в мастере телеметрии событий.</span><span class="sxs-lookup"><span data-stu-id="5ae4a-106">time that customer took to complete the step in wizard step completion Event Telemetry.</span></span>

<span data-ttu-id="5ae4a-107">[Пользовательские измерения](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) можно запросить в аналитике приложений:</span><span class="sxs-lookup"><span data-stu-id="5ae4a-107">You can query [custom measurements](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) in Application Analytics:</span></span>

```
customEvents
| where customMeasurements != ""
| summarize avg(todouble(customMeasurements["Completion Time"]) * itemCount)
```

 > [!NOTE]
 > <span data-ttu-id="5ae4a-108">Пользовательские измерения связаны с элементом телеметрии, к которому они принадлежат.</span><span class="sxs-lookup"><span data-stu-id="5ae4a-108">Custom measurements are associated with the telemetry item they belong to.</span></span> <span data-ttu-id="5ae4a-109">Они должны быть доступны для выборки с использованием элемента телеметрии, содержащего эти измерения.</span><span class="sxs-lookup"><span data-stu-id="5ae4a-109">They are subject to sampling with the telemetry item containing those measurements.</span></span> <span data-ttu-id="5ae4a-110">Чтобы отследить измерения со значением, которое не зависит от другого типа телеметрии, используйте [телеметрию метрик](../articles/application-insights/app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="5ae4a-110">To track a measurement that has a value independent from other telemetry types, use [Metric telemetry](../articles/application-insights/app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="5ae4a-111">Максимальная длина ключа: 150</span><span class="sxs-lookup"><span data-stu-id="5ae4a-111">Max key length: 150</span></span>
