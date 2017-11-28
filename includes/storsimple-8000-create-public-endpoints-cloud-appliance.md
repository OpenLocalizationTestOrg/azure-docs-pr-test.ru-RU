#### <a name="to-create-public-endpoints-on-the-cloud-appliance"></a><span data-ttu-id="79a3e-101">Создание общедоступных конечных точек на облачном устройстве</span><span class="sxs-lookup"><span data-stu-id="79a3e-101">To create public endpoints on the cloud appliance</span></span>

1. <span data-ttu-id="79a3e-102">Войдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="79a3e-102">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="79a3e-103">Перейдите к разделу **Виртуальные машины**, а затем выберите виртуальную машину, которая используется как облачное устройство.</span><span class="sxs-lookup"><span data-stu-id="79a3e-103">Go to **Virtual Machines**, and then select and click the virtual machine that is being used as your cloud appliance.</span></span>
    
3. <span data-ttu-id="79a3e-104">Необходимо создать правило группы безопасности сети (NSG), чтобы управлять исходящим и входящим потоком трафика виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="79a3e-104">You need to create a network security group (NSG) rule to control the flow of traffic in and out of your virtual machine.</span></span> <span data-ttu-id="79a3e-105">Выполните следующие действия, чтобы создать правило NSG.</span><span class="sxs-lookup"><span data-stu-id="79a3e-105">Perform the following steps to create an NSG rule.</span></span>
    1. <span data-ttu-id="79a3e-106">Щелкните **Группа безопасности сети**.</span><span class="sxs-lookup"><span data-stu-id="79a3e-106">Select **Network security group**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. <span data-ttu-id="79a3e-107">Выберите представленную группу безопасности сети по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="79a3e-107">Click the default network security group that is presented.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. <span data-ttu-id="79a3e-108">Выберите **Правила безопасности для входящего трафика**.</span><span class="sxs-lookup"><span data-stu-id="79a3e-108">Select **Inbound security rules**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. <span data-ttu-id="79a3e-109">Щелкните **+ Добавить**, чтобы создать правило безопасности для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="79a3e-109">Click **+ Add** to create an inbound security rule.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        <span data-ttu-id="79a3e-110">В колонке "Добавление правила безопасности для входящего трафика" сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="79a3e-110">In the Add inbound security rule blade:</span></span>

        1. <span data-ttu-id="79a3e-111">В поле **Имя** введите имя конечной точки WinRMHttps.</span><span class="sxs-lookup"><span data-stu-id="79a3e-111">For the **Name**, type the following name for the endpoint: WinRMHttps.</span></span>
        
        2. <span data-ttu-id="79a3e-112">В поле **Приоритет** выберите число меньше 1000 (которое является приоритетом для правила по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="79a3e-112">For the **Priority**, select a number lesser than 1000 (which is the priority for the default rule).</span></span> <span data-ttu-id="79a3e-113">Чем выше значение, тем ниже приоритет.</span><span class="sxs-lookup"><span data-stu-id="79a3e-113">Higher the value, lower the priority.</span></span>

        3. <span data-ttu-id="79a3e-114">Задайте для параметра **Источник** значение **Любой**.</span><span class="sxs-lookup"><span data-stu-id="79a3e-114">Set the **Source** to **Any**.</span></span>

        4. <span data-ttu-id="79a3e-115">В поле **Служба** выберите **WinRM**.</span><span class="sxs-lookup"><span data-stu-id="79a3e-115">For the **Service**, select **WinRM**.</span></span> <span data-ttu-id="79a3e-116">Для параметра **Протокол** автоматически задается значение **TCP**, а для параметра **Диапазон портов** — значение **5986**.</span><span class="sxs-lookup"><span data-stu-id="79a3e-116">The **Protocol** is automatically set to **TCP** and the **Port range** is set to **5986**.</span></span>

        5. <span data-ttu-id="79a3e-117">Нажмите кнопку **ОК**, чтобы создать правило.</span><span class="sxs-lookup"><span data-stu-id="79a3e-117">Click **OK** to create the rule.</span></span>

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. <span data-ttu-id="79a3e-118">Последний шаг — связывание группы безопасности сети с подсетью или определенным сетевым интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="79a3e-118">Your final step is to associate your network security group with a subnet or a specific network interface.</span></span> <span data-ttu-id="79a3e-119">Выполните следующие действия, чтобы связать группу безопасности сети с подсетью.</span><span class="sxs-lookup"><span data-stu-id="79a3e-119">Perform the following steps to associate your network security group with a subnet.</span></span>
    1. <span data-ttu-id="79a3e-120">Выберите **Подсети**.</span><span class="sxs-lookup"><span data-stu-id="79a3e-120">Go to **Subnets**.</span></span>
    2. <span data-ttu-id="79a3e-121">Щелкните **+ Associate** (+ Связать).</span><span class="sxs-lookup"><span data-stu-id="79a3e-121">Click **+ Associate**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. <span data-ttu-id="79a3e-122">Выберите виртуальную сеть, а затем — соответствующую подсеть.</span><span class="sxs-lookup"><span data-stu-id="79a3e-122">Select your virtual network, and then select the appropriate subnet.</span></span>
    4. <span data-ttu-id="79a3e-123">Нажмите кнопку **ОК**, чтобы создать правило.</span><span class="sxs-lookup"><span data-stu-id="79a3e-123">Click **OK** to create the rule.</span></span>

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

<span data-ttu-id="79a3e-124">После создания правила вы можете просмотреть его сведения, чтобы определить общедоступный виртуальный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="79a3e-124">After the rule is created, you can view its details to determine the Public Virtual IP (VIP) address.</span></span> <span data-ttu-id="79a3e-125">Запишите этот адрес.</span><span class="sxs-lookup"><span data-stu-id="79a3e-125">Record this address.</span></span>


