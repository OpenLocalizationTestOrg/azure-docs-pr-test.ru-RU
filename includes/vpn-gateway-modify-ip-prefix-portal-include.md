### <span data-ttu-id="269d6-101"><a name="noconnection"></a>Изменение префиксов IP-адресов для шлюза локальной сети при отсутствии подключения шлюза</span><span class="sxs-lookup"><span data-stu-id="269d6-101"><a name="noconnection"></a>To modify local network gateway IP address prefixes - no gateway connection</span></span>

#### <a name="to-add-additional-address-prefixes"></a><span data-ttu-id="269d6-102">Чтобы добавить дополнительные префиксы адресов:</span><span class="sxs-lookup"><span data-stu-id="269d6-102">To add additional address prefixes:</span></span>

1. <span data-ttu-id="269d6-103">В ресурсе "Шлюз локальной сети" в разделе **Параметры** щелкните **Конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="269d6-103">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="269d6-104">Добавьте пространство IP-адресов в поле *Добавить дополнительный диапазон адресов*.</span><span class="sxs-lookup"><span data-stu-id="269d6-104">Add the IP address space in the *Add additional address range* box.</span></span>
3. <span data-ttu-id="269d6-105">Нажмите кнопку **Save** (Сохранить), чтобы сохранить настройки.</span><span class="sxs-lookup"><span data-stu-id="269d6-105">Click **Save** to save your settings.</span></span>

#### <a name="to-remove-address-prefixes"></a><span data-ttu-id="269d6-106">Чтобы удалить префиксы адресов, используйте фрагмент кода ниже.</span><span class="sxs-lookup"><span data-stu-id="269d6-106">To remove address prefixes:</span></span>

1. <span data-ttu-id="269d6-107">В ресурсе "Шлюз локальной сети" в разделе **Параметры** щелкните **Конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="269d6-107">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="269d6-108">Нажмите кнопку **...**</span><span class="sxs-lookup"><span data-stu-id="269d6-108">Click the **'...'**</span></span> <span data-ttu-id="269d6-109">в строке с префиксом, который нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="269d6-109">on the line containing the prefix you want to remove.</span></span>
3. <span data-ttu-id="269d6-110">Нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="269d6-110">Click **Remove**.</span></span>
4. <span data-ttu-id="269d6-111">Нажмите кнопку **Save** (Сохранить), чтобы сохранить настройки.</span><span class="sxs-lookup"><span data-stu-id="269d6-111">Click **Save** to save your settings.</span></span>

### <span data-ttu-id="269d6-112"><a name="withconnection"></a>Изменение префиксов IP-адресов для шлюза локальной сети при наличии подключения шлюза</span><span class="sxs-lookup"><span data-stu-id="269d6-112"><a name="withconnection"></a>To modify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="269d6-113">Если шлюз уже подключен и вам нужно добавить или удалить префиксы IP-адресов, указанные для локального сетевого шлюза, выполните приведенные ниже шаги именно в такой последовательности.</span><span class="sxs-lookup"><span data-stu-id="269d6-113">If you have a gateway connection and want to add or remove the IP address prefixes contained in your local network gateway, you need to do the following steps, in order.</span></span> <span data-ttu-id="269d6-114">После этого VPN-подключение будет некоторое время недоступно.</span><span class="sxs-lookup"><span data-stu-id="269d6-114">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="269d6-115">При изменении префиксов IP-адресов не нужно удалять VPN-шлюз.</span><span class="sxs-lookup"><span data-stu-id="269d6-115">When modifying IP address prefixes, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="269d6-116">Необходимо удалить только подключение.</span><span class="sxs-lookup"><span data-stu-id="269d6-116">You only need to remove the connection.</span></span>

#### <a name="1-remove-the-connection"></a><span data-ttu-id="269d6-117">1. Удалите подключение.</span><span class="sxs-lookup"><span data-stu-id="269d6-117">1. Remove the connection.</span></span>

1. <span data-ttu-id="269d6-118">В ресурсе "Шлюз локальной сети" в разделе **Параметры** щелкните **Подключения**.</span><span class="sxs-lookup"><span data-stu-id="269d6-118">On the Local Network Gateway resource, in the **Settings** section, click **Connections**.</span></span>
2. <span data-ttu-id="269d6-119">Нажмите кнопку **...** в строке для каждого подключения, а затем — кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="269d6-119">Click the **...** on the line for each connection, then click **Delete**.</span></span>
3. <span data-ttu-id="269d6-120">Нажмите кнопку **Save** (Сохранить), чтобы сохранить настройки.</span><span class="sxs-lookup"><span data-stu-id="269d6-120">Click **Save** to save your settings.</span></span>

#### <a name="2-modify-the-address-prefixes"></a><span data-ttu-id="269d6-121">2. Изменение префиксов адресов.</span><span class="sxs-lookup"><span data-stu-id="269d6-121">2. Modify the address prefixes.</span></span>

<span data-ttu-id="269d6-122">Чтобы добавить дополнительные префиксы адресов:</span><span class="sxs-lookup"><span data-stu-id="269d6-122">To add additional address prefixes:</span></span>

1. <span data-ttu-id="269d6-123">В ресурсе "Шлюз локальной сети" в разделе **Параметры** щелкните **Конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="269d6-123">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="269d6-124">Добавьте пространство IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="269d6-124">Add the IP address space.</span></span>
3. <span data-ttu-id="269d6-125">Нажмите кнопку **Save** (Сохранить), чтобы сохранить настройки.</span><span class="sxs-lookup"><span data-stu-id="269d6-125">Click **Save** to save your settings.</span></span>

<span data-ttu-id="269d6-126">Чтобы удалить префиксы адресов, используйте фрагмент кода ниже.</span><span class="sxs-lookup"><span data-stu-id="269d6-126">To remove address prefixes:</span></span>

1. <span data-ttu-id="269d6-127">В ресурсе "Шлюз локальной сети" в разделе **Параметры** щелкните **Конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="269d6-127">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="269d6-128">Нажмите кнопку **...** в строке с префиксом, который нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="269d6-128">Click the **...** on the line containing the prefix you want to remove.</span></span>
3. <span data-ttu-id="269d6-129">Нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="269d6-129">Click **Remove**.</span></span>
4. <span data-ttu-id="269d6-130">Нажмите кнопку **Save** (Сохранить), чтобы сохранить настройки.</span><span class="sxs-lookup"><span data-stu-id="269d6-130">Click **Save** to save your settings.</span></span>

#### <a name="3-recreate-the-connection"></a><span data-ttu-id="269d6-131">3. Повторное создание подключения.</span><span class="sxs-lookup"><span data-stu-id="269d6-131">3. Recreate the connection.</span></span>

1. <span data-ttu-id="269d6-132">Перейдите к шлюзу вашей виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="269d6-132">Navigate to the Virtual Network Gateway for your VNet.</span></span> <span data-ttu-id="269d6-133">(не шлюзу локальной сети).</span><span class="sxs-lookup"><span data-stu-id="269d6-133">(Not the Local Network Gateway.)</span></span>
2. <span data-ttu-id="269d6-134">В ресурсе "Шлюз виртуальной сети" в разделе **Параметры** щелкните **Подключения**.</span><span class="sxs-lookup"><span data-stu-id="269d6-134">On the Virtual Network Gateway, in the **Settings** section, click **Connections**.</span></span>
3. <span data-ttu-id="269d6-135">Щелкните **+Добавить**, чтобы открыть колонку **Добавление подключения**.</span><span class="sxs-lookup"><span data-stu-id="269d6-135">Click the **+ Add** to open the **Add connection** blade.</span></span>
4. <span data-ttu-id="269d6-136">Заново создайте подключение.</span><span class="sxs-lookup"><span data-stu-id="269d6-136">Recreate your connection.</span></span>
5. <span data-ttu-id="269d6-137">Нажмите кнопку **ОК**, чтобы создать подключение.</span><span class="sxs-lookup"><span data-stu-id="269d6-137">Click **OK** to create the connection.</span></span>