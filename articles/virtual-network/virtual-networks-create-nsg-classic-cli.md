---
title: "Здравствуйте, toocreate aaaHow Nsg в классическом режиме с помощью Azure CLI | Документы Microsoft"
description: "Узнайте, как toocreate и развернуть Nsg в классическом режиме, с помощью hello Azure CLI"
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
ms.openlocfilehash: eb78861e10a0dd950bb2c3783ee957d1cce55016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-nsgs-classic-in-hello-azure-cli"></a><span data-ttu-id="ae7bf-103">Как toocreate Nsg (классической) для hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ae7bf-103">How toocreate NSGs (classic) in hello Azure CLI</span></span>
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="ae7bf-104">В этой статье рассматриваются hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="ae7bf-105">Вы также можете [создать Nsg в модели развертывания диспетчера ресурсов hello](virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ae7bf-105">You can also [create NSGs in hello Resource Manager deployment model](virtual-networks-create-nsg-arm-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="ae7bf-106">приведенную ниже команду Azure CLI Образец Hello ожидать простой среде уже создан на основании hello сценарии выше.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-106">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="ae7bf-107">Требуется toorun hello команд, отображаемых в этом документе, вначале построить hello тестовой среды, [создания виртуальной сети](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ae7bf-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment by [creating a VNet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="ae7bf-108">Как toocreate hello NSG для подсети hello переднего плана</span><span class="sxs-lookup"><span data-stu-id="ae7bf-108">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="ae7bf-109">toocreate с именем NSG с именем **NSG-FrontEnd** на основании hello сценарии выше, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-109">toocreate an NSG named named **NSG-FrontEnd** based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="ae7bf-110">Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-110">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="ae7bf-111">Запустите hello  **`azure config mode`**  tooswitch tooclassic команда режим, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-111">Run hello **`azure config mode`** command tooswitch tooclassic mode, as shown below.</span></span>
   
        azure config mode asm
   
    <span data-ttu-id="ae7bf-112">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ae7bf-112">Expected output:</span></span>
   
        info:    New mode is asm
3. <span data-ttu-id="ae7bf-113">Запустите hello  **`azure network nsg create`**  toocreate команда NSG.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-113">Run hello **`azure network nsg create`** command toocreate an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    <span data-ttu-id="ae7bf-114">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ae7bf-114">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="ae7bf-115">Параметры</span><span class="sxs-lookup"><span data-stu-id="ae7bf-115">Parameters:</span></span>
   
   * <span data-ttu-id="ae7bf-116">**-l (или --location)**.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-116">**-l (or --location)**.</span></span> <span data-ttu-id="ae7bf-117">Регион Azure, где hello новой NSG будет создан.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-117">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="ae7bf-118">В нашем случае это *westus*.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-118">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="ae7bf-119">**-n (или --name)**.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-119">**-n (or --name)**.</span></span> <span data-ttu-id="ae7bf-120">Имя для hello новая NSG.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-120">Name for hello new NSG.</span></span> <span data-ttu-id="ae7bf-121">В данном сценарии это *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-121">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="ae7bf-122">Запустите hello  **`azure network nsg rule create`**  toocreate команда правило, разрешающее доступ tooport 3389 (RDP) из Интернета hello.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-122">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 3389 (RDP) from hello Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="ae7bf-123">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ae7bf-123">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="ae7bf-124">Параметры</span><span class="sxs-lookup"><span data-stu-id="ae7bf-124">Parameters:</span></span>
   
   * <span data-ttu-id="ae7bf-125">**-a (или --nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-125">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="ae7bf-126">Имя в какие hello будет создано правило NSG hello.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-126">Name of hello NSG in which hello rule will be created.</span></span> <span data-ttu-id="ae7bf-127">В данном сценарии это *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-127">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="ae7bf-128">**-n (или --name)**.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-128">**-n (or --name)**.</span></span> <span data-ttu-id="ae7bf-129">Имя для нового правила hello.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-129">Name for hello new rule.</span></span> <span data-ttu-id="ae7bf-130">В нашем случае это *rdp-rule*.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-130">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="ae7bf-131">**-c (или --action)**.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-131">**-c (or --action)**.</span></span> <span data-ttu-id="ae7bf-132">Уровень доступа для правила hello (запретить или разрешить).</span><span class="sxs-lookup"><span data-stu-id="ae7bf-132">Access level for hello rule (Deny or Allow).</span></span>
   * <span data-ttu-id="ae7bf-133">**-p (или --protocol)**.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-133">**-p (or --protocol)**.</span></span> <span data-ttu-id="ae7bf-134">Протокол (Tcp, Udp или *) для правила hello.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-134">Protocol (Tcp, Udp, or *) for hello rule.</span></span>
   * <span data-ttu-id="ae7bf-135">**-r (или --type)**.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-135">**-r (or --type)**.</span></span> <span data-ttu-id="ae7bf-136">Направление подключения (Inbound или Outbound).</span><span class="sxs-lookup"><span data-stu-id="ae7bf-136">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="ae7bf-137">**-y (или --priority)**.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-137">**-y (or --priority)**.</span></span> <span data-ttu-id="ae7bf-138">Приоритет для правила hello.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-138">Priority for hello rule.</span></span>
   * <span data-ttu-id="ae7bf-139">**-f (или --source-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-139">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="ae7bf-140">Префикс адреса источника в CIDR или использование тегов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-140">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="ae7bf-141">**-o (или --source-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-141">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="ae7bf-142">Исходный порт или диапазон портов.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-142">Source port, or port range.</span></span>
   * <span data-ttu-id="ae7bf-143">**-e (или --destination-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-143">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="ae7bf-144">Префикс адреса назначения в CIDR или использование тегов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-144">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="ae7bf-145">**-u (или --destination-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-145">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="ae7bf-146">Конечный порт или диапазон портов.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-146">Destination port, or port range.</span></span>
5. <span data-ttu-id="ae7bf-147">Запустите hello  **`azure network nsg rule create`**  toocreate команда правило, разрешающее доступ tooport 80 (HTTP) из Интернета hello.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-147">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 80 (HTTP) from hello Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="ae7bf-148">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ae7bf-148">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
6. <span data-ttu-id="ae7bf-149">Запустите hello  **`azure network nsg subnet add`**  команда toolink hello NSG toohello внешнего интерфейса подсети.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-149">Run hello **`azure network nsg subnet add`** command toolink hello NSG toohello front end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    <span data-ttu-id="ae7bf-150">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ae7bf-150">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="ae7bf-151">Hello toocreate NSG для hello обратно конечного подсети</span><span class="sxs-lookup"><span data-stu-id="ae7bf-151">How toocreate hello NSG for hello back end subnet</span></span>
<span data-ttu-id="ae7bf-152">toocreate с именем NSG с именем *NSG серверной* на основании hello сценарии выше, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-152">toocreate an NSG named named *NSG-BackEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="ae7bf-153">Запустите hello  **`azure network nsg create`**  toocreate команда NSG.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-153">Run hello **`azure network nsg create`** command toocreate an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    <span data-ttu-id="ae7bf-154">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ae7bf-154">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
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
   
    <span data-ttu-id="ae7bf-155">Параметры</span><span class="sxs-lookup"><span data-stu-id="ae7bf-155">Parameters:</span></span>
   
   * <span data-ttu-id="ae7bf-156">**-l (или --location)**.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-156">**-l (or --location)**.</span></span> <span data-ttu-id="ae7bf-157">Регион Azure, где hello новой NSG будет создан.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-157">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="ae7bf-158">В нашем случае это *westus*.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-158">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="ae7bf-159">**-n (или --name)**.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-159">**-n (or --name)**.</span></span> <span data-ttu-id="ae7bf-160">Имя для hello новая NSG.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-160">Name for hello new NSG.</span></span> <span data-ttu-id="ae7bf-161">В данном сценарии это *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-161">For our scenario, *NSG-FrontEnd*.</span></span>
2. <span data-ttu-id="ae7bf-162">Запустите hello  **`azure network nsg rule create`**  toocreate команда правило, разрешающее доступ tooport 1433 (SQL) из подсети hello переднего плана.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-162">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 1433 (SQL) from hello front end subnet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="ae7bf-163">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ae7bf-163">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
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
3. <span data-ttu-id="ae7bf-164">Запустите hello  **`azure network nsg rule create`**  toocreate команда правило, запрещающее доступ toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-164">Run hello **`azure network nsg rule create`** command toocreate a rule that denies access toohello Internet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    <span data-ttu-id="ae7bf-165">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ae7bf-165">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
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
4. <span data-ttu-id="ae7bf-166">Запустите hello  **`azure network nsg subnet add`**  toohello NSG hello toolink обратно завершить подсети команды.</span><span class="sxs-lookup"><span data-stu-id="ae7bf-166">Run hello **`azure network nsg subnet add`** command toolink hello NSG toohello back end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    <span data-ttu-id="ae7bf-167">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ae7bf-167">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-BackEndX"
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

