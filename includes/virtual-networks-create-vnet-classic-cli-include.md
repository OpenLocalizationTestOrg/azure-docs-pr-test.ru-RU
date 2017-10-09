## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a><span data-ttu-id="28b49-101">Как toocreate классической виртуальной сети, с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="28b49-101">How toocreate a classic VNet using Azure CLI</span></span>
<span data-ttu-id="28b49-102">Можно использовать toomanage hello Azure CLI из командной строки hello с любого компьютера под управлением Windows, Linux или OSX ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="28b49-102">You can use hello Azure CLI toomanage your Azure resources from hello command prompt from any computer running Windows, Linux, or OSX.</span></span> <span data-ttu-id="28b49-103">toocreate виртуальной сети с помощью hello Azure CLI, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="28b49-103">toocreate a VNet by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="28b49-104">Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../articles/cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="28b49-104">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../articles/cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="28b49-105">Запустите hello **Создание виртуальной сети azure сети** команды toocreate виртуальную сеть и подсеть, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="28b49-105">Run hello **azure network vnet create** command toocreate a VNet and a subnet, as shown below.</span></span> <span data-ttu-id="28b49-106">Список Hello отображаться после вывода hello объясняется hello параметров, используемых.</span><span class="sxs-lookup"><span data-stu-id="28b49-106">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    <span data-ttu-id="28b49-107">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="28b49-107">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * <span data-ttu-id="28b49-108">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="28b49-108">**--vnet**.</span></span> <span data-ttu-id="28b49-109">Имя создания toobe виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="28b49-109">Name of hello VNet toobe created.</span></span> <span data-ttu-id="28b49-110">В данном сценарии это *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="28b49-110">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="28b49-111">**-e (или --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="28b49-111">**-e (or --address-space)**.</span></span> <span data-ttu-id="28b49-112">Адресное пространство виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="28b49-112">VNet address space.</span></span> <span data-ttu-id="28b49-113">В данном сценарии это *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="28b49-113">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="28b49-114">**-i (или -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="28b49-114">**-i (or -cidr)**.</span></span> <span data-ttu-id="28b49-115">Маска подсети в формате CIDR.</span><span class="sxs-lookup"><span data-stu-id="28b49-115">Network mask in CIDR format.</span></span> <span data-ttu-id="28b49-116">В данном сценарии это *16*.</span><span class="sxs-lookup"><span data-stu-id="28b49-116">For our scenario, *16*.</span></span>
   * <span data-ttu-id="28b49-117">**-n (или --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="28b49-117">**-n (or --subnet-name**).</span></span> <span data-ttu-id="28b49-118">Имя первой подсети hello.</span><span class="sxs-lookup"><span data-stu-id="28b49-118">Name of hello first subnet.</span></span> <span data-ttu-id="28b49-119">В данном сценарии это *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="28b49-119">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="28b49-120">**-p (или --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="28b49-120">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="28b49-121">Начальный IP-адрес для подсети или адресное пространство подсети.</span><span class="sxs-lookup"><span data-stu-id="28b49-121">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="28b49-122">В нашем сценарии это *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="28b49-122">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="28b49-123">**-r (или --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="28b49-123">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="28b49-124">Маска подсети в формате CIDR для подсети.</span><span class="sxs-lookup"><span data-stu-id="28b49-124">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="28b49-125">В данном сценарии это *24*.</span><span class="sxs-lookup"><span data-stu-id="28b49-125">For our scenario, *24*.</span></span>
   * <span data-ttu-id="28b49-126">**-l (или --location)**.</span><span class="sxs-lookup"><span data-stu-id="28b49-126">**-l (or --location)**.</span></span> <span data-ttu-id="28b49-127">Регион Azure, где будут создаваться hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="28b49-127">Azure region where hello VNet will be created.</span></span> <span data-ttu-id="28b49-128">В данном сценарии это *Central US*.</span><span class="sxs-lookup"><span data-stu-id="28b49-128">For our scenario, *Central US*.</span></span>
3. <span data-ttu-id="28b49-129">Запустите hello **создать подсеть виртуальной сети azure сети** toocreate команда подсеть, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="28b49-129">Run hello **azure network vnet subnet create** command toocreate a subnet as shown below.</span></span> <span data-ttu-id="28b49-130">Список Hello отображаться после вывода hello объясняется hello параметров, используемых.</span><span class="sxs-lookup"><span data-stu-id="28b49-130">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    <span data-ttu-id="28b49-131">Вот hello ожидается выходных данных для приведенных выше команд hello.</span><span class="sxs-lookup"><span data-stu-id="28b49-131">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * <span data-ttu-id="28b49-132">**-t (или --vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="28b49-132">**-t (or --vnet-name**.</span></span> <span data-ttu-id="28b49-133">Имя виртуальной сети, где будут создаваться подсети hello hello.</span><span class="sxs-lookup"><span data-stu-id="28b49-133">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="28b49-134">В данном сценарии это *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="28b49-134">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="28b49-135">**-n (или --name)**.</span><span class="sxs-lookup"><span data-stu-id="28b49-135">**-n (or --name)**.</span></span> <span data-ttu-id="28b49-136">Имя новой подсети hello.</span><span class="sxs-lookup"><span data-stu-id="28b49-136">Name of hello new subnet.</span></span> <span data-ttu-id="28b49-137">В нашем сценарии это *BackEnd*.</span><span class="sxs-lookup"><span data-stu-id="28b49-137">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="28b49-138">**-a (или --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="28b49-138">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="28b49-139">Блок подсети CIDR.</span><span class="sxs-lookup"><span data-stu-id="28b49-139">Subnet CIDR block.</span></span> <span data-ttu-id="28b49-140">В данном сценарии это *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="28b49-140">Four our scenario, *192.168.2.0/24*.</span></span>
4. <span data-ttu-id="28b49-141">Запустите hello **Показать виртуальной сети azure сети** команды tooview свойства hello hello новой виртуальной сети, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="28b49-141">Run hello **azure network vnet show** command tooview hello properties of hello new vnet, as shown below.</span></span>
   
            azure network vnet show
   
    <span data-ttu-id="28b49-142">Вот hello ожидается выходных данных для приведенных выше команд hello.</span><span class="sxs-lookup"><span data-stu-id="28b49-142">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
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

