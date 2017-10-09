### <span data-ttu-id="d9759-101"><a name="noconnection"></a>toomodify локальной сети шлюза префиксов IP-адресов — подключение к шлюзу</span><span class="sxs-lookup"><span data-stu-id="d9759-101"><a name="noconnection"></a>toomodify local network gateway IP address prefixes - no gateway connection</span></span>

#### <a name="tooadd-additional-address-prefixes"></a><span data-ttu-id="d9759-102">префиксы tooadd дополнительный адрес:</span><span class="sxs-lookup"><span data-stu-id="d9759-102">tooadd additional address prefixes:</span></span>

1. <span data-ttu-id="d9759-103">На hello ресурса шлюза локальной сети в hello **параметры** щелкните **конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="d9759-103">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="d9759-104">Добавьте пространство IP-адресов hello в hello *добавить дополнительный диапазон адресов* поле.</span><span class="sxs-lookup"><span data-stu-id="d9759-104">Add hello IP address space in hello *Add additional address range* box.</span></span>
3. <span data-ttu-id="d9759-105">Нажмите кнопку **Сохранить** toosave параметры.</span><span class="sxs-lookup"><span data-stu-id="d9759-105">Click **Save** toosave your settings.</span></span>

#### <a name="tooremove-address-prefixes"></a><span data-ttu-id="d9759-106">tooremove префиксы адресов:</span><span class="sxs-lookup"><span data-stu-id="d9759-106">tooremove address prefixes:</span></span>

1. <span data-ttu-id="d9759-107">На hello ресурса шлюза локальной сети в hello **параметры** щелкните **конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="d9759-107">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="d9759-108">Нажмите кнопку hello **«...»** hello строке, содержащей префикс hello требуется tooremove.</span><span class="sxs-lookup"><span data-stu-id="d9759-108">Click hello **'...'** on hello line containing hello prefix you want tooremove.</span></span>
3. <span data-ttu-id="d9759-109">Нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="d9759-109">Click **Remove**.</span></span>
4. <span data-ttu-id="d9759-110">Нажмите кнопку **Сохранить** toosave параметры.</span><span class="sxs-lookup"><span data-stu-id="d9759-110">Click **Save** toosave your settings.</span></span>

### <span data-ttu-id="d9759-111"><a name="withconnection"></a>toomodify локальной сети шлюза префиксов IP-адресов — существующие подключения шлюза</span><span class="sxs-lookup"><span data-stu-id="d9759-111"><a name="withconnection"></a>toomodify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="d9759-112">Если после подключения шлюза и хотите tooadd или префиксов IP-адресов hello, содержащихся в шлюз локальной сети, необходимо hello toodo следующие шаги в порядке.</span><span class="sxs-lookup"><span data-stu-id="d9759-112">If you have a gateway connection and want tooadd or remove hello IP address prefixes contained in your local network gateway, you need toodo hello following steps, in order.</span></span> <span data-ttu-id="d9759-113">После этого VPN-подключение будет некоторое время недоступно.</span><span class="sxs-lookup"><span data-stu-id="d9759-113">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="d9759-114">При изменении префиксов IP-адресов, не требуется toodelete hello VPN-шлюз.</span><span class="sxs-lookup"><span data-stu-id="d9759-114">When modifying IP address prefixes, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="d9759-115">Необходимо только подключение tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="d9759-115">You only need tooremove hello connection.</span></span>

#### <a name="1-remove-hello-connection"></a><span data-ttu-id="d9759-116">1. Удалите подключение hello.</span><span class="sxs-lookup"><span data-stu-id="d9759-116">1. Remove hello connection.</span></span>

1. <span data-ttu-id="d9759-117">На hello ресурса шлюза локальной сети в hello **параметры** щелкните **подключения**.</span><span class="sxs-lookup"><span data-stu-id="d9759-117">On hello Local Network Gateway resource, in hello **Settings** section, click **Connections**.</span></span>
2. <span data-ttu-id="d9759-118">Нажмите кнопку hello **...**  hello строке для каждого соединения, нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="d9759-118">Click hello **...** on hello line for each connection, then click **Delete**.</span></span>
3. <span data-ttu-id="d9759-119">Нажмите кнопку **Сохранить** toosave параметры.</span><span class="sxs-lookup"><span data-stu-id="d9759-119">Click **Save** toosave your settings.</span></span>

#### <a name="2-modify-hello-address-prefixes"></a><span data-ttu-id="d9759-120">2. Измените префиксы адресов hello.</span><span class="sxs-lookup"><span data-stu-id="d9759-120">2. Modify hello address prefixes.</span></span>

<span data-ttu-id="d9759-121">префиксы tooadd дополнительный адрес:</span><span class="sxs-lookup"><span data-stu-id="d9759-121">tooadd additional address prefixes:</span></span>

1. <span data-ttu-id="d9759-122">На hello ресурса шлюза локальной сети в hello **параметры** щелкните **конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="d9759-122">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="d9759-123">Добавьте hello пространство IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="d9759-123">Add hello IP address space.</span></span>
3. <span data-ttu-id="d9759-124">Нажмите кнопку **Сохранить** toosave параметры.</span><span class="sxs-lookup"><span data-stu-id="d9759-124">Click **Save** toosave your settings.</span></span>

<span data-ttu-id="d9759-125">tooremove префиксы адресов:</span><span class="sxs-lookup"><span data-stu-id="d9759-125">tooremove address prefixes:</span></span>

1. <span data-ttu-id="d9759-126">На hello ресурса шлюза локальной сети в hello **параметры** щелкните **конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="d9759-126">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="d9759-127">Нажмите кнопку hello **...**  hello строке, содержащей префикс hello требуется tooremove.</span><span class="sxs-lookup"><span data-stu-id="d9759-127">Click hello **...** on hello line containing hello prefix you want tooremove.</span></span>
3. <span data-ttu-id="d9759-128">Нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="d9759-128">Click **Remove**.</span></span>
4. <span data-ttu-id="d9759-129">Нажмите кнопку **Сохранить** toosave параметры.</span><span class="sxs-lookup"><span data-stu-id="d9759-129">Click **Save** toosave your settings.</span></span>

#### <a name="3-recreate-hello-connection"></a><span data-ttu-id="d9759-130">3. Повторно создайте подключение hello.</span><span class="sxs-lookup"><span data-stu-id="d9759-130">3. Recreate hello connection.</span></span>

1. <span data-ttu-id="d9759-131">Перейдите toohello шлюза виртуальной сети для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="d9759-131">Navigate toohello Virtual Network Gateway for your VNet.</span></span> <span data-ttu-id="d9759-132">(Не hello шлюза локальной сети.)</span><span class="sxs-lookup"><span data-stu-id="d9759-132">(Not hello Local Network Gateway.)</span></span>
2. <span data-ttu-id="d9759-133">На hello шлюза виртуальной сети в hello **параметры** щелкните **подключения**.</span><span class="sxs-lookup"><span data-stu-id="d9759-133">On hello Virtual Network Gateway, in hello **Settings** section, click **Connections**.</span></span>
3. <span data-ttu-id="d9759-134">Нажмите кнопку hello **+ добавить** tooopen hello **добавить подключение** колонку.</span><span class="sxs-lookup"><span data-stu-id="d9759-134">Click hello **+ Add** tooopen hello **Add connection** blade.</span></span>
4. <span data-ttu-id="d9759-135">Заново создайте подключение.</span><span class="sxs-lookup"><span data-stu-id="d9759-135">Recreate your connection.</span></span>
5. <span data-ttu-id="d9759-136">Нажмите кнопку **ОК** toocreate hello соединения.</span><span class="sxs-lookup"><span data-stu-id="d9759-136">Click **OK** toocreate hello connection.</span></span>
