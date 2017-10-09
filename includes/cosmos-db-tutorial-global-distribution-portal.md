
Узнайте больше о глобальном распределении Azure Cosmos DB в этом видео из цикла "Пятница с Azure" от Скотта Хенсельмана (Scott Hanselman) и главного технического руководителя Картика Рамана (Karthik Raman).

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

Дополнительные сведения о том, как функционирует репликация глобальной базы данных в Cosmos DB, см. в статье о [глобальном распределении данных в Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).

## <a id="addregion"></a>Добавление областей глобальной базы данных с помощью портала Azure hello
База данных Azure Cosmos DB доступна во всех [регионах Azure][azureregions] по всему миру. После выбора hello уровень согласованности по умолчанию для учетной записи базы данных, можно связать одну или несколько областей (в зависимости от выбранного уровня и глобальные распространения требований к согласованности по умолчанию).

1. В hello [портал Azure](https://portal.azure.com/)в hello левой панели, щелкнув **Azure Cosmos DB**.
2. В hello **Azure Cosmos DB** колонки, toomodify учетной записи базы данных выберите hello.
3. В колонке hello учетной записи, нажмите кнопку **глобально реплицировать данные** меню "hello".
4. В hello **глобально реплицировать данные** колонке выберите tooadd hello области или удалить, щелкнув областей в карте hello и нажмите кнопку **Сохранить**. Нет области tooadding стоимость см. в разделе hello [странице цен](https://azure.microsoft.com/pricing/details/documentdb/) или hello [распределение данных глобально с DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) для получения дополнительных сведений.
   
    ![Щелкните области hello в tooadd карты hello или удалить их][1]
    
После добавления второй области hello **перехода на другой ресурс вручную** hello включен параметр **глобально реплицировать данные** колонке hello портала. Можно использовать этот процесс перехода на другой ресурс hello tootest параметр или изменить регион hello основной записи. После добавления третьего области hello **приоритетов отработки отказа** включен параметр hello же колонки, можно изменить порядок отработки отказа hello для операций чтения.  

### <a name="selecting-global-database-regions"></a>Выбор регионов глобальной базы данных
Существуют два распространенных сценария настройки нескольких регионов:

1. Доставка низкой задержкой доступа пользователей tooend toodata независимо от того, где они находятся земного шара hello
2. Добавление региональной устойчивости для непрерывности бизнес-процессов и аварийного восстановления (BCDR)

Предоставляющих tooend низкой задержкой-пользователям рекомендуется toodeploy оба приложения hello и добавить Cosmos базу данных Azure в регионах hello, имеет соответствующие пользователи приложения hello toowhere расположены.

Для BCDR, рекомендуется tooadd областей, на основании пар номеров области hello, описанные в hello [бизнеса непрерывности и аварийного восстановления (BCDR): пару регионы Azure] [ bcdr] статьи.

<!--

## <a id="selectwriteregion"></a>Select hello write region

While all regions associated with your Cosmos DB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive hello write (insert, upsert, replace, delete) requests. tooset hello active write region, do hello following  


1. In hello **Azure Cosmos DB** blade, select hello database account toomodify.
2. In hello account blade, click **Replicate data globally** from hello menu.
3. In hello **Replicate data globally** blade, click **Manual Failover** from hello top bar.
    ![Change hello write region under Azure Cosmos DB Account > Replicate data globally > Manual Failover][2]
4. Select a read region toobecome hello new write region, click hello checkbox tooconfirm triggering a failover, and click OK
    ![Change hello write region by selecting a new region in list under Azure Cosmos DB Account > Replicate data globally > Manual Failover][3]

--->

<!--Image references-->
[1]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-add-region.png
[2]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-1.png
[3]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-2.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: ../articles/cosmos-db/consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
