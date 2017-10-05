---
title: "Создание виртуальной машины Windows с помощью PowerShell | Документация Майкрософт"
description: "Создание виртуальных машин Windows с использованием Azure PowerShell и классической модели развертывания."
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
ms.openlocfilehash: 75c6cf17ee269ae169d9f2f748d0985ca07e454e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-the-classic-deployment-model"></a><span data-ttu-id="ada6e-103">Создание виртуальной машины Windows с использованием PowerShell и классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="ada6e-103">Create a Windows virtual machine with PowerShell and the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ada6e-104">Портал Azure — Windows</span><span class="sxs-lookup"><span data-stu-id="ada6e-104">Azure portal - Windows</span></span>](tutorial.md)
> * [<span data-ttu-id="ada6e-105">PowerShell — Windows</span><span class="sxs-lookup"><span data-stu-id="ada6e-105">PowerShell - Windows</span></span>](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> <span data-ttu-id="ada6e-106">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ada6e-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ada6e-107">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="ada6e-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="ada6e-108">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ada6e-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="ada6e-109">Узнайте, как [выполнить эти действия с помощью модели Resource Manager](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ada6e-109">Learn how to [perform these steps using the Resource Manager model](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="ada6e-110">Ниже показано, как настроить набор команд Azure PowerShell для создания и предварительной настройки виртуальной машины Azure под управлением Windows, используя подход на базе стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="ada6e-110">These steps show you how to customize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="ada6e-111">Этот процесс можно использовать для быстрого создания набора команд для новой виртуальной машины под управлением Windows и расширения существующего развертывания либо создания нескольких наборов команд, позволяющих быстро создать настраиваемую среду для разработки/тестирования или для ИТ-специалистов.</span><span class="sxs-lookup"><span data-stu-id="ada6e-111">You can use this process to quickly create a command set for a new Windows-based virtual machine and expand an existing deployment or to create multiple command sets that quickly build out a custom dev/test or IT pro environment.</span></span>

<span data-ttu-id="ada6e-112">Материал в этих шагах для создания наборов команд Azure PowerShell представлен таким образом, что достаточно лишь заполнить пробелы.</span><span class="sxs-lookup"><span data-stu-id="ada6e-112">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="ada6e-113">Этот подход может оказаться полезным, если вы не знакомы с PowerShell или хотите знать, какие именно значения следует задать для обеспечения работоспособности конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ada6e-113">This approach can be useful if you are new to PowerShell or you just want to know what values to specify for successful configuration.</span></span> <span data-ttu-id="ada6e-114">Опытные пользователи PowerShell могут подставить в команды собственные значения для переменных (строки, начинающиеся со знака "$").</span><span class="sxs-lookup"><span data-stu-id="ada6e-114">Advanced PowerShell users can take the commands and substitute their own values for the variables (the lines beginning with "$").</span></span>

<span data-ttu-id="ada6e-115">Если вы еще не сделали этого, следуйте указаниям в разделе [Как установить и настроить Azure PowerShell](/powershell/azure/overview) , чтобы установить Azure PowerShell на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="ada6e-115">If you haven't done so already, use the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) to install Azure PowerShell on your local computer.</span></span> <span data-ttu-id="ada6e-116">Затем откройте командную строку Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ada6e-116">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="ada6e-117">Шаг 1. Добавление учетной записи</span><span class="sxs-lookup"><span data-stu-id="ada6e-117">Step 1: Add your account</span></span>
1. <span data-ttu-id="ada6e-118">В командной строке PowerShell введите **Add-AzureAccount** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="ada6e-118">At the PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span> 
2. <span data-ttu-id="ada6e-119">Введите адрес электронной почты, связанный с подпиской Azure, и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="ada6e-119">Type in the email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="ada6e-120">Введите пароль к учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ada6e-120">Type in the password for your account.</span></span> 
4. <span data-ttu-id="ada6e-121">Щелкните **Войти**.</span><span class="sxs-lookup"><span data-stu-id="ada6e-121">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="ada6e-122">Шаг 2. Выбор подписки и учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="ada6e-122">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="ada6e-123">Укажите подписку Azure и учетную запись хранения, выполнив следующие команды в командной строке Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ada6e-123">Set your Azure subscription and storage account by running these commands at the Windows PowerShell command prompt.</span></span> <span data-ttu-id="ada6e-124">Замените все содержимое внутри кавычек, включая знаки < и >, правильными именами.</span><span class="sxs-lookup"><span data-stu-id="ada6e-124">Replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="ada6e-125">Правильное имя подписки можно получить из свойства SubscriptionName в выходных данных команды **Get-AzureSubscription** .</span><span class="sxs-lookup"><span data-stu-id="ada6e-125">You can get the correct subscription name from the SubscriptionName property of the output of the **Get-AzureSubscription** command.</span></span> <span data-ttu-id="ada6e-126">Правильное имя учетной записи хранения можно получить из свойства Label в выходных данных команды **Get-AzureStorageAccount** после выполнения команды **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="ada6e-126">You can get the correct storage account name from the Label property of the output of the **Get-AzureStorageAccount** command after you run the **Select-AzureSubscription** command.</span></span>

## <a name="step-3-determine-the-imagefamily"></a><span data-ttu-id="ada6e-127">Шаг 3. Определение ImageFamily</span><span class="sxs-lookup"><span data-stu-id="ada6e-127">Step 3: Determine the ImageFamily</span></span>
<span data-ttu-id="ada6e-128">Затем необходимо определить значение ImageFamily или Label для определенного образа, соответствующего создаваемой виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="ada6e-128">Next, you need to determine the ImageFamily or Label value for the specific image corresponding to the Azure virtual machine you want to create.</span></span> <span data-ttu-id="ada6e-129">Список доступных значений ImageFamily можно получить с помощью данной команды.</span><span class="sxs-lookup"><span data-stu-id="ada6e-129">You can get the list of available ImageFamily values with this command.</span></span>

    Get-AzureVMImage | select ImageFamily -Unique

<span data-ttu-id="ada6e-130">Ниже приведено несколько примеров значений ImageFamily для компьютеров под управлением Windows:</span><span class="sxs-lookup"><span data-stu-id="ada6e-130">Here are some examples of ImageFamily values for Windows-based computers:</span></span>

* <span data-ttu-id="ada6e-131">Центр обработки данных Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="ada6e-131">Windows Server 2012 R2 Datacenter</span></span>
* <span data-ttu-id="ada6e-132">Windows Server 2008 R2 с пакетом обновления 1</span><span class="sxs-lookup"><span data-stu-id="ada6e-132">Windows Server 2008 R2 SP1</span></span>
* <span data-ttu-id="ada6e-133">Windows Server 2016 Technical Preview 4</span><span class="sxs-lookup"><span data-stu-id="ada6e-133">Windows Server 2016 Technical Preview 4</span></span>
* <span data-ttu-id="ada6e-134">SQL Server 2012 SP1 Enterprise на базе Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="ada6e-134">SQL Server 2012 SP1 Enterprise on Windows Server 2012</span></span>

<span data-ttu-id="ada6e-135">Если вы нашли образ, который искали, откройте новый экземпляр любого текстового редактора или интегрированную среду сценариев PowerShell (ISE).</span><span class="sxs-lookup"><span data-stu-id="ada6e-135">If you find the image you are looking for, open a fresh instance of the text editor of your choice or the PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="ada6e-136">Скопируйте следующий текст в новый текстовый файл или среду PowerShell ISE, замещая значение ImageFamily.</span><span class="sxs-lookup"><span data-stu-id="ada6e-136">Copy the following into the new text file or the PowerShell ISE, substituting the ImageFamily value.</span></span>

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="ada6e-137">В некоторых случаях имя образа находится в свойстве Label, а не в значении ImageFamily.</span><span class="sxs-lookup"><span data-stu-id="ada6e-137">In some cases, the image name is in the Label property instead of the ImageFamily value.</span></span> <span data-ttu-id="ada6e-138">Если вы не нашли нужный образ с помощью свойства ImageFamily, отобразите список образов по свойству Label с помощью данной команды.</span><span class="sxs-lookup"><span data-stu-id="ada6e-138">If you didn't find the image that you are looking for using the ImageFamily property, list the images by their Label property with this command.</span></span>

    Get-AzureVMImage | select Label -Unique

<span data-ttu-id="ada6e-139">Если вы нашли нужный образ с помощью этой команды, откройте новый экземпляр любого текстового редактора или среду PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="ada6e-139">If you find the right image with this command, open a fresh instance of the text editor of your choice or the PowerShell ISE.</span></span> <span data-ttu-id="ada6e-140">Скопируйте следующий текст в новый текстовый файл или среду PowerShell ISE, замещая значение Label.</span><span class="sxs-lookup"><span data-stu-id="ada6e-140">Copy the following into the new text file or the PowerShell ISE, substituting the Label value.</span></span>

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a><span data-ttu-id="ada6e-141">Шаг 4. Создание своего набора команд</span><span class="sxs-lookup"><span data-stu-id="ada6e-141">Step 4: Build your command set</span></span>
<span data-ttu-id="ada6e-142">Сформируйте остальную часть набора команд. Для этого скопируйте соответствующий набор приведенных ниже блоков в новый текстовый файл или среду ISE, а затем подставьте значения переменных и удалите знаки < и >.</span><span class="sxs-lookup"><span data-stu-id="ada6e-142">Build the rest of your command set by copying the appropriate set of blocks below into your new text file or the ISE and then filling in the variable values and removing the < and > characters.</span></span> <span data-ttu-id="ada6e-143">Чтобы иметь представление о конечном результате, см. два [примера](#examples), приведенных в конце этой статьи.</span><span class="sxs-lookup"><span data-stu-id="ada6e-143">See the two [examples](#examples) at the end of this article for an idea of the final result.</span></span>

<span data-ttu-id="ada6e-144">Начните создавать свой набор команд, выбрав один из этих двух блоков команд (обязательно).</span><span class="sxs-lookup"><span data-stu-id="ada6e-144">Start your command set by choosing one of these two command blocks (required).</span></span>

<span data-ttu-id="ada6e-145">Вариант 1. Укажите имя и размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ada6e-145">Option 1: Specify a virtual machine name and a size.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="ada6e-146">Вариант 2. Укажите имя, размер, а также имя группы доступности.</span><span class="sxs-lookup"><span data-stu-id="ada6e-146">Option 2: Specify a name, size, and availability set name.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

<span data-ttu-id="ada6e-147">Сведения о значениях InstanceSize для виртуальных машин серии D, DS или G см. в разделе [Размеры виртуальных машин и облачных служб для Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="ada6e-147">For the InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="ada6e-148">Если у вас имеется соглашение Enterprise по программе Software Assurance и вы хотите воспользоваться [преимуществами гибридного использования](https://azure.microsoft.com/pricing/hybrid-use-benefit/) Windows Server, то добавьте параметр **-LicenseType** к командлету **New-AzureVMConfig**, чтобы передать значение **Windows_Server** для типичного варианта использования.</span><span class="sxs-lookup"><span data-stu-id="ada6e-148">If you have an Enterprise Agreement with Software Assurance, and intend to take advantage of the Windows Server [Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/), add the **-LicenseType** parameter to the **New-AzureVMConfig** cmdlet, passing the value **Windows_Server** for the typical use case.</span></span>  <span data-ttu-id="ada6e-149">Убедитесь, что используете переданный вами образ. Чтобы применить преимущества гибридного использования, стандартный образ из коллекции не подходит.</span><span class="sxs-lookup"><span data-stu-id="ada6e-149">Be sure you are using an image you have uploaded; you cannot use a standard image from the Gallery with the Hybrid Use Benefit.</span></span>
> 
> 

<span data-ttu-id="ada6e-150">При необходимости для автономного компьютера Windows укажите учетную запись локального администратора и пароль.</span><span class="sxs-lookup"><span data-stu-id="ada6e-150">Optionally, for a standalone Windows computer, specify the local administrator account and password.</span></span>

    $cred=Get-Credential -Message "Type the name and password of the local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

<span data-ttu-id="ada6e-151">Выберите надежный пароль.</span><span class="sxs-lookup"><span data-stu-id="ada6e-151">Choose a strong password.</span></span> <span data-ttu-id="ada6e-152">Чтобы проверить его надежность, см. раздел [Проверка надежности пароля. Использование надежных паролей](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span><span class="sxs-lookup"><span data-stu-id="ada6e-152">To check its strength, see [Password Checker: Using Strong Passwords](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span></span>

<span data-ttu-id="ada6e-153">Если потребуется добавить компьютер с Windows в существующий домен Active Directory, укажите учетную запись локального администратора и пароль, домен, а также имя и пароль учетной записи домена.</span><span class="sxs-lookup"><span data-stu-id="ada6e-153">Optionally, to add the Windows computer to an existing Active Directory domain, specify the local administrator account and password, the domain, and the name and password of a domain account.</span></span>

    $cred1=Get-Credential –Message "Type the name and password of the local administrator account."
    $cred2=Get-Credential –Message "Now type the name (not including the domain) and password of an account that has permission to add the machine to the domain."
    $domaindns="<FQDN of the domain that the machine is joining>"
    $domacctdomain="<domain of the account that has permission to add the machine to the domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="ada6e-154">Дополнительные параметры предварительной настройки для виртуальных машин под управлением Windows см. в описании синтаксиса для набора параметров **Windows** и **WindowsDomain** в [Add-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span><span class="sxs-lookup"><span data-stu-id="ada6e-154">For additional pre-configuration options for Windows-based virtual machines, see the syntax for the **Windows** and **WindowsDomain** parameter sets in [Add-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span></span>

<span data-ttu-id="ada6e-155">При необходимости назначьте виртуальной машине определенный IP-адрес, известный как статический выделенный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="ada6e-155">Optionally, assign the virtual machine a specific IP address, known as a static DIP.</span></span>

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

<span data-ttu-id="ada6e-156">Доступность определенного IP-адреса можно проверить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ada6e-156">You can verify that a specific IP address is available with:</span></span>

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

<span data-ttu-id="ada6e-157">При необходимости назначьте виртуальную машину определенной подсети в виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="ada6e-157">Optionally, assign the virtual machine to a specific subnet in an Azure virtual network.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "<name of the subnet>"

<span data-ttu-id="ada6e-158">При необходимости добавьте в виртуальную машину один диск данных.</span><span class="sxs-lookup"><span data-stu-id="ada6e-158">Optionally, add a single data disk to the virtual machine.</span></span>

    $disksize=<size of the disk in GB>
    $disklabel="<the label on the disk>"
    $lun=<Logical Unit Number (LUN) of the disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

<span data-ttu-id="ada6e-159">Для контроллера домена Active Directory установите в $hcaching значение "None".</span><span class="sxs-lookup"><span data-stu-id="ada6e-159">For an Active Directory domain controller, set $hcaching to "None".</span></span>

<span data-ttu-id="ada6e-160">При необходимости добавьте в виртуальную машину существующий сбалансированный по нагрузке набор для внешнего трафика.</span><span class="sxs-lookup"><span data-stu-id="ada6e-160">Optionally, add the virtual machine to an existing load-balanced set for external traffic.</span></span>

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of the internal port>
    $pubport=<port number of the external port>
    $endpointname="<name of the endpoint>"
    $lbsetname="<name of the existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

<span data-ttu-id="ada6e-161">И в завершение выберите один из обязательных блоков команд для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ada6e-161">Finally, choose one of these required command blocks for creating the virtual machine.</span></span>

<span data-ttu-id="ada6e-162">Вариант 1. Создайте виртуальную машину в существующей облачной службе.</span><span class="sxs-lookup"><span data-stu-id="ada6e-162">Option 1: Create the virtual machine in an existing cloud service.</span></span>

    New-AzureVM –ServiceName "<short name of the cloud service>" -VMs $vm1

<span data-ttu-id="ada6e-163">Короткое имя облачной службы — это то имя, которое отображается в списке облачных служб или в списке групп ресурсов на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ada6e-163">The short name of the cloud service is the name that appears in the list of Cloud Services in the Azure portal or in the list of Resource Groups in the Azure portal.</span></span>

<span data-ttu-id="ada6e-164">Вариант 2. Создайте виртуальную машину в существующей облачной службе и виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ada6e-164">Option 2: Create the virtual machine in an existing cloud service and virtual network.</span></span>

    $svcname="<short name of the cloud service>"
    $vnetname="<name of the virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a><span data-ttu-id="ada6e-165">Шаг 5. Запуск набора команд</span><span class="sxs-lookup"><span data-stu-id="ada6e-165">Step 5: Run your command set</span></span>
<span data-ttu-id="ada6e-166">Просмотрите в текстовом редакторе или среде PowerShell ISE созданный набор команд Azure PowerShell, состоящий из нескольких блоков команд из шага 4.</span><span class="sxs-lookup"><span data-stu-id="ada6e-166">Review the Azure PowerShell command set you built in your text editor or the PowerShell ISE consisting of multiple blocks of commands from step 4.</span></span> <span data-ttu-id="ada6e-167">Убедитесь, что указаны все необходимые переменные и что они имеют правильные значения.</span><span class="sxs-lookup"><span data-stu-id="ada6e-167">Ensure that you have specified all the needed variables and that they have the correct values.</span></span> <span data-ttu-id="ada6e-168">Убедитесь также, что удалены все знаки < и >.</span><span class="sxs-lookup"><span data-stu-id="ada6e-168">Also make sure that you have removed all the < and > characters.</span></span>

<span data-ttu-id="ada6e-169">Если вы используете текстовый редактор, скопируйте набор команд в буфер обмена и щелкните правой кнопкой мыши открытую командную строку Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ada6e-169">If you are using a text editor, copy the command set to the clipboard and then right-click your open Windows PowerShell command prompt.</span></span> <span data-ttu-id="ada6e-170">При этом набор команд выполняется в виде последовательности команд PowerShell, и создается виртуальная машина Azure.</span><span class="sxs-lookup"><span data-stu-id="ada6e-170">This will issue the command set as a series of PowerShell commands and create your Azure virtual machine.</span></span> <span data-ttu-id="ada6e-171">Или выполните набор команд в среде PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="ada6e-171">Alternately, run the command set in the PowerShell ISE.</span></span>

<span data-ttu-id="ada6e-172">Если вы собираетесь снова создать эту или подобную виртуальную машину, можно предпринять следующее:</span><span class="sxs-lookup"><span data-stu-id="ada6e-172">If you will be creating this virtual machine again or a similar one, you can:</span></span>

* <span data-ttu-id="ada6e-173">Сохраните этот набор команд как файл сценария PowerShell (PS1-файл).</span><span class="sxs-lookup"><span data-stu-id="ada6e-173">Save this command set as a PowerShell script file (*.ps1).</span></span>
* <span data-ttu-id="ada6e-174">Сохраните этот набор команд как Runbook службы автоматизации Azure в разделе **Учетные записи автоматизации** портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ada6e-174">Save this command set as an Azure Automation runbook in the **Automation Accounts** section of the Azure portal.</span></span>

## <span data-ttu-id="ada6e-175"><a id="examples"></a>Примеры</span><span class="sxs-lookup"><span data-stu-id="ada6e-175"><a id="examples"></a>Examples</span></span>
<span data-ttu-id="ada6e-176">Ниже приведено два примера применения описанных выше способов для создания наборов команд Azure PowerShell, создающих виртуальные машины под управлением Windows в Azure.</span><span class="sxs-lookup"><span data-stu-id="ada6e-176">Here are two examples of using the steps above to build Azure PowerShell command sets that create Windows-based Azure virtual machines.</span></span>

### <a name="example-1"></a><span data-ttu-id="ada6e-177">Пример 1</span><span class="sxs-lookup"><span data-stu-id="ada6e-177">Example 1</span></span>
<span data-ttu-id="ada6e-178">Мне требуется набор команд PowerShell для создания исходной виртуальной машины Linux для контроллера домена Active Directory, который:</span><span class="sxs-lookup"><span data-stu-id="ada6e-178">I need a PowerShell command set to create the initial virtual machine for an Active Directory domain controller that:</span></span>

* <span data-ttu-id="ada6e-179">использует образ Windows Server 2012 R2 Datacenter;</span><span class="sxs-lookup"><span data-stu-id="ada6e-179">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="ada6e-180">имеет имя AZDC1;</span><span class="sxs-lookup"><span data-stu-id="ada6e-180">Has the name AZDC1.</span></span>
* <span data-ttu-id="ada6e-181">является автономным компьютером;</span><span class="sxs-lookup"><span data-stu-id="ada6e-181">Is a standalone computer.</span></span>
* <span data-ttu-id="ada6e-182">имеет дополнительный диск данных объемом 20 ГБ;</span><span class="sxs-lookup"><span data-stu-id="ada6e-182">Has an additional data disk of 20 GB.</span></span>
* <span data-ttu-id="ada6e-183">имеет статический IP-адрес 192.168.244.4;</span><span class="sxs-lookup"><span data-stu-id="ada6e-183">Has the static IP address 192.168.244.4.</span></span>
* <span data-ttu-id="ada6e-184">находится в подсети BackEnd виртуальной сети AZDatacenter;</span><span class="sxs-lookup"><span data-stu-id="ada6e-184">Is in the BackEnd subnet of the AZDatacenter virtual network.</span></span>
* <span data-ttu-id="ada6e-185">находится в облачной службе Azure-TailspinToys.</span><span class="sxs-lookup"><span data-stu-id="ada6e-185">Is in the Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="ada6e-186">Вот соответствующий набор команд Azure PowerShell для создания такой виртуальной машины, в котором для удобства чтения между блоками вставлены пустые строки.</span><span class="sxs-lookup"><span data-stu-id="ada6e-186">Here is the corresponding Azure PowerShell command set to create this virtual machine, with blank lines between each block for readability.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type the name and password of the local administrator account."
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

### <a name="example-2"></a><span data-ttu-id="ada6e-187">Пример 2</span><span class="sxs-lookup"><span data-stu-id="ada6e-187">Example 2</span></span>
<span data-ttu-id="ada6e-188">Мне требуется набор команд PowerShell для создания виртуальной машины Linux для бизнес-сервера, который:</span><span class="sxs-lookup"><span data-stu-id="ada6e-188">I need a PowerShell command set to create a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="ada6e-189">использует образ Windows Server 2012 R2 Datacenter;</span><span class="sxs-lookup"><span data-stu-id="ada6e-189">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="ada6e-190">имеет имя LOB1;</span><span class="sxs-lookup"><span data-stu-id="ada6e-190">Has the name LOB1.</span></span>
* <span data-ttu-id="ada6e-191">является членом домена corp.contoso.com;</span><span class="sxs-lookup"><span data-stu-id="ada6e-191">Is a member of the corp.contoso.com domain.</span></span>
* <span data-ttu-id="ada6e-192">имеет дополнительный диск данных объемом 200 ГБ;</span><span class="sxs-lookup"><span data-stu-id="ada6e-192">Has an additional data disk of 200 GB.</span></span>
* <span data-ttu-id="ada6e-193">находится в подсети FrontEnd виртуальной сети AZDatacenter;</span><span class="sxs-lookup"><span data-stu-id="ada6e-193">Is in the FrontEnd subnet of the AZDatacenter virtual network.</span></span>
* <span data-ttu-id="ada6e-194">находится в облачной службе Azure-TailspinToys.</span><span class="sxs-lookup"><span data-stu-id="ada6e-194">Is in the Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="ada6e-195">Вот соответствующий набор команд Azure PowerShell для создания такой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ada6e-195">Here is the corresponding Azure PowerShell command set to create this virtual machine.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type the name and password of the local administrator account."
    $cred2=Get-Credential –Message "Now type the name (not including the domain) and password of an account that has permission to add the machine to the domain."
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


## <a name="next-steps"></a><span data-ttu-id="ada6e-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ada6e-196">Next steps</span></span>
<span data-ttu-id="ada6e-197">Если требуется диск ОС больше 127 ГБ, вы можете [расширить диск ОС](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ada6e-197">If you need an OS disk that is larger than 127 GB, you can [expand the OS drive](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

