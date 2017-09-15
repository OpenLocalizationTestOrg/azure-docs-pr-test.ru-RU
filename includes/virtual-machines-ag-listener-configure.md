<span data-ttu-id="89395-101">Прослушиватель группы доступности — это IP-адрес и сетевое имя, с которых ожидается передача данных в группе доступности SQL Server.</span><span class="sxs-lookup"><span data-stu-id="89395-101">The availability group listener is an IP address and network name that the SQL Server availability group listens on.</span></span> <span data-ttu-id="89395-102">Чтобы создать прослушиватель группы доступности, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="89395-102">To create the availability group listener, do the following:</span></span>

1. <span data-ttu-id="89395-103"><a name="getnet"></a>Получите имя сетевого ресурса для кластера.</span><span class="sxs-lookup"><span data-stu-id="89395-103"><a name="getnet"></a>Get the name of the cluster network resource.</span></span>

    <span data-ttu-id="89395-104">а.</span><span class="sxs-lookup"><span data-stu-id="89395-104">a.</span></span> <span data-ttu-id="89395-105">Подключитесь по протоколу RDP к виртуальной машине Azure, на которой размещена основная реплика.</span><span class="sxs-lookup"><span data-stu-id="89395-105">Use RDP to connect to the Azure virtual machine that hosts the primary replica.</span></span> 

    <span data-ttu-id="89395-106">b.</span><span class="sxs-lookup"><span data-stu-id="89395-106">b.</span></span> <span data-ttu-id="89395-107">Откройте диспетчер отказоустойчивости кластеров.</span><span class="sxs-lookup"><span data-stu-id="89395-107">Open Failover Cluster Manager.</span></span>

    <span data-ttu-id="89395-108">c.</span><span class="sxs-lookup"><span data-stu-id="89395-108">c.</span></span> <span data-ttu-id="89395-109">Выберите узел **Сети** и запишите имя сети кластера.</span><span class="sxs-lookup"><span data-stu-id="89395-109">Select the **Networks** node, and note the cluster network name.</span></span> <span data-ttu-id="89395-110">Это имя нужно использовать в переменной `$ClusterNetworkName` в сценарии PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89395-110">Use this name in the `$ClusterNetworkName` variable in the PowerShell script.</span></span> <span data-ttu-id="89395-111">На следующем изображении сетевое имя кластера — **Cluster Network 1**:</span><span class="sxs-lookup"><span data-stu-id="89395-111">In the following image the cluster network name is **Cluster Network 1**:</span></span>

   ![Сетевое имя кластера](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <span data-ttu-id="89395-113"><a name="addcap"></a>Добавьте точку доступа клиента.</span><span class="sxs-lookup"><span data-stu-id="89395-113"><a name="addcap"></a>Add the client access point.</span></span>  
    <span data-ttu-id="89395-114">Точка доступа клиента — это сетевое имя, которое используют приложения для подключения к базам данных в группе доступности.</span><span class="sxs-lookup"><span data-stu-id="89395-114">The client access point is the network name that applications use to connect to the databases in an availability group.</span></span> <span data-ttu-id="89395-115">Создайте точку доступа клиента в диспетчере отказоустойчивости кластеров.</span><span class="sxs-lookup"><span data-stu-id="89395-115">Create the client access point in Failover Cluster Manager.</span></span>

    <span data-ttu-id="89395-116">а.</span><span class="sxs-lookup"><span data-stu-id="89395-116">a.</span></span> <span data-ttu-id="89395-117">Разверните имя кластера и нажмите кнопку **Роли**.</span><span class="sxs-lookup"><span data-stu-id="89395-117">Expand the cluster name, and then click **Roles**.</span></span>

    <span data-ttu-id="89395-118">b.</span><span class="sxs-lookup"><span data-stu-id="89395-118">b.</span></span> <span data-ttu-id="89395-119">На панели **Роли** щелкните правой кнопкой мыши имя группы доступности и выберите **Добавить ресурс** > **Точка доступа клиента**.</span><span class="sxs-lookup"><span data-stu-id="89395-119">In the **Roles** pane, right-click the availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>

   ![Точка доступа клиента](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    <span data-ttu-id="89395-121">c.</span><span class="sxs-lookup"><span data-stu-id="89395-121">c.</span></span> <span data-ttu-id="89395-122">В поле **Имя** создайте имя для нового прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="89395-122">In the **Name** box, create a name for this new listener.</span></span> 
   <span data-ttu-id="89395-123">Имя для нового прослушивателя — это сетевое имя, которое используют приложения для подключения к базам данных в группе доступности SQL Server.</span><span class="sxs-lookup"><span data-stu-id="89395-123">The name for the new listener is the network name that applications use to connect to databases in the SQL Server availability group.</span></span>
   
    <span data-ttu-id="89395-124">г)</span><span class="sxs-lookup"><span data-stu-id="89395-124">d.</span></span> <span data-ttu-id="89395-125">Чтобы завершить создание прослушивателя, нажмите кнопку **Далее** дважды, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="89395-125">To finish creating the listener, click **Next** twice, and then click **Finish**.</span></span> <span data-ttu-id="89395-126">Не подключайте прослушивателя или ресурс на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="89395-126">Do not bring the listener or resource online at this point.</span></span>

3. <span data-ttu-id="89395-127"><a name="congroup"></a>Настройте ресурс IP-адреса для группы доступности.</span><span class="sxs-lookup"><span data-stu-id="89395-127"><a name="congroup"></a>Configure the IP resource for the availability group.</span></span>

    <span data-ttu-id="89395-128">а.</span><span class="sxs-lookup"><span data-stu-id="89395-128">a.</span></span> <span data-ttu-id="89395-129">Щелкните вкладку **Ресурсы** и разверните созданную точку доступа клиента.</span><span class="sxs-lookup"><span data-stu-id="89395-129">Click the **Resources** tab, and then expand the client access point you created.</span></span>  
    <span data-ttu-id="89395-130">Точка доступа клиента не подключена к сети.</span><span class="sxs-lookup"><span data-stu-id="89395-130">The client access point is offline.</span></span>

   ![Точка доступа клиента](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    <span data-ttu-id="89395-132">b.</span><span class="sxs-lookup"><span data-stu-id="89395-132">b.</span></span> <span data-ttu-id="89395-133">Щелкните правой кнопкой мыши ресурс IP-адреса и выберите пункт "Свойства".</span><span class="sxs-lookup"><span data-stu-id="89395-133">Right-click the IP resource, and then click properties.</span></span> <span data-ttu-id="89395-134">Запишите IP-адрес и используйте его в переменной `$IPResourceName` в скрипте PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89395-134">Note the name of the IP address, and use it in the `$IPResourceName` variable in the PowerShell script.</span></span>

    <span data-ttu-id="89395-135">c.</span><span class="sxs-lookup"><span data-stu-id="89395-135">c.</span></span> <span data-ttu-id="89395-136">В разделе **IP-адрес** выберите параметр **Статический IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="89395-136">Under **IP Address**, click **Static IP Address**.</span></span> <span data-ttu-id="89395-137">Задайте тот же IP-адрес, который использовался на портале Azure при настройке адреса подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="89395-137">Set the IP address as the same address that you used when you set the load balancer address on the Azure portal.</span></span>

   ![Ресурс IP-адреса](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <span data-ttu-id="89395-139"><a name = "dependencyGroup"></a>Сделайте так, чтобы ресурс группы доступности SQL Server зависел от точки доступа клиента.</span><span class="sxs-lookup"><span data-stu-id="89395-139"><a name = "dependencyGroup"></a>Make the SQL Server availability group resource dependent on the client access point.</span></span>

    <span data-ttu-id="89395-140">а.</span><span class="sxs-lookup"><span data-stu-id="89395-140">a.</span></span> <span data-ttu-id="89395-141">В диспетчере отказоустойчивости кластеров щелкните **Роли** и выберите группу доступности.</span><span class="sxs-lookup"><span data-stu-id="89395-141">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span>

    <span data-ttu-id="89395-142">b.</span><span class="sxs-lookup"><span data-stu-id="89395-142">b.</span></span> <span data-ttu-id="89395-143">На вкладке **Ресурсы** в разделе **Другие ресурсы** щелкните правой кнопкой мыши группу ресурсов и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="89395-143">On the **Resources** tab, under **Other Resources**, right-click the availability resource group, and then click **Properties**.</span></span> 

    <span data-ttu-id="89395-144">c.</span><span class="sxs-lookup"><span data-stu-id="89395-144">c.</span></span> <span data-ttu-id="89395-145">На вкладке "Зависимости" добавьте имя ресурса точки доступа клиента (прослушивателя).</span><span class="sxs-lookup"><span data-stu-id="89395-145">On the dependencies tab, add the name of the client access point (the listener) resource.</span></span>

   ![Ресурс IP-адреса](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    <span data-ttu-id="89395-147">г)</span><span class="sxs-lookup"><span data-stu-id="89395-147">d.</span></span> <span data-ttu-id="89395-148">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="89395-148">Click **OK**.</span></span>

5. <span data-ttu-id="89395-149"><a name="listname"></a>Сделайте так, чтобы ресурс точки доступа клиента зависел от IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="89395-149"><a name="listname"></a>Make the client access point resource dependent on the IP address.</span></span>

    <span data-ttu-id="89395-150">а.</span><span class="sxs-lookup"><span data-stu-id="89395-150">a.</span></span> <span data-ttu-id="89395-151">В диспетчере отказоустойчивости кластеров щелкните **Роли** и выберите группу доступности.</span><span class="sxs-lookup"><span data-stu-id="89395-151">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span> 

    <span data-ttu-id="89395-152">b.</span><span class="sxs-lookup"><span data-stu-id="89395-152">b.</span></span> <span data-ttu-id="89395-153">На вкладке **Ресурсы** в разделе **Имя сервера** щелкните ресурс точки доступа клиента правой кнопкой мыши и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="89395-153">On the **Resources** tab, right-click the client access point resource under **Server Name**, and then click **Properties**.</span></span> 

   ![Ресурс IP-адреса](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    <span data-ttu-id="89395-155">c.</span><span class="sxs-lookup"><span data-stu-id="89395-155">c.</span></span> <span data-ttu-id="89395-156">Перейдите на вкладку **Зависимости** .</span><span class="sxs-lookup"><span data-stu-id="89395-156">Click the **Dependencies** tab.</span></span> <span data-ttu-id="89395-157">Убедитесь, что IP-адрес — это зависимость.</span><span class="sxs-lookup"><span data-stu-id="89395-157">Verify that the IP address is a dependency.</span></span> <span data-ttu-id="89395-158">В противном случае укажите IP-адрес в качестве зависимости.</span><span class="sxs-lookup"><span data-stu-id="89395-158">If it is not, set a dependency on the IP address.</span></span> <span data-ttu-id="89395-159">Если в списке несколько ресурсов, убедитесь, что IP-адреса имеют зависимости OR, а не AND.</span><span class="sxs-lookup"><span data-stu-id="89395-159">If there are multiple resources listed, verify that the IP addresses have OR, not AND, dependencies.</span></span> <span data-ttu-id="89395-160">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="89395-160">Click **OK**.</span></span> 

   ![Ресурс IP-адреса](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    <span data-ttu-id="89395-162">г)</span><span class="sxs-lookup"><span data-stu-id="89395-162">d.</span></span> <span data-ttu-id="89395-163">Щелкните правой кнопкой мыши имя прослушивателя, а затем щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="89395-163">Right-click the listener name, and then click **Bring Online**.</span></span> 

    >[!TIP]
    ><span data-ttu-id="89395-164">Вы можете проверить правильность настройки зависимостей.</span><span class="sxs-lookup"><span data-stu-id="89395-164">You can validate that the dependencies are correctly configured.</span></span> <span data-ttu-id="89395-165">В диспетчере отказоустойчивости кластеров перейдите к разделу "Роли", щелкните группу доступности правой кнопкой мыши, затем щелкните **Дополнительные действия** и **Показать отчет о зависимостях**.</span><span class="sxs-lookup"><span data-stu-id="89395-165">In Failover Cluster Manager, go to Roles, right-click the availability group, click **More Actions**, and then click  **Show Dependency Report**.</span></span> <span data-ttu-id="89395-166">Когда зависимости настроены правильно, группа доступности зависит от имени сети, которое, в свою очередь, зависит от IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="89395-166">When the dependencies are correctly configured, the availability group is dependent on the network name, and the network name is dependent on the IP address.</span></span> 


6. <span data-ttu-id="89395-167"><a name="setparam"></a>Настройте параметры кластера в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89395-167"><a name="setparam"></a>Set the cluster parameters in PowerShell.</span></span>
    
    <span data-ttu-id="89395-168">а.</span><span class="sxs-lookup"><span data-stu-id="89395-168">a.</span></span> <span data-ttu-id="89395-169">Скопируйте следующий скрипт PowerShell на один из экземпляров SQL Server.</span><span class="sxs-lookup"><span data-stu-id="89395-169">Copy the following PowerShell script to one of your SQL Server instances.</span></span> <span data-ttu-id="89395-170">Обновите переменные для среды.</span><span class="sxs-lookup"><span data-stu-id="89395-170">Update the variables for your environment.</span></span>     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
    $IPResourceName = "<IPResourceName>" # the IP Address resource name
    $ILBIP = “<n.n.n.n>” # the IP Address of the Internal Load Balancer (ILB). This is the static IP address for the load balancer you configured in the Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    <span data-ttu-id="89395-171">b.</span><span class="sxs-lookup"><span data-stu-id="89395-171">b.</span></span> <span data-ttu-id="89395-172">Задайте параметры кластера, выполнив скрипт PowerShell на одном из узлов кластера.</span><span class="sxs-lookup"><span data-stu-id="89395-172">Set the cluster parameters by running the PowerShell script on one of the cluster nodes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="89395-173">Если экземпляры SQL Server находятся в разных регионах, необходимо дважды запустить сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89395-173">If your SQL Server instances are in separate regions, you need to run the PowerShell script twice.</span></span> <span data-ttu-id="89395-174">При первом запуске используйте значения `$ILBIP` и `$ProbePort` из первого региона.</span><span class="sxs-lookup"><span data-stu-id="89395-174">The first time, use the `$ILBIP` and `$ProbePort` from the first region.</span></span> <span data-ttu-id="89395-175">При втором запуске используйте значения `$ILBIP` и `$ProbePort` из второго региона.</span><span class="sxs-lookup"><span data-stu-id="89395-175">The second time, use the `$ILBIP` and `$ProbePort` from the second region.</span></span> <span data-ttu-id="89395-176">Сетевое имя кластера и имя ресурса IP-адреса кластера совпадают.</span><span class="sxs-lookup"><span data-stu-id="89395-176">The cluster network name and the cluster IP resource name are the same.</span></span> 
