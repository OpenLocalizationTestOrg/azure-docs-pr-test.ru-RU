---
title: "aaaCreate виртуальной Машины Windows с помощью PowerShell | Документы Microsoft"
description: "Создайте виртуальные машины Windows с помощью Azure PowerShell и hello классической модели развертывания."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 42c0d4be-573c-45d1-b9b0-9327537702f7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 5339f458c1f08f6e1752a53191f19402fab8ea25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-hello-classic-deployment-model"></a><span data-ttu-id="ea764-103">Создание виртуальной машины Windows с помощью PowerShell и hello классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="ea764-103">Create a Windows virtual machine with PowerShell and hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea764-104">Портал Azure — Windows</span><span class="sxs-lookup"><span data-stu-id="ea764-104">Azure portal - Windows</span></span>](tutorial.md)
> * [<span data-ttu-id="ea764-105">PowerShell — Windows</span><span class="sxs-lookup"><span data-stu-id="ea764-105">PowerShell - Windows</span></span>](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> <span data-ttu-id="ea764-106">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ea764-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ea764-107">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="ea764-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ea764-108">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ea764-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ea764-109">Узнайте, каким образом слишком[выполните следующие действия с помощью диспетчера ресурсов модели hello](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ea764-109">Learn how too[perform these steps using hello Resource Manager model](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="ea764-110">Следующие шаги показывают, как toocustomize набор Azure PowerShell команды, создание и предварительная настройка виртуальной машины на основе Windows Azure, используя подход стандартного блока.</span><span class="sxs-lookup"><span data-stu-id="ea764-110">These steps show you how toocustomize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="ea764-111">Этот процесс можно использовать tooquickly создать набор команд для новой виртуальной машины под управлением Windows и разверните существующего развертывания, или toocreate несколько команда задает, быстро строить пользовательские разработки и тестирования или специалистов ИТ-среде.</span><span class="sxs-lookup"><span data-stu-id="ea764-111">You can use this process tooquickly create a command set for a new Windows-based virtual machine and expand an existing deployment or toocreate multiple command sets that quickly build out a custom dev/test or IT pro environment.</span></span>

<span data-ttu-id="ea764-112">Материал в этих шагах для создания наборов команд Azure PowerShell представлен таким образом, что достаточно лишь заполнить пробелы.</span><span class="sxs-lookup"><span data-stu-id="ea764-112">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="ea764-113">Этот подход может оказаться полезным, если вы являетесь новый tooPowerShell или необходимо просто tooknow toospecify какие значения для успешной настройки.</span><span class="sxs-lookup"><span data-stu-id="ea764-113">This approach can be useful if you are new tooPowerShell or you just want tooknow what values toospecify for successful configuration.</span></span> <span data-ttu-id="ea764-114">Опытные пользователи PowerShell можно воспользоваться командами hello и подставьте собственные значения для переменных hello (hello строки, начинающиеся с «$»).</span><span class="sxs-lookup"><span data-stu-id="ea764-114">Advanced PowerShell users can take hello commands and substitute their own values for hello variables (hello lines beginning with "$").</span></span>

<span data-ttu-id="ea764-115">Если вы еще не сделали этого, используйте инструкции hello в [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="ea764-115">If you haven't done so already, use hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell on your local computer.</span></span> <span data-ttu-id="ea764-116">Затем откройте командную строку Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea764-116">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="ea764-117">Шаг 1. Добавление учетной записи</span><span class="sxs-lookup"><span data-stu-id="ea764-117">Step 1: Add your account</span></span>
1. <span data-ttu-id="ea764-118">Введите в командной строке PowerShell hello **Add-AzureAccount** и нажмите кнопку **ввод**.</span><span class="sxs-lookup"><span data-stu-id="ea764-118">At hello PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span> 
2. <span data-ttu-id="ea764-119">Введите адрес электронной почты hello, связанных с подпиской Azure и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="ea764-119">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="ea764-120">Введите в hello пароль своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ea764-120">Type in hello password for your account.</span></span> 
4. <span data-ttu-id="ea764-121">Щелкните **Войти**.</span><span class="sxs-lookup"><span data-stu-id="ea764-121">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="ea764-122">Шаг 2. Выбор подписки и учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="ea764-122">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="ea764-123">Задайте подписка Azure и учетной записи хранилища, выполнив следующие команды в командной строке Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ea764-123">Set your Azure subscription and storage account by running these commands at hello Windows PowerShell command prompt.</span></span> <span data-ttu-id="ea764-124">Замените все содержимое в кавычках hello, включая hello < и > символы, правильные имена hello.</span><span class="sxs-lookup"><span data-stu-id="ea764-124">Replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="ea764-125">Hello правильное имя подписки можно получить из hello свойство Имя_подписки выходной hello hello **Get-AzureSubscription** команды.</span><span class="sxs-lookup"><span data-stu-id="ea764-125">You can get hello correct subscription name from hello SubscriptionName property of hello output of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="ea764-126">Можно получить имя учетной записи хранения правильно hello hello свойства Label выходные данные hello hello **Get AzureStorageAccount** команду после запуска hello **Select-AzureSubscription** команды.</span><span class="sxs-lookup"><span data-stu-id="ea764-126">You can get hello correct storage account name from hello Label property of hello output of hello **Get-AzureStorageAccount** command after you run hello **Select-AzureSubscription** command.</span></span>

## <a name="step-3-determine-hello-imagefamily"></a><span data-ttu-id="ea764-127">Шаг 3: Определение hello ImageFamily</span><span class="sxs-lookup"><span data-stu-id="ea764-127">Step 3: Determine hello ImageFamily</span></span>
<span data-ttu-id="ea764-128">Далее необходимо toodetermine hello ImageFamily или значение метки для соответствующего toohello hello конкретный образ виртуальной машины Azure требуется toocreate.</span><span class="sxs-lookup"><span data-stu-id="ea764-128">Next, you need toodetermine hello ImageFamily or Label value for hello specific image corresponding toohello Azure virtual machine you want toocreate.</span></span> <span data-ttu-id="ea764-129">Вы можете получить hello список доступных значений ImageFamily с помощью этой команды.</span><span class="sxs-lookup"><span data-stu-id="ea764-129">You can get hello list of available ImageFamily values with this command.</span></span>

    Get-AzureVMImage | select ImageFamily -Unique

<span data-ttu-id="ea764-130">Ниже приведено несколько примеров значений ImageFamily для компьютеров под управлением Windows:</span><span class="sxs-lookup"><span data-stu-id="ea764-130">Here are some examples of ImageFamily values for Windows-based computers:</span></span>

* <span data-ttu-id="ea764-131">Центр обработки данных Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="ea764-131">Windows Server 2012 R2 Datacenter</span></span>
* <span data-ttu-id="ea764-132">Windows Server 2008 R2 с пакетом обновления 1</span><span class="sxs-lookup"><span data-stu-id="ea764-132">Windows Server 2008 R2 SP1</span></span>
* <span data-ttu-id="ea764-133">Windows Server 2016 Technical Preview 4</span><span class="sxs-lookup"><span data-stu-id="ea764-133">Windows Server 2016 Technical Preview 4</span></span>
* <span data-ttu-id="ea764-134">SQL Server 2012 SP1 Enterprise на базе Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="ea764-134">SQL Server 2012 SP1 Enterprise on Windows Server 2012</span></span>

<span data-ttu-id="ea764-135">Если найти образ hello, которую вы ищете, откройте создания нового экземпляра редактора текста hello choice или hello PowerShell интегрированная среда сценариев (ISE).</span><span class="sxs-lookup"><span data-stu-id="ea764-135">If you find hello image you are looking for, open a fresh instance of hello text editor of your choice or hello PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="ea764-136">Скопируйте следующие hello в hello новый текстовый файл или hello интегрированной среды Сценариев PowerShell, заменив значение ImageFamily hello.</span><span class="sxs-lookup"><span data-stu-id="ea764-136">Copy hello following into hello new text file or hello PowerShell ISE, substituting hello ImageFamily value.</span></span>

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="ea764-137">В некоторых случаях имя образа hello уже hello свойства Label вместо hello значение ImageFamily.</span><span class="sxs-lookup"><span data-stu-id="ea764-137">In some cases, hello image name is in hello Label property instead of hello ImageFamily value.</span></span> <span data-ttu-id="ea764-138">Если вы не нашли hello образ, который вы ищете с помощью свойства ImageFamily hello, списка образов hello по их свойству метки с помощью этой команды.</span><span class="sxs-lookup"><span data-stu-id="ea764-138">If you didn't find hello image that you are looking for using hello ImageFamily property, list hello images by their Label property with this command.</span></span>

    Get-AzureVMImage | select Label -Unique

<span data-ttu-id="ea764-139">Если вы нашли hello правом изображении с помощью этой команды, откройте создания нового экземпляра hello текстовом редакторе choice или hello интегрированной среды Сценариев PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea764-139">If you find hello right image with this command, open a fresh instance of hello text editor of your choice or hello PowerShell ISE.</span></span> <span data-ttu-id="ea764-140">Скопируйте следующие hello в hello новый текстовый файл или hello интегрированной среды Сценариев PowerShell, заменив значение метки hello.</span><span class="sxs-lookup"><span data-stu-id="ea764-140">Copy hello following into hello new text file or hello PowerShell ISE, substituting hello Label value.</span></span>

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a><span data-ttu-id="ea764-141">Шаг 4. Создание своего набора команд</span><span class="sxs-lookup"><span data-stu-id="ea764-141">Step 4: Build your command set</span></span>
<span data-ttu-id="ea764-142">Построение rest hello набор путем копирования в новый текстовый файл или hello интегрированной среды Сценариев и затем заполнив hello значения переменных, а также удаление hello < и > символов hello соответствующий набор блоков ниже команды.</span><span class="sxs-lookup"><span data-stu-id="ea764-142">Build hello rest of your command set by copying hello appropriate set of blocks below into your new text file or hello ISE and then filling in hello variable values and removing hello < and > characters.</span></span> <span data-ttu-id="ea764-143">. В разделе hello двух [примеры](#examples) конце hello в этой статье для получения представления hello конечного результата.</span><span class="sxs-lookup"><span data-stu-id="ea764-143">See hello two [examples](#examples) at hello end of this article for an idea of hello final result.</span></span>

<span data-ttu-id="ea764-144">Начните создавать свой набор команд, выбрав один из этих двух блоков команд (обязательно).</span><span class="sxs-lookup"><span data-stu-id="ea764-144">Start your command set by choosing one of these two command blocks (required).</span></span>

<span data-ttu-id="ea764-145">Вариант 1. Укажите имя и размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ea764-145">Option 1: Specify a virtual machine name and a size.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="ea764-146">Вариант 2. Укажите имя, размер, а также имя группы доступности.</span><span class="sxs-lookup"><span data-stu-id="ea764-146">Option 2: Specify a name, size, and availability set name.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

<span data-ttu-id="ea764-147">Hello InstanceSize значения для D-, DS- или виртуальные машины серии G см [виртуальной машины размеры и облачных служб для Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea764-147">For hello InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="ea764-148">Если Enterprise Agreement с программой Software Assurance и предполагаете tootake преимуществами hello Windows Server [преимущество использования гибридной](https://azure.microsoft.com/pricing/hybrid-use-benefit/), добавьте **- LicenseType** toohello параметр  **Новый AzureVMConfig** командлета, передав значение hello **Windows_Server** hello типичный вариант использования.</span><span class="sxs-lookup"><span data-stu-id="ea764-148">If you have an Enterprise Agreement with Software Assurance, and intend tootake advantage of hello Windows Server [Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/), add the **-LicenseType** parameter toohello **New-AzureVMConfig** cmdlet, passing hello value **Windows_Server** for hello typical use case.</span></span>  <span data-ttu-id="ea764-149">Убедитесь, что вы используете образ, который вы отправили; нельзя использовать стандартный образ из коллекции hello с hello гибридного использовать преимущество.</span><span class="sxs-lookup"><span data-stu-id="ea764-149">Be sure you are using an image you have uploaded; you cannot use a standard image from hello Gallery with hello Hybrid Use Benefit.</span></span>
> 
> 

<span data-ttu-id="ea764-150">При необходимости для автономном компьютере Windows, укажите hello учетной записи локального администратора и пароль.</span><span class="sxs-lookup"><span data-stu-id="ea764-150">Optionally, for a standalone Windows computer, specify hello local administrator account and password.</span></span>

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

<span data-ttu-id="ea764-151">Выберите надежный пароль.</span><span class="sxs-lookup"><span data-stu-id="ea764-151">Choose a strong password.</span></span> <span data-ttu-id="ea764-152">toocheck его надежность. в разделе [проверки паролей: использование надежных паролей](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea764-152">toocheck its strength, see [Password Checker: Using Strong Passwords](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span></span>

<span data-ttu-id="ea764-153">При необходимости tooadd hello Windows компьютер tooan существующему домену Active Directory, укажите hello учетной записи локального администратора и пароль, домен hello hello имя и пароль учетной записи домена.</span><span class="sxs-lookup"><span data-stu-id="ea764-153">Optionally, tooadd hello Windows computer tooan existing Active Directory domain, specify hello local administrator account and password, hello domain, and hello name and password of a domain account.</span></span>

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="<FQDN of hello domain that hello machine is joining>"
    $domacctdomain="<domain of hello account that has permission tooadd hello machine toohello domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="ea764-154">Дополнительные способы предварительной настройки виртуальных машин под управлением Windows, см. синтаксис hello hello **Windows** и **WindowsDomain** наборы параметров [ -AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span><span class="sxs-lookup"><span data-stu-id="ea764-154">For additional pre-configuration options for Windows-based virtual machines, see hello syntax for hello **Windows** and **WindowsDomain** parameter sets in [Add-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span></span>

<span data-ttu-id="ea764-155">При необходимости назначьте виртуальной машине hello определенный IP-адрес, известный как статический DIP-адрес.</span><span class="sxs-lookup"><span data-stu-id="ea764-155">Optionally, assign hello virtual machine a specific IP address, known as a static DIP.</span></span>

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

<span data-ttu-id="ea764-156">Доступность определенного IP-адреса можно проверить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ea764-156">You can verify that a specific IP address is available with:</span></span>

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

<span data-ttu-id="ea764-157">При необходимости назначьте hello виртуальной машины tooa конкретной подсети в виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="ea764-157">Optionally, assign hello virtual machine tooa specific subnet in an Azure virtual network.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "<name of hello subnet>"

<span data-ttu-id="ea764-158">При необходимости добавьте данные одного диска toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ea764-158">Optionally, add a single data disk toohello virtual machine.</span></span>

    $disksize=<size of hello disk in GB>
    $disklabel="<hello label on hello disk>"
    $lun=<Logical Unit Number (LUN) of hello disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

<span data-ttu-id="ea764-159">Для контроллера домена Active Directory, задайте $hcaching слишком «None».</span><span class="sxs-lookup"><span data-stu-id="ea764-159">For an Active Directory domain controller, set $hcaching too"None".</span></span>

<span data-ttu-id="ea764-160">При необходимости добавьте hello виртуальной машины tooan существующий набор балансировки нагрузки для внешнего трафика.</span><span class="sxs-lookup"><span data-stu-id="ea764-160">Optionally, add hello virtual machine tooan existing load-balanced set for external traffic.</span></span>

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of hello internal port>
    $pubport=<port number of hello external port>
    $endpointname="<name of hello endpoint>"
    $lbsetname="<name of hello existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

<span data-ttu-id="ea764-161">Наконец можно выберите один из этих блоков необходимую команду для создания виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="ea764-161">Finally, choose one of these required command blocks for creating hello virtual machine.</span></span>

<span data-ttu-id="ea764-162">Вариант 1: Создание виртуальной машины hello в существующей облачной службе.</span><span class="sxs-lookup"><span data-stu-id="ea764-162">Option 1: Create hello virtual machine in an existing cloud service.</span></span>

    New-AzureVM –ServiceName "<short name of hello cloud service>" -VMs $vm1

<span data-ttu-id="ea764-163">Краткое имя Hello hello облачной службы является hello имя, которое отображается в списке hello облачных служб в hello портал Azure или hello список групп ресурсов в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ea764-163">hello short name of hello cloud service is hello name that appears in hello list of Cloud Services in hello Azure portal or in hello list of Resource Groups in hello Azure portal.</span></span>

<span data-ttu-id="ea764-164">Вариант 2: Создание виртуальной машины hello в существующей облачной службы и виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ea764-164">Option 2: Create hello virtual machine in an existing cloud service and virtual network.</span></span>

    $svcname="<short name of hello cloud service>"
    $vnetname="<name of hello virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a><span data-ttu-id="ea764-165">Шаг 5. Запуск набора команд</span><span class="sxs-lookup"><span data-stu-id="ea764-165">Step 5: Run your command set</span></span>
<span data-ttu-id="ea764-166">Просмотрите набор команд Azure PowerShell hello, созданных в текстовом редакторе или hello интегрированной среды Сценариев PowerShell, состоящий из нескольких блоков команды из шага 4.</span><span class="sxs-lookup"><span data-stu-id="ea764-166">Review hello Azure PowerShell command set you built in your text editor or hello PowerShell ISE consisting of multiple blocks of commands from step 4.</span></span> <span data-ttu-id="ea764-167">Убедитесь, что указаны все переменные hello требуется и что они имеют правильные значения hello.</span><span class="sxs-lookup"><span data-stu-id="ea764-167">Ensure that you have specified all hello needed variables and that they have hello correct values.</span></span> <span data-ttu-id="ea764-168">Убедитесь, что были удалены все символы hello < и >.</span><span class="sxs-lookup"><span data-stu-id="ea764-168">Also make sure that you have removed all hello < and > characters.</span></span>

<span data-ttu-id="ea764-169">При использовании в текстовом редакторе, команду копирования hello задать toohello буфер обмена и щелкните правой кнопкой мыши откройте командную строку Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea764-169">If you are using a text editor, copy hello command set toohello clipboard and then right-click your open Windows PowerShell command prompt.</span></span> <span data-ttu-id="ea764-170">Это будет выдавать набор команд hello как ряд команд PowerShell, а также создать виртуальную машину Azure.</span><span class="sxs-lookup"><span data-stu-id="ea764-170">This will issue hello command set as a series of PowerShell commands and create your Azure virtual machine.</span></span> <span data-ttu-id="ea764-171">Кроме того выполните команду hello, установка в интегрированной среде Сценариев PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ea764-171">Alternately, run hello command set in hello PowerShell ISE.</span></span>

<span data-ttu-id="ea764-172">Если вы собираетесь снова создать эту или подобную виртуальную машину, можно предпринять следующее:</span><span class="sxs-lookup"><span data-stu-id="ea764-172">If you will be creating this virtual machine again or a similar one, you can:</span></span>

* <span data-ttu-id="ea764-173">Сохраните этот набор команд как файл сценария PowerShell (PS1-файл).</span><span class="sxs-lookup"><span data-stu-id="ea764-173">Save this command set as a PowerShell script file (*.ps1).</span></span>
* <span data-ttu-id="ea764-174">Эта команда задать в качестве runbook службы автоматизации Azure в hello Сохранить **учетные записи автоматизации** раздел hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ea764-174">Save this command set as an Azure Automation runbook in hello **Automation Accounts** section of hello Azure portal.</span></span>

## <span data-ttu-id="ea764-175"><a id="examples"></a>Примеры</span><span class="sxs-lookup"><span data-stu-id="ea764-175"><a id="examples"></a>Examples</span></span>
<span data-ttu-id="ea764-176">Ниже приведены два примера использования hello уровня выше наборов команд Azure PowerShell toobuild, создаваемые на основе Windows Azure виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="ea764-176">Here are two examples of using hello steps above toobuild Azure PowerShell command sets that create Windows-based Azure virtual machines.</span></span>

### <a name="example-1"></a><span data-ttu-id="ea764-177">Пример 1</span><span class="sxs-lookup"><span data-stu-id="ea764-177">Example 1</span></span>
<span data-ttu-id="ea764-178">Требуется PowerShell команда задавать toocreate hello начальной виртуальную машину для контроллера домена Active Directory:</span><span class="sxs-lookup"><span data-stu-id="ea764-178">I need a PowerShell command set toocreate hello initial virtual machine for an Active Directory domain controller that:</span></span>

* <span data-ttu-id="ea764-179">Использует образ Windows Server 2012 R2 Datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="ea764-179">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="ea764-180">Имеет имя hello AZDC1.</span><span class="sxs-lookup"><span data-stu-id="ea764-180">Has hello name AZDC1.</span></span>
* <span data-ttu-id="ea764-181">является автономным компьютером;</span><span class="sxs-lookup"><span data-stu-id="ea764-181">Is a standalone computer.</span></span>
* <span data-ttu-id="ea764-182">имеет дополнительный диск данных объемом 20 ГБ;</span><span class="sxs-lookup"><span data-stu-id="ea764-182">Has an additional data disk of 20 GB.</span></span>
* <span data-ttu-id="ea764-183">Имеет статический IP-адрес hello 192.168.244.4.</span><span class="sxs-lookup"><span data-stu-id="ea764-183">Has hello static IP address 192.168.244.4.</span></span>
* <span data-ttu-id="ea764-184">Находится в подсети серверной hello hello AZDatacenter виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ea764-184">Is in hello BackEnd subnet of hello AZDatacenter virtual network.</span></span>
* <span data-ttu-id="ea764-185">— В облачной службе Azure TailspinToys hello.</span><span class="sxs-lookup"><span data-stu-id="ea764-185">Is in hello Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="ea764-186">Вот hello соответствующего Azure PowerShell команду set toocreate этой виртуальной машины с пустой строки между каждым разделом для удобства чтения.</span><span class="sxs-lookup"><span data-stu-id="ea764-186">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine, with blank lines between each block for readability.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

### <a name="example-2"></a><span data-ttu-id="ea764-187">Пример 2</span><span class="sxs-lookup"><span data-stu-id="ea764-187">Example 2</span></span>
<span data-ttu-id="ea764-188">Требуется PowerShell набора команд toocreate виртуальной машины для бизнес-сервера:</span><span class="sxs-lookup"><span data-stu-id="ea764-188">I need a PowerShell command set toocreate a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="ea764-189">Использует образ Windows Server 2012 R2 Datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="ea764-189">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="ea764-190">Имеет имя hello LOB1.</span><span class="sxs-lookup"><span data-stu-id="ea764-190">Has hello name LOB1.</span></span>
* <span data-ttu-id="ea764-191">Является членом домена corp.contoso.com hello.</span><span class="sxs-lookup"><span data-stu-id="ea764-191">Is a member of hello corp.contoso.com domain.</span></span>
* <span data-ttu-id="ea764-192">имеет дополнительный диск данных объемом 200 ГБ;</span><span class="sxs-lookup"><span data-stu-id="ea764-192">Has an additional data disk of 200 GB.</span></span>
* <span data-ttu-id="ea764-193">Возможности hello внешней подсети виртуальной сети AZDatacenter hello.</span><span class="sxs-lookup"><span data-stu-id="ea764-193">Is in hello FrontEnd subnet of hello AZDatacenter virtual network.</span></span>
* <span data-ttu-id="ea764-194">— В облачной службе Azure TailspinToys hello.</span><span class="sxs-lookup"><span data-stu-id="ea764-194">Is in hello Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="ea764-195">Вот hello соответствующего Azure PowerShell команду set toocreate этой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ea764-195">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="corp.contoso.com"
    $domacctdomain="CORP"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "FrontEnd"

    $disksize=200
    $disklabel="LOBData"
    $lun=0
    $hcaching="ReadWrite"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="next-steps"></a><span data-ttu-id="ea764-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ea764-196">Next steps</span></span>
<span data-ttu-id="ea764-197">Если потребуется диск ОС, не должен превышать 127 ГБ, вы можете [разверните диск hello ОС](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ea764-197">If you need an OS disk that is larger than 127 GB, you can [expand hello OS drive](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

