1. <span data-ttu-id="0509d-101">В диспетчере отказоустойчивости кластеров разверните **Роли** и выделите свою группу доступности.</span><span class="sxs-lookup"><span data-stu-id="0509d-101">In Failover Cluster Manager, expand **Roles**, and then highlight your availability group.</span></span>  

2. <span data-ttu-id="0509d-102">На hello **ресурсов** вкладке, щелкните правой кнопкой мыши имя прослушивателя hello и нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="0509d-102">On hello **Resources** tab, right-click hello listener name, and then click **Properties**.</span></span>

3. <span data-ttu-id="0509d-103">Нажмите кнопку hello **зависимости** вкладки. Если несколько ресурсов, убедитесь, что hello IP-адреса имеют или не зависимости.</span><span class="sxs-lookup"><span data-stu-id="0509d-103">Click hello **Dependencies** tab. If multiple resources are listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span>  

4. <span data-ttu-id="0509d-104">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0509d-104">Click **OK**.</span></span>

5. <span data-ttu-id="0509d-105">Щелкните правой кнопкой мыши имя прослушивателя hello и нажмите кнопку **перевести в оперативный режим**.</span><span class="sxs-lookup"><span data-stu-id="0509d-105">Right-click hello listener name, and then click **Bring Online**.</span></span>

6. <span data-ttu-id="0509d-106">После hello прослушивателя находится в оперативном режиме на hello **ресурсов** вкладке, щелкните правой кнопкой мыши группу доступности hello и нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="0509d-106">After hello listener is online, on hello **Resources** tab, right-click hello availability group, and then click **Properties**.</span></span>
   
    ![Настройка группы доступности hello](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. <span data-ttu-id="0509d-108">Создайте зависимость от ресурса имени прослушивателя hello (не hello имя IP-адреса ресурсов), а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0509d-108">Create a dependency on hello listener name resource (not hello IP address resources name), and then click **OK**.</span></span>
   
    ![Добавление зависимости от имени прослушивателя hello](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. <span data-ttu-id="0509d-110">Запустите SQL Server Management Studio и подключитесь toohello первичной реплики.</span><span class="sxs-lookup"><span data-stu-id="0509d-110">Start SQL Server Management Studio, and then connect toohello primary replica.</span></span>

9. <span data-ttu-id="0509d-111">Go слишком**высокий уровень доступности AlwaysOn** > **группы доступности** > **\<AvailabilityGroupName\>**   >  **Прослушиватели группы доступности**.</span><span class="sxs-lookup"><span data-stu-id="0509d-111">Go too**AlwaysOn High Availability** > **Availability Groups** > **\<AvailabilityGroupName\>** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="0509d-112">отображать имя прослушивателя Hello, созданный в диспетчере отказоустойчивости кластеров.</span><span class="sxs-lookup"><span data-stu-id="0509d-112">hello listener name that you created in Failover Cluster Manager should be displayed.</span></span>

10. <span data-ttu-id="0509d-113">Щелкните правой кнопкой мыши имя прослушивателя hello и нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="0509d-113">Right-click hello listener name, and then click **Properties**.</span></span>

11. <span data-ttu-id="0509d-114">В hello **порт** укажите hello номер порта для прослушивателя группы доступности hello $EndpointPort, который использовался ранее с помощью hello (1433 — по умолчанию hello в этом учебнике) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0509d-114">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort that you used earlier (in this tutorial, 1433 was hello default), and then click **OK**.</span></span>

