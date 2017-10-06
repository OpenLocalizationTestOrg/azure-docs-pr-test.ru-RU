---
title: "Доменные службы Azure Active Directory: руководство по администрированию | Документация Майкрософт"
description: "Присоедините виртуальную машину tooa управляемого домена Windows с помощью Azure PowerShell и hello классической модели развертывания."
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9143b843-7327-43c3-baab-6e24a18db25e
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 21bc5930d84c5368a120f9d81f09320e2a0168fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain-using-powershell"></a><span data-ttu-id="a652c-103">К домену Windows Server виртуальной машины tooa управляемых с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a652c-103">Join a Windows Server virtual machine tooa managed domain using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a652c-104">Классический портал Azure — Windows</span><span class="sxs-lookup"><span data-stu-id="a652c-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="a652c-105">PowerShell — Windows</span><span class="sxs-lookup"><span data-stu-id="a652c-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="a652c-106">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a652c-106">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a652c-107">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="a652c-107">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="a652c-108">Доменные службы Azure AD в настоящее время не поддерживает модель диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="a652c-108">Azure AD Domain Services does not currently support hello Resource Manager model.</span></span>
>
>

<span data-ttu-id="a652c-109">Следующие шаги показывают, как toocustomize набор Azure PowerShell команды, создание и предварительная настройка виртуальной машины на основе Windows Azure, используя подход стандартного блока.</span><span class="sxs-lookup"><span data-stu-id="a652c-109">These steps show you how toocustomize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="a652c-110">Эти шаги помогут выполнить виртуальной машины на основе Windows Azure и присоединить ее управляемый домен tooan доменные службы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a652c-110">These steps help you build a Windows-based Azure virtual machine and join it tooan Azure AD Domain Services managed domain.</span></span>

<span data-ttu-id="a652c-111">Материал в этих шагах для создания наборов команд Azure PowerShell представлен таким образом, что достаточно лишь заполнить пробелы.</span><span class="sxs-lookup"><span data-stu-id="a652c-111">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="a652c-112">Этот подход может оказаться полезным, если вы являетесь новый tooPowerShell или требуется tooknow toospecify какие значения для успешной настройки.</span><span class="sxs-lookup"><span data-stu-id="a652c-112">This approach can be useful if you are new tooPowerShell or you want tooknow what values toospecify for successful configuration.</span></span> <span data-ttu-id="a652c-113">Опытные пользователи PowerShell можно воспользоваться командами hello и подставьте собственные значения для переменных hello (hello строки, начинающиеся с «$»).</span><span class="sxs-lookup"><span data-stu-id="a652c-113">Advanced PowerShell users can take hello commands and substitute their own values for hello variables (hello lines beginning with "$").</span></span>

<span data-ttu-id="a652c-114">Если вы еще не сделали этого, используйте инструкции hello в [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="a652c-114">If you haven't done so already, use hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell on your local computer.</span></span> <span data-ttu-id="a652c-115">Затем откройте командную строку Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a652c-115">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="a652c-116">Шаг 1. Добавление учетной записи</span><span class="sxs-lookup"><span data-stu-id="a652c-116">Step 1: Add your account</span></span>
1. <span data-ttu-id="a652c-117">Введите в командной строке PowerShell hello **Add-AzureAccount** и нажмите кнопку **ввод**.</span><span class="sxs-lookup"><span data-stu-id="a652c-117">At hello PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span>
2. <span data-ttu-id="a652c-118">Введите адрес электронной почты hello, связанных с подпиской Azure и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="a652c-118">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span>
3. <span data-ttu-id="a652c-119">Введите в hello пароль своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a652c-119">Type in hello password for your account.</span></span>
4. <span data-ttu-id="a652c-120">Щелкните **Войти**.</span><span class="sxs-lookup"><span data-stu-id="a652c-120">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="a652c-121">Шаг 2. Выбор подписки и учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="a652c-121">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="a652c-122">Задайте подписка Azure и учетной записи хранилища, выполнив следующие команды в командной строке Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="a652c-122">Set your Azure subscription and storage account by running these commands at hello Windows PowerShell command prompt.</span></span> <span data-ttu-id="a652c-123">Замените все содержимое в кавычках hello, включая hello < и > символы, правильные имена hello.</span><span class="sxs-lookup"><span data-stu-id="a652c-123">Replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="a652c-124">Hello правильное имя подписки можно получить из hello свойство Имя_подписки выходной hello hello **Get-AzureSubscription** команды.</span><span class="sxs-lookup"><span data-stu-id="a652c-124">You can get hello correct subscription name from hello SubscriptionName property of hello output of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="a652c-125">Можно получить имя учетной записи хранения правильно hello hello свойства Label выходные данные hello hello **Get AzureStorageAccount** команду после запуска hello **Select-AzureSubscription** команды.</span><span class="sxs-lookup"><span data-stu-id="a652c-125">You can get hello correct storage account name from hello Label property of hello output of hello **Get-AzureStorageAccount** command after you run hello **Select-AzureSubscription** command.</span></span>

## <a name="step-3-step-by-step-walkthrough---provision-hello-virtual-machine-and-join-it-toohello-managed-domain"></a><span data-ttu-id="a652c-126">Шаг 3: Пошаговое руководство - подготовки виртуальной машины hello и присоедините его toohello управляемого домена</span><span class="sxs-lookup"><span data-stu-id="a652c-126">Step 3: Step-by-step walkthrough - provision hello virtual machine and join it toohello managed domain</span></span>
<span data-ttu-id="a652c-127">Вот hello соответствующего Azure PowerShell команду set toocreate этой виртуальной машины с пустой строки между каждым разделом для удобства чтения.</span><span class="sxs-lookup"><span data-stu-id="a652c-127">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine, with blank lines between each block for readability.</span></span>

<span data-ttu-id="a652c-128">Укажите сведения о подготовки виртуальной машины toobe с Windows hello.</span><span class="sxs-lookup"><span data-stu-id="a652c-128">Specify information about hello Windows virtual machine toobe provisioned.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

<span data-ttu-id="a652c-129">Hello InstanceSize значения для D-, DS- или виртуальные машины серии G см [виртуальной машины размеры и облачных служб для Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="a652c-129">For hello InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

<span data-ttu-id="a652c-130">Приводятся сведения о hello управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="a652c-130">Provide information about hello managed domain.</span></span>

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

<span data-ttu-id="a652c-131">Укажите имя hello hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="a652c-131">Specify hello name of hello cloud service.</span></span>

    $svcname="Contoso100-test"

<span data-ttu-id="a652c-132">Укажите имя hello toowhich hello hello виртуальной сети, должны быть присоединены к виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="a652c-132">Specify hello name of hello virtual network toowhich hello VM should be joined.</span></span> <span data-ttu-id="a652c-133">Убедитесь, hello AAD-управляемого домена в этой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a652c-133">Ensure that hello AAD-DS managed domain is available in this virtual network.</span></span>

    $vnetname="MyPreviewVnet"

<span data-ttu-id="a652c-134">Toobe образ виртуальной Машины выберите hello используется tooprovision hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a652c-134">Select hello VM image toobe used tooprovision hello VM.</span></span>

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="a652c-135">Настройка виртуальной Машины — имя набора ВМ, hello экземпляр размер & изображения toobe используется.</span><span class="sxs-lookup"><span data-stu-id="a652c-135">Configure hello VM - set VM name, instance size & image toobe used.</span></span>

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="a652c-136">Получите учетные данные локального администратора для hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a652c-136">Obtain local administrator credentials for hello VM.</span></span> <span data-ttu-id="a652c-137">Укажите надежный пароль локального администратора.</span><span class="sxs-lookup"><span data-stu-id="a652c-137">Choose a strong local administrator password.</span></span>

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

<span data-ttu-id="a652c-138">Получите учетные данные для учетной записи пользователя, принадлежащий too'AAD контроллера домена Администраторы группы toojoin ВМ toohello управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="a652c-138">Obtain credentials for a user account belonging too'AAD DC Administrators' group toojoin VM toohello managed domain.</span></span> <span data-ttu-id="a652c-139">Не указывайте hello имя домена — как имя пользователя hello для экземпляра, в нашем примере мы указываем «bob».</span><span class="sxs-lookup"><span data-stu-id="a652c-139">Do not specify hello domain name - for instance, in our example, we specify 'bob' as hello user name.</span></span>

    $domainadmincred=Get-Credential –Message "Now type hello name (DO NOT INCLUDE hello DOMAIN) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

<span data-ttu-id="a652c-140">Настройка виртуальной Машины hello - указать требования к соединения домена и необходимые учетные данные.</span><span class="sxs-lookup"><span data-stu-id="a652c-140">Configure hello VM - specify domain join requirement & required credentials.</span></span>

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="a652c-141">Задайте подсеть для hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a652c-141">Set a subnet for hello VM.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

<span data-ttu-id="a652c-142">Необязательно: Точка toohello IP-адрес домена hello.</span><span class="sxs-lookup"><span data-stu-id="a652c-142">Optional: Point toohello IP address of hello domain.</span></span> <span data-ttu-id="a652c-143">Если значение hello toobe управляемого домена доменные службы Azure AD hello hello IP-адреса DNS-серверов для виртуальной сети hello, этот шаг не требуется.</span><span class="sxs-lookup"><span data-stu-id="a652c-143">If you set hello IP addresses of hello Azure AD Domain Services managed domain toobe hello DNS servers for hello virtual network, this step is not required.</span></span>

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

<span data-ttu-id="a652c-144">Теперь hello подготовки присоединенных к домену Windows виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a652c-144">Now, provision hello domain-joined Windows VM.</span></span>

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-tooprovision-a-windows-vm-and-automatically-join-it-tooan-aad-domain-services-managed-domain"></a><span data-ttu-id="a652c-145">Сценарий tooprovision виртуальной Машины Windows и автоматически присоединить управляемого домена tooan AAD доменных служб</span><span class="sxs-lookup"><span data-stu-id="a652c-145">Script tooprovision a Windows VM and automatically join it tooan AAD Domain Services managed domain</span></span>
<span data-ttu-id="a652c-146">Этот набор команд PowerShell создает виртуальную машину для бизнес-сервера со следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="a652c-146">This PowerShell command set creates a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="a652c-147">Использует образ Windows Server 2012 R2 Datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="a652c-147">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="a652c-148">имеет размер "очень малая";</span><span class="sxs-lookup"><span data-stu-id="a652c-148">Is an extra small virtual machine.</span></span>
* <span data-ttu-id="a652c-149">Имеет имя hello Contoso100 теста.</span><span class="sxs-lookup"><span data-stu-id="a652c-149">Has hello name Contoso100-test.</span></span>
* <span data-ttu-id="a652c-150">— Автоматически домена присоединены к домену toohello contoso100 управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="a652c-150">Is automatically domain joined toohello contoso100 managed domain.</span></span>
* <span data-ttu-id="a652c-151">Добавляется toohello же виртуальной сети hello управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="a652c-151">Is added toohello same virtual network as hello managed domain.</span></span>

<span data-ttu-id="a652c-152">Ниже приведен полный пример скрипта toocreate hello на виртуальной машине Windows hello и автоматически присоединить управляемого домена toohello доменные службы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a652c-152">Here is hello full sample script toocreate hello Windows virtual machine and automatically join it toohello Azure AD Domain Services managed domain.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

    $domainadmincred=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a><span data-ttu-id="a652c-153">Похожий контент</span><span class="sxs-lookup"><span data-stu-id="a652c-153">Related Content</span></span>
* [<span data-ttu-id="a652c-154">Приступая к работе с доменными службами Azure AD</span><span class="sxs-lookup"><span data-stu-id="a652c-154">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="a652c-155">Administer an Azure AD Domain Services managed domain (Администрирование управляемого домена доменных служб Azure AD)</span><span class="sxs-lookup"><span data-stu-id="a652c-155">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
