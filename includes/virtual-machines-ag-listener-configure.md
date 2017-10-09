<span data-ttu-id="5e7d3-101">прослушиватель группы доступности Hello — IP-адресом и сетевым имя, hello SQL Server прослушивает группы доступности.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-101">hello availability group listener is an IP address and network name that hello SQL Server availability group listens on.</span></span> <span data-ttu-id="5e7d3-102">прослушиватель группы доступности hello toocreate hello следующие:</span><span class="sxs-lookup"><span data-stu-id="5e7d3-102">toocreate hello availability group listener, do hello following:</span></span>

1. <span data-ttu-id="5e7d3-103"><a name="getnet"></a>Получите имя сетевого ресурса кластера hello hello.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-103"><a name="getnet"></a>Get hello name of hello cluster network resource.</span></span>

    <span data-ttu-id="5e7d3-104">а.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-104">a.</span></span> <span data-ttu-id="5e7d3-105">С помощью протокола удаленного рабочего СТОЛА tooconnect toohello виртуальную машину Azure, на котором размещена первичная реплика hello.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-105">Use RDP tooconnect toohello Azure virtual machine that hosts hello primary replica.</span></span> 

    <span data-ttu-id="5e7d3-106">b.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-106">b.</span></span> <span data-ttu-id="5e7d3-107">Откройте диспетчер отказоустойчивости кластеров.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-107">Open Failover Cluster Manager.</span></span>

    <span data-ttu-id="5e7d3-108">c.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-108">c.</span></span> <span data-ttu-id="5e7d3-109">Выберите hello **сетей** узла и сетевое имя кластера Примечание hello.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-109">Select hello **Networks** node, and note hello cluster network name.</span></span> <span data-ttu-id="5e7d3-110">Используйте это имя в hello `$ClusterNetworkName` переменной в hello сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-110">Use this name in hello `$ClusterNetworkName` variable in hello PowerShell script.</span></span> <span data-ttu-id="5e7d3-111">В hello за сетевое имя кластера hello изображения следует **сети кластера 1**:</span><span class="sxs-lookup"><span data-stu-id="5e7d3-111">In hello following image hello cluster network name is **Cluster Network 1**:</span></span>

   ![Сетевое имя кластера](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <span data-ttu-id="5e7d3-113"><a name="addcap"></a>Добавление клиентской точки доступа hello.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-113"><a name="addcap"></a>Add hello client access point.</span></span>  
    <span data-ttu-id="5e7d3-114">точка доступа клиента Hello — hello сетевого имени, который используется приложениями баз данных toohello tooconnect в группе доступности.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-114">hello client access point is hello network name that applications use tooconnect toohello databases in an availability group.</span></span> <span data-ttu-id="5e7d3-115">Создайте точку доступа клиента hello в диспетчере отказоустойчивости кластеров.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-115">Create hello client access point in Failover Cluster Manager.</span></span>

    <span data-ttu-id="5e7d3-116">а.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-116">a.</span></span> <span data-ttu-id="5e7d3-117">Разверните имя кластера hello и щелкните **ролей**.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-117">Expand hello cluster name, and then click **Roles**.</span></span>

    <span data-ttu-id="5e7d3-118">b.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-118">b.</span></span> <span data-ttu-id="5e7d3-119">В hello **ролей** панели, щелкните правой кнопкой мыши группу доступности hello имя, а затем выберите **добавить ресурс** > **точки доступа клиента**.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-119">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>

   ![Точка доступа клиента](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    <span data-ttu-id="5e7d3-121">c.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-121">c.</span></span> <span data-ttu-id="5e7d3-122">В hello **имя** Создайте имя для этого нового прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-122">In hello **Name** box, create a name for this new listener.</span></span> 
   <span data-ttu-id="5e7d3-123">Hello для hello новый прослушиватель имеет имя hello сетевого имени, который используется приложениями tooconnect toodatabases в группе доступности SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-123">hello name for hello new listener is hello network name that applications use tooconnect toodatabases in hello SQL Server availability group.</span></span>
   
    <span data-ttu-id="5e7d3-124">d.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-124">d.</span></span> <span data-ttu-id="5e7d3-125">toofinish при создании прослушивателя hello, нажмите кнопку **Далее** дважды, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-125">toofinish creating hello listener, click **Next** twice, and then click **Finish**.</span></span> <span data-ttu-id="5e7d3-126">Не следует переводить прослушиватель hello или ресурс в оперативный режим на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-126">Do not bring hello listener or resource online at this point.</span></span>

3. <span data-ttu-id="5e7d3-127"><a name="congroup"></a>Настройте hello IP-ресурс для группы доступности hello.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-127"><a name="congroup"></a>Configure hello IP resource for hello availability group.</span></span>

    <span data-ttu-id="5e7d3-128">а.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-128">a.</span></span> <span data-ttu-id="5e7d3-129">Нажмите кнопку hello **ресурсов** вкладку, а затем раскройте точку доступа клиента hello, вы создали.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-129">Click hello **Resources** tab, and then expand hello client access point you created.</span></span>  
    <span data-ttu-id="5e7d3-130">точка доступа клиента Hello находится в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-130">hello client access point is offline.</span></span>

   ![Точка доступа клиента](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    <span data-ttu-id="5e7d3-132">b.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-132">b.</span></span> <span data-ttu-id="5e7d3-133">Щелкните правой кнопкой мыши hello IP-ресурс и выберите пункт Свойства.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-133">Right-click hello IP resource, and then click properties.</span></span> <span data-ttu-id="5e7d3-134">Запишите имя hello hello IP-адрес и использовать его в hello `$IPResourceName` переменной в hello сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-134">Note hello name of hello IP address, and use it in hello `$IPResourceName` variable in hello PowerShell script.</span></span>

    <span data-ttu-id="5e7d3-135">c.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-135">c.</span></span> <span data-ttu-id="5e7d3-136">В разделе **IP-адрес** выберите параметр **Статический IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-136">Under **IP Address**, click **Static IP Address**.</span></span> <span data-ttu-id="5e7d3-137">Задать hello IP-адрес как hello же адрес используется при установке hello адрес подсистемы балансировки нагрузки для hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-137">Set hello IP address as hello same address that you used when you set hello load balancer address on hello Azure portal.</span></span>

   ![Ресурс IP-адреса](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <span data-ttu-id="5e7d3-139"><a name = "dependencyGroup"></a>Зависеть ресурс группы доступности SQL Server hello hello клиентской точки доступа.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-139"><a name = "dependencyGroup"></a>Make hello SQL Server availability group resource dependent on hello client access point.</span></span>

    <span data-ttu-id="5e7d3-140">а.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-140">a.</span></span> <span data-ttu-id="5e7d3-141">В диспетчере отказоустойчивости кластеров щелкните **Роли** и выберите группу доступности.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-141">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span>

    <span data-ttu-id="5e7d3-142">b.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-142">b.</span></span> <span data-ttu-id="5e7d3-143">На hello **ресурсов** в разделе **другие ресурсы**, щелкните правой кнопкой мыши группу ресурсов доступности hello и нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-143">On hello **Resources** tab, under **Other Resources**, right-click hello availability resource group, and then click **Properties**.</span></span> 

    <span data-ttu-id="5e7d3-144">c.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-144">c.</span></span> <span data-ttu-id="5e7d3-145">На вкладке зависимости hello добавьте имя hello ресурса точек (прослушиватель hello) hello клиентского доступа.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-145">On hello dependencies tab, add hello name of hello client access point (hello listener) resource.</span></span>

   ![Ресурс IP-адреса](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    <span data-ttu-id="5e7d3-147">г)</span><span class="sxs-lookup"><span data-stu-id="5e7d3-147">d.</span></span> <span data-ttu-id="5e7d3-148">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-148">Click **OK**.</span></span>

5. <span data-ttu-id="5e7d3-149"><a name="listname"></a>Сделать hello клиентского доступа точки ресурса, зависящее от hello IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-149"><a name="listname"></a>Make hello client access point resource dependent on hello IP address.</span></span>

    <span data-ttu-id="5e7d3-150">а.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-150">a.</span></span> <span data-ttu-id="5e7d3-151">В диспетчере отказоустойчивости кластеров щелкните **Роли** и выберите группу доступности.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-151">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span> 

    <span data-ttu-id="5e7d3-152">b.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-152">b.</span></span> <span data-ttu-id="5e7d3-153">На hello **ресурсов** щелкните правой кнопкой мыши ресурс точки доступа клиента hello в **имя сервера**, а затем нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-153">On hello **Resources** tab, right-click hello client access point resource under **Server Name**, and then click **Properties**.</span></span> 

   ![Ресурс IP-адреса](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    <span data-ttu-id="5e7d3-155">c.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-155">c.</span></span> <span data-ttu-id="5e7d3-156">Нажмите кнопку hello **зависимости** вкладки. Убедитесь, что IP-адрес hello зависимость.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-156">Click hello **Dependencies** tab. Verify that hello IP address is a dependency.</span></span> <span data-ttu-id="5e7d3-157">Если это не так, задайте зависимость hello IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-157">If it is not, set a dependency on hello IP address.</span></span> <span data-ttu-id="5e7d3-158">Если перечислено несколько ресурсов, убедитесь, что hello IP-адреса имеют или не зависимости.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-158">If there are multiple resources listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span> <span data-ttu-id="5e7d3-159">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-159">Click **OK**.</span></span> 

   ![Ресурс IP-адреса](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    <span data-ttu-id="5e7d3-161">d.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-161">d.</span></span> <span data-ttu-id="5e7d3-162">Щелкните правой кнопкой мыши имя прослушивателя hello и нажмите кнопку **перевести в оперативный режим**.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-162">Right-click hello listener name, and then click **Bring Online**.</span></span> 

    >[!TIP]
    ><span data-ttu-id="5e7d3-163">Можно проверить правильность настройки зависимостей, приветствия.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-163">You can validate that hello dependencies are correctly configured.</span></span> <span data-ttu-id="5e7d3-164">TooRoles перейдите в Диспетчер отказоустойчивости кластеров, щелкните правой кнопкой мыши группу доступности hello, нажмите кнопку **дополнительные действия**, а затем нажмите кнопку **Показать отчет о зависимостях**.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-164">In Failover Cluster Manager, go tooRoles, right-click hello availability group, click **More Actions**, and then click  **Show Dependency Report**.</span></span> <span data-ttu-id="5e7d3-165">Если зависимости hello правильно настроены, hello группы доступности определяется hello сетевое имя и hello сетевого имени зависит от hello IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-165">When hello dependencies are correctly configured, hello availability group is dependent on hello network name, and hello network name is dependent on hello IP address.</span></span> 


6. <span data-ttu-id="5e7d3-166"><a name="setparam"></a>Настроить параметры кластера hello в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-166"><a name="setparam"></a>Set hello cluster parameters in PowerShell.</span></span>
    
    <span data-ttu-id="5e7d3-167">а.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-167">a.</span></span> <span data-ttu-id="5e7d3-168">Скопируйте hello, следуя tooone сценария PowerShell в экземплярах SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-168">Copy hello following PowerShell script tooone of your SQL Server instances.</span></span> <span data-ttu-id="5e7d3-169">Обновите hello переменные среды.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-169">Update hello variables for your environment.</span></span>     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    <span data-ttu-id="5e7d3-170">b.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-170">b.</span></span> <span data-ttu-id="5e7d3-171">Задайте параметры кластера hello, выполнив hello сценарий PowerShell на одном из узлов кластера hello.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-171">Set hello cluster parameters by running hello PowerShell script on one of hello cluster nodes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="5e7d3-172">Если экземпляры SQL Server находятся в отдельных регионах, требуется сценарий PowerShell toorun hello дважды.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-172">If your SQL Server instances are in separate regions, you need toorun hello PowerShell script twice.</span></span> <span data-ttu-id="5e7d3-173">Здравствуйте, первый раз, использовать hello `$ILBIP` и `$ProbePort` из первой области hello.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-173">hello first time, use hello `$ILBIP` and `$ProbePort` from hello first region.</span></span> <span data-ttu-id="5e7d3-174">Здравствуйте, второй раз, использовать hello `$ILBIP` и `$ProbePort` из второй области hello.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-174">hello second time, use hello `$ILBIP` and `$ProbePort` from hello second region.</span></span> <span data-ttu-id="5e7d3-175">сетевое имя кластера Hello и имя ресурса IP кластера hello hello же.</span><span class="sxs-lookup"><span data-stu-id="5e7d3-175">hello cluster network name and hello cluster IP resource name are hello same.</span></span> 
