---
title: "aaaReplicate виртуальных машин Hyper-V с помощью PowerShell и диспетчера ресурсов Azure | Документы Microsoft"
description: "Автоматизация hello репликации tooAzure виртуальных машин Hyper-V с помощью PowerShell и диспетчера ресурсов Azure в Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="4e517-103">Репликация между локальными виртуальными машинами Hyper-V и Azure с помощью PowerShell и Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4e517-103">Replicate between on-premises Hyper-V virtual machines and Azure by using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4e517-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="4e517-104">Azure Portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="4e517-105">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4e517-105">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
> * [<span data-ttu-id="4e517-106">Классический портал</span><span class="sxs-lookup"><span data-stu-id="4e517-106">Classic Portal</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a><span data-ttu-id="4e517-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="4e517-107">Overview</span></span>
<span data-ttu-id="4e517-108">Azure Site Recovery поддерживает tooyour бизнес-непрерывности и аварийного восстановления стратегии, управляя операциями репликации, отработки отказа и восстановления виртуальных машин в различных вариантов развертывания.</span><span class="sxs-lookup"><span data-stu-id="4e517-108">Azure Site Recovery contributes tooyour business continuity and disaster recovery strategy by orchestrating replication, failover, and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="4e517-109">Полный список сценариев развертывания см. в разделе hello [Обзор Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4e517-109">For a full list of deployment scenarios, see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="4e517-110">Azure PowerShell — это модуль, предоставляет toomanage командлеты Azure через Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e517-110">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="4e517-111">Он может работать с двумя типами модулей: hello Azure профиля модуля или hello модуль диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="4e517-111">It can work with two types of modules: hello Azure Profile module, or hello Azure Resource Manager module.</span></span>

<span data-ttu-id="4e517-112">Командлеты PowerShell для службы Site Recovery, доступные в Azure PowerShell для диспетчера ресурсов Azure, позволяют обеспечить защиту и выполнить восстановление серверов в Azure.</span><span class="sxs-lookup"><span data-stu-id="4e517-112">Site Recovery PowerShell cmdlets, available with Azure PowerShell for Azure Resource Manager, help you protect and recover your servers in Azure.</span></span>

<span data-ttu-id="4e517-113">В этой статье описывается как toouse Windows PowerShell, вместе с Azure Resource Manager, tooconfigure toodeploy Site Recovery и управлять tooAzure защиты сервера.</span><span class="sxs-lookup"><span data-stu-id="4e517-113">This article describes how toouse Windows PowerShell, together with Azure Resource Manager, toodeploy Site Recovery tooconfigure and orchestrate server protection tooAzure.</span></span> <span data-ttu-id="4e517-114">пример Hello, используемые в этой статье показано, как tooprotect, отработки отказа и восстановления виртуальных машин на tooAzure узла Hyper-V, с помощью Azure PowerShell с помощью диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="4e517-114">hello example used in this article shows you how tooprotect, fail over, and recover virtual machines on a Hyper-V host tooAzure, by using Azure PowerShell with Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="4e517-115">Hello командлеты PowerShell восстановления сайта в настоящее время позволяют hello tooconfigure следующие: один tooanother сайта диспетчера виртуальных машин, tooAzure сайта диспетчера виртуальных машин и tooAzure узла Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="4e517-115">hello Site Recovery PowerShell cmdlets currently allow you tooconfigure hello following: one Virtual Machine Manager site tooanother, a Virtual Machine Manager site tooAzure, and a Hyper-V site tooAzure.</span></span>
>
>

<span data-ttu-id="4e517-116">Не требуется toobe toouse expert PowerShell в этой статье, но вам нужен toounderstand hello основные понятия, например модули, командлеты и сеансов.</span><span class="sxs-lookup"><span data-stu-id="4e517-116">You don't need toobe a PowerShell expert toouse this article, but you do need toounderstand hello basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="4e517-117">Дополнительные сведения о Windows PowerShell можно найти в разделе [Начало работы с Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e517-117">For more information about Windows PowerShell, see [Getting Started with Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="4e517-118">Дополнительные сведения см. также в статье [Использование Azure PowerShell с Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="4e517-118">You can also read more about [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4e517-119">Партнеры корпорации Майкрософт, которые являются частью программы hello поставщика облачных решений (CSP) можно настроить и управлять защиты серверов, клиентов; tootheir клиентов соответствующих CSP подписки (клиента).</span><span class="sxs-lookup"><span data-stu-id="4e517-119">Microsoft partners that are part of hello Cloud Solution Provider (CSP) program can configure and manage protection of their customers' servers tootheir customers' respective CSP subscriptions (tenant subscriptions).</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="4e517-120">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="4e517-120">Before you start</span></span>
<span data-ttu-id="4e517-121">Убедитесь, что выполнены следующие предварительные требования.</span><span class="sxs-lookup"><span data-stu-id="4e517-121">Make sure you have these prerequisites in place:</span></span>

* <span data-ttu-id="4e517-122">Учетная запись [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="4e517-122">A [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="4e517-123">Начните с [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4e517-123">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="4e517-124">Также вы можете ознакомиться с [расценками на использование менеджера Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="4e517-124">In addition, you can read about [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="4e517-125">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="4e517-125">Azure PowerShell 1.0.</span></span> <span data-ttu-id="4e517-126">Дополнительные сведения об этом выпуске и как tooinstall, в разделе [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="4e517-126">For information about this release and how tooinstall it, see [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span></span>
* <span data-ttu-id="4e517-127">Hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) и [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) модулей.</span><span class="sxs-lookup"><span data-stu-id="4e517-127">hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) and [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span></span> <span data-ttu-id="4e517-128">Можно получить последние версии этих модулей hello hello [коллекции PowerShell](https://www.powershellgallery.com/)</span><span class="sxs-lookup"><span data-stu-id="4e517-128">You can get hello latest versions of these modules from hello [PowerShell gallery](https://www.powershellgallery.com/)</span></span>

<span data-ttu-id="4e517-129">В этой статье показано, как toouse Azure Powershell с tooconfigure диспетчера ресурсов Azure и управление ими защиты серверов.</span><span class="sxs-lookup"><span data-stu-id="4e517-129">This article illustrates how toouse Azure Powershell with Azure Resource Manager tooconfigure and manage protection of your servers.</span></span> <span data-ttu-id="4e517-130">пример Hello, используемые в этой статье показано, как tooprotect виртуальной машины, работающей на узле Hyper-V, tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4e517-130">hello example used in this article shows you how tooprotect a virtual machine, running on a Hyper-V host, tooAzure.</span></span> <span data-ttu-id="4e517-131">Hello следующие необходимые условия — пример определенного toothis.</span><span class="sxs-lookup"><span data-stu-id="4e517-131">hello following prerequisites are specific toothis example.</span></span> <span data-ttu-id="4e517-132">Более широкий набор требований для hello различные сценарии восстановления сайта, см. документации toohello относится toothat сценария.</span><span class="sxs-lookup"><span data-stu-id="4e517-132">For a more comprehensive set of requirements for hello various Site Recovery scenarios, refer toohello documentation pertaining toothat scenario.</span></span>

* <span data-ttu-id="4e517-133">Узел Hyper-V под управлением Windows Server 2012 R2 или Microsoft Hyper-V Server 2012 R2, содержащий одну или несколько виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="4e517-133">A Hyper-V host running Windows Server 2012 R2 or Microsoft Hyper-V Server 2012 R2 containing one or more virtual machines.</span></span>
* <span data-ttu-id="4e517-134">Серверы Hyper-V подключен toohello Интернет, напрямую или через прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="4e517-134">Hyper-V servers connected toohello Internet, either directly or through a proxy.</span></span>
* <span data-ttu-id="4e517-135">Hello требуется tooprotect виртуальные машины должны соответствовать [требования виртуальной машины](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="4e517-135">hello virtual machines you want tooprotect should conform with [Virtual Machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

## <a name="step-1-sign-in-tooyour-azure-account"></a><span data-ttu-id="4e517-136">Шаг 1: Войдите в учетную запись Azure tooyour</span><span class="sxs-lookup"><span data-stu-id="4e517-136">Step 1: Sign in tooyour Azure account</span></span>
1. <span data-ttu-id="4e517-137">Откройте консоль PowerShell и выполнения этой команды toosign в tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="4e517-137">Open a PowerShell console and run this command toosign in tooyour Azure account.</span></span> <span data-ttu-id="4e517-138">командлет Hello вызов веб-страницы, которое предложит ввести учетные данные учетной записи.</span><span class="sxs-lookup"><span data-stu-id="4e517-138">hello cmdlet brings up a web page that will prompt you for your account credentials.</span></span>

        Login-AzureRmAccount

    <span data-ttu-id="4e517-139">Кроме того, также может включать учетные данные учетной записи toohello параметр `Login-AzureRmAccount` командлет с помощью hello `-Credential` параметра.</span><span class="sxs-lookup"><span data-stu-id="4e517-139">Alternately, you could also include your account credentials as a parameter toohello `Login-AzureRmAccount` cmdlet, by using hello `-Credential` parameter.</span></span>

    <span data-ttu-id="4e517-140">Если партнер CSP работе от имени клиента, укажите hello клиента как клиента, с помощью имени основного домена tenantID или клиента.</span><span class="sxs-lookup"><span data-stu-id="4e517-140">If you are CSP partner working on behalf of a tenant, specify hello customer as a tenant, by using their tenantID or tenant primary domain name.</span></span>

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. <span data-ttu-id="4e517-141">Учетной записи может иметь несколько подписок, следует связывать hello подписку toouse с учетной записью hello.</span><span class="sxs-lookup"><span data-stu-id="4e517-141">An account can have several subscriptions, so you should associate hello subscription you want toouse with hello account.</span></span>

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. <span data-ttu-id="4e517-142">Убедитесь, что подписки зарегистрированных toouse hello Azure поставщиков для служб восстановления и восстановления сайта с помощью hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="4e517-142">Verify that your subscription is registered toouse hello Azure providers for Recovery Services and Site Recovery, by using hello following commands:</span></span>

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   <span data-ttu-id="4e517-143">В выходные данные этих команд, если hello hello **RegistrationState** задано слишком**зарегистрированные**, можно продолжить tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="4e517-143">In hello output of these commands, if hello **RegistrationState** is set too**Registered**, you can proceed tooStep 2.</span></span> <span data-ttu-id="4e517-144">В противном случае необходимо зарегистрировать поставщик отсутствует hello в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="4e517-144">If not, you should register hello missing provider in your subscription.</span></span>

   <span data-ttu-id="4e517-145">tooregister hello поставщика Azure Site Recovery и службы восстановления, запустите hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="4e517-145">tooregister hello Azure provider for Site Recovery and Recovery Services, run hello following commands:</span></span>

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   <span data-ttu-id="4e517-146">Убедитесь, что поставщики hello успешно зарегистрирован с помощью следующих команд hello: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` и `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span><span class="sxs-lookup"><span data-stu-id="4e517-146">Verify that hello providers registered successfully by using hello following commands: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` and `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span></span>

## <a name="step-2-set-up-hello-recovery-services-vault"></a><span data-ttu-id="4e517-147">Шаг 2: Настройка hello в хранилище службы восстановления</span><span class="sxs-lookup"><span data-stu-id="4e517-147">Step 2: Set up hello Recovery Services vault</span></span>
1. <span data-ttu-id="4e517-148">Создайте группу ресурсов диспетчера ресурсов Azure, в котором будет создание хранилища hello, или используйте существующую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4e517-148">Create an Azure Resource Manager resource group in which you'll create hello vault, or use an existing resource group.</span></span> <span data-ttu-id="4e517-149">Можно создать новую группу ресурсов с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4e517-149">You can create a new resource group by using hello following command:</span></span>

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    <span data-ttu-id="4e517-150">где hello $ResourceGroupName переменной содержит hello имя группы ресурсов hello требуется toocreate и hello $Geo переменная содержит hello Azure регион, в какую группу ресурсов hello toocreate (например, «Юг Бразилии»).</span><span class="sxs-lookup"><span data-stu-id="4e517-150">where hello $ResourceGroupName variable contains hello name of hello resource group you want toocreate, and hello $Geo variable contains hello Azure region in which toocreate hello resource group (for example, "Brazil South").</span></span>

    <span data-ttu-id="4e517-151">Список групп ресурсов в подписке можно получить с помощью hello `Get-AzureRmResourceGroup` командлета.</span><span class="sxs-lookup"><span data-stu-id="4e517-151">You can obtain a list of resource groups in your subscription by using hello `Get-AzureRmResourceGroup` cmdlet.</span></span>
2. <span data-ttu-id="4e517-152">Создайте хранилище служб восстановления Azure следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4e517-152">Create a new Azure Recovery Services vault as follows:</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    <span data-ttu-id="4e517-153">Список существующих хранилищ можно получить с помощью hello `Get-AzureRmRecoveryServicesVault` командлета.</span><span class="sxs-lookup"><span data-stu-id="4e517-153">You can retrieve a list of existing vaults by using hello `Get-AzureRmRecoveryServicesVault` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="4e517-154">Если вы хотите tooperform операции восстановления сайта хранилищ, созданные с помощью классического портала hello или модуля Azure Service Management PowerShell hello, список таких хранилищ можно получить с помощью hello `Get-AzureRmSiteRecoveryVault` командлета.</span><span class="sxs-lookup"><span data-stu-id="4e517-154">If you wish tooperform operations on Site Recovery vaults created using hello classic portal or hello Azure Service Management PowerShell module, you can retrieve a list of such vaults by using hello `Get-AzureRmSiteRecoveryVault` cmdlet.</span></span> <span data-ttu-id="4e517-155">Для каждой новой операции рекомендуется создавать отдельное хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="4e517-155">You should create a new Recovery Services vault for all new operations.</span></span> <span data-ttu-id="4e517-156">Hello хранилищ Site Recovery, ранее созданную поддерживаются, но у вас нет новейших функций hello.</span><span class="sxs-lookup"><span data-stu-id="4e517-156">hello Site Recovery vaults you've created earlier are supported, but don't have hello latest features.</span></span>
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="4e517-157">Шаг 3: Настройка hello контекст хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="4e517-157">Step 3: Set hello Recovery Services vault context</span></span>
1. <span data-ttu-id="4e517-158">Задайте контекст хранилища hello, выполнив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4e517-158">Set hello vault context by running hello following command:</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a><span data-ttu-id="4e517-159">Шаг 4: Создание узла Hyper-V и создание нового ключа регистрации хранилища для узла hello.</span><span class="sxs-lookup"><span data-stu-id="4e517-159">Step 4: Create a Hyper-V site and generate a new vault registration key for hello site.</span></span>
1. <span data-ttu-id="4e517-160">Создайте сайт Hyper-V следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4e517-160">Create a new Hyper-V site as follows:</span></span>

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    <span data-ttu-id="4e517-161">Этот командлет запускает узел hello toocreate задания Site Recovery и возвращает объект задания Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="4e517-161">This cmdlet starts a Site Recovery job toocreate hello site, and returns a Site Recovery job object.</span></span> <span data-ttu-id="4e517-162">Дождитесь toocomplete задания hello и убедитесь в успешном завершении задания hello.</span><span class="sxs-lookup"><span data-stu-id="4e517-162">Wait for hello job toocomplete and verify that hello job completed successfully.</span></span>

    <span data-ttu-id="4e517-163">Можно получить объект задания hello и тем самым проверьте hello текущее состояние задания hello, с помощью командлета Get-AzureRmSiteRecoveryJob hello.</span><span class="sxs-lookup"><span data-stu-id="4e517-163">You can retrieve hello job object, and thereby check hello current status of hello job, by using hello Get-AzureRmSiteRecoveryJob cmdlet.</span></span>
2. <span data-ttu-id="4e517-164">Создать и скачать ключ регистрации для сайта hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4e517-164">Generate and download a registration key for hello site, as follows:</span></span>

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    <span data-ttu-id="4e517-165">Копировать hello загружаются узла ключа toohello Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="4e517-165">Copy hello downloaded key toohello Hyper-V host.</span></span> <span data-ttu-id="4e517-166">Вам также потребуется hello ключа tooregister hello Hyper-V узла toohello сайт.</span><span class="sxs-lookup"><span data-stu-id="4e517-166">You need hello key tooregister hello Hyper-V host toohello site.</span></span>

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a><span data-ttu-id="4e517-167">Шаг 5: Установка поставщика Azure Site Recovery hello и агента служб восстановления Azure на узле Hyper-V</span><span class="sxs-lookup"><span data-stu-id="4e517-167">Step 5: Install hello Azure Site Recovery provider and Azure Recovery Services Agent on your Hyper-V host</span></span>
1. <span data-ttu-id="4e517-168">Загрузить установщик hello hello последнюю версию поставщика hello из [Microsoft](https://aka.ms/downloaddra).</span><span class="sxs-lookup"><span data-stu-id="4e517-168">Download hello installer for hello latest version of hello provider from [Microsoft](https://aka.ms/downloaddra).</span></span>
2. <span data-ttu-id="4e517-169">Установщик выполнения hello на узле Hyper-V и в конце hello hello установки по-прежнему toohello этап регистрации.</span><span class="sxs-lookup"><span data-stu-id="4e517-169">Run hello installer on your Hyper-V host, and at hello end of hello installation continue toohello registration step.</span></span>
3. <span data-ttu-id="4e517-170">При появлении запроса предоставляют hello скачать ключ регистрации узла и выполнить регистрацию узла toohello hello Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="4e517-170">When prompted, provide hello downloaded site registration key, and complete registration of hello Hyper-V host toohello site.</span></span>
4. <span data-ttu-id="4e517-171">Убедитесь, что зарегистрированные toohello сайта, на которых размещены hello Hyper-V с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4e517-171">Verify that hello Hyper-V host is registered toohello site by using hello following command:</span></span>

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a><span data-ttu-id="4e517-172">Шаг 6: Создайте политику репликации и связать его с контейнера защиты hello</span><span class="sxs-lookup"><span data-stu-id="4e517-172">Step 6: Create a replication policy and associate it with hello protection container</span></span>
1. <span data-ttu-id="4e517-173">Создайте политику репликации, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4e517-173">Create a replication policy as follows:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    <span data-ttu-id="4e517-174">Проверка hello вернул tooensure задания успешное создание политики репликации hello.</span><span class="sxs-lookup"><span data-stu-id="4e517-174">Check hello returned job tooensure that hello replication policy creation succeeds.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4e517-175">Hello указанную учетную запись хранения должна быть в hello же регионе Azure, что ваше хранилище служб восстановления и должно быть включена георепликация.</span><span class="sxs-lookup"><span data-stu-id="4e517-175">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="4e517-176">Если hello восстановления учетной записи хранения имеет тип хранилища Azure (классические), переход на другой ресурс hello защищенных машин восстановить hello машины tooAzure IaaS (классические).</span><span class="sxs-lookup"><span data-stu-id="4e517-176">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="4e517-177">Hello указана учетная запись хранения для восстановления типа хранилища Azure (Azure Resource Manager), переход на другой ресурс hello защищены машины восстановить hello машины tooAzure IaaS (диспетчера ресурсов Azure).</span><span class="sxs-lookup"><span data-stu-id="4e517-177">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   >
2. <span data-ttu-id="4e517-178">Получите hello защиты соответствующий toohello узел контейнера, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4e517-178">Get hello protection container corresponding toohello site, as follows:</span></span>

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. <span data-ttu-id="4e517-179">Запустите hello сопоставление контейнера защиты hello с политикой репликации hello, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="4e517-179">Start hello association of hello protection container with hello replication policy, as follows:</span></span>

     <span data-ttu-id="4e517-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer.</span><span class="sxs-lookup"><span data-stu-id="4e517-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span></span>

   <span data-ttu-id="4e517-181">Дождитесь toocomplete задания ассоциации hello и убедитесь, что он успешно завершено.</span><span class="sxs-lookup"><span data-stu-id="4e517-181">Wait for hello association job toocomplete, and ensure that it completed successfully.</span></span>

## <a name="step-7-enable-protection-for-virtual-machines"></a><span data-ttu-id="4e517-182">Шаг 7. Включение защиты для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="4e517-182">Step 7: Enable protection for virtual machines</span></span>
1. <span data-ttu-id="4e517-183">Получите hello защиты сущности соответствующего toohello виртуальной Машины требуется tooprotect, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="4e517-183">Get hello protection entity corresponding toohello VM you want tooprotect, as follows:</span></span>

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. <span data-ttu-id="4e517-184">Защищать hello виртуальной машины, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="4e517-184">Start protecting hello virtual machine, as follows:</span></span>

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > <span data-ttu-id="4e517-185">Hello указанную учетную запись хранения должна быть в hello же регионе Azure, что ваше хранилище служб восстановления и должно быть включена георепликация.</span><span class="sxs-lookup"><span data-stu-id="4e517-185">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="4e517-186">Если hello восстановления учетной записи хранения имеет тип хранилища Azure (классические), переход на другой ресурс hello защищенных машин восстановить hello машины tooAzure IaaS (классические).</span><span class="sxs-lookup"><span data-stu-id="4e517-186">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="4e517-187">Hello указана учетная запись хранения для восстановления типа хранилища Azure (Azure Resource Manager), переход на другой ресурс hello защищены машины восстановить hello машины tooAzure IaaS (диспетчера ресурсов Azure).</span><span class="sxs-lookup"><span data-stu-id="4e517-187">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   > <span data-ttu-id="4e517-188">Если hello ВМ, вы защищаете имеет более одного диска вложенного tooit, укажите hello диска операционной системы с помощью hello *OSDiskName* параметра.</span><span class="sxs-lookup"><span data-stu-id="4e517-188">If hello VM you are protecting has more than one disk attached tooit, specify hello operating system disk by using hello *OSDiskName* parameter.</span></span>
   >
   >
3. <span data-ttu-id="4e517-189">Дождитесь tooreach виртуальных машин hello защищенное состояние после начальной репликации hello.</span><span class="sxs-lookup"><span data-stu-id="4e517-189">Wait for hello virtual machines tooreach a protected state after hello initial replication.</span></span> <span data-ttu-id="4e517-190">Это может занять некоторое время, в зависимости от таких факторов, как объем hello toobe данные реплицируются и hello tooAzure вышестоящего пропускную способность.</span><span class="sxs-lookup"><span data-stu-id="4e517-190">This can take a while, depending on factors such as hello amount of data toobe replicated and hello available upstream bandwidth tooAzure.</span></span> <span data-ttu-id="4e517-191">Состояние задания Hello и StateDescription следующим образом, обновляются при hello достижения в защищенное состояние виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4e517-191">hello job State and StateDescription are updated as follows, upon hello VM reaching a protected state.</span></span>

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. <span data-ttu-id="4e517-192">Обновите свойства восстановления, например hello размера роли виртуальной Машины и отработки отказа tooupon карты интерфейса сети hello сети Azure tooattach hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4e517-192">Update recovery properties, such as hello VM role size, and hello Azure network tooattach hello virtual machine's network interface cards tooupon failover.</span></span>

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update hello virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a><span data-ttu-id="4e517-193">Шаг 8. Запуск тестовой отработки отказа</span><span class="sxs-lookup"><span data-stu-id="4e517-193">Step 8: Run a test failover</span></span>
1. <span data-ttu-id="4e517-194">Запустите задание тестовой отработки отказа, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4e517-194">Run a test failover job, as follows:</span></span>

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. <span data-ttu-id="4e517-195">Проверьте теста hello создания виртуальной Машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="4e517-195">Verify that hello test VM is created in Azure.</span></span> <span data-ttu-id="4e517-196">(hello теста отработки отказа Задание приостановлено, после создания hello тестовой виртуальной Машине в Azure.</span><span class="sxs-lookup"><span data-stu-id="4e517-196">(hello test failover job is suspended, after creating hello test VM in Azure.</span></span> <span data-ttu-id="4e517-197">Hello завершения задания по очистке дефекты hello создан при возобновлении задания hello, как показано в следующем шаге hello.)</span><span class="sxs-lookup"><span data-stu-id="4e517-197">hello job completes by cleaning up hello created artefacts upon resuming hello job, as illustrated in hello next step.)</span></span>
3. <span data-ttu-id="4e517-198">Полный hello тестирования отработки отказа следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4e517-198">Complete hello test failover, as follows:</span></span>

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a><span data-ttu-id="4e517-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4e517-199">Next Steps</span></span>
<span data-ttu-id="4e517-200">[Узнайте больше](https://msdn.microsoft.com/library/azure/mt637930.aspx) о командлетах PowerShell инструмента Azure Resource Manager для службы Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="4e517-200">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
