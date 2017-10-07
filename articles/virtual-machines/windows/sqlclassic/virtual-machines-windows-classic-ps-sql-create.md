---
title: "aaaCreate виртуальной машины SQL Server PowerShell Azure (классические) | Документы Microsoft"
description: "Содержит описание действий и сценарии PowerShell для создания виртуальной машины Azure на основе образа из коллекции образов виртуальных машин SQL Server. В этом разделе используется режим классическое развертывание hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: b14d5d9bc192fa0a21126395ee20ffd06b3bf47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a><span data-ttu-id="185d6-104">Подготовка виртуальной машины SQL Server к работе с помощью Azure PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="185d6-104">Provision a SQL Server virtual machine using Azure PowerShell (Classic)</span></span>

<span data-ttu-id="185d6-105">В этой статье шаги как toocreate виртуальной машины SQL Server в Azure с помощью hello командлеты PowerShell.</span><span class="sxs-lookup"><span data-stu-id="185d6-105">This article provides steps for how toocreate a SQL Server virtual machine in Azure by using hello PowerShell cmdlets.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="185d6-106">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="185d6-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="185d6-107">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="185d6-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="185d6-108">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="185d6-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="185d6-109">Hello диспетчера ресурсов версию этого раздела в разделе [подготовки виртуальной машины SQL Server с помощью диспетчера ресурсов Azure PowerShell](../sql/virtual-machines-windows-ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="185d6-109">For hello Resource Manager version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Resource Manager](../sql/virtual-machines-windows-ps-sql-create.md).</span></span>

### <a name="install-and-configure-powershell"></a><span data-ttu-id="185d6-110">Установка и настройка PowerShell</span><span class="sxs-lookup"><span data-stu-id="185d6-110">Install and configure PowerShell:</span></span>
1. <span data-ttu-id="185d6-111">Если у вас нет учетной записи Azure, используйте [бесплатную пробную версию Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="185d6-111">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
2. <span data-ttu-id="185d6-112">[Загрузите и установите последнюю команд Azure PowerShell hello](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="185d6-112">[Download and install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>
3. <span data-ttu-id="185d6-113">Запустите Windows PowerShell и подключите его tooyour подписки Azure с hello **Add-AzureAccount** команды.</span><span class="sxs-lookup"><span data-stu-id="185d6-113">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a><span data-ttu-id="185d6-114">Определение целевого региона Azure</span><span class="sxs-lookup"><span data-stu-id="185d6-114">Determine your target Azure region</span></span>

<span data-ttu-id="185d6-115">Ваша виртуальная машина SQL Server будет размещаться в облачной службе, которая находится в определенном регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="185d6-115">Your SQL Server Virtual Machine will be hosted in a cloud service that resides a specific Azure region.</span></span> <span data-ttu-id="185d6-116">Hello следующих шагов помочь toodetermine вы свой регион, учетной записи хранилища и облачную службу, которая будет использоваться для hello конца учебника hello.</span><span class="sxs-lookup"><span data-stu-id="185d6-116">hello following steps help you toodetermine your region, storage account, and cloud service that will be used for hello rest of hello tutorial.</span></span>

1. <span data-ttu-id="185d6-117">Определите hello центра обработки данных требуется toouse toohost ВМ SQL Server.</span><span class="sxs-lookup"><span data-stu-id="185d6-117">Determine hello data center that you want toouse toohost your SQL Server VM.</span></span> <span data-ttu-id="185d6-118">Hello следующую команду PowerShell отображает список доступных регионов.</span><span class="sxs-lookup"><span data-stu-id="185d6-118">hello following PowerShell command displays a list of available region names.</span></span>

   ```powershell
   (Get-AzureLocation).Name
   ```

2. <span data-ttu-id="185d6-119">После определения вашей предпочтительного источника задайте переменную с именем **$dcLocation** toothat области.</span><span class="sxs-lookup"><span data-stu-id="185d6-119">Once you've identified your preferred location, set a variable named **$dcLocation** toothat region.</span></span> <span data-ttu-id="185d6-120">Здравствуйте, например, следующая команда задает hello области слишком «Восток США»:</span><span class="sxs-lookup"><span data-stu-id="185d6-120">For example, hello following command sets hello region too"East US":</span></span>

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a><span data-ttu-id="185d6-121">Указание подписки и учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="185d6-121">Set your subscription and storage account</span></span>

1. <span data-ttu-id="185d6-122">Определите hello подписки Azure, которая будет использоваться для новой виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="185d6-122">Determine hello Azure subscription you will use for hello new virtual machine.</span></span>

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. <span data-ttu-id="185d6-123">Назначить подписки Azure к целевой toohello **$subscr** переменной.</span><span class="sxs-lookup"><span data-stu-id="185d6-123">Assign your target Azure subscription toohello **$subscr** variable.</span></span> <span data-ttu-id="185d6-124">Затем установите ее как текущую подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="185d6-124">Then set this as your current Azure subscription.</span></span>

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. <span data-ttu-id="185d6-125">После этого проверьте наличие существующих учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="185d6-125">Then check for existing storage accounts.</span></span> <span data-ttu-id="185d6-126">Hello следующий сценарий отображает все учетные записи хранения, которые существуют в вашем регионе выбранной:</span><span class="sxs-lookup"><span data-stu-id="185d6-126">hello following script displays all storage accounts that exist in your chosen region:</span></span>

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > <span data-ttu-id="185d6-127">Если требуется учетной записи хранения, следует сначала создайте имя учетной записи хранения все строчные с помощью команды New-AzureStorageAccount hello как следующий пример hello:`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span><span class="sxs-lookup"><span data-stu-id="185d6-127">If you require a new storage account, first create an all-lower-case storage account name with hello New-AzureStorageAccount command as in hello following example: `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span></span>

4. <span data-ttu-id="185d6-128">Назначить hello целевого хранилища учетной записи имя toohello **$staccount**.</span><span class="sxs-lookup"><span data-stu-id="185d6-128">Assign hello target storage account name toohello **$staccount**.</span></span> <span data-ttu-id="185d6-129">Затем с помощью **Set-AzureSubscription** tooset hello подписки и текущей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="185d6-129">Then use **Set-AzureSubscription** tooset hello subscription and current storage account.</span></span>

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a><span data-ttu-id="185d6-130">Выбор образа виртуальной машины SQL Server</span><span class="sxs-lookup"><span data-stu-id="185d6-130">Select a SQL Server virtual machine image</span></span>

1. <span data-ttu-id="185d6-131">Определить список доступных образов виртуальных машин SQL Server из коллекции hello hello.</span><span class="sxs-lookup"><span data-stu-id="185d6-131">Find out hello list of available SQL Server virtual machines images from hello gallery.</span></span> <span data-ttu-id="185d6-132">Свойство **ImageFamily** для этих образов начинается с «SQL».</span><span class="sxs-lookup"><span data-stu-id="185d6-132">These images all have an **ImageFamily** property that starts with "SQL".</span></span> <span data-ttu-id="185d6-133">Hello следующий запрос отображает hello образ семейства доступных tooyou, имеют предварительно установить SQL Server.</span><span class="sxs-lookup"><span data-stu-id="185d6-133">hello following query displays hello image family available tooyou that have SQL Server preinstalled.</span></span>

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. <span data-ttu-id="185d6-134">Найдя семейства образ виртуальной машины hello, может иметься несколько образов, опубликованных в этом семействе.</span><span class="sxs-lookup"><span data-stu-id="185d6-134">When you find hello  virtual machine image family, there could be multiple published images in this family.</span></span> <span data-ttu-id="185d6-135">Используйте hello следующий скрипт имя образа toofind hello последней опубликованной виртуальной машины для вашей семьи выбранное изображение (например, **SQL Server 2016 RTM Enterprise на Windows Server 2012 R2**):</span><span class="sxs-lookup"><span data-stu-id="185d6-135">Use hello following script toofind hello latest published virtual machine image name for your selected image family (such as **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):</span></span>

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a><span data-ttu-id="185d6-136">Создание виртуальной машины hello</span><span class="sxs-lookup"><span data-stu-id="185d6-136">Create hello virtual machine</span></span>

<span data-ttu-id="185d6-137">Наконец Создание hello виртуальной машины с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="185d6-137">Finally, create hello virtual machine with PowerShell:</span></span>

1. <span data-ttu-id="185d6-138">Создание облака service toohost hello новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="185d6-138">Create a cloud service toohost hello new VM.</span></span> <span data-ttu-id="185d6-139">Обратите внимание, что также возможно toouse существующую облачную службу вместо него.</span><span class="sxs-lookup"><span data-stu-id="185d6-139">Note that it is also possible toouse an existing cloud service instead.</span></span> <span data-ttu-id="185d6-140">Создать новую переменную **$svcname** с hello короткое имя hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="185d6-140">Create a new variable **$svcname** with hello short name of hello cloud service.</span></span>

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. <span data-ttu-id="185d6-141">Укажите имя виртуальной машины hello и размер.</span><span class="sxs-lookup"><span data-stu-id="185d6-141">Specify hello virtual machine name and a size.</span></span> <span data-ttu-id="185d6-142">Дополнительные сведения о размерах виртуальных машин см. в разделе [Размеры виртуальных машин в Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="185d6-142">For more information about virtual machine sizes, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. <span data-ttu-id="185d6-143">Укажите учетную запись локального администратора hello и пароль.</span><span class="sxs-lookup"><span data-stu-id="185d6-143">Specify hello local administrator account and password.</span></span>

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. <span data-ttu-id="185d6-144">Выполнения hello следующий скрипт toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="185d6-144">Run hello following script toocreate hello virtual machine.</span></span>

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> <span data-ttu-id="185d6-145">Дополнительные пояснения и параметры конфигурации см. в разделе hello **создайте свой набор команд** статьи [toocreate использование Azure PowerShell и предварительной настройки виртуальных машин на основе Windows](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="185d6-145">For additional explanation and configuration options, see hello **Build your command set** section in [Use Azure PowerShell toocreate and preconfigure Windows-based Virtual Machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="example-powershell-script"></a><span data-ttu-id="185d6-146">Пример сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="185d6-146">Example PowerShell script</span></span>

<span data-ttu-id="185d6-147">Hello следующий сценарий является примером полный скрипт, который создает **SQL Server 2016 RTM Enterprise на Windows Server 2012 R2** виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="185d6-147">hello following script provides an example of a complete script that creates a **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2** virtual machine.</span></span> <span data-ttu-id="185d6-148">Если вы используете этот сценарий, необходимо настроить hello начальной переменных, основанных на предыдущих шагах hello в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="185d6-148">If you use this script, you must customize hello initial variables based on hello previous steps in this topic.</span></span>

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set hello current subscription and storage account
# Comment out hello New-AzureStorageAccount line if hello account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select hello most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create hello new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create hello VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create hello SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a><span data-ttu-id="185d6-149">Подключение к удаленному рабочему столу</span><span class="sxs-lookup"><span data-stu-id="185d6-149">Connect with remote desktop</span></span>

1. <span data-ttu-id="185d6-150">Создание файлов RDP hello в toolaunch папке текущего пользователя hello документа установки toocomplete эти виртуальные машины:</span><span class="sxs-lookup"><span data-stu-id="185d6-150">Create hello RDP files in hello current user's document folder toolaunch these virtual machines toocomplete setup:</span></span>

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. <span data-ttu-id="185d6-151">В каталоге "документы" hello запустите hello RDP-файл.</span><span class="sxs-lookup"><span data-stu-id="185d6-151">In hello documents directory, launch hello RDP file.</span></span> <span data-ttu-id="185d6-152">Связь с hello имя пользователя администратора и пароль, предоставленные ранее (например, если имя пользователя было VMAdmin, укажите «\VMAdmin» в качестве пользователя hello и предоставить пароль hello).</span><span class="sxs-lookup"><span data-stu-id="185d6-152">Connect with hello administrator user name and password provided earlier (for example, if your user name was VMAdmin, specify "\VMAdmin" as hello user and provide hello password).</span></span>

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a><span data-ttu-id="185d6-153">Настройка завершения hello hello машины SQL Server для удаленного доступа</span><span class="sxs-lookup"><span data-stu-id="185d6-153">Complete hello configuration of hello SQL Server Machine for remote access</span></span>

<span data-ttu-id="185d6-154">После входа в систему компьютера toohello с удаленным рабочим столом, настройте SQL Server в соответствии с инструкциями hello в [действия для настройки подключения к SQL Server на виртуальной Машине Azure](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="185d6-154">After logging on toohello machine with remote desktop, configure SQL Server based on hello instructions in [Steps for configuring SQL Server connectivity in an Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

## <a name="next-steps"></a><span data-ttu-id="185d6-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="185d6-155">Next steps</span></span>

<span data-ttu-id="185d6-156">Имеются дополнительные инструкции для подготовки виртуальных машин с помощью PowerShell в hello [документация по виртуальным машинам](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="185d6-156">You can find additional instructions for provisioning virtual machines with PowerShell in hello [virtual machines documentation](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="185d6-157">Во многих случаях hello следующим шагом является toomigrate toothis вашей базы данных новую виртуальную Машину SQL Server.</span><span class="sxs-lookup"><span data-stu-id="185d6-157">In many cases, hello next step is toomigrate your databases toothis new SQL Server VM.</span></span> <span data-ttu-id="185d6-158">Руководство по миграции базы данных см. в разделе [миграция tooSQL базы данных сервера на Виртуальной машине Azure](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="185d6-158">For database migration guidance, see [Migrating a Database tooSQL Server on an Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="185d6-159">Если вы хотите использовать hello Azure портала toocreate виртуальных машин SQL, см. раздел [подготовки виртуальной машины SQL Server в Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="185d6-159">If you're also interested in using hello Azure portal toocreate SQL Virtual Machines, see [Provisioning a SQL Server Virtual Machine on Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="185d6-160">Обратите внимание, что учебника hello hello, проходит через портал hello создает виртуальных машин с помощью модели рекомендуется диспетчера ресурсов, а не hello классической модели, используемые в данном разделе PowerShell.</span><span class="sxs-lookup"><span data-stu-id="185d6-160">Note that hello tutorial that walks you through hello portal creates VMs using hello recommended Resource Manager model, rather than hello classic model used in this PowerShell topic.</span></span>

<span data-ttu-id="185d6-161">Кроме toothese ресурсов, рекомендуется изучить [другие разделы, посвященные toorunning SQL Server в виртуальных машинах Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="185d6-161">In addition toothese resources, we recommend that you review [other topics related toorunning SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
