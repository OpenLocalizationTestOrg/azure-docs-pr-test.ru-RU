---
title: "tooAzure виртуальных машин Hyper-V aaaReplicate hello классическом портале с помощью PowerShell | Документы Microsoft"
description: "Автоматизация hello репликацию виртуальных машин Hyper-V в облаках VMM с помощью Site Recovery и PowerShell в классическом портале hello"
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: tysonn
ms.assetid: 9011f567-e0b4-4306-951a-b30da19f5db6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: d6847b46ac227209e6890de4ab603b23f827360f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-tooazure-with-powershell-in-hello-classic-portal"></a><span data-ttu-id="17b98-103">Реплицировать tooAzure виртуальных машин Hyper-V с помощью PowerShell в классическом портале hello</span><span class="sxs-lookup"><span data-stu-id="17b98-103">Replicate Hyper-V VMs tooAzure with PowerShell in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="17b98-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="17b98-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="17b98-105">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="17b98-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="17b98-106">Классический портал</span><span class="sxs-lookup"><span data-stu-id="17b98-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="17b98-107">PowerShell — классическая модель</span><span class="sxs-lookup"><span data-stu-id="17b98-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="17b98-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="17b98-108">Overview</span></span>
<span data-ttu-id="17b98-109">Azure Site Recovery поддерживает tooyour бизнес-непрерывности и аварийного восстановления (BCDR) стратегии, управляя операциями репликации, отработки отказа и восстановления виртуальных машин в различных вариантов развертывания.</span><span class="sxs-lookup"><span data-stu-id="17b98-109">Azure Site Recovery contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="17b98-110">Полный список развертывания сценариев. в разделе hello [Обзор Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="17b98-110">For a full list of deployment scenarios see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="17b98-111">В этой статье показано, как toouse PowerShell tooautomate общие задачи должны tooperform при настройке виртуальных машин Hyper-V Azure Site Recovery tooreplicate в хранилище tooAzure облаков System Center VMM.</span><span class="sxs-lookup"><span data-stu-id="17b98-111">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooAzure storage.</span></span>

<span data-ttu-id="17b98-112">статья Hello содержит необходимые условия для сценария hello и показано, как установить tooset копирование в хранилище Site Recovery hello поставщика Azure Site Recovery на исходном сервере VMM hello, зарегистрируйте сервер hello в хранилище hello, добавьте учетную запись хранилища Azure, установите hello Azure Агент служб восстановления на серверах узлов Hyper-V, настройте параметры защиты для облаков VMM, будет применен tooall защищенные виртуальные машины, а затем включите защиту для этих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="17b98-112">hello article includes prerequisites for hello scenario, and shows you how tooset up a Site Recovery vault, install hello Azure Site Recovery Provider on hello source VMM server, register hello server in hello vault, add an Azure storage account, install hello Azure Recovery Services agent on Hyper-V host servers, configure protection settings for VMM clouds that will be applied tooall protected virtual machines, and then enable protection for those virtual machines.</span></span> <span data-ttu-id="17b98-113">После этого тестирования toomake отработки отказа hello, убедиться, что все работает должным образом.</span><span class="sxs-lookup"><span data-stu-id="17b98-113">Finish up by testing hello failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="17b98-114">Если возникли проблемы с установкой этого сценария опубликовать вопросы на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="17b98-114">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="17b98-115">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="17b98-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="17b98-116">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="17b98-116">This article covers using hello Classic deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="17b98-117">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="17b98-117">Before you start</span></span>
<span data-ttu-id="17b98-118">Убедитесь, что выполнены следующие предварительные требования.</span><span class="sxs-lookup"><span data-stu-id="17b98-118">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="17b98-119">Предварительные требования Azure</span><span class="sxs-lookup"><span data-stu-id="17b98-119">Azure prerequisites</span></span>
* <span data-ttu-id="17b98-120">Вам потребуется учетная запись [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="17b98-120">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="17b98-121">Начните с [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17b98-121">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="17b98-122">Вам потребуется данные реплицируются toostore учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="17b98-122">You'll need an Azure storage account toostore replicated data.</span></span> <span data-ttu-id="17b98-123">Hello учетная запись должна включена георепликация.</span><span class="sxs-lookup"><span data-stu-id="17b98-123">hello account needs geo-replication enabled.</span></span> <span data-ttu-id="17b98-124">Он должен быть в hello же регионе, что хранилище Azure Site Recovery hello и связанные с hello одной подписке.</span><span class="sxs-lookup"><span data-stu-id="17b98-124">It should be in hello same region as hello Azure Site Recovery vault and be associated with hello same subscription.</span></span> <span data-ttu-id="17b98-125">См. [дополнительные сведения о службе хранилища Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="17b98-125">[Learn more about Azure storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="17b98-126">Необходимо убедиться, что, нужно tooprotect виртуальные машины соответствуют toomake [предварительные требования виртуальной машины Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="17b98-126">You'll need toomake sure that virtual machines you want tooprotect comply with [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

### <a name="vmm-prerequisites"></a><span data-ttu-id="17b98-127">Предварительные требования VMM</span><span class="sxs-lookup"><span data-stu-id="17b98-127">VMM prerequisites</span></span>
* <span data-ttu-id="17b98-128">Вам потребуется сервер VMM под управлением System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="17b98-128">You'll need  VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="17b98-129">Необходимо по крайней мере одно облако на сервер VMM требуется tooprotect hello.</span><span class="sxs-lookup"><span data-stu-id="17b98-129">You'll need at least one cloud on hello VMM server you want tooprotect.</span></span> <span data-ttu-id="17b98-130">облако Hello должен содержать:</span><span class="sxs-lookup"><span data-stu-id="17b98-130">hello cloud should contain:</span></span>
  * <span data-ttu-id="17b98-131">одну или несколько групп узлов VMM;</span><span class="sxs-lookup"><span data-stu-id="17b98-131">One or more VMM host groups.</span></span>
  * <span data-ttu-id="17b98-132">один или несколько серверов узлов или кластеров Hyper-V в каждой группе узлов;</span><span class="sxs-lookup"><span data-stu-id="17b98-132">One or more Hyper-V host servers or clusters in each host group .</span></span>
  * <span data-ttu-id="17b98-133">Один или несколько виртуальных машин на сервере Hyper-V источника hello.</span><span class="sxs-lookup"><span data-stu-id="17b98-133">One or more virtual machines on hello source Hyper-V server.</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="17b98-134">Предварительные требования Hyper-V</span><span class="sxs-lookup"><span data-stu-id="17b98-134">Hyper-V prerequisites</span></span>
* <span data-ttu-id="17b98-135">Hello серверы узла Hyper-V должны работать под управлением **Windows Server 2012** с ролью Hyper-V или **Microsoft Hyper-V Server 2012** и иметь hello установлены последние обновления.</span><span class="sxs-lookup"><span data-stu-id="17b98-135">hello host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have hello latest updates installed.</span></span>
* <span data-ttu-id="17b98-136">Если Hyper-V выполняется в кластере, учтите, что брокер кластера не создается автоматически при использовании кластера на основе статических IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="17b98-136">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="17b98-137">Брокер кластера hello tooconfigure вам потребуется вручную.</span><span class="sxs-lookup"><span data-stu-id="17b98-137">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="17b98-138">toodo это, в диспетчере сервера > Диспетчер отказоустойчивости кластеров, подключите toohello кластер, щелкните **настроить роль** и выберите **брокера реплики Hyper-V** в hello **выберите роль**экрана приветствия мастера высокой доступности.</span><span class="sxs-lookup"><span data-stu-id="17b98-138">toodo this, in Server Manager > Failover Cluster Manager, connect toohello cluster, click **Configure Role** and select **Hyper-V Replica Broker** in hello **Select Role** screen of hello High Availability wizard.</span></span>
* <span data-ttu-id="17b98-139">Любой сервер узла Hyper-V или кластера, для которого требуется защита toomanage должны включаться в облаке VMM.</span><span class="sxs-lookup"><span data-stu-id="17b98-139">Any Hyper-V host server or cluster for which you want toomanage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="17b98-140">Предварительные требования сетевого сопоставления</span><span class="sxs-lookup"><span data-stu-id="17b98-140">Network mapping prerequisites</span></span>
<span data-ttu-id="17b98-141">При защите виртуальных машин в Azure сетевое сопоставление сопоставление между сетями VM на исходном сервере VMM hello и целевой сетях Azure tooenable hello следующее:</span><span class="sxs-lookup"><span data-stu-id="17b98-141">When you protect virtual machines in Azure network mapping maps between VM networks on hello source VMM server and target Azure networks tooenable hello following:</span></span>

* <span data-ttu-id="17b98-142">Все машины, которые отработки отказа на hello же может подключиться tooeach других, независимо от используемого плана восстановления, находящиеся в сеть.</span><span class="sxs-lookup"><span data-stu-id="17b98-142">All machines which fail over on hello same network can connect tooeach other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="17b98-143">Если сетевой шлюз настроен hello целевой сети Azure, виртуальные машины могут подключаться tooother локальных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="17b98-143">If a network gateway is setup on hello target Azure network, virtual machines can connect tooother on-premises virtual machines.</span></span>
* <span data-ttu-id="17b98-144">Если не настроить сети сопоставление только виртуальные машины, которые выполняют отработку отказа в hello же плана восстановления будут другие возможности tooconnect tooeach после tooAzure перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="17b98-144">If you don’t configure network mapping only virtual machines that fail over in hello same recovery plan will be able tooconnect tooeach other after failover tooAzure.</span></span>

<span data-ttu-id="17b98-145">Если требуется, чтобы toodeploy сетевого сопоставления необходимо иметь hello следующее:</span><span class="sxs-lookup"><span data-stu-id="17b98-145">If you want toodeploy network mapping you'll need hello following:</span></span>

* <span data-ttu-id="17b98-146">виртуальные машины Hello требуется tooprotect на исходном сервере VMM hello должно быть tooa подключенной сети виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="17b98-146">hello virtual machines you want tooprotect on hello source VMM server should be connected tooa VM network.</span></span> <span data-ttu-id="17b98-147">Сеть должна быть связанной tooa логической сети, связанной с облаком hello.</span><span class="sxs-lookup"><span data-stu-id="17b98-147">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
* <span data-ttu-id="17b98-148">Сеть Azure toowhich реплицировать виртуальные машины могут подключаться после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="17b98-148">An Azure network toowhich replicated virtual machines can connect after failover.</span></span> <span data-ttu-id="17b98-149">Будет предложено выбрать этой сети во время hello перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="17b98-149">You'll select this network at hello time of failover.</span></span> <span data-ttu-id="17b98-150">сеть Hello должны находиться в hello же регионе, что подписки Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="17b98-150">hello network should be in hello same region as your Azure Site Recovery subscription.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="17b98-151">Необходимые компоненты PowerShell</span><span class="sxs-lookup"><span data-stu-id="17b98-151">PowerShell prerequisites</span></span>
<span data-ttu-id="17b98-152">Убедитесь, что у вас есть toogo готовности Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="17b98-152">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="17b98-153">Если вы уже используете PowerShell, вам потребуется tooupgrade tooversion 0.8.10 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="17b98-153">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="17b98-154">Сведения о настройке PowerShell см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="17b98-154">For information about setting up PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="17b98-155">После установки и настройки PowerShell вы можете просматривать все hello доступных командлетов для службы hello [здесь](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="17b98-155">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="17b98-156">toolearn советы, помогающие использовать командлеты hello, например как значения параметров, входы и выходы обычно обрабатываются в Azure PowerShell, в разделе [начало работы с командлетами Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="17b98-156">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see [Get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="17b98-157">Шаг 1: Задайте подписку hello</span><span class="sxs-lookup"><span data-stu-id="17b98-157">Step 1: Set hello subscription</span></span>
<span data-ttu-id="17b98-158">В PowerShell выполните следующие командлеты.</span><span class="sxs-lookup"><span data-stu-id="17b98-158">In PowerShell, run these cmdlets:</span></span>

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

<span data-ttu-id="17b98-159">Замените hello элементы внутри hello «< >» свои данные.</span><span class="sxs-lookup"><span data-stu-id="17b98-159">Replace hello elements within hello "< >" with your specific information.</span></span>

## <a name="step-2-create-a-site-recovery-vault"></a><span data-ttu-id="17b98-160">Шаг 2. Создание хранилища Site Recovery</span><span class="sxs-lookup"><span data-stu-id="17b98-160">Step 2: Create a Site Recovery vault</span></span>
<span data-ttu-id="17b98-161">В PowerShell замените элементы hello в «< >» hello свои данные и выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="17b98-161">In PowerShell, replace hello elements within hello "< >" with your specific information, and run these commands:</span></span>

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a><span data-ttu-id="17b98-162">Шаг 3. Создание ключа регистрации хранилища</span><span class="sxs-lookup"><span data-stu-id="17b98-162">Step 3: Generate a vault registration key</span></span>
<span data-ttu-id="17b98-163">Создайте ключ регистрации в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="17b98-163">Generate a registration key in hello vault.</span></span> <span data-ttu-id="17b98-164">После загрузки hello поставщика Azure Site Recovery и установите его на сервере VMM hello, используемой этим сервером VMM hello tooregister ключа в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="17b98-164">After you download hello Azure Site Recovery Provider and install it on hello VMM server, you'll use this key tooregister hello VMM server in hello vault.</span></span>

1. <span data-ttu-id="17b98-165">Получить файл параметр hello хранилища и задать контекст hello:</span><span class="sxs-lookup"><span data-stu-id="17b98-165">Get hello vault setting file and set hello context:</span></span>

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. <span data-ttu-id="17b98-166">Задайте контекст хранилища hello, выполнив hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="17b98-166">Set hello vault context by running hello following commands:</span></span>

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="17b98-167">Шаг 4: Установка поставщика Azure Site Recovery hello</span><span class="sxs-lookup"><span data-stu-id="17b98-167">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="17b98-168">На виртуальной машине VMM hello создайте каталог, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="17b98-168">On hello VMM machine, create a directory by running hello following command:</span></span>

   ```

   pushd C:\ASR\

   ```
2. <span data-ttu-id="17b98-169">Извлеките файлы hello, с помощью поставщика загружаются hello, выполнив следующую команду hello</span><span class="sxs-lookup"><span data-stu-id="17b98-169">Extract hello files using hello downloaded provider by running hello following command</span></span>

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. <span data-ttu-id="17b98-170">Установите поставщик hello, с помощью hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="17b98-170">Install hello provider using hello following commands:</span></span>

   ```

   .\SetupDr.exe /i

   ```

   ```

   $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
   do
   {
     $isNotInstalled = $true;
     if(Test-Path $installationRegPath)
     {
         $isNotInstalled = $false;
     }
   }While($isNotInstalled)

   ```

   <span data-ttu-id="17b98-171">Дождитесь установки toofinish hello.</span><span class="sxs-lookup"><span data-stu-id="17b98-171">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="17b98-172">Зарегистрируйте сервер hello в хранилище hello, с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="17b98-172">Register hello server in hello vault using hello following command:</span></span>

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="17b98-173">Шаг 5. Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="17b98-173">Step 5: Create an Azure storage account</span></span>
<span data-ttu-id="17b98-174">Если у вас нет учетной записи Azure, создайте учетную запись с включенной репликацией geo, выполнив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="17b98-174">If you don't have an Azure storage account, create a geo-replication enabled account by running hello following command:</span></span>

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

<span data-ttu-id="17b98-175">Обратите внимание, что учетная запись хранения hello должна быть в hello же регионе, что служба восстановления сайтов Azure hello и связанные с hello одной подписке.</span><span class="sxs-lookup"><span data-stu-id="17b98-175">Note that hello storage account must be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription.</span></span>

## <a name="step-6-install-hello-azure-recovery-services-agent"></a><span data-ttu-id="17b98-176">Шаг 6: Установите агент служб восстановления Azure hello</span><span class="sxs-lookup"><span data-stu-id="17b98-176">Step 6: Install hello Azure Recovery Services Agent</span></span>
<span data-ttu-id="17b98-177">Hello портал Azure, установка агента служб восстановления Azure hello на каждом сервере узла Hyper-V, расположенных в облаках VMM hello требуется tooprotect.</span><span class="sxs-lookup"><span data-stu-id="17b98-177">From hello Azure portal, install hello Azure Recovery Services agent on each Hyper-V host server located in hello VMM clouds you want tooprotect.</span></span>

<span data-ttu-id="17b98-178">Выполните следующую команду на всех узлах VMM hello.</span><span class="sxs-lookup"><span data-stu-id="17b98-178">Run hello following command on all VMM hosts:</span></span>

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="17b98-179">Шаг 7. Настройка параметров защиты облачных систем</span><span class="sxs-lookup"><span data-stu-id="17b98-179">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="17b98-180">Создайте профиль tooAzure облачной защиты, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="17b98-180">Create a cloud protection profile tooAzure by running hello following command:</span></span>

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. <span data-ttu-id="17b98-181">Получите контейнер защиты, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="17b98-181">Get a protection container by running hello following commands:</span></span>

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. <span data-ttu-id="17b98-182">Запустите hello сопоставление контейнера защиты hello с облаком hello:</span><span class="sxs-lookup"><span data-stu-id="17b98-182">Start hello association of hello protection container with hello cloud:</span></span>

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. <span data-ttu-id="17b98-183">После завершения задания hello, выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="17b98-183">After hello job has finished, run hello following command:</span></span>

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. <span data-ttu-id="17b98-184">После завершения обработки задания hello, выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="17b98-184">After hello job has finished processing, run hello following command:</span></span>

        Do
        {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

        if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
        }While($isJobLeftForProcessing)



<span data-ttu-id="17b98-185">toocheck hello завершения операции hello, следуйте указаниям hello [наблюдение за активностью](#monitor).</span><span class="sxs-lookup"><span data-stu-id="17b98-185">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="17b98-186">Шаг 8. Настройка сетевого сопоставления</span><span class="sxs-lookup"><span data-stu-id="17b98-186">Step 8: Configure network mapping</span></span>
<span data-ttu-id="17b98-187">Перед началом сопоставления сетей убедитесь, что виртуальные машины на исходном сервере VMM hello tooa подключенной сети виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="17b98-187">Before you begin network mapping verify that virtual machines on hello source VMM server are connected tooa VM network.</span></span> <span data-ttu-id="17b98-188">Кроме того, создайте одну или несколько виртуальных сетей Azure.</span><span class="sxs-lookup"><span data-stu-id="17b98-188">In addition, create one or more Azure virtual networks.</span></span> <span data-ttu-id="17b98-189">Обратите внимание, что несколько сетей виртуальной Машины может быть сопоставленных tooa одной сетью Azure.</span><span class="sxs-lookup"><span data-stu-id="17b98-189">Note that multiple VM networks can be mapped tooa single Azure network.</span></span>

<span data-ttu-id="17b98-190">Обратите внимание, что если hello целевая сеть содержит несколько подсетей, и одна из этих подсетей имеет hello находится совпадает с именем подсети, на какие hello исходной виртуальной машины, то hello реплики виртуальной машины после отработки отказа будет подключенных toothat целевой подсети.</span><span class="sxs-lookup"><span data-stu-id="17b98-190">Note that if hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="17b98-191">Если целевой подсети с совпадающим именем не существует, hello виртуальная машина будет подключенных toohello первой подсети в сети hello.</span><span class="sxs-lookup"><span data-stu-id="17b98-191">If there is not a target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>

<span data-ttu-id="17b98-192">Первая команда Hello возвращает серверов для hello текущее хранилище Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="17b98-192">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="17b98-193">Hello команда сохраняет серверы Microsoft Azure Site Recovery hello в переменной hello $Servers массива.</span><span class="sxs-lookup"><span data-stu-id="17b98-193">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

    $Servers = Get-AzureSiteRecoveryServer


<span data-ttu-id="17b98-194">Вторая команда Hello возвращает hello сети восстановления сайта для первого сервера hello в массиве hello $Servers.</span><span class="sxs-lookup"><span data-stu-id="17b98-194">hello second command gets hello site recovery network for hello first server in hello $Servers array.</span></span> <span data-ttu-id="17b98-195">Команда Hello сохраняет сетей hello в hello $Networks переменной.</span><span class="sxs-lookup"><span data-stu-id="17b98-195">hello command stores hello networks in hello $Networks variable.</span></span>

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

<span data-ttu-id="17b98-196">Третья команда Hello возвращает подписками Azure с помощью командлета Get-AzureSubscription hello и затем сохраняет это значение в переменной hello $Subscriptions.</span><span class="sxs-lookup"><span data-stu-id="17b98-196">hello third command gets your Azure subscriptions by using hello Get-AzureSubscription cmdlet, and then stores that value in hello $Subscriptions variable.</span></span>

    $Subscriptions = Get-AzureSubscription



<span data-ttu-id="17b98-197">Четвертая команда Hello получает виртуальные сети Azure с помощью командлета Get-AzureVNetSite hello, а затем это значение в переменной hello $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="17b98-197">hello fourth command gets Azure virtual networks by using hello Get-AzureVNetSite cmdlet, and then that value in hello $AzureVmNetworks variable.</span></span>

    $AzureVmNetworks = Get-AzureVNetSite



<span data-ttu-id="17b98-198">Hello окончательного создает сопоставление между первичной и сетями виртуальной машины Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="17b98-198">hello final cmdlet creates a mapping between hello primary network and hello Azure virtual machine network.</span></span> <span data-ttu-id="17b98-199">командлет Hello указывает hello основной сети как первый элемент $Networks hello.</span><span class="sxs-lookup"><span data-stu-id="17b98-199">hello cmdlet specifies hello primary network as hello first element of $Networks.</span></span> <span data-ttu-id="17b98-200">командлет Hello указывает сеть виртуальной машины как первого элемента hello $AzureVmNetworks с помощью его идентификатора.</span><span class="sxs-lookup"><span data-stu-id="17b98-200">hello cmdlet specifies a virtual machine network as hello first element of $AzureVmNetworks by using its ID.</span></span> <span data-ttu-id="17b98-201">Команда Hello содержит идентификатор вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="17b98-201">hello command includes your Azure subscription ID.</span></span>

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="17b98-202">Шаг 9. Включение защиты для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="17b98-202">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="17b98-203">После надлежащей настройки серверов, облаков и сетей, можно включить защиту для виртуальных машин в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="17b98-203">After servers, clouds, and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span> <span data-ttu-id="17b98-204">Обратите внимание hello следующие:</span><span class="sxs-lookup"><span data-stu-id="17b98-204">Note hello following:</span></span>

<span data-ttu-id="17b98-205">Виртуальные машины должны соответствовать [предварительным требованиям к виртуальным машинам Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="17b98-205">Virtual machines must meet [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

<span data-ttu-id="17b98-206">tooenable защиты hello операционной системы и свойства диска операционной системы необходимо задать для виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="17b98-206">tooenable protection hello operating system and operating system disk properties must be set for hello virtual machine.</span></span> <span data-ttu-id="17b98-207">При создании виртуальной машины в VMM с помощью шаблона виртуальной машины можно задать свойство hello.</span><span class="sxs-lookup"><span data-stu-id="17b98-207">When you create a virtual machine in VMM using a virtual machine template you can set hello property.</span></span> <span data-ttu-id="17b98-208">Можно также задать эти свойства для существующих виртуальных машин на hello **Общие** и **конфигурация оборудования** вкладки свойств виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="17b98-208">You can also set these properties for existing virtual machines on hello **General** and **Hardware Configuration** tabs of hello virtual machine properties.</span></span> <span data-ttu-id="17b98-209">Если не установить эти свойства в VMM вы будете может tooconfigure их на портале Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="17b98-209">If you don't set these properties in VMM you'll be able tooconfigure them in hello Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="17b98-210">Защита tooenable выполнения hello следующая команда контейнера защиты tooget hello:</span><span class="sxs-lookup"><span data-stu-id="17b98-210">tooenable protection, run hello following command tooget hello protection container:</span></span>

     <span data-ttu-id="17b98-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span><span class="sxs-lookup"><span data-stu-id="17b98-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span></span>
2. <span data-ttu-id="17b98-212">Получите сущность защиты hello (VM), выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="17b98-212">Get hello protection entity (VM) by running hello following command:</span></span>

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. <span data-ttu-id="17b98-213">Включите hello аварийного восстановления для hello виртуальной Машины, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="17b98-213">Enable hello DR for hello VM by running hello following command:</span></span>

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a><span data-ttu-id="17b98-214">Выполните тестирование развертывания</span><span class="sxs-lookup"><span data-stu-id="17b98-214">Test your deployment</span></span>
<span data-ttu-id="17b98-215">Планирование развертывания можно запустить тестовую отработку отказа для одной виртуальной машины или создайте план восстановления, состоящий из нескольких виртуальных машин и запустите тестовую отработку отказа для hello tootest.</span><span class="sxs-lookup"><span data-stu-id="17b98-215">tootest your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for hello plan.</span></span> <span data-ttu-id="17b98-216">Тестовая обработка отказа имитирует механизм отработки отказа и восстановления в изолированной сети.</span><span class="sxs-lookup"><span data-stu-id="17b98-216">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="17b98-217">Обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="17b98-217">Note that:</span></span>

* <span data-ttu-id="17b98-218">Tooconnect toohello виртуальной машины в Azure с помощью удаленного рабочего стола, после отработки отказа hello, включите подключение к удаленному рабочему столу на виртуальной машине hello перед запуском тестовой отработки отказа hello.</span><span class="sxs-lookup"><span data-stu-id="17b98-218">If you want tooconnect toohello virtual machine in Azure using Remote Desktop after hello failover, enable Remote Desktop Connection on hello virtual machine before you run hello test failover.</span></span>
* <span data-ttu-id="17b98-219">После отработки отказа будут использоваться открытый IP адрес tooconnect toohello виртуальной машины в Azure с помощью удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="17b98-219">After failover, you'll use a public IP address tooconnect toohello virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="17b98-220">Если требуется toodo это, убедитесь, что нет политик домена, запретить подключения tooa виртуальной машины, с помощью общедоступного адреса.</span><span class="sxs-lookup"><span data-stu-id="17b98-220">If you want toodo this, ensure you don't have any domain policies that prevent you from connecting tooa virtual machine using a public address.</span></span>

<span data-ttu-id="17b98-221">toocheck hello завершения операции hello, следуйте указаниям hello [наблюдение за активностью](#monitor).</span><span class="sxs-lookup"><span data-stu-id="17b98-221">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="create-a-recovery-plan"></a><span data-ttu-id="17b98-222">Создайте план восстановления</span><span class="sxs-lookup"><span data-stu-id="17b98-222">Create a recovery plan</span></span>
1. <span data-ttu-id="17b98-223">Создание XML-файл в качестве шаблона для плана восстановления, используя данные hello ниже и сохраните его как «C:\RPTemplatePath.xml».</span><span class="sxs-lookup"><span data-stu-id="17b98-223">Create an .xml file as a template for your recovery plan using hello data below, and then save it as "C:\RPTemplatePath.xml".</span></span>
2. <span data-ttu-id="17b98-224">Измените узел RecoveryPlan hello идентификатор, имя, PrimaryServerId и SecondaryServerId.</span><span class="sxs-lookup"><span data-stu-id="17b98-224">Change hello RecoveryPlan node Id, Name, PrimaryServerId, and SecondaryServerId.</span></span>
3. <span data-ttu-id="17b98-225">Измените узел ProtectionEntity hello PrimaryProtectionEntityId (vmid из VMM).</span><span class="sxs-lookup"><span data-stu-id="17b98-225">Change hello ProtectionEntity node PrimaryProtectionEntityId (vmid from VMM).</span></span>
4. <span data-ttu-id="17b98-226">Можно добавить дополнительные виртуальные машины, добавив дополнительные узлы ProtectionEntity.</span><span class="sxs-lookup"><span data-stu-id="17b98-226">You can add more VMs by adding more ProtectionEntity nodes.</span></span>

        <#
        <?xml version="1.0" encoding="utf-16"?>
        <RecoveryPlan Id="d0323b26-5be2-471b-addc-0a8742796610" Name="rp-test"     PrimaryServerId="9350a530-d5af-435b-9f2b-b941b5d9fcd5"     SecondaryServerId="21a9403c-6ec1-44f2-b744-b4e50b792387" Description=""     Version="V2014_07">
          <Actions />
          <ActionGroups>
            <ShutdownAllActionGroup Id="ShutdownAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </ShutdownAllActionGroup>
            <FailoverAllActionGroup Id="FailoverAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </FailoverAllActionGroup>
            <BootActionGroup Id="DefaultActionGroup">
              <PreActionSequence />
              <PostActionSequence />
              <ProtectionEntity PrimaryProtectionEntityId="d4c8ce92-a613-4c63-9b03-    cf163cc36ef8" />
            </BootActionGroup>
          </ActionGroups>
          <ActionGroupSequence>
            <ActionGroup Id="ShutdownAllActionGroup" ActionId="ShutdownAllActionGroup"     Before="FailoverAllActionGroup" />
            <ActionGroup Id="FailoverAllActionGroup" ActionId="FailoverAllActionGroup"     After="ShutdownAllActionGroup" Before="DefaultActionGroup" />
            <ActionGroup Id="DefaultActionGroup" ActionId="DefaultActionGroup" After="FailoverAllActionGroup"/>
          </ActionGroupSequence>
        </RecoveryPlan>
        #>



1. <span data-ttu-id="17b98-227">Заполните данных hello в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="17b98-227">Fill in hello data in hello template:</span></span>

        $TemplatePath = "C:\RPTemplatePath.xml";



1. <span data-ttu-id="17b98-228">Создайте hello RecoveryPlan:</span><span class="sxs-lookup"><span data-stu-id="17b98-228">Create hello RecoveryPlan:</span></span>

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a><span data-ttu-id="17b98-229">Запуск тестовой отработки отказа</span><span class="sxs-lookup"><span data-stu-id="17b98-229">Run a test failover</span></span>
1. <span data-ttu-id="17b98-230">Получите объект RecoveryPlan hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="17b98-230">Get hello RecoveryPlan object by running hello following command:</span></span>

     <span data-ttu-id="17b98-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span><span class="sxs-lookup"><span data-stu-id="17b98-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span></span>
2. <span data-ttu-id="17b98-232">Запустите тестовую отработку отказа hello, выполнив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="17b98-232">Start hello test failover by running hello following command:</span></span>

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <span data-ttu-id="17b98-233"><a name=monitor></a> Мониторинг активности</span><span class="sxs-lookup"><span data-stu-id="17b98-233"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="17b98-234">Используйте следующие команды toomonitor hello действие hello.</span><span class="sxs-lookup"><span data-stu-id="17b98-234">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="17b98-235">Обратите внимание, что на toowait между задания для обработки toofinish hello.</span><span class="sxs-lookup"><span data-stu-id="17b98-235">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

    Do
    {
            $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
            Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
            if($job -eq $null -or $job.StateDescription -ne "Completed")
            {
                $isJobLeftForProcessing = $true;
            }

        if($isJobLeftForProcessing)
            {
                Start-Sleep -Seconds 60
            }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="17b98-236">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="17b98-236">Next steps</span></span>
<span data-ttu-id="17b98-237">[Узнайте больше](/powershell/azure/overview) о командлетах PowerShell для Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="17b98-237">[Read more](/powershell/azure/overview) about Azure Site Recovery PowerShell cmdlets.</span></span> <span data-ttu-id="17b98-238"></a>.</span><span class="sxs-lookup"><span data-stu-id="17b98-238"></a>.</span></span>
