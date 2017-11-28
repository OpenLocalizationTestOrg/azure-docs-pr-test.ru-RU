---
title: "aaaCreate сетевых групп безопасности - Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как toocreate и развертывание сетевых групп безопасности с помощью hello Azure CLI 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eeb7feedab959d92659e03c5c46d93fdfc08faea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-10"></a><span data-ttu-id="ac376-103">Создание группы безопасности с помощью Azure CLI 1.0 hello сети</span><span class="sxs-lookup"><span data-stu-id="ac376-103">Create network security groups using hello Azure CLI 1.0</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="ac376-104">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="ac376-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="ac376-105">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="ac376-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="ac376-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="ac376-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="ac376-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) -CLI нашей поколения для модели развертывания управления hello ресурсов</span><span class="sxs-lookup"><span data-stu-id="ac376-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) - our next-generation CLI for hello resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="ac376-108">В этой статье рассматриваются hello модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ac376-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="ac376-109">Вы также можете [создать Nsg в hello классической модели развертывания](virtual-networks-create-nsg-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ac376-109">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="ac376-110">приведенную ниже команду Azure CLI Образец Hello ожидать простой среде уже создан на основании hello сценарии выше.</span><span class="sxs-lookup"><span data-stu-id="ac376-110">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> 

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="ac376-111">Как toocreate hello NSG для подсети hello переднего плана</span><span class="sxs-lookup"><span data-stu-id="ac376-111">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="ac376-112">toocreate с именем NSG с именем *NSG-FrontEnd* на основании hello сценарии выше, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="ac376-112">toocreate an NSG named named *NSG-FrontEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="ac376-113">Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="ac376-113">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="ac376-114">Запустите hello **azure конфигурации режима** tooswitch tooResource Manager режим команд, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ac376-114">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="ac376-115">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ac376-115">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="ac376-116">Запустите hello **создать сеть azure nsg** toocreate команда NSG.</span><span class="sxs-lookup"><span data-stu-id="ac376-116">Run hello **azure network nsg create** command toocreate an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-FrontEnd
   
    <span data-ttu-id="ac376-117">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ac376-117">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
        data:    Name                            : NSG-FrontEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
   
    <span data-ttu-id="ac376-118">Параметры</span><span class="sxs-lookup"><span data-stu-id="ac376-118">Parameters:</span></span>
   
   * <span data-ttu-id="ac376-119">**-g (или --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="ac376-119">**-g (or --resource-group)**.</span></span> <span data-ttu-id="ac376-120">Имя группы ресурсов hello, где будут создаваться hello NSG.</span><span class="sxs-lookup"><span data-stu-id="ac376-120">Name of hello resource group where hello NSG will be created.</span></span> <span data-ttu-id="ac376-121">В данном сценарии это *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="ac376-121">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="ac376-122">**-l (или --location)**.</span><span class="sxs-lookup"><span data-stu-id="ac376-122">**-l (or --location)**.</span></span> <span data-ttu-id="ac376-123">Регион Azure, где hello новой NSG будет создан.</span><span class="sxs-lookup"><span data-stu-id="ac376-123">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="ac376-124">В нашем случае это *westus*.</span><span class="sxs-lookup"><span data-stu-id="ac376-124">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="ac376-125">**-n (или --name)**.</span><span class="sxs-lookup"><span data-stu-id="ac376-125">**-n (or --name)**.</span></span> <span data-ttu-id="ac376-126">Имя для hello новая NSG.</span><span class="sxs-lookup"><span data-stu-id="ac376-126">Name for hello new NSG.</span></span> <span data-ttu-id="ac376-127">В данном сценарии это *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="ac376-127">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="ac376-128">Запустите hello **создать правило nsg сети azure** команда toocreate правило, разрешающее доступ tooport 3389 (RDP) из Интернета hello.</span><span class="sxs-lookup"><span data-stu-id="ac376-128">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 3389 (RDP) from hello Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="ac376-129">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ac376-129">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        warn:    Using default direction: Inbound
        info:    Looking up hello network security rule "rdp-rule"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp
        -rule
        data:    Name                            : rdp-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 3389
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="ac376-130">Параметры</span><span class="sxs-lookup"><span data-stu-id="ac376-130">Parameters:</span></span>
   
   * <span data-ttu-id="ac376-131">**-a (или --nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="ac376-131">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="ac376-132">Имя в какие hello будет создано правило NSG hello.</span><span class="sxs-lookup"><span data-stu-id="ac376-132">Name of hello NSG in which hello rule will be created.</span></span> <span data-ttu-id="ac376-133">В данном сценарии это *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="ac376-133">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="ac376-134">**-n (или --name)**.</span><span class="sxs-lookup"><span data-stu-id="ac376-134">**-n (or --name)**.</span></span> <span data-ttu-id="ac376-135">Имя для нового правила hello.</span><span class="sxs-lookup"><span data-stu-id="ac376-135">Name for hello new rule.</span></span> <span data-ttu-id="ac376-136">В нашем случае это *rdp-rule*.</span><span class="sxs-lookup"><span data-stu-id="ac376-136">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="ac376-137">**-c (или --access)**.</span><span class="sxs-lookup"><span data-stu-id="ac376-137">**-c (or --access)**.</span></span> <span data-ttu-id="ac376-138">Уровень доступа для правила hello (запретить или разрешить).</span><span class="sxs-lookup"><span data-stu-id="ac376-138">Access level for hello rule (Deny or Allow).</span></span>
   * <span data-ttu-id="ac376-139">**-p (или --protocol)**.</span><span class="sxs-lookup"><span data-stu-id="ac376-139">**-p (or --protocol)**.</span></span> <span data-ttu-id="ac376-140">Протокол (Tcp, Udp или *) для правила hello.</span><span class="sxs-lookup"><span data-stu-id="ac376-140">Protocol (Tcp, Udp, or *) for hello rule.</span></span>
   * <span data-ttu-id="ac376-141">**-r (or --direction)**.</span><span class="sxs-lookup"><span data-stu-id="ac376-141">**-r (or --direction)**.</span></span> <span data-ttu-id="ac376-142">Направление подключения (Inbound или Outbound).</span><span class="sxs-lookup"><span data-stu-id="ac376-142">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="ac376-143">**-y (или --priority)**.</span><span class="sxs-lookup"><span data-stu-id="ac376-143">**-y (or --priority)**.</span></span> <span data-ttu-id="ac376-144">Приоритет для правила hello.</span><span class="sxs-lookup"><span data-stu-id="ac376-144">Priority for hello rule.</span></span>
   * <span data-ttu-id="ac376-145">**-f (или --source-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="ac376-145">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="ac376-146">Префикс адреса источника в CIDR или использование тегов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ac376-146">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="ac376-147">**-o (или --source-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="ac376-147">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="ac376-148">Исходный порт или диапазон портов.</span><span class="sxs-lookup"><span data-stu-id="ac376-148">Source port, or port range.</span></span>
   * <span data-ttu-id="ac376-149">**-e (или --destination-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="ac376-149">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="ac376-150">Префикс адреса назначения в CIDR или использование тегов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ac376-150">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="ac376-151">**-u (или --destination-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="ac376-151">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="ac376-152">Конечный порт или диапазон портов.</span><span class="sxs-lookup"><span data-stu-id="ac376-152">Destination port, or port range.</span></span>    
5. <span data-ttu-id="ac376-153">Запустите hello **создать правило nsg сети azure** команда toocreate правило, разрешающее доступ tooport 80 (HTTP) из Интернета hello.</span><span class="sxs-lookup"><span data-stu-id="ac376-153">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 80 (HTTP) from hello Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="ac376-154">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ac376-154">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 80
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="ac376-155">Запустите hello **набор подсети виртуальной сети azure сети** команда toolink hello NSG toohello внешнего интерфейса подсети.</span><span class="sxs-lookup"><span data-stu-id="ac376-155">Run hello **azure network vnet subnet set** command toolink hello NSG toohello front end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -o NSG-FrontEnd
   
    <span data-ttu-id="ac376-156">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ac376-156">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="ac376-157">Hello toocreate NSG для hello обратно конечного подсети</span><span class="sxs-lookup"><span data-stu-id="ac376-157">How toocreate hello NSG for hello back end subnet</span></span>
<span data-ttu-id="ac376-158">toocreate с именем NSG с именем *NSG серверной* на основании hello сценарии выше, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="ac376-158">toocreate an NSG named named *NSG-BackEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="ac376-159">Запустите hello **создать сеть azure nsg** toocreate команда NSG.</span><span class="sxs-lookup"><span data-stu-id="ac376-159">Run hello **azure network nsg create** command toocreate an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-BackEnd
   
    <span data-ttu-id="ac376-160">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ac376-160">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd
        data:    Name                            : NSG-BackEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
2. <span data-ttu-id="ac376-161">Запустите hello **создать правило nsg сети azure** команда toocreate правило, разрешающее доступ tooport 1433 (SQL) из подсети hello переднего плана.</span><span class="sxs-lookup"><span data-stu-id="ac376-161">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 1433 (SQL) from hello front end subnet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="ac376-162">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ac376-162">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "sql-rule"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule
        data:    Name                            : sql-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 1433
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="ac376-163">Запустите hello **создать правило nsg сети azure** команда toocreate правило, запрещающее доступ toohello Интернет из.</span><span class="sxs-lookup"><span data-stu-id="ac376-163">Run hello **azure network nsg rule create** command toocreate a rule that denies access toohello Internet from.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n web-rule -c Deny -p * -r Outbound -y 200 -f * -o * -e Internet -u *
   
    <span data-ttu-id="ac376-164">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ac376-164">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : *
        data:    Source Port                     : *
        data:    Destination IP                  : Internet
        data:    Destination Port                : *
        data:    Protocol                        : *
        data:    Direction                       : Outbound
        data:    Access                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="ac376-165">Запустите hello **набор подсети виртуальной сети azure сети** команды toohello NSG hello toolink обратно завершить подсети.</span><span class="sxs-lookup"><span data-stu-id="ac376-165">Run hello **azure network vnet subnet set** command toolink hello NSG toohello back end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -o NSG-BackEnd
   
    <span data-ttu-id="ac376-166">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ac376-166">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Setting subnet "BackEnd"
        info:    Looking up hello subnet "BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/BackEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : BackEnd
        data:    Address prefix                  : 192.168.2.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL1/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL2/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

