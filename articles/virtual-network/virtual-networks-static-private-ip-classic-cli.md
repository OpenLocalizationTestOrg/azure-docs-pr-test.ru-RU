---
title: "aaaConfigure частных IP-адресов для виртуальных машин (обычная) — Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как tooconfigure частных IP-адресов для виртуальных машин (классические) с помощью hello Azure командной строки (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 417a57181bcf5c2e6101bf3bdf63fc94ebc99df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-cli-10"></a><span data-ttu-id="4438c-103">Настройка частного IP-адреса для виртуальной машины (классические) с помощью hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4438c-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="4438c-104">В этой статье рассматриваются hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="4438c-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="4438c-105">Вы также можете [управление статический частный IP-адрес в модели развертывания диспетчера ресурсов hello](virtual-networks-static-private-ip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4438c-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-cli.md).</span></span>

<span data-ttu-id="4438c-106">приведенную ниже команду Azure CLI Образец Hello ожидать простой среде уже создан.</span><span class="sxs-lookup"><span data-stu-id="4438c-106">hello sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="4438c-107">Если требуется toorun hello команд, отображаемых в этом документе, вначале построить hello тестовой среды, описанные в [создании виртуальной сети](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4438c-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="4438c-108">Как toospecify статических частных IP-адресов при создании виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="4438c-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="4438c-109">Новая виртуальная машина с именем toocreate *DNS01* в новой облачной службы с именем *TestService* на основании hello сценарии выше, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4438c-109">toocreate a new VM named *DNS01* in a new cloud service named *TestService* based on hello scenario above, follow these steps:</span></span>

1. <span data-ttu-id="4438c-110">Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="4438c-110">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="4438c-111">Запустите hello **создания службы azure** команды toocreate hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="4438c-111">Run hello **azure service create** command toocreate hello cloud service.</span></span>
   
        azure service create TestService --location uscentral
   
    <span data-ttu-id="4438c-112">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="4438c-112">Expected output:</span></span>
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. <span data-ttu-id="4438c-113">Запустите hello **azure создать ВМ** команда toocreate hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4438c-113">Run hello **azure create vm** command toocreate hello VM.</span></span> <span data-ttu-id="4438c-114">Обратите внимание, значение hello статический частный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="4438c-114">Notice hello value for a static private IP address.</span></span> <span data-ttu-id="4438c-115">Список Hello отображаться после вывода hello объясняется hello параметров, используемых.</span><span class="sxs-lookup"><span data-stu-id="4438c-115">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    <span data-ttu-id="4438c-116">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="4438c-116">Expected output:</span></span>
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting too"Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * <span data-ttu-id="4438c-117">**-l (или --location)**.</span><span class="sxs-lookup"><span data-stu-id="4438c-117">**-l (or --location)**.</span></span> <span data-ttu-id="4438c-118">Регион Azure, где будут создаваться hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4438c-118">Azure region where hello VM will be created.</span></span> <span data-ttu-id="4438c-119">В данном случае это — *centralus*.</span><span class="sxs-lookup"><span data-stu-id="4438c-119">For our scenario, *centralus*.</span></span>
   * <span data-ttu-id="4438c-120">**-n (или --vm-name)**.</span><span class="sxs-lookup"><span data-stu-id="4438c-120">**-n (or --vm-name)**.</span></span> <span data-ttu-id="4438c-121">Имя создания toobe ВМ hello.</span><span class="sxs-lookup"><span data-stu-id="4438c-121">Name of hello VM toobe created.</span></span>
   * <span data-ttu-id="4438c-122">**-w (или --virtual-network-name)**.</span><span class="sxs-lookup"><span data-stu-id="4438c-122">**-w (or --virtual-network-name)**.</span></span> <span data-ttu-id="4438c-123">Имя виртуальной сети, где будут создаваться hello ВМ hello.</span><span class="sxs-lookup"><span data-stu-id="4438c-123">Name of hello VNet where hello VM will be created.</span></span> 
   * <span data-ttu-id="4438c-124">**-S (или --static-ip)**.</span><span class="sxs-lookup"><span data-stu-id="4438c-124">**-S (or --static-ip)**.</span></span> <span data-ttu-id="4438c-125">Статический частный IP-адрес для hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4438c-125">Static private IP address for hello VM.</span></span>
   * <span data-ttu-id="4438c-126">**TestService**.</span><span class="sxs-lookup"><span data-stu-id="4438c-126">**TestService**.</span></span> <span data-ttu-id="4438c-127">Имя облачной службы hello, где будут создаваться hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4438c-127">Name of hello cloud service where hello VM will be created.</span></span>
   * <span data-ttu-id="4438c-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2.**</span><span class="sxs-lookup"><span data-stu-id="4438c-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span></span> <span data-ttu-id="4438c-129">Изображение, используемое toocreate hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4438c-129">Image used toocreate hello VM.</span></span>
   * <span data-ttu-id="4438c-130">**adminuser**.</span><span class="sxs-lookup"><span data-stu-id="4438c-130">**adminuser**.</span></span> <span data-ttu-id="4438c-131">Локальный администратор для виртуальной Машины Windows hello.</span><span class="sxs-lookup"><span data-stu-id="4438c-131">Local administrator for hello Windows VM.</span></span>
   * <span data-ttu-id="4438c-132">**AdminP@ssw0rd**.</span><span class="sxs-lookup"><span data-stu-id="4438c-132">**AdminP@ssw0rd**.</span></span> <span data-ttu-id="4438c-133">Пароль локального администратора для виртуальной Машины Windows hello.</span><span class="sxs-lookup"><span data-stu-id="4438c-133">Local administrator password for hello Windows VM.</span></span>

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="4438c-134">Как статических частных IP-tooretrieve адресов сведения для виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="4438c-134">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="4438c-135">tooview hello статических частного IP-адреса сведения для hello создания ВМ с hello-сценарий, приведенный выше, запустите следующую команду Azure CLI hello и просмотрите значение hello *StaticIP сети*:</span><span class="sxs-lookup"><span data-stu-id="4438c-135">tooview hello static private IP address information for hello VM created with hello script above, run hello following Azure CLI command and observe hello value for *Network StaticIP*:</span></span>

    azure vm static-ip show DNS01

<span data-ttu-id="4438c-136">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="4438c-136">Expected output:</span></span>

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="4438c-137">Как tooremove статических частных IP-адресов из виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="4438c-137">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="4438c-138">tooremove hello статический частный IP-адрес добавлен toohello ВМ в скрипте hello выше выполнения hello следующую команду Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="4438c-138">tooremove hello static private IP address added toohello VM in hello script above, run hello following Azure CLI command:</span></span>

    azure vm static-ip remove DNS01

<span data-ttu-id="4438c-139">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="4438c-139">Expected output:</span></span>

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-tooadd-a-static-private-ip-tooan-existing-vm"></a><span data-ttu-id="4438c-140">Как tooadd статических закрытый tooan IP существующей виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="4438c-140">How tooadd a static private IP tooan existing VM</span></span>
<span data-ttu-id="4438c-141">tooadd статические частного IP адрес toohello виртуальной Машины, созданной с помощью скрипта hello выше runt следующей команды:</span><span class="sxs-lookup"><span data-stu-id="4438c-141">tooadd a static private IP address toohello VM created using hello script above, runt he following command:</span></span>

    azure vm static-ip set DNS01 192.168.1.101

<span data-ttu-id="4438c-142">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="4438c-142">Expected output:</span></span>

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a><span data-ttu-id="4438c-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4438c-143">Next steps</span></span>
* <span data-ttu-id="4438c-144">Ознакомьтесь с информацией о [зарезервированных общедоступных IP-адресах](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="4438c-144">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="4438c-145">Узнайте об [общедоступных IP-адресах уровня экземпляра (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="4438c-145">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="4438c-146">Обратитесь к hello [зарезервированные интерфейсы REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="4438c-146">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

