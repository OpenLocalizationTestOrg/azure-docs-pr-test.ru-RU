---
title: "Как создавать сетевые группы безопасности в классическом режиме с помощью интерфейса командной строки Azure | Документация Майкрософт"
description: "Узнайте, как создавать и развертывать сетевые группы безопасности в классическом режиме, используя интерфейс командной строки Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 17d98950-5fbb-4653-bef6-d822ab37541e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 115a1937a4c88ba2b986a40c84b1b759ed5e03b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-nsgs-classic-in-the-azure-cli"></a><span data-ttu-id="51c5d-103">Как создавать сетевые группы безопасности (в классическом режиме) в интерфейсе командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="51c5d-103">How to create NSGs (classic) in the Azure CLI</span></span>
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="51c5d-104">В этой статье рассматривается классическая модель развертывания.</span><span class="sxs-lookup"><span data-stu-id="51c5d-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="51c5d-105">Вы также можете [создавать группы безопасности сети с использованием модели развертывания на основе диспетчера ресурсов](virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="51c5d-105">You can also [create NSGs in the Resource Manager deployment model](virtual-networks-create-nsg-arm-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="51c5d-106">Для приведенных ниже примеров команд интерфейса командной строки Azure требуется уже созданная простая среда, основанная на приведенном выше сценарии.</span><span class="sxs-lookup"><span data-stu-id="51c5d-106">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="51c5d-107">Чтобы выполнять команды в соответствии с инструкциями, представленными в этом документе, сначала создайте тестовую среду, [создав виртуальную сеть](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="51c5d-107">If you want to run the commands as they are displayed in this document, first build the test environment by [creating a VNet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="51c5d-108">Как создавать сетевую группу безопасности для подсети переднего плана</span><span class="sxs-lookup"><span data-stu-id="51c5d-108">How to create the NSG for the front end subnet</span></span>
<span data-ttu-id="51c5d-109">Чтобы создать сетевую группу безопасности под названием **NSG-FrontEnd** по описанному выше сценарию, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="51c5d-109">To create an NSG named named **NSG-FrontEnd** based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="51c5d-110">Если вы еще не пользовались Azure CLI, ознакомьтесь со статьей [Установка и настройка CLI Azure](../cli-install-nodejs.md) и следуйте инструкциям вплоть до выбора учетной записи Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="51c5d-110">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="51c5d-111">Запустите команду **`azure config mode`** , чтобы перейти в классический режим, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="51c5d-111">Run the **`azure config mode`** command to switch to classic mode, as shown below.</span></span>
   
        azure config mode asm
   
    <span data-ttu-id="51c5d-112">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="51c5d-112">Expected output:</span></span>
   
        info:    New mode is asm
3. <span data-ttu-id="51c5d-113">Запустите команду **`azure network nsg create`** , чтобы создать сетевую группу безопасности.</span><span class="sxs-lookup"><span data-stu-id="51c5d-113">Run the **`azure network nsg create`** command to create an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    <span data-ttu-id="51c5d-114">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="51c5d-114">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : NSG-FrontEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="51c5d-115">Параметры</span><span class="sxs-lookup"><span data-stu-id="51c5d-115">Parameters:</span></span>
   
   * <span data-ttu-id="51c5d-116">**-l (или --location)**.</span><span class="sxs-lookup"><span data-stu-id="51c5d-116">**-l (or --location)**.</span></span> <span data-ttu-id="51c5d-117">Регион Azure, в котором будет создана группа безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="51c5d-117">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="51c5d-118">В нашем случае это *westus*.</span><span class="sxs-lookup"><span data-stu-id="51c5d-118">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="51c5d-119">**-n (или --name)**.</span><span class="sxs-lookup"><span data-stu-id="51c5d-119">**-n (or --name)**.</span></span> <span data-ttu-id="51c5d-120">Имя новой группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="51c5d-120">Name for the new NSG.</span></span> <span data-ttu-id="51c5d-121">В данном сценарии это *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="51c5d-121">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="51c5d-122">Выполните команду **`azure network nsg rule create`** , чтобы создать правило, которое разрешает доступ к точке 3389 (RDP) из Интернета.</span><span class="sxs-lookup"><span data-stu-id="51c5d-122">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 3389 (RDP) from the Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="51c5d-123">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="51c5d-123">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : rdp-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 3389
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="51c5d-124">Параметры</span><span class="sxs-lookup"><span data-stu-id="51c5d-124">Parameters:</span></span>
   
   * <span data-ttu-id="51c5d-125">**-a (или --nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="51c5d-125">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="51c5d-126">Имя сетевой группы безопасности, в которой будет создано правило.</span><span class="sxs-lookup"><span data-stu-id="51c5d-126">Name of the NSG in which the rule will be created.</span></span> <span data-ttu-id="51c5d-127">В данном сценарии это *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="51c5d-127">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="51c5d-128">**-n (или --name)**.</span><span class="sxs-lookup"><span data-stu-id="51c5d-128">**-n (or --name)**.</span></span> <span data-ttu-id="51c5d-129">Имя нового правила.</span><span class="sxs-lookup"><span data-stu-id="51c5d-129">Name for the new rule.</span></span> <span data-ttu-id="51c5d-130">В данном сценарии это *rdp-rule*.</span><span class="sxs-lookup"><span data-stu-id="51c5d-130">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="51c5d-131">**-c (или --action)**.</span><span class="sxs-lookup"><span data-stu-id="51c5d-131">**-c (or --action)**.</span></span> <span data-ttu-id="51c5d-132">Уровень доступа для правила (Deny или Allow).</span><span class="sxs-lookup"><span data-stu-id="51c5d-132">Access level for the rule (Deny or Allow).</span></span>
   * <span data-ttu-id="51c5d-133">**-p (или --protocol)**.</span><span class="sxs-lookup"><span data-stu-id="51c5d-133">**-p (or --protocol)**.</span></span> <span data-ttu-id="51c5d-134">Протокол (Tcp, Udp или *) для правила.</span><span class="sxs-lookup"><span data-stu-id="51c5d-134">Protocol (Tcp, Udp, or *) for the rule.</span></span>
   * <span data-ttu-id="51c5d-135">**-r (или --type)**.</span><span class="sxs-lookup"><span data-stu-id="51c5d-135">**-r (or --type)**.</span></span> <span data-ttu-id="51c5d-136">Направление подключения (Inbound или Outbound).</span><span class="sxs-lookup"><span data-stu-id="51c5d-136">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="51c5d-137">**-y (или --priority)**.</span><span class="sxs-lookup"><span data-stu-id="51c5d-137">**-y (or --priority)**.</span></span> <span data-ttu-id="51c5d-138">Приоритет правила.</span><span class="sxs-lookup"><span data-stu-id="51c5d-138">Priority for the rule.</span></span>
   * <span data-ttu-id="51c5d-139">**-f (или --source-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="51c5d-139">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="51c5d-140">Префикс адреса источника в CIDR или использование тегов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="51c5d-140">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="51c5d-141">**-o (или --source-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="51c5d-141">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="51c5d-142">Исходный порт или диапазон портов.</span><span class="sxs-lookup"><span data-stu-id="51c5d-142">Source port, or port range.</span></span>
   * <span data-ttu-id="51c5d-143">**-e (или --destination-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="51c5d-143">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="51c5d-144">Префикс адреса назначения в CIDR или использование тегов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="51c5d-144">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="51c5d-145">**-u (или --destination-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="51c5d-145">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="51c5d-146">Конечный порт или диапазон портов.</span><span class="sxs-lookup"><span data-stu-id="51c5d-146">Destination port, or port range.</span></span>
5. <span data-ttu-id="51c5d-147">Выполните команду **`azure network nsg rule create`** , чтобы создать правило, которое разрешает доступ к порту 80 (HTTP) из Интернета.</span><span class="sxs-lookup"><span data-stu-id="51c5d-147">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 80 (HTTP) from the Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="51c5d-148">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="51c5d-148">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="51c5d-149">Выполните команду **`azure network nsg subnet add`** , чтобы связать сетевую группу безопасности с подсетью переднего плана.</span><span class="sxs-lookup"><span data-stu-id="51c5d-149">Run the **`azure network nsg subnet add`** command to link the NSG to the front end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    <span data-ttu-id="51c5d-150">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="51c5d-150">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="51c5d-151">Как создать группу безопасности сети для внутренней подсети</span><span class="sxs-lookup"><span data-stu-id="51c5d-151">How to create the NSG for the back end subnet</span></span>
<span data-ttu-id="51c5d-152">Чтобы создать сетевую группу безопасности под названием *NSG-BackEnd* по описанному выше сценарию, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="51c5d-152">To create an NSG named named *NSG-BackEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="51c5d-153">Запустите команду **`azure network nsg create`** , чтобы создать сетевую группу безопасности.</span><span class="sxs-lookup"><span data-stu-id="51c5d-153">Run the **`azure network nsg create`** command to create an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    <span data-ttu-id="51c5d-154">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="51c5d-154">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : NSG-BackEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="51c5d-155">Параметры</span><span class="sxs-lookup"><span data-stu-id="51c5d-155">Parameters:</span></span>
   
   * <span data-ttu-id="51c5d-156">**-l (или --location)**.</span><span class="sxs-lookup"><span data-stu-id="51c5d-156">**-l (or --location)**.</span></span> <span data-ttu-id="51c5d-157">Регион Azure, в котором будет создана группа безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="51c5d-157">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="51c5d-158">В нашем случае это *westus*.</span><span class="sxs-lookup"><span data-stu-id="51c5d-158">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="51c5d-159">**-n (или --name)**.</span><span class="sxs-lookup"><span data-stu-id="51c5d-159">**-n (or --name)**.</span></span> <span data-ttu-id="51c5d-160">Имя новой группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="51c5d-160">Name for the new NSG.</span></span> <span data-ttu-id="51c5d-161">В данном сценарии это *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="51c5d-161">For our scenario, *NSG-FrontEnd*.</span></span>
2. <span data-ttu-id="51c5d-162">Выполните команду **`azure network nsg rule create`** , чтобы создать правило, которое разрешает доступ к порту 1433 (SQL) из подсети переднего плана.</span><span class="sxs-lookup"><span data-stu-id="51c5d-162">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 1433 (SQL) from the front end subnet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="51c5d-163">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="51c5d-163">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : sql-rule
        data:    Source address prefix           : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 1433
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="51c5d-164">Выполните команду **`azure network nsg rule create`** , чтобы создать правило, которое запрещает доступ к Интернету.</span><span class="sxs-lookup"><span data-stu-id="51c5d-164">Run the **`azure network nsg rule create`** command to create a rule that denies access to the Internet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    <span data-ttu-id="51c5d-165">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="51c5d-165">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : *
        data:    Source Port                     : *
        data:    Destination address prefix      : INTERNET
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Outbound
        data:    Action                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="51c5d-166">Выполните команду **`azure network nsg subnet add`** , чтобы связать сетевую группу безопасности с внутренней подсетью.</span><span class="sxs-lookup"><span data-stu-id="51c5d-166">Run the **`azure network nsg subnet add`** command to link the NSG to the back end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    <span data-ttu-id="51c5d-167">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="51c5d-167">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up the network security group "NSG-BackEndX"
        info:    Looking up the subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

