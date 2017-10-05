---
title: "Доменные службы Azure Active Directory: руководство по администрированию | Документация Майкрософт"
description: "Присоедините виртуальную машину Windows к управляемому домену, используя Azure PowerShell и классическую модель развертывания."
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
ms.openlocfilehash: 1bb1546fb616131a1e1868a0d0610c4cad5d73e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-windows-server-virtual-machine-to-a-managed-domain-using-powershell"></a><span data-ttu-id="38f9f-103">Присоединение виртуальной машины Windows Server к управляемому домену с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="38f9f-103">Join a Windows Server virtual machine to a managed domain using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="38f9f-104">Классический портал Azure — Windows</span><span class="sxs-lookup"><span data-stu-id="38f9f-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="38f9f-105">PowerShell — Windows</span><span class="sxs-lookup"><span data-stu-id="38f9f-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="38f9f-106">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="38f9f-106">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="38f9f-107">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="38f9f-107">This article covers using the classic deployment model.</span></span> <span data-ttu-id="38f9f-108">Сейчас доменные службы Azure AD не поддерживают модель Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="38f9f-108">Azure AD Domain Services does not currently support the Resource Manager model.</span></span>
>
>

<span data-ttu-id="38f9f-109">Ниже показано, как настроить набор команд Azure PowerShell для создания и предварительной настройки виртуальной машины Azure под управлением Windows, используя подход на базе стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="38f9f-109">These steps show you how to customize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="38f9f-110">Приведенные ниже шаги помогут создать виртуальную машину Azure под управлением Windows и присоединить ее к управляемому домену доменных служб Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38f9f-110">These steps help you build a Windows-based Azure virtual machine and join it to an Azure AD Domain Services managed domain.</span></span>

<span data-ttu-id="38f9f-111">Материал в этих шагах для создания наборов команд Azure PowerShell представлен таким образом, что достаточно лишь заполнить пробелы.</span><span class="sxs-lookup"><span data-stu-id="38f9f-111">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="38f9f-112">Это удобно, если вы не работали с PowerShell или хотите знать, какие именно значения отвечают за работоспособность конфигурации.</span><span class="sxs-lookup"><span data-stu-id="38f9f-112">This approach can be useful if you are new to PowerShell or you want to know what values to specify for successful configuration.</span></span> <span data-ttu-id="38f9f-113">Опытные пользователи PowerShell могут подставить в команды собственные значения для переменных (строки, начинающиеся со знака "$").</span><span class="sxs-lookup"><span data-stu-id="38f9f-113">Advanced PowerShell users can take the commands and substitute their own values for the variables (the lines beginning with "$").</span></span>

<span data-ttu-id="38f9f-114">Если вы еще не сделали этого, следуйте указаниям в разделе [Как установить и настроить Azure PowerShell](/powershell/azure/overview) , чтобы установить Azure PowerShell на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="38f9f-114">If you haven't done so already, use the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) to install Azure PowerShell on your local computer.</span></span> <span data-ttu-id="38f9f-115">Затем откройте командную строку Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="38f9f-115">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="38f9f-116">Шаг 1. Добавление учетной записи</span><span class="sxs-lookup"><span data-stu-id="38f9f-116">Step 1: Add your account</span></span>
1. <span data-ttu-id="38f9f-117">В командной строке PowerShell введите **Add-AzureAccount** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="38f9f-117">At the PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span>
2. <span data-ttu-id="38f9f-118">Введите адрес электронной почты, связанный с подпиской Azure, и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="38f9f-118">Type in the email address associated with your Azure subscription and click **Continue**.</span></span>
3. <span data-ttu-id="38f9f-119">Введите пароль к учетной записи.</span><span class="sxs-lookup"><span data-stu-id="38f9f-119">Type in the password for your account.</span></span>
4. <span data-ttu-id="38f9f-120">Щелкните **Войти**.</span><span class="sxs-lookup"><span data-stu-id="38f9f-120">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="38f9f-121">Шаг 2. Выбор подписки и учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="38f9f-121">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="38f9f-122">Укажите подписку Azure и учетную запись хранения, выполнив следующие команды в командной строке Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="38f9f-122">Set your Azure subscription and storage account by running these commands at the Windows PowerShell command prompt.</span></span> <span data-ttu-id="38f9f-123">Замените все содержимое внутри кавычек, включая знаки < и >, правильными именами.</span><span class="sxs-lookup"><span data-stu-id="38f9f-123">Replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="38f9f-124">Правильное имя подписки можно получить из свойства SubscriptionName в выходных данных команды **Get-AzureSubscription** .</span><span class="sxs-lookup"><span data-stu-id="38f9f-124">You can get the correct subscription name from the SubscriptionName property of the output of the **Get-AzureSubscription** command.</span></span> <span data-ttu-id="38f9f-125">Правильное имя учетной записи хранения можно получить из свойства Label в выходных данных команды **Get-AzureStorageAccount** после выполнения команды **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="38f9f-125">You can get the correct storage account name from the Label property of the output of the **Get-AzureStorageAccount** command after you run the **Select-AzureSubscription** command.</span></span>

## <a name="step-3-step-by-step-walkthrough---provision-the-virtual-machine-and-join-it-to-the-managed-domain"></a><span data-ttu-id="38f9f-126">Шаг 3. Пошаговое руководство — подготовка виртуальной машины и ее присоединение к управляемому домену</span><span class="sxs-lookup"><span data-stu-id="38f9f-126">Step 3: Step-by-step walkthrough - provision the virtual machine and join it to the managed domain</span></span>
<span data-ttu-id="38f9f-127">Вот соответствующий набор команд Azure PowerShell для создания такой виртуальной машины, в котором для удобства чтения между блоками вставлены пустые строки.</span><span class="sxs-lookup"><span data-stu-id="38f9f-127">Here is the corresponding Azure PowerShell command set to create this virtual machine, with blank lines between each block for readability.</span></span>

<span data-ttu-id="38f9f-128">Укажите сведения о подготавливаемой виртуальной машине Windows.</span><span class="sxs-lookup"><span data-stu-id="38f9f-128">Specify information about the Windows virtual machine to be provisioned.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

<span data-ttu-id="38f9f-129">Сведения о значениях InstanceSize для виртуальных машин серии D, DS или G см. в разделе [Размеры виртуальных машин и облачных служб для Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="38f9f-129">For the InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

<span data-ttu-id="38f9f-130">Предоставьте сведения об управляемом домене.</span><span class="sxs-lookup"><span data-stu-id="38f9f-130">Provide information about the managed domain.</span></span>

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

<span data-ttu-id="38f9f-131">Укажите имя облачной службы.</span><span class="sxs-lookup"><span data-stu-id="38f9f-131">Specify the name of the cloud service.</span></span>

    $svcname="Contoso100-test"

<span data-ttu-id="38f9f-132">Укажите имя виртуальной сети, к которой следует присоединить эту виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="38f9f-132">Specify the name of the virtual network to which the VM should be joined.</span></span> <span data-ttu-id="38f9f-133">Убедитесь, что управляемый домен доменных служб AAD доступен в этой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="38f9f-133">Ensure that the AAD-DS managed domain is available in this virtual network.</span></span>

    $vnetname="MyPreviewVnet"

<span data-ttu-id="38f9f-134">Выберите образ виртуальной машины, который будет использоваться для подготовки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="38f9f-134">Select the VM image to be used to provision the VM.</span></span>

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="38f9f-135">Настройте виртуальную машину — укажите ее имя, размер экземпляра и образ, который должен использоваться.</span><span class="sxs-lookup"><span data-stu-id="38f9f-135">Configure the VM - set VM name, instance size & image to be used.</span></span>

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="38f9f-136">Получите учетные данные локального администратора для этой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="38f9f-136">Obtain local administrator credentials for the VM.</span></span> <span data-ttu-id="38f9f-137">Укажите надежный пароль локального администратора.</span><span class="sxs-lookup"><span data-stu-id="38f9f-137">Choose a strong local administrator password.</span></span>

    $localadmincred=Get-Credential –Message "Type the name and password of the local administrator account."

<span data-ttu-id="38f9f-138">Получите учетные данные для учетной записи пользователя, относящейся к группе "Администраторы DC AAD", чтобы присоединить виртуальную машину к управляемому домену.</span><span class="sxs-lookup"><span data-stu-id="38f9f-138">Obtain credentials for a user account belonging to 'AAD DC Administrators' group to join VM to the managed domain.</span></span> <span data-ttu-id="38f9f-139">Не указывайте имя домена — например, в нашем примере в качестве имени пользователя мы указываем "bob".</span><span class="sxs-lookup"><span data-stu-id="38f9f-139">Do not specify the domain name - for instance, in our example, we specify 'bob' as the user name.</span></span>

    $domainadmincred=Get-Credential –Message "Now type the name (DO NOT INCLUDE THE DOMAIN) and password of an account in the AAD DC Administrators group, that has permission to add the machine to the domain."

<span data-ttu-id="38f9f-140">Настройте виртуальную машину — укажите требование присоединения к домену и необходимые учетные данные.</span><span class="sxs-lookup"><span data-stu-id="38f9f-140">Configure the VM - specify domain join requirement & required credentials.</span></span>

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="38f9f-141">Задайте подсеть для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="38f9f-141">Set a subnet for the VM.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

<span data-ttu-id="38f9f-142">Необязательно: укажите IP-адрес домена.</span><span class="sxs-lookup"><span data-stu-id="38f9f-142">Optional: Point to the IP address of the domain.</span></span> <span data-ttu-id="38f9f-143">Если в качестве IP-адресов управляемого домена доменных служб Azure AD используются DNS-серверы для виртуальной сети, этот шаг не требуется.</span><span class="sxs-lookup"><span data-stu-id="38f9f-143">If you set the IP addresses of the Azure AD Domain Services managed domain to be the DNS servers for the virtual network, this step is not required.</span></span>

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

<span data-ttu-id="38f9f-144">Теперь подготовьте присоединенную к домену виртуальную машину Windows.</span><span class="sxs-lookup"><span data-stu-id="38f9f-144">Now, provision the domain-joined Windows VM.</span></span>

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-to-provision-a-windows-vm-and-automatically-join-it-to-an-aad-domain-services-managed-domain"></a><span data-ttu-id="38f9f-145">Сценарий для подготовки виртуальной машины Windows и ее автоматического присоединения к управляемому домену доменных служб AAD</span><span class="sxs-lookup"><span data-stu-id="38f9f-145">Script to provision a Windows VM and automatically join it to an AAD Domain Services managed domain</span></span>
<span data-ttu-id="38f9f-146">Этот набор команд PowerShell создает виртуальную машину для бизнес-сервера со следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="38f9f-146">This PowerShell command set creates a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="38f9f-147">использует образ Windows Server 2012 R2 Datacenter;</span><span class="sxs-lookup"><span data-stu-id="38f9f-147">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="38f9f-148">имеет размер "очень малая";</span><span class="sxs-lookup"><span data-stu-id="38f9f-148">Is an extra small virtual machine.</span></span>
* <span data-ttu-id="38f9f-149">имеет имя Contoso100-test;</span><span class="sxs-lookup"><span data-stu-id="38f9f-149">Has the name Contoso100-test.</span></span>
* <span data-ttu-id="38f9f-150">является автоматически присоединяемой к управляемому домену contoso100;</span><span class="sxs-lookup"><span data-stu-id="38f9f-150">Is automatically domain joined to the contoso100 managed domain.</span></span>
* <span data-ttu-id="38f9f-151">добавляется в ту же виртуальную сеть, что и управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="38f9f-151">Is added to the same virtual network as the managed domain.</span></span>

<span data-ttu-id="38f9f-152">Ниже приведен полный пример сценария для создания виртуальной машины Windows и ее автоматического присоединения к управляемому домену доменных служб Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38f9f-152">Here is the full sample script to create the Windows virtual machine and automatically join it to the Azure AD Domain Services managed domain.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type the name and password of the local administrator account."

    $domainadmincred=Get-Credential –Message "Now type the name (not including the domain) and password of an account in the AAD DC Administrators group, that has permission to add the machine to the domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a><span data-ttu-id="38f9f-153">Похожий контент</span><span class="sxs-lookup"><span data-stu-id="38f9f-153">Related Content</span></span>
* [<span data-ttu-id="38f9f-154">Приступая к работе с доменными службами Azure AD</span><span class="sxs-lookup"><span data-stu-id="38f9f-154">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="38f9f-155">Administer an Azure AD Domain Services managed domain (Администрирование управляемого домена доменных служб Azure AD)</span><span class="sxs-lookup"><span data-stu-id="38f9f-155">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
