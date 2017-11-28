
<span data-ttu-id="53a57-101">Узнайте больше о глобальном распределении Azure Cosmos DB в этом видео из цикла "Пятница с Azure" от Скотта Хенсельмана (Scott Hanselman) и главного технического руководителя Картика Рамана (Karthik Raman).</span><span class="sxs-lookup"><span data-stu-id="53a57-101">You can learn about Azure Cosmos DB global distribution in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

<span data-ttu-id="53a57-102">Дополнительные сведения о том, как функционирует репликация глобальной базы данных в Cosmos DB, см. в статье о [глобальном распределении данных в Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="53a57-102">For more information about how global database replication works in Cosmos DB, see [Distribute data globally with Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span></span>

## <span data-ttu-id="53a57-103"><a id="addregion"></a>Добавление регионов глобальной базы данных с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="53a57-103"><a id="addregion"></a>Add global database regions using the Azure Portal</span></span>
<span data-ttu-id="53a57-104">База данных Azure Cosmos DB доступна во всех [регионах Azure][azureregions] по всему миру.</span><span class="sxs-lookup"><span data-stu-id="53a57-104">Azure Cosmos DB is available in all [Azure regions][azureregions] world-wide.</span></span> <span data-ttu-id="53a57-105">После выбора уровня согласованности по умолчанию для учетной записи базы данных вы можете связать один или несколько регионов (в зависимости от выбранного уровня согласованности по умолчанию и потребностей глобального распространения).</span><span class="sxs-lookup"><span data-stu-id="53a57-105">After selecting the default consistency level for your database account, you can associate one or more regions (depending on your choice of default consistency level and global distribution needs).</span></span>

1. <span data-ttu-id="53a57-106">На левой панели на [портале Azure](https://portal.azure.com/) щелкните **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="53a57-106">In the [Azure portal](https://portal.azure.com/), in the left bar, click **Azure Cosmos DB**.</span></span>
2. <span data-ttu-id="53a57-107">В колонке **Azure Cosmos DB** выберите учетную запись базы данных, которую нужно изменить.</span><span class="sxs-lookup"><span data-stu-id="53a57-107">In the **Azure Cosmos DB** blade, select the database account to modify.</span></span>
3. <span data-ttu-id="53a57-108">В меню колонки учетной записи щелкните **Глобальная репликация данных**.</span><span class="sxs-lookup"><span data-stu-id="53a57-108">In the account blade, click **Replicate data globally** from the menu.</span></span>
4. <span data-ttu-id="53a57-109">В колонке **Глобальная репликация данных** выберите регионы для добавления или удаления, щелкнув их на карте, и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="53a57-109">In the **Replicate data globally** blade, select the regions to add or remove by clicking regions in the map, and then click **Save**.</span></span> <span data-ttu-id="53a57-110">Добавление регионов оплачивается. Для получения дополнительной информации перейдите на [страницу цен](https://azure.microsoft.com/pricing/details/documentdb/) или прочитайте статью [Глобальное распространение данных с помощью DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="53a57-110">There is a cost to adding regions, see the [pricing page](https://azure.microsoft.com/pricing/details/documentdb/) or the [Distribute data globally with DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) article for more information.</span></span>
   
    ![Можно щелкать регионы на карте, чтобы добавить или удалить их.][1]
    
<span data-ttu-id="53a57-112">Когда вы добавите второй регион, на портале в колонке **Глобальная репликация данных** активируется параметр **Ручная отработка отказа**.</span><span class="sxs-lookup"><span data-stu-id="53a57-112">Once you add a second region, the **Manual Failover** option is enabled on the **Replicate data globally** blade in the portal.</span></span> <span data-ttu-id="53a57-113">Этот параметр можно использовать для тестирования отработки отказа или изменения основного региона записи.</span><span class="sxs-lookup"><span data-stu-id="53a57-113">You can use this option to test the failover process or change the primary write region.</span></span> <span data-ttu-id="53a57-114">После добавления третьего региона в той же колонке активируется параметр **Приоритеты при отработке отказа**, позволяющий изменить порядок отработки отказов для операций чтения.</span><span class="sxs-lookup"><span data-stu-id="53a57-114">Once you add a third region, the **Failover Priorities** option is enabled on the same blade so that you can change the failover order for reads.</span></span>  

### <a name="selecting-global-database-regions"></a><span data-ttu-id="53a57-115">Выбор регионов глобальной базы данных</span><span class="sxs-lookup"><span data-stu-id="53a57-115">Selecting global database regions</span></span>
<span data-ttu-id="53a57-116">Существуют два распространенных сценария настройки нескольких регионов:</span><span class="sxs-lookup"><span data-stu-id="53a57-116">There are two common scenarios for configuring two or more regions:</span></span>

1. <span data-ttu-id="53a57-117">Обеспечение низкой задержки при обращении пользователей к данным по всему миру не зависимо от расположения.</span><span class="sxs-lookup"><span data-stu-id="53a57-117">Delivering low-latency access to data to end users no matter where they are located around the globe</span></span>
2. <span data-ttu-id="53a57-118">Добавление региональной устойчивости для непрерывности бизнес-процессов и аварийного восстановления (BCDR)</span><span class="sxs-lookup"><span data-stu-id="53a57-118">Adding regional resiliency for business continuity and disaster recovery (BCDR)</span></span>

<span data-ttu-id="53a57-119">Чтобы обеспечить низкую задержку для пользователей, мы советуем развернуть приложение и добавить Azure Cosmos DB в регионы, соответствующие расположению пользователей приложения.</span><span class="sxs-lookup"><span data-stu-id="53a57-119">For delivering low-latency to end-users, it is recommended to deploy both the application and add Azure Cosmos DB in the regions thats correspond to where the application's users are located.</span></span>

<span data-ttu-id="53a57-120">Для BCDR мы рекомендуем добавлять регионы исходя из пар регионов, описанных в статье [Непрерывность бизнес-процессов и аварийное восстановление в службах BizTalk: пары регионов Azure][bcdr].</span><span class="sxs-lookup"><span data-stu-id="53a57-120">For BCDR, it is recommended to add regions based on the region pairs described in the [Business continuity and disaster recovery (BCDR): Azure Paired Regions][bcdr] article.</span></span>

<!--

## <a id="selectwriteregion"></a>Select the write region

While all regions associated with your Cosmos DB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive the write (insert, upsert, replace, delete) requests. To set the active write region, do the following  


1. In the **Azure Cosmos DB** blade, select the database account to modify.
2. In the account blade, click **Replicate data globally** from the menu.
3. In the **Replicate data globally** blade, click **Manual Failover** from the top bar.
    ![Change the write region under Azure Cosmos DB Account > Replicate data globally > Manual Failover][2]
4. Select a read region to become the new write region, click the checkbox to confirm triggering a failover, and click OK
    ![Change the write region by selecting a new region in list under Azure Cosmos DB Account > Replicate data globally > Manual Failover][3]

--->

<!--Image references-->
[1]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-add-region.png
[2]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-1.png
[3]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-2.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: ../articles/cosmos-db/consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
