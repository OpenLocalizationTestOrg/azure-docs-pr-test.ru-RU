---
title: "Настройка группы доступности Always On на виртуальной машине Azure с помощью PowerShell | Документация Майкрософт"
description: "В этом руководстве используются ресурсы, которые были созданы с помощью классической модели развертывания. Здесь вы будете создавать группы доступности Always On в Azure с помощью PowerShell."
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
ms.openlocfilehash: b99cf767fb931d3f7fe14fcbe7990126244613ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-always-on-availability-group-on-an-azure-vm-with-powershell"></a><span data-ttu-id="ed6df-104">Настройка группы доступности Always On на виртуальной машине Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed6df-104">Configure the Always On availability group on an Azure VM with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ed6df-105">Классическая модель: пользовательский интерфейс</span><span class="sxs-lookup"><span data-stu-id="ed6df-105">Classic: UI</span></span>](../classic/portal-sql-alwayson-availability-groups.md)
> * <span data-ttu-id="ed6df-106">[Классическая модель: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span><span class="sxs-lookup"><span data-stu-id="ed6df-106">[Classic: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span></span><br/>

<span data-ttu-id="ed6df-107">Прежде чем начать, учтите, что теперь можно выполнить эту задачу в модели Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ed6df-107">Before you begin, consider that you can now complete this task in Azure resource manager model.</span></span> <span data-ttu-id="ed6df-108">Для новых развертываний мы советуем использовать модель Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ed6df-108">We recommend Azure resource manager model for new deployments.</span></span> <span data-ttu-id="ed6df-109">См. сведения в статье [Введение в группы доступности Always On SQL Server на виртуальных машинах Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ed6df-109">See [SQL Server Always On availability groups on Azure virtual machines](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ed6df-110">Для большинства новых развертываний рекомендуется использовать модель Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ed6df-110">We recommend that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="ed6df-111">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ed6df-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ed6df-112">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="ed6df-112">This article covers using the classic deployment model.</span></span>

<span data-ttu-id="ed6df-113">Виртуальные машины Azure могут помочь администраторам баз данных сократить затраты при реализации более высокого уровня доступности системы SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed6df-113">Azure virtual machines (VMs) can help database administrators to lower the cost of a high-availability SQL Server system.</span></span> <span data-ttu-id="ed6df-114">В этом руководстве описано, как реализовать группу доступности с помощью сквозного соединения SQL Server Always On в среде Azure.</span><span class="sxs-lookup"><span data-stu-id="ed6df-114">This tutorial shows you how to implement an availability group by using SQL Server Always On end-to-end inside an Azure environment.</span></span> <span data-ttu-id="ed6df-115">Когда вы завершите, решение SQL Server Always On в Azure будет состоять из следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ed6df-115">At the end of the tutorial, your SQL Server Always On solution in Azure will consist of the following elements:</span></span>

* <span data-ttu-id="ed6df-116">Виртуальной сети, которая содержит множество подсетей, в том числе внешнюю и внутреннюю подсети;</span><span class="sxs-lookup"><span data-stu-id="ed6df-116">A virtual network that contains multiple subnets, including a front-end and a back-end subnet.</span></span>
* <span data-ttu-id="ed6df-117">контроллера домена с доменом Active Directory;</span><span class="sxs-lookup"><span data-stu-id="ed6df-117">A domain controller with an Active Directory domain.</span></span>
* <span data-ttu-id="ed6df-118">двух виртуальных машин SQL Server, развернутых во внутреннюю подсеть и присоединенных к домену Active Directory;</span><span class="sxs-lookup"><span data-stu-id="ed6df-118">Two SQL Server VMs that are deployed to the back-end subnet and joined to the Active Directory domain.</span></span>
* <span data-ttu-id="ed6df-119">отказоустойчивого кластера Windows из трех узлов с моделью кворума "Большинство узлов";</span><span class="sxs-lookup"><span data-stu-id="ed6df-119">A three-node Windows failover cluster with the Node Majority quorum model.</span></span>
* <span data-ttu-id="ed6df-120">группы доступности с двумя репликами с синхронной фиксацией базы данных доступности.</span><span class="sxs-lookup"><span data-stu-id="ed6df-120">An availability group with two synchronous-commit replicas of an availability database.</span></span>

<span data-ttu-id="ed6df-121">Этот сценарий — хороший выбор из-за его простоты на Azure, а не из-за его экономичности или других факторов.</span><span class="sxs-lookup"><span data-stu-id="ed6df-121">This scenario is a good choice for its simplicity on Azure, not for its cost-effectiveness or other factors.</span></span> <span data-ttu-id="ed6df-122">Например, можно сократить число виртуальных машин для группы доступности с двумя репликами, чтобы сократить часы вычислительных операций в Azure, используя контроллер домена как следящую общую папку кворума в отказоустойчивом кластере из двух узлов.</span><span class="sxs-lookup"><span data-stu-id="ed6df-122">For example, you can minimize the number of VMs for a two-replica availability group to save on compute hours in Azure by using the domain controller as the quorum file share witness in a two-node failover cluster.</span></span> <span data-ttu-id="ed6df-123">Этот метод сократит число виртуальных машин на одну по сравнению с указанной выше конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="ed6df-123">This method reduces the VM count by one from the above configuration.</span></span>

<span data-ttu-id="ed6df-124">В данном руководстве показаны шаги, необходимые для настройки описанного решения. Подробные сведения каждого этапа не приводятся.</span><span class="sxs-lookup"><span data-stu-id="ed6df-124">This tutorial is intended to show you the steps that are required to set up the described solution above, without elaborating on the details of each step.</span></span> <span data-ttu-id="ed6df-125">Вместо предоставления элементов графического пользовательского интерфейса на каждом этапе в руководстве используются скрипты PowerShell для быстрого ознакомления с этапами.</span><span class="sxs-lookup"><span data-stu-id="ed6df-125">Therefore, instead of providing the GUI configuration steps, it uses PowerShell scripting to take you quickly through each step.</span></span> <span data-ttu-id="ed6df-126">В этом учебнике предполагается следующее:</span><span class="sxs-lookup"><span data-stu-id="ed6df-126">This tutorial assumes the following:</span></span>

* <span data-ttu-id="ed6df-127">Вы уже имеете учетную запись Azure с подпиской для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="ed6df-127">You already have an Azure account with the virtual machine subscription.</span></span>
* <span data-ttu-id="ed6df-128">В системе установлены [командлеты Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ed6df-128">You've installed the [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>
* <span data-ttu-id="ed6df-129">Вы хорошо понимаете принцип работы групп доступности Always On в локальных решениях.</span><span class="sxs-lookup"><span data-stu-id="ed6df-129">You already have a solid understanding of Always On availability groups for on-premises solutions.</span></span> <span data-ttu-id="ed6df-130">Дополнительные сведения см. в разделе [Группы доступности AlwaysOn (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed6df-130">For more information, see [Always On availability groups (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span></span>

## <a name="connect-to-your-azure-subscription-and-create-the-virtual-network"></a><span data-ttu-id="ed6df-131">Подключение к подписке Azure и создание виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="ed6df-131">Connect to your Azure subscription and create the virtual network</span></span>
1. <span data-ttu-id="ed6df-132">В окне Powershell на локальном компьютере импортируйте модуль Azure, скачайте файл параметров публикации на компьютер и подключите сеанс PowerShell к подписке Azure путем импорта скачанных параметров публикации.</span><span class="sxs-lookup"><span data-stu-id="ed6df-132">In a PowerShell window on your local computer, import the Azure module, download the publishing settings file to your machine, and connect your PowerShell session to your Azure subscription by importing the downloaded publishing settings.</span></span>

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    <span data-ttu-id="ed6df-133">Команда **Get AzurePublishgSettingsFile** автоматически создает сертификат управления, а Azure скачивает его на компьютер.</span><span class="sxs-lookup"><span data-stu-id="ed6df-133">The **Get-AzurePublishSettingsFile** command automatically generates a management certificate with Azure and downloads it to your machine.</span></span> <span data-ttu-id="ed6df-134">Автоматически откроется браузер, где потребуется ввести данные учетной записи Майкрософт для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="ed6df-134">A browser is automatically opened, and you're prompted to enter the Microsoft account credentials for your Azure subscription.</span></span> <span data-ttu-id="ed6df-135">Скачанный **PUBLISHSETTINGS**-файл содержит всю информацию, необходимую для управления подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="ed6df-135">The downloaded **.publishsettings** file contains all the information that you need to manage your Azure subscription.</span></span> <span data-ttu-id="ed6df-136">После сохранения этого файла в локальный каталог импортируйте его с помощью команды **Import-AzurePublishSettingsFile**.</span><span class="sxs-lookup"><span data-stu-id="ed6df-136">After saving this file to a local directory, import it by using the **Import-AzurePublishSettingsFile** command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ed6df-137">PUBLISHSETTINGS-файл содержит учетные данные (незакодированные), используемые для администрирования подписок и служб Azure.</span><span class="sxs-lookup"><span data-stu-id="ed6df-137">The .publishsettings file contains your credentials (unencoded) that are used to administer your Azure subscriptions and services.</span></span> <span data-ttu-id="ed6df-138">В целях безопасности этот файл рекомендуется временно хранить за пределами исходных каталогов (например, в папке Libraries\Documents), а затем удалить его после выполнения импорта.</span><span class="sxs-lookup"><span data-stu-id="ed6df-138">The security best practice for this file is to store it temporarily outside your source directories (for example, in the Libraries\Documents folder), and then delete it after the import has finished.</span></span> <span data-ttu-id="ed6df-139">Злоумышленник, получивший доступ к PUBLISHSETTINGS-файлу, сможет изменять, создавать и удалять ваши службы Azure.</span><span class="sxs-lookup"><span data-stu-id="ed6df-139">A malicious user who gains access to the .publishsettings file can edit, create, and delete your Azure services.</span></span>

2. <span data-ttu-id="ed6df-140">Определите ряд переменных, которые будут использоваться для создания облачной ИТ-инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="ed6df-140">Define a series of variables that you'll use to create your cloud IT infrastructure.</span></span>

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

    <span data-ttu-id="ed6df-141">Чтобы обеспечить дальнейшее успешное выполнение команд, обратите внимание на следующее:</span><span class="sxs-lookup"><span data-stu-id="ed6df-141">Pay attention to the following to ensure that your commands will succeed later:</span></span>

   * <span data-ttu-id="ed6df-142">Переменные **$storageAccountName** и **$dcServiceName** должны быть уникальными, так как они используются для идентификации в Интернете соответственно облачной учетной записи хранения и облачного сервера.</span><span class="sxs-lookup"><span data-stu-id="ed6df-142">Variables **$storageAccountName** and **$dcServiceName** must be unique because they're used to identify your cloud storage account and cloud server, respectively, on the Internet.</span></span>
   * <span data-ttu-id="ed6df-143">Имена переменных **$affinityGroupName** и **$virtualNetworkName** задаются в документе конфигурации виртуальной сети, который будет использован позднее.</span><span class="sxs-lookup"><span data-stu-id="ed6df-143">The names that you specify for variables **$affinityGroupName** and **$virtualNetworkName** are configured in the virtual network configuration document that you'll use later.</span></span>
   * <span data-ttu-id="ed6df-144">**$sqlImageName** указывает обновленное имя образа виртуальной машины, который содержит SQL Server 2012 Enterprise Edition с пакетом обновления 1 (SP1).</span><span class="sxs-lookup"><span data-stu-id="ed6df-144">**$sqlImageName** specifies the updated name of the VM image that contains SQL Server 2012 Service Pack 1 Enterprise Edition.</span></span>
   * <span data-ttu-id="ed6df-145">Для простоты во всем руководстве используется единственный пароль — **Contoso!000**.</span><span class="sxs-lookup"><span data-stu-id="ed6df-145">For simplicity, **Contoso!000** is the same password that's used throughout the entire tutorial.</span></span>

3. <span data-ttu-id="ed6df-146">Создайте территориальную группу</span><span class="sxs-lookup"><span data-stu-id="ed6df-146">Create an affinity group.</span></span>

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. <span data-ttu-id="ed6df-147">Создайте виртуальную сеть, импортировав файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ed6df-147">Create a virtual network by importing a configuration file.</span></span>

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    <span data-ttu-id="ed6df-148">Файл конфигурации содержит следующий XML-документ.</span><span class="sxs-lookup"><span data-stu-id="ed6df-148">The configuration file contains the following XML document.</span></span> <span data-ttu-id="ed6df-149">Вкратце, он определяет виртуальную сеть под названием **ContosoNET** в территориальной группе, которая называется **ContosoAG**.</span><span class="sxs-lookup"><span data-stu-id="ed6df-149">In brief, it specifies a virtual network called **ContosoNET** in the affinity group called **ContosoAG**.</span></span> <span data-ttu-id="ed6df-150">Она имеет адресное пространство **10.10.0.0/16** и две подсети **10.10.1.0/24** и **10.10.2.0/24**, которые являются интерфейсной и конечной подсетями соответственно.</span><span class="sxs-lookup"><span data-stu-id="ed6df-150">It has the address space **10.10.0.0/16** and has two subnets, **10.10.1.0/24** and **10.10.2.0/24**, which are the front subnet and back subnet, respectively.</span></span> <span data-ttu-id="ed6df-151">В интерфейсной подсети можно разместить клиентские приложения, например Microsoft SharePoint,</span><span class="sxs-lookup"><span data-stu-id="ed6df-151">The front subnet is where you can place client applications such as Microsoft SharePoint.</span></span> <span data-ttu-id="ed6df-152">а в конечной подсети размещаются виртуальные машины SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed6df-152">The back subnet is where you'll place the SQL Server VMs.</span></span> <span data-ttu-id="ed6df-153">Если переменные **$affinityGroupName** и **$virtualNetworkName** были изменены, следует изменить и соответствующие имена, приведенные ниже.</span><span class="sxs-lookup"><span data-stu-id="ed6df-153">If you change the **$affinityGroupName** and **$virtualNetworkName** variables earlier, you must also change the corresponding names below.</span></span>

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

5. <span data-ttu-id="ed6df-154">Создайте учетную запись хранения, связанную с созданной территориальной группой, а затем установите ее в качестве текущей учетной записи хранения в своей подписке.</span><span class="sxs-lookup"><span data-stu-id="ed6df-154">Create a storage account that's associated with the affinity group that you created, and set it as the current storage account in your subscription.</span></span>

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. <span data-ttu-id="ed6df-155">Создайте сервер контроллера домена в новой облачной службе и группе доступности.</span><span class="sxs-lookup"><span data-stu-id="ed6df-155">Create the domain controller server in the new cloud service and availability set.</span></span>

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

    <span data-ttu-id="ed6df-156">Эти переданные команды выполняют следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="ed6df-156">These piped commands do the following things:</span></span>

   * <span data-ttu-id="ed6df-157">**New-AzureVMConfig** создает конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ed6df-157">**New-AzureVMConfig** creates a VM configuration.</span></span>
   * <span data-ttu-id="ed6df-158">**Add-AzureProvisioningConfig** задает параметры конфигурации отдельного сервера Windows.</span><span class="sxs-lookup"><span data-stu-id="ed6df-158">**Add-AzureProvisioningConfig** gives the configuration parameters of a standalone Windows server.</span></span>
   * <span data-ttu-id="ed6df-159">**Add-AzureDataDisk** добавляет диск данных, который используется для хранения данных Active Directory, при этом параметр кэширования задан как None.</span><span class="sxs-lookup"><span data-stu-id="ed6df-159">**Add-AzureDataDisk** adds the data disk that you'll use for storing Active Directory data, with the caching option set to None.</span></span>
   * <span data-ttu-id="ed6df-160">**New-AzureVM** создает новую облачную службу и новую виртуальную машину Azure в новой облачной службе.</span><span class="sxs-lookup"><span data-stu-id="ed6df-160">**New-AzureVM** creates a new cloud service and creates the new Azure VM in the new cloud service.</span></span>

7. <span data-ttu-id="ed6df-161">Дождитесь полной подготовки к работе новой виртуальной машины и скачайте файл удаленного рабочего стола в рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="ed6df-161">Wait for the new VM to be fully provisioned, and download the remote desktop file to your working directory.</span></span> <span data-ttu-id="ed6df-162">Так как подготовка виртуальной машины Azure к работе занимает длительное время, цикл `while` продолжает опрашивать новую виртуальную машину до тех пор, пока она не станет готова к использованию.</span><span class="sxs-lookup"><span data-stu-id="ed6df-162">Because the new Azure VM takes a long time to provision, the `while` loop continues to poll the new VM until it's ready for use.</span></span>

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

<span data-ttu-id="ed6df-163">Сервер контроллера домена успешно подготовлен.</span><span class="sxs-lookup"><span data-stu-id="ed6df-163">The domain controller server is now successfully provisioned.</span></span> <span data-ttu-id="ed6df-164">Далее нужно настроить домен Active Directory на этом сервере контроллера домена.</span><span class="sxs-lookup"><span data-stu-id="ed6df-164">Next, you'll configure the Active Directory domain on this domain controller server.</span></span> <span data-ttu-id="ed6df-165">Не закрывайте окно PowerShell на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="ed6df-165">Leave the PowerShell window open on your local computer.</span></span> <span data-ttu-id="ed6df-166">Оно пригодится вам позже во время создания двух виртуальных машин SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed6df-166">You'll use it again later to create the two SQL Server VMs.</span></span>

## <a name="configure-the-domain-controller"></a><span data-ttu-id="ed6df-167">Настройка контроллера домена</span><span class="sxs-lookup"><span data-stu-id="ed6df-167">Configure the domain controller</span></span>
1. <span data-ttu-id="ed6df-168">Подключитесь к серверу контроллера домена, запустив файл удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="ed6df-168">Connect to the domain controller server by launching the remote desktop file.</span></span> <span data-ttu-id="ed6df-169">Используйте имя администратора компьютера AzureAdmin и пароль **Contoso!000**, которые вы указали при создании новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ed6df-169">Use the machine administrator’s username AzureAdmin and password **Contoso!000**, which you specified when you created the new VM.</span></span>
2. <span data-ttu-id="ed6df-170">Откройте окно PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="ed6df-170">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="ed6df-171">Выполните следующую команду **DCPROMO.EXE**, чтобы настроить домен **corp.contoso.com** с каталогами данных на диске M.</span><span class="sxs-lookup"><span data-stu-id="ed6df-171">Run the following **DCPROMO.EXE** command to set up the **corp.contoso.com** domain, with the data directories on drive M.</span></span>

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

    <span data-ttu-id="ed6df-172">После завершения команды виртуальная машина автоматически перезагружается.</span><span class="sxs-lookup"><span data-stu-id="ed6df-172">After the command finishes, the VM restarts automatically.</span></span>

4. <span data-ttu-id="ed6df-173">Подключитесь к серверу контроллера домена еще раз, запустив файл удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="ed6df-173">Connect to the domain controller server again by launching the remote desktop file.</span></span> <span data-ttu-id="ed6df-174">На этот раз войдите с именем **CORP\Administrator**.</span><span class="sxs-lookup"><span data-stu-id="ed6df-174">This time, sign in as **CORP\Administrator**.</span></span>
5. <span data-ttu-id="ed6df-175">Откройте окно Powershell в режиме администратора и импортируйте модуль Active Directory PowerShell с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="ed6df-175">Open a PowerShell window in administrator mode, and import the Active Directory PowerShell module by using the following command:</span></span>

        Import-Module ActiveDirectory

6. <span data-ttu-id="ed6df-176">Выполните следующие команды, чтобы добавить трех пользователей в домен.</span><span class="sxs-lookup"><span data-stu-id="ed6df-176">Run the following commands to add three users to the domain.</span></span>

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

    <span data-ttu-id="ed6df-177">**CORP\Install** служит для настройки всего, что связано с экземплярами службы SQL Server, отказоустойчивым кластером и группой доступности.</span><span class="sxs-lookup"><span data-stu-id="ed6df-177">**CORP\Install** is used to configure everything related to the SQL Server service instances, the failover cluster, and the availability group.</span></span> <span data-ttu-id="ed6df-178">**CORP\SQLSvc1** и **CORP\SQLSvc2** используются в качестве учетных записей службы SQL Server для двух виртуальных машин SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed6df-178">**CORP\SQLSvc1** and **CORP\SQLSvc2** are used as the SQL Server service accounts for the two SQL Server VMs.</span></span>
7. <span data-ttu-id="ed6df-179">Затем выполните следующие команды, чтобы предоставить учетной записи **CORP\Install** разрешения для создания объектов компьютеров в домене.</span><span class="sxs-lookup"><span data-stu-id="ed6df-179">Next, run the following commands to give **CORP\Install** the permissions to create computer objects in the domain.</span></span>

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    <span data-ttu-id="ed6df-180">Идентификатор GUID, указанный выше,— это GUID для типа объекта-компьютера.</span><span class="sxs-lookup"><span data-stu-id="ed6df-180">The GUID specified above is the GUID for the computer object type.</span></span> <span data-ttu-id="ed6df-181">Для учетной записи **CORP\Install** требуются разрешения **Чтение всех свойств** и **Создание объектов компьютеров**. Они необходимы для создания объектов Active Directory для отказоустойчивого кластера.</span><span class="sxs-lookup"><span data-stu-id="ed6df-181">The **CORP\Install** account needs the **Read All Properties** and **Create Computer Objects** permission to create the Active Direct objects for the failover cluster.</span></span> <span data-ttu-id="ed6df-182">Разрешение **Чтение всех свойств** предоставлено учетной записи CORP\Install по умолчанию, поэтому предоставлять его явным образом не требуется.</span><span class="sxs-lookup"><span data-stu-id="ed6df-182">The **Read All Properties** permission is already given to CORP\Install by default, so you don't need to grant it explicitly.</span></span> <span data-ttu-id="ed6df-183">Дополнительные сведения о разрешениях, необходимых для создания отказоустойчивого кластера, см. в статье [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx) (Пошаговое руководство по отказоустойчивым кластерам. Настройка учетных записей в Active Directory).</span><span class="sxs-lookup"><span data-stu-id="ed6df-183">For more information on permissions that are needed to create the failover cluster, see [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span></span>

    <span data-ttu-id="ed6df-184">После завершения настройки Active Directory и объектов пользователей нужно создать две виртуальные машины SQL Server и присоединить их к этому домену.</span><span class="sxs-lookup"><span data-stu-id="ed6df-184">Now that you've finished configuring Active Directory and the user objects, you'll create two SQL Server VMs and join them to this domain.</span></span>

## <a name="create-the-sql-server-vms"></a><span data-ttu-id="ed6df-185">Создание виртуальных машин SQL Server</span><span class="sxs-lookup"><span data-stu-id="ed6df-185">Create the SQL Server VMs</span></span>
1. <span data-ttu-id="ed6df-186">Перейдите в окно PowerShell, открытое на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="ed6df-186">Continue to use the PowerShell window that's open on your local computer.</span></span> <span data-ttu-id="ed6df-187">Определите следующие дополнительные переменные:</span><span class="sxs-lookup"><span data-stu-id="ed6df-187">Define the following additional variables:</span></span>

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

    <span data-ttu-id="ed6df-188">IP-адрес **10.10.0.4** обычно назначается первой виртуальной машине, созданной в подсети **10.10.0.0/16** вашей виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="ed6df-188">The IP address **10.10.0.4** is typically assigned to the first VM that you create in the **10.10.0.0/16** subnet of your Azure virtual network.</span></span> <span data-ttu-id="ed6df-189">Необходимо убедиться, что это адрес сервера контроллера домена. Для этого выполните команду **IPCONFIG**.</span><span class="sxs-lookup"><span data-stu-id="ed6df-189">You should verify that this is the address of your domain controller server by running **IPCONFIG**.</span></span>
2. <span data-ttu-id="ed6df-190">Выполните следующий набор команд, чтобы создать в отказоустойчивом кластере первую виртуальную машину с именем **ContosoQuorum**:</span><span class="sxs-lookup"><span data-stu-id="ed6df-190">Run the following piped commands to create the first VM in the failover cluster, named **ContosoQuorum**:</span></span>

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

    <span data-ttu-id="ed6df-191">Обратите внимание на следующее относительно указанной выше команды:</span><span class="sxs-lookup"><span data-stu-id="ed6df-191">Note the following regarding the command above:</span></span>

   * <span data-ttu-id="ed6df-192">**New-AzureVMConfig** создает конфигурацию виртуальной машины с заданным именем группы доступности.</span><span class="sxs-lookup"><span data-stu-id="ed6df-192">**New-AzureVMConfig** creates a VM configuration with the desired availability set name.</span></span> <span data-ttu-id="ed6df-193">Последующие виртуальные машины будут созданы с тем же именем группы доступности, поэтому они присоединяются к той же группе доступности.</span><span class="sxs-lookup"><span data-stu-id="ed6df-193">The subsequent VMs will be created with the same availability set name so that they're joined to the same availability set.</span></span>
   * <span data-ttu-id="ed6df-194">**Add-AzureProvisioningConfig** объединяет виртуальную машину с созданным доменом Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ed6df-194">**Add-AzureProvisioningConfig** joins the VM to the Active Directory domain that you created.</span></span>
   * <span data-ttu-id="ed6df-195">**Set-AzureSubnet** размещает виртуальную машину в конечной подсети.</span><span class="sxs-lookup"><span data-stu-id="ed6df-195">**Set-AzureSubnet** places the VM in the back subnet.</span></span>
   * <span data-ttu-id="ed6df-196">**New-AzureVM** создает новую облачную службу и новую виртуальную машину Azure в новой облачной службе.</span><span class="sxs-lookup"><span data-stu-id="ed6df-196">**New-AzureVM** creates a new cloud service and creates the new Azure VM in the new cloud service.</span></span> <span data-ttu-id="ed6df-197">Параметр **DnsSettings** указывает, что для сервера DNS, который используется для серверов в новой облачной службе, задан IP-адрес **10.10.0.4**.</span><span class="sxs-lookup"><span data-stu-id="ed6df-197">The **DnsSettings** parameter specifies that the DNS server for the servers in the new cloud service has the IP address **10.10.0.4**.</span></span> <span data-ttu-id="ed6df-198">Это IP-адрес сервера контроллера домена.</span><span class="sxs-lookup"><span data-stu-id="ed6df-198">This is the IP address of the domain controller server.</span></span> <span data-ttu-id="ed6df-199">Этот параметр необходим для активации новых виртуальных машин в облачной службе для успешного присоединения к домену Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ed6df-199">This parameter is needed to enable the new VMs in the cloud service to join to the Active Directory domain successfully.</span></span> <span data-ttu-id="ed6df-200">Без этого параметра вам потребуется вручную настроить параметры IPv4 на виртуальной машине для использования сервера контроллера домена в качестве основного DNS-сервера после подготовки виртуальной машины и ее присоединения к домену Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ed6df-200">Without this parameter, you must manually set the IPv4 settings in your VM to use the domain controller server as the primary DNS server after the VM is provisioned, and then join the VM to the Active Directory domain.</span></span>
3. <span data-ttu-id="ed6df-201">Выполните следующий набор команд, чтобы создать виртуальные машины SQL Server с именами **ContosoSQL1** и **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="ed6df-201">Run the following piped commands to create the SQL Server VMs, named **ContosoSQL1** and **ContosoSQL2**.</span></span>

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

    <span data-ttu-id="ed6df-202">Обратите внимание на следующее относительно указанных выше команд:</span><span class="sxs-lookup"><span data-stu-id="ed6df-202">Note the following regarding the commands above:</span></span>

   * <span data-ttu-id="ed6df-203">**New-AzureVMConfig** использует то же имя группы доступности, что и сервер контроллера домена, и использует образ SQL Server 2012 Enterprise Edition с пакетом обновления 1 (SP1) из коллекции виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="ed6df-203">**New-AzureVMConfig** uses the same availability set name as the domain controller server, and uses the SQL Server 2012 Service Pack 1 Enterprise Edition image in the virtual machine gallery.</span></span> <span data-ttu-id="ed6df-204">Кроме того, этот набор команд задает режим диска операционной системы на чтение кэша (запрет записи в кэш).</span><span class="sxs-lookup"><span data-stu-id="ed6df-204">It also sets the operating system disk to read-caching only (no write caching).</span></span> <span data-ttu-id="ed6df-205">Мы советуем переносить файлы баз данных на отдельный диск данных, подсоединенный к виртуальной машине, и настроить для него запрет на чтение кэша или запись в кэш.</span><span class="sxs-lookup"><span data-stu-id="ed6df-205">We recommend that you migrate the database files to a separate data disk that you attach to the VM, and configure it with no read or write caching.</span></span> <span data-ttu-id="ed6df-206">Однако наилучшая альтернатива — удалить кэширование записи на диске операционной системы, так как кэширование чтения с этого диска удалить нельзя.</span><span class="sxs-lookup"><span data-stu-id="ed6df-206">However, the next best thing is to remove write caching on the operating system disk because you can't remove read caching on the operating system disk.</span></span>
   * <span data-ttu-id="ed6df-207">**Add-AzureProvisioningConfig** объединяет виртуальную машину с созданным доменом Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ed6df-207">**Add-AzureProvisioningConfig** joins the VM to the Active Directory domain that you created.</span></span>
   * <span data-ttu-id="ed6df-208">**Set-AzureSubnet** размещает виртуальную машину в конечной подсети.</span><span class="sxs-lookup"><span data-stu-id="ed6df-208">**Set-AzureSubnet** places the VM in the back subnet.</span></span>
   * <span data-ttu-id="ed6df-209">**Add-AzureEndpoint** добавляет конечные точки доступа, чтобы клиентские приложения могли обращаться к экземплярам службы SQL Server через Интернет.</span><span class="sxs-lookup"><span data-stu-id="ed6df-209">**Add-AzureEndpoint** adds access endpoints so that client applications can access these SQL Server services instances on the Internet.</span></span> <span data-ttu-id="ed6df-210">Виртуальным машинам ContosoSQL1 и ContosoSQL2 назначаются различные порты.</span><span class="sxs-lookup"><span data-stu-id="ed6df-210">Different ports are given to ContosoSQL1 and ContosoSQL2.</span></span>
   * <span data-ttu-id="ed6df-211">**New-AzureVM** создает новую виртуальную машину SQL Server в той же облачной службе, что и ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="ed6df-211">**New-AzureVM** creates the new SQL Server VM in the same cloud service as ContosoQuorum.</span></span> <span data-ttu-id="ed6df-212">Если виртуальные машины должны находиться в одной группе доступности, то необходимо размещать их в одной облачной службе.</span><span class="sxs-lookup"><span data-stu-id="ed6df-212">You must place the VMs in the same cloud service if you want them to be in the same availability set.</span></span>
4. <span data-ttu-id="ed6df-213">Дождитесь полной подготовки к работе каждой виртуальной машины и скачайте для каждой виртуальной машины файл удаленного рабочего стола в рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="ed6df-213">Wait for each VM to be fully provisioned and for each VM to download its remote desktop file to your working directory.</span></span> <span data-ttu-id="ed6df-214">Цикл `for` проходит по трем новым виртуальным машинам и выполняет для каждой из них команды в фигурных скобках верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="ed6df-214">The `for` loop cycles through the three new VMs and executes the commands inside the top-level curly brackets for each of them.</span></span>

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until the VM status is "ReadyRole"
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

    <span data-ttu-id="ed6df-215">Виртуальные машины SQL Server подготовлены и запущены, но они устанавливаются с SQL Server с использованием параметров по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ed6df-215">The SQL Server VMs are now provisioned and running, but they're installed with SQL Server with default options.</span></span>

## <a name="initialize-the-failover-cluster-vms"></a><span data-ttu-id="ed6df-216">Инициализация виртуальных машин отказоустойчивого кластера</span><span class="sxs-lookup"><span data-stu-id="ed6df-216">Initialize the failover cluster VMs</span></span>
<span data-ttu-id="ed6df-217">В этом разделе вам необходимо изменить три сервера, которые будут использоваться в отказоустойчивом кластере и при установке SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed6df-217">In this section, you need to modify the three servers that you'll use in the failover cluster and the SQL Server installation.</span></span> <span data-ttu-id="ed6df-218">В частности:</span><span class="sxs-lookup"><span data-stu-id="ed6df-218">Specifically:</span></span>

* <span data-ttu-id="ed6df-219">Все серверы. Необходимо установить компонент **отказоустойчивой кластеризации**.</span><span class="sxs-lookup"><span data-stu-id="ed6df-219">All servers: You need to install the **Failover Clustering** feature.</span></span>
* <span data-ttu-id="ed6df-220">Все серверы. Необходимо добавить учетную запись **CORP\Install** в качестве **администратора** виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ed6df-220">All servers: You need to add **CORP\Install** as the machine **administrator**.</span></span>
* <span data-ttu-id="ed6df-221">Только ContosoSQL1 и ContosoSQL2. Необходимо добавить учетную запись **CORP\Install** в качестве роли **sysadmin** в базе данных по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ed6df-221">ContosoSQL1 and ContosoSQL2 only: You need to add **CORP\Install** as a **sysadmin** role in the default database.</span></span>
* <span data-ttu-id="ed6df-222">Только ContosoSQL1 и ContosoSQL2. Необходимо добавить учетную запись **NT AUTHORITY\System** в качестве имени входа со следующими разрешениями:</span><span class="sxs-lookup"><span data-stu-id="ed6df-222">ContosoSQL1 and ContosoSQL2 only: You need to add **NT AUTHORITY\System** as a sign-in with the following permissions:</span></span>

  * <span data-ttu-id="ed6df-223">Изменение любой группы доступности</span><span class="sxs-lookup"><span data-stu-id="ed6df-223">Alter any availability group</span></span>
  * <span data-ttu-id="ed6df-224">Соединение SQL</span><span class="sxs-lookup"><span data-stu-id="ed6df-224">Connect SQL</span></span>
  * <span data-ttu-id="ed6df-225">Просмотр состояния сервера</span><span class="sxs-lookup"><span data-stu-id="ed6df-225">View server state</span></span>
* <span data-ttu-id="ed6df-226">Только ContosoSQL1 и ContosoSQL2. Протокол **TCP** уже включен на виртуальной машине SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed6df-226">ContosoSQL1 and ContosoSQL2 only: The **TCP** protocol is already enabled on the SQL Server VM.</span></span> <span data-ttu-id="ed6df-227">Однако все еще требуется открыть брандмауэр для удаленного доступа к SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed6df-227">However, you still need to open the firewall for remote access of SQL Server.</span></span>

<span data-ttu-id="ed6df-228">Теперь все готово к запуску.</span><span class="sxs-lookup"><span data-stu-id="ed6df-228">Now, you're ready to start.</span></span> <span data-ttu-id="ed6df-229">Выполните следующие шаги, начиная с **ContosoQuorum**.</span><span class="sxs-lookup"><span data-stu-id="ed6df-229">Beginning with **ContosoQuorum**, follow the steps below:</span></span>

1. <span data-ttu-id="ed6df-230">Подключитесь к **ContosoQuorum** , запустив файлы удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="ed6df-230">Connect to **ContosoQuorum** by launching the remote desktop files.</span></span> <span data-ttu-id="ed6df-231">Используйте имя администратора компьютера **AzureAdmin** и пароль **Contoso!000**, которые вы указали при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ed6df-231">Use the machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created the VMs.</span></span>
2. <span data-ttu-id="ed6df-232">Убедитесь, что компьютеры успешно добавлены в домен **corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="ed6df-232">Verify that the computers have been successfully joined to **corp.contoso.com**.</span></span>
3. <span data-ttu-id="ed6df-233">Дождитесь, пока программа установки SQL Server не завершит автоматические задачи инициализации, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="ed6df-233">Wait for the SQL Server installation to finish running the automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="ed6df-234">Откройте окно PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="ed6df-234">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="ed6df-235">Установите компонент отказоустойчивой кластеризации Windows.</span><span class="sxs-lookup"><span data-stu-id="ed6df-235">Install the Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="ed6df-236">Добавьте **CORP\Install** в качестве локального администратора.</span><span class="sxs-lookup"><span data-stu-id="ed6df-236">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="ed6df-237">Выйдите из ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="ed6df-237">Sign out of ContosoQuorum.</span></span> <span data-ttu-id="ed6df-238">Теперь работа с этим сервером завершена.</span><span class="sxs-lookup"><span data-stu-id="ed6df-238">You're done with this server now.</span></span>

        logoff.exe

<span data-ttu-id="ed6df-239">Затем инициализируйте виртуальные машины **ContosoSQL1** и **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="ed6df-239">Next, initialize **ContosoSQL1** and **ContosoSQL2**.</span></span> <span data-ttu-id="ed6df-240">Выполните следующие шаги, которые идентичны для обеих виртуальных машин SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed6df-240">Follow the steps below, which are identical for both SQL Server VMs.</span></span>

1. <span data-ttu-id="ed6df-241">Подключитесь к двум виртуальным машинам SQL Server, запустив файлы удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="ed6df-241">Connect to the two SQL Server VMs by launching the remote desktop files.</span></span> <span data-ttu-id="ed6df-242">Используйте имя администратора компьютера **AzureAdmin** и пароль **Contoso!000**, которые вы указали при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ed6df-242">Use the machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created the VMs.</span></span>
2. <span data-ttu-id="ed6df-243">Убедитесь, что компьютеры успешно добавлены в домен **corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="ed6df-243">Verify that the computers have been successfully joined to **corp.contoso.com**.</span></span>
3. <span data-ttu-id="ed6df-244">Дождитесь, пока программа установки SQL Server не завершит автоматические задачи инициализации, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="ed6df-244">Wait for the SQL Server installation to finish running the automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="ed6df-245">Откройте окно PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="ed6df-245">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="ed6df-246">Установите компонент отказоустойчивой кластеризации Windows.</span><span class="sxs-lookup"><span data-stu-id="ed6df-246">Install the Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="ed6df-247">Добавьте **CORP\Install** в качестве локального администратора.</span><span class="sxs-lookup"><span data-stu-id="ed6df-247">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="ed6df-248">Импортируйте поставщика SQL Server PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed6df-248">Import the SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. <span data-ttu-id="ed6df-249">Добавьте **CORP\Install** в качестве роли sysadmin для экземпляра SQL Server по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ed6df-249">Add **CORP\Install** as the sysadmin role for the default SQL Server instance.</span></span>

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. <span data-ttu-id="ed6df-250">Добавьте **NT AUTHORITY\System** в качестве имени входа с тремя описанными выше разрешениями.</span><span class="sxs-lookup"><span data-stu-id="ed6df-250">Add **NT AUTHORITY\System** as a sign-in with the three permissions described above.</span></span>

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP TO [NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL TO [NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE TO [NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. <span data-ttu-id="ed6df-251">Откройте брандмауэр для удаленного доступа к SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed6df-251">Open the firewall for remote access of SQL Server.</span></span>

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. <span data-ttu-id="ed6df-252">Выйдите из обеих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="ed6df-252">Sign out of both VMs.</span></span>

         logoff.exe

<span data-ttu-id="ed6df-253">Теперь можно приступить к настройке группы доступности.</span><span class="sxs-lookup"><span data-stu-id="ed6df-253">Finally, you're ready to configure the availability group.</span></span> <span data-ttu-id="ed6df-254">Для выполнения всех действий с **ContosoSQL1** будет использоваться поставщик SQL Server PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed6df-254">You'll use the SQL Server PowerShell Provider to perform all of the work on **ContosoSQL1**.</span></span>

## <a name="configure-the-availability-group"></a><span data-ttu-id="ed6df-255">Настройка группы доступности</span><span class="sxs-lookup"><span data-stu-id="ed6df-255">Configure the availability group</span></span>
1. <span data-ttu-id="ed6df-256">Снова подключитесь к **ContosoSQL1** , запустив файлы удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="ed6df-256">Connect to **ContosoSQL1** again by launching the remote desktop files.</span></span> <span data-ttu-id="ed6df-257">Вместо входа с помощью учетной записи компьютера войдите с помощью учетной записи **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="ed6df-257">Instead of signing in by using the machine account, sign in by using **CORP\Install**.</span></span>
2. <span data-ttu-id="ed6df-258">Откройте окно PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="ed6df-258">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="ed6df-259">Определите следующие переменные.</span><span class="sxs-lookup"><span data-stu-id="ed6df-259">Define the following variables:</span></span>

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
4. <span data-ttu-id="ed6df-260">Импортируйте поставщика SQL Server PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed6df-260">Import the SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. <span data-ttu-id="ed6df-261">Измените учетную запись службы SQL Server для ContosoSQL1 на CORP\SQLSvc1.</span><span class="sxs-lookup"><span data-stu-id="ed6df-261">Change the SQL Server service account for ContosoSQL1 to CORP\SQLSvc1.</span></span>

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. <span data-ttu-id="ed6df-262">Измените учетную запись службы SQL Server для ContosoSQL2 на CORP\SQLSvc2.</span><span class="sxs-lookup"><span data-stu-id="ed6df-262">Change the SQL Server service account for ContosoSQL2 to CORP\SQLSvc2.</span></span>

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. <span data-ttu-id="ed6df-263">Скачайте файл **CreateAzureFailoverCluster.ps1** из статьи [Create Failover Cluster for Always On Availability Groups in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) (Создание отказоустойчивого кластера для групп доступности Always On на виртуальной машине Azure) в локальный рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="ed6df-263">Download **CreateAzureFailoverCluster.ps1** from [Create Failover Cluster for Always On Availability Groups in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) to the local working directory.</span></span> <span data-ttu-id="ed6df-264">Этот скрипт поможет создать рабочий отказоустойчивый кластер.</span><span class="sxs-lookup"><span data-stu-id="ed6df-264">You'll use this script to help you create a functional failover cluster.</span></span> <span data-ttu-id="ed6df-265">Важные сведения о взаимодействии кластеров Windows с сетью Azure см. в статье [Высокий уровень доступности и аварийное восстановление для SQL Server на виртуальных машинах Azure](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ed6df-265">For important information on how Windows Failover Clustering interacts with the Azure network, see [High availability and disaster recovery for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>
8. <span data-ttu-id="ed6df-266">Измените рабочий каталог и создайте отказоустойчивый кластер с помощью скачанного сценария.</span><span class="sxs-lookup"><span data-stu-id="ed6df-266">Change to your working directory and create the failover cluster with the downloaded script.</span></span>

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. <span data-ttu-id="ed6df-267">Включите группы доступности Always On для экземпляров SQL Server по умолчанию на виртуальных машинах **ContosoSQL1** и **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="ed6df-267">Enable Always On availability groups for the default SQL Server instances on **ContosoSQL1** and **ContosoSQL2**.</span></span>

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
10. <span data-ttu-id="ed6df-268">Создайте каталог резервной копии и предоставьте разрешения для учетных записей службы SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed6df-268">Create a backup directory and grant permissions for the SQL Server service accounts.</span></span> <span data-ttu-id="ed6df-269">Этот каталог будет использоваться для подготовки базы данных на вторичной реплике.</span><span class="sxs-lookup"><span data-stu-id="ed6df-269">You'll use this directory to prepare the availability database on the secondary replica.</span></span>

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. <span data-ttu-id="ed6df-270">Создайте базу данных в **ContosoSQL1** с именем **MyDB1**, создайте полный архив и архив журнала, а затем восстановите их на виртуальной машине **ContosoSQL2** с параметром **WITH NORECOVERY**.</span><span class="sxs-lookup"><span data-stu-id="ed6df-270">Create a database on **ContosoSQL1** called **MyDB1**, take both a full backup and a log backup, and restore them on **ContosoSQL2** with the **WITH NORECOVERY** option.</span></span>

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. <span data-ttu-id="ed6df-271">Создайте конечные точки группы доступности на трех ВМ SQL Server и задайте соответствующие разрешения для конечных точек.</span><span class="sxs-lookup"><span data-stu-id="ed6df-271">Create the availability group endpoints on the SQL Server VMs and set the proper permissions on the endpoints.</span></span>

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
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] TO [$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] TO [$acct1]" -ServerInstance $server2
13. <span data-ttu-id="ed6df-272">Создайте реплики доступности.</span><span class="sxs-lookup"><span data-stu-id="ed6df-272">Create the availability replicas.</span></span>

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
14. <span data-ttu-id="ed6df-273">Теперь создайте группу доступности и добавьте в нее вторичную реплику.</span><span class="sxs-lookup"><span data-stu-id="ed6df-273">Finally, create the availability group and join the secondary replica to the availability group.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ed6df-274">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ed6df-274">Next steps</span></span>
<span data-ttu-id="ed6df-275">Решение SQL Server Always On на основе группы доступности в Azure успешно создано.</span><span class="sxs-lookup"><span data-stu-id="ed6df-275">You've now successfully implemented SQL Server Always On by creating an availability group in Azure.</span></span> <span data-ttu-id="ed6df-276">Инструкции по настройке прослушивателя для этой группы доступности см. в статье [Настройка прослушивателя внутренней подсистемы балансировки нагрузки для группы доступности Always On в Azure](../classic/ps-sql-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="ed6df-276">To configure a listener for this availability group, see [Configure an ILB listener for Always On availability groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="ed6df-277">Дополнительные сведения об использовании SQL Server в Azure см. в статье [Общие сведения об SQL Server на виртуальных машинах Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ed6df-277">For other information about using SQL Server in Azure, see [SQL Server on Azure virtual machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
