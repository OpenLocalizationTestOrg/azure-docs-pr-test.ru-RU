---
title: "aaaCreate виртуальной сети Azure (классические) с несколькими подсетями | Документы Microsoft"
description: "Узнайте, как toocreate виртуальной сети (классической) с несколькими подсетями в Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a><span data-ttu-id="40401-103">Создание (классической) виртуальной сети с несколькими подсетями</span><span class="sxs-lookup"><span data-stu-id="40401-103">Create a virtual network (classic) with multiple subnets</span></span>

> [!IMPORTANT]
> <span data-ttu-id="40401-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="40401-104">Azure has two [different deployment models](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="40401-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="40401-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="40401-106">Корпорация Майкрософт рекомендует создать большинство новые виртуальные сети через hello [диспетчера ресурсов](virtual-networks-create-vnet-arm-pportal.md) модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="40401-106">Microsoft recommends creating most new virtual networks through hello [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) deployment model.</span></span>

<span data-ttu-id="40401-107">В этом учебнике показано, как toocreate основные виртуальной сети Azure (классические), имеющий разделения открытых и закрытых подсетей.</span><span class="sxs-lookup"><span data-stu-id="40401-107">In this tutorial, learn how toocreate a basic Azure virtual network (classic) that has separate public and private subnets.</span></span> <span data-ttu-id="40401-108">Ресурсы Azure, такие как виртуальные машины и облачные службы, можно создавать в подсети.</span><span class="sxs-lookup"><span data-stu-id="40401-108">You can create Azure resources, like Virtual machines and Cloud services in a subnet.</span></span> <span data-ttu-id="40401-109">Ресурсы, созданные в виртуальных сетях (классические) могут взаимодействовать друг с другом и с ресурсами в других сетях подключенных tooa виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="40401-109">Resources created in virtual networks (classic) can communicate with each other, and with resources in other networks connected tooa virtual network.</span></span>

<span data-ttu-id="40401-110">Дополнительные сведения обо всех параметрах виртуальной сети и подсети см. в [этой](virtual-network-manage-network.md) и [этой](virtual-network-manage-subnet.md) статье.</span><span class="sxs-lookup"><span data-stu-id="40401-110">Learn more about all [virtual network](virtual-network-manage-network.md) and [subnet](virtual-network-manage-subnet.md) settings.</span></span>

> [!WARNING]
> <span data-ttu-id="40401-111">При [отключении подписки](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit) классические виртуальные сети сразу же удаляются Azure</span><span class="sxs-lookup"><span data-stu-id="40401-111">Virtual networks (classic) are immediately deleted by Azure when a [subscription is disabled](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span></span> <span data-ttu-id="40401-112">Виртуальные сети (классической) удаляются независимо от того, существуют ли ресурсов в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="40401-112">Virtual networks (classic) are deleted regardless of whether resources exist in hello virtual network.</span></span> <span data-ttu-id="40401-113">Если после повторного включения подписки hello, необходимо повторно создать ресурсы, которые существовали в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="40401-113">If you later re-enable hello subscription, resources that existed in hello virtual network must be recreated.</span></span>

<span data-ttu-id="40401-114">Можно создать виртуальную сеть (классические) с помощью hello [портал Azure](#portal), hello [Azure командной строки (CLI) 1.0](#azure-cli), или [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="40401-114">You can create a virtual network (classic) by using hello [Azure portal](#portal), hello [Azure command-line interface (CLI) 1.0](#azure-cli), or [PowerShell](#powershell).</span></span>

## <a name="portal"></a><span data-ttu-id="40401-115">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="40401-115">Portal</span></span>

1. <span data-ttu-id="40401-116">В веб-браузере перейдите toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="40401-116">In an Internet browser, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="40401-117">Войдите с использованием [учетной записи Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="40401-117">Log in using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="40401-118">Если у вас нет учетной записи Azure, вы можете зарегистрироваться и получить [бесплатную пробную версию](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="40401-118">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="40401-119">Нажмите кнопку **+ создать** hello портала.</span><span class="sxs-lookup"><span data-stu-id="40401-119">Click **+New** in hello portal.</span></span>
3. <span data-ttu-id="40401-120">Введите *виртуальная сеть* в hello **поиска hello Marketplace** поле вверху hello hello **New** колонки, отображается.</span><span class="sxs-lookup"><span data-stu-id="40401-120">Enter *Virtual network* in hello **Search hello Marketplace** box at hello top of hello **New** blade that appears.</span></span>  <span data-ttu-id="40401-121">Нажмите кнопку **виртуальная сеть** когда он появится в результатах поиска hello.</span><span class="sxs-lookup"><span data-stu-id="40401-121">Click **Virtual network** when it appears in hello search results.</span></span>
4. <span data-ttu-id="40401-122">Выберите **классический** в hello **выберите модель развертывания** поле в hello **виртуальной сети** колонки, отображается, нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="40401-122">Select **Classic** in hello **Select a deployment model** box in hello **Virtual Network** blade that appears, then click **Create**.</span></span> 
5. <span data-ttu-id="40401-123">Введите следующие значения на hello hello **Создание виртуальной сети (классические)** колонку и нажмите кнопку **создать**:</span><span class="sxs-lookup"><span data-stu-id="40401-123">Enter hello following values on hello **Create virtual network (classic)** blade and then click **Create**:</span></span>

    |<span data-ttu-id="40401-124">Настройка</span><span class="sxs-lookup"><span data-stu-id="40401-124">Setting</span></span>|<span data-ttu-id="40401-125">Значение</span><span class="sxs-lookup"><span data-stu-id="40401-125">Value</span></span>|
    |---|---|
    |<span data-ttu-id="40401-126">Имя</span><span class="sxs-lookup"><span data-stu-id="40401-126">Name</span></span>|<span data-ttu-id="40401-127">myVnet</span><span class="sxs-lookup"><span data-stu-id="40401-127">myVnet</span></span>|
    |<span data-ttu-id="40401-128">Пространство адресов</span><span class="sxs-lookup"><span data-stu-id="40401-128">Address space</span></span>|<span data-ttu-id="40401-129">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="40401-129">10.0.0.0/16</span></span>|
    |<span data-ttu-id="40401-130">Имя подсети</span><span class="sxs-lookup"><span data-stu-id="40401-130">Subnet name</span></span>|<span data-ttu-id="40401-131">Общедоступные</span><span class="sxs-lookup"><span data-stu-id="40401-131">Public</span></span>|
    |<span data-ttu-id="40401-132">Диапазон адресов подсети</span><span class="sxs-lookup"><span data-stu-id="40401-132">Subnet address range</span></span>|<span data-ttu-id="40401-133">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="40401-133">10.0.0.0/24</span></span>|
    |<span data-ttu-id="40401-134">Группа ресурсов</span><span class="sxs-lookup"><span data-stu-id="40401-134">Resource group</span></span>|<span data-ttu-id="40401-135">Оставьте выбранным пункт **Создать**, а затем введите **MyResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="40401-135">Leave **Create new** selected, and then enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="40401-136">Подписка и расположение</span><span class="sxs-lookup"><span data-stu-id="40401-136">Subscription and location</span></span>|<span data-ttu-id="40401-137">Выберите подписку и расположение.</span><span class="sxs-lookup"><span data-stu-id="40401-137">Select your subscription and location.</span></span>

    <span data-ttu-id="40401-138">Если вы новый tooAzure, Дополнительные сведения о [групп ресурсов](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [подписки](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), и [расположения](https://azure.microsoft.com/regions) (также называется tooas *областей*).</span><span class="sxs-lookup"><span data-stu-id="40401-138">If you're new tooAzure, learn more about [resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (also referred tooas *regions*).</span></span>
4. <span data-ttu-id="40401-139">На портале hello при создании виртуальной сети можно создать только одну подсеть.</span><span class="sxs-lookup"><span data-stu-id="40401-139">In hello portal, you can create only one subnet when you create a virtual network.</span></span> <span data-ttu-id="40401-140">В этом учебнике создается второй подсети после создания виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="40401-140">In this tutorial, you create a second subnet after you create hello virtual network.</span></span> <span data-ttu-id="40401-141">Позже может создать ресурсы, доступном через Интернет в hello **открытый** подсети.</span><span class="sxs-lookup"><span data-stu-id="40401-141">You might later create Internet-accessible resources in hello **Public** subnet.</span></span> <span data-ttu-id="40401-142">Можно также создать ресурсы, которые недоступны из hello Интернета в hello **закрытый** подсети.</span><span class="sxs-lookup"><span data-stu-id="40401-142">You also might create resources that aren't accessible from hello Internet in hello **Private** subnet.</span></span> <span data-ttu-id="40401-143">toocreate Здравствуйте вторую подсеть, введите **myVnet** в hello **Найдите ресурсы** поле вверху hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="40401-143">toocreate hello second subnet, enter **myVnet** in hello **Search resources** box at hello top of hello page.</span></span> <span data-ttu-id="40401-144">Нажмите кнопку **myVnet** когда он появится в результатах поиска hello.</span><span class="sxs-lookup"><span data-stu-id="40401-144">Click **myVnet** when it appears in hello search results.</span></span>
5. <span data-ttu-id="40401-145">Нажмите кнопку **подсети** (в hello **параметры** раздела) на hello **Создание виртуальной сети (классические)** колонки, отображается.</span><span class="sxs-lookup"><span data-stu-id="40401-145">Click **Subnets** (in hello **SETTINGS** section) on hello **Create virtual network (classic)** blade that appears.</span></span>
6. <span data-ttu-id="40401-146">Нажмите кнопку **+ добавить** на hello **myVnet - подсети** колонки, отображается.</span><span class="sxs-lookup"><span data-stu-id="40401-146">Click **+Add** on hello **myVnet - Subnets** blade that appears.</span></span>
7. <span data-ttu-id="40401-147">Введите **закрытый** для **имя** на hello **добавить подсеть** колонку.</span><span class="sxs-lookup"><span data-stu-id="40401-147">Enter **Private** for **Name** on hello **Add subnet** blade.</span></span> <span data-ttu-id="40401-148">Для **Диапазон адресов** введите **10.0.1.0/24**.</span><span class="sxs-lookup"><span data-stu-id="40401-148">Enter **10.0.1.0/24** for **Address range**.</span></span>  <span data-ttu-id="40401-149">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="40401-149">Click **OK**.</span></span>
8. <span data-ttu-id="40401-150">На hello **myVnet - подсети** колонку, вы увидите hello **открытый** и **закрытый** подсети, которые были созданы.</span><span class="sxs-lookup"><span data-stu-id="40401-150">On hello **myVnet - Subnets** blade, you can see hello **Public** and **Private** subnets that you created.</span></span>
9. <span data-ttu-id="40401-151">**Необязательный**: после завершения этого учебника, может потребоваться toodelete hello ресурсы, которые были созданы, чтобы не будет взиматься плата за использование:</span><span class="sxs-lookup"><span data-stu-id="40401-151">**Optional**: When you finish this tutorial, you might want toodelete hello resources that you created, so that you don't incur usage charges:</span></span>
    - <span data-ttu-id="40401-152">Нажмите кнопку **Обзор** на hello **myVnet** колонку.</span><span class="sxs-lookup"><span data-stu-id="40401-152">Click **Overview** on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="40401-153">Нажмите кнопку hello **удаление** значок hello **myVnet** колонку.</span><span class="sxs-lookup"><span data-stu-id="40401-153">Click hello **Delete** icon on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="40401-154">tooconfirm hello удаления, нажмите кнопку **Да** в hello **удаления виртуальной сети** поле.</span><span class="sxs-lookup"><span data-stu-id="40401-154">tooconfirm hello deletion, click **Yes** in hello **Delete virtual network** box.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="40401-155">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="40401-155">Azure CLI</span></span>

1. <span data-ttu-id="40401-156">Вы можете либо [Установка и настройка hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), или использовать hello CLI в hello оболочки облако Azure.</span><span class="sxs-lookup"><span data-stu-id="40401-156">You can either [install and configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), or use hello CLI within hello Azure Cloud Shell.</span></span> <span data-ttu-id="40401-157">Hello оболочки облако Azure — это бесплатные Bash, который выполняется непосредственно в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="40401-157">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="40401-158">Он имеет hello Azure CLI предварительно установить и настроить toouse с вашей учетной записью.</span><span class="sxs-lookup"><span data-stu-id="40401-158">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="40401-159">Введите tooget справочные сведения о командах CLI, `azure <command> --help`.</span><span class="sxs-lookup"><span data-stu-id="40401-159">tooget help for CLI commands, type `azure <command> --help`.</span></span> 
2. <span data-ttu-id="40401-160">В сеансе CLI вход tooAzure командой hello ниже.</span><span class="sxs-lookup"><span data-stu-id="40401-160">In a CLI session, log in tooAzure with hello command that follows.</span></span> <span data-ttu-id="40401-161">Если щелкнуть **опробовать** hello флажок ниже, открывается оболочки облака.</span><span class="sxs-lookup"><span data-stu-id="40401-161">If you click **Try it** in hello box below, a Cloud Shell opens.</span></span> <span data-ttu-id="40401-162">Вы можете войти tooyour подписки Azure, не вводя hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="40401-162">You can log in tooyour Azure subscription, without entering hello following command:</span></span>

    ```azurecli-interactive
    azure login
    ```

3. <span data-ttu-id="40401-163">hello tooensure CLI находится в режиме управления службой, введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="40401-163">tooensure hello CLI is in Service Management mode, enter hello following command:</span></span>

    ```azurecli-interactive
    azure config mode asm
    ```

4. <span data-ttu-id="40401-164">Создайте виртуальную сеть с частной подсетью:</span><span class="sxs-lookup"><span data-stu-id="40401-164">Create a virtual network with a private subnet:</span></span>

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. <span data-ttu-id="40401-165">Создание общей подсети в виртуальной сети hello:</span><span class="sxs-lookup"><span data-stu-id="40401-165">Create a public subnet within hello virtual network:</span></span>

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. <span data-ttu-id="40401-166">Просмотрите hello виртуальную сеть и подсети.</span><span class="sxs-lookup"><span data-stu-id="40401-166">Review hello virtual network and subnets:</span></span>

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. <span data-ttu-id="40401-167">**Необязательный**: toodelete hello ресурсы, созданные после завершения этого учебника, чтобы не будет взиматься плата за использование может потребоваться:</span><span class="sxs-lookup"><span data-stu-id="40401-167">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges:</span></span>

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> <span data-ttu-id="40401-168">Хотя нельзя указать toocreate группы ресурсов виртуальной сети (классической) с помощью hello CLI, Azure создает виртуальную сеть hello в группе ресурсов с именем *сети по умолчанию*.</span><span class="sxs-lookup"><span data-stu-id="40401-168">Though you can't specify a resource group toocreate a virtual network (classic) in using hello CLI, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

## <a name="powershell"></a><span data-ttu-id="40401-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="40401-169">PowerShell</span></span>

1. <span data-ttu-id="40401-170">Установите последнюю версию hello hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) модуля.</span><span class="sxs-lookup"><span data-stu-id="40401-170">Install hello latest version of hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) module.</span></span> <span data-ttu-id="40401-171">Если у вас отсутствует новый tooAzure PowerShell, [Обзор Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="40401-171">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="40401-172">Запустите сеанс PowerShell.</span><span class="sxs-lookup"><span data-stu-id="40401-172">Start a PowerShell session.</span></span>
3. <span data-ttu-id="40401-173">В PowerShell, войдите в tooAzure, указав hello `Add-AzureAccount` команды.</span><span class="sxs-lookup"><span data-stu-id="40401-173">In PowerShell, log in tooAzure by entering hello `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="40401-174">Изменить hello следующий путь и имя файла, при необходимости экспортировать существующий файл конфигурации сети:</span><span class="sxs-lookup"><span data-stu-id="40401-174">Change hello following path and filename, as appropriate, then export your existing network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. <span data-ttu-id="40401-175">toocreate виртуальная сеть с общедоступных и частных подсетях, используйте любой текстовый редактор tooadd hello **VirtualNetworkSite** элемента, следующего toohello файла конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="40401-175">toocreate a virtual network with public and private subnets, use any text editor tooadd hello **VirtualNetworkSite** element that follows toohello network configuration file.</span></span>

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    <span data-ttu-id="40401-176">Просмотрите hello полного [схема файла конфигурации сети](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="40401-176">Review hello full [network configuration file schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

6. <span data-ttu-id="40401-177">Импорт файла конфигурации сети hello:</span><span class="sxs-lookup"><span data-stu-id="40401-177">Import hello network configuration file:</span></span>

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > <span data-ttu-id="40401-178">Импорт файла конфигурации сети измененные может привести к изменения tooexisting виртуальные сети (классической) для вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="40401-178">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="40401-179">Убедитесь в добавлении hello предыдущих виртуальной сети и не изменить или удалить все существующие виртуальные сети из подписки.</span><span class="sxs-lookup"><span data-stu-id="40401-179">Ensure you only add hello previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

7. <span data-ttu-id="40401-180">Просмотрите hello виртуальную сеть и подсети.</span><span class="sxs-lookup"><span data-stu-id="40401-180">Review hello virtual network and subnets:</span></span>

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. <span data-ttu-id="40401-181">**Необязательный**: может потребоваться toodelete hello ресурсы, созданные после завершения этого учебника, чтобы не будет взиматься плата за использование.</span><span class="sxs-lookup"><span data-stu-id="40401-181">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges.</span></span> <span data-ttu-id="40401-182">toodelete hello виртуальной сети, полный шаги 4 – 6, это время удаления hello **VirtualNetworkSite** элемент, добавленный на шаге 5.</span><span class="sxs-lookup"><span data-stu-id="40401-182">toodelete hello virtual network, complete steps 4-6 again, this time removing hello **VirtualNetworkSite** element you added in step 5.</span></span>
 
> [!NOTE]
> <span data-ttu-id="40401-183">Хотя нельзя указать toocreate группы ресурсов виртуальной сети (классической) с помощью PowerShell, Azure создает виртуальную сеть hello в группе ресурсов с именем *сети по умолчанию*.</span><span class="sxs-lookup"><span data-stu-id="40401-183">Though you can't specify a resource group toocreate a virtual network (classic) in using PowerShell, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="40401-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="40401-184">Next steps</span></span>

- <span data-ttu-id="40401-185">toolearn о все параметры виртуальной сети и подсети, в разделе [управлять виртуальными сетями](virtual-network-manage-network.md) и [управление подсети виртуальной сети](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="40401-185">toolearn about all virtual network and subnet settings, see [Manage virtual networks](virtual-network-manage-network.md) and [Manage virtual network subnets](virtual-network-manage-subnet.md).</span></span> <span data-ttu-id="40401-186">Имеются различные варианты использования виртуальных сетей и подсетей в рабочей среде toomeet различные требования к среде.</span><span class="sxs-lookup"><span data-stu-id="40401-186">You have various options for using virtual networks and subnets in a production environment toomeet different requirements.</span></span>
- <span data-ttu-id="40401-187">toofilter входящего и исходящего трафика подсети, создание и применение [сетевых групп безопасности](virtual-networks-nsg.md) toosubnets.</span><span class="sxs-lookup"><span data-stu-id="40401-187">toofilter inbound and outbound subnet traffic, create and apply [network security groups](virtual-networks-nsg.md) toosubnets.</span></span>
- <span data-ttu-id="40401-188">Создание [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) или [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) виртуальной машины и подключите его tooan существующей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="40401-188">Create a [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or a [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machine, and then connect it tooan existing virtual network.</span></span>
- <span data-ttu-id="40401-189">tooconnect двух виртуальных сетей в hello же расположению Azure, создание [виртуальную сеть пиринга](create-peering-different-deployment-models.md) между виртуальными сетями hello.</span><span class="sxs-lookup"><span data-stu-id="40401-189">tooconnect two virtual networks in hello same Azure location, create a  [virtual network peering](create-peering-different-deployment-models.md) between hello virtual networks.</span></span> <span data-ttu-id="40401-190">Можно установить равноправное подключение к виртуальной сети (диспетчера ресурсов) tooa виртуальной сети (классические), но не удается создать пиринг между двумя виртуальными сетями (классические).</span><span class="sxs-lookup"><span data-stu-id="40401-190">You can peer a virtual network (Resource Manager) tooa virtual network (classic), but you cannot create a peering between two virtual networks (classic).</span></span>
- <span data-ttu-id="40401-191">Подключения hello виртуальной сети tooan в локальной сети с помощью [VPN-шлюз](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) или [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) канала.</span><span class="sxs-lookup"><span data-stu-id="40401-191">Connect hello virtual network tooan on-premises network by using a [VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span></span>
