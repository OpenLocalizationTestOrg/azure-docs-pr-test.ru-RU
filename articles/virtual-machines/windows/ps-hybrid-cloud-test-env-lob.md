---
title: "aaaLOB приложения тестовой среды | Документы Microsoft"
description: "Узнайте, как Интернет toocreate бизнес-приложений в гибридной облачной среды для IT pro или разработка тестирование."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 92d2d8ce-60ed-4512-95e5-a7fe3b0ca00b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: e9f825bbb1cbeb841ee3c974ebf6721dc236c311
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a><span data-ttu-id="38d65-103">Настройка веб бизнес-приложения в гибридном облаке для тестирования</span><span class="sxs-lookup"><span data-stu-id="38d65-103">Set up a web-based LOB application in a hybrid cloud for testing</span></span>
<span data-ttu-id="38d65-104">В этом разделе описываются шаги по созданию имитации гибридной облачной среды для тестирования сетевого бизнес-приложения, размещенного в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="38d65-104">This topic steps you through creating a simulated hybrid cloud environment for testing a web-based line of business (LOB) application hosted in Microsoft Azure.</span></span> <span data-ttu-id="38d65-105">Здесь представлена конфигурация полученный hello.</span><span class="sxs-lookup"><span data-stu-id="38d65-105">Here is hello resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="38d65-106">В эту конфигурацию входят:</span><span class="sxs-lookup"><span data-stu-id="38d65-106">This configuration consists of:</span></span>

* <span data-ttu-id="38d65-107">Имитация локальной сети, размещенных в Azure (hello тестовая лаборатория виртуальной сети).</span><span class="sxs-lookup"><span data-stu-id="38d65-107">A simulated on-premises network hosted in Azure (hello TestLab VNet).</span></span>
* <span data-ttu-id="38d65-108">виртуальная сеть с подключением между организациями, размещенная в Azure (TestVNET);</span><span class="sxs-lookup"><span data-stu-id="38d65-108">A cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="38d65-109">VPN-подключение типа "виртуальная сеть — виртуальная сеть";</span><span class="sxs-lookup"><span data-stu-id="38d65-109">A VNet-to-VNet VPN connection.</span></span>
* <span data-ttu-id="38d65-110">Веб-сервера LOB, SQL server и дополнительный контроллер домена в виртуальной сети TestVNET hello.</span><span class="sxs-lookup"><span data-stu-id="38d65-110">A web-based LOB server, SQL server, and secondary domain controller in hello TestVNET virtual network.</span></span>

<span data-ttu-id="38d65-111">Это основа и общая начальная точка, на базе которой можно:</span><span class="sxs-lookup"><span data-stu-id="38d65-111">This configuration provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="38d65-112">разрабатывать и тестировать бизнес-приложения, размещенные в службах IIS, с помощью сервера базы данных SQL Server 2014 в Azure.</span><span class="sxs-lookup"><span data-stu-id="38d65-112">Develop and test LOB applications hosted on Internet Information Services (IIS) with a SQL Server 2014 database backend in Azure.</span></span>
* <span data-ttu-id="38d65-113">выполнять тестирование имитации гибридной облачной рабочей нагрузки ИТ-среды.</span><span class="sxs-lookup"><span data-stu-id="38d65-113">Perform testing of this simulated hybrid cloud-based IT workload.</span></span>

<span data-ttu-id="38d65-114">Существует три основных этапа toosetting этой тестовой среды гибридного облака:</span><span class="sxs-lookup"><span data-stu-id="38d65-114">There are three major phases toosetting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="38d65-115">Настройка hello имитацию гибридной облачной среды.</span><span class="sxs-lookup"><span data-stu-id="38d65-115">Set up hello simulated hybrid cloud environment.</span></span>
2. <span data-ttu-id="38d65-116">Настройка компьютера hello SQL server (SQL1).</span><span class="sxs-lookup"><span data-stu-id="38d65-116">Configure hello SQL server computer (SQL1).</span></span>
3. <span data-ttu-id="38d65-117">Настройка сервера LOB hello (LOB1).</span><span class="sxs-lookup"><span data-stu-id="38d65-117">Configure hello LOB server (LOB1).</span></span>

<span data-ttu-id="38d65-118">Для этой рабочей нагрузки требуется подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="38d65-118">This workload requires an Azure subscription.</span></span> <span data-ttu-id="38d65-119">Если у вас есть подписка MSDN или Visual Studio, ознакомьтесь с разделом [Ежемесячная сумма денег на счете в Azure для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="38d65-119">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

<span data-ttu-id="38d65-120">Пример производства бизнес-приложения, размещенные в Azure см. в разделе hello **бизнес-приложений** чертежом архитектуры в [схем архитектуры программного обеспечения корпорации Майкрософт и чертежей](http://msdn.microsoft.com/dn630664).</span><span class="sxs-lookup"><span data-stu-id="38d65-120">For an example of a production LOB application hosted in Azure, see hello **Line of business applications** architecture blueprint at [Microsoft Software Architecture Diagrams and Blueprints](http://msdn.microsoft.com/dn630664).</span></span>

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a><span data-ttu-id="38d65-121">Этап 1: Настройка hello имитацию гибридной облачной среды</span><span class="sxs-lookup"><span data-stu-id="38d65-121">Phase 1: Set up hello simulated hybrid cloud environment</span></span>
<span data-ttu-id="38d65-122">Создать hello [имитацию гибридного облака тестовой среде](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="38d65-122">Create hello [simulated hybrid cloud test environment](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="38d65-123">Поскольку данной тестовой среды не требуется наличие hello server hello APP1 в подсети корпоративной сети hello, можно завершить работу сейчас.</span><span class="sxs-lookup"><span data-stu-id="38d65-123">Because this test environment does not require hello presence of hello APP1 server on hello Corpnet subnet, you can shut it down for now.</span></span>

<span data-ttu-id="38d65-124">Это текущая конфигурация.</span><span class="sxs-lookup"><span data-stu-id="38d65-124">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a><span data-ttu-id="38d65-125">Этап 2: Настройка компьютера hello SQL server (SQL1)</span><span class="sxs-lookup"><span data-stu-id="38d65-125">Phase 2: Configure hello SQL server computer (SQL1)</span></span>
<span data-ttu-id="38d65-126">При необходимости начать компьютер DC2 hello hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="38d65-126">From hello Azure portal, start hello DC2 computer if needed.</span></span>

<span data-ttu-id="38d65-127">Теперь создайте виртуальную машину для SQL1, выполнив следующие команды в командной строке Azure PowerShell на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="38d65-127">Next, create a virtual machine for SQL1 with these commands at an Azure PowerShell command prompt on your local computer.</span></span> <span data-ttu-id="38d65-128">Предыдущий toorunning эти команды заполнить hello значения переменных и удалить hello < и > символов.</span><span class="sxs-lookup"><span data-stu-id="38d65-128">Prior toorunning these commands, fill in hello variable values and remove hello < and > characters.</span></span>

    $rgName="<your resource group name>"
    $locName="<hello Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for hello SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="38d65-129">Используйте hello Azure портала tooconnect tooSQL1 с помощью учетной записи локального администратора hello SQL1.</span><span class="sxs-lookup"><span data-stu-id="38d65-129">Use hello Azure portal tooconnect tooSQL1 using hello local administrator account of SQL1.</span></span>

<span data-ttu-id="38d65-130">Настройте брандмауэр Windows правила tooallow связности тестирования и трафик SQL Server.</span><span class="sxs-lookup"><span data-stu-id="38d65-130">Next, configure Windows Firewall rules tooallow basic connectivity testing and SQL Server traffic.</span></span> <span data-ttu-id="38d65-131">Из командной строки Windows PowerShell с правами администратора на SQL1 выполните следующие команды.</span><span class="sxs-lookup"><span data-stu-id="38d65-131">From an administrator-level Windows PowerShell command prompt on SQL1, run these commands.</span></span>

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="38d65-132">команда ping Hello должны появиться четыре успешного ответа от IP-адрес 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="38d65-132">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="38d65-133">Добавьте hello дополнительный диск данных на сервере SQL1 как новый том с буквой hello диска «f:».</span><span class="sxs-lookup"><span data-stu-id="38d65-133">Next, add hello extra data disk on SQL1 as a new volume with hello drive letter F:.</span></span>

1. <span data-ttu-id="38d65-134">Hello левой панели диспетчера сервера щелкните **файловых служб и служб хранилища**, а затем нажмите кнопку **дисков**.</span><span class="sxs-lookup"><span data-stu-id="38d65-134">In hello left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="38d65-135">В области содержимого hello в hello **дисков** щелкните **диск 2** (с hello **секции** значение слишком**Неизвестный**).</span><span class="sxs-lookup"><span data-stu-id="38d65-135">In hello contents pane, in hello **Disks** group, click **disk 2** (with hello **Partition** set too**Unknown**).</span></span>
3. <span data-ttu-id="38d65-136">Щелкните **Задачи**, а затем **Новый том**.</span><span class="sxs-lookup"><span data-stu-id="38d65-136">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="38d65-137">Hello перед началом страница приветствия мастера создания тома, щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="38d65-137">On hello Before you begin page of hello New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="38d65-138">На сервере выберите hello hello и страницы с диска, нажмите кнопку **диск 2**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="38d65-138">On hello Select hello server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="38d65-139">При появлении запроса нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="38d65-139">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="38d65-140">Щелкните hello задать hello размер страницы приветствия тома, **Далее**.</span><span class="sxs-lookup"><span data-stu-id="38d65-140">On hello Specify hello size of hello volume page, click **Next**.</span></span>
7. <span data-ttu-id="38d65-141">На hello Assign tooa диска буква или папка "нажмите" **Далее**.</span><span class="sxs-lookup"><span data-stu-id="38d65-141">On hello Assign tooa drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="38d65-142">На странице параметров системы hello выберите файл, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="38d65-142">On hello Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="38d65-143">На странице подтверждения выбранных элементов hello щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="38d65-143">On hello Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="38d65-144">После завершения нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="38d65-144">When complete, click **Close**.</span></span>

<span data-ttu-id="38d65-145">Выполняйте эти команды в командной строке Windows PowerShell hello на SQL1:</span><span class="sxs-lookup"><span data-stu-id="38d65-145">Run these commands at hello Windows PowerShell command prompt on SQL1:</span></span>

    md f:\Data
    md f:\Log
    md f:\Backup

<span data-ttu-id="38d65-146">Далее подсоедините SQL1 toohello CORP домена Windows Server Active Directory с помощью следующих команд в командной строке Windows PowerShell hello на SQL1.</span><span class="sxs-lookup"><span data-stu-id="38d65-146">Next, join SQL1 toohello CORP Windows Server Active Directory domain with these commands at hello Windows PowerShell prompt on SQL1.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="38d65-147">Использовать учетную запись hello CORP\User1 при появлении запроса учетных данных учетной записи домена toosupply для hello **Add-Computer** команды.</span><span class="sxs-lookup"><span data-stu-id="38d65-147">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="38d65-148">После перезагрузки компьютера используйте hello Azure портала tooconnect tooSQL1 *учетную запись локального администратора hello SQL1*.</span><span class="sxs-lookup"><span data-stu-id="38d65-148">After restarting, use hello Azure portal tooconnect tooSQL1 *with hello local administrator account of SQL1*.</span></span>

<span data-ttu-id="38d65-149">Настройте диска «f:» toouse hello SQL Server 2014 для новых баз данных, а также для разрешения учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="38d65-149">Next, configure SQL Server 2014 toouse hello F: drive for new databases and for user account permissions.</span></span>

1. <span data-ttu-id="38d65-150">Hello начальном экране введите **управления SQL Server**, а затем нажмите кнопку **SQL Server 2014 Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="38d65-150">From hello Start screen, type **SQL Server Management**, and then click **SQL Server 2014 Management Studio**.</span></span>
2. <span data-ttu-id="38d65-151">В **подключения tooServer**, нажмите кнопку **Connect**.</span><span class="sxs-lookup"><span data-stu-id="38d65-151">In **Connect tooServer**, click **Connect**.</span></span>
3. <span data-ttu-id="38d65-152">Щелкните правой кнопкой мыши в области дерева обозревателя объектов hello **SQL1**, а затем нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="38d65-152">In hello Object Explorer tree pane, right-click **SQL1**, and then click **Properties**.</span></span>
4. <span data-ttu-id="38d65-153">В hello **свойства сервера** окно, нажмите кнопку **параметры базы данных**.</span><span class="sxs-lookup"><span data-stu-id="38d65-153">In hello **Server Properties** window, click **Database Settings**.</span></span>
5. <span data-ttu-id="38d65-154">Найдите hello **базы данных по умолчанию расположений** и задайте следующие значения:</span><span class="sxs-lookup"><span data-stu-id="38d65-154">Locate hello **Database default locations** and set these values:</span></span> 
   * <span data-ttu-id="38d65-155">Для **данные**, путь к типу hello **f:\Data**.</span><span class="sxs-lookup"><span data-stu-id="38d65-155">For **Data**, type hello path **f:\Data**.</span></span>
   * <span data-ttu-id="38d65-156">Для **журнала**, путь к типу hello **f:\Log**.</span><span class="sxs-lookup"><span data-stu-id="38d65-156">For **Log**, type hello path **f:\Log**.</span></span>
   * <span data-ttu-id="38d65-157">Для **резервного копирования**, путь к типу hello **f:\Backup**.</span><span class="sxs-lookup"><span data-stu-id="38d65-157">For **Backup**, type hello path **f:\Backup**.</span></span>
   * <span data-ttu-id="38d65-158">Примечание. Только новые базы данных будут использовать эти расположения.</span><span class="sxs-lookup"><span data-stu-id="38d65-158">Note: Only new databases use these locations.</span></span>
6. <span data-ttu-id="38d65-159">Нажмите кнопку hello **ОК** tooclose окна hello.</span><span class="sxs-lookup"><span data-stu-id="38d65-159">Click hello **OK** tooclose hello window.</span></span>
7. <span data-ttu-id="38d65-160">В hello **обозревателя объектов** древовидном откройте **безопасности**.</span><span class="sxs-lookup"><span data-stu-id="38d65-160">In hello **Object Explorer** tree pane, open **Security**.</span></span>
8. <span data-ttu-id="38d65-161">Щелкните правой кнопкой мыши **Имена входа**, а затем выберите **Создать имя входа**.</span><span class="sxs-lookup"><span data-stu-id="38d65-161">Right-click **Logins** and then click **New Login**.</span></span>
9. <span data-ttu-id="38d65-162">В поле **Имя входа** введите **CORP\User1**.</span><span class="sxs-lookup"><span data-stu-id="38d65-162">In **Login name**, type **CORP\User1**.</span></span>
10. <span data-ttu-id="38d65-163">На hello **ролей сервера** щелкните **sysadmin**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="38d65-163">On hello **Server Roles** page, click **sysadmin**, and then click **OK**.</span></span>
11. <span data-ttu-id="38d65-164">Закройте Microsoft SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="38d65-164">Close Microsoft SQL Server Management Studio.</span></span>

<span data-ttu-id="38d65-165">Это текущая конфигурация.</span><span class="sxs-lookup"><span data-stu-id="38d65-165">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a><span data-ttu-id="38d65-166">Этап 3: Настройка сервера LOB hello (LOB1)</span><span class="sxs-lookup"><span data-stu-id="38d65-166">Phase 3: Configure hello LOB server (LOB1)</span></span>
<span data-ttu-id="38d65-167">Сначала создайте виртуальную машину для LOB1 с помощью следующих команд командной hello Azure PowerShell на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="38d65-167">First, create a virtual machine for LOB1 with these commands at hello Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="38d65-168">Затем используйте hello Azure портала tooconnect tooLOB1 с учетными данными hello LOB1 учетной записи локального администратора hello.</span><span class="sxs-lookup"><span data-stu-id="38d65-168">Next, use hello Azure portal tooconnect tooLOB1 with hello credentials of hello local administrator account of LOB1.</span></span>

<span data-ttu-id="38d65-169">Настройте трафика tooallow правило брандмауэра Windows для тестирования связности.</span><span class="sxs-lookup"><span data-stu-id="38d65-169">Next, configure a Windows Firewall rule tooallow traffic for basic connectivity testing.</span></span> <span data-ttu-id="38d65-170">Из командной строки Windows PowerShell с правами администратора на LOB1 выполните следующие команды.</span><span class="sxs-lookup"><span data-stu-id="38d65-170">From an administrator-level Windows PowerShell command prompt on LOB1, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="38d65-171">команда ping Hello должны появиться четыре успешного ответа от IP-адрес 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="38d65-171">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="38d65-172">Далее присоединен к домену CORP Active Directory toohello LOB1 с помощью следующих команд в командной строке Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="38d65-172">Next, join LOB1 toohello CORP Active Directory domain with these commands at hello Windows PowerShell prompt.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="38d65-173">Использовать учетную запись hello CORP\User1 при появлении запроса учетных данных учетной записи домена toosupply для hello **Add-Computer** команды.</span><span class="sxs-lookup"><span data-stu-id="38d65-173">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="38d65-174">После перезагрузки компьютера используйте hello Azure портала tooconnect tooLOB1 с hello CORP\User1 учетную запись и пароль.</span><span class="sxs-lookup"><span data-stu-id="38d65-174">After restarting, use hello Azure portal tooconnect tooLOB1 with hello CORP\User1 account and password.</span></span>

<span data-ttu-id="38d65-175">Затем настройте LOB1 для служб IIS и протестируйте доступ из CLIENT1.</span><span class="sxs-lookup"><span data-stu-id="38d65-175">Next, configure LOB1 for IIS and test access from CLIENT1.</span></span>

1. <span data-ttu-id="38d65-176">В диспетчере серверов выберите **Добавить роли и компоненты**.</span><span class="sxs-lookup"><span data-stu-id="38d65-176">From Server Manager, click **Add roles and features**.</span></span>
2. <span data-ttu-id="38d65-177">На hello **перед началом** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="38d65-177">On hello **Before you begin** page, click **Next**.</span></span>
3. <span data-ttu-id="38d65-178">На hello **Выбор типа установки** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="38d65-178">On hello **Select installation type** page, click **Next**.</span></span>
4. <span data-ttu-id="38d65-179">На hello **Выбор целевого сервера** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="38d65-179">On hello **Select destination server** page, click **Next**.</span></span>
5. <span data-ttu-id="38d65-180">На hello **ролей сервера** щелкните **веб-сервер (IIS)** в списке hello **ролей**.</span><span class="sxs-lookup"><span data-stu-id="38d65-180">On hello **Server roles** page, click **Web Server (IIS)** in hello list of **Roles**.</span></span>
6. <span data-ttu-id="38d65-181">При появлении запроса щелкните **Добавить компоненты**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="38d65-181">When prompted, click **Add Features**, and then click **Next**.</span></span>
7. <span data-ttu-id="38d65-182">На hello **Выбор компонентов** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="38d65-182">On hello **Select features** page, click **Next**.</span></span>
8. <span data-ttu-id="38d65-183">На hello **веб-сервер (IIS)** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="38d65-183">On hello **Web Server (IIS)** page, click **Next**.</span></span>
9. <span data-ttu-id="38d65-184">На hello **Выбор служб ролей** страницы, выберите или снимите флажки hello hello служб для проверки вашей бизнес-приложения и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="38d65-184">On hello **Select role services** page, select or clear hello check boxes for hello services you need for testing your LOB application, and then click **Next**.</span></span>
10. <span data-ttu-id="38d65-185">На hello **подтверждение выбранных параметров установки** щелкните **установить**.</span><span class="sxs-lookup"><span data-stu-id="38d65-185">On hello **Confirm installation selections** page, click **Install**.</span></span>
11. <span data-ttu-id="38d65-186">Дождитесь завершения установки hello компонентов и нажмите кнопку **закрыть**.</span><span class="sxs-lookup"><span data-stu-id="38d65-186">Wait until hello installation of components has completed and then click **Close**.</span></span>
12. <span data-ttu-id="38d65-187">Из hello портал Azure подключите компьютер CLIENT1 toohello с учетными данными учетной записью CORP\User1 hello, а затем запустите Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="38d65-187">From hello Azure portal, connect toohello CLIENT1 computer with hello CORP\User1 account credentials, and then start Internet Explorer.</span></span>
13. <span data-ttu-id="38d65-188">Введите в адресной строке hello **http://lob1/** и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="38d65-188">In hello Address bar, type **http://lob1/** and then press ENTER.</span></span> <span data-ttu-id="38d65-189">Вы увидите веб-страницы IIS 8 умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="38d65-189">You should see hello default IIS 8 web page.</span></span>

<span data-ttu-id="38d65-190">Это текущая конфигурация.</span><span class="sxs-lookup"><span data-stu-id="38d65-190">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="38d65-191">Эта среда хорошо, теперь готовы для вас toodeploy веб-приложения на LOB1 и тестирования функции из CLIENT1 в подсети корпоративной сети hello.</span><span class="sxs-lookup"><span data-stu-id="38d65-191">This environment is now ready for you toodeploy your web-based application on LOB1 and test functionality from CLIENT1 on hello Corpnet subnet.</span></span>

## <a name="next-step"></a><span data-ttu-id="38d65-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="38d65-192">Next step</span></span>
* <span data-ttu-id="38d65-193">Добавить новую виртуальную машину с помощью hello [портал Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="38d65-193">Add a new virtual machine using hello [Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

