---
title: "хранилище служб восстановления Azure tooan aaaUpgrade хранилище Site Recovery"
description: "Узнайте, как хранилище Azure Site Recovery tooupgrade tooa служб восстановления хранилище"
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/31/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: a18a923ee3bad91873e654c9b9b5bf8b83acc123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-site-recovery-vault-tooan-azure-resource-manager-based-recovery-services-vault"></a><span data-ttu-id="e9da0-103">Обновления в хранилище служб восстановления диспетчера ресурсов Azure Site Recovery tooan хранилища</span><span class="sxs-lookup"><span data-stu-id="e9da0-103">Upgrade a Site Recovery vault tooan Azure Resource Manager-based Recovery Services vault</span></span>

<span data-ttu-id="e9da0-104">В этой статье описывается, как tooupgrade Azure Site Recovery хранилищ tooAzure диспетчер ресурсов на основе службы восстановления хранилищ не оказывает никакого воздействия на текущей репликации.</span><span class="sxs-lookup"><span data-stu-id="e9da0-104">This article describes how tooupgrade Azure Site Recovery vaults tooAzure Resource Manager-based Recovery Service vaults without any impact on ongoing replication.</span></span> <span data-ttu-id="e9da0-105">Дополнительные сведения о функциях и преимуществах Azure Resource Manager см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e9da0-105">For more information about Azure Resource Manager features and benefits, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="e9da0-106">Введение</span><span class="sxs-lookup"><span data-stu-id="e9da0-106">Introduction</span></span>
<span data-ttu-id="e9da0-107">Хранилище служб восстановления — это ресурс Azure Resource Manager для управления резервного копирования и аварийного восстановления, изначально в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="e9da0-107">A Recovery Services vault is an Azure Resource Manager resource for managing backup and disaster recovery natively in hello cloud.</span></span> <span data-ttu-id="e9da0-108">Это единое хранилище, в котором можно использовать в hello новый портал Azure и он заменяет классический hello резервного копирования и хранилищ Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e9da0-108">It is a unified vault that you can use in hello new Azure portal, and it replaces hello classic backup and Site Recovery vaults.</span></span>

<span data-ttu-id="e9da0-109">Хранилища служб восстановления предоставляют возможность воспользоваться множеством функций, включая следующие:</span><span class="sxs-lookup"><span data-stu-id="e9da0-109">Recovery Services vaults offer an array of features, including:</span></span>

* <span data-ttu-id="e9da0-110">Поддержка Azure Resource Manager. Вы можете обеспечить защиту и отработку отказа виртуальных машин и физических компьютеров в стеке Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e9da0-110">Azure Resource Manager support: You can protect and fail over your virtual machines and physical machines into an Azure Resource Manager stack.</span></span>

* <span data-ttu-id="e9da0-111">Исключить диск: Если временные файлы или высокая степень изменения данных, что вы не хотите toouse к пропускной способности для тома можно исключить из репликации.</span><span class="sxs-lookup"><span data-stu-id="e9da0-111">Exclude disk: If you have temp files or high churn data that you don’t want toouse all your bandwidth for, you can exclude volumes from replication.</span></span> <span data-ttu-id="e9da0-112">Эта возможность включена в настоящее время *VMware tooAzure* и *tooAzure Hyper-V* и расширена также сценарии tooother.</span><span class="sxs-lookup"><span data-stu-id="e9da0-112">This capability has been enabled currently in *VMware tooAzure* and *Hyper-V tooAzure* and is extended tooother scenarios as well.</span></span>

* <span data-ttu-id="e9da0-113">Поддержка premium и локально избыточное хранилище: теперь могут защитить серверы в хранилище premium учетные записи, которые позволяют клиентам выше tooprotect приложений с помощью операций ввода/вывода в секунду (IOPS).</span><span class="sxs-lookup"><span data-stu-id="e9da0-113">Support for premium and locally redundant storage: You can now protect servers in premium storage accounts that allow customers tooprotect applications with higher input/output operations per second (IOPS).</span></span> <span data-ttu-id="e9da0-114">В настоящее время эта возможность поддерживается в *VMware tooAzure*.</span><span class="sxs-lookup"><span data-stu-id="e9da0-114">This capability is currently enabled in *VMware tooAzure*.</span></span>

* <span data-ttu-id="e9da0-115">Упрощенная схема качества Приступая к работе: hello усиленной Приступая к работе качества было разработано toomake аварийного восстановления установки легко.</span><span class="sxs-lookup"><span data-stu-id="e9da0-115">Streamlined getting-started experience: hello enhanced getting-started experience has been designed toomake disaster-recovery setup easy.</span></span>

* <span data-ttu-id="e9da0-116">Резервное копирование и восстановление узла управления из hello же хранилище: теперь защиты серверов для аварийного восстановления или выполнить резервное копирование из hello же хранилища, который может снизить издержки значительно управление.</span><span class="sxs-lookup"><span data-stu-id="e9da0-116">Backup and Site Recovery management from hello same vault: You can now protect servers for disaster recovery or perform backup from hello same vault, which can reduce your management overhead significantly.</span></span>

<span data-ttu-id="e9da0-117">Дополнительные сведения о возможности обновления hello и компонентах см. в разделе hello [хранения данных, резервное копирование и восстановление блог](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span><span class="sxs-lookup"><span data-stu-id="e9da0-117">For more information about hello upgraded experience and features, see hello [Storage, Backup, and Recovery blog](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span></span>

## <a name="salient-features"></a><span data-ttu-id="e9da0-118">Ключевые возможности</span><span class="sxs-lookup"><span data-stu-id="e9da0-118">Salient features</span></span>

* <span data-ttu-id="e9da0-119">Отсутствие влияния на выполняющуюся репликацию. Выполняющаяся репликация продолжается без перерывов во время и после обновления.</span><span class="sxs-lookup"><span data-stu-id="e9da0-119">No impact on ongoing replication: Ongoing replications continue without any interruption during and post upgrade.</span></span>

* <span data-ttu-id="e9da0-120">Отсутствие дополнительных затрат. Воспользуйтесь полным набором новых возможностей без дополнительных затрат.</span><span class="sxs-lookup"><span data-stu-id="e9da0-120">No additional cost: Get an entire set of updated capabilities at no additional cost.</span></span>

* <span data-ttu-id="e9da0-121">Без потери данных: поскольку этот процесс обновления, а не миграции, существующих точек восстановления репликации и параметры остаются без изменений во время и после обновления hello.</span><span class="sxs-lookup"><span data-stu-id="e9da0-121">No data loss: Because this process is an upgrade and not a migration, existing replication recovery points and settings remain intact during and after hello upgrade.</span></span>


## <a name="what-happens-during-hello-vault-upgrade"></a><span data-ttu-id="e9da0-122">Что происходит во время обновления hello хранилища?</span><span class="sxs-lookup"><span data-stu-id="e9da0-122">What happens during hello vault upgrade?</span></span>

<span data-ttu-id="e9da0-123">Во время обновления hello нельзя выполнять операции, такие как регистрация нового сервера или при включении репликации для виртуальной машины (VM).</span><span class="sxs-lookup"><span data-stu-id="e9da0-123">During hello upgrade, you cannot perform operations such as registering a new server or enabling replication for a virtual machine (VM).</span></span> <span data-ttu-id="e9da0-124">Операции, включающие данные из чтения или записи toohello хранилища данных, такие как репликация хранилища toohello защищенные элементы, выполняться по-прежнему.</span><span class="sxs-lookup"><span data-stu-id="e9da0-124">Operations that involve reading data from or writing data toohello vault, such as ongoing replication of protected items toohello vault, continue uninterrupted.</span></span>

### <a name="changes-tooautomation-and-tooling-after-hello-upgrade"></a><span data-ttu-id="e9da0-125">Изменения tooautomation и инструментарий после обновления hello</span><span class="sxs-lookup"><span data-stu-id="e9da0-125">Changes tooautomation and tooling after hello upgrade</span></span>
<span data-ttu-id="e9da0-126">Как тип хранилища hello обновление из hello классической модели toohello диспетчера ресурсов развертывания модели развертывания, обновите существующую среду автоматизации hello или tooensure средства, что toowork продолжается после обновления hello.</span><span class="sxs-lookup"><span data-stu-id="e9da0-126">As you upgrade hello vault type from hello classic deployment model toohello Resource Manager deployment model, update hello existing automation or tooling tooensure that it continues toowork after hello upgrade.</span></span>

### <a name="prepare-your-environment-for-hello-upgrade"></a><span data-ttu-id="e9da0-127">Подготовка среды для обновления hello</span><span class="sxs-lookup"><span data-stu-id="e9da0-127">Prepare your environment for hello upgrade</span></span>

* [<span data-ttu-id="e9da0-128">Установите PowerShell или ее tooversion 5 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="e9da0-128">Install PowerShell or upgrade it tooversion 5 or later</span></span>](https://www.microsoft.com/download/details.aspx?id=50395)
* [<span data-ttu-id="e9da0-129">Установите последнюю версию Azure PowerShell MSI hello</span><span class="sxs-lookup"><span data-stu-id="e9da0-129">Install hello latest version of Azure PowerShell MSI</span></span>](https://github.com/Azure/azure-powershell/releases)
* [<span data-ttu-id="e9da0-130">Загрузка скрипта обновления хранилища служб восстановления hello</span><span class="sxs-lookup"><span data-stu-id="e9da0-130">Download hello Recovery Services vault upgrade script</span></span>](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a><span data-ttu-id="e9da0-131">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e9da0-131">Prerequisites</span></span>
<span data-ttu-id="e9da0-132">в хранилищах службы восстановления диспетчера ресурсов tooAzure хранилищ tooupgrade из Site Recovery, должны выполняться следующие требования к hello:</span><span class="sxs-lookup"><span data-stu-id="e9da0-132">tooupgrade from Site Recovery vaults tooAzure Resource Manager-based Recovery Service vaults, you must meet hello following requirements:</span></span>

* <span data-ttu-id="e9da0-133">Версия агента не ниже: hello версия поставщика восстановления сайта Azure, установленный на сервере должна быть 5.1.1700.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e9da0-133">Minimum agent version: hello version of Azure Site Recovery Provider installed on your server must be 5.1.1700.0 or later.</span></span>

* <span data-ttu-id="e9da0-134">Поддерживаемая конфигурация. Не настраивайте для хранилища сеть SAN и группы доступности AlwaysOn SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e9da0-134">Supported configuration: You cannot configure your vault with storage area network (SAN) or SQL Server AlwaysOn Availability Groups.</span></span> <span data-ttu-id="e9da0-135">Остальные конфигурации поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="e9da0-135">All other configurations are supported.</span></span>

    >[!NOTE]
    ><span data-ttu-id="e9da0-136">После обновления hello вы можете управлять сопоставления хранилища только через PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e9da0-136">After hello upgrade, you can manage storage mapping only via PowerShell.</span></span>

* <span data-ttu-id="e9da0-137">Поддерживаемое развертывание сценария: ваше хранилище не должны быть hello *VMware tooAzure* модели развертывания устаревших версий.</span><span class="sxs-lookup"><span data-stu-id="e9da0-137">Supported deployment scenario: Your vault shouldn’t be hello *VMware tooAzure* legacy deployment model.</span></span> <span data-ttu-id="e9da0-138">Прежде чем продолжить, необходимо сначала переместите toohello расширенного развертывания модели.</span><span class="sxs-lookup"><span data-stu-id="e9da0-138">Before you proceed, first move toohello enhanced deployment model.</span></span>

* <span data-ttu-id="e9da0-139">Активных заданий инициированной пользователем, включающих управления плоскости операций: поскольку плоскости управления toohello доступ ограничен во время обновления, выполнения всех операций управления плоскости можно запустить обновление hello.</span><span class="sxs-lookup"><span data-stu-id="e9da0-139">No active user-initiated jobs that involve management plane operations: Because access toohello management plane is restricted during upgrade, complete all your management plane actions before you trigger hello upgrade.</span></span> <span data-ttu-id="e9da0-140">Этот процесс не касается выполняющейся репликации.</span><span class="sxs-lookup"><span data-stu-id="e9da0-140">This process doesn’t include ongoing replication.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="e9da0-141">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="e9da0-141">Frequently asked questions</span></span>

<span data-ttu-id="e9da0-142">**Влияет ли обновление на выполняющуюся репликацию?**</span><span class="sxs-lookup"><span data-stu-id="e9da0-142">**Does this upgrade affect my ongoing replication?**</span></span>

<span data-ttu-id="e9da0-143">Нет.</span><span class="sxs-lookup"><span data-stu-id="e9da0-143">No.</span></span> <span data-ttu-id="e9da0-144">Вашей текущей репликации продолжается без перерыва во время и после обновления hello.</span><span class="sxs-lookup"><span data-stu-id="e9da0-144">Your ongoing replication continues uninterrupted during and after hello upgrade.</span></span>

<span data-ttu-id="e9da0-145">**Что происходит toonetwork параметров, таких как параметры виртуальной частной сети и IP-сайт сайт?**</span><span class="sxs-lookup"><span data-stu-id="e9da0-145">**What happens toonetwork settings such as site-to-site VPN and IP settings?**</span></span>

<span data-ttu-id="e9da0-146">Обновление Hello не влияет на параметры сети hello.</span><span class="sxs-lookup"><span data-stu-id="e9da0-146">hello upgrade doesn't affect hello network settings.</span></span> <span data-ttu-id="e9da0-147">Все подключения Azure к локальной среде не меняются.</span><span class="sxs-lookup"><span data-stu-id="e9da0-147">All Azure-to-on-premises connections remain intact.</span></span>

<span data-ttu-id="e9da0-148">**Что произойдет toomy хранилищ, если я не планируется tooupgrade в hello ближайшее будущее?**</span><span class="sxs-lookup"><span data-stu-id="e9da0-148">**What happens toomy vaults if I don’t plan tooupgrade in hello near future?**</span></span>

<span data-ttu-id="e9da0-149">Поддержка хранилище Site Recovery на портале Azure старого hello будет считаться устаревшей начиная с сентября 2017 г.</span><span class="sxs-lookup"><span data-stu-id="e9da0-149">Support for Site Recovery vault in hello old Azure portal will be deprecated starting September 2017.</span></span> <span data-ttu-id="e9da0-150">Настоятельно рекомендуется использовать новый портал toohello toomove hello функций обновления.</span><span class="sxs-lookup"><span data-stu-id="e9da0-150">We strongly recommend that you use hello upgrade feature toomove toohello new portal.</span></span>

<span data-ttu-id="e9da0-151">**Как изменятся существующие средства с этим планом миграции?**</span><span class="sxs-lookup"><span data-stu-id="e9da0-151">**What does this migration plan mean for my existing tooling?**</span></span>  

<span data-ttu-id="e9da0-152">Обновление модели развертывания диспетчера ресурсов toohello инструменты — hello наиболее важные изменения, которые необходимо учитывать в планы обновления.</span><span class="sxs-lookup"><span data-stu-id="e9da0-152">Updating your tooling toohello Resource Manager deployment model is one of hello most important changes that you must account for in your upgrade plans.</span></span> <span data-ttu-id="e9da0-153">Hello хранилищами служб восстановления основаны на модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="e9da0-153">hello Recovery Services vaults are based on hello Resource Manager deployment model.</span></span> 

<span data-ttu-id="e9da0-154">**Как долго hello плоскости управления простоя последнего?**</span><span class="sxs-lookup"><span data-stu-id="e9da0-154">**How long does hello management-plane downtime last?**</span></span>

<span data-ttu-id="e9da0-155">Обновление Hello обычно занимает около 15 минут too30 и может занять несколько tooa максимального значения одного часа.</span><span class="sxs-lookup"><span data-stu-id="e9da0-155">hello upgrade ordinarily takes about 15 too30 minutes, and it could take up tooa maximum of one hour.</span></span>

<span data-ttu-id="e9da0-156">**Возможен ли откат после обновления?**</span><span class="sxs-lookup"><span data-stu-id="e9da0-156">**Can I roll back after upgrading?**</span></span>

<span data-ttu-id="e9da0-157">Нет.</span><span class="sxs-lookup"><span data-stu-id="e9da0-157">No.</span></span> <span data-ttu-id="e9da0-158">Откат не поддерживается после hello ресурсы были успешно обновлены.</span><span class="sxs-lookup"><span data-stu-id="e9da0-158">Rollback is not supported after hello resources have been successfully upgraded.</span></span>

<span data-ttu-id="e9da0-159">**Можно ли проверить Мои подписки или ресурсы toosee ли они могут быть обновлены?**</span><span class="sxs-lookup"><span data-stu-id="e9da0-159">**Can I validate my subscription or resources toosee whether they can be upgraded?**</span></span>

<span data-ttu-id="e9da0-160">Да.</span><span class="sxs-lookup"><span data-stu-id="e9da0-160">Yes.</span></span> <span data-ttu-id="e9da0-161">В hello поддерживается платформой вариант обновления, а hello первым этапом обновления hello является toovalidate, ресурсы hello поддерживает обновление.</span><span class="sxs-lookup"><span data-stu-id="e9da0-161">In hello platform-supported upgrade option, hello first step in hello upgrade is toovalidate that hello resources are capable of an upgrade.</span></span> <span data-ttu-id="e9da0-162">При сбое проверки hello, вы получите соответствующие сообщения об ошибках или предупреждений.</span><span class="sxs-lookup"><span data-stu-id="e9da0-162">If hello validation fails, you will receive appropriate error messages or warnings.</span></span>

<span data-ttu-id="e9da0-163">**Как сообщать проблемы с обновлением hello?**</span><span class="sxs-lookup"><span data-stu-id="e9da0-163">**How do I report an issue with hello upgrade?**</span></span>

<span data-ttu-id="e9da0-164">При возникновении каких-либо ошибок во время обновления hello, обратите внимание, идентификатор операции hello, перечисленные в hello ошибки.</span><span class="sxs-lookup"><span data-stu-id="e9da0-164">If you experience any failures during hello upgrade, note hello operation ID that's listed in hello error.</span></span> <span data-ttu-id="e9da0-165">Поддержка Microsoft заранее будет работать по устранению проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="e9da0-165">Microsoft Support will proactively work on resolving hello issue.</span></span> <span data-ttu-id="e9da0-166">Вы также можете связаться hello специалистам службы поддержки ваш идентификатор подписки, имя хранилища и идентификатором операции.</span><span class="sxs-lookup"><span data-stu-id="e9da0-166">You can also contact hello Support team with your subscription ID, vault name, and operation ID.</span></span> <span data-ttu-id="e9da0-167">Поддержка будет работать tooresolve hello проблему как можно быстрее.</span><span class="sxs-lookup"><span data-stu-id="e9da0-167">Support will work tooresolve hello issue as quickly as possible.</span></span> <span data-ttu-id="e9da0-168">Не пытайтесь выполнить повторно операцию hello, пока не будет явно соответствии toodo так корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="e9da0-168">Do not retry hello operation unless you are explicitly instructed toodo so by Microsoft.</span></span>

## <a name="run-hello-script"></a><span data-ttu-id="e9da0-169">Запустите сценарий hello</span><span class="sxs-lookup"><span data-stu-id="e9da0-169">Run hello script</span></span>

<span data-ttu-id="e9da0-170">В PowerShell запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e9da0-170">In PowerShell, run hello following command:</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* <span data-ttu-id="e9da0-171">SubscriptionID: идентификатор подписки hello, связанной с хранилищем hello, обновлении.</span><span class="sxs-lookup"><span data-stu-id="e9da0-171">SubscriptionID: hello subscription ID that's associated with hello vault that you're upgrading.</span></span>

* <span data-ttu-id="e9da0-172">VaultName: имя hello hello хранилища, которое вы осуществили обновление.</span><span class="sxs-lookup"><span data-stu-id="e9da0-172">VaultName: hello name of hello vault that you're upgrading.</span></span>

* <span data-ttu-id="e9da0-173">Расположение: hello расположение хранилища hello, которое вы осуществили обновление.</span><span class="sxs-lookup"><span data-stu-id="e9da0-173">Location: hello location of hello vault that you're upgrading.</span></span>

* <span data-ttu-id="e9da0-174">ResourceType. HyperVRecoveryManagerVault для хранилищ Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e9da0-174">ResourceType: HyperVRecoveryManagerVault for Site Recovery vaults.</span></span>

* <span data-ttu-id="e9da0-175">TargetResourceGroupName: hello группы ресурсов, в которую будут hello обновлены разместить toobe хранилища.</span><span class="sxs-lookup"><span data-stu-id="e9da0-175">TargetResourceGroupName: hello resource group into which you want hello upgraded vault toobe placed.</span></span> <span data-ttu-id="e9da0-176">TargetResourceGroupName может быть имеющейся группой ресурсов Azure Resource Manager или новой.</span><span class="sxs-lookup"><span data-stu-id="e9da0-176">TargetResourceGroupName can be an existing resource group in Azure Resource Manager or a new one.</span></span> <span data-ttu-id="e9da0-177">Если hello, предоставляемое TargetResourceGroupName не существует, он создается в процессе обновления hello в hello же местоположения, что хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="e9da0-177">If hello TargetResourceGroupName that's supplied does not exist, it is created as part of hello upgrade in hello same location as hello vault.</span></span> <span data-ttu-id="e9da0-178">Дополнительные сведения см. раздел «Группы ресурсов» hello [Обзор диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="e9da0-178">For more information, see hello "Resource groups" section of [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

    >[!NOTE]
    ><span data-ttu-id="e9da0-179">Именование группы ресурсов — тема toocertain ограничения.</span><span class="sxs-lookup"><span data-stu-id="e9da0-179">Resource group naming is subject toocertain constraints.</span></span> <span data-ttu-id="e9da0-180">хранилище tooprevent сбой при обновлении, быть тщательно убедиться, что hello tooobserve соглашение об именовании.</span><span class="sxs-lookup"><span data-stu-id="e9da0-180">tooprevent vault upgrade failure, be sure tooobserve hello naming convention carefully.</span></span>
    >
    ><span data-ttu-id="e9da0-181">Например:</span><span class="sxs-lookup"><span data-stu-id="e9da0-181">For example:</span></span>
    >
    ><span data-ttu-id="e9da0-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span><span class="sxs-lookup"><span data-stu-id="e9da0-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span></span>

<span data-ttu-id="e9da0-183">Кроме того можно запустить следующий сценарий hello.</span><span class="sxs-lookup"><span data-stu-id="e9da0-183">Alternatively, you can run hello following script.</span></span> <span data-ttu-id="e9da0-184">Введите значения hello hello необходимые параметры.</span><span class="sxs-lookup"><span data-stu-id="e9da0-184">Enter hello values for hello required parameters.</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for hello following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. <span data-ttu-id="e9da0-185">Hello сценарий PowerShell предлагает вам tooenter учетные данные.</span><span class="sxs-lookup"><span data-stu-id="e9da0-185">hello PowerShell script prompts you tooenter your credentials.</span></span> <span data-ttu-id="e9da0-186">Введите их дважды, один раз для hello классическое развертывание модели учетной записи и один раз для hello учетной записи диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="e9da0-186">Enter them twice, once for hello classic deployment model account and once for hello Azure Resource Manager account.</span></span>

2. <span data-ttu-id="e9da0-187">После ввода учетных данных, скрипт hello выполняется toodetermine проверка ли вашей инфраструктуры установки соответствует hello упомянутых выше требованиям.</span><span class="sxs-lookup"><span data-stu-id="e9da0-187">After you've entered your credentials, hello script runs a check toodetermine whether your infrastructure setup meets hello previously mentioned requirements.</span></span>

3. <span data-ttu-id="e9da0-188">После проверки и подтверждения предварительные требования hello все запрашиваемые tooproceed с обновлением хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="e9da0-188">After hello prerequisites have been checked and confirmed, you are prompted tooproceed with hello vault upgrade.</span></span> <span data-ttu-id="e9da0-189">процесс обновления Hello запускает обновление вашего хранилища.</span><span class="sxs-lookup"><span data-stu-id="e9da0-189">hello upgrade process starts upgrading your vault.</span></span> <span data-ttu-id="e9da0-190">Hello всего обновления может занять 15 toocomplete too30 минут.</span><span class="sxs-lookup"><span data-stu-id="e9da0-190">hello entire upgrade can take 15 too30 minutes toocomplete.</span></span>

4. <span data-ttu-id="e9da0-191">После успешного завершения обновления hello, можно получить доступ к hello обновленного хранилища в новый портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e9da0-191">After hello upgrade has been completed successfully, you can access hello upgraded vault in hello new Azure portal.</span></span>

## <a name="post-upgrade-vault-management"></a><span data-ttu-id="e9da0-192">Управление хранилищем после обновления</span><span class="sxs-lookup"><span data-stu-id="e9da0-192">Post-upgrade vault management</span></span>

### <a name="replicate-by-using-azure-site-recovery-in-hello-recovery-services-vault"></a><span data-ttu-id="e9da0-193">Репликация с помощью Azure Site Recovery в hello в хранилище службы восстановления</span><span class="sxs-lookup"><span data-stu-id="e9da0-193">Replicate by using Azure Site Recovery in hello Recovery Services vault</span></span>

* <span data-ttu-id="e9da0-194">Виртуальные машины Azure теперь можно защитить от tooanother одного региона.</span><span class="sxs-lookup"><span data-stu-id="e9da0-194">You can now protect your Azure VMs from one region tooanother.</span></span> <span data-ttu-id="e9da0-195">Дополнительные сведения см. в статье [Репликация виртуальных машин Azure между регионами с помощью Azure Site Recovery](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="e9da0-195">For more information, see [Replicate Azure VMs between regions with Azure Site Recovery](site-recovery-azure-to-azure.md).</span></span>

* <span data-ttu-id="e9da0-196">Дополнительные сведения о репликации виртуальных машин VMware tooAzure см. в разделе [tooAzure реплицировать виртуальные машины VMware с Site Recovery](vmware-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e9da0-196">For more information about replicating VMware VMs tooAzure, see [Replicate VMware VMs tooAzure with Site Recovery](vmware-walkthrough-overview.md).</span></span>

* <span data-ttu-id="e9da0-197">Дополнительные сведения о репликации tooAzure виртуальных машин Hyper-V (без VMM) см. в разделе [tooAzure виртуальных машин (без VMM) реплицировать Hyper-V](hyper-v-site-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e9da0-197">For more information about replicating Hyper-V VMs (without VMM) tooAzure, see [Replicate Hyper-V virtual machines (without VMM) tooAzure](hyper-v-site-walkthrough-overview.md).</span></span>

* <span data-ttu-id="e9da0-198">Дополнительные сведения о репликации tooAzure виртуальных машин Hyper-V (с помощью VMM) см. в разделе [репликации Hyper-V виртуальных машин в tooAzure облака VMM, с помощью Site Recovery в hello портал Azure](vmm-to-azure-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e9da0-198">For more information about replicating Hyper-V VMs (with VMM) tooAzure, see [Replicate Hyper-V virtual machines in VMM clouds tooAzure using Site Recovery in hello Azure portal](vmm-to-azure-walkthrough-overview.md).</span></span>

* <span data-ttu-id="e9da0-199">Дополнительные сведения о репликации виртуальных машин Hyper (с помощью VMM) tooa вторичного сайта см. в разделе [Здравствуйте, репликацию Hyper-V виртуальных машин в VMM облаков tooa вторичных VMM узел с помощью портала Azure](site-recovery-vmm-to-vmm.md).</span><span class="sxs-lookup"><span data-stu-id="e9da0-199">For more information about replicating Hyper-VMs (with VMM) tooa secondary site, see [Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site using hello Azure portal](site-recovery-vmm-to-vmm.md).</span></span>

* <span data-ttu-id="e9da0-200">Дополнительные сведения о репликации виртуальных машин VMware tooa вторичного сайта см. в разделе [Replicate локальных виртуальных машин VMware или физическими серверами tooa вторичного сайта на классическом портале Azure hello](site-recovery-vmware-to-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="e9da0-200">For more information about replicating VMware VMs tooa secondary site, see [Replicate on-premises VMware virtual machines or physical servers tooa secondary site in hello classic Azure portal](site-recovery-vmware-to-vmware.md).</span></span>

### <a name="view-your-replicated-items"></a><span data-ttu-id="e9da0-201">Просмотр реплицированных элементов</span><span class="sxs-lookup"><span data-stu-id="e9da0-201">View your replicated items</span></span>

<span data-ttu-id="e9da0-202">Hello следующем рисунке показана страница панели мониторинга хранилища служб восстановления hello, отображающий ключа сущности для hello хранилища.</span><span class="sxs-lookup"><span data-stu-id="e9da0-202">hello following image shows hello Recovery Services vault dashboard page that displays key entities for hello vault.</span></span> <span data-ttu-id="e9da0-203">Выберите список защищенные объекты в хранилище hello tooview **Site Recovery** > **реплицируются элементы**.</span><span class="sxs-lookup"><span data-stu-id="e9da0-203">tooview a list of protected entities in hello vault, select **Site Recovery** > **Replicated items**.</span></span>


![Реплицированные элементы](./media/upgrade-site-recovery-vaults/replicateditems.png)

<span data-ttu-id="e9da0-205">Hello следующем рисунке показан hello рабочий процесс для просмотра вашего реплицированные элементы и hello **перехода на другой ресурс** команду для запуска отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="e9da0-205">hello following image shows hello workflow for viewing your replicated items and hello **Failover** command for initiating a failover.</span></span>

![Реплицированные элементы](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a><span data-ttu-id="e9da0-207">Просмотр параметров репликации</span><span class="sxs-lookup"><span data-stu-id="e9da0-207">View your replication settings</span></span>

<span data-ttu-id="e9da0-208">В хранилище Site Recovery hello каждой группы защиты оснащен частота копирования, хранения точки восстановления, частота моментальных снимков согласованного состояния приложений и другие параметры репликации.</span><span class="sxs-lookup"><span data-stu-id="e9da0-208">In hello Site Recovery vault, each protection group is configured with copy frequency, recovery point retention, frequency of application consistent snapshots, and other replication settings.</span></span> <span data-ttu-id="e9da0-209">В хранилище служб восстановления hello эти параметры настраиваются как политику репликации.</span><span class="sxs-lookup"><span data-stu-id="e9da0-209">In hello Recovery Services vault, these settings are configured as a replication policy.</span></span> <span data-ttu-id="e9da0-210">Hello hello политики называется hello имя группы защиты hello или hello *primarycloud_Policy*.</span><span class="sxs-lookup"><span data-stu-id="e9da0-210">hello name of hello policy is hello name of hello protection group or hello *primarycloud_Policy*.</span></span>

<span data-ttu-id="e9da0-211">Дополнительные сведения о политике репликации см. в разделе [управления политикой репликации для VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="e9da0-211">For more information about replication policy, see [Manage replication policy for VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).</span></span>
