## <a name="public-ip-address"></a><span data-ttu-id="36deb-101">Общедоступный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="36deb-101">Public IP address</span></span>
<span data-ttu-id="36deb-102">Ресурс общедоступного IP-адреса предоставляет зарезервированный или динамический общедоступный IP-адрес для Интернета.</span><span class="sxs-lookup"><span data-stu-id="36deb-102">A public IP address resource provides either a reserved or dynamic Internet facing IP address.</span></span> <span data-ttu-id="36deb-103">Несмотря на то, что вы сможете создать общедоступный IP-адрес в виде отдельного объекта, необходимо tooassociate его tooactually tooanother объекта используйте адрес hello.</span><span class="sxs-lookup"><span data-stu-id="36deb-103">Although you can create a public IP address as a stand alone object, you need tooassociate it tooanother object tooactually use hello address.</span></span> <span data-ttu-id="36deb-104">Можно связать балансировщик нагрузки tooa открытый IP адрес, шлюз приложений или toothose Сетевых Internet tooprovide доступ к ресурсам.</span><span class="sxs-lookup"><span data-stu-id="36deb-104">You can associate a public IP address tooa load balancer, application  gateway, or a NIC tooprovide Internet access toothose resources.</span></span>  

| <span data-ttu-id="36deb-105">Свойство</span><span class="sxs-lookup"><span data-stu-id="36deb-105">Property</span></span> | <span data-ttu-id="36deb-106">Описание</span><span class="sxs-lookup"><span data-stu-id="36deb-106">Description</span></span> | <span data-ttu-id="36deb-107">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="36deb-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36deb-108">**publicIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="36deb-108">**publicIPAllocationMethod**</span></span> |<span data-ttu-id="36deb-109">Определяет, если IP-адрес hello *статических* или *динамическое*.</span><span class="sxs-lookup"><span data-stu-id="36deb-109">Defines if hello IP address is *static* or *dynamic*.</span></span> |<span data-ttu-id="36deb-110">static, dynamic</span><span class="sxs-lookup"><span data-stu-id="36deb-110">static, dynamic</span></span> |
| <span data-ttu-id="36deb-111">**idleTimeoutInMinutes**</span><span class="sxs-lookup"><span data-stu-id="36deb-111">**idleTimeoutInMinutes**</span></span> |<span data-ttu-id="36deb-112">Определяет hello аут времени бездействия, значение по умолчанию 4 минуты.</span><span class="sxs-lookup"><span data-stu-id="36deb-112">Defines hello idle time out, with a default value of 4 minutes.</span></span> <span data-ttu-id="36deb-113">Если дополнительные пакеты для данного сеанса не получено в течение этого времени, hello сеанс завершен.</span><span class="sxs-lookup"><span data-stu-id="36deb-113">If no more packets for a given session is received within this time, hello session is terminated.</span></span> |<span data-ttu-id="36deb-114">любое значение от 4 до 30</span><span class="sxs-lookup"><span data-stu-id="36deb-114">any value between 4 and 30</span></span> |
| <span data-ttu-id="36deb-115">**ipAddress**</span><span class="sxs-lookup"><span data-stu-id="36deb-115">**ipAddress**</span></span> |<span data-ttu-id="36deb-116">Tooobject назначить IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="36deb-116">IP address assigned tooobject.</span></span> <span data-ttu-id="36deb-117">Это свойство доступно только для чтения.</span><span class="sxs-lookup"><span data-stu-id="36deb-117">This is a read-only property.</span></span> |<span data-ttu-id="36deb-118">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="36deb-118">104.42.233.77</span></span> |

### <a name="dns-settings"></a><span data-ttu-id="36deb-119">Параметры DNS</span><span class="sxs-lookup"><span data-stu-id="36deb-119">DNS settings</span></span>
<span data-ttu-id="36deb-120">Общедоступные IP-адреса иметь дочерний объект с именем **dnsSettings** содержащий hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="36deb-120">Public IP addresses have a child object named **dnsSettings** containing hello following properties:</span></span>

| <span data-ttu-id="36deb-121">Свойство</span><span class="sxs-lookup"><span data-stu-id="36deb-121">Property</span></span> | <span data-ttu-id="36deb-122">Описание</span><span class="sxs-lookup"><span data-stu-id="36deb-122">Description</span></span> | <span data-ttu-id="36deb-123">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="36deb-123">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36deb-124">**domainNameLabel**</span><span class="sxs-lookup"><span data-stu-id="36deb-124">**domainNameLabel**</span></span> |<span data-ttu-id="36deb-125">Узел для разрешения имен.</span><span class="sxs-lookup"><span data-stu-id="36deb-125">Host named used for name resolution.</span></span> |<span data-ttu-id="36deb-126">www, ftp, vm1</span><span class="sxs-lookup"><span data-stu-id="36deb-126">www, ftp, vm1</span></span> |
| <span data-ttu-id="36deb-127">**fqdn**</span><span class="sxs-lookup"><span data-stu-id="36deb-127">**fqdn**</span></span> |<span data-ttu-id="36deb-128">Полное имя для hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="36deb-128">Fully qualified name for hello public IP.</span></span> |<span data-ttu-id="36deb-129">www.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="36deb-129">www.westus.cloudapp.azure.com</span></span> |
| <span data-ttu-id="36deb-130">**reverseFqdn**</span><span class="sxs-lookup"><span data-stu-id="36deb-130">**reverseFqdn**</span></span> |<span data-ttu-id="36deb-131">Полное доменное имя, которое разрешает toohello IP-адрес и зарегистрирован в DNS, как запись PTR.</span><span class="sxs-lookup"><span data-stu-id="36deb-131">Fully qualified domain name that resolves toohello IP address and is registered in DNS as a PTR record.</span></span> |<span data-ttu-id="36deb-132">www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="36deb-132">www.contoso.com.</span></span> |

<span data-ttu-id="36deb-133">Пример общедоступного IP-адреса в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="36deb-133">Sample public IP address in JSON format:</span></span>

    {
       "name": "PIP01",
       "location": "North US",
       "tags": { "key": "value" },
       "properties": {
          "publicIPAllocationMethod": "Static",
          "idleTimeoutInMinutes": 4,
          "ipAddress": "104.42.233.77",
          "dnsSettings": {
             "domainNameLabel": "mylabel",
             "fqdn": "mylabel.westus.cloudapp.azure.com",
             "reverseFqdn": "contoso.com."
          }
       }
    } 

### <a name="additional-resources"></a><span data-ttu-id="36deb-134">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="36deb-134">Additional resources</span></span>
* <span data-ttu-id="36deb-135">См. дополнительные сведения об [общедоступных IP-адресах](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="36deb-135">Get more information about [public IP addresses](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span></span>
* <span data-ttu-id="36deb-136">Узнайте об [общедоступных IP-адресах уровня экземпляра](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="36deb-136">Learn about [instance level public IP addresses](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span></span>
* <span data-ttu-id="36deb-137">Чтение hello [справочной документации REST API](https://msdn.microsoft.com/library/azure/mt163638.aspx) для открытого IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="36deb-137">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163638.aspx) for public IP addresses.</span></span>

