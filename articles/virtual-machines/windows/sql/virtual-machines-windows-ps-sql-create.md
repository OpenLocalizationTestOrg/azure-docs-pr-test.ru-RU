---
title: "Создание виртуальной машины SQL Server в Azure PowerShell (Resource Manager) | Документация Майкрософт"
description: "Содержит описание действий и сценарии PowerShell для создания виртуальной машины Azure на основе образа из коллекции образов виртуальных машин SQL Server."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: aa90a1d017af5f477407ab33f0580904472f412b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a><span data-ttu-id="72515-103">Подготовка виртуальной машины SQL Server к работе с помощью Azure PowerShell (в Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="72515-103">Provision a SQL Server virtual machine using Azure PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="72515-104">Портал</span><span class="sxs-lookup"><span data-stu-id="72515-104">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="72515-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="72515-105">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a><span data-ttu-id="72515-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="72515-106">Overview</span></span>
<span data-ttu-id="72515-107">В этом руководстве показано, как создать одну виртуальную машину Azure, используя модель развертывания с помощью **Azure Resource Manager** и командлеты Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72515-107">This tutorial shows you how to create a single Azure virtual machine using the **Azure Resource Manager** deployment model using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="72515-108">Мы создадим одну виртуальную машину, используя один диск из образа в коллекции SQL.</span><span class="sxs-lookup"><span data-stu-id="72515-108">In this tutorial, we will create a single virtual machine using a single disk drive from an image in the SQL Gallery.</span></span> <span data-ttu-id="72515-109">Мы также создадим новых поставщиков ресурсов хранения, сетевых и вычислительных ресурсов, которые будут использоваться виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="72515-109">We will create new providers for the storage, network, and compute resources that will be used by the virtual machine.</span></span> <span data-ttu-id="72515-110">Вы можете использовать существующие поставщики для любых из этих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="72515-110">If you have existing providers for any of these resources, you can use those providers instead.</span></span>

<span data-ttu-id="72515-111">Версию этого раздела для классической модели см. в статье [Подготовка виртуальной машины SQL Server к работе с помощью Azure PowerShell (классическая модель)](../classic/ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="72515-111">If you need the classic version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Classic](../classic/ps-sql-create.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72515-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="72515-112">Prerequisites</span></span>
<span data-ttu-id="72515-113">Для работы с этим руководством вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="72515-113">For this tutorial you'll need:</span></span>

* <span data-ttu-id="72515-114">Учетная запись Azure и подписка (еще до начала).</span><span class="sxs-lookup"><span data-stu-id="72515-114">An Azure account and subscription before you start.</span></span> <span data-ttu-id="72515-115">Если у вас ее нет, зарегистрируйтесь, чтобы [воспользоваться бесплатной пробной версией](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="72515-115">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="72515-116">[Azure PowerShell](/powershell/azure/overview)1.4.0 или более поздней версии (в этом учебнике использовалась версия 1.5.0).</span><span class="sxs-lookup"><span data-stu-id="72515-116">[Azure PowerShell)](/powershell/azure/overview), minimum version of 1.4.0 or later (this tutorial written using version 1.5.0).</span></span>
  * <span data-ttu-id="72515-117">Чтобы получить сведения о версии, выполните команду **Get-Module Azure -ListAvailable**.</span><span class="sxs-lookup"><span data-stu-id="72515-117">To retrieve your version, type **Get-Module Azure -ListAvailable**.</span></span>

## <a name="configure-your-subscription"></a><span data-ttu-id="72515-118">Настройка подписки</span><span class="sxs-lookup"><span data-stu-id="72515-118">Configure your subscription</span></span>
<span data-ttu-id="72515-119">Откройте Windows PowerShell и установите доступ к учетной записи Azure, выполнив указанный ниже командлет.</span><span class="sxs-lookup"><span data-stu-id="72515-119">Open Windows PowerShell and establish access to your Azure account by running the following cmdlet.</span></span> <span data-ttu-id="72515-120">Откроется окно входа, в котором необходимо ввести свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="72515-120">You will be presented with a sign in screen to enter your credentials.</span></span> <span data-ttu-id="72515-121">Используйте тот же адрес электронной почты и пароль, который вы используете для входа на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="72515-121">Use the same email and password that you use to sign in to the Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="72515-122">После успешного входа на экране будут отображаться некоторые сведения, включая идентификатор подписки, под которым вы вошли в систему.</span><span class="sxs-lookup"><span data-stu-id="72515-122">After successfully signing in you will see some information on screen that includes the SubscriptionId with which you signed in.</span></span> <span data-ttu-id="72515-123">Это подписка, в которой будут созданы ресурсы для этого руководства (если вы не перейдете к другой подписке).</span><span class="sxs-lookup"><span data-stu-id="72515-123">This is the subscription in which the resources for this tutorial will be created unless you change to a different subscription.</span></span> <span data-ttu-id="72515-124">При наличии нескольких идентификаторов подписки выполните следующий командлет, чтобы получить список всех идентификаторов подписки:</span><span class="sxs-lookup"><span data-stu-id="72515-124">If you have multiple SubscriptionIds, run the following cmdlet to return a list of all of your SubscriptionIds:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="72515-125">Чтобы использовать другой идентификатор подписки, выполните следующий командлет с требуемым идентификатором подписки:</span><span class="sxs-lookup"><span data-stu-id="72515-125">To change to another SubscriptionID, run the following cmdlet with your desired SubscriptionId.</span></span>

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a><span data-ttu-id="72515-126">Определение переменных образа</span><span class="sxs-lookup"><span data-stu-id="72515-126">Define image variables</span></span>
<span data-ttu-id="72515-127">Чтобы упростить использование и понимание завершенного сценария из этого руководства, сначала мы определим количество переменных.</span><span class="sxs-lookup"><span data-stu-id="72515-127">To simplify usability and understanding of the completed script from this tutorial, we will start by defining a number of variables.</span></span> <span data-ttu-id="72515-128">Изменяйте значения параметров по своему усмотрению. Однако учитывайте при этом ограничения именования, связанные с длиной имени и специальными знаками.</span><span class="sxs-lookup"><span data-stu-id="72515-128">Change the parameter values as you see fit, but beware of naming restrictions related to name lengths and special characters when modifying the values provided.</span></span>

### <a name="location-and-resource-group"></a><span data-ttu-id="72515-129">Расположение и группа ресурсов</span><span class="sxs-lookup"><span data-stu-id="72515-129">Location and Resource Group</span></span>
<span data-ttu-id="72515-130">Используйте две указанные ниже переменные, чтобы определить область данных и группу ресурсов, в которых будут создаваться другие ресурсы для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="72515-130">Use two variables to define the data region and the resource group into which you will create the other resources for the virtual machine.</span></span>

<span data-ttu-id="72515-131">Измените их соответствующим образом, а затем выполните следующие командлеты, чтобы инициализировать эти переменные:</span><span class="sxs-lookup"><span data-stu-id="72515-131">Modify as desired and then execute the following cmdlets to initialize these variables.</span></span>

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a><span data-ttu-id="72515-132">Свойства хранилища</span><span class="sxs-lookup"><span data-stu-id="72515-132">Storage properties</span></span>
<span data-ttu-id="72515-133">Используйте следующие переменные, чтобы определить учетную запись хранения и тип хранилища в виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="72515-133">Use the following variables to define the storage account and the type of storage to be used by the virtual machine.</span></span>

<span data-ttu-id="72515-134">Измените их соответствующим образом, а затем выполните командлет ниже, чтобы инициализировать эти переменные.</span><span class="sxs-lookup"><span data-stu-id="72515-134">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span> <span data-ttu-id="72515-135">Обратите внимание, что в этом примере используется [хранилище уровня "Премиум"](../../../storage/common/storage-premium-storage.md), которое рекомендуется для рабочих нагрузок в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="72515-135">Note that in this example, we are using [Premium Storage](../../../storage/common/storage-premium-storage.md), which is recommended for production workloads.</span></span> <span data-ttu-id="72515-136">Дополнительные сведения об этом руководстве, а также другие рекомендации см. в статье [Рекомендации по оптимизации производительности SQL Server в виртуальных машинах Azure](virtual-machines-windows-sql-performance.md).</span><span class="sxs-lookup"><span data-stu-id="72515-136">For details on this guidance and other recommendations, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a><span data-ttu-id="72515-137">Свойства сети</span><span class="sxs-lookup"><span data-stu-id="72515-137">Network properties</span></span>
<span data-ttu-id="72515-138">Используйте указанные ниже переменные, чтобы определить сетевой интерфейс, метод распределения TCP/IP, имя виртуальной сети, имя виртуальной подсети, диапазон IP-адресов для виртуальной сети, диапазон IP-адресов для подсети и метку общедоступного доменного имени, которые будет использовать сеть на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="72515-138">Use the following variables to define the network interface, the TCP/IP allocation method, the virtual network name, the virtual subnet name, the range of IP addresses for the virtual network, the range of IP addresses for the subnet, and the public domain name label to be used by the network in the virtual machine.</span></span>

<span data-ttu-id="72515-139">Измените их соответствующим образом, а затем выполните командлет ниже, чтобы инициализировать эти переменные.</span><span class="sxs-lookup"><span data-stu-id="72515-139">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span>

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a><span data-ttu-id="72515-140">Свойства виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="72515-140">Virtual machine properties</span></span>
<span data-ttu-id="72515-141">Используйте указанные ниже переменные, чтобы определить имя виртуальной машины, имя компьютера, размер виртуальной машины и имя диска операционной системы для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="72515-141">Use the following variables to define the virtual machine name, the computer name, the virtual machine size, and the operating system disk name for the virtual machine.</span></span>

<span data-ttu-id="72515-142">Измените их соответствующим образом, а затем выполните командлет ниже, чтобы инициализировать эти переменные.</span><span class="sxs-lookup"><span data-stu-id="72515-142">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span>

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a><span data-ttu-id="72515-143">Свойства образа</span><span class="sxs-lookup"><span data-stu-id="72515-143">Image properties</span></span>
<span data-ttu-id="72515-144">Используйте следующие переменные, чтобы определить образ, который будет применен для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="72515-144">Use the following variables to define the image to use for the virtual machine.</span></span> <span data-ttu-id="72515-145">В этом примере используется образ SQL Server 2016 Enterprise.</span><span class="sxs-lookup"><span data-stu-id="72515-145">In this example, the SQL Server 2016 Enterprise image is used.</span></span>

<span data-ttu-id="72515-146">Измените их соответствующим образом, а затем выполните командлет ниже, чтобы инициализировать эти переменные.</span><span class="sxs-lookup"><span data-stu-id="72515-146">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span>

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

<span data-ttu-id="72515-147">Вы можете получить полный список образов SQL Server, выполнив команду Get-AzureRmVMImageOffer:</span><span class="sxs-lookup"><span data-stu-id="72515-147">Note that you can get a full list of SQL Server image offerings with the Get-AzureRmVMImageOffer command:</span></span>

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

<span data-ttu-id="72515-148">Кроме того, выполнив команду Get-AzureRmVMImageSku, можно получить сведения о единицах хранения, доступных для предложения.</span><span class="sxs-lookup"><span data-stu-id="72515-148">And you can see the Skus available for an offering with the Get-AzureRmVMImageSku command.</span></span> <span data-ttu-id="72515-149">При выполнении следующей команды отображаются все SKU для предложения **SQL2014SP1-WS2012R2** .</span><span class="sxs-lookup"><span data-stu-id="72515-149">The following command shows all Skus available for the **SQL2014SP1-WS2012R2** offer.</span></span>

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a><span data-ttu-id="72515-150">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="72515-150">Create a resource group</span></span>
<span data-ttu-id="72515-151">Если используется модель развертывания с помощью Resource Manager, первый создаваемый объект — группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="72515-151">With the Resource Manager deployment model, the first object that you create is the resource group.</span></span> <span data-ttu-id="72515-152">Мы используем командлет [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup), чтобы создать группу ресурсов Azure и соответствующие ресурсы. При этом имя и расположение группы ресурсов определяются в переменных, инициализированных ранее.</span><span class="sxs-lookup"><span data-stu-id="72515-152">We will use the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet to create an Azure resource group and its resources with the resource group name and location defined by the variables that you previously initialized.</span></span>

<span data-ttu-id="72515-153">Выполните следующий командлет, чтобы создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="72515-153">Execute the following cmdlet to create your new resource group.</span></span>

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a><span data-ttu-id="72515-154">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="72515-154">Create a storage account</span></span>
<span data-ttu-id="72515-155">Виртуальной машине требуются ресурсы хранения для диска операционной системы, а также файлов данных и журналов SQL Server.</span><span class="sxs-lookup"><span data-stu-id="72515-155">The virtual machine requires storage resources for the operating system disk and for the SQL Server data and log files.</span></span> <span data-ttu-id="72515-156">Для упрощения мы создадим один диск для всех ресурсов.</span><span class="sxs-lookup"><span data-stu-id="72515-156">For simplicity, we will create a single disk for both.</span></span> <span data-ttu-id="72515-157">Позже можно будет подключить дополнительные диски, выполнив командлет [Add-Azure Disk](/powershell/module/azure/add-azuredisk), чтобы поместить файлы данных и журналов SQL Server на выделенные диски.</span><span class="sxs-lookup"><span data-stu-id="72515-157">You can attach additional disks later using the [Add-Azure Disk](/powershell/module/azure/add-azuredisk) cmdlet in order to place your SQL Server data and log files on dedicated disks.</span></span> <span data-ttu-id="72515-158">Мы выполним командлет [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount), чтобы создать стандартную учетную запись хранения в новой группе ресурсов. При этом имя учетной записи хранения, номер SKU хранилища и расположение определяются в переменных, инициализированных ранее.</span><span class="sxs-lookup"><span data-stu-id="72515-158">We will use the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet to create a standard storage account in your new resource group and with the storage account name, storage Sku name, and location defined using the variables that you previously initialized.</span></span>

<span data-ttu-id="72515-159">Выполните следующий командлет, чтобы создать учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="72515-159">Execute the following cmdlet to create your new storage account.</span></span>

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a><span data-ttu-id="72515-160">Создание сетевых ресурсов</span><span class="sxs-lookup"><span data-stu-id="72515-160">Create network resources</span></span>
<span data-ttu-id="72515-161">Виртуальной машине нужны сетевые ресурсы для подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="72515-161">The virtual machine requires a number of network resources for network connectivity.</span></span>

* <span data-ttu-id="72515-162">Каждой виртуальной машине требуется виртуальная сеть.</span><span class="sxs-lookup"><span data-stu-id="72515-162">Each virtual machine requires a virtual network.</span></span>
* <span data-ttu-id="72515-163">Для виртуальной сети следует определить по крайней мере одну подсеть.</span><span class="sxs-lookup"><span data-stu-id="72515-163">A virtual network must have at least one subnet defined.</span></span>
* <span data-ttu-id="72515-164">Для сетевого интерфейса следует определить общедоступный или частный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="72515-164">A network interface must be defined with either a public or a private IP address.</span></span>

### <a name="create-a-virtual-network-subnet-configuration"></a><span data-ttu-id="72515-165">Создание конфигурации подсети в виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="72515-165">Create a virtual network subnet configuration</span></span>
<span data-ttu-id="72515-166">Сначала мы создадим конфигурацию подсети для нашей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="72515-166">We will start by creating a subnet configuration for our virtual network.</span></span> <span data-ttu-id="72515-167">Для целей учебника мы создадим подсеть по умолчанию, используя командлет [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) .</span><span class="sxs-lookup"><span data-stu-id="72515-167">For our tutorial, we will create a default subnet using the [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span></span> <span data-ttu-id="72515-168">Имя подсети и префикс адреса для нашей конфигурации подсети в виртуальной сети определяются в переменных, инициализированных ранее.</span><span class="sxs-lookup"><span data-stu-id="72515-168">We will create our virtual network subnet configuration with the subnet name and address prefix defined using the variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="72515-169">Выполнив этот командлет, можно определить дополнительные свойства конфигурации подсети виртуальной сети. Однако это выходит за рамки данного руководства.</span><span class="sxs-lookup"><span data-stu-id="72515-169">You can define additional properties of the virtual network subnet configuration using this cmdlet, but that is beyond the scope of this tutorial.</span></span>
>
>

<span data-ttu-id="72515-170">Выполните следующий командлет, чтобы создать конфигурацию виртуальной подсети.</span><span class="sxs-lookup"><span data-stu-id="72515-170">Execute the following cmdlet to create your virtual subnet configuration.</span></span>

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a><span data-ttu-id="72515-171">Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="72515-171">Create a virtual network</span></span>
<span data-ttu-id="72515-172">Далее с помощью командлета [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) мы создадим виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="72515-172">Next, we will create our virtual network using the [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span></span> <span data-ttu-id="72515-173">в новой группе ресурсов. При этом имя, расположение и префикс адреса определяются в переменных, инициализированных ранее. Кроме того, мы используем конфигурацию подсети, определенную на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="72515-173">We will create our virtual network in your new resource group, with the name, location, and address prefix defined using the variables that you previously initialized, and using the subnet configuration that you defined in the previous step.</span></span>

<span data-ttu-id="72515-174">Выполните следующий командлет, чтобы создать виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="72515-174">Execute the following cmdlet to create your virtual network.</span></span>

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-the-public-ip-address"></a><span data-ttu-id="72515-175">Создание общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="72515-175">Create the public IP address</span></span>
<span data-ttu-id="72515-176">Теперь, определив виртуальную сеть, необходимо настроить IP-адрес для подключения к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="72515-176">Now that we have our virtual network defined, we need to configure an IP address for connectivity to the virtual machine.</span></span> <span data-ttu-id="72515-177">В этом руководстве мы создадим общедоступный IP-адрес с применением динамического предоставления IP-адресов, чтобы обеспечить подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="72515-177">For this tutorial, we will create a public IP address using dynamic IP addressing to support Internet connectivity.</span></span> <span data-ttu-id="72515-178">Мы используем командлет [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress), чтобы создать общедоступный IP-адрес в ранее созданной группе ресурсов. При этом имя, расположение, метод распределения и метка общедоступного имени DNS-домена определяются в переменных, инициализированных ранее.</span><span class="sxs-lookup"><span data-stu-id="72515-178">We will use the [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet to create the public IP address in the resource group created prevously and with the name, location, allocation method, and DNS domain name label defined using the variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="72515-179">Выполнив этот командлет, можно определить дополнительные свойства общедоступного IP-адреса. Однако это выходит за рамки данного руководства.</span><span class="sxs-lookup"><span data-stu-id="72515-179">You can define additional properties of the public IP address using this cmdlet, but that is beyond the scope of this initial tutorial.</span></span> <span data-ttu-id="72515-180">Кроме того, можно создать частный или статический адрес, но это также выходит за рамки данного руководства.</span><span class="sxs-lookup"><span data-stu-id="72515-180">You could also create a private address or an address with a static address, but that is also beyond the scope of this tutorial.</span></span>
>
>

<span data-ttu-id="72515-181">Выполните следующий командлет, чтобы создать общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="72515-181">Execute the following cmdlet to create your public IP address.</span></span>

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-the-network-interface"></a><span data-ttu-id="72515-182">Создание сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="72515-182">Create the network interface</span></span>
<span data-ttu-id="72515-183">Теперь все готово для создания сетевого интерфейса, который будет использовать виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="72515-183">We are now ready to create the network interface that our virtual machine will use.</span></span> <span data-ttu-id="72515-184">Мы используем командлет [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) , чтобы создать сетевой интерфейс в ранее созданной группе ресурсов с ранее определенными именем, расположением, подсетью и общедоступным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="72515-184">We will use the [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet to create our network interface in the resource group created earlier and with the name, location, subnet and public IP address previously defined.</span></span>

<span data-ttu-id="72515-185">Выполните следующий командлет, чтобы создать сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="72515-185">Execute the following cmdlet to create your network interface.</span></span>

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a><span data-ttu-id="72515-186">Настройка объекта виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="72515-186">Configure a VM object</span></span>
<span data-ttu-id="72515-187">После определения ресурсов хранения и сетевых ресурсов можно определить вычислительные ресурсы для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="72515-187">Now that we have storage and network resources defined, we are ready to define compute resources for the virtual machine.</span></span> <span data-ttu-id="72515-188">В рамках целей руководства мы укажем размер виртуальной машины, различные свойства операционной системы, ранее созданный сетевой интерфейс, определим хранилище BLOB-объектов, а затем укажем диск операционной системы.</span><span class="sxs-lookup"><span data-stu-id="72515-188">For our tutorial, we will specify the virtual machine size and various operating system properties, specify the network interface that we previously created, define blob storage, and then specify the operating system disk.</span></span>

### <a name="create-the-vm-object"></a><span data-ttu-id="72515-189">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="72515-189">Create the VM object</span></span>
<span data-ttu-id="72515-190">Сначала мы укажем размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="72515-190">We will start by specifying the virtual machine size.</span></span> <span data-ttu-id="72515-191">В этом руководстве мы указываем DS13.</span><span class="sxs-lookup"><span data-stu-id="72515-191">For this tutorial, we are specifying a DS13.</span></span> <span data-ttu-id="72515-192">Мы используем командлет [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), чтобы создать настраиваемый объект виртуальной машины. При этом имя и размер определяются в переменных, инициализированных ранее.</span><span class="sxs-lookup"><span data-stu-id="72515-192">We will use the [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet to create a configurable virtual machine object with the name and size defined using the variables that you previously initialized.</span></span>

<span data-ttu-id="72515-193">Выполните следующий командлет, чтобы создать объект виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="72515-193">Execute the following cmdlet to create the virtual machine object.</span></span>

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-to-hold-the-name-and-password-for-the-local-administrator-credentials"></a><span data-ttu-id="72515-194">Создание объекта учетных данных для хранения имени и пароля локального администратора</span><span class="sxs-lookup"><span data-stu-id="72515-194">Create a credential object to hold the name and password for the local administrator credentials</span></span>
<span data-ttu-id="72515-195">Чтобы задать свойства операционной системы для виртуальной машины, необходимо сначала предоставить учетные данные для учетной записи локального администратора в виде защищенной строки.</span><span class="sxs-lookup"><span data-stu-id="72515-195">Before we can set the operating system properties for the virtual machine, we need to supply the credentials for the local administrator account as a secure string.</span></span> <span data-ttu-id="72515-196">Для этого мы используем командлет [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) .</span><span class="sxs-lookup"><span data-stu-id="72515-196">To accomplish this, we will use the [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

<span data-ttu-id="72515-197">Выполните следующий командлет и в окне запроса учетных данных Windows PowerShell введите имя и пароль, которые будут использоваться для учетной записи локального администратора на виртуальной машине Windows.</span><span class="sxs-lookup"><span data-stu-id="72515-197">Execute the following cmdlet and, in the Windows PowerShell credential request window, type the name and password to use for the local administrator account in the Windows virtual machine.</span></span>

    $Credential = Get-Credential -Message "Type the name and password of the local administrator account."

### <a name="set-the-operating-system-properties-for-the-virtual-machine"></a><span data-ttu-id="72515-198">Определение свойств операционной системы для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="72515-198">Set the operating system properties for the virtual machine</span></span>
<span data-ttu-id="72515-199">Теперь мы можем задать свойства операционной системы виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="72515-199">Now we are ready to set the virtual machine's operating system properties.</span></span> <span data-ttu-id="72515-200">Мы используем командлет [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), чтобы задать тип операционной системы Windows. Для этого нужно установить [агент виртуальной машины](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Укажите, что командлет включает автоматическое обновление, и задайте имя виртуальной машины, имя компьютера и учетные данные в переменных, инициализированных ранее.</span><span class="sxs-lookup"><span data-stu-id="72515-200">We will use the [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet to set the type of operating system as Windows, require the [virtual machine agent](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to be installed, specify that the cmdlet enables auto update and set the virtual machine name, the computer name, and the credential using the variables that you previously initialized.</span></span>

<span data-ttu-id="72515-201">Выполните следующий командлет, чтобы задать свойства операционной системы для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="72515-201">Execute the following cmdlet to set the operating system properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-the-network-interface-to-the-virtual-machine"></a><span data-ttu-id="72515-202">Добавление сетевого интерфейса к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="72515-202">Add the network interface to the virtual machine</span></span>
<span data-ttu-id="72515-203">Далее мы добавим созданный ранее сетевой интерфейс к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="72515-203">Next, we will add the network interface that we created previously to the virtual machine.</span></span> <span data-ttu-id="72515-204">Для этого мы используем командлет [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) и переменную сетевого интерфейса, определенную ранее.</span><span class="sxs-lookup"><span data-stu-id="72515-204">We will use the [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet to add the network interface using the network interface variable that you defined earlier.</span></span>

<span data-ttu-id="72515-205">Выполните следующий командлет, чтобы указать сетевой интерфейс для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="72515-205">Execute the following cmdlet to set the network interface for your virtual machine.</span></span>

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-the-blob-storage-location-for-the-disk-to-be-used-by-the-virtual-machine"></a><span data-ttu-id="72515-206">Определение расположения хранилища BLOB-объектов для диска, используемого виртуальной машиной</span><span class="sxs-lookup"><span data-stu-id="72515-206">Set the blob storage location for the disk to be used by the virtual machine</span></span>
<span data-ttu-id="72515-207">Далее мы укажем расположение хранилища BLOB-объектов для диска, который будет использоваться в виртуальной машине, с определенными ранее переменными.</span><span class="sxs-lookup"><span data-stu-id="72515-207">Next, we will set the blob storage location for the disk to be used by the virtual machine using the variables that you defined earlier.</span></span>

<span data-ttu-id="72515-208">Выполните следующий командлет, чтобы задать расположение хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="72515-208">Execute the following cmdlet to set the blob storage location.</span></span>

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-the-operating-system-disk-properties-for-the-virtual-machine"></a><span data-ttu-id="72515-209">Определение свойств диска операционной системы для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="72515-209">Set the operating system disk properties for the virtual machine</span></span>
<span data-ttu-id="72515-210">Далее мы зададим свойства диска операционной системы для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="72515-210">Next, we will set the operating system disk properties for the virtual machine.</span></span> <span data-ttu-id="72515-211">Мы используем командлет [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) , чтобы указать, что для операционной системы виртуальной машины используется образ, настроить кэширование для чтения (так как SQL Server устанавливается на том же диске), а также определить имя виртуальной машины и диск операционной системы с использованием переменных, определенных ранее.</span><span class="sxs-lookup"><span data-stu-id="72515-211">We will use the [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet to specify that the operating system for the virtual machine will come from an image, to set caching to read only (because SQL Server is being installed on the same disk) and define the virtual machine name and the operating system disk defined using the variables that we defined earlier.</span></span>

<span data-ttu-id="72515-212">Выполните следующий командлет, чтобы задать свойства диска операционной системы для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="72515-212">Execute the following cmdlet to set the operating system disk properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-the-platform-image-for-the-virtual-machine"></a><span data-ttu-id="72515-213">Определение образа платформы для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="72515-213">Specify the platform image for the virtual machine</span></span>
<span data-ttu-id="72515-214">Последний этап конфигурации — определение образа платформы для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="72515-214">Our last configuration step is to specify the platform image for our virtual machine.</span></span> <span data-ttu-id="72515-215">В рамках этого руководства мы используем последний образ SQL Server 2016 CTP-версии.</span><span class="sxs-lookup"><span data-stu-id="72515-215">For our tutorial, we are using the latest SQL Server 2016 CTP image.</span></span> <span data-ttu-id="72515-216">Мы используем командлет [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) , чтобы задать образ согласно значениям переменных, определенных ранее.</span><span class="sxs-lookup"><span data-stu-id="72515-216">We will use the [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet to use this image as defined by the variables that you defined earlier.</span></span>

<span data-ttu-id="72515-217">Выполните следующий командлет, чтобы указать образ платформы для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="72515-217">Execute the following cmdlet to specify the platform image for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-the-sql-vm"></a><span data-ttu-id="72515-218">Создание виртуальной машины SQL</span><span class="sxs-lookup"><span data-stu-id="72515-218">Create the SQL VM</span></span>
<span data-ttu-id="72515-219">Теперь по завершении конфигурации все готово для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="72515-219">Now that you have finished the configuration steps, you are ready to create the virtual machine.</span></span> <span data-ttu-id="72515-220">Для этого мы используем командлет [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) и определенные переменные.</span><span class="sxs-lookup"><span data-stu-id="72515-220">We will use the [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet to create the virtual machine using the variables that we have defined.</span></span>

<span data-ttu-id="72515-221">Выполните следующий командлет, чтобы создать виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="72515-221">Execute the following cmdlet to create your virtual machine.</span></span>

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

<span data-ttu-id="72515-222">Теперь виртуальная машина создана.</span><span class="sxs-lookup"><span data-stu-id="72515-222">The virtual machine is created.</span></span> <span data-ttu-id="72515-223">Обратите внимание, что стандартная учетная запись хранения создается для диагностики загрузки, так как для диска виртуальной машины указана учетная запись хранилища класса Premium.</span><span class="sxs-lookup"><span data-stu-id="72515-223">Notice that a standard storage account is created for boot diagnostics because the specified storage account for the virtual machine's disk is a premium storage account.</span></span>

<span data-ttu-id="72515-224">Теперь этот компьютер можно просмотреть на портале Azure, чтобы увидеть [его общедоступный IP-адрес и полное доменное имя](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="72515-224">You can now view this machine in the Azure Portal to see [its public IP address and its fully qualified domain name](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="example-script"></a><span data-ttu-id="72515-225">Пример сценария</span><span class="sxs-lookup"><span data-stu-id="72515-225">Example script</span></span>
<span data-ttu-id="72515-226">Файл ниже содержит полный сценарий PowerShell для этого руководства.</span><span class="sxs-lookup"><span data-stu-id="72515-226">The following script contains the complete PowerShell script for this tutorial.</span></span> <span data-ttu-id="72515-227">Предполагается, что вы уже настроили подписку Azure на использование с командами **Add-AzureRmAccount** и **Select-AzureRmSubscription**.</span><span class="sxs-lookup"><span data-stu-id="72515-227">It assumes that you have already setup the Azure subscription to use with the **Add-AzureRmAccount** and **Select-AzureRmSubscription** commands.</span></span>

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type the name and password of the local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create the VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a><span data-ttu-id="72515-228">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="72515-228">Next steps</span></span>
<span data-ttu-id="72515-229">После создания виртуальной машины вы можете подключиться к ней, используя протокол удаленного рабочего и настроив подключение.</span><span class="sxs-lookup"><span data-stu-id="72515-229">After the virtual machine is created, you are ready to connect to the virtual machine using RDP and setup connectivity.</span></span> <span data-ttu-id="72515-230">Дополнительные сведения см. в статье [Подключение к виртуальной машине SQL Server в Azure (диспетчер ресурсов)](virtual-machines-windows-sql-connect.md).</span><span class="sxs-lookup"><span data-stu-id="72515-230">For more information, see [Connect to a SQL Server Virtual Machine on Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span></span>

