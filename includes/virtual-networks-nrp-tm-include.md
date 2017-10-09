## <a name="traffic-manager-profile"></a><span data-ttu-id="b339c-101">Профиль диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="b339c-101">Traffic Manager Profile</span></span>
<span data-ttu-id="b339c-102">Диспетчер трафика и его дочерних ресурса конечной точки включить tooendpoints по DNS в Azure и за пределами Azure.</span><span class="sxs-lookup"><span data-stu-id="b339c-102">Traffic manager and its child endpoint resource enable DNS routing tooendpoints in Azure and outside of Azure.</span></span> <span data-ttu-id="b339c-103">Такое распределение трафика регулируется с помощью политик.</span><span class="sxs-lookup"><span data-stu-id="b339c-103">Such traffic distribution is governed by routing  policy methods.</span></span> <span data-ttu-id="b339c-104">Диспетчер трафика также позволяет отслеживать toobe работоспособности конечной точки и трафика, соответствующим образом распространяется на основе hello работоспособности конечной точки.</span><span class="sxs-lookup"><span data-stu-id="b339c-104">Traffic manager also allows endpoint health toobe monitored, and traffic diverted appropriately based on hello health of an endpoint.</span></span> 

| <span data-ttu-id="b339c-105">Свойство</span><span class="sxs-lookup"><span data-stu-id="b339c-105">Property</span></span> | <span data-ttu-id="b339c-106">Описание</span><span class="sxs-lookup"><span data-stu-id="b339c-106">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b339c-107">**trafficRoutingMethod**</span><span class="sxs-lookup"><span data-stu-id="b339c-107">**trafficRoutingMethod**</span></span> |<span data-ttu-id="b339c-108">Возможные значения: *Performance* (производительный), *Weighted* (взвешенный) и *Priority* (приоритетный).</span><span class="sxs-lookup"><span data-stu-id="b339c-108">possible values are *Performance*, *Weighted*, and *Priority*</span></span> |
| <span data-ttu-id="b339c-109">**dnsConfig**</span><span class="sxs-lookup"><span data-stu-id="b339c-109">**dnsConfig**</span></span> |<span data-ttu-id="b339c-110">Полное доменное имя для профиля hello</span><span class="sxs-lookup"><span data-stu-id="b339c-110">FQDN for hello profile</span></span> |
| <span data-ttu-id="b339c-111">**Протокол**</span><span class="sxs-lookup"><span data-stu-id="b339c-111">**Protocol**</span></span> |<span data-ttu-id="b339c-112">Протокол мониторинга. Возможные значения: *HTTP* и *HTTPS*.</span><span class="sxs-lookup"><span data-stu-id="b339c-112">monitoring protocol, possible values are *HTTP* and *HTTPS*</span></span> |
| <span data-ttu-id="b339c-113">**Порт**</span><span class="sxs-lookup"><span data-stu-id="b339c-113">**Port**</span></span> |<span data-ttu-id="b339c-114">порт мониторинга</span><span class="sxs-lookup"><span data-stu-id="b339c-114">monitoring port</span></span> |
| <span data-ttu-id="b339c-115">**Путь**</span><span class="sxs-lookup"><span data-stu-id="b339c-115">**Path**</span></span> |<span data-ttu-id="b339c-116">путь мониторинга</span><span class="sxs-lookup"><span data-stu-id="b339c-116">monitoring path</span></span> |
| <span data-ttu-id="b339c-117">**Конечные точки**</span><span class="sxs-lookup"><span data-stu-id="b339c-117">**Endpoints**</span></span> |<span data-ttu-id="b339c-118">контейнер для ресурсов конечных точек</span><span class="sxs-lookup"><span data-stu-id="b339c-118">container for endpoint resources</span></span> |

### <a name="endpoint"></a><span data-ttu-id="b339c-119">Конечная точка</span><span class="sxs-lookup"><span data-stu-id="b339c-119">Endpoint</span></span>
<span data-ttu-id="b339c-120">Конечная точка — это дочерний ресурс профиля диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="b339c-120">An endpoint is a child resource of a Traffic Manager Profile.</span></span> <span data-ttu-id="b339c-121">Он представляет собой службу или веб-трафика пользователя toowhich конечной точке распространяется на основе политики настроен hello в hello ресурс профиля диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="b339c-121">It represents a service or web endpoint toowhich user traffic is distributed based on hello configured policy in hello Traffic Manager Profile resource.</span></span> 

| <span data-ttu-id="b339c-122">Свойство</span><span class="sxs-lookup"><span data-stu-id="b339c-122">Property</span></span> | <span data-ttu-id="b339c-123">Описание</span><span class="sxs-lookup"><span data-stu-id="b339c-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b339c-124">**Тип**</span><span class="sxs-lookup"><span data-stu-id="b339c-124">**Type**</span></span> |<span data-ttu-id="b339c-125">Здравствуйте, тип конечной точки hello, возможные значения: *Azure конечной точки*, *внешней конечной точки*, и *вложенные конечной точки*</span><span class="sxs-lookup"><span data-stu-id="b339c-125">hello type of hello endpoint, possible values are *Azure End point*, *External Endpoint*, and  *Nested Endpoint*</span></span> |
| <span data-ttu-id="b339c-126">**targetResourceId**</span><span class="sxs-lookup"><span data-stu-id="b339c-126">**targetResourceId**</span></span> |<span data-ttu-id="b339c-127">общедоступный IP-адрес конечной точки службы или сайта</span><span class="sxs-lookup"><span data-stu-id="b339c-127">public IP address of a service or web endpoint.</span></span> <span data-ttu-id="b339c-128">Это может быть конечная точка Azure или внешняя конечная точка.</span><span class="sxs-lookup"><span data-stu-id="b339c-128">This can be an Azure or external endpoint.</span></span> |
| <span data-ttu-id="b339c-129">**Вес**</span><span class="sxs-lookup"><span data-stu-id="b339c-129">**Weight**</span></span> |<span data-ttu-id="b339c-130">вес конечной точки, используемый при управлении трафиком</span><span class="sxs-lookup"><span data-stu-id="b339c-130">endpoint weight used in traffic management.</span></span> |
| <span data-ttu-id="b339c-131">**Приоритет**</span><span class="sxs-lookup"><span data-stu-id="b339c-131">**Priority**</span></span> |<span data-ttu-id="b339c-132">приоритет hello конечной точки, используемые toodefine действие отработки отказа</span><span class="sxs-lookup"><span data-stu-id="b339c-132">priority of hello endpoint, used toodefine a failover action</span></span> |

<span data-ttu-id="b339c-133">Пример диспетчера трафика в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="b339c-133">Sample of Traffic Manager in Json format:</span></span> 

        {
            "apiVersion": "[variables('tmApiVersion')]",
            "type": "Microsoft.Network/trafficManagerProfiles",
            "name": "VMEndpointExample",
            "location": "global",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '0')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '1')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '2')]",
            ],
            "properties": {
                "profileStatus": "Enabled",
                "trafficRoutingMethod": "Weighted",
                "dnsConfig": {
                    "relativeName": "[parameters('dnsname')]",
                    "ttl": 30
                },
                "monitorConfig": {
                    "protocol": "http",
                    "port": 80,
                    "path": "/"
                },
                "endpoints": [
                    {
                        "name": "endpoint0",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 0))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint1",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 1))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint2",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 2))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    }
                ]
            }
        }


## <a name="additional-resources"></a><span data-ttu-id="b339c-134">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b339c-134">Additional resources</span></span>
<span data-ttu-id="b339c-135">Дополнительные сведения см. в [документации по REST API для диспетчера трафика](https://msdn.microsoft.com/library/azure/mt163664.aspx).</span><span class="sxs-lookup"><span data-stu-id="b339c-135">Read [REST API documentation for Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) for more information.</span></span>

