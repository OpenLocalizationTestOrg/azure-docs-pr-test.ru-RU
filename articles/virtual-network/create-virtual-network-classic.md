---
title: "Создание (классической) виртуальной сети Azure с несколькими подсетями | Документация Майкрософт"
description: "Узнайте, как создать (классическую) виртуальную сеть с несколькими подсетями в Azure."
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
ms.openlocfilehash: 95c2f4fe40590a8d809f634fb5b2c92d07421bb0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a><span data-ttu-id="9a989-103">Создание (классической) виртуальной сети с несколькими подсетями</span><span class="sxs-lookup"><span data-stu-id="9a989-103">Create a virtual network (classic) with multiple subnets</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a989-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9a989-104">Azure has two [different deployment models](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="9a989-105">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="9a989-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="9a989-106">Для создания виртуальных сетей корпорация Майкрософт рекомендует использовать модель развертывания с помощью [Resource Manager](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="9a989-106">Microsoft recommends creating most new virtual networks through the [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) deployment model.</span></span>

<span data-ttu-id="9a989-107">В рамках этого руководства вы узнаете, как создать базовую (классическую) виртуальную сеть Azure с отдельными общедоступной и частной подсетями.</span><span class="sxs-lookup"><span data-stu-id="9a989-107">In this tutorial, learn how to create a basic Azure virtual network (classic) that has separate public and private subnets.</span></span> <span data-ttu-id="9a989-108">Ресурсы Azure, такие как виртуальные машины и облачные службы, можно создавать в подсети.</span><span class="sxs-lookup"><span data-stu-id="9a989-108">You can create Azure resources, like Virtual machines and Cloud services in a subnet.</span></span> <span data-ttu-id="9a989-109">Ресурсы, созданные в (классической) виртуальной сети, могут взаимодействовать друг с другом и с ресурсами в других сетях, подключенных к виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9a989-109">Resources created in virtual networks (classic) can communicate with each other, and with resources in other networks connected to a virtual network.</span></span>

<span data-ttu-id="9a989-110">Дополнительные сведения обо всех параметрах виртуальной сети и подсети см. в [этой](virtual-network-manage-network.md) и [этой](virtual-network-manage-subnet.md) статье.</span><span class="sxs-lookup"><span data-stu-id="9a989-110">Learn more about all [virtual network](virtual-network-manage-network.md) and [subnet](virtual-network-manage-subnet.md) settings.</span></span>

> [!WARNING]
> <span data-ttu-id="9a989-111">При [отключении подписки](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit) классические виртуальные сети сразу же удаляются Azure</span><span class="sxs-lookup"><span data-stu-id="9a989-111">Virtual networks (classic) are immediately deleted by Azure when a [subscription is disabled](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span></span> <span data-ttu-id="9a989-112">независимо от наличия ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9a989-112">Virtual networks (classic) are deleted regardless of whether resources exist in the virtual network.</span></span> <span data-ttu-id="9a989-113">После повторного включения подписки необходимо повторно создать ресурсы, находившиеся в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9a989-113">If you later re-enable the subscription, resources that existed in the virtual network must be recreated.</span></span>

<span data-ttu-id="9a989-114">Классическую виртуальную сеть можно создать с помощью [портала Azure](#portal), [командной строки (CLI) Azure 1.0](#azure-cli) или [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="9a989-114">You can create a virtual network (classic) by using the [Azure portal](#portal), the [Azure command-line interface (CLI) 1.0](#azure-cli), or [PowerShell](#powershell).</span></span>

## <a name="portal"></a><span data-ttu-id="9a989-115">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9a989-115">Portal</span></span>

1. <span data-ttu-id="9a989-116">С помощью браузера войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9a989-116">In an Internet browser, go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9a989-117">Войдите с использованием [учетной записи Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="9a989-117">Log in using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="9a989-118">Если у вас нет учетной записи Azure, вы можете зарегистрироваться и получить [бесплатную пробную версию](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="9a989-118">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="9a989-119">На портале нажмите кнопку **+ Создать**.</span><span class="sxs-lookup"><span data-stu-id="9a989-119">Click **+New** in the portal.</span></span>
3. <span data-ttu-id="9a989-120">В верхней части открывшейся колонки *Создать* в поле **Поиск по Marketplace** введите **виртуальная сеть**.</span><span class="sxs-lookup"><span data-stu-id="9a989-120">Enter *Virtual network* in the **Search the Marketplace** box at the top of the **New** blade that appears.</span></span>  <span data-ttu-id="9a989-121">Когда в результатах поиска появится пункт **Виртуальная сеть**, щелкните его.</span><span class="sxs-lookup"><span data-stu-id="9a989-121">Click **Virtual network** when it appears in the search results.</span></span>
4. <span data-ttu-id="9a989-122">В открывшейся колонке **Виртуальная сеть** в поле **Выбор модели развертывания** выберите **Классический** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9a989-122">Select **Classic** in the **Select a deployment model** box in the **Virtual Network** blade that appears, then click **Create**.</span></span> 
5. <span data-ttu-id="9a989-123">В колонке **Create virtual network (classic)** (Создать виртуальную сеть (классическую)) введите приведенные ниже значения, а затем щелкните **Создать**:</span><span class="sxs-lookup"><span data-stu-id="9a989-123">Enter the following values on the **Create virtual network (classic)** blade and then click **Create**:</span></span>

    |<span data-ttu-id="9a989-124">Настройка</span><span class="sxs-lookup"><span data-stu-id="9a989-124">Setting</span></span>|<span data-ttu-id="9a989-125">Значение</span><span class="sxs-lookup"><span data-stu-id="9a989-125">Value</span></span>|
    |---|---|
    |<span data-ttu-id="9a989-126">Имя</span><span class="sxs-lookup"><span data-stu-id="9a989-126">Name</span></span>|<span data-ttu-id="9a989-127">myVnet</span><span class="sxs-lookup"><span data-stu-id="9a989-127">myVnet</span></span>|
    |<span data-ttu-id="9a989-128">Пространство адресов</span><span class="sxs-lookup"><span data-stu-id="9a989-128">Address space</span></span>|<span data-ttu-id="9a989-129">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="9a989-129">10.0.0.0/16</span></span>|
    |<span data-ttu-id="9a989-130">Имя подсети</span><span class="sxs-lookup"><span data-stu-id="9a989-130">Subnet name</span></span>|<span data-ttu-id="9a989-131">Общедоступные</span><span class="sxs-lookup"><span data-stu-id="9a989-131">Public</span></span>|
    |<span data-ttu-id="9a989-132">Диапазон адресов подсети</span><span class="sxs-lookup"><span data-stu-id="9a989-132">Subnet address range</span></span>|<span data-ttu-id="9a989-133">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="9a989-133">10.0.0.0/24</span></span>|
    |<span data-ttu-id="9a989-134">Группа ресурсов</span><span class="sxs-lookup"><span data-stu-id="9a989-134">Resource group</span></span>|<span data-ttu-id="9a989-135">Оставьте выбранным пункт **Создать**, а затем введите **MyResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="9a989-135">Leave **Create new** selected, and then enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="9a989-136">Подписка и расположение</span><span class="sxs-lookup"><span data-stu-id="9a989-136">Subscription and location</span></span>|<span data-ttu-id="9a989-137">Выберите подписку и расположение.</span><span class="sxs-lookup"><span data-stu-id="9a989-137">Select your subscription and location.</span></span>

    <span data-ttu-id="9a989-138">Если вы еще не работали с Azure, ознакомьтесь со сведениями о [группах ресурсов](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [подписках](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) и [расположениях](https://azure.microsoft.com/regions) (которые также называются *регионами*).</span><span class="sxs-lookup"><span data-stu-id="9a989-138">If you're new to Azure, learn more about [resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (also referred to as *regions*).</span></span>
4. <span data-ttu-id="9a989-139">На портале при создании виртуальной сети можно создать только одну подсеть.</span><span class="sxs-lookup"><span data-stu-id="9a989-139">In the portal, you can create only one subnet when you create a virtual network.</span></span> <span data-ttu-id="9a989-140">В рамках этого руководства вы узнаете, как создать вторую подсеть после создания виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9a989-140">In this tutorial, you create a second subnet after you create the virtual network.</span></span> <span data-ttu-id="9a989-141">Позже вы можете создать ресурсы, доступные из Интернета, в **общедоступной** подсети.</span><span class="sxs-lookup"><span data-stu-id="9a989-141">You might later create Internet-accessible resources in the **Public** subnet.</span></span> <span data-ttu-id="9a989-142">Ресурсы, которые недоступны из Интернета, можно создать в **частной** подсети.</span><span class="sxs-lookup"><span data-stu-id="9a989-142">You also might create resources that aren't accessible from the Internet in the **Private** subnet.</span></span> <span data-ttu-id="9a989-143">Чтобы создать вторую подсеть, введите **myVnet** в поле **Поиск ресурсов** в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="9a989-143">To create the second subnet, enter **myVnet** in the **Search resources** box at the top of the page.</span></span> <span data-ttu-id="9a989-144">Когда сеть **myVnet** появится в результатах поиска, щелкните ее.</span><span class="sxs-lookup"><span data-stu-id="9a989-144">Click **myVnet** when it appears in the search results.</span></span>
5. <span data-ttu-id="9a989-145">В открывшейся колонке **Create virtual network (classic)** (Создание виртуальной сети (классическая)) щелкните **Подсети** (в разделе **Параметры**).</span><span class="sxs-lookup"><span data-stu-id="9a989-145">Click **Subnets** (in the **SETTINGS** section) on the **Create virtual network (classic)** blade that appears.</span></span>
6. <span data-ttu-id="9a989-146">В открывшейся колонке **myVnet — Подсети** щелкните **+Add** (+Добавить).</span><span class="sxs-lookup"><span data-stu-id="9a989-146">Click **+Add** on the **myVnet - Subnets** blade that appears.</span></span>
7. <span data-ttu-id="9a989-147">В колонке **Добавление подсети** для **имени** введите **Частное**.</span><span class="sxs-lookup"><span data-stu-id="9a989-147">Enter **Private** for **Name** on the **Add subnet** blade.</span></span> <span data-ttu-id="9a989-148">Для **Диапазон адресов** введите **10.0.1.0/24**.</span><span class="sxs-lookup"><span data-stu-id="9a989-148">Enter **10.0.1.0/24** for **Address range**.</span></span>  <span data-ttu-id="9a989-149">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9a989-149">Click **OK**.</span></span>
8. <span data-ttu-id="9a989-150">В колонке **myVnet — Подсети** отображаются созданные **общедоступная** и **частная** подсети.</span><span class="sxs-lookup"><span data-stu-id="9a989-150">On the **myVnet - Subnets** blade, you can see the **Public** and **Private** subnets that you created.</span></span>
9. <span data-ttu-id="9a989-151">**Необязательно.** По завершении работы с этим руководством может потребоваться удалить созданные ресурсы, чтобы за их использование не взималась плата:</span><span class="sxs-lookup"><span data-stu-id="9a989-151">**Optional**: When you finish this tutorial, you might want to delete the resources that you created, so that you don't incur usage charges:</span></span>
    - <span data-ttu-id="9a989-152">В колонке **myVnet** щелкните **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="9a989-152">Click **Overview** on the **myVnet** blade.</span></span>
    - <span data-ttu-id="9a989-153">В колонке **myVnet** щелкните значок **Удаление**.</span><span class="sxs-lookup"><span data-stu-id="9a989-153">Click the **Delete** icon on the **myVnet** blade.</span></span>
    - <span data-ttu-id="9a989-154">В окне **Удалить виртуальную сеть** нажмите кнопку **Да**, чтобы подтвердить удаление.</span><span class="sxs-lookup"><span data-stu-id="9a989-154">To confirm the deletion, click **Yes** in the **Delete virtual network** box.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="9a989-155">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="9a989-155">Azure CLI</span></span>

1. <span data-ttu-id="9a989-156">Вы можете [установить и настроить Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) или использовать интерфейс командной строки в Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="9a989-156">You can either [install and configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), or use the CLI within the Azure Cloud Shell.</span></span> <span data-ttu-id="9a989-157">Azure Cloud Shell — это бесплатная оболочка Bash, которую можно запускать непосредственно на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="9a989-157">The Azure Cloud Shell is a free Bash shell that you can run directly within the Azure portal.</span></span> <span data-ttu-id="9a989-158">Она включает предварительно установленный интерфейс Azure CLI и настроена для использования с вашей учетной записью.</span><span class="sxs-lookup"><span data-stu-id="9a989-158">It has the Azure CLI preinstalled and configured to use with your account.</span></span> <span data-ttu-id="9a989-159">Для получения справки по командам интерфейса командной строки введите `azure <command> --help`.</span><span class="sxs-lookup"><span data-stu-id="9a989-159">To get help for CLI commands, type `azure <command> --help`.</span></span> 
2. <span data-ttu-id="9a989-160">В сеансе интерфейса командной строки войдите в Azure, используя команду ниже.</span><span class="sxs-lookup"><span data-stu-id="9a989-160">In a CLI session, log in to Azure with the command that follows.</span></span> <span data-ttu-id="9a989-161">Если щелкнуть **Попробуйте!** в поле ниже, откроется Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="9a989-161">If you click **Try it** in the box below, a Cloud Shell opens.</span></span> <span data-ttu-id="9a989-162">Вы можете войти в подписку Azure, не вводя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9a989-162">You can log in to your Azure subscription, without entering the following command:</span></span>

    ```azurecli-interactive
    azure login
    ```

3. <span data-ttu-id="9a989-163">Чтобы убедиться, что интерфейс командной строки находится в режиме управления службами, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9a989-163">To ensure the CLI is in Service Management mode, enter the following command:</span></span>

    ```azurecli-interactive
    azure config mode asm
    ```

4. <span data-ttu-id="9a989-164">Создайте виртуальную сеть с частной подсетью:</span><span class="sxs-lookup"><span data-stu-id="9a989-164">Create a virtual network with a private subnet:</span></span>

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. <span data-ttu-id="9a989-165">Создайте общедоступную подсеть в виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="9a989-165">Create a public subnet within the virtual network:</span></span>

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. <span data-ttu-id="9a989-166">Создайте виртуальную сеть и подсети:</span><span class="sxs-lookup"><span data-stu-id="9a989-166">Review the virtual network and subnets:</span></span>

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. <span data-ttu-id="9a989-167">**Необязательно.** По завершении работы с этим руководством может потребоваться удалить созданные ресурсы, чтобы за их использование не взималась плата:</span><span class="sxs-lookup"><span data-stu-id="9a989-167">**Optional**: You might want to delete the resources that you created when you finish this tutorial, so that you don't incur usage charges:</span></span>

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> <span data-ttu-id="9a989-168">Нельзя указать группу ресурсов, в которой будет создана классическая виртуальная сеть, с помощью интерфейса командной строки. Azure создает виртуальную сеть в группе ресурсов с именем *Default-Networking*.</span><span class="sxs-lookup"><span data-stu-id="9a989-168">Though you can't specify a resource group to create a virtual network (classic) in using the CLI, Azure creates the virtual network in a resource group named *Default-Networking*.</span></span>

## <a name="powershell"></a><span data-ttu-id="9a989-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a989-169">PowerShell</span></span>

1. <span data-ttu-id="9a989-170">Установите последнюю версию модуля [Azure](https://www.powershellgallery.com/packages/Azure) PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9a989-170">Install the latest version of the PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) module.</span></span> <span data-ttu-id="9a989-171">Если вы еще не работали с Azure PowerShell, ознакомьтесь со статьей [Overview of Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json) (Общие сведения об Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="9a989-171">If you're new to Azure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="9a989-172">Запустите сеанс PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9a989-172">Start a PowerShell session.</span></span>
3. <span data-ttu-id="9a989-173">В PowerShell войдите в Azure, введя команду `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="9a989-173">In PowerShell, log in to Azure by entering the `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="9a989-174">Измените следующий путь и имя файла (при необходимости), а затем экспортируйте имеющийся файл конфигурации сети:</span><span class="sxs-lookup"><span data-stu-id="9a989-174">Change the following path and filename, as appropriate, then export your existing network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. <span data-ttu-id="9a989-175">Для создания виртуальной сети с общедоступной и частной подсетями воспользуйтесь любым текстовым редактором, чтобы добавить следующий элемент **VirtualNetworkSite** в файл конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="9a989-175">To create a virtual network with public and private subnets, use any text editor to add the **VirtualNetworkSite** element that follows to the network configuration file.</span></span>

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

    <span data-ttu-id="9a989-176">Просмотрите полную [схему файла конфигурации сети](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="9a989-176">Review the full [network configuration file schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

6. <span data-ttu-id="9a989-177">Импортируйте файл конфигурации сети:</span><span class="sxs-lookup"><span data-stu-id="9a989-177">Import the network configuration file:</span></span>

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > <span data-ttu-id="9a989-178">Импорт измененного файла конфигурации сети может привести к изменениям в классических виртуальных сетях в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="9a989-178">Importing a changed network configuration file can cause changes to existing virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="9a989-179">Убедитесь, что вы добавили только указанную выше виртуальную сеть и не изменили или удалили имеющиеся в своей подписке виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="9a989-179">Ensure you only add the previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

7. <span data-ttu-id="9a989-180">Создайте виртуальную сеть и подсети:</span><span class="sxs-lookup"><span data-stu-id="9a989-180">Review the virtual network and subnets:</span></span>

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. <span data-ttu-id="9a989-181">**Необязательно.** По завершении работы с этим руководством может потребоваться удалить созданные ресурсы, чтобы за их использование не взималась плата:</span><span class="sxs-lookup"><span data-stu-id="9a989-181">**Optional**: You might want to delete the resources that you created when you finish this tutorial, so that you don't incur usage charges.</span></span> <span data-ttu-id="9a989-182">Чтобы удалить виртуальную сеть, выполните шаги 4–6, но при этом удалите элемент **VirtualNetworkSite**, добавленный на шаге 5.</span><span class="sxs-lookup"><span data-stu-id="9a989-182">To delete the virtual network, complete steps 4-6 again, this time removing the **VirtualNetworkSite** element you added in step 5.</span></span>
 
> [!NOTE]
> <span data-ttu-id="9a989-183">Нельзя указать группу ресурсов, в которой будет создана классическая виртуальная сеть, с помощью PowerShell. Azure создает виртуальную сеть в группе ресурсов с именем *Default-Networking*.</span><span class="sxs-lookup"><span data-stu-id="9a989-183">Though you can't specify a resource group to create a virtual network (classic) in using PowerShell, Azure creates the virtual network in a resource group named *Default-Networking*.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="9a989-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9a989-184">Next steps</span></span>

- <span data-ttu-id="9a989-185">Дополнительные сведения о всех параметрах виртуальной сети и подсети см. в статьях [Создание, изменение или удаление виртуальных сетей](virtual-network-manage-network.md) и [Создание, изменение и удаление подсети в виртуальной сети](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="9a989-185">To learn about all virtual network and subnet settings, see [Manage virtual networks](virtual-network-manage-network.md) and [Manage virtual network subnets](virtual-network-manage-subnet.md).</span></span> <span data-ttu-id="9a989-186">Доступны различные варианты использования виртуальных сетей и подсетей в рабочей среде для соответствия различным требованиям.</span><span class="sxs-lookup"><span data-stu-id="9a989-186">You have various options for using virtual networks and subnets in a production environment to meet different requirements.</span></span>
- <span data-ttu-id="9a989-187">Вы можете фильтровать входящий и исходящий трафик подсети, создавая и применяя к ней [группы безопасности сети](virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="9a989-187">To filter inbound and outbound subnet traffic, create and apply [network security groups](virtual-networks-nsg.md) to subnets.</span></span>
- <span data-ttu-id="9a989-188">Создайте виртуальную машину [с Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) или [с Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json), а затем подключите ее к имеющейся виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9a989-188">Create a [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or a [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machine, and then connect it to an existing virtual network.</span></span>
- <span data-ttu-id="9a989-189">Чтобы подключить две виртуальные сети в одном расположении Azure, создайте [пиринг виртуальных сетей](create-peering-different-deployment-models.md) между ними.</span><span class="sxs-lookup"><span data-stu-id="9a989-189">To connect two virtual networks in the same Azure location, create a  [virtual network peering](create-peering-different-deployment-models.md) between the virtual networks.</span></span> <span data-ttu-id="9a989-190">Вы можете настроить пиринг между виртуальной сетью диспетчера ресурсов и классической виртуальной сетью, но не между двумя классическими виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="9a989-190">You can peer a virtual network (Resource Manager) to a virtual network (classic), but you cannot create a peering between two virtual networks (classic).</span></span>
- <span data-ttu-id="9a989-191">Чтобы подключить виртуальную сеть к локальной сети, используйте [VPN-шлюз](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) или канал [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9a989-191">Connect the virtual network to an on-premises network by using a [VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span></span>
