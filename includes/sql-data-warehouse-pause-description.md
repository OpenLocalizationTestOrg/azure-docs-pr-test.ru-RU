
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, hello following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
<span data-ttu-id="86ba7-101">toosave затраты, можно приостановить и возобновить вычислительные ресурсы по требованию.</span><span class="sxs-lookup"><span data-stu-id="86ba7-101">toosave costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="86ba7-102">Например если не будет использоваться hello базы данных во время ночь hello и по выходным, можно приостановить ее работу в то время и возобновите ее работу в течение дня hello.</span><span class="sxs-lookup"><span data-stu-id="86ba7-102">For example, if you won't be using hello database during hello night and on weekends, you can pause it during those times, and resume it during hello day.</span></span> <span data-ttu-id="86ba7-103">Вы не будете платить за Dwu во время приостановки базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="86ba7-103">You won't be charged for DWUs while hello database is paused.</span></span>

<span data-ttu-id="86ba7-104">При приостановке работы базы данных происходит следующее.</span><span class="sxs-lookup"><span data-stu-id="86ba7-104">When you pause a database:</span></span>

* <span data-ttu-id="86ba7-105">Ресурсов памяти и вычислительных ресурсов возвращаются toohello пула ресурсов, доступных в центре обработки данных hello</span><span class="sxs-lookup"><span data-stu-id="86ba7-105">Compute and memory resources are returned toohello pool of available resources in hello data center</span></span>
* <span data-ttu-id="86ba7-106">DWU затраты равны нулю hello время паузы hello.</span><span class="sxs-lookup"><span data-stu-id="86ba7-106">DWU costs are zero for hello duration of hello pause.</span></span>
* <span data-ttu-id="86ba7-107">Хранилище данных не затрагивается, и ваши данные остаются без изменений.</span><span class="sxs-lookup"><span data-stu-id="86ba7-107">Data storage is not affected and your data stays intact.</span></span> 
* <span data-ttu-id="86ba7-108">Хранилище данных SQL отменяет все выполняющиеся и поставленные в очередь операции.</span><span class="sxs-lookup"><span data-stu-id="86ba7-108">SQL Data Warehouse cancels all running or queued operations.</span></span>

