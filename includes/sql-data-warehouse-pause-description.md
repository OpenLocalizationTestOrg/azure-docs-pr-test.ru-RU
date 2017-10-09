
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, hello following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
toosave затраты, можно приостановить и возобновить вычислительные ресурсы по требованию. Например если не будет использоваться hello базы данных во время ночь hello и по выходным, можно приостановить ее работу в то время и возобновите ее работу в течение дня hello. Вы не будете платить за Dwu во время приостановки базы данных hello.

При приостановке работы базы данных происходит следующее.

* Ресурсов памяти и вычислительных ресурсов возвращаются toohello пула ресурсов, доступных в центре обработки данных hello
* DWU затраты равны нулю hello время паузы hello.
* Хранилище данных не затрагивается, и ваши данные остаются без изменений. 
* Хранилище данных SQL отменяет все выполняющиеся и поставленные в очередь операции.

