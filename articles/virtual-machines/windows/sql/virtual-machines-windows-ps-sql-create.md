---
title: "aaaCreate виртуальной машины с SQL Server в Azure PowerShell (диспетчера ресурсов) | Документы Microsoft"
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
ms.openlocfilehash: 2b8cb8f69ff9894a95eab617816a60c8674eeefa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a><span data-ttu-id="b110e-103">Подготовка виртуальной машины SQL Server к работе с помощью Azure PowerShell (в Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="b110e-103">Provision a SQL Server virtual machine using Azure PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b110e-104">Портал</span><span class="sxs-lookup"><span data-stu-id="b110e-104">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="b110e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b110e-105">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a><span data-ttu-id="b110e-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="b110e-106">Overview</span></span>
<span data-ttu-id="b110e-107">В этом учебнике показано, как hello в одной виртуальной машине Azure с помощью toocreate **диспетчера ресурсов Azure** развертывания модели с помощью командлетов Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b110e-107">This tutorial shows you how toocreate a single Azure virtual machine using hello **Azure Resource Manager** deployment model using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="b110e-108">В этом учебнике мы создадим одной виртуальной машины с помощью одного диска из образа в коллекции SQL hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-108">In this tutorial, we will create a single virtual machine using a single disk drive from an image in hello SQL Gallery.</span></span> <span data-ttu-id="b110e-109">Мы создадим новые поставщики для hello хранилища, сети и вычислительных ресурсов, которые будут использоваться виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-109">We will create new providers for hello storage, network, and compute resources that will be used by hello virtual machine.</span></span> <span data-ttu-id="b110e-110">Вы можете использовать существующие поставщики для любых из этих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b110e-110">If you have existing providers for any of these resources, you can use those providers instead.</span></span>

<span data-ttu-id="b110e-111">Если требуется hello базовую версию этого раздела, см. раздел [подготовки виртуальной машины SQL Server с помощью Azure PowerShell Classic](../classic/ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="b110e-111">If you need hello classic version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Classic](../classic/ps-sql-create.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b110e-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b110e-112">Prerequisites</span></span>
<span data-ttu-id="b110e-113">Для работы с этим руководством вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="b110e-113">For this tutorial you'll need:</span></span>

* <span data-ttu-id="b110e-114">Учетная запись Azure и подписка (еще до начала).</span><span class="sxs-lookup"><span data-stu-id="b110e-114">An Azure account and subscription before you start.</span></span> <span data-ttu-id="b110e-115">Если у вас ее нет, зарегистрируйтесь, чтобы [воспользоваться бесплатной пробной версией](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b110e-115">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b110e-116">[Azure PowerShell](/powershell/azure/overview)1.4.0 или более поздней версии (в этом учебнике использовалась версия 1.5.0).</span><span class="sxs-lookup"><span data-stu-id="b110e-116">[Azure PowerShell)](/powershell/azure/overview), minimum version of 1.4.0 or later (this tutorial written using version 1.5.0).</span></span>
  * <span data-ttu-id="b110e-117">tooretrieve версию, тип **Azure Get-Module - ListAvailable**.</span><span class="sxs-lookup"><span data-stu-id="b110e-117">tooretrieve your version, type **Get-Module Azure -ListAvailable**.</span></span>

## <a name="configure-your-subscription"></a><span data-ttu-id="b110e-118">Настройка подписки</span><span class="sxs-lookup"><span data-stu-id="b110e-118">Configure your subscription</span></span>
<span data-ttu-id="b110e-119">Откройте Windows PowerShell и установить tooyour доступа учетной записи Azure, выполнив следующий командлет hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-119">Open Windows PowerShell and establish access tooyour Azure account by running hello following cmdlet.</span></span> <span data-ttu-id="b110e-120">Откроется экран tooenter имя входа учетные данные.</span><span class="sxs-lookup"><span data-stu-id="b110e-120">You will be presented with a sign in screen tooenter your credentials.</span></span> <span data-ttu-id="b110e-121">Используйте hello же электронной почты и пароль, использовать toosign в toohello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b110e-121">Use hello same email and password that you use toosign in toohello Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="b110e-122">После успешного входа в некоторые сведения можно просмотреть на экране, которая включает в себя SubscriptionId hello, с которой вы выполнили вход.</span><span class="sxs-lookup"><span data-stu-id="b110e-122">After successfully signing in you will see some information on screen that includes hello SubscriptionId with which you signed in.</span></span> <span data-ttu-id="b110e-123">Это hello подписки, в которой hello ресурсы в этом учебнике будет создан, если вы не изменили tooa другую подписку.</span><span class="sxs-lookup"><span data-stu-id="b110e-123">This is hello subscription in which hello resources for this tutorial will be created unless you change tooa different subscription.</span></span> <span data-ttu-id="b110e-124">При наличии нескольких SubscriptionIds, выполните следующий командлет tooreturn hello список всех вашей SubscriptionIds:</span><span class="sxs-lookup"><span data-stu-id="b110e-124">If you have multiple SubscriptionIds, run hello following cmdlet tooreturn a list of all of your SubscriptionIds:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="b110e-125">tooanother toochange SubscriptionID, запустите следующий командлет с вашей требуемой SubscriptionId hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-125">toochange tooanother SubscriptionID, run hello following cmdlet with your desired SubscriptionId.</span></span>

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a><span data-ttu-id="b110e-126">Определение переменных образа</span><span class="sxs-lookup"><span data-stu-id="b110e-126">Define image variables</span></span>
<span data-ttu-id="b110e-127">toosimplify удобство использования и понимание hello выполнить сценарий из этого учебника, начнем, определив несколько переменных.</span><span class="sxs-lookup"><span data-stu-id="b110e-127">toosimplify usability and understanding of hello completed script from this tutorial, we will start by defining a number of variables.</span></span> <span data-ttu-id="b110e-128">Изменить значения параметров hello, при необходимости, но Учтите, что именования ограничения связанные tooname длины и специальные символы при изменении значений hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-128">Change hello parameter values as you see fit, but beware of naming restrictions related tooname lengths and special characters when modifying hello values provided.</span></span>

### <a name="location-and-resource-group"></a><span data-ttu-id="b110e-129">Расположение и группа ресурсов</span><span class="sxs-lookup"><span data-stu-id="b110e-129">Location and Resource Group</span></span>
<span data-ttu-id="b110e-130">Используйте две переменные toodefine hello данных региона и hello группа ресурсов, в который будут созданы другие ресурсы для виртуальной машины hello hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-130">Use two variables toodefine hello data region and hello resource group into which you will create hello other resources for hello virtual machine.</span></span>

<span data-ttu-id="b110e-131">При желании изменить, а затем выполните следующие командлеты tooinitialize hello эти переменные.</span><span class="sxs-lookup"><span data-stu-id="b110e-131">Modify as desired and then execute hello following cmdlets tooinitialize these variables.</span></span>

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a><span data-ttu-id="b110e-132">Свойства хранилища</span><span class="sxs-lookup"><span data-stu-id="b110e-132">Storage properties</span></span>
<span data-ttu-id="b110e-133">Используйте следующие переменные toodefine hello учетной записи и hello тип хранения для toobe хранилища, используемый виртуальной машиной hello hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-133">Use hello following variables toodefine hello storage account and hello type of storage toobe used by hello virtual machine.</span></span>

<span data-ttu-id="b110e-134">При желании изменить, а затем выполните следующий командлет tooinitialize hello эти переменные.</span><span class="sxs-lookup"><span data-stu-id="b110e-134">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span> <span data-ttu-id="b110e-135">Обратите внимание, что в этом примере используется [хранилище уровня "Премиум"](../../../storage/common/storage-premium-storage.md), которое рекомендуется для рабочих нагрузок в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="b110e-135">Note that in this example, we are using [Premium Storage](../../../storage/common/storage-premium-storage.md), which is recommended for production workloads.</span></span> <span data-ttu-id="b110e-136">Дополнительные сведения об этом руководстве, а также другие рекомендации см. в статье [Рекомендации по оптимизации производительности SQL Server в виртуальных машинах Azure](virtual-machines-windows-sql-performance.md).</span><span class="sxs-lookup"><span data-stu-id="b110e-136">For details on this guidance and other recommendations, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a><span data-ttu-id="b110e-137">Свойства сети</span><span class="sxs-lookup"><span data-stu-id="b110e-137">Network properties</span></span>
<span data-ttu-id="b110e-138">Используйте следующие переменные toodefine hello сетевого интерфейса, способ распределения hello TCP/IP, hello виртуальной сети имя, hello виртуальной подсети, hello диапазон IP-адресов для виртуальной сети hello, hello диапазон IP-адресов для подсети hello и hello hello toobe имя метки общедоступные сети hello hello виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="b110e-138">Use hello following variables toodefine hello network interface, hello TCP/IP allocation method, hello virtual network name, hello virtual subnet name, hello range of IP addresses for hello virtual network, hello range of IP addresses for hello subnet, and hello public domain name label toobe used by hello network in hello virtual machine.</span></span>

<span data-ttu-id="b110e-139">При желании изменить, а затем выполните следующий командлет tooinitialize hello эти переменные.</span><span class="sxs-lookup"><span data-stu-id="b110e-139">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a><span data-ttu-id="b110e-140">Свойства виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b110e-140">Virtual machine properties</span></span>
<span data-ttu-id="b110e-141">Используйте следующие имя виртуальной машины hello toodefine переменные, имя компьютера hello, размер виртуальной машины hello и hello имя диска операционной системы для виртуальной машины hello hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-141">Use hello following variables toodefine hello virtual machine name, hello computer name, hello virtual machine size, and hello operating system disk name for hello virtual machine.</span></span>

<span data-ttu-id="b110e-142">При желании изменить, а затем выполните следующий командлет tooinitialize hello эти переменные.</span><span class="sxs-lookup"><span data-stu-id="b110e-142">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a><span data-ttu-id="b110e-143">Свойства образа</span><span class="sxs-lookup"><span data-stu-id="b110e-143">Image properties</span></span>
<span data-ttu-id="b110e-144">Используйте следующие переменные toodefine hello изображения toouse для виртуальной машины hello hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-144">Use hello following variables toodefine hello image toouse for hello virtual machine.</span></span> <span data-ttu-id="b110e-145">В этом примере используется образ SQL Server 2016 Enterprise hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-145">In this example, hello SQL Server 2016 Enterprise image is used.</span></span>

<span data-ttu-id="b110e-146">При желании изменить, а затем выполните следующий командлет tooinitialize hello эти переменные.</span><span class="sxs-lookup"><span data-stu-id="b110e-146">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

<span data-ttu-id="b110e-147">Обратите внимание, что можно получить полный список предложений образа SQL Server с помощью команды Get-AzureRmVMImageOffer hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-147">Note that you can get a full list of SQL Server image offerings with hello Get-AzureRmVMImageOffer command:</span></span>

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

<span data-ttu-id="b110e-148">И вы увидите hello номера SKU для предложения с помощью команды Get-AzureRmVMImageSku hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-148">And you can see hello Skus available for an offering with hello Get-AzureRmVMImageSku command.</span></span> <span data-ttu-id="b110e-149">Hello следующая команда показывает все номера SKU для hello **SQL2014SP1 WS2012R2** предлагают.</span><span class="sxs-lookup"><span data-stu-id="b110e-149">hello following command shows all Skus available for hello **SQL2014SP1-WS2012R2** offer.</span></span>

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a><span data-ttu-id="b110e-150">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="b110e-150">Create a resource group</span></span>
<span data-ttu-id="b110e-151">С помощью модели развертывания диспетчера ресурсов hello hello первый объект, который вы создаете — hello группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b110e-151">With hello Resource Manager deployment model, hello first object that you create is hello resource group.</span></span> <span data-ttu-id="b110e-152">Мы будем использовать hello [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) toocreate командлет группе ресурсов Azure и его ресурсы с ресурсом hello группы имя и расположение определяется hello переменные, которые ранее инициализирован.</span><span class="sxs-lookup"><span data-stu-id="b110e-152">We will use hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate an Azure resource group and its resources with hello resource group name and location defined by hello variables that you previously initialized.</span></span>

<span data-ttu-id="b110e-153">Выполните следующий командлет toocreate hello новой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b110e-153">Execute hello following cmdlet toocreate your new resource group.</span></span>

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a><span data-ttu-id="b110e-154">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="b110e-154">Create a storage account</span></span>
<span data-ttu-id="b110e-155">Hello виртуальной машине требуется ресурсы хранения для диска операционной системы hello и hello данных SQL Server и файлов журнала.</span><span class="sxs-lookup"><span data-stu-id="b110e-155">hello virtual machine requires storage resources for hello operating system disk and for hello SQL Server data and log files.</span></span> <span data-ttu-id="b110e-156">Для упрощения мы создадим один диск для всех ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b110e-156">For simplicity, we will create a single disk for both.</span></span> <span data-ttu-id="b110e-157">Можно подключить дополнительные диски, позднее с помощью hello [диска Azure добавить](/powershell/module/azure/add-azuredisk) командлета в порядок tooplace данных SQL Server и файлы журнала на выделенные диски.</span><span class="sxs-lookup"><span data-stu-id="b110e-157">You can attach additional disks later using hello [Add-Azure Disk](/powershell/module/azure/add-azuredisk) cmdlet in order tooplace your SQL Server data and log files on dedicated disks.</span></span> <span data-ttu-id="b110e-158">Мы будем использовать hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) toocreate командлет стандартное хранилище учетную запись в новой группы ресурсов и hello имя учетной записи хранения, имя Sku хранения и места, определенного с помощью переменных hello, которую ранее инициализирован.</span><span class="sxs-lookup"><span data-stu-id="b110e-158">We will use hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate a standard storage account in your new resource group and with hello storage account name, storage Sku name, and location defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="b110e-159">Выполните следующий командлет toocreate hello учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="b110e-159">Execute hello following cmdlet toocreate your new storage account.</span></span>

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a><span data-ttu-id="b110e-160">Создание сетевых ресурсов</span><span class="sxs-lookup"><span data-stu-id="b110e-160">Create network resources</span></span>
<span data-ttu-id="b110e-161">Hello виртуальной машины необходимо указать число сетевых ресурсов для подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="b110e-161">hello virtual machine requires a number of network resources for network connectivity.</span></span>

* <span data-ttu-id="b110e-162">Каждой виртуальной машине требуется виртуальная сеть.</span><span class="sxs-lookup"><span data-stu-id="b110e-162">Each virtual machine requires a virtual network.</span></span>
* <span data-ttu-id="b110e-163">Для виртуальной сети следует определить по крайней мере одну подсеть.</span><span class="sxs-lookup"><span data-stu-id="b110e-163">A virtual network must have at least one subnet defined.</span></span>
* <span data-ttu-id="b110e-164">Для сетевого интерфейса следует определить общедоступный или частный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="b110e-164">A network interface must be defined with either a public or a private IP address.</span></span>

### <a name="create-a-virtual-network-subnet-configuration"></a><span data-ttu-id="b110e-165">Создание конфигурации подсети в виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="b110e-165">Create a virtual network subnet configuration</span></span>
<span data-ttu-id="b110e-166">Сначала мы создадим конфигурацию подсети для нашей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b110e-166">We will start by creating a subnet configuration for our virtual network.</span></span> <span data-ttu-id="b110e-167">В этом руководстве мы создадим подсеть по умолчанию с помощью hello [New AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) командлета.</span><span class="sxs-lookup"><span data-stu-id="b110e-167">For our tutorial, we will create a default subnet using hello [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span></span> <span data-ttu-id="b110e-168">Мы создадим нашей конфигурации подсети виртуальной сети с hello подсети имя и адрес префикс, определенный с помощью hello переменные, которые ранее инициализирован.</span><span class="sxs-lookup"><span data-stu-id="b110e-168">We will create our virtual network subnet configuration with hello subnet name and address prefix defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="b110e-169">Можно определить дополнительные свойства конфигурации подсети виртуальной сети hello, с помощью этого командлета, но они выходят за рамки данного учебника hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-169">You can define additional properties of hello virtual network subnet configuration using this cmdlet, but that is beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="b110e-170">Выполните следующий командлет toocreate hello конфигурацию виртуальной подсети.</span><span class="sxs-lookup"><span data-stu-id="b110e-170">Execute hello following cmdlet toocreate your virtual subnet configuration.</span></span>

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a><span data-ttu-id="b110e-171">Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="b110e-171">Create a virtual network</span></span>
<span data-ttu-id="b110e-172">После этого мы создадим нашей виртуальной сети, с помощью hello [New AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) командлета.</span><span class="sxs-lookup"><span data-stu-id="b110e-172">Next, we will create our virtual network using hello [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span></span> <span data-ttu-id="b110e-173">Мы создадим нашей виртуальной сети в новую группу ресурсов, с именем hello, расположение и адрес префикс, определенный с использованием hello переменные, которые ранее инициализирован и конфигурация hello подсети, определенные в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-173">We will create our virtual network in your new resource group, with hello name, location, and address prefix defined using hello variables that you previously initialized, and using hello subnet configuration that you defined in hello previous step.</span></span>

<span data-ttu-id="b110e-174">Выполните следующий командлет toocreate hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b110e-174">Execute hello following cmdlet toocreate your virtual network.</span></span>

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="b110e-175">Создать общедоступный IP-адрес hello</span><span class="sxs-lookup"><span data-stu-id="b110e-175">Create hello public IP address</span></span>
<span data-ttu-id="b110e-176">Теперь, когда у нас есть определенные виртуальной сети, нужно tooconfigure IP-адрес для подключения к toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b110e-176">Now that we have our virtual network defined, we need tooconfigure an IP address for connectivity toohello virtual machine.</span></span> <span data-ttu-id="b110e-177">В этом учебнике мы создадим общедоступный IP-адрес, с помощью динамических IP-адресов, адресация toosupport подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="b110e-177">For this tutorial, we will create a public IP address using dynamic IP addressing toosupport Internet connectivity.</span></span> <span data-ttu-id="b110e-178">Мы будем использовать hello [New AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) командлет toocreate hello общедоступный IP-адрес в prevously Создание группы ресурсов hello и с именем hello, расположение, способ распределения и определяются с помощью hello метка DNS-имени домена переменные, которые ранее инициализирован.</span><span class="sxs-lookup"><span data-stu-id="b110e-178">We will use hello [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate hello public IP address in hello resource group created prevously and with hello name, location, allocation method, and DNS domain name label defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="b110e-179">Можно определить дополнительные свойства hello общедоступный IP-адрес с помощью этого командлета, но это вне области hello начальной учебника.</span><span class="sxs-lookup"><span data-stu-id="b110e-179">You can define additional properties of hello public IP address using this cmdlet, but that is beyond hello scope of this initial tutorial.</span></span> <span data-ttu-id="b110e-180">Можно также создать частный адрес или адрес со статическим адресом, но также они выходят за рамки данного учебника hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-180">You could also create a private address or an address with a static address, but that is also beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="b110e-181">Выполните следующий командлет toocreate hello открытый IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="b110e-181">Execute hello following cmdlet toocreate your public IP address.</span></span>

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a><span data-ttu-id="b110e-182">Создание сетевого интерфейса hello</span><span class="sxs-lookup"><span data-stu-id="b110e-182">Create hello network interface</span></span>
<span data-ttu-id="b110e-183">Мы стали готовы toocreate hello сетевого интерфейса, который будет использовать наши виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b110e-183">We are now ready toocreate hello network interface that our virtual machine will use.</span></span> <span data-ttu-id="b110e-184">Мы будем использовать hello [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) ранее определенные командлет toocreate нашей сетевого интерфейса в группе ресурсов hello, созданного ранее и с hello, местоположение, подсеть и общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="b110e-184">We will use hello [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate our network interface in hello resource group created earlier and with hello name, location, subnet and public IP address previously defined.</span></span>

<span data-ttu-id="b110e-185">Выполните следующий командлет toocreate hello сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b110e-185">Execute hello following cmdlet toocreate your network interface.</span></span>

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a><span data-ttu-id="b110e-186">Настройка объекта виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b110e-186">Configure a VM object</span></span>
<span data-ttu-id="b110e-187">Теперь, когда у нас есть ресурсы хранилища и сети, определенные, не готов toodefine вычислительных ресурсов для виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-187">Now that we have storage and network resources defined, we are ready toodefine compute resources for hello virtual machine.</span></span> <span data-ttu-id="b110e-188">В этом руководстве мы hello размер виртуальной машины, а также различные свойства операционной системы, укажите hello сетевого интерфейса, который мы создали ранее, определить хранилище больших двоичных объектов и укажите hello диска операционной системы.</span><span class="sxs-lookup"><span data-stu-id="b110e-188">For our tutorial, we will specify hello virtual machine size and various operating system properties, specify hello network interface that we previously created, define blob storage, and then specify hello operating system disk.</span></span>

### <a name="create-hello-vm-object"></a><span data-ttu-id="b110e-189">Создание hello объекта виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="b110e-189">Create hello VM object</span></span>
<span data-ttu-id="b110e-190">Начнем с указанием размера виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-190">We will start by specifying hello virtual machine size.</span></span> <span data-ttu-id="b110e-191">В этом руководстве мы указываем DS13.</span><span class="sxs-lookup"><span data-stu-id="b110e-191">For this tutorial, we are specifying a DS13.</span></span> <span data-ttu-id="b110e-192">Мы будем использовать hello [New AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) toocreate командлет объект можно настроить виртуальную машину с именем hello и размер, определенный с помощью hello переменные, которые ранее инициализирован.</span><span class="sxs-lookup"><span data-stu-id="b110e-192">We will use hello [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate a configurable virtual machine object with hello name and size defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="b110e-193">Выполните следующий объект виртуальной машины hello toocreate командлета hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-193">Execute hello following cmdlet toocreate hello virtual machine object.</span></span>

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a><span data-ttu-id="b110e-194">Создайте учетные данные объекта toohold hello имя и пароль для учетной записи локального администратора hello</span><span class="sxs-lookup"><span data-stu-id="b110e-194">Create a credential object toohold hello name and password for hello local administrator credentials</span></span>
<span data-ttu-id="b110e-195">Прежде чем мы можно задать свойства hello операционной системы для виртуальной машины hello, нужны toosupply hello учетные данные для учетной записи локального администратора hello виде защищенной строки.</span><span class="sxs-lookup"><span data-stu-id="b110e-195">Before we can set hello operating system properties for hello virtual machine, we need toosupply hello credentials for hello local administrator account as a secure string.</span></span> <span data-ttu-id="b110e-196">tooaccomplish это, мы будем использовать hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="b110e-196">tooaccomplish this, we will use hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

<span data-ttu-id="b110e-197">Выполните следующий командлет hello и в окне запроса учетных данных Windows PowerShell hello введите hello toouse имя и пароль для учетной записи локального администратора hello в виртуальной машине Windows hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-197">Execute hello following cmdlet and, in hello Windows PowerShell credential request window, type hello name and password toouse for hello local administrator account in hello Windows virtual machine.</span></span>

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a><span data-ttu-id="b110e-198">Задать свойства hello операционной системы для виртуальной машины hello</span><span class="sxs-lookup"><span data-stu-id="b110e-198">Set hello operating system properties for hello virtual machine</span></span>
<span data-ttu-id="b110e-199">Теперь мы все свойства операционной системы готов tooset hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b110e-199">Now we are ready tooset hello virtual machine's operating system properties.</span></span> <span data-ttu-id="b110e-200">Мы будем использовать hello [набор AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) командлет tooset hello тип операционной системы Windows, требует hello [агент виртуальной машины](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe установлен, укажите, что hello включает автоматически обновление и задайте имя виртуальной машины hello, имя компьютера hello и hello учетные данные, используя hello переменные, которые ранее инициализирован.</span><span class="sxs-lookup"><span data-stu-id="b110e-200">We will use hello [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet tooset hello type of operating system as Windows, require hello [virtual machine agent](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe installed, specify that hello cmdlet enables auto update and set hello virtual machine name, hello computer name, and hello credential using hello variables that you previously initialized.</span></span>

<span data-ttu-id="b110e-201">Выполнение hello следующие свойства командлет tooset hello операционной системы для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b110e-201">Execute hello following cmdlet tooset hello operating system properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a><span data-ttu-id="b110e-202">Добавление hello сетевой интерфейс toohello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b110e-202">Add hello network interface toohello virtual machine</span></span>
<span data-ttu-id="b110e-203">Далее мы добавим hello сетевого интерфейса, созданного ранее toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b110e-203">Next, we will add hello network interface that we created previously toohello virtual machine.</span></span> <span data-ttu-id="b110e-204">Мы будем использовать hello [AzureRmVMNetworkInterface добавить](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) командлет tooadd hello сетевого интерфейса с помощью hello переменной сетевого интерфейса, определенного ранее.</span><span class="sxs-lookup"><span data-stu-id="b110e-204">We will use hello [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet tooadd hello network interface using hello network interface variable that you defined earlier.</span></span>

<span data-ttu-id="b110e-205">Выполнение hello, выполнив командлет tooset hello сетевого интерфейса для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b110e-205">Execute hello following cmdlet tooset hello network interface for your virtual machine.</span></span>

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a><span data-ttu-id="b110e-206">Задать место хранения большого двоичного объекта hello hello toobe диск, используемый виртуальной машиной hello</span><span class="sxs-lookup"><span data-stu-id="b110e-206">Set hello blob storage location for hello disk toobe used by hello virtual machine</span></span>
<span data-ttu-id="b110e-207">Затем мы определим место хранения большого двоичного объекта hello hello toobe диск, используемый виртуальной машиной hello hello переменных, определенных вами ранее.</span><span class="sxs-lookup"><span data-stu-id="b110e-207">Next, we will set hello blob storage location for hello disk toobe used by hello virtual machine using hello variables that you defined earlier.</span></span>

<span data-ttu-id="b110e-208">Выполните следующие места хранения больших двоичных объектов hello tooset командлет hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-208">Execute hello following cmdlet tooset hello blob storage location.</span></span>

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a><span data-ttu-id="b110e-209">Задайте свойства диска для виртуальной машины hello hello операционной системы</span><span class="sxs-lookup"><span data-stu-id="b110e-209">Set hello operating system disk properties for hello virtual machine</span></span>
<span data-ttu-id="b110e-210">Далее мы установим hello операционной системы свойства диска для виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-210">Next, we will set hello operating system disk properties for hello virtual machine.</span></span> <span data-ttu-id="b110e-211">Мы будем использовать hello [AzureRmVMOSDisk набор](/powershell/module/azurerm.compute/set-azurermvmosdisk) toospecify командлета, hello операционной системы для виртуальной машины hello поступит из образа, кэширование только tooread tooset (так как SQL Server устанавливается на hello общий диск) и определения имя виртуальной машины Hello и диск операционной системы hello, определяются с помощью hello переменные, которые было определено ранее.</span><span class="sxs-lookup"><span data-stu-id="b110e-211">We will use hello [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet toospecify that hello operating system for hello virtual machine will come from an image, tooset caching tooread only (because SQL Server is being installed on hello same disk) and define hello virtual machine name and hello operating system disk defined using hello variables that we defined earlier.</span></span>

<span data-ttu-id="b110e-212">Выполнение hello следующие свойства командлет tooset hello операционной системы диска для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b110e-212">Execute hello following cmdlet tooset hello operating system disk properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a><span data-ttu-id="b110e-213">Укажите образ платформы hello для hello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b110e-213">Specify hello platform image for hello virtual machine</span></span>
<span data-ttu-id="b110e-214">Наш последний шаг настройки — образ платформы hello toospecify для нашей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b110e-214">Our last configuration step is toospecify hello platform image for our virtual machine.</span></span> <span data-ttu-id="b110e-215">В этом руководстве мы используем hello последний образ SQL Server 2016 CTP.</span><span class="sxs-lookup"><span data-stu-id="b110e-215">For our tutorial, we are using hello latest SQL Server 2016 CTP image.</span></span> <span data-ttu-id="b110e-216">Мы будем использовать hello [AzureRmVMSourceImage набор](/powershell/module/azurerm.compute/set-azurermvmsourceimage) toouse командлет этот образ в соответствии с определением hello переменных, определенных вами ранее.</span><span class="sxs-lookup"><span data-stu-id="b110e-216">We will use hello [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse this image as defined by hello variables that you defined earlier.</span></span>

<span data-ttu-id="b110e-217">Выполнение hello, выполнив командлет образа платформы hello toospecify для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b110e-217">Execute hello following cmdlet toospecify hello platform image for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a><span data-ttu-id="b110e-218">Создать виртуальную Машину SQL hello</span><span class="sxs-lookup"><span data-stu-id="b110e-218">Create hello SQL VM</span></span>
<span data-ttu-id="b110e-219">Теперь, после завершения действия по настройке hello, все готово toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b110e-219">Now that you have finished hello configuration steps, you are ready toocreate hello virtual machine.</span></span> <span data-ttu-id="b110e-220">Мы будем использовать hello [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) командлет toocreate hello виртуальной машины с помощью hello переменные, которые мы определили.</span><span class="sxs-lookup"><span data-stu-id="b110e-220">We will use hello [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate hello virtual machine using hello variables that we have defined.</span></span>

<span data-ttu-id="b110e-221">Выполните следующий командлет toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b110e-221">Execute hello following cmdlet toocreate your virtual machine.</span></span>

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

<span data-ttu-id="b110e-222">создается виртуальная машина Hello.</span><span class="sxs-lookup"><span data-stu-id="b110e-222">hello virtual machine is created.</span></span> <span data-ttu-id="b110e-223">Обратите внимание, что стандартная учетная запись хранения создается для Диагностика загрузки поскольку hello указана учетная запись хранения для диска виртуальной машины hello — учетная запись хранения premium.</span><span class="sxs-lookup"><span data-stu-id="b110e-223">Notice that a standard storage account is created for boot diagnostics because hello specified storage account for hello virtual machine's disk is a premium storage account.</span></span>

<span data-ttu-id="b110e-224">Этот компьютер теперь можно просмотреть в toosee портала Azure hello [его общедоступный IP-адрес и его полное доменное имя](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="b110e-224">You can now view this machine in hello Azure Portal toosee [its public IP address and its fully qualified domain name](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="example-script"></a><span data-ttu-id="b110e-225">Пример сценария</span><span class="sxs-lookup"><span data-stu-id="b110e-225">Example script</span></span>
<span data-ttu-id="b110e-226">Hello следующий скрипт содержит hello полный скрипт PowerShell для этого учебника.</span><span class="sxs-lookup"><span data-stu-id="b110e-226">hello following script contains hello complete PowerShell script for this tutorial.</span></span> <span data-ttu-id="b110e-227">Он предполагает, что уже toouse подписки Azure приветствия программы установки с hello **добавить AzureRmAccount** и **AzureRmSubscription выберите** команд.</span><span class="sxs-lookup"><span data-stu-id="b110e-227">It assumes that you have already setup hello Azure subscription toouse with hello **Add-AzureRmAccount** and **Select-AzureRmSubscription** commands.</span></span>

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
    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create hello VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a><span data-ttu-id="b110e-228">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b110e-228">Next steps</span></span>
<span data-ttu-id="b110e-229">После создания виртуальной машины hello их готовности tooconnect toohello виртуальной машины с помощью подключения удаленного рабочего СТОЛА и установки.</span><span class="sxs-lookup"><span data-stu-id="b110e-229">After hello virtual machine is created, you are ready tooconnect toohello virtual machine using RDP and setup connectivity.</span></span> <span data-ttu-id="b110e-230">Дополнительные сведения см. в разделе [подключения виртуальной машины SQL Server в Azure (диспетчера ресурсов) tooa](virtual-machines-windows-sql-connect.md).</span><span class="sxs-lookup"><span data-stu-id="b110e-230">For more information, see [Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span></span>

