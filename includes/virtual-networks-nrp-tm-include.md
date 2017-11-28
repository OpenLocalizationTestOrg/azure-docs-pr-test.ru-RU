## <a name="traffic-manager-profile"></a><span data-ttu-id="2e7ea-101">Профиль диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="2e7ea-101">Traffic Manager Profile</span></span>
<span data-ttu-id="2e7ea-102">Ресурс диспетчера трафика и его дочерней конечной точки обеспечивает маршрутизацию DNS к конечным точкам Azure и за пределы Azure.</span><span class="sxs-lookup"><span data-stu-id="2e7ea-102">Traffic manager and its child endpoint resource enable DNS routing to endpoints in Azure and outside of Azure.</span></span> <span data-ttu-id="2e7ea-103">Такое распределение трафика регулируется с помощью политик.</span><span class="sxs-lookup"><span data-stu-id="2e7ea-103">Such traffic distribution is governed by routing  policy methods.</span></span> <span data-ttu-id="2e7ea-104">Диспетчер трафика позволяет также отслеживать работоспособность конечных точек и перенаправлять трафик с учетом работоспособности конечной точки.</span><span class="sxs-lookup"><span data-stu-id="2e7ea-104">Traffic manager also allows endpoint health to be monitored, and traffic diverted appropriately based on the health of an endpoint.</span></span> 

| <span data-ttu-id="2e7ea-105">Свойство</span><span class="sxs-lookup"><span data-stu-id="2e7ea-105">Property</span></span> | <span data-ttu-id="2e7ea-106">Описание</span><span class="sxs-lookup"><span data-stu-id="2e7ea-106">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2e7ea-107">**trafficRoutingMethod**</span><span class="sxs-lookup"><span data-stu-id="2e7ea-107">**trafficRoutingMethod**</span></span> |<span data-ttu-id="2e7ea-108">Возможные значения: *Performance* (производительный), *Weighted* (взвешенный) и *Priority* (приоритетный).</span><span class="sxs-lookup"><span data-stu-id="2e7ea-108">possible values are *Performance*, *Weighted*, and *Priority*</span></span> |
| <span data-ttu-id="2e7ea-109">**dnsConfig**</span><span class="sxs-lookup"><span data-stu-id="2e7ea-109">**dnsConfig**</span></span> |<span data-ttu-id="2e7ea-110">полное доменное имя для профиля</span><span class="sxs-lookup"><span data-stu-id="2e7ea-110">FQDN for the profile</span></span> |
| <span data-ttu-id="2e7ea-111">**Протокол**</span><span class="sxs-lookup"><span data-stu-id="2e7ea-111">**Protocol**</span></span> |<span data-ttu-id="2e7ea-112">Протокол мониторинга. Возможные значения: *HTTP* и *HTTPS*.</span><span class="sxs-lookup"><span data-stu-id="2e7ea-112">monitoring protocol, possible values are *HTTP* and *HTTPS*</span></span> |
| <span data-ttu-id="2e7ea-113">**Порт**</span><span class="sxs-lookup"><span data-stu-id="2e7ea-113">**Port**</span></span> |<span data-ttu-id="2e7ea-114">порт мониторинга</span><span class="sxs-lookup"><span data-stu-id="2e7ea-114">monitoring port</span></span> |
| <span data-ttu-id="2e7ea-115">**Путь**</span><span class="sxs-lookup"><span data-stu-id="2e7ea-115">**Path**</span></span> |<span data-ttu-id="2e7ea-116">путь мониторинга</span><span class="sxs-lookup"><span data-stu-id="2e7ea-116">monitoring path</span></span> |
| <span data-ttu-id="2e7ea-117">**Конечные точки**</span><span class="sxs-lookup"><span data-stu-id="2e7ea-117">**Endpoints**</span></span> |<span data-ttu-id="2e7ea-118">контейнер для ресурсов конечных точек</span><span class="sxs-lookup"><span data-stu-id="2e7ea-118">container for endpoint resources</span></span> |

### <a name="endpoint"></a><span data-ttu-id="2e7ea-119">Конечная точка</span><span class="sxs-lookup"><span data-stu-id="2e7ea-119">Endpoint</span></span>
<span data-ttu-id="2e7ea-120">Конечная точка — это дочерний ресурс профиля диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="2e7ea-120">An endpoint is a child resource of a Traffic Manager Profile.</span></span> <span data-ttu-id="2e7ea-121">Он представляет службу или сетевую конечную точку, на которые распределяется трафик с учетом политики, настроенной в ресурсе профиля диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="2e7ea-121">It represents a service or web endpoint to which user traffic is distributed based on the configured policy in the Traffic Manager Profile resource.</span></span> 

| <span data-ttu-id="2e7ea-122">Свойство</span><span class="sxs-lookup"><span data-stu-id="2e7ea-122">Property</span></span> | <span data-ttu-id="2e7ea-123">Описание</span><span class="sxs-lookup"><span data-stu-id="2e7ea-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2e7ea-124">**Тип**</span><span class="sxs-lookup"><span data-stu-id="2e7ea-124">**Type**</span></span> |<span data-ttu-id="2e7ea-125">Тип конечной точки. Возможные значения: *Конечная точка Azure*, *Внешняя конечная точка* и *Вложенная конечная точка*.</span><span class="sxs-lookup"><span data-stu-id="2e7ea-125">the type of the endpoint, possible values are *Azure End point*, *External Endpoint*, and  *Nested Endpoint*</span></span> |
| <span data-ttu-id="2e7ea-126">**targetResourceId**</span><span class="sxs-lookup"><span data-stu-id="2e7ea-126">**targetResourceId**</span></span> |<span data-ttu-id="2e7ea-127">общедоступный IP-адрес конечной точки службы или сайта</span><span class="sxs-lookup"><span data-stu-id="2e7ea-127">public IP address of a service or web endpoint.</span></span> <span data-ttu-id="2e7ea-128">Это может быть конечная точка Azure или внешняя конечная точка.</span><span class="sxs-lookup"><span data-stu-id="2e7ea-128">This can be an Azure or external endpoint.</span></span> |
| <span data-ttu-id="2e7ea-129">**Вес**</span><span class="sxs-lookup"><span data-stu-id="2e7ea-129">**Weight**</span></span> |<span data-ttu-id="2e7ea-130">вес конечной точки, используемый при управлении трафиком</span><span class="sxs-lookup"><span data-stu-id="2e7ea-130">endpoint weight used in traffic management.</span></span> |
| <span data-ttu-id="2e7ea-131">**Приоритет**</span><span class="sxs-lookup"><span data-stu-id="2e7ea-131">**Priority**</span></span> |<span data-ttu-id="2e7ea-132">приоритет конечной точки, используемый для определения действия отработки отказа</span><span class="sxs-lookup"><span data-stu-id="2e7ea-132">priority of the endpoint, used to define a failover action</span></span> |

<span data-ttu-id="2e7ea-133">Пример диспетчера трафика в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="2e7ea-133">Sample of Traffic Manager in Json format:</span></span> 

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


## <a name="additional-resources"></a><span data-ttu-id="2e7ea-134">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2e7ea-134">Additional resources</span></span>
<span data-ttu-id="2e7ea-135">Дополнительные сведения см. в [документации по REST API для диспетчера трафика](https://msdn.microsoft.com/library/azure/mt163664.aspx).</span><span class="sxs-lookup"><span data-stu-id="2e7ea-135">Read [REST API documentation for Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) for more information.</span></span>

