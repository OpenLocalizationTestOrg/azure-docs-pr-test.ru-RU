## <a name="network-security-group"></a><span data-ttu-id="3a5f4-101">Группа безопасности сети</span><span class="sxs-lookup"><span data-stu-id="3a5f4-101">Network Security Group</span></span>
<span data-ttu-id="3a5f4-102">Ресурс NSG позволяет создать периметр безопасности для рабочих нагрузок путем реализации разрешающих и запрещающих правил.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-102">An NSG resource enables the creation of security boundary for workloads, by implementing allow and deny rules.</span></span> <span data-ttu-id="3a5f4-103">Такие правила могут быть применены к виртуальной машине, сетевой карте или подсети.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-103">Such rules can be applied to a VM, a NIC, or a subnet.</span></span>

| <span data-ttu-id="3a5f4-104">Свойство</span><span class="sxs-lookup"><span data-stu-id="3a5f4-104">Property</span></span> | <span data-ttu-id="3a5f4-105">Описание</span><span class="sxs-lookup"><span data-stu-id="3a5f4-105">Description</span></span> | <span data-ttu-id="3a5f4-106">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="3a5f4-106">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3a5f4-107">**Подсети**</span><span class="sxs-lookup"><span data-stu-id="3a5f4-107">**subnets**</span></span> |<span data-ttu-id="3a5f4-108">Список идентификаторов подсетей, к которым применена группа безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-108">List of subnet ids the NSG is applied to.</span></span> |<span data-ttu-id="3a5f4-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span><span class="sxs-lookup"><span data-stu-id="3a5f4-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span></span> |
| <span data-ttu-id="3a5f4-110">**securityRules**</span><span class="sxs-lookup"><span data-stu-id="3a5f4-110">**securityRules**</span></span> |<span data-ttu-id="3a5f4-111">Список правил безопасности, которые определяют группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-111">List of security rules that make up the NSG</span></span> |<span data-ttu-id="3a5f4-112">См. раздел [Правило безопасности](#Security-rule) ниже.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-112">See [Security rule](#Security-rule) below</span></span> |
| <span data-ttu-id="3a5f4-113">**defaultSecurityRules**</span><span class="sxs-lookup"><span data-stu-id="3a5f4-113">**defaultSecurityRules**</span></span> |<span data-ttu-id="3a5f4-114">Список правил безопасности по умолчанию в каждой группе безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-114">List of default security rules present in every NSG</span></span> |<span data-ttu-id="3a5f4-115">См. раздел [Правила безопасности по умолчанию](#Default-security-rules) ниже.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-115">See [Default security rules](#Default-security-rules) below</span></span> |

* <span data-ttu-id="3a5f4-116">**Правило безопасности** : для NSG можно определить несколько правил безопасности.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-116">**Security rule** - An NSG can have multiple security rules defined.</span></span> <span data-ttu-id="3a5f4-117">Каждое правило может разрешать или запрещать различные типы трафика.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-117">Each rule can allow or deny different types of traffic.</span></span>

### <a name="security-rule"></a><span data-ttu-id="3a5f4-118">Правило безопасности</span><span class="sxs-lookup"><span data-stu-id="3a5f4-118">Security rule</span></span>
<span data-ttu-id="3a5f4-119">Правило безопасности является дочерним ресурсом группы безопасности сети, содержащим описанные ниже свойства.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-119">A security rule is a child resource of an NSG containing the properties below.</span></span>

| <span data-ttu-id="3a5f4-120">Свойство</span><span class="sxs-lookup"><span data-stu-id="3a5f4-120">Property</span></span> | <span data-ttu-id="3a5f4-121">Описание</span><span class="sxs-lookup"><span data-stu-id="3a5f4-121">Description</span></span> | <span data-ttu-id="3a5f4-122">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="3a5f4-122">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3a5f4-123">**description**</span><span class="sxs-lookup"><span data-stu-id="3a5f4-123">**description**</span></span> |<span data-ttu-id="3a5f4-124">Описание правила.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-124">Description for the rule</span></span> |<span data-ttu-id="3a5f4-125">Разрешить входящий трафик для всех виртуальных машин в подсети X.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-125">Allow inbound traffic for all VMs in subnet X</span></span> |
| <span data-ttu-id="3a5f4-126">**protocol**</span><span class="sxs-lookup"><span data-stu-id="3a5f4-126">**protocol**</span></span> |<span data-ttu-id="3a5f4-127">Протокол правила для сопоставления.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-127">Protocol to match for the rule</span></span> |<span data-ttu-id="3a5f4-128">TCP, UDP или *</span><span class="sxs-lookup"><span data-stu-id="3a5f4-128">TCP, UDP, or *</span></span> |
| <span data-ttu-id="3a5f4-129">**sourcePortRange**</span><span class="sxs-lookup"><span data-stu-id="3a5f4-129">**sourcePortRange**</span></span> |<span data-ttu-id="3a5f4-130">Диапазон портов источника правила для сопоставления.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-130">Source port range to match for the rule</span></span> |<span data-ttu-id="3a5f4-131">80, 100–200, *</span><span class="sxs-lookup"><span data-stu-id="3a5f4-131">80, 100-200, *</span></span> |
| <span data-ttu-id="3a5f4-132">**destinationPortRange**</span><span class="sxs-lookup"><span data-stu-id="3a5f4-132">**destinationPortRange**</span></span> |<span data-ttu-id="3a5f4-133">Диапазон портов назначения правила для сопоставления.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-133">Destination port range to match for the rule</span></span> |<span data-ttu-id="3a5f4-134">80, 100–200, *</span><span class="sxs-lookup"><span data-stu-id="3a5f4-134">80, 100-200, *</span></span> |
| <span data-ttu-id="3a5f4-135">**sourceAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="3a5f4-135">**sourceAddressPrefix**</span></span> |<span data-ttu-id="3a5f4-136">Префикс адреса источника правила для сопоставления.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-136">Source address prefix to match for the rule</span></span> |<span data-ttu-id="3a5f4-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="3a5f4-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="3a5f4-138">**destinationAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="3a5f4-138">**destinationAddressPrefix**</span></span> |<span data-ttu-id="3a5f4-139">Префикс адреса назначения правила для сопоставления.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-139">Destination address prefix to match for the rule</span></span> |<span data-ttu-id="3a5f4-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="3a5f4-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="3a5f4-141">**direction**</span><span class="sxs-lookup"><span data-stu-id="3a5f4-141">**direction**</span></span> |<span data-ttu-id="3a5f4-142">Направление трафика правила для сопоставления.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-142">Direction of traffic to match for the rule</span></span> |<span data-ttu-id="3a5f4-143">inbound или outbound</span><span class="sxs-lookup"><span data-stu-id="3a5f4-143">inbound or outbound</span></span> |
| <span data-ttu-id="3a5f4-144">**priority**</span><span class="sxs-lookup"><span data-stu-id="3a5f4-144">**priority**</span></span> |<span data-ttu-id="3a5f4-145">Приоритет правила.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-145">Priority for the rule.</span></span> <span data-ttu-id="3a5f4-146">Правила проверяются в порядке приоритета. Когда применяется правило, соответствие дополнительным правилам не проверяется.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-146">Rules are checked int he order of priority, once a rule applies, no more rules are tested for matching.</span></span> |<span data-ttu-id="3a5f4-147">10, 100, 65000</span><span class="sxs-lookup"><span data-stu-id="3a5f4-147">10, 100, 65000</span></span> |
| <span data-ttu-id="3a5f4-148">**access**</span><span class="sxs-lookup"><span data-stu-id="3a5f4-148">**access**</span></span> |<span data-ttu-id="3a5f4-149">Тип доступа, применяемый при соответствии правилу.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-149">Type of access to apply if the rule matches</span></span> |<span data-ttu-id="3a5f4-150">allow или deny</span><span class="sxs-lookup"><span data-stu-id="3a5f4-150">allow or deny</span></span> |

<span data-ttu-id="3a5f4-151">Пример группы безопасности сети в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="3a5f4-151">Sample NSG in JSON format:</span></span>

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

### <a name="default-security-rules"></a><span data-ttu-id="3a5f4-152">Правила безопасности по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3a5f4-152">Default security rules</span></span>

<span data-ttu-id="3a5f4-153">Правила безопасности по умолчанию имеют те же свойства, что и правила безопасности.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-153">Default security rules have the same properties available in security rules.</span></span> <span data-ttu-id="3a5f4-154">Они существуют для обеспечения базовых подключений между ресурсами, к которым применены группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-154">They exist to provide basic connectivity between resources that have NSGs applied to them.</span></span> <span data-ttu-id="3a5f4-155">Вам следует знать, какие существуют [правила безопасности по умолчанию](../articles/virtual-network/virtual-networks-nsg.md#default-rules).</span><span class="sxs-lookup"><span data-stu-id="3a5f4-155">Make sure you know which [default security rules](../articles/virtual-network/virtual-networks-nsg.md#default-rules) exist.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="3a5f4-156">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3a5f4-156">Additional resources</span></span>
* <span data-ttu-id="3a5f4-157">Более подробная информация о [группах безопасности сети](../articles/virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="3a5f4-157">Get more information about [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span></span>
* <span data-ttu-id="3a5f4-158">Прочитайте [справочную документацию по REST API](https://msdn.microsoft.com/library/azure/mt163615.aspx) для групп безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-158">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163615.aspx) for NSGs.</span></span>
* <span data-ttu-id="3a5f4-159">Прочитайте [справочную документацию по REST API](https://msdn.microsoft.com/library/azure/mt163580.aspx) для правил безопасности.</span><span class="sxs-lookup"><span data-stu-id="3a5f4-159">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163580.aspx) for security rules.</span></span>
