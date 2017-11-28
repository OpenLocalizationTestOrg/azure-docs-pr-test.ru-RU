<span data-ttu-id="3e175-101">На этом шаге вручную создается прослушиватель группы доступности в диспетчере отказоустойчивости кластеров и службе SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="3e175-101">In this step, you manually create the availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

1. <span data-ttu-id="3e175-102">Откройте диспетчер отказоустойчивого кластера из узла, на котором размещена первичная реплика.</span><span class="sxs-lookup"><span data-stu-id="3e175-102">Open Failover Cluster Manager from the node that hosts the primary replica.</span></span>

2. <span data-ttu-id="3e175-103">Выберите узел **Сети** и запишите имя сети кластера.</span><span class="sxs-lookup"><span data-stu-id="3e175-103">Select the **Networks** node, and then note the cluster network name.</span></span> <span data-ttu-id="3e175-104">Это имя будет использоваться в переменной $ClusterNetworkName в скрипте PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e175-104">This name is used in the $ClusterNetworkName variable in the PowerShell script.</span></span>

3. <span data-ttu-id="3e175-105">Разверните имя кластера и нажмите кнопку **Роли**.</span><span class="sxs-lookup"><span data-stu-id="3e175-105">Expand the cluster name, and then click **Roles**.</span></span>

4. <span data-ttu-id="3e175-106">На панели **Роли** щелкните правой кнопкой мыши имя группы доступности и выберите **Добавить ресурс** > **Точка доступа клиента**.</span><span class="sxs-lookup"><span data-stu-id="3e175-106">In the **Roles** pane, right-click the availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>
   
    ![Добавление точки доступа клиента для группы доступности](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. <span data-ttu-id="3e175-108">В поле **Имя** создайте имя для этого нового прослушивателя, а затем дважды щелкните **Далее** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="3e175-108">In the **Name** box, create a name for this new listener, click **Next** twice, and then click **Finish**.</span></span>  
    <span data-ttu-id="3e175-109">Не подключайте прослушивателя или ресурс на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="3e175-109">Do not bring the listener or resource online at this point.</span></span>

6. <span data-ttu-id="3e175-110">Перейдите на вкладку **Ресурсы** и разверните созданную точку доступа клиента.</span><span class="sxs-lookup"><span data-stu-id="3e175-110">Click the **Resources** tab, and then expand the client access point you just created.</span></span> 
    <span data-ttu-id="3e175-111">Отобразится ресурс IP-адреса для каждой сети в кластере.</span><span class="sxs-lookup"><span data-stu-id="3e175-111">The IP address resource for each cluster network in your cluster is displayed.</span></span> <span data-ttu-id="3e175-112">Если это решение только для Azure, вы увидите только один ресурс IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="3e175-112">If this is an Azure-only solution, only one IP address resource is displayed.</span></span>

7. <span data-ttu-id="3e175-113">Выполните одно из приведенных ниже действий.</span><span class="sxs-lookup"><span data-stu-id="3e175-113">Do either of the following:</span></span>
   
   * <span data-ttu-id="3e175-114">Для настройки гибридного решения:</span><span class="sxs-lookup"><span data-stu-id="3e175-114">To configure a hybrid solution:</span></span>
     
        <span data-ttu-id="3e175-115">а.</span><span class="sxs-lookup"><span data-stu-id="3e175-115">a.</span></span> <span data-ttu-id="3e175-116">Щелкните правой кнопкой мыши ресурс IP-адреса, соответствующий локальной подсети, и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="3e175-116">Right-click the IP address resource that corresponds to your on-premises subnet, and then select **Properties**.</span></span> <span data-ttu-id="3e175-117">Запишите имя IP-адреса и имя сети.</span><span class="sxs-lookup"><span data-stu-id="3e175-117">Note the IP address name and network name.</span></span>
   
        <span data-ttu-id="3e175-118">b.</span><span class="sxs-lookup"><span data-stu-id="3e175-118">b.</span></span> <span data-ttu-id="3e175-119">Выберите **Статический IP-адрес**, присвойте неиспользуемый IP-адрес и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3e175-119">Select **Static IP Address**, assign an unused IP address, and then click **OK**.</span></span>
 
   * <span data-ttu-id="3e175-120">Для настройки решения только для Azure:</span><span class="sxs-lookup"><span data-stu-id="3e175-120">To configure an Azure-only solution:</span></span>

        <span data-ttu-id="3e175-121">а.</span><span class="sxs-lookup"><span data-stu-id="3e175-121">a.</span></span> <span data-ttu-id="3e175-122">Щелкните правой кнопкой мыши ресурс IP-адреса, соответствующий подсети Azure, и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="3e175-122">Right-click the IP address resource that corresponds to your Azure subnet, and then select **Properties**.</span></span>
       
       > [!NOTE]
       > <span data-ttu-id="3e175-123">Если позднее прослушиватель не будет подключаться из-за конфликтующего IP-адреса, выбранного протоколом DHCP, вы сможете настроить допустимый статический IP-адрес в этом окне свойств.</span><span class="sxs-lookup"><span data-stu-id="3e175-123">If the listener later fails to come online because of a conflicting IP address selected by DHCP, you can configure a valid static IP address in this properties window.</span></span>
       > 
       > 

       <span data-ttu-id="3e175-124">b.</span><span class="sxs-lookup"><span data-stu-id="3e175-124">b.</span></span> <span data-ttu-id="3e175-125">В этом же окне свойств **IP-адрес** измените **имя IP-адреса**.</span><span class="sxs-lookup"><span data-stu-id="3e175-125">In the same **IP Address** properties window, change the **IP Address Name**.</span></span>  
        <span data-ttu-id="3e175-126">Это имя будет использоваться в переменной $IPResourceName скрипта PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e175-126">This name is used in the $IPResourceName variable of the PowerShell script.</span></span> <span data-ttu-id="3e175-127">Повторите этот шаг для каждого IP-ресурса, если решение распространяется на несколько виртуальных сетей Azure.</span><span class="sxs-lookup"><span data-stu-id="3e175-127">If your solution spans multiple Azure virtual networks, repeat this step for each IP resource.</span></span>

