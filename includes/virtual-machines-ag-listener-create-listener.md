<span data-ttu-id="22aa4-101">На этом шаге вы вручную создать прослушиватель группы доступности hello в Диспетчер отказоустойчивости кластеров и SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="22aa4-101">In this step, you manually create hello availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

1. <span data-ttu-id="22aa4-102">Откройте Диспетчер отказоустойчивости кластеров из узла "hello", на котором размещена первичная реплика hello.</span><span class="sxs-lookup"><span data-stu-id="22aa4-102">Open Failover Cluster Manager from hello node that hosts hello primary replica.</span></span>

2. <span data-ttu-id="22aa4-103">Выберите hello **сетей** узел, а затем — сетевое имя кластера Примечание hello.</span><span class="sxs-lookup"><span data-stu-id="22aa4-103">Select hello **Networks** node, and then note hello cluster network name.</span></span> <span data-ttu-id="22aa4-104">Это имя используется в переменной hello $ClusterNetworkName в hello сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22aa4-104">This name is used in hello $ClusterNetworkName variable in hello PowerShell script.</span></span>

3. <span data-ttu-id="22aa4-105">Разверните имя кластера hello и щелкните **ролей**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-105">Expand hello cluster name, and then click **Roles**.</span></span>

4. <span data-ttu-id="22aa4-106">В hello **ролей** панели, щелкните правой кнопкой мыши группу доступности hello имя, а затем выберите **добавить ресурс** > **точки доступа клиента**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-106">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>
   
    ![Добавление точки доступа клиента для группы доступности](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. <span data-ttu-id="22aa4-108">В hello **имя** введите имя для этого нового прослушивателя, нажмите кнопку **Далее** дважды, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-108">In hello **Name** box, create a name for this new listener, click **Next** twice, and then click **Finish**.</span></span>  
    <span data-ttu-id="22aa4-109">Не следует переводить прослушиватель hello или ресурс в оперативный режим на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="22aa4-109">Do not bring hello listener or resource online at this point.</span></span>

6. <span data-ttu-id="22aa4-110">Нажмите кнопку hello **ресурсов** вкладку, а затем разверните только что созданную точку доступа клиента hello.</span><span class="sxs-lookup"><span data-stu-id="22aa4-110">Click hello **Resources** tab, and then expand hello client access point you just created.</span></span> 
    <span data-ttu-id="22aa4-111">отображается Hello ресурс IP-адреса для каждой сети кластера в кластере.</span><span class="sxs-lookup"><span data-stu-id="22aa4-111">hello IP address resource for each cluster network in your cluster is displayed.</span></span> <span data-ttu-id="22aa4-112">Если это решение только для Azure, вы увидите только один ресурс IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="22aa4-112">If this is an Azure-only solution, only one IP address resource is displayed.</span></span>

7. <span data-ttu-id="22aa4-113">Выполните одно из следующих hello.</span><span class="sxs-lookup"><span data-stu-id="22aa4-113">Do either of hello following:</span></span>
   
   * <span data-ttu-id="22aa4-114">tooconfigure гибридное решение:</span><span class="sxs-lookup"><span data-stu-id="22aa4-114">tooconfigure a hybrid solution:</span></span>
     
        <span data-ttu-id="22aa4-115">а.</span><span class="sxs-lookup"><span data-stu-id="22aa4-115">a.</span></span> <span data-ttu-id="22aa4-116">Щелкните правой кнопкой мыши hello ресурс IP-адреса, соответствующий tooyour в локальной подсети, а затем выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-116">Right-click hello IP address resource that corresponds tooyour on-premises subnet, and then select **Properties**.</span></span> <span data-ttu-id="22aa4-117">Обратите внимание, hello IP-адрес и имя сети.</span><span class="sxs-lookup"><span data-stu-id="22aa4-117">Note hello IP address name and network name.</span></span>
   
        <span data-ttu-id="22aa4-118">b.</span><span class="sxs-lookup"><span data-stu-id="22aa4-118">b.</span></span> <span data-ttu-id="22aa4-119">Выберите **Статический IP-адрес**, присвойте неиспользуемый IP-адрес и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-119">Select **Static IP Address**, assign an unused IP address, and then click **OK**.</span></span>
 
   * <span data-ttu-id="22aa4-120">tooconfigure решения только в Azure:</span><span class="sxs-lookup"><span data-stu-id="22aa4-120">tooconfigure an Azure-only solution:</span></span>

        <span data-ttu-id="22aa4-121">а.</span><span class="sxs-lookup"><span data-stu-id="22aa4-121">a.</span></span> <span data-ttu-id="22aa4-122">Щелкните правой кнопкой мыши hello ресурс IP-адреса, соответствующий tooyour подсети Azure, а затем выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-122">Right-click hello IP address resource that corresponds tooyour Azure subnet, and then select **Properties**.</span></span>
       
       > [!NOTE]
       > <span data-ttu-id="22aa4-123">Если прослушиватель hello позднее происходит сбой toocome в оперативный режим из-за конфликтующих выбранного DHCP-сервером IP-адреса, можно настроить допустимый статический IP-адрес в этом окне свойств.</span><span class="sxs-lookup"><span data-stu-id="22aa4-123">If hello listener later fails toocome online because of a conflicting IP address selected by DHCP, you can configure a valid static IP address in this properties window.</span></span>
       > 
       > 

       <span data-ttu-id="22aa4-124">b.</span><span class="sxs-lookup"><span data-stu-id="22aa4-124">b.</span></span> <span data-ttu-id="22aa4-125">В hello же **IP-адрес** окно свойств, изменение hello **имя IP-адреса**.</span><span class="sxs-lookup"><span data-stu-id="22aa4-125">In hello same **IP Address** properties window, change hello **IP Address Name**.</span></span>  
        <span data-ttu-id="22aa4-126">Это имя используется в переменной hello $IPResourceName hello сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22aa4-126">This name is used in hello $IPResourceName variable of hello PowerShell script.</span></span> <span data-ttu-id="22aa4-127">Повторите этот шаг для каждого IP-ресурса, если решение распространяется на несколько виртуальных сетей Azure.</span><span class="sxs-lookup"><span data-stu-id="22aa4-127">If your solution spans multiple Azure virtual networks, repeat this step for each IP resource.</span></span>

