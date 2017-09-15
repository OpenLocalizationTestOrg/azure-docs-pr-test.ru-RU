## <a name="how-to-create-a-classic-vnet-using-azure-cli"></a><span data-ttu-id="e5cb7-101">Создание классической виртуальной сети с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="e5cb7-101">How to create a classic VNet using Azure CLI</span></span>
<span data-ttu-id="e5cb7-102">Интерфейс командной строки Azure можно использовать для управления ресурсами Azure из командной строки с любого компьютера под управлением Windows, Linux или OSX.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-102">You can use the Azure CLI to manage your Azure resources from the command prompt from any computer running Windows, Linux, or OSX.</span></span> <span data-ttu-id="e5cb7-103">Чтобы создать виртуальную сеть с помощью интерфейса командной строки Azure, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-103">To create a VNet by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="e5cb7-104">Если вы еще не пользовались Azure CLI, ознакомьтесь со статьей [Установка и настройка CLI Azure](../articles/cli-install-nodejs.md) и следуйте инструкциям вплоть до выбора учетной записи Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-104">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../articles/cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="e5cb7-105">Выполните команду **azure network vnet create** , чтобы создать виртуальную сеть и подсеть, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-105">Run the **azure network vnet create** command to create a VNet and a subnet, as shown below.</span></span> <span data-ttu-id="e5cb7-106">В списке, который откроется после выполнения команды, будут указаны используемые параметры.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-106">The list shown after the output explains the parameters used.</span></span>
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    <span data-ttu-id="e5cb7-107">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5cb7-107">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * <span data-ttu-id="e5cb7-108">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-108">**--vnet**.</span></span> <span data-ttu-id="e5cb7-109">Имя виртуальной сети, которую нужно будет создать.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-109">Name of the VNet to be created.</span></span> <span data-ttu-id="e5cb7-110">В данном сценарии это *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="e5cb7-110">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="e5cb7-111">**-e (или --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-111">**-e (or --address-space)**.</span></span> <span data-ttu-id="e5cb7-112">Адресное пространство виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-112">VNet address space.</span></span> <span data-ttu-id="e5cb7-113">В данном сценарии это *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="e5cb7-113">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="e5cb7-114">**-i (или -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-114">**-i (or -cidr)**.</span></span> <span data-ttu-id="e5cb7-115">Маска подсети в формате CIDR.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-115">Network mask in CIDR format.</span></span> <span data-ttu-id="e5cb7-116">В данном сценарии это *16*.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-116">For our scenario, *16*.</span></span>
   * <span data-ttu-id="e5cb7-117">**-n (или --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="e5cb7-117">**-n (or --subnet-name**).</span></span> <span data-ttu-id="e5cb7-118">Имя первой подсети.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-118">Name of the first subnet.</span></span> <span data-ttu-id="e5cb7-119">В данном сценарии это *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-119">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="e5cb7-120">**-p (или --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-120">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="e5cb7-121">Начальный IP-адрес для подсети или адресное пространство подсети.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-121">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="e5cb7-122">В нашем сценарии это *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-122">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="e5cb7-123">**-r (или --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-123">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="e5cb7-124">Маска подсети в формате CIDR для подсети.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-124">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="e5cb7-125">В данном сценарии это *24*.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-125">For our scenario, *24*.</span></span>
   * <span data-ttu-id="e5cb7-126">**-l (или --location)**.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-126">**-l (or --location)**.</span></span> <span data-ttu-id="e5cb7-127">Регион Azure, в котором будет создана виртуальная сеть.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-127">Azure region where the VNet will be created.</span></span> <span data-ttu-id="e5cb7-128">В данном сценарии это *Central US*.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-128">For our scenario, *Central US*.</span></span>
3. <span data-ttu-id="e5cb7-129">Выполните команду **azure network vnet subnet create** , чтобы создать подсеть, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-129">Run the **azure network vnet subnet create** command to create a subnet as shown below.</span></span> <span data-ttu-id="e5cb7-130">В списке, который откроется после выполнения команды, будут указаны используемые параметры.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-130">The list shown after the output explains the parameters used.</span></span>
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    <span data-ttu-id="e5cb7-131">Вот результат, ожидаемый для указанной выше команды:</span><span class="sxs-lookup"><span data-stu-id="e5cb7-131">Here is the expected output for the command above:</span></span>
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up the subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * <span data-ttu-id="e5cb7-132">**-t (или --vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-132">**-t (or --vnet-name**.</span></span> <span data-ttu-id="e5cb7-133">Имя виртуальной сети, в которой будет создана подсеть.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-133">Name of the VNet where the subnet will be created.</span></span> <span data-ttu-id="e5cb7-134">В данном сценарии это *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-134">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="e5cb7-135">**-n (или --name)**.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-135">**-n (or --name)**.</span></span> <span data-ttu-id="e5cb7-136">Имя новой подсети.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-136">Name of the new subnet.</span></span> <span data-ttu-id="e5cb7-137">В нашем сценарии это *BackEnd*.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-137">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="e5cb7-138">**-a (или --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-138">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="e5cb7-139">Блок подсети CIDR.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-139">Subnet CIDR block.</span></span> <span data-ttu-id="e5cb7-140">В данном сценарии это *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-140">Four our scenario, *192.168.2.0/24*.</span></span>
4. <span data-ttu-id="e5cb7-141">Выполните команду **azure network vnet show** , как показано ниже, чтобы просмотреть свойства новой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e5cb7-141">Run the **azure network vnet show** command to view the properties of the new vnet, as shown below.</span></span>
   
            azure network vnet show
   
    <span data-ttu-id="e5cb7-142">Вот результат, ожидаемый для указанной выше команды:</span><span class="sxs-lookup"><span data-stu-id="e5cb7-142">Here is the expected output for the command above:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up the virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

