
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, hello following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
<span data-ttu-id="5b3c6-101">При возобновлении работы базы данных происходят указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="5b3c6-101">When you resume a database:</span></span>

* <span data-ttu-id="5b3c6-102">Хранилище данных SQL получает вычислительные ресурсы и ресурсы памяти для заданного количества единиц DWU.</span><span class="sxs-lookup"><span data-stu-id="5b3c6-102">SQL Data Warehouse acquires compute and memory resources for your DWU setting.</span></span>
* <span data-ttu-id="5b3c6-103">Вычисляется стоимость возобновления DWU.</span><span class="sxs-lookup"><span data-stu-id="5b3c6-103">Compute charges for your DWUs resume.</span></span>
* <span data-ttu-id="5b3c6-104">Данные становятся доступны.</span><span class="sxs-lookup"><span data-stu-id="5b3c6-104">Your data will be available.</span></span>
* <span data-ttu-id="5b3c6-105">Вам потребуется toorestart запросы рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="5b3c6-105">You will need toorestart your workload queries.</span></span>

