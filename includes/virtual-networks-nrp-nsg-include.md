## <a name="network-security-group"></a><span data-ttu-id="f65e3-101">Группа безопасности сети</span><span class="sxs-lookup"><span data-stu-id="f65e3-101">Network Security Group</span></span>
<span data-ttu-id="f65e3-102">Ресурс NSG обеспечивает создание hello защитная граница для рабочих нагрузок, путем реализации разрешать и запрещать правила.</span><span class="sxs-lookup"><span data-stu-id="f65e3-102">An NSG resource enables hello creation of security boundary for workloads, by implementing allow and deny rules.</span></span> <span data-ttu-id="f65e3-103">Такие правила могут быть применены tooa виртуальной Машины, сетевой Адаптер или подсети.</span><span class="sxs-lookup"><span data-stu-id="f65e3-103">Such rules can be applied tooa VM, a NIC, or a subnet.</span></span>

| <span data-ttu-id="f65e3-104">Свойство</span><span class="sxs-lookup"><span data-stu-id="f65e3-104">Property</span></span> | <span data-ttu-id="f65e3-105">Описание</span><span class="sxs-lookup"><span data-stu-id="f65e3-105">Description</span></span> | <span data-ttu-id="f65e3-106">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="f65e3-106">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f65e3-107">**Подсети**</span><span class="sxs-lookup"><span data-stu-id="f65e3-107">**subnets**</span></span> |<span data-ttu-id="f65e3-108">Список идентификаторов подсети hello NSG применяется.</span><span class="sxs-lookup"><span data-stu-id="f65e3-108">List of subnet ids hello NSG is applied to.</span></span> |<span data-ttu-id="f65e3-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span><span class="sxs-lookup"><span data-stu-id="f65e3-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span></span> |
| <span data-ttu-id="f65e3-110">**securityRules**</span><span class="sxs-lookup"><span data-stu-id="f65e3-110">**securityRules**</span></span> |<span data-ttu-id="f65e3-111">Список правил безопасности, которые составляют hello NSG</span><span class="sxs-lookup"><span data-stu-id="f65e3-111">List of security rules that make up hello NSG</span></span> |<span data-ttu-id="f65e3-112">См. раздел [Правило безопасности](#Security-rule) ниже.</span><span class="sxs-lookup"><span data-stu-id="f65e3-112">See [Security rule](#Security-rule) below</span></span> |
| <span data-ttu-id="f65e3-113">**defaultSecurityRules**</span><span class="sxs-lookup"><span data-stu-id="f65e3-113">**defaultSecurityRules**</span></span> |<span data-ttu-id="f65e3-114">Список правил безопасности по умолчанию в каждой группе безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="f65e3-114">List of default security rules present in every NSG</span></span> |<span data-ttu-id="f65e3-115">См. раздел [Правила безопасности по умолчанию](#Default-security-rules) ниже.</span><span class="sxs-lookup"><span data-stu-id="f65e3-115">See [Default security rules](#Default-security-rules) below</span></span> |

* <span data-ttu-id="f65e3-116">**Правило безопасности** : для NSG можно определить несколько правил безопасности.</span><span class="sxs-lookup"><span data-stu-id="f65e3-116">**Security rule** - An NSG can have multiple security rules defined.</span></span> <span data-ttu-id="f65e3-117">Каждое правило может разрешать или запрещать различные типы трафика.</span><span class="sxs-lookup"><span data-stu-id="f65e3-117">Each rule can allow or deny different types of traffic.</span></span>

### <a name="security-rule"></a><span data-ttu-id="f65e3-118">Правило безопасности</span><span class="sxs-lookup"><span data-stu-id="f65e3-118">Security rule</span></span>
<span data-ttu-id="f65e3-119">Правило безопасности является дочерний ресурс NSG, содержащий свойства hello ниже.</span><span class="sxs-lookup"><span data-stu-id="f65e3-119">A security rule is a child resource of an NSG containing hello properties below.</span></span>

| <span data-ttu-id="f65e3-120">Свойство</span><span class="sxs-lookup"><span data-stu-id="f65e3-120">Property</span></span> | <span data-ttu-id="f65e3-121">Описание</span><span class="sxs-lookup"><span data-stu-id="f65e3-121">Description</span></span> | <span data-ttu-id="f65e3-122">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="f65e3-122">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f65e3-123">**description**</span><span class="sxs-lookup"><span data-stu-id="f65e3-123">**description**</span></span> |<span data-ttu-id="f65e3-124">Описание для правила hello</span><span class="sxs-lookup"><span data-stu-id="f65e3-124">Description for hello rule</span></span> |<span data-ttu-id="f65e3-125">Разрешить входящий трафик для всех виртуальных машин в подсети X.</span><span class="sxs-lookup"><span data-stu-id="f65e3-125">Allow inbound traffic for all VMs in subnet X</span></span> |
| <span data-ttu-id="f65e3-126">**protocol**</span><span class="sxs-lookup"><span data-stu-id="f65e3-126">**protocol**</span></span> |<span data-ttu-id="f65e3-127">Протокол toomatch для правила hello</span><span class="sxs-lookup"><span data-stu-id="f65e3-127">Protocol toomatch for hello rule</span></span> |<span data-ttu-id="f65e3-128">TCP, UDP или *</span><span class="sxs-lookup"><span data-stu-id="f65e3-128">TCP, UDP, or *</span></span> |
| <span data-ttu-id="f65e3-129">**sourcePortRange**</span><span class="sxs-lookup"><span data-stu-id="f65e3-129">**sourcePortRange**</span></span> |<span data-ttu-id="f65e3-130">Toomatch диапазон портов источника для правила hello</span><span class="sxs-lookup"><span data-stu-id="f65e3-130">Source port range toomatch for hello rule</span></span> |<span data-ttu-id="f65e3-131">80, 100–200, *</span><span class="sxs-lookup"><span data-stu-id="f65e3-131">80, 100-200, *</span></span> |
| <span data-ttu-id="f65e3-132">**destinationPortRange**</span><span class="sxs-lookup"><span data-stu-id="f65e3-132">**destinationPortRange**</span></span> |<span data-ttu-id="f65e3-133">Toomatch диапазон портов назначения для правила hello</span><span class="sxs-lookup"><span data-stu-id="f65e3-133">Destination port range toomatch for hello rule</span></span> |<span data-ttu-id="f65e3-134">80, 100–200, *</span><span class="sxs-lookup"><span data-stu-id="f65e3-134">80, 100-200, *</span></span> |
| <span data-ttu-id="f65e3-135">**sourceAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="f65e3-135">**sourceAddressPrefix**</span></span> |<span data-ttu-id="f65e3-136">Toomatch префикс адреса источника для правила hello</span><span class="sxs-lookup"><span data-stu-id="f65e3-136">Source address prefix toomatch for hello rule</span></span> |<span data-ttu-id="f65e3-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="f65e3-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="f65e3-138">**destinationAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="f65e3-138">**destinationAddressPrefix**</span></span> |<span data-ttu-id="f65e3-139">Toomatch префикс адреса назначения для правила hello</span><span class="sxs-lookup"><span data-stu-id="f65e3-139">Destination address prefix toomatch for hello rule</span></span> |<span data-ttu-id="f65e3-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="f65e3-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="f65e3-141">**direction**</span><span class="sxs-lookup"><span data-stu-id="f65e3-141">**direction**</span></span> |<span data-ttu-id="f65e3-142">Направление трафика toomatch для правила hello</span><span class="sxs-lookup"><span data-stu-id="f65e3-142">Direction of traffic toomatch for hello rule</span></span> |<span data-ttu-id="f65e3-143">inbound или outbound</span><span class="sxs-lookup"><span data-stu-id="f65e3-143">inbound or outbound</span></span> |
| <span data-ttu-id="f65e3-144">**priority**</span><span class="sxs-lookup"><span data-stu-id="f65e3-144">**priority**</span></span> |<span data-ttu-id="f65e3-145">Приоритет для правила hello.</span><span class="sxs-lookup"><span data-stu-id="f65e3-145">Priority for hello rule.</span></span> <span data-ttu-id="f65e3-146">Правила проверяются в порядке приоритета. Когда применяется правило, соответствие дополнительным правилам не проверяется.</span><span class="sxs-lookup"><span data-stu-id="f65e3-146">Rules are checked int he order of priority, once a rule applies, no more rules are tested for matching.</span></span> |<span data-ttu-id="f65e3-147">10, 100, 65000</span><span class="sxs-lookup"><span data-stu-id="f65e3-147">10, 100, 65000</span></span> |
| <span data-ttu-id="f65e3-148">**access**</span><span class="sxs-lookup"><span data-stu-id="f65e3-148">**access**</span></span> |<span data-ttu-id="f65e3-149">Тип доступа tooapply ли соответствует правилу hello</span><span class="sxs-lookup"><span data-stu-id="f65e3-149">Type of access tooapply if hello rule matches</span></span> |<span data-ttu-id="f65e3-150">allow или deny</span><span class="sxs-lookup"><span data-stu-id="f65e3-150">allow or deny</span></span> |

<span data-ttu-id="f65e3-151">Пример группы безопасности сети в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="f65e3-151">Sample NSG in JSON format:</span></span>

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a><span data-ttu-id="f65e3-152">Правила безопасности по умолчанию</span><span class="sxs-lookup"><span data-stu-id="f65e3-152">Default security rules</span></span>

<span data-ttu-id="f65e3-153">Правила безопасности по умолчанию имеют hello и те же свойства, доступные в правилах безопасности.</span><span class="sxs-lookup"><span data-stu-id="f65e3-153">Default security rules have hello same properties available in security rules.</span></span> <span data-ttu-id="f65e3-154">Они существуют tooprovide базовых соединений между ресурсами, имеющих toothem Nsg применяется.</span><span class="sxs-lookup"><span data-stu-id="f65e3-154">They exist tooprovide basic connectivity between resources that have NSGs applied toothem.</span></span> <span data-ttu-id="f65e3-155">Вам следует знать, какие существуют [правила безопасности по умолчанию](../articles/virtual-network/virtual-networks-nsg.md#default-rules).</span><span class="sxs-lookup"><span data-stu-id="f65e3-155">Make sure you know which [default security rules](../articles/virtual-network/virtual-networks-nsg.md#default-rules) exist.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="f65e3-156">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f65e3-156">Additional resources</span></span>
* <span data-ttu-id="f65e3-157">Более подробная информация о [группах безопасности сети](../articles/virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="f65e3-157">Get more information about [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span></span>
* <span data-ttu-id="f65e3-158">Чтение hello [справочной документации REST API](https://msdn.microsoft.com/library/azure/mt163615.aspx) для Nsg.</span><span class="sxs-lookup"><span data-stu-id="f65e3-158">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163615.aspx) for NSGs.</span></span>
* <span data-ttu-id="f65e3-159">Чтение hello [справочной документации REST API](https://msdn.microsoft.com/library/azure/mt163580.aspx) для правил безопасности.</span><span class="sxs-lookup"><span data-stu-id="f65e3-159">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163580.aspx) for security rules.</span></span>
