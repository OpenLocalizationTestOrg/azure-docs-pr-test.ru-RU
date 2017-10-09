#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a><span data-ttu-id="0a0b1-101">toocreate общедоступные конечные точки в облаке устройстве hello</span><span class="sxs-lookup"><span data-stu-id="0a0b1-101">toocreate public endpoints on hello cloud appliance</span></span>

1. <span data-ttu-id="0a0b1-102">Войдите в систему toohello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-102">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="0a0b1-103">Go слишком**виртуальные машины**, выберите и нажмите кнопку hello виртуальную машину, которая используется как вашим устройством в облаке.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-103">Go too**Virtual Machines**, and then select and click hello virtual machine that is being used as your cloud appliance.</span></span>
    
3. <span data-ttu-id="0a0b1-104">Необходимо toocreate сетевой безопасности группы (NSG) правило toocontrol hello поток трафика и из него виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-104">You need toocreate a network security group (NSG) rule toocontrol hello flow of traffic in and out of your virtual machine.</span></span> <span data-ttu-id="0a0b1-105">Выполните следующие шаги toocreate правило NSG hello.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-105">Perform hello following steps toocreate an NSG rule.</span></span>
    1. <span data-ttu-id="0a0b1-106">Щелкните **Группа безопасности сети**.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-106">Select **Network security group**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. <span data-ttu-id="0a0b1-107">Выберите группы безопасности сети по умолчанию hello, представленные.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-107">Click hello default network security group that is presented.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. <span data-ttu-id="0a0b1-108">Выберите **Правила безопасности для входящего трафика**.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-108">Select **Inbound security rules**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. <span data-ttu-id="0a0b1-109">Нажмите кнопку **+ добавить** toocreate правило безопасности для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-109">Click **+ Add** toocreate an inbound security rule.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        <span data-ttu-id="0a0b1-110">В колонке правила безопасности для входящего трафика добавить hello:</span><span class="sxs-lookup"><span data-stu-id="0a0b1-110">In hello Add inbound security rule blade:</span></span>

        1. <span data-ttu-id="0a0b1-111">Для hello **имя**, hello введите следующее имя для конечной точки hello: WinRMHttps.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-111">For hello **Name**, type hello following name for hello endpoint: WinRMHttps.</span></span>
        
        2. <span data-ttu-id="0a0b1-112">Для hello **приоритет**выберите номер меньше 1000 (hello приоритет для правила по умолчанию hello).</span><span class="sxs-lookup"><span data-stu-id="0a0b1-112">For hello **Priority**, select a number lesser than 1000 (which is hello priority for hello default rule).</span></span> <span data-ttu-id="0a0b1-113">Чем выше значение hello, более низкий приоритет hello.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-113">Higher hello value, lower hello priority.</span></span>

        3. <span data-ttu-id="0a0b1-114">Набор hello **источника** слишком**любой**.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-114">Set hello **Source** too**Any**.</span></span>

        4. <span data-ttu-id="0a0b1-115">Для hello **службы**выберите **WinRM**.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-115">For hello **Service**, select **WinRM**.</span></span> <span data-ttu-id="0a0b1-116">Hello **протокола** автоматически устанавливается слишком**TCP** и hello **диапазон портов** задано слишком**5986**.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-116">hello **Protocol** is automatically set too**TCP** and hello **Port range** is set too**5986**.</span></span>

        5. <span data-ttu-id="0a0b1-117">Нажмите кнопку **ОК** toocreate hello правило.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-117">Click **OK** toocreate hello rule.</span></span>

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. <span data-ttu-id="0a0b1-118">Последняя операция — tooassociate группы безопасности сети с подсетью или определенного сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-118">Your final step is tooassociate your network security group with a subnet or a specific network interface.</span></span> <span data-ttu-id="0a0b1-119">Выполните следующие шаги tooassociate hello сетевой группы безопасности с подсетью.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-119">Perform hello following steps tooassociate your network security group with a subnet.</span></span>
    1. <span data-ttu-id="0a0b1-120">Go слишком**подсети**.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-120">Go too**Subnets**.</span></span>
    2. <span data-ttu-id="0a0b1-121">Щелкните **+ Associate** (+ Связать).</span><span class="sxs-lookup"><span data-stu-id="0a0b1-121">Click **+ Associate**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. <span data-ttu-id="0a0b1-122">Выберите виртуальной сети, а затем выберите соответствующую подсеть hello.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-122">Select your virtual network, and then select hello appropriate subnet.</span></span>
    4. <span data-ttu-id="0a0b1-123">Нажмите кнопку **ОК** toocreate hello правило.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-123">Click **OK** toocreate hello rule.</span></span>

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

<span data-ttu-id="0a0b1-124">После создания правила hello, можно просмотреть его сведения toodetermine hello открытый виртуальный IP-адресов (VIP) адрес.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-124">After hello rule is created, you can view its details toodetermine hello Public Virtual IP (VIP) address.</span></span> <span data-ttu-id="0a0b1-125">Запишите этот адрес.</span><span class="sxs-lookup"><span data-stu-id="0a0b1-125">Record this address.</span></span>


