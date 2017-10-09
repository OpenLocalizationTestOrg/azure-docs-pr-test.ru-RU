---
title: "aaaConfigure hello группы доступности AlwaysOn на Виртуальной машине Azure с помощью PowerShell | Документы Microsoft"
description: "В этом учебнике используется ресурсов, которые были созданы с помощью hello классической модели развертывания. Используйте PowerShell toocreate группы доступности AlwaysOn в Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a4e2f175-fe56-4218-86c7-a43fb916cc64
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: d4a27e203b2ff299adebec2b010c03422459b3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-always-on-availability-group-on-an-azure-vm-with-powershell"></a><span data-ttu-id="a4a0a-104">Настройка группы доступности Always On для hello на Виртуальной машине Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4a0a-104">Configure hello Always On availability group on an Azure VM with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4a0a-105">Классическая модель: пользовательский интерфейс</span><span class="sxs-lookup"><span data-stu-id="a4a0a-105">Classic: UI</span></span>](../classic/portal-sql-alwayson-availability-groups.md)
> * <span data-ttu-id="a4a0a-106">[Классическая модель: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span><span class="sxs-lookup"><span data-stu-id="a4a0a-106">[Classic: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span></span><br/>

<span data-ttu-id="a4a0a-107">Прежде чем начать, учтите, что теперь можно выполнить эту задачу в модели Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-107">Before you begin, consider that you can now complete this task in Azure resource manager model.</span></span> <span data-ttu-id="a4a0a-108">Для новых развертываний мы советуем использовать модель Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-108">We recommend Azure resource manager model for new deployments.</span></span> <span data-ttu-id="a4a0a-109">См. сведения в статье [Введение в группы доступности Always On SQL Server на виртуальных машинах Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4a0a-109">See [SQL Server Always On availability groups on Azure virtual machines](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4a0a-110">Корпорация Майкрософт рекомендует наиболее новые развертывания для использования модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-110">We recommend that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="a4a0a-111">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a4a0a-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a4a0a-112">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-112">This article covers using hello classic deployment model.</span></span>

<span data-ttu-id="a4a0a-113">Виртуальные машины (VM) Azure может помочь стоимости hello toolower администраторы базы данных системы SQL Server высокой доступности.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-113">Azure virtual machines (VMs) can help database administrators toolower hello cost of a high-availability SQL Server system.</span></span> <span data-ttu-id="a4a0a-114">Этот учебник показывает, как группировать tooimplement доступности с помощью SQL Server Always On end-to-end среде Azure.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-114">This tutorial shows you how tooimplement an availability group by using SQL Server Always On end-to-end inside an Azure environment.</span></span> <span data-ttu-id="a4a0a-115">В конце учебника hello hello решения AlwaysOn в SQL Server в Azure будет состоять из hello следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="a4a0a-115">At hello end of hello tutorial, your SQL Server Always On solution in Azure will consist of hello following elements:</span></span>

* <span data-ttu-id="a4a0a-116">Виртуальной сети, которая содержит множество подсетей, в том числе внешнюю и внутреннюю подсети;</span><span class="sxs-lookup"><span data-stu-id="a4a0a-116">A virtual network that contains multiple subnets, including a front-end and a back-end subnet.</span></span>
* <span data-ttu-id="a4a0a-117">контроллера домена с доменом Active Directory;</span><span class="sxs-lookup"><span data-stu-id="a4a0a-117">A domain controller with an Active Directory domain.</span></span>
* <span data-ttu-id="a4a0a-118">Две виртуальные машины SQL Server, развернутые toohello внутренней подсети и присоединены к домену toohello домена Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-118">Two SQL Server VMs that are deployed toohello back-end subnet and joined toohello Active Directory domain.</span></span>
* <span data-ttu-id="a4a0a-119">Отказоустойчивый кластер Windows трех узлов с моделью кворума большинства узлов hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-119">A three-node Windows failover cluster with hello Node Majority quorum model.</span></span>
* <span data-ttu-id="a4a0a-120">группы доступности с двумя репликами с синхронной фиксацией базы данных доступности.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-120">An availability group with two synchronous-commit replicas of an availability database.</span></span>

<span data-ttu-id="a4a0a-121">Этот сценарий — хороший выбор из-за его простоты на Azure, а не из-за его экономичности или других факторов.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-121">This scenario is a good choice for its simplicity on Azure, not for its cost-effectiveness or other factors.</span></span> <span data-ttu-id="a4a0a-122">Например можно свести к минимуму hello число виртуальных машин для группы доступности с двумя репликами toosave часы вычислительных операций в Azure, используя hello контроллер домена как следящую общую папку hello кворума в кластере отработки отказа двух узлов.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-122">For example, you can minimize hello number of VMs for a two-replica availability group toosave on compute hours in Azure by using hello domain controller as hello quorum file share witness in a two-node failover cluster.</span></span> <span data-ttu-id="a4a0a-123">Этот метод уменьшает число виртуальных Машин hello из hello выше конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-123">This method reduces hello VM count by one from hello above configuration.</span></span>

<span data-ttu-id="a4a0a-124">Этот учебник предназначен, что tooshow hello шаги, необходимые tooset копирование hello описано решение выше, не приводятся подробные сведения каждого этапа hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-124">This tutorial is intended tooshow you hello steps that are required tooset up hello described solution above, without elaborating on hello details of each step.</span></span> <span data-ttu-id="a4a0a-125">Таким образом вместо обеспечивает действия по настройке hello графического пользовательского интерфейса, он использует tootake сценариев PowerShell можно быстро через каждый шаг.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-125">Therefore, instead of providing hello GUI configuration steps, it uses PowerShell scripting tootake you quickly through each step.</span></span> <span data-ttu-id="a4a0a-126">В этом учебнике предполагается hello следующее:</span><span class="sxs-lookup"><span data-stu-id="a4a0a-126">This tutorial assumes hello following:</span></span>

* <span data-ttu-id="a4a0a-127">Уже имеется учетная запись Azure с подпиской для виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-127">You already have an Azure account with hello virtual machine subscription.</span></span>
* <span data-ttu-id="a4a0a-128">После установки hello [командлетов Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a4a0a-128">You've installed hello [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>
* <span data-ttu-id="a4a0a-129">Вы хорошо понимаете принцип работы групп доступности Always On в локальных решениях.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-129">You already have a solid understanding of Always On availability groups for on-premises solutions.</span></span> <span data-ttu-id="a4a0a-130">Дополнительные сведения см. в разделе [Группы доступности AlwaysOn (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4a0a-130">For more information, see [Always On availability groups (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span></span>

## <a name="connect-tooyour-azure-subscription-and-create-hello-virtual-network"></a><span data-ttu-id="a4a0a-131">Подключение tooyour подписки Azure и создать виртуальную сеть hello</span><span class="sxs-lookup"><span data-stu-id="a4a0a-131">Connect tooyour Azure subscription and create hello virtual network</span></span>
1. <span data-ttu-id="a4a0a-132">В окне PowerShell на локальном компьютере импортируйте модуль Azure hello, загрузите hello машины tooyour файл параметров публикации и подключения к tooyour сеанса PowerShell подписки Azure путем импорта hello загрузки параметров публикации.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-132">In a PowerShell window on your local computer, import hello Azure module, download hello publishing settings file tooyour machine, and connect your PowerShell session tooyour Azure subscription by importing hello downloaded publishing settings.</span></span>

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    <span data-ttu-id="a4a0a-133">Hello **Get-AzurePublishSettingsFile** команда автоматически создает сертификат управления с помощью Azure и загружает его tooyour машины.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-133">hello **Get-AzurePublishSettingsFile** command automatically generates a management certificate with Azure and downloads it tooyour machine.</span></span> <span data-ttu-id="a4a0a-134">Автоматически откроется браузер, и все данные учетной записи Майкрософт запрос tooenter hello для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-134">A browser is automatically opened, and you're prompted tooenter hello Microsoft account credentials for your Azure subscription.</span></span> <span data-ttu-id="a4a0a-135">загружаются Hello **.publishsettings** файле содержится вся информация hello требуется toomanage подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-135">hello downloaded **.publishsettings** file contains all hello information that you need toomanage your Azure subscription.</span></span> <span data-ttu-id="a4a0a-136">После сохранения этого файла tooa локальный каталог, импортировать его, используя hello **команду Import-AzurePublishSettingsFile** команды.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-136">After saving this file tooa local directory, import it by using hello **Import-AzurePublishSettingsFile** command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a4a0a-137">файл PUBLISHSETTINGS Hello содержит учетные данные (Незакодированные), используемые tooadminister подписки Azure и служб.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-137">hello .publishsettings file contains your credentials (unencoded) that are used tooadminister your Azure subscriptions and services.</span></span> <span data-ttu-id="a4a0a-138">Hello рекомендации по безопасности для этого файла является toostore он временно за пределами исходных каталогов (например, в папке Libraries\Documents hello), а затем удалите его после завершения импорта hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-138">hello security best practice for this file is toostore it temporarily outside your source directories (for example, in hello Libraries\Documents folder), and then delete it after hello import has finished.</span></span> <span data-ttu-id="a4a0a-139">Злоумышленник, получивший доступ toohello PUBLISHSETTINGS-файл можно изменять, создавать и удалять служб Azure.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-139">A malicious user who gains access toohello .publishsettings file can edit, create, and delete your Azure services.</span></span>

2. <span data-ttu-id="a4a0a-140">Определите ряд переменных, вы сможете использовать toocreate облачной ИТ-инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-140">Define a series of variables that you'll use toocreate your cloud IT infrastructure.</span></span>

        $location = "West US"
        $affinityGroupName = "ContosoAG"
        $affinityGroupDescription = "Contoso SQL HADR Affinity Group"
        $affinityGroupLabel = "IaaS BI Affinity Group"
        $networkConfigPath = "C:\scripts\Network.netcfg"
        $virtualNetworkName = "ContosoNET"
        $storageAccountName = "<uniquestorageaccountname>"
        $storageAccountLabel = "Contoso SQL HADR Storage Account"
        $storageAccountContainer = "https://" + $storageAccountName + ".blob.core.windows.net/vhds/"
        $winImageName = (Get-AzureVMImage | where {$_.Label -like "Windows Server 2008 R2 SP1*"} | sort PublishedDate -Descending)[0].ImageName
        $sqlImageName = (Get-AzureVMImage | where {$_.Label -like "SQL Server 2012 SP1 Enterprise*"} | sort PublishedDate -Descending)[0].ImageName
        $dcServerName = "ContosoDC"
        $dcServiceName = "<uniqueservicename>"
        $availabilitySetName = "SQLHADR"
        $vmAdminUser = "AzureAdmin"
        $vmAdminPassword = "Contoso!000"
        $workingDir = "c:\scripts\"

    <span data-ttu-id="a4a0a-141">Обратите внимания toohello после tooensure, который позднее будет успешным команды:</span><span class="sxs-lookup"><span data-stu-id="a4a0a-141">Pay attention toohello following tooensure that your commands will succeed later:</span></span>

   * <span data-ttu-id="a4a0a-142">Переменные **$storageAccountName** и **$dcServiceName** должно быть уникальным, так как они используются tooidentify вашей учетная запись облачного хранилища и облачного сервера соответственно на hello Интернет.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-142">Variables **$storageAccountName** and **$dcServiceName** must be unique because they're used tooidentify your cloud storage account and cloud server, respectively, on hello Internet.</span></span>
   * <span data-ttu-id="a4a0a-143">Здравствуйте, имена, указанные для переменных **$affinityGroupName** и **$virtualNetworkName** настраиваются в документе конфигурации hello виртуальной сети, которые будут использоваться позже.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-143">hello names that you specify for variables **$affinityGroupName** and **$virtualNetworkName** are configured in hello virtual network configuration document that you'll use later.</span></span>
   * <span data-ttu-id="a4a0a-144">**$sqlImageName** указывает hello обновить имя образа виртуальной Машины hello, который содержит SQL Server 2012 Service Pack 1 Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-144">**$sqlImageName** specifies hello updated name of hello VM image that contains SQL Server 2012 Service Pack 1 Enterprise Edition.</span></span>
   * <span data-ttu-id="a4a0a-145">Для простоты **Contoso! 000** Здравствуйте, же пароль, который используется на протяжении всего учебника hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-145">For simplicity, **Contoso!000** is hello same password that's used throughout hello entire tutorial.</span></span>

3. <span data-ttu-id="a4a0a-146">Создайте территориальную группу</span><span class="sxs-lookup"><span data-stu-id="a4a0a-146">Create an affinity group.</span></span>

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. <span data-ttu-id="a4a0a-147">Создайте виртуальную сеть, импортировав файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-147">Create a virtual network by importing a configuration file.</span></span>

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    <span data-ttu-id="a4a0a-148">файл конфигурации Hello содержит следующие XML-документ hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-148">hello configuration file contains hello following XML document.</span></span> <span data-ttu-id="a4a0a-149">Вкратце, он указывает виртуальную сеть с именем **ContosoNET** в территориальной группе hello вызывается **ContosoAG**.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-149">In brief, it specifies a virtual network called **ContosoNET** in hello affinity group called **ContosoAG**.</span></span> <span data-ttu-id="a4a0a-150">Он имеет hello адресное пространство **10.10.0.0/16** и две подсети **10.10.1.0/24** и **10.10.2.0/24**, являющиеся интерфейсной подсети hello и задней подсеть соответственно.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-150">It has hello address space **10.10.0.0/16** and has two subnets, **10.10.1.0/24** and **10.10.2.0/24**, which are hello front subnet and back subnet, respectively.</span></span> <span data-ttu-id="a4a0a-151">Hello интерфейсной подсети — расположения клиентские приложения, например Microsoft SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-151">hello front subnet is where you can place client applications such as Microsoft SharePoint.</span></span> <span data-ttu-id="a4a0a-152">Hello конечной подсети является расположения hello виртуальные машины SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-152">hello back subnet is where you'll place hello SQL Server VMs.</span></span> <span data-ttu-id="a4a0a-153">При изменении hello **$affinityGroupName** и **$virtualNetworkName** переменных ранее, необходимо также изменить соответствующие имена ниже hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-153">If you change hello **$affinityGroupName** and **$virtualNetworkName** variables earlier, you must also change hello corresponding names below.</span></span>

        <NetworkConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <Dns />
            <VirtualNetworkSites>
              <VirtualNetworkSite name="ContosoNET" AffinityGroup="ContosoAG">
                <AddressSpace>
                  <AddressPrefix>10.10.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="Front">
                    <AddressPrefix>10.10.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="Back">
                    <AddressPrefix>10.10.2.0/24</AddressPrefix>
                  </Subnet>
                </Subnets>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

5. <span data-ttu-id="a4a0a-154">Создайте учетную запись хранилища, связанной с hello территориальная группа создана и задать его в качестве текущей учетной записи хранилища hello в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-154">Create a storage account that's associated with hello affinity group that you created, and set it as hello current storage account in your subscription.</span></span>

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. <span data-ttu-id="a4a0a-155">Создайте сервер контроллера домена hello в hello новой облачной службе и группе доступности.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-155">Create hello domain controller server in hello new cloud service and availability set.</span></span>

        New-AzureVMConfig `
            -Name $dcServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$dcServerName.vhd" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -Windows `
                -DisableAutomaticUpdates `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword |
                New-AzureVM `
                    -ServiceName $dcServiceName `
                    –AffinityGroup $affinityGroupName `
                    -VNetName $virtualNetworkName

    <span data-ttu-id="a4a0a-156">Эти перенаправленные команды hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a4a0a-156">These piped commands do hello following things:</span></span>

   * <span data-ttu-id="a4a0a-157">**New-AzureVMConfig** создает конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-157">**New-AzureVMConfig** creates a VM configuration.</span></span>
   * <span data-ttu-id="a4a0a-158">**-AzureProvisioningConfig** дает hello параметры конфигурации изолированного сервера Windows.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-158">**Add-AzureProvisioningConfig** gives hello configuration parameters of a standalone Windows server.</span></span>
   * <span data-ttu-id="a4a0a-159">**-AzureDataDisk** добавляет диск данных hello, который будет использоваться для хранения данных Active Directory с кэширование параметр set tooNone hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-159">**Add-AzureDataDisk** adds hello data disk that you'll use for storing Active Directory data, with hello caching option set tooNone.</span></span>
   * <span data-ttu-id="a4a0a-160">**Новый-AzureVM** создает новую облачную службу, а hello новой виртуальной Машины Azure в новой облачной службе hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-160">**New-AzureVM** creates a new cloud service and creates hello new Azure VM in hello new cloud service.</span></span>

7. <span data-ttu-id="a4a0a-161">Дождитесь hello toobe новой виртуальной Машины полностью подготовлены и загрузить hello файл удаленного рабочего стола tooyour рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-161">Wait for hello new VM toobe fully provisioned, and download hello remote desktop file tooyour working directory.</span></span> <span data-ttu-id="a4a0a-162">Здравствуйте, так как hello новой виртуальной Машины Azure использует tooprovision много времени, `while` цикл продолжает toopoll hello новой виртуальной Машины, пока он не готов к использованию.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-162">Because hello new Azure VM takes a long time tooprovision, hello `while` loop continues toopoll hello new VM until it's ready for use.</span></span>

        $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName

        While ($VMStatus.InstanceStatus -ne "ReadyRole")
        {
            write-host "Waiting for " $VMStatus.Name "... Current Status = " $VMStatus.InstanceStatus
            Start-Sleep -Seconds 15
            $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName
        }

        Get-AzureRemoteDesktopFile `
            -ServiceName $dcServiceName `
            -Name $dcServerName `
            -LocalPath "$workingDir$dcServerName.rdp"

<span data-ttu-id="a4a0a-163">Hello сервера контроллера домена успешно подготовлен.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-163">hello domain controller server is now successfully provisioned.</span></span> <span data-ttu-id="a4a0a-164">Далее следует настроить hello домена Active Directory на этом сервере контроллера домена.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-164">Next, you'll configure hello Active Directory domain on this domain controller server.</span></span> <span data-ttu-id="a4a0a-165">Не закрывайте окно hello PowerShell на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-165">Leave hello PowerShell window open on your local computer.</span></span> <span data-ttu-id="a4a0a-166">Оно будет использоваться снова далее toocreate hello две виртуальные машины SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-166">You'll use it again later toocreate hello two SQL Server VMs.</span></span>

## <a name="configure-hello-domain-controller"></a><span data-ttu-id="a4a0a-167">Настройка контроллера домена hello</span><span class="sxs-lookup"><span data-stu-id="a4a0a-167">Configure hello domain controller</span></span>
1. <span data-ttu-id="a4a0a-168">Подключитесь toohello сервера контроллера домена, запустив файл удаленного рабочего стола hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-168">Connect toohello domain controller server by launching hello remote desktop file.</span></span> <span data-ttu-id="a4a0a-169">Использовать AzureAdmin имя пользователя и пароль администратора машины hello **Contoso! 000**, который был указан при создании hello новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-169">Use hello machine administrator’s username AzureAdmin and password **Contoso!000**, which you specified when you created hello new VM.</span></span>
2. <span data-ttu-id="a4a0a-170">Откройте окно PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-170">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="a4a0a-171">Запустите следующие hello **DCPROMO. EXE** tooset команду копирования hello **corp.contoso.com** домен с hello каталоги данных на диск M.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-171">Run hello following **DCPROMO.EXE** command tooset up hello **corp.contoso.com** domain, with hello data directories on drive M.</span></span>

        dcpromo.exe `
            /unattend `
            /ReplicaOrNewDomain:Domain `
            /NewDomain:Forest `
            /NewDomainDNSName:corp.contoso.com `
            /ForestLevel:4 `
            /DomainNetbiosName:CORP `
            /DomainLevel:4 `
            /InstallDNS:Yes `
            /ConfirmGc:Yes `
            /CreateDNSDelegation:No `
            /DatabasePath:"C:\Windows\NTDS" `
            /LogPath:"C:\Windows\NTDS" `
            /SYSVOLPath:"C:\Windows\SYSVOL" `
            /SafeModeAdminPassword:"Contoso!000"

    <span data-ttu-id="a4a0a-172">После завершения выполнения команды hello hello виртуальная машина автоматически перезапустится.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-172">After hello command finishes, hello VM restarts automatically.</span></span>

4. <span data-ttu-id="a4a0a-173">Повторное подключение toohello сервера контроллера домена, запустив файл удаленного рабочего стола hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-173">Connect toohello domain controller server again by launching hello remote desktop file.</span></span> <span data-ttu-id="a4a0a-174">На этот раз войдите с именем **CORP\Administrator**.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-174">This time, sign in as **CORP\Administrator**.</span></span>
5. <span data-ttu-id="a4a0a-175">Откройте окно PowerShell с правами администратора и импортируйте модуль Active Directory PowerShell hello с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a4a0a-175">Open a PowerShell window in administrator mode, and import hello Active Directory PowerShell module by using hello following command:</span></span>

        Import-Module ActiveDirectory

6. <span data-ttu-id="a4a0a-176">Выполните следующие команды tooadd трех пользователей toohello домена hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-176">Run hello following commands tooadd three users toohello domain.</span></span>

        $pwd = ConvertTo-SecureString "Contoso!000" -AsPlainText -Force
        New-ADUser `
            -Name 'Install' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc1' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc2' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true

    <span data-ttu-id="a4a0a-177">**CORP\Install** является используется tooconfigure все данные, связанные с экземплярами службы SQL Server toohello, hello отказоустойчивого кластера группы доступности hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-177">**CORP\Install** is used tooconfigure everything related toohello SQL Server service instances, hello failover cluster, and hello availability group.</span></span> <span data-ttu-id="a4a0a-178">**CORP\SQLSvc1** и **CORP\SQLSvc2** , используются в качестве учетных записей служб SQL Server hello hello двух виртуальных машин SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-178">**CORP\SQLSvc1** and **CORP\SQLSvc2** are used as hello SQL Server service accounts for hello two SQL Server VMs.</span></span>
7. <span data-ttu-id="a4a0a-179">Hello Далее, выполните следующие команды toogive **CORP\Install** hello разрешения toocreate объектов-компьютеров в домене hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-179">Next, run hello following commands toogive **CORP\Install** hello permissions toocreate computer objects in hello domain.</span></span>

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    <span data-ttu-id="a4a0a-180">Hello GUID, указанный выше — hello GUID для типа объекта компьютера hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-180">hello GUID specified above is hello GUID for hello computer object type.</span></span> <span data-ttu-id="a4a0a-181">Hello **CORP\Install** учетная запись должна hello **чтение всех свойств** и **создание объектов-компьютеров** Active Direct hello toocreate разрешение объектов для отработки отказа hello кластер.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-181">hello **CORP\Install** account needs hello **Read All Properties** and **Create Computer Objects** permission toocreate hello Active Direct objects for hello failover cluster.</span></span> <span data-ttu-id="a4a0a-182">Hello **чтение всех свойств** разрешение уже предоставлено tooCORP\Install по умолчанию, поэтому не требуется toogrant его явным образом.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-182">hello **Read All Properties** permission is already given tooCORP\Install by default, so you don't need toogrant it explicitly.</span></span> <span data-ttu-id="a4a0a-183">Дополнительные сведения о разрешениях, необходимых toocreate hello отказоустойчивого кластера, см. в разделе [Пошаговое руководство по отказоустойчивому кластеру: Настройка учетных записей в Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4a0a-183">For more information on permissions that are needed toocreate hello failover cluster, see [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span></span>

    <span data-ttu-id="a4a0a-184">Теперь, после завершения настройки Active Directory и объектов пользователей hello, вы создадите двух виртуальных машин SQL Server и присоединить их toothis домена.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-184">Now that you've finished configuring Active Directory and hello user objects, you'll create two SQL Server VMs and join them toothis domain.</span></span>

## <a name="create-hello-sql-server-vms"></a><span data-ttu-id="a4a0a-185">Создание виртуальных машин SQL Server hello</span><span class="sxs-lookup"><span data-stu-id="a4a0a-185">Create hello SQL Server VMs</span></span>
1. <span data-ttu-id="a4a0a-186">По-прежнему toouse окно hello PowerShell, открытое на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-186">Continue toouse hello PowerShell window that's open on your local computer.</span></span> <span data-ttu-id="a4a0a-187">Определите следующие дополнительные переменные hello:</span><span class="sxs-lookup"><span data-stu-id="a4a0a-187">Define hello following additional variables:</span></span>

        $domainName= "corp"
        $FQDN = "corp.contoso.com"
        $subnetName = "Back"
        $sqlServiceName = "<uniqueservicename>"
        $quorumServerName = "ContosoQuorum"
        $sql1ServerName = "ContosoSQL1"
        $sql2ServerName = "ContosoSQL2"
        $availabilitySetName = "SQLHADR"
        $dataDiskSize = 100
        $dnsSettings = New-AzureDns -Name "ContosoBackDNS" -IPAddress "10.10.0.4"

    <span data-ttu-id="a4a0a-188">Здравствуйте, IP-адрес **10.10.0.4** toohello обычно назначается первой виртуальной Машины, созданной в hello **10.10.0.0/16** подсети виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-188">hello IP address **10.10.0.4** is typically assigned toohello first VM that you create in hello **10.10.0.0/16** subnet of your Azure virtual network.</span></span> <span data-ttu-id="a4a0a-189">Следует убедиться, что это hello адрес сервера контроллера домена, запустив **IPCONFIG**.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-189">You should verify that this is hello address of your domain controller server by running **IPCONFIG**.</span></span>
2. <span data-ttu-id="a4a0a-190">С именем виртуальной Машины в отказоустойчивом кластере hello, выполнения hello следующий набор команд toocreate hello сначала **ContosoQuorum**:</span><span class="sxs-lookup"><span data-stu-id="a4a0a-190">Run hello following piped commands toocreate hello first VM in hello failover cluster, named **ContosoQuorum**:</span></span>

        New-AzureVMConfig `
            -Name $quorumServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$quorumServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    New-AzureVM `
                        -ServiceName $sqlServiceName `
                        –AffinityGroup $affinityGroupName `
                        -VNetName $virtualNetworkName `
                        -DnsSettings $dnsSettings

    <span data-ttu-id="a4a0a-191">Обратите внимание hello следующее относительно приведенных выше команд hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-191">Note hello following regarding hello command above:</span></span>

   * <span data-ttu-id="a4a0a-192">**Новый AzureVMConfig** создает конфигурацию виртуальной Машины с hello заданным именем группы доступности.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-192">**New-AzureVMConfig** creates a VM configuration with hello desired availability set name.</span></span> <span data-ttu-id="a4a0a-193">Hello последующие виртуальные машины будут созданы со hello же имя набора доступности, чтобы все они присоединены toohello одной группе доступности.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-193">hello subsequent VMs will be created with hello same availability set name so that they're joined toohello same availability set.</span></span>
   * <span data-ttu-id="a4a0a-194">**-AzureProvisioningConfig** соединения hello домена Active Directory toohello виртуальной Машины, созданной.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-194">**Add-AzureProvisioningConfig** joins hello VM toohello Active Directory domain that you created.</span></span>
   * <span data-ttu-id="a4a0a-195">**SET-AzureSubnet** местах hello виртуальной Машины в конечной подсети hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-195">**Set-AzureSubnet** places hello VM in hello back subnet.</span></span>
   * <span data-ttu-id="a4a0a-196">**Новый-AzureVM** создает новую облачную службу, а hello новой виртуальной Машины Azure в новой облачной службе hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-196">**New-AzureVM** creates a new cloud service and creates hello new Azure VM in hello new cloud service.</span></span> <span data-ttu-id="a4a0a-197">Hello **DnsSettings** для hello серверов в новой облачной службе hello имеет hello IP-адрес указывает этот DNS-сервер hello **10.10.0.4**.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-197">hello **DnsSettings** parameter specifies that hello DNS server for hello servers in hello new cloud service has hello IP address **10.10.0.4**.</span></span> <span data-ttu-id="a4a0a-198">Это IP-адрес сервера контроллера домена hello hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-198">This is hello IP address of hello domain controller server.</span></span> <span data-ttu-id="a4a0a-199">Этот параметр необходим tooenable hello новых виртуальных машин в домене Active Directory для службы toojoin hello облака toohello успешно.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-199">This parameter is needed tooenable hello new VMs in hello cloud service toojoin toohello Active Directory domain successfully.</span></span> <span data-ttu-id="a4a0a-200">Без этого параметра необходимо вручную задать параметры IPv4 hello в вашей виртуальной Машины toouse hello контроллер домена как основной DNS-сервер hello после подготовки hello виртуальной Машины и затем присоединить домену Active Directory toohello hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-200">Without this parameter, you must manually set hello IPv4 settings in your VM toouse hello domain controller server as hello primary DNS server after hello VM is provisioned, and then join hello VM toohello Active Directory domain.</span></span>
3. <span data-ttu-id="a4a0a-201">Выполнения hello следующие выведенной команды toocreate hello виртуальные машины SQL Server с именем **ContosoSQL1** и **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-201">Run hello following piped commands toocreate hello SQL Server VMs, named **ContosoSQL1** and **ContosoSQL2**.</span></span>

        # Create ContosoSQL1...
        New-AzureVMConfig `
            -Name $sql1ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql1ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 1 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

        # Create ContosoSQL2...
        New-AzureVMConfig `
            -Name $sql2ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql2ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 2 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

    <span data-ttu-id="a4a0a-202">Обратите внимание hello следующее относительно hello показанные выше команды.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-202">Note hello following regarding hello commands above:</span></span>

   * <span data-ttu-id="a4a0a-203">**Новый AzureVMConfig** использует hello же имя набора доступности как контроллер домена hello и использует hello образа SQL Server 2012 Service Pack 1 Enterprise Edition в коллекции виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-203">**New-AzureVMConfig** uses hello same availability set name as hello domain controller server, and uses hello SQL Server 2012 Service Pack 1 Enterprise Edition image in hello virtual machine gallery.</span></span> <span data-ttu-id="a4a0a-204">Он также устанавливает hello операционной системы диска tooread кэша (запрет записи в кэш).</span><span class="sxs-lookup"><span data-stu-id="a4a0a-204">It also sets hello operating system disk tooread-caching only (no write caching).</span></span> <span data-ttu-id="a4a0a-205">Мы рекомендуем hello базы данных файлы tooa отдельный диск с данными присоединения toohello виртуальной Машины и настроить в нем нет чтение или кэширование записи.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-205">We recommend that you migrate hello database files tooa separate data disk that you attach toohello VM, and configure it with no read or write caching.</span></span> <span data-ttu-id="a4a0a-206">Однако Наилучшая альтернатива hello это tooremove кэширование записи на диск операционной системы hello, так как не удается удалить кэширование на диске операционной системы hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-206">However, hello next best thing is tooremove write caching on hello operating system disk because you can't remove read caching on hello operating system disk.</span></span>
   * <span data-ttu-id="a4a0a-207">**-AzureProvisioningConfig** соединения hello домена Active Directory toohello виртуальной Машины, созданной.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-207">**Add-AzureProvisioningConfig** joins hello VM toohello Active Directory domain that you created.</span></span>
   * <span data-ttu-id="a4a0a-208">**SET-AzureSubnet** местах hello виртуальной Машины в конечной подсети hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-208">**Set-AzureSubnet** places hello VM in hello back subnet.</span></span>
   * <span data-ttu-id="a4a0a-209">**-AzureEndpoint** добавляет конечные точки доступа, чтобы клиентские приложения могут обращаться к эти экземпляры служб SQL Server на hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-209">**Add-AzureEndpoint** adds access endpoints so that client applications can access these SQL Server services instances on hello Internet.</span></span> <span data-ttu-id="a4a0a-210">Другие порты, получают tooContosoSQL1 и ContosoSQL2.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-210">Different ports are given tooContosoSQL1 and ContosoSQL2.</span></span>
   * <span data-ttu-id="a4a0a-211">**Новый-AzureVM** создает hello новую виртуальную Машину SQL Server в hello же облачную службу как ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-211">**New-AzureVM** creates hello new SQL Server VM in hello same cloud service as ContosoQuorum.</span></span> <span data-ttu-id="a4a0a-212">Виртуальные машины hello необходимо поместить в hello же облачную службу при необходимости toobe в одной группе доступности hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-212">You must place hello VMs in hello same cloud service if you want them toobe in hello same availability set.</span></span>
4. <span data-ttu-id="a4a0a-213">Дождитесь каждого toobe ВМ полностью подготовлены, а для каждой виртуальной Машины toodownload его файл удаленного рабочего стола tooyour рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-213">Wait for each VM toobe fully provisioned and for each VM toodownload its remote desktop file tooyour working directory.</span></span> <span data-ttu-id="a4a0a-214">Hello `for` цикла циклически hello трем новым виртуальным машинам и выполняет команды hello в фигурных скобках верхнего уровня hello для каждого из них.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-214">hello `for` loop cycles through hello three new VMs and executes hello commands inside hello top-level curly brackets for each of them.</span></span>

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until hello VM status is "ReadyRole"
            While ($VM.InstanceStatus -ne "ReadyRole")
            {
                write-host "  Current Status = " $VM.InstanceStatus
                Start-Sleep -Seconds 15
                $VM = Get-AzureVM -ServiceName $VM.ServiceName -Name $VM.InstanceName
            }

            write-host "  Current Status = " $VM.InstanceStatus

            # Download remote desktop file
            Get-AzureRemoteDesktopFile -ServiceName $VM.ServiceName -Name $VM.InstanceName -LocalPath "$workingDir$($VM.InstanceName).rdp"
        }

    <span data-ttu-id="a4a0a-215">виртуальные машины Hello SQL Server настроены и запущены, но они установлены с помощью SQL Server с параметрами по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-215">hello SQL Server VMs are now provisioned and running, but they're installed with SQL Server with default options.</span></span>

## <a name="initialize-hello-failover-cluster-vms"></a><span data-ttu-id="a4a0a-216">Инициализировать hello отказоустойчивого кластера виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="a4a0a-216">Initialize hello failover cluster VMs</span></span>
<span data-ttu-id="a4a0a-217">В этом разделе требуется три серверов hello toomodify, которые будут использоваться в отказоустойчивом кластере hello и hello установки SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-217">In this section, you need toomodify hello three servers that you'll use in hello failover cluster and hello SQL Server installation.</span></span> <span data-ttu-id="a4a0a-218">В частности:</span><span class="sxs-lookup"><span data-stu-id="a4a0a-218">Specifically:</span></span>

* <span data-ttu-id="a4a0a-219">Все серверы: требуется tooinstall hello **отказоустойчивой кластеризации** компонентов.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-219">All servers: You need tooinstall hello **Failover Clustering** feature.</span></span>
* <span data-ttu-id="a4a0a-220">Все серверы: требуется tooadd **CORP\Install** как hello машина **администратора**.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-220">All servers: You need tooadd **CORP\Install** as hello machine **administrator**.</span></span>
* <span data-ttu-id="a4a0a-221">Только ContosoSQL1 и ContosoSQL2: требуется tooadd **CORP\Install** как **sysadmin** роли в базе данных по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-221">ContosoSQL1 and ContosoSQL2 only: You need tooadd **CORP\Install** as a **sysadmin** role in hello default database.</span></span>
* <span data-ttu-id="a4a0a-222">Только ContosoSQL1 и ContosoSQL2: требуется tooadd **NT AUTHORITY\System** как вход с hello следующие разрешения:</span><span class="sxs-lookup"><span data-stu-id="a4a0a-222">ContosoSQL1 and ContosoSQL2 only: You need tooadd **NT AUTHORITY\System** as a sign-in with hello following permissions:</span></span>

  * <span data-ttu-id="a4a0a-223">Изменение любой группы доступности</span><span class="sxs-lookup"><span data-stu-id="a4a0a-223">Alter any availability group</span></span>
  * <span data-ttu-id="a4a0a-224">Соединение SQL</span><span class="sxs-lookup"><span data-stu-id="a4a0a-224">Connect SQL</span></span>
  * <span data-ttu-id="a4a0a-225">Просмотр состояния сервера</span><span class="sxs-lookup"><span data-stu-id="a4a0a-225">View server state</span></span>
* <span data-ttu-id="a4a0a-226">Только ContosoSQL1 и ContosoSQL2: hello **TCP** протокол уже включен на виртуальной Машине SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-226">ContosoSQL1 and ContosoSQL2 only: hello **TCP** protocol is already enabled on hello SQL Server VM.</span></span> <span data-ttu-id="a4a0a-227">Однако по-прежнему требуются tooopen hello брандмауэра для удаленного доступа к SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-227">However, you still need tooopen hello firewall for remote access of SQL Server.</span></span>

<span data-ttu-id="a4a0a-228">Теперь вы готовы toostart.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-228">Now, you're ready toostart.</span></span> <span data-ttu-id="a4a0a-229">Начиная с версии **ContosoQuorum**, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a4a0a-229">Beginning with **ContosoQuorum**, follow hello steps below:</span></span>

1. <span data-ttu-id="a4a0a-230">Подключение слишком**ContosoQuorum** путем запуска файлов удаленного рабочего стола hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-230">Connect too**ContosoQuorum** by launching hello remote desktop files.</span></span> <span data-ttu-id="a4a0a-231">Используйте имя пользователя администратора машины hello **AzureAdmin** и пароль **Contoso! 000**, указанные при создании виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-231">Use hello machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created hello VMs.</span></span>
2. <span data-ttu-id="a4a0a-232">Убедитесь, что компьютеры hello была успешно присоединена слишком**corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-232">Verify that hello computers have been successfully joined too**corp.contoso.com**.</span></span>
3. <span data-ttu-id="a4a0a-233">Дождитесь hello toofinish установки на SQL Server под управлением hello автоматизировать задачи инициализации, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-233">Wait for hello SQL Server installation toofinish running hello automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="a4a0a-234">Откройте окно PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-234">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="a4a0a-235">Установите компонент отказоустойчивой кластеризации Windows hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-235">Install hello Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="a4a0a-236">Добавьте **CORP\Install** в качестве локального администратора.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-236">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="a4a0a-237">Выйдите из ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-237">Sign out of ContosoQuorum.</span></span> <span data-ttu-id="a4a0a-238">Теперь работа с этим сервером завершена.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-238">You're done with this server now.</span></span>

        logoff.exe

<span data-ttu-id="a4a0a-239">Затем инициализируйте виртуальные машины **ContosoSQL1** и **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-239">Next, initialize **ContosoSQL1** and **ContosoSQL2**.</span></span> <span data-ttu-id="a4a0a-240">Выполните hello шаги, которые идентичны для обеих виртуальных машин SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-240">Follow hello steps below, which are identical for both SQL Server VMs.</span></span>

1. <span data-ttu-id="a4a0a-241">Подключитесь toohello двух виртуальных машин SQL Server, запустив файлы удаленного рабочего стола hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-241">Connect toohello two SQL Server VMs by launching hello remote desktop files.</span></span> <span data-ttu-id="a4a0a-242">Используйте имя пользователя администратора машины hello **AzureAdmin** и пароль **Contoso! 000**, указанные при создании виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-242">Use hello machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created hello VMs.</span></span>
2. <span data-ttu-id="a4a0a-243">Убедитесь, что компьютеры hello была успешно присоединена слишком**corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-243">Verify that hello computers have been successfully joined too**corp.contoso.com**.</span></span>
3. <span data-ttu-id="a4a0a-244">Дождитесь hello toofinish установки на SQL Server под управлением hello автоматизировать задачи инициализации, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-244">Wait for hello SQL Server installation toofinish running hello automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="a4a0a-245">Откройте окно PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-245">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="a4a0a-246">Установите компонент отказоустойчивой кластеризации Windows hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-246">Install hello Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="a4a0a-247">Добавьте **CORP\Install** в качестве локального администратора.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-247">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="a4a0a-248">Импортируйте поставщик SQL Server PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-248">Import hello SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. <span data-ttu-id="a4a0a-249">Добавить **CORP\Install** как hello роли sysadmin для экземпляра SQL Server по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-249">Add **CORP\Install** as hello sysadmin role for hello default SQL Server instance.</span></span>

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. <span data-ttu-id="a4a0a-250">Добавить **NT AUTHORITY\System** как вход с описанными выше разрешениями hello трех.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-250">Add **NT AUTHORITY\System** as a sign-in with hello three permissions described above.</span></span>

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. <span data-ttu-id="a4a0a-251">Откройте брандмауэр Windows hello для удаленного доступа к SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-251">Open hello firewall for remote access of SQL Server.</span></span>

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. <span data-ttu-id="a4a0a-252">Выйдите из обеих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-252">Sign out of both VMs.</span></span>

         logoff.exe

<span data-ttu-id="a4a0a-253">Наконец вы готовы tooconfigure группы доступности hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-253">Finally, you're ready tooconfigure hello availability group.</span></span> <span data-ttu-id="a4a0a-254">Вы воспользуетесь tooperform hello поставщик SQL Server PowerShell, работающие hello со **ContosoSQL1**.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-254">You'll use hello SQL Server PowerShell Provider tooperform all of hello work on **ContosoSQL1**.</span></span>

## <a name="configure-hello-availability-group"></a><span data-ttu-id="a4a0a-255">Настройка группы доступности hello</span><span class="sxs-lookup"><span data-stu-id="a4a0a-255">Configure hello availability group</span></span>
1. <span data-ttu-id="a4a0a-256">Подключение слишком**ContosoSQL1** еще раз путем запуска файлов удаленного рабочего стола hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-256">Connect too**ContosoSQL1** again by launching hello remote desktop files.</span></span> <span data-ttu-id="a4a0a-257">Вместо вход с помощью учетной записи компьютера hello, войдите в систему с **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-257">Instead of signing in by using hello machine account, sign in by using **CORP\Install**.</span></span>
2. <span data-ttu-id="a4a0a-258">Откройте окно PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-258">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="a4a0a-259">Определите следующие переменные hello:</span><span class="sxs-lookup"><span data-stu-id="a4a0a-259">Define hello following variables:</span></span>

        $server1 = "ContosoSQL1"
        $server2 = "ContosoSQL2"
        $serverQuorum = "ContosoQuorum"
        $acct1 = "CORP\SQLSvc1"
        $acct2 = "CORP\SQLSvc2"
        $password = "Contoso!000"
        $clusterName = "Cluster1"
        $timeout = New-Object System.TimeSpan -ArgumentList 0, 0, 30
        $db = "MyDB1"
        $backupShare = "\\$server1\backup"
        $quorumShare = "\\$server1\quorum"
        $ag = "AG1"
4. <span data-ttu-id="a4a0a-260">Импортируйте поставщик SQL Server PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-260">Import hello SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. <span data-ttu-id="a4a0a-261">Изменение учетной записи службы SQL Server hello для ContosoSQL1 tooCORP\SQLSvc1.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-261">Change hello SQL Server service account for ContosoSQL1 tooCORP\SQLSvc1.</span></span>

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. <span data-ttu-id="a4a0a-262">Изменение учетной записи службы SQL Server hello для ContosoSQL2 tooCORP\SQLSvc2.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-262">Change hello SQL Server service account for ContosoSQL2 tooCORP\SQLSvc2.</span></span>

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. <span data-ttu-id="a4a0a-263">Загрузить **CreateAzureFailoverCluster.ps1** из [Создание отказоустойчивого кластера для группы доступности AlwaysOn в виртуальной Машине Azure](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello локальный рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-263">Download **CreateAzureFailoverCluster.ps1** from [Create Failover Cluster for Always On Availability Groups in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello local working directory.</span></span> <span data-ttu-id="a4a0a-264">Вы будете использовать этот сценарий toohelp, Создание функциональной отказоустойчивого кластера.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-264">You'll use this script toohelp you create a functional failover cluster.</span></span> <span data-ttu-id="a4a0a-265">Важная информация по отказоустойчивой кластеризации Windows взаимодействие с hello Azure сети см. в разделе [высокий уровень доступности и аварийного восстановления SQL Server в виртуальных машинах Azure](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a4a0a-265">For important information on how Windows Failover Clustering interacts with hello Azure network, see [High availability and disaster recovery for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>
8. <span data-ttu-id="a4a0a-266">Изменить tooyour рабочий каталог и создайте hello отказоустойчивого кластера с помощью сценария загружаются hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-266">Change tooyour working directory and create hello failover cluster with hello downloaded script.</span></span>

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. <span data-ttu-id="a4a0a-267">Включение групп доступности AlwaysOn для экземпляров SQL Server по умолчанию hello **ContosoSQL1** и **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-267">Enable Always On availability groups for hello default SQL Server instances on **ContosoSQL1** and **ContosoSQL2**.</span></span>

        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server1\Default `
            -Force
        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server2\Default `
            -NoServiceRestart
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
10. <span data-ttu-id="a4a0a-268">Создать каталог резервных копий и предоставьте разрешения для учетных записей служб SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-268">Create a backup directory and grant permissions for hello SQL Server service accounts.</span></span> <span data-ttu-id="a4a0a-269">Вы используете tooprepare directory hello баз данных доступности на вторичной реплике hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-269">You'll use this directory tooprepare hello availability database on hello secondary replica.</span></span>

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. <span data-ttu-id="a4a0a-270">Создание базы данных на **ContosoSQL1** вызывается **MyDB1**, выполните полную резервную копию и резервную копию журнала и восстановить их на **ContosoSQL2** с hello **WITH Параметр NORECOVERY** параметр.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-270">Create a database on **ContosoSQL1** called **MyDB1**, take both a full backup and a log backup, and restore them on **ContosoSQL2** with hello **WITH NORECOVERY** option.</span></span>

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. <span data-ttu-id="a4a0a-271">Создайте конечные точки группы доступности hello на hello виртуальные машины SQL Server и задайте соответствующие разрешения hello в конечных точках hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-271">Create hello availability group endpoints on hello SQL Server VMs and set hello proper permissions on hello endpoints.</span></span>

         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server1\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"
         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server2\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"

         Invoke-SqlCmd -Query "CREATE LOGIN [$acct2] FROM WINDOWS" -ServerInstance $server1
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct1]" -ServerInstance $server2
13. <span data-ttu-id="a4a0a-272">Создание реплики доступности hello.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-272">Create hello availability replicas.</span></span>

         $primaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server1 `
             -EndpointURL "TCP://$server1.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
         $secondaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server2 `
             -EndpointURL "TCP://$server2.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
14. <span data-ttu-id="a4a0a-273">Наконец создайте группу доступности hello и группы доступности toohello вторичная реплика hello соединения.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-273">Finally, create hello availability group and join hello secondary replica toohello availability group.</span></span>

         New-SqlAvailabilityGroup `
             -Name $ag `
             -Path "SQLSERVER:\SQL\$server1\Default" `
             -AvailabilityReplica @($primaryReplica,$secondaryReplica) `
             -Database $db
         Join-SqlAvailabilityGroup `
             -Path "SQLSERVER:\SQL\$server2\Default" `
             -Name $ag
         Add-SqlAvailabilityDatabase `
             -Path "SQLSERVER:\SQL\$server2\Default\AvailabilityGroups\$ag" `
             -Database $db

## <a name="next-steps"></a><span data-ttu-id="a4a0a-274">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a4a0a-274">Next steps</span></span>
<span data-ttu-id="a4a0a-275">Решение SQL Server Always On на основе группы доступности в Azure успешно создано.</span><span class="sxs-lookup"><span data-stu-id="a4a0a-275">You've now successfully implemented SQL Server Always On by creating an availability group in Azure.</span></span> <span data-ttu-id="a4a0a-276">tooconfigure прослушивателя для этой группы доступности. в разделе [настроить прослушиватель ILB для групп доступности AlwaysOn в Azure](../classic/ps-sql-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="a4a0a-276">tooconfigure a listener for this availability group, see [Configure an ILB listener for Always On availability groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="a4a0a-277">Дополнительные сведения об использовании SQL Server в Azure см. в статье [Общие сведения об SQL Server на виртуальных машинах Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4a0a-277">For other information about using SQL Server in Azure, see [SQL Server on Azure virtual machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
