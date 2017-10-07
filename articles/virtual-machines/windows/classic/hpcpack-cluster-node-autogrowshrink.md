---
title: "узлы кластера HPC Pack aaaAutoscale | Документы Microsoft"
description: "Автоматически увеличиваться и уменьшаться hello число вычислительными узлами кластера HPC Pack в Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0bdf55625d337a2bbfe05677682d645a584798d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a><span data-ttu-id="b5d72-103">Автоматически увеличиваться и уменьшаться hello ресурсы кластера HPC Pack в Azure, в соответствии с toohello рабочая нагрузка кластера</span><span class="sxs-lookup"><span data-stu-id="b5d72-103">Automatically grow and shrink hello HPC Pack cluster resources in Azure according toohello cluster workload</span></span>
<span data-ttu-id="b5d72-104">Если выполняется развертывание узлов «Повышения» Azure в кластере HPC Pack или создать кластер пакета HPC на виртуальных машинах Azure, вы можете способ автоматического увеличения или сжатия hello ресурсы кластера, например узлов или ядер согласно hello рабочей нагрузки в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="b5d72-104">If you deploy Azure “burst” nodes in your HPC Pack cluster, or you create an HPC Pack cluster in Azure VMs, you may want a way to automatically grow or shrink hello cluster resources such as nodes or cores according to hello workload on hello cluster.</span></span> <span data-ttu-id="b5d72-105">Масштабирование ресурсов кластера hello таким образом позволяет toouse ресурсам Azure более эффективно и управлять их стоимостью.</span><span class="sxs-lookup"><span data-stu-id="b5d72-105">Scaling hello cluster resources in this way allows you toouse your Azure resources more efficiently and control their costs.</span></span>

<span data-ttu-id="b5d72-106">В этой статье показано два способа HPC Pack предоставляет tooautoscale вычислительные ресурсы:</span><span class="sxs-lookup"><span data-stu-id="b5d72-106">This article shows you two ways that HPC Pack provides tooautoscale compute resources:</span></span>

* <span data-ttu-id="b5d72-107">Свойство кластера HPC Pack Hello **AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="b5d72-107">hello HPC Pack cluster property **AutoGrowShrink**</span></span>

* <span data-ttu-id="b5d72-108">Hello **AzureAutoGrowShrink.ps1** скрипт HPC PowerShell</span><span class="sxs-lookup"><span data-stu-id="b5d72-108">hello **AzureAutoGrowShrink.ps1** HPC PowerShell script</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="b5d72-109">В настоящее время можно автоматически увеличивать и сжимать только вычислительные узлы пакета HPC под управлением ОС Windows Server.</span><span class="sxs-lookup"><span data-stu-id="b5d72-109">Currently you can only automatically grow and shrink HPC Pack compute nodes that are running a Windows Server operating system.</span></span>


## <a name="set-hello-autogrowshrink-cluster-property"></a><span data-ttu-id="b5d72-110">Задайте для свойства кластера AutoGrowShrink hello</span><span class="sxs-lookup"><span data-stu-id="b5d72-110">Set hello AutoGrowShrink cluster property</span></span>
### <a name="prerequisites"></a><span data-ttu-id="b5d72-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b5d72-111">Prerequisites</span></span>

* <span data-ttu-id="b5d72-112">**HPC Pack 2012 R2 с обновлением 2 или более поздней версии кластера** -hello головной узел кластера может быть развернут локально или на виртуальной Машине Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d72-112">**HPC Pack 2012 R2 Update 2 or later cluster** - hello cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="b5d72-113">В разделе [Настройка гибридного кластера с помощью пакета HPC](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget работы с локальной головного узла и узлы «Повышения» Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d72-113">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="b5d72-114">В разделе hello [скрипт развертывания IaaS пакета HPC](hpcpack-cluster-powershell-script.md) tooquickly развертывание кластера HPC Pack на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d72-114">See hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) tooquickly deploy an HPC Pack cluster in Azure VMs.</span></span>

* <span data-ttu-id="b5d72-115">**Для кластера с головным узлом в Azure (модель развертывания Resource Manager)**. Начиная с версии пакета HPC 2016 аутентификация сертификата в приложении Azure Active Directory используется для автоматического увеличения и сжатия виртуальных машин кластера, развернутых с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b5d72-115">**For a cluster with a head node in Azure (Resource Manager deployment model)** - Starting in HPC Pack 2016, certificate authentication in an Azure Active Directory application is used for automatically growing and shrinking cluster VMs deployed using Azure Resource Manager.</span></span> <span data-ttu-id="b5d72-116">Настройте сертификат следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b5d72-116">Configure a certificate as follows:</span></span>

  1. <span data-ttu-id="b5d72-117">После развертывания кластера подключитесь с удаленного рабочего стола tooone головного узла.</span><span class="sxs-lookup"><span data-stu-id="b5d72-117">After cluster deployment, connect by Remote Desktop tooone head node.</span></span>

  2. <span data-ttu-id="b5d72-118">Отправка hello сертификата (в формате PFX с закрытым ключом) tooeach головного узла и установите tooCert:\LocalMachine\My и Cert: \LocalMachine\Root.</span><span class="sxs-lookup"><span data-stu-id="b5d72-118">Upload hello certificate (PFX format with private key) tooeach head node and install tooCert:\LocalMachine\My and Cert:\LocalMachine\Root.</span></span>

  3. <span data-ttu-id="b5d72-119">Запустите Azure PowerShell с правами администратора и выполните следующие команды на один головной узел hello:</span><span class="sxs-lookup"><span data-stu-id="b5d72-119">Start Azure PowerShell as an administrator and run hello following commands on one head node:</span></span>

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    <span data-ttu-id="b5d72-120">Если ваша учетная запись находится в более чем одного клиента Azure Active Directory или подписки Azure, можно запустить следующие hello команд tooselect hello правильный клиента и подписки:</span><span class="sxs-lookup"><span data-stu-id="b5d72-120">If your account is in more than one Azure Active Directory tenant or Azure subscription, you can run hello following command tooselect hello correct tenant and subscription:</span></span>
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    <span data-ttu-id="b5d72-121">Запустите следующие команды tooview hello hello выбранного клиента и подписки:</span><span class="sxs-lookup"><span data-stu-id="b5d72-121">Run hello following command tooview hello currently selected tenant and subscription:</span></span>
    
    ```powershell
        Get-AzureRMContext
    ```

  4. <span data-ttu-id="b5d72-122">Запустите следующий сценарий hello</span><span class="sxs-lookup"><span data-stu-id="b5d72-122">Run hello following script</span></span>

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    <span data-ttu-id="b5d72-123">где:</span><span class="sxs-lookup"><span data-stu-id="b5d72-123">where</span></span>

    <span data-ttu-id="b5d72-124">**DisplayName** — отображаемое имя активного приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d72-124">**DisplayName** - Azure Active Application display name.</span></span> <span data-ttu-id="b5d72-125">Если приложение hello не существует, он создается в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b5d72-125">If hello application does not exist, it is created in Azure Active Directory.</span></span>

    <span data-ttu-id="b5d72-126">**Домашняя страница** -hello Домашняя страница приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b5d72-126">**HomePage** - hello home page of hello application.</span></span> <span data-ttu-id="b5d72-127">Вы можете настроить пустой URL-адрес, как предшествующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="b5d72-127">You can configure a dummy URL, as in hello preceding example.</span></span>

    <span data-ttu-id="b5d72-128">**IdentifierUri** -идентификатор приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b5d72-128">**IdentifierUri** - Identifier of hello application.</span></span> <span data-ttu-id="b5d72-129">Вы можете настроить пустой URL-адрес, как предшествующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="b5d72-129">You can configure a dummy URL, as in hello preceding example.</span></span>

    <span data-ttu-id="b5d72-130">**CertificateThumbprint** -отпечаток сертификата hello установлен на головном узле hello в шаге 1.</span><span class="sxs-lookup"><span data-stu-id="b5d72-130">**CertificateThumbprint** - Thumbprint of hello certificate you installed on hello head node in Step 1.</span></span>

    <span data-ttu-id="b5d72-131">**TenantId** — идентификатор клиента каталога Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b5d72-131">**TenantId** - Tenant ID of your Azure Active Directory.</span></span> <span data-ttu-id="b5d72-132">Hello идентификатор клиента можно получить с портала Azure Active Directory hello **свойства** страницы.</span><span class="sxs-lookup"><span data-stu-id="b5d72-132">You can get hello Tenant ID from hello Azure Active Directory portal **Properties** page.</span></span>

    <span data-ttu-id="b5d72-133">Чтобы получить дополнительные сведения о **ConfigARMAutoGrowShrinkCert.ps1**, выполните `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="b5d72-133">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span></span>


* <span data-ttu-id="b5d72-134">**Для кластера с головного узла в Azure (классической модели развертывания)** — Если используется кластер hello toocreate скрипт развертывания hello IaaS пакета HPC в hello классической модели развертывания, включите hello **AutoGrowShrink** кластера свойство, задав параметр AutoGrowShrink hello в файле конфигурации кластера hello.</span><span class="sxs-lookup"><span data-stu-id="b5d72-134">**For a cluster with a head node in Azure (classic deployment model)** - If you use hello HPC Pack IaaS deployment script toocreate hello cluster in hello classic deployment model, enable hello **AutoGrowShrink** cluster property by setting hello AutoGrowShrink option in hello cluster configuration file.</span></span> <span data-ttu-id="b5d72-135">Дополнительные сведения см. в разделе документации hello hello [сценарий загрузки](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="b5d72-135">For details, see hello documentation accompanying hello [script download](https://www.microsoft.com/download/details.aspx?id=44949).</span></span>

    <span data-ttu-id="b5d72-136">Кроме того, включите hello **AutoGrowShrink** свойство кластера после развертывания hello кластера с помощью HPC PowerShell команд, описанных в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="b5d72-136">Alternatively, enable hello **AutoGrowShrink** cluster property after you deploy hello cluster by using HPC PowerShell commands described in hello following section.</span></span> <span data-ttu-id="b5d72-137">tooprepare для этого первого полного hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="b5d72-137">tooprepare for this, first complete hello following steps:</span></span>

  1. <span data-ttu-id="b5d72-138">Настройка сертификата управления Azure на головном узле hello и hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d72-138">Configure an Azure management certificate on hello head node and in hello Azure subscription.</span></span> <span data-ttu-id="b5d72-139">Для тестирования развертывания можно использовать самозаверяющий сертификат по умолчанию Microsoft HPC Azure hello, который устанавливает пакета HPC на головном узле hello и затем отправьте этот сертификат tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d72-139">For a test deployment, you can use hello Default Microsoft HPC Azure self-signed certificate that HPC Pack installs on hello head node, and then upload that certificate tooyour Azure subscription.</span></span> <span data-ttu-id="b5d72-140">Параметры и инструкции см. в разделе hello [библиотеки TechNet рекомендации](https://technet.microsoft.com/library/gg481759.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5d72-140">For options and steps, see hello [TechNet Library guidance](https://technet.microsoft.com/library/gg481759.aspx).</span></span>

  2. <span data-ttu-id="b5d72-141">Запустите **regedit** на головном узле hello перейдите tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo и добавьте строковое значение.</span><span class="sxs-lookup"><span data-stu-id="b5d72-141">Run **regedit** on hello head node, go tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo, and add a string value.</span></span> <span data-ttu-id="b5d72-142">Задайте имя значения hello слишком «Отпечаток» и значение данных toohello отпечаток сертификата hello в шаге 1.</span><span class="sxs-lookup"><span data-stu-id="b5d72-142">Set hello Value name too“ThumbPrint”, and Value data toohello thumbprint of hello certificate in Step 1.</span></span>

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a><span data-ttu-id="b5d72-143">Свойства AutoGrowShrink hello tooset команды HPC PowerShell</span><span class="sxs-lookup"><span data-stu-id="b5d72-143">HPC PowerShell commands tooset hello AutoGrowShrink property</span></span>
<span data-ttu-id="b5d72-144">Ниже приведены образец HPC PowerShell команды tooset **AutoGrowShrink** и tootune его поведения, используя дополнительные параметры.</span><span class="sxs-lookup"><span data-stu-id="b5d72-144">Following are sample HPC PowerShell commands tooset **AutoGrowShrink** and tootune its behavior with additional parameters.</span></span> <span data-ttu-id="b5d72-145">В разделе [AutoGrowShrink параметры](#AutoGrowShrink-parameters) далее в этой статье для hello полный список параметров.</span><span class="sxs-lookup"><span data-stu-id="b5d72-145">See [AutoGrowShrink parameters](#AutoGrowShrink-parameters) later in this article for hello complete list of settings.</span></span>

<span data-ttu-id="b5d72-146">toorun эти команды, запустите HPC PowerShell на головном узле кластера hello с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="b5d72-146">toorun these commands, start HPC PowerShell on hello cluster head node as an administrator.</span></span>

<span data-ttu-id="b5d72-147">**hello tooenable AutoGrowShrink свойство**</span><span class="sxs-lookup"><span data-stu-id="b5d72-147">**tooenable hello AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

<span data-ttu-id="b5d72-148">**hello toodisable AutoGrowShrink свойство**</span><span class="sxs-lookup"><span data-stu-id="b5d72-148">**toodisable hello AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

<span data-ttu-id="b5d72-149">**toochange hello расти интервал в минутах**</span><span class="sxs-lookup"><span data-stu-id="b5d72-149">**toochange hello grow interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

<span data-ttu-id="b5d72-150">**toochange hello уменьшить интервал в минутах**</span><span class="sxs-lookup"><span data-stu-id="b5d72-150">**toochange hello shrink interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

<span data-ttu-id="b5d72-151">**tooview hello AutoGrowShrink в текущей конфигурации**</span><span class="sxs-lookup"><span data-stu-id="b5d72-151">**tooview hello current configuration of AutoGrowShrink**</span></span>

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

<span data-ttu-id="b5d72-152">**группы узлов tooexclude из AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="b5d72-152">**tooexclude node groups from AutoGrowShrink**</span></span>

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> <span data-ttu-id="b5d72-153">Этот параметр поддерживается, начиная с версии пакета HPC 2016.</span><span class="sxs-lookup"><span data-stu-id="b5d72-153">This parameter is supported starting in HPC Pack 2016</span></span>
>

### <a name="autogrowshrink-parameters"></a><span data-ttu-id="b5d72-154">Параметры AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="b5d72-154">AutoGrowShrink parameters</span></span>
<span data-ttu-id="b5d72-155">Hello ниже приведены параметры AutoGrowShrink, которые можно изменить с помощью hello **HpcClusterProperty набора** команды.</span><span class="sxs-lookup"><span data-stu-id="b5d72-155">hello following are AutoGrowShrink parameters that you can modify by using hello **Set-HpcClusterProperty** command.</span></span>

* <span data-ttu-id="b5d72-156">**EnableGrowShrink** - переключение tooenable или отключить hello **AutoGrowShrink** свойство.</span><span class="sxs-lookup"><span data-stu-id="b5d72-156">**EnableGrowShrink** - Switch tooenable or disable hello **AutoGrowShrink** property.</span></span>
* <span data-ttu-id="b5d72-157">**ParamSweepTasksPerCore** -количество параметрической очистки задач toogrow одного ядра.</span><span class="sxs-lookup"><span data-stu-id="b5d72-157">**ParamSweepTasksPerCore** - Number of parametric sweep tasks toogrow one core.</span></span> <span data-ttu-id="b5d72-158">по умолчанию Hello — одно ядро toogrow каждой задачи.</span><span class="sxs-lookup"><span data-stu-id="b5d72-158">hello default is toogrow one core per task.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b5d72-159">Изменения HPC Pack QFE KB3134307 **ParamSweepTasksPerCore** слишком**TasksPerResourceUnit**.</span><span class="sxs-lookup"><span data-stu-id="b5d72-159">HPC Pack QFE KB3134307 changes **ParamSweepTasksPerCore** too**TasksPerResourceUnit**.</span></span> <span data-ttu-id="b5d72-160">Он основан на типе ресурса задания hello и может быть узел, сокета или core.</span><span class="sxs-lookup"><span data-stu-id="b5d72-160">It is based on hello job resource type and can be node, socket, or core.</span></span>
  >
  >
* <span data-ttu-id="b5d72-161">**GrowThreshold** -пороговое значение автоматического увеличения tootrigger задач в очереди.</span><span class="sxs-lookup"><span data-stu-id="b5d72-161">**GrowThreshold** - Threshold of queued tasks tootrigger automatic growth.</span></span> <span data-ttu-id="b5d72-162">по умолчанию Hello-1, это означает, что если 1 или более задач в hello в очереди состояний, автоматически увеличивать размер узлов.</span><span class="sxs-lookup"><span data-stu-id="b5d72-162">hello default is 1, which means that if there are 1 or more tasks in hello queued state, automatically grow nodes.</span></span>
* <span data-ttu-id="b5d72-163">**GrowInterval** -интервал в минутах tootrigger автоматическое приращение.</span><span class="sxs-lookup"><span data-stu-id="b5d72-163">**GrowInterval** - Interval in minutes tootrigger automatic growth.</span></span> <span data-ttu-id="b5d72-164">Интервал по умолчанию Hello составляет 5 минут.</span><span class="sxs-lookup"><span data-stu-id="b5d72-164">hello default interval is 5 minutes.</span></span>
* <span data-ttu-id="b5d72-165">**ShrinkInterval** -интервал в минутах tootrigger автоматическое сжатие.</span><span class="sxs-lookup"><span data-stu-id="b5d72-165">**ShrinkInterval** - Interval in minutes tootrigger automatic shrinking.</span></span> <span data-ttu-id="b5d72-166">Интервал по умолчанию Hello составляет 5 минут. |</span><span class="sxs-lookup"><span data-stu-id="b5d72-166">hello default interval is 5 minutes.|</span></span>
* <span data-ttu-id="b5d72-167">**ShrinkIdleTimes** -количество непрерывных проверок tooshrink tooindicate hello узлов бездействуют.</span><span class="sxs-lookup"><span data-stu-id="b5d72-167">**ShrinkIdleTimes** - Number of continuous checks tooshrink tooindicate hello nodes are idle.</span></span> <span data-ttu-id="b5d72-168">по умолчанию Hello-3 раза.</span><span class="sxs-lookup"><span data-stu-id="b5d72-168">hello default is 3 times.</span></span> <span data-ttu-id="b5d72-169">Например, если hello **ShrinkInterval** 5 минут, пакет HPC проверяет, является ли узел hello простоя каждые 5 минут.</span><span class="sxs-lookup"><span data-stu-id="b5d72-169">For example, if hello **ShrinkInterval** is 5 minutes, HPC Pack checks whether hello node is idle every 5 minutes.</span></span> <span data-ttu-id="b5d72-170">Если узлы hello в состояние бездействия hello после 3 непрерывных проверок (15 минут), пакет HPC сжимает этого узла.</span><span class="sxs-lookup"><span data-stu-id="b5d72-170">If hello nodes are in hello idle state after 3 continuous checks (15 minutes), then HPC Pack shrinks that node.</span></span>
* <span data-ttu-id="b5d72-171">**ExtraNodesGrowRatio** -дополнительных процент toogrow узлы для заданий интерфейса передачи сообщений (MPI).</span><span class="sxs-lookup"><span data-stu-id="b5d72-171">**ExtraNodesGrowRatio** - Additional percentage of nodes toogrow for Message Passing Interface (MPI) jobs.</span></span> <span data-ttu-id="b5d72-172">значение по умолчанию Hello-1, означающее HPC Pack роста узлы % 1 для заданий MPI.</span><span class="sxs-lookup"><span data-stu-id="b5d72-172">hello default value is 1, which means that HPC Pack grows nodes 1% for MPI jobs.</span></span>
* <span data-ttu-id="b5d72-173">**GrowByMin** -переключение tooindicate ли политика автоматического увеличения hello основан на hello минимальные ресурсы, необходимые для задания hello.</span><span class="sxs-lookup"><span data-stu-id="b5d72-173">**GrowByMin** - Switch tooindicate whether hello autogrow policy is based on hello minimum resources required for hello job.</span></span> <span data-ttu-id="b5d72-174">по умолчанию Hello равно false, что означает, что пакет HPC увеличился узлов для задания в соответствии с hello максимальное ресурсы, необходимые для задания hello.</span><span class="sxs-lookup"><span data-stu-id="b5d72-174">hello default is false, which means that HPC Pack grows nodes for jobs based on hello maximum resources required for hello jobs.</span></span>
* <span data-ttu-id="b5d72-175">**SoaJobGrowThreshold** -пороговое значение входящих SOA запросов tootrigger hello автоматическое увеличение процесса.</span><span class="sxs-lookup"><span data-stu-id="b5d72-175">**SoaJobGrowThreshold** - Threshold of incoming SOA requests tootrigger hello automatic grow process.</span></span> <span data-ttu-id="b5d72-176">значение по умолчанию Hello — 50 000.</span><span class="sxs-lookup"><span data-stu-id="b5d72-176">hello default value is 50000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b5d72-177">Этот параметр поддерживается, начиная с версии пакета HPC 2012 R2 с обновлением 3.</span><span class="sxs-lookup"><span data-stu-id="b5d72-177">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
  >
* <span data-ttu-id="b5d72-178">**SoaRequestsPerCore** -количество входящих SOA запросов toogrow одного ядра.</span><span class="sxs-lookup"><span data-stu-id="b5d72-178">**SoaRequestsPerCore** -Number of incoming SOA requests toogrow one core.</span></span> <span data-ttu-id="b5d72-179">значение по умолчанию Hello — 20000.</span><span class="sxs-lookup"><span data-stu-id="b5d72-179">hello default value is 20000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b5d72-180">Этот параметр поддерживается, начиная с версии пакета HPC 2012 R2 с обновлением 3.</span><span class="sxs-lookup"><span data-stu-id="b5d72-180">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
* <span data-ttu-id="b5d72-181">**ExcludeNodeGroups** — узлы в hello указаны группы узлов автоматически увеличиваться и уменьшаться.</span><span class="sxs-lookup"><span data-stu-id="b5d72-181">**ExcludeNodeGroups** – Nodes in hello specified node groups do not automatically grow and shrink.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="b5d72-182">Этот параметр поддерживается, начиная с версии пакета HPC 2016.</span><span class="sxs-lookup"><span data-stu-id="b5d72-182">This parameter is supported starting in HPC Pack 2016.</span></span>
  >

### <a name="mpi-example"></a><span data-ttu-id="b5d72-183">Пример MPI</span><span class="sxs-lookup"><span data-stu-id="b5d72-183">MPI example</span></span>
<span data-ttu-id="b5d72-184">По умолчанию пакет HPC увеличивается на 1% дополнительные узлы для заданий MPI (**ExtraNodesGrowRatio** имеет значение too1).</span><span class="sxs-lookup"><span data-stu-id="b5d72-184">By default HPC Pack grows 1% extra nodes for MPI jobs (**ExtraNodesGrowRatio** is set too1).</span></span> <span data-ttu-id="b5d72-185">Hello причина заключается в том, что MPI может потребоваться несколько узлов и hello задание можно запустить только в том случае, когда готовы все узлы.</span><span class="sxs-lookup"><span data-stu-id="b5d72-185">hello reason is that MPI may require multiple nodes, and hello job can only run when all nodes are ready.</span></span> <span data-ttu-id="b5d72-186">При запуске узлов Azure иногда одного узла могут потребоваться дополнительные toostart времени, чем другие, вызывая другие узлы toobe простоя во время ожидания для этого узла tooget готовности.</span><span class="sxs-lookup"><span data-stu-id="b5d72-186">When Azure starts nodes, occasionally one node might need more time toostart than others, causing other nodes toobe idle while waiting for that node tooget ready.</span></span> <span data-ttu-id="b5d72-187">Увеличивая размер дополнительных узлов, пакет HPC сокращает это время ожидания ресурса и потенциально сокращает расходы.</span><span class="sxs-lookup"><span data-stu-id="b5d72-187">By growing extra nodes, HPC Pack reduces this resource waiting time, and potentially saves costs.</span></span> <span data-ttu-id="b5d72-188">Процент hello tooincrease дополнительных узлов для заданий MPI (например, too10%), выполнить команду, аналогичную</span><span class="sxs-lookup"><span data-stu-id="b5d72-188">tooincrease hello percentage of extra nodes for MPI jobs (for example, too10%), run a command similar to</span></span>

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a><span data-ttu-id="b5d72-189">Пример SOA</span><span class="sxs-lookup"><span data-stu-id="b5d72-189">SOA example</span></span>
<span data-ttu-id="b5d72-190">По умолчанию **SoaJobGrowThreshold** задано too50000 и **SoaRequestsPerCore** имеет значение too200000.</span><span class="sxs-lookup"><span data-stu-id="b5d72-190">By default, **SoaJobGrowThreshold** is set too50000 and **SoaRequestsPerCore** is set too200000.</span></span> <span data-ttu-id="b5d72-191">Если отправить одно задание SOA с 70 000 запросов, будет существовать одна задача, поставленная в очередь, и 70 000 входящих запросов.</span><span class="sxs-lookup"><span data-stu-id="b5d72-191">If you submit one SOA job with 70000 requests, there is one queued task and incoming requests are 70000.</span></span> <span data-ttu-id="b5d72-192">В этом случае пакет HPC роста 1 ядро hello в очереди задач, и для входящих запросов увеличивается (70000 50000) или в общее роста 2 ядра, для этого задания SOA 20000 = 1 core.</span><span class="sxs-lookup"><span data-stu-id="b5d72-192">In this case HPC Pack grows 1 core for hello queued task, and for incoming requests, grows (70000 - 50000)/20000 = 1 core, so in total grows 2 cores for this SOA job.</span></span>

## <a name="run-hello-azureautogrowshrinkps1-script"></a><span data-ttu-id="b5d72-193">Запустите сценарий AzureAutoGrowShrink.ps1 hello</span><span class="sxs-lookup"><span data-stu-id="b5d72-193">Run hello AzureAutoGrowShrink.ps1 script</span></span>
### <a name="prerequisites"></a><span data-ttu-id="b5d72-194">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b5d72-194">Prerequisites</span></span>

* <span data-ttu-id="b5d72-195">**HPC Pack 2012 R2 с обновлением 1 или более поздней версии кластера** - hello **AzureAutoGrowShrink.ps1** скрипта установлен в папке hello % CCP_HOME % bin.</span><span class="sxs-lookup"><span data-stu-id="b5d72-195">**HPC Pack 2012 R2 Update 1 or later cluster** - hello **AzureAutoGrowShrink.ps1** script is installed in hello %CCP_HOME%bin folder.</span></span> <span data-ttu-id="b5d72-196">Hello головной узел кластера может быть развернут локально или на виртуальной Машине Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d72-196">hello cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="b5d72-197">В разделе [Настройка гибридного кластера с помощью пакета HPC](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget работы с локальной головного узла и узлы «Повышения» Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d72-197">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="b5d72-198">. В разделе hello [скрипт развертывания IaaS пакета HPC](hpcpack-cluster-powershell-script.md) tooquickly развертывание кластера HPC Pack на виртуальных машинах Azure или используйте [шаблона Azure краткое руководство](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span><span class="sxs-lookup"><span data-stu-id="b5d72-198">See hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) tooquickly deploy an HPC Pack cluster in Azure VMs, or use an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span></span>
* <span data-ttu-id="b5d72-199">**Azure PowerShell 1.4.0** -скрипт hello в настоящее время зависит от этой конкретной версии Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5d72-199">**Azure PowerShell 1.4.0** - hello script currently depends on this specific version of Azure PowerShell.</span></span>
* <span data-ttu-id="b5d72-200">**Для кластера с помощью Azure burst узлы** -скрипт hello на клиентском компьютере с установленным пакетом HPC или на головном узле hello.</span><span class="sxs-lookup"><span data-stu-id="b5d72-200">**For a cluster with Azure burst nodes** - Run hello script on a client computer where HPC Pack is installed, or on hello head node.</span></span> <span data-ttu-id="b5d72-201">Если выполняется на клиентском компьютере, убедитесь, что вы hello переменной $env: CCP_SCHEDULER toopoint toohello головного узла.</span><span class="sxs-lookup"><span data-stu-id="b5d72-201">If running on a client computer, ensure that you set hello variable $env:CCP_SCHEDULER toopoint toohello head node.</span></span> <span data-ttu-id="b5d72-202">Hello узлы «Повышения» Azure должны быть добавлены toohello кластера, но они могут быть в hello не развернутом состоянии.</span><span class="sxs-lookup"><span data-stu-id="b5d72-202">hello Azure “burst” nodes must be added toohello cluster, but they may be in hello Not-Deployed state.</span></span>
* <span data-ttu-id="b5d72-203">**Для кластера, развернутых в виртуальных машинах Azure (модели развертывания диспетчера ресурсов)** -кластер виртуальных машин Azure, развернутых в модели развертывания диспетчера ресурсов hello, скрипт hello поддерживает два метода для проверки подлинности Azure: вход tooyour учетная запись Azure сценарий hello toorun каждый раз (путем запуска `Login-AzureRmAccount`, или настройте tooauthenticate участника службы с сертификатом.</span><span class="sxs-lookup"><span data-stu-id="b5d72-203">**For a cluster deployed in Azure VMs (Resource Manager deployment model)** - For a cluster of Azure VMs deployed in hello Resource Manager deployment model, hello script supports two methods for Azure authentication: sign in tooyour Azure account toorun hello script every time (by running `Login-AzureRmAccount`, or configure a service principal tooauthenticate with a certificate.</span></span> <span data-ttu-id="b5d72-204">Пакет HPC предоставляет сценарий hello **ConfigARMAutoGrowShrinkCert.ps** toocreate участника службы с сертификатом.</span><span class="sxs-lookup"><span data-stu-id="b5d72-204">HPC Pack provides hello script **ConfigARMAutoGrowShrinkCert.ps** toocreate a service principal with certificate.</span></span> <span data-ttu-id="b5d72-205">Hello сценарий создает приложение Azure Active Directory (Azure AD) и субъекта-службы и назначает участника службы toohello роль участника hello.</span><span class="sxs-lookup"><span data-stu-id="b5d72-205">hello script creates an Azure Active Directory (Azure AD) application and a service principal, and assigns hello Contributor role toohello service principal.</span></span> <span data-ttu-id="b5d72-206">сценарий toorun hello, запустите Azure PowerShell от имени администратора и выполните hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="b5d72-206">toorun hello script, start Azure PowerShell  as administrator and run hello following commands:</span></span>

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    <span data-ttu-id="b5d72-207">Чтобы получить дополнительные сведения о **ConfigARMAutoGrowShrinkCert.ps1**, выполните `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="b5d72-207">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span></span>

* <span data-ttu-id="b5d72-208">**Для кластера, развернутых в виртуальных машинах Azure (классической модели развертывания)** -скрипт hello на hello ВМ головного узла, так как он зависит от hello **Start-HpcIaaSNode.ps1** и **Stop-HpcIaaSNode.ps1**сценарии, которые установлены на ней.</span><span class="sxs-lookup"><span data-stu-id="b5d72-208">**For a cluster deployed in Azure VMs (classic deployment model)** - Run hello script on hello head node VM, because it depends on hello **Start-HpcIaaSNode.ps1** and **Stop-HpcIaaSNode.ps1** scripts that are installed there.</span></span> <span data-ttu-id="b5d72-209">Кроме того, эти сценарии требуют сертификат управления Azure или файл параметров публикации (см. статью [Управление вычислительными узлами в кластере на основе пакета HPC в Azure](hpcpack-cluster-node-manage.md)).</span><span class="sxs-lookup"><span data-stu-id="b5d72-209">Those scripts additionally require an Azure management certificate or publish settings file (see [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md)).</span></span> <span data-ttu-id="b5d72-210">Убедитесь, что все hello вычислений узел виртуальных машин, необходимо уже добавлены toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="b5d72-210">Make sure all hello compute node VMs you need are already added toohello cluster.</span></span> <span data-ttu-id="b5d72-211">Они могут находиться в остановленном состоянии hello.</span><span class="sxs-lookup"><span data-stu-id="b5d72-211">They may be in hello Stopped state.</span></span>



### <a name="syntax"></a><span data-ttu-id="b5d72-212">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="b5d72-212">Syntax</span></span>
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="b5d72-213">Параметры</span><span class="sxs-lookup"><span data-stu-id="b5d72-213">Parameters</span></span>
* <span data-ttu-id="b5d72-214">**NodeTemplates** -имена toodefine шаблоны узла hello hello область для узлов toogrow hello и сжатия.</span><span class="sxs-lookup"><span data-stu-id="b5d72-214">**NodeTemplates** - Names of hello node templates toodefine hello scope for hello nodes toogrow and shrink.</span></span> <span data-ttu-id="b5d72-215">Если не указан (имеет значение по умолчанию hello @()), все узлы в hello **AzureNodes** узел группы находятся в области, если **NodeType** имеет значение AzureNodes, и все узлы в hello **ComputeNodes** узел группы находятся в области, когда **NodeType** имеет значение ComputeNodes.</span><span class="sxs-lookup"><span data-stu-id="b5d72-215">If not specified (hello default value is @()), all nodes in hello **AzureNodes** node group are in scope when **NodeType** has a value of AzureNodes, and all nodes in hello **ComputeNodes** node group are in scope when **NodeType** has a value of ComputeNodes.</span></span>
* <span data-ttu-id="b5d72-216">**JobTemplates** -имена hello задания области hello toodefine шаблоны для узлов toogrow hello.</span><span class="sxs-lookup"><span data-stu-id="b5d72-216">**JobTemplates** - Names of hello job templates toodefine hello scope for hello nodes toogrow.</span></span>
* <span data-ttu-id="b5d72-217">**NodeType** — тип узла toogrow hello и сжатия.</span><span class="sxs-lookup"><span data-stu-id="b5d72-217">**NodeType** - hello type of node toogrow and shrink.</span></span> <span data-ttu-id="b5d72-218">Поддерживаемые значения:</span><span class="sxs-lookup"><span data-stu-id="b5d72-218">Supported values are:</span></span>

  * <span data-ttu-id="b5d72-219">**AzureNodes** — для (расширительных) узлов PaaS Azure в локальной среде или в кластере IaaS Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d72-219">**AzureNodes** – for Azure PaaS (burst) nodes in an on-premises or Azure IaaS cluster.</span></span>
  * <span data-ttu-id="b5d72-220">**ComputeNodes** — для виртуальных машин вычислительных узлов только в кластере IaaS Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d72-220">**ComputeNodes** - for compute node VMs only in an Azure IaaS cluster.</span></span>

* <span data-ttu-id="b5d72-221">**NumOfQueuedJobsPerNodeToGrow** -количество заданий в очереди, необходимых toogrow один узел.</span><span class="sxs-lookup"><span data-stu-id="b5d72-221">**NumOfQueuedJobsPerNodeToGrow** - Number of queued jobs required toogrow one node.</span></span>
* <span data-ttu-id="b5d72-222">**NumOfQueuedJobsToGrowThreshold** -hello пороговое значение числа заданий в очереди toostart hello увеличиваться процесса.</span><span class="sxs-lookup"><span data-stu-id="b5d72-222">**NumOfQueuedJobsToGrowThreshold** - hello threshold number of queued jobs toostart hello grow process.</span></span>
* <span data-ttu-id="b5d72-223">**NumOfActiveQueuedTasksPerNodeToGrow** -hello количество активных задач в очереди, необходимых toogrow один узел.</span><span class="sxs-lookup"><span data-stu-id="b5d72-223">**NumOfActiveQueuedTasksPerNodeToGrow** - hello number of active queued tasks required toogrow one node.</span></span> <span data-ttu-id="b5d72-224">Если для **NumOfQueuedJobsPerNodeToGrow** указано значение больше 0, этот параметр пропускается.</span><span class="sxs-lookup"><span data-stu-id="b5d72-224">If **NumOfQueuedJobsPerNodeToGrow** is specified with a value greater than 0, this parameter is ignored.</span></span>
* <span data-ttu-id="b5d72-225">**NumOfActiveQueuedTasksToGrowThreshold** -hello пороговое число активных задач в очереди toostart hello увеличиваться процесса.</span><span class="sxs-lookup"><span data-stu-id="b5d72-225">**NumOfActiveQueuedTasksToGrowThreshold** - hello threshold number of active queued tasks toostart hello grow process.</span></span>
* <span data-ttu-id="b5d72-226">**NumOfInitialNodesToGrow** - hello первоначального минимальное число узлов toogrow, если все узлы hello в области находятся **не развернуто** или **остановлена (освобождена)**.</span><span class="sxs-lookup"><span data-stu-id="b5d72-226">**NumOfInitialNodesToGrow** - hello initial minimum number of nodes toogrow if all hello nodes in scope are **Not-Deployed** or **Stopped (Deallocated)**.</span></span>
* <span data-ttu-id="b5d72-227">**GrowCheckIntervalMins** -hello интервал в минутах между проверяет toogrow.</span><span class="sxs-lookup"><span data-stu-id="b5d72-227">**GrowCheckIntervalMins** - hello interval in minutes between checks toogrow.</span></span>
* <span data-ttu-id="b5d72-228">**ShrinkCheckIntervalMins** -hello интервал в минутах между проверяет tooshrink.</span><span class="sxs-lookup"><span data-stu-id="b5d72-228">**ShrinkCheckIntervalMins** - hello interval in minutes between checks tooshrink.</span></span>
* <span data-ttu-id="b5d72-229">**ShrinkCheckIdleTimes** -hello количество проверок непрерывного сжатия (разделенные **ShrinkCheckIntervalMins**) узлов hello tooindicate бездействуют.</span><span class="sxs-lookup"><span data-stu-id="b5d72-229">**ShrinkCheckIdleTimes** - hello number of continuous shrink checks (separated by **ShrinkCheckIntervalMins**) tooindicate hello nodes are idle.</span></span>
* <span data-ttu-id="b5d72-230">**UseLastConfigurations** -hello предыдущие конфигурации, сохраненные в файле параметров hello.</span><span class="sxs-lookup"><span data-stu-id="b5d72-230">**UseLastConfigurations** - hello previous configurations saved in hello argument file.</span></span>
* <span data-ttu-id="b5d72-231">**ArgFile**- hello имя toosave файл, используемый аргумент hello и hello конфигураций toorun hello скрипт обновления.</span><span class="sxs-lookup"><span data-stu-id="b5d72-231">**ArgFile**- hello name of hello argument file used toosave and update hello configurations toorun hello script.</span></span>
* <span data-ttu-id="b5d72-232">**LogFilePrefix** -hello префикс имени файла журнала hello.</span><span class="sxs-lookup"><span data-stu-id="b5d72-232">**LogFilePrefix** - hello prefix name of hello log file.</span></span> <span data-ttu-id="b5d72-233">Можно указать путь.</span><span class="sxs-lookup"><span data-stu-id="b5d72-233">You can specify a path.</span></span> <span data-ttu-id="b5d72-234">По умолчанию hello журнала является письменного toohello текущий рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="b5d72-234">By default hello log is written toohello current working directory.</span></span>

### <a name="example-1"></a><span data-ttu-id="b5d72-235">Пример 1</span><span class="sxs-lookup"><span data-stu-id="b5d72-235">Example 1</span></span>
<span data-ttu-id="b5d72-236">Hello следующий пример настраивает hello Azure пакета развертывания с шаблоном AzureNode по умолчанию toogrow узлов и автоматически уменьшается.</span><span class="sxs-lookup"><span data-stu-id="b5d72-236">hello following example configures hello Azure burst nodes deployed with the Default AzureNode Template toogrow and shrink automatically.</span></span> <span data-ttu-id="b5d72-237">Если все узлы изначально находятся в hello **не развернуто** состоянии, по крайней мере 3 узлы запущены.</span><span class="sxs-lookup"><span data-stu-id="b5d72-237">If all the nodes are initially in hello **Not-Deployed** state, at least 3 nodes are started.</span></span> <span data-ttu-id="b5d72-238">Если hello количество заданий в очереди превышает 8, hello сценарий запускает узлы, пока их количество не превышает отношение hello заданий в очереди для **NumOfQueuedJobsPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="b5d72-238">If hello number of queued jobs exceeds 8, hello script starts nodes until their number exceeds hello ratio of queued jobs to **NumOfQueuedJobsPerNodeToGrow**.</span></span> <span data-ttu-id="b5d72-239">Если узел найден toobe простоя в 3 раз подряд, он останавливается.</span><span class="sxs-lookup"><span data-stu-id="b5d72-239">If a node is found toobe idle in 3 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a><span data-ttu-id="b5d72-240">Пример 2</span><span class="sxs-lookup"><span data-stu-id="b5d72-240">Example 2</span></span>
<span data-ttu-id="b5d72-241">Hello следующий пример настраивает hello Azure ВМ вычислительных узлов развернут с toogrow шаблоном ComputeNode по умолчанию hello и автоматически уменьшается.</span><span class="sxs-lookup"><span data-stu-id="b5d72-241">hello following example configures hello Azure compute node VMs deployed with hello Default ComputeNode Template toogrow and shrink automatically.</span></span>
<span data-ttu-id="b5d72-242">Hello задания, настроенные с шаблона задания по умолчанию hello определить область hello рабочей нагрузки в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="b5d72-242">hello jobs configured by hello Default job template define hello scope of the workload on hello cluster.</span></span> <span data-ttu-id="b5d72-243">Если все узлы hello изначально были остановлены, запускаются по крайней мере 5 узлов.</span><span class="sxs-lookup"><span data-stu-id="b5d72-243">If all hello nodes are initially stopped, at least 5 nodes are started.</span></span> <span data-ttu-id="b5d72-244">Если hello число активных задач в очереди превышает 15, hello сценарий запускает узлы, пока их количество не превышает отношение активных задач в очереди hello слишком**NumOfActiveQueuedTasksPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="b5d72-244">If hello number of active queued tasks exceeds 15, hello script starts nodes until their number exceeds hello ratio of active queued tasks too**NumOfActiveQueuedTasksPerNodeToGrow**.</span></span> <span data-ttu-id="b5d72-245">Если узел найден toobe бездействия в 10 раз подряд, он останавливается.</span><span class="sxs-lookup"><span data-stu-id="b5d72-245">If a node is found toobe idle in 10 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
