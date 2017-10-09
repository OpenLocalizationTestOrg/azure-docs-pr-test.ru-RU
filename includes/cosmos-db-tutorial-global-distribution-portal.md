
<span data-ttu-id="b0c2b-101">Узнайте больше о глобальном распределении Azure Cosmos DB в этом видео из цикла "Пятница с Azure" от Скотта Хенсельмана (Scott Hanselman) и главного технического руководителя Картика Рамана (Karthik Raman).</span><span class="sxs-lookup"><span data-stu-id="b0c2b-101">You can learn about Azure Cosmos DB global distribution in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

<span data-ttu-id="b0c2b-102">Дополнительные сведения о том, как функционирует репликация глобальной базы данных в Cosmos DB, см. в статье о [глобальном распределении данных в Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="b0c2b-102">For more information about how global database replication works in Cosmos DB, see [Distribute data globally with Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span></span>

## <span data-ttu-id="b0c2b-103"><a id="addregion"></a>Добавление областей глобальной базы данных с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="b0c2b-103"><a id="addregion"></a>Add global database regions using hello Azure Portal</span></span>
<span data-ttu-id="b0c2b-104">База данных Azure Cosmos DB доступна во всех [регионах Azure][azureregions] по всему миру.</span><span class="sxs-lookup"><span data-stu-id="b0c2b-104">Azure Cosmos DB is available in all [Azure regions][azureregions] world-wide.</span></span> <span data-ttu-id="b0c2b-105">После выбора hello уровень согласованности по умолчанию для учетной записи базы данных, можно связать одну или несколько областей (в зависимости от выбранного уровня и глобальные распространения требований к согласованности по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="b0c2b-105">After selecting hello default consistency level for your database account, you can associate one or more regions (depending on your choice of default consistency level and global distribution needs).</span></span>

1. <span data-ttu-id="b0c2b-106">В hello [портал Azure](https://portal.azure.com/)в hello левой панели, щелкнув **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="b0c2b-106">In hello [Azure portal](https://portal.azure.com/), in hello left bar, click **Azure Cosmos DB**.</span></span>
2. <span data-ttu-id="b0c2b-107">В hello **Azure Cosmos DB** колонки, toomodify учетной записи базы данных выберите hello.</span><span class="sxs-lookup"><span data-stu-id="b0c2b-107">In hello **Azure Cosmos DB** blade, select hello database account toomodify.</span></span>
3. <span data-ttu-id="b0c2b-108">В колонке hello учетной записи, нажмите кнопку **глобально реплицировать данные** меню "hello".</span><span class="sxs-lookup"><span data-stu-id="b0c2b-108">In hello account blade, click **Replicate data globally** from hello menu.</span></span>
4. <span data-ttu-id="b0c2b-109">В hello **глобально реплицировать данные** колонке выберите tooadd hello области или удалить, щелкнув областей в карте hello и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b0c2b-109">In hello **Replicate data globally** blade, select hello regions tooadd or remove by clicking regions in hello map, and then click **Save**.</span></span> <span data-ttu-id="b0c2b-110">Нет области tooadding стоимость см. в разделе hello [странице цен](https://azure.microsoft.com/pricing/details/documentdb/) или hello [распределение данных глобально с DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="b0c2b-110">There is a cost tooadding regions, see hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/) or hello [Distribute data globally with DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) article for more information.</span></span>
   
    ![Щелкните области hello в tooadd карты hello или удалить их][1]
    
<span data-ttu-id="b0c2b-112">После добавления второй области hello **перехода на другой ресурс вручную** hello включен параметр **глобально реплицировать данные** колонке hello портала.</span><span class="sxs-lookup"><span data-stu-id="b0c2b-112">Once you add a second region, hello **Manual Failover** option is enabled on hello **Replicate data globally** blade in hello portal.</span></span> <span data-ttu-id="b0c2b-113">Можно использовать этот процесс перехода на другой ресурс hello tootest параметр или изменить регион hello основной записи.</span><span class="sxs-lookup"><span data-stu-id="b0c2b-113">You can use this option tootest hello failover process or change hello primary write region.</span></span> <span data-ttu-id="b0c2b-114">После добавления третьего области hello **приоритетов отработки отказа** включен параметр hello же колонки, можно изменить порядок отработки отказа hello для операций чтения.</span><span class="sxs-lookup"><span data-stu-id="b0c2b-114">Once you add a third region, hello **Failover Priorities** option is enabled on hello same blade so that you can change hello failover order for reads.</span></span>  

### <a name="selecting-global-database-regions"></a><span data-ttu-id="b0c2b-115">Выбор регионов глобальной базы данных</span><span class="sxs-lookup"><span data-stu-id="b0c2b-115">Selecting global database regions</span></span>
<span data-ttu-id="b0c2b-116">Существуют два распространенных сценария настройки нескольких регионов:</span><span class="sxs-lookup"><span data-stu-id="b0c2b-116">There are two common scenarios for configuring two or more regions:</span></span>

1. <span data-ttu-id="b0c2b-117">Доставка низкой задержкой доступа пользователей tooend toodata независимо от того, где они находятся земного шара hello</span><span class="sxs-lookup"><span data-stu-id="b0c2b-117">Delivering low-latency access toodata tooend users no matter where they are located around hello globe</span></span>
2. <span data-ttu-id="b0c2b-118">Добавление региональной устойчивости для непрерывности бизнес-процессов и аварийного восстановления (BCDR)</span><span class="sxs-lookup"><span data-stu-id="b0c2b-118">Adding regional resiliency for business continuity and disaster recovery (BCDR)</span></span>

<span data-ttu-id="b0c2b-119">Предоставляющих tooend низкой задержкой-пользователям рекомендуется toodeploy оба приложения hello и добавить Cosmos базу данных Azure в регионах hello, имеет соответствующие пользователи приложения hello toowhere расположены.</span><span class="sxs-lookup"><span data-stu-id="b0c2b-119">For delivering low-latency tooend-users, it is recommended toodeploy both hello application and add Azure Cosmos DB in hello regions thats correspond toowhere hello application's users are located.</span></span>

<span data-ttu-id="b0c2b-120">Для BCDR, рекомендуется tooadd областей, на основании пар номеров области hello, описанные в hello [бизнеса непрерывности и аварийного восстановления (BCDR): пару регионы Azure] [ bcdr] статьи.</span><span class="sxs-lookup"><span data-stu-id="b0c2b-120">For BCDR, it is recommended tooadd regions based on hello region pairs described in hello [Business continuity and disaster recovery (BCDR): Azure Paired Regions][bcdr] article.</span></span>

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
