---
title: "Повышение уровня хранилища Site Recovery до хранилища служб восстановления Azure"
description: "Сведения об обновлении хранилища Site Recovery до хранилища служб восстановления Azure"
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
ms.openlocfilehash: fdb33ea0d08353b491f2934fcf885fcb6910b9a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="upgrade-a-site-recovery-vault-to-an-azure-resource-manager-based-recovery-services-vault"></a><span data-ttu-id="10e5b-103">Повышение уровня хранилища Site Recovery до хранилища служб восстановления на основе Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="10e5b-103">Upgrade a Site Recovery vault to an Azure Resource Manager-based Recovery Services vault</span></span>

<span data-ttu-id="10e5b-104">В этой статье описывается обновление хранилищ Azure Site Recovery до хранилищ служб восстановления на основе Azure Resource Manager без влияния на выполняющуюся репликацию.</span><span class="sxs-lookup"><span data-stu-id="10e5b-104">This article describes how to upgrade Azure Site Recovery vaults to Azure Resource Manager-based Recovery Service vaults without any impact on ongoing replication.</span></span> <span data-ttu-id="10e5b-105">Дополнительные сведения о функциях и преимуществах Azure Resource Manager см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="10e5b-105">For more information about Azure Resource Manager features and benefits, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="10e5b-106">Введение</span><span class="sxs-lookup"><span data-stu-id="10e5b-106">Introduction</span></span>
<span data-ttu-id="10e5b-107">Хранилище служб восстановления — это ресурс Azure Resource Manager для управления архивацией и аварийным восстановлением в облаке.</span><span class="sxs-lookup"><span data-stu-id="10e5b-107">A Recovery Services vault is an Azure Resource Manager resource for managing backup and disaster recovery natively in the cloud.</span></span> <span data-ttu-id="10e5b-108">Это единое хранилище, которое можно использовать на новом портале Azure. Это замена классическому резервному хранилищу и хранилищу Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="10e5b-108">It is a unified vault that you can use in the new Azure portal, and it replaces the classic backup and Site Recovery vaults.</span></span>

<span data-ttu-id="10e5b-109">Хранилища служб восстановления предоставляют возможность воспользоваться множеством функций, включая следующие:</span><span class="sxs-lookup"><span data-stu-id="10e5b-109">Recovery Services vaults offer an array of features, including:</span></span>

* <span data-ttu-id="10e5b-110">Поддержка Azure Resource Manager. Вы можете обеспечить защиту и отработку отказа виртуальных машин и физических компьютеров в стеке Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="10e5b-110">Azure Resource Manager support: You can protect and fail over your virtual machines and physical machines into an Azure Resource Manager stack.</span></span>

* <span data-ttu-id="10e5b-111">Исключение диска. Если у вас имеются временные файлы или быстро изменяющиеся данные, на которые вы не хотите использовать пропускную способность в полном объеме, тома можно исключить из репликации.</span><span class="sxs-lookup"><span data-stu-id="10e5b-111">Exclude disk: If you have temp files or high churn data that you don’t want to use all your bandwidth for, you can exclude volumes from replication.</span></span> <span data-ttu-id="10e5b-112">Эта возможность недавно включена в сценарии развертывания *VMware в Azure* и *Hyper-V в Azure*, а также распространяется на другие сценарии.</span><span class="sxs-lookup"><span data-stu-id="10e5b-112">This capability has been enabled currently in *VMware to Azure* and *Hyper-V to Azure* and is extended to other scenarios as well.</span></span>

* <span data-ttu-id="10e5b-113">Поддержка для хранилища класса Premium и локально избыточного хранилища. Теперь защиту серверов можно обеспечить в учетных записях хранения класса Premium, которые позволяют защитить приложения с высокой скоростью выполнения операций ввода-вывода в секунду.</span><span class="sxs-lookup"><span data-stu-id="10e5b-113">Support for premium and locally redundant storage: You can now protect servers in premium storage accounts that allow customers to protect applications with higher input/output operations per second (IOPS).</span></span> <span data-ttu-id="10e5b-114">В настоящее время эта возможность включена в сценарий развертывания *VMware в Azure*.</span><span class="sxs-lookup"><span data-stu-id="10e5b-114">This capability is currently enabled in *VMware to Azure*.</span></span>

* <span data-ttu-id="10e5b-115">Оптимизация начала работы. Теперь, когда вы приступаете к работе, у вас есть дополнительные возможности, которые помогут упростить настройку аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="10e5b-115">Streamlined getting-started experience: The enhanced getting-started experience has been designed to make disaster-recovery setup easy.</span></span>

* <span data-ttu-id="10e5b-116">Управление архивацией и Site Recovery из одного хранилища. Теперь вы можете обеспечить защиту серверов для аварийного восстановления или выполнить архивацию в одном хранилище и значительно снизить расходы на управление.</span><span class="sxs-lookup"><span data-stu-id="10e5b-116">Backup and Site Recovery management from the same vault: You can now protect servers for disaster recovery or perform backup from the same vault, which can reduce your management overhead significantly.</span></span>

<span data-ttu-id="10e5b-117">Дополнительные сведения о новых функциях и возможностях см. в записи блога [Azure Site Recovery now has a simplified experience plus support for ARM and CSP](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/) (Упрощение работы в Azure Site Recovery и поддержка ARM и CSP).</span><span class="sxs-lookup"><span data-stu-id="10e5b-117">For more information about the upgraded experience and features, see the [Storage, Backup, and Recovery blog](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span></span>

## <a name="salient-features"></a><span data-ttu-id="10e5b-118">Ключевые возможности</span><span class="sxs-lookup"><span data-stu-id="10e5b-118">Salient features</span></span>

* <span data-ttu-id="10e5b-119">Отсутствие влияния на выполняющуюся репликацию. Выполняющаяся репликация продолжается без перерывов во время и после обновления.</span><span class="sxs-lookup"><span data-stu-id="10e5b-119">No impact on ongoing replication: Ongoing replications continue without any interruption during and post upgrade.</span></span>

* <span data-ttu-id="10e5b-120">Отсутствие дополнительных затрат. Воспользуйтесь полным набором новых возможностей без дополнительных затрат.</span><span class="sxs-lookup"><span data-stu-id="10e5b-120">No additional cost: Get an entire set of updated capabilities at no additional cost.</span></span>

* <span data-ttu-id="10e5b-121">Сохранение данных. Так как это обновление, а не миграция, имеющиеся параметры и точки восстановления репликации остаются неизменными во время и после обновления.</span><span class="sxs-lookup"><span data-stu-id="10e5b-121">No data loss: Because this process is an upgrade and not a migration, existing replication recovery points and settings remain intact during and after the upgrade.</span></span>


## <a name="what-happens-during-the-vault-upgrade"></a><span data-ttu-id="10e5b-122">Что происходит во время обновления хранилища?</span><span class="sxs-lookup"><span data-stu-id="10e5b-122">What happens during the vault upgrade?</span></span>

<span data-ttu-id="10e5b-123">Во время обновления нельзя выполнять такие операции, как регистрация нового сервера и включение репликации для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="10e5b-123">During the upgrade, you cannot perform operations such as registering a new server or enabling replication for a virtual machine (VM).</span></span> <span data-ttu-id="10e5b-124">Операции, предполагающие считывание или запись данных в хранилище, например репликация защищенных элементов в хранилище, продолжают выполняться без перерывов.</span><span class="sxs-lookup"><span data-stu-id="10e5b-124">Operations that involve reading data from or writing data to the vault, such as ongoing replication of protected items to the vault, continue uninterrupted.</span></span>

### <a name="changes-to-automation-and-tooling-after-the-upgrade"></a><span data-ttu-id="10e5b-125">Изменение возможностей автоматизации и инструментария после обновления</span><span class="sxs-lookup"><span data-stu-id="10e5b-125">Changes to automation and tooling after the upgrade</span></span>
<span data-ttu-id="10e5b-126">После обновления типа хранилища с классической модели на модель развертывания с помощью Resource Manager обновите существующую службу автоматизации или инструментарий, чтобы обеспечить их работу после обновления.</span><span class="sxs-lookup"><span data-stu-id="10e5b-126">As you upgrade the vault type from the classic deployment model to the Resource Manager deployment model, update the existing automation or tooling to ensure that it continues to work after the upgrade.</span></span>

### <a name="prepare-your-environment-for-the-upgrade"></a><span data-ttu-id="10e5b-127">Подготовка среды к обновлению</span><span class="sxs-lookup"><span data-stu-id="10e5b-127">Prepare your environment for the upgrade</span></span>

* [<span data-ttu-id="10e5b-128">Установите PowerShell или обновите ее до версии 5 или более поздней</span><span class="sxs-lookup"><span data-stu-id="10e5b-128">Install PowerShell or upgrade it to version 5 or later</span></span>](https://www.microsoft.com/download/details.aspx?id=50395)
* [<span data-ttu-id="10e5b-129">Установите последнюю версию Azure PowerShell MSI</span><span class="sxs-lookup"><span data-stu-id="10e5b-129">Install the latest version of Azure PowerShell MSI</span></span>](https://github.com/Azure/azure-powershell/releases)
* [<span data-ttu-id="10e5b-130">Скачайте скрипт для обновления хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="10e5b-130">Download the Recovery Services vault upgrade script</span></span>](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a><span data-ttu-id="10e5b-131">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="10e5b-131">Prerequisites</span></span>
<span data-ttu-id="10e5b-132">Для обновления хранилищ Site Recovery до хранилищ службы восстановления на основе Azure Resource Manager выполните следующие предварительные требования.</span><span class="sxs-lookup"><span data-stu-id="10e5b-132">To upgrade from Site Recovery vaults to Azure Resource Manager-based Recovery Service vaults, you must meet the following requirements:</span></span>

* <span data-ttu-id="10e5b-133">Минимальная версия агента. Требуется установить на сервере поставщик Azure Site Recovery версии 5.1.1700.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="10e5b-133">Minimum agent version: The version of Azure Site Recovery Provider installed on your server must be 5.1.1700.0 or later.</span></span>

* <span data-ttu-id="10e5b-134">Поддерживаемая конфигурация. Не настраивайте для хранилища сеть SAN и группы доступности AlwaysOn SQL Server.</span><span class="sxs-lookup"><span data-stu-id="10e5b-134">Supported configuration: You cannot configure your vault with storage area network (SAN) or SQL Server AlwaysOn Availability Groups.</span></span> <span data-ttu-id="10e5b-135">Остальные конфигурации поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="10e5b-135">All other configurations are supported.</span></span>

    >[!NOTE]
    ><span data-ttu-id="10e5b-136">После обновления управлять сопоставлением хранилища можно только с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="10e5b-136">After the upgrade, you can manage storage mapping only via PowerShell.</span></span>

* <span data-ttu-id="10e5b-137">Поддерживаемый сценарий развертывания. В вашем хранилище не должна быть реализована старая модель развертывания *VMware в Azure*.</span><span class="sxs-lookup"><span data-stu-id="10e5b-137">Supported deployment scenario: Your vault shouldn’t be the *VMware to Azure* legacy deployment model.</span></span> <span data-ttu-id="10e5b-138">Прежде чем продолжить, перейдите к расширенной модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="10e5b-138">Before you proceed, first move to the enhanced deployment model.</span></span>

* <span data-ttu-id="10e5b-139">Отсутствие активных заданий, инициированных пользователем, включающих операции на плоскости управления. Так как во время обновления доступ к плоскости управления ограничен, необходимо завершить все операции плоскости управления, прежде чем активировать обновление.</span><span class="sxs-lookup"><span data-stu-id="10e5b-139">No active user-initiated jobs that involve management plane operations: Because access to the management plane is restricted during upgrade, complete all your management plane actions before you trigger the upgrade.</span></span> <span data-ttu-id="10e5b-140">Этот процесс не касается выполняющейся репликации.</span><span class="sxs-lookup"><span data-stu-id="10e5b-140">This process doesn’t include ongoing replication.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="10e5b-141">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="10e5b-141">Frequently asked questions</span></span>

<span data-ttu-id="10e5b-142">**Влияет ли обновление на выполняющуюся репликацию?**</span><span class="sxs-lookup"><span data-stu-id="10e5b-142">**Does this upgrade affect my ongoing replication?**</span></span>

<span data-ttu-id="10e5b-143">Нет.</span><span class="sxs-lookup"><span data-stu-id="10e5b-143">No.</span></span> <span data-ttu-id="10e5b-144">Во время и после обновления репликация продолжается без перерыва.</span><span class="sxs-lookup"><span data-stu-id="10e5b-144">Your ongoing replication continues uninterrupted during and after the upgrade.</span></span>

<span data-ttu-id="10e5b-145">**Что происходит с параметрами сети (VPN типа "сеть — сеть", параметры IP-адресов)?**</span><span class="sxs-lookup"><span data-stu-id="10e5b-145">**What happens to network settings such as site-to-site VPN and IP settings?**</span></span>

<span data-ttu-id="10e5b-146">Обновление не влияет на параметры сети.</span><span class="sxs-lookup"><span data-stu-id="10e5b-146">The upgrade doesn't affect the network settings.</span></span> <span data-ttu-id="10e5b-147">Все подключения Azure к локальной среде не меняются.</span><span class="sxs-lookup"><span data-stu-id="10e5b-147">All Azure-to-on-premises connections remain intact.</span></span>

<span data-ttu-id="10e5b-148">**Что произойдет с моими хранилищами, если я не планирую обновление в ближайшем будущем?**</span><span class="sxs-lookup"><span data-stu-id="10e5b-148">**What happens to my vaults if I don’t plan to upgrade in the near future?**</span></span>

<span data-ttu-id="10e5b-149">Начиная с сентября 2017 года будет прекращена поддержка хранилища Site Recovery на старом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="10e5b-149">Support for Site Recovery vault in the old Azure portal will be deprecated starting September 2017.</span></span> <span data-ttu-id="10e5b-150">Мы настоятельно рекомендуем использовать функцию обновления для перехода к новому порталу.</span><span class="sxs-lookup"><span data-stu-id="10e5b-150">We strongly recommend that you use the upgrade feature to move to the new portal.</span></span>

<span data-ttu-id="10e5b-151">**Как изменятся существующие средства с этим планом миграции?**</span><span class="sxs-lookup"><span data-stu-id="10e5b-151">**What does this migration plan mean for my existing tooling?**</span></span>  

<span data-ttu-id="10e5b-152">Одним из важнейших изменений, которое следует учесть в плане обновления, является обновление набора инструментов до модели развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="10e5b-152">Updating your tooling to the Resource Manager deployment model is one of the most important changes that you must account for in your upgrade plans.</span></span> <span data-ttu-id="10e5b-153">Хранилища служб восстановления созданы на основе модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="10e5b-153">The Recovery Services vaults are based on the Resource Manager deployment model.</span></span> 

<span data-ttu-id="10e5b-154">**Сколько времени продлится простой плоскости управления?**</span><span class="sxs-lookup"><span data-stu-id="10e5b-154">**How long does the management-plane downtime last?**</span></span>

<span data-ttu-id="10e5b-155">Обновление обычно длится от 15 до 30 минут, но не более часа.</span><span class="sxs-lookup"><span data-stu-id="10e5b-155">The upgrade ordinarily takes about 15 to 30 minutes, and it could take up to a maximum of one hour.</span></span>

<span data-ttu-id="10e5b-156">**Возможен ли откат после обновления?**</span><span class="sxs-lookup"><span data-stu-id="10e5b-156">**Can I roll back after upgrading?**</span></span>

<span data-ttu-id="10e5b-157">Нет.</span><span class="sxs-lookup"><span data-stu-id="10e5b-157">No.</span></span> <span data-ttu-id="10e5b-158">Откат после успешного обновления ресурсов не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="10e5b-158">Rollback is not supported after the resources have been successfully upgraded.</span></span>

<span data-ttu-id="10e5b-159">**Можно ли проверить подписку или ресурсы, чтобы узнать, подходят ли они для обновления?**</span><span class="sxs-lookup"><span data-stu-id="10e5b-159">**Can I validate my subscription or resources to see whether they can be upgraded?**</span></span>

<span data-ttu-id="10e5b-160">Да.</span><span class="sxs-lookup"><span data-stu-id="10e5b-160">Yes.</span></span> <span data-ttu-id="10e5b-161">Первый шаг при обновлении с поддержкой платформы — убедиться, что ресурсы поддерживают обновление.</span><span class="sxs-lookup"><span data-stu-id="10e5b-161">In the platform-supported upgrade option, the first step in the upgrade is to validate that the resources are capable of an upgrade.</span></span> <span data-ttu-id="10e5b-162">В случае сбоя проверки отобразятся соответствующие сообщения об ошибке или предупреждения.</span><span class="sxs-lookup"><span data-stu-id="10e5b-162">If the validation fails, you will receive appropriate error messages or warnings.</span></span>

<span data-ttu-id="10e5b-163">**Как сообщить о проблеме с обновлением?**</span><span class="sxs-lookup"><span data-stu-id="10e5b-163">**How do I report an issue with the upgrade?**</span></span>

<span data-ttu-id="10e5b-164">Если вы столкнулись с какими-либо сбоями во время обновления, запишите идентификатор операции, указанный в сообщении об ошибке.</span><span class="sxs-lookup"><span data-stu-id="10e5b-164">If you experience any failures during the upgrade, note the operation ID that's listed in the error.</span></span> <span data-ttu-id="10e5b-165">Служба поддержки Майкрософт примет профилактические меры для устранения этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="10e5b-165">Microsoft Support will proactively work on resolving the issue.</span></span> <span data-ttu-id="10e5b-166">Вы можете обратиться в службу поддержки, указав идентификатор подписки, имя хранилища и идентификатор операции.</span><span class="sxs-lookup"><span data-stu-id="10e5b-166">You can also contact the Support team with your subscription ID, vault name, and operation ID.</span></span> <span data-ttu-id="10e5b-167">Служба поддержки попробует устранить проблему как можно быстрее.</span><span class="sxs-lookup"><span data-stu-id="10e5b-167">Support will work to resolve the issue as quickly as possible.</span></span> <span data-ttu-id="10e5b-168">Не повторяйте операцию, если это явно не указано в инструкциях корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="10e5b-168">Do not retry the operation unless you are explicitly instructed to do so by Microsoft.</span></span>

## <a name="run-the-script"></a><span data-ttu-id="10e5b-169">Запуск сценария</span><span class="sxs-lookup"><span data-stu-id="10e5b-169">Run the script</span></span>

<span data-ttu-id="10e5b-170">Выполните следующую команду в PowerShell:</span><span class="sxs-lookup"><span data-stu-id="10e5b-170">In PowerShell, run the following command:</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* <span data-ttu-id="10e5b-171">SubscriptionID. Идентификатор подписки, связанный с обновляемым хранилищем.</span><span class="sxs-lookup"><span data-stu-id="10e5b-171">SubscriptionID: The subscription ID that's associated with the vault that you're upgrading.</span></span>

* <span data-ttu-id="10e5b-172">VaultName. Имя обновляемого хранилища.</span><span class="sxs-lookup"><span data-stu-id="10e5b-172">VaultName: The name of the vault that you're upgrading.</span></span>

* <span data-ttu-id="10e5b-173">Location. Расположение обновляемого хранилища.</span><span class="sxs-lookup"><span data-stu-id="10e5b-173">Location: The location of the vault that you're upgrading.</span></span>

* <span data-ttu-id="10e5b-174">ResourceType. HyperVRecoveryManagerVault для хранилищ Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="10e5b-174">ResourceType: HyperVRecoveryManagerVault for Site Recovery vaults.</span></span>

* <span data-ttu-id="10e5b-175">TargetResourceGroupName. Группа ресурсов, в которую будет помещено обновленное хранилище.</span><span class="sxs-lookup"><span data-stu-id="10e5b-175">TargetResourceGroupName: The resource group into which you want the upgraded vault to be placed.</span></span> <span data-ttu-id="10e5b-176">TargetResourceGroupName может быть имеющейся группой ресурсов Azure Resource Manager или новой.</span><span class="sxs-lookup"><span data-stu-id="10e5b-176">TargetResourceGroupName can be an existing resource group in Azure Resource Manager or a new one.</span></span> <span data-ttu-id="10e5b-177">Если указанное значение TargetResourceGroupName не существует, оно создается в рамках обновления в том же расположении, что и хранилище.</span><span class="sxs-lookup"><span data-stu-id="10e5b-177">If the TargetResourceGroupName that's supplied does not exist, it is created as part of the upgrade in the same location as the vault.</span></span> <span data-ttu-id="10e5b-178">Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="10e5b-178">For more information, see the "Resource groups" section of [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

    >[!NOTE]
    ><span data-ttu-id="10e5b-179">Имена групп ресурсов имеют определенные ограничения.</span><span class="sxs-lookup"><span data-stu-id="10e5b-179">Resource group naming is subject to certain constraints.</span></span> <span data-ttu-id="10e5b-180">Для предотвращения сбоя обновления хранилища следуйте соглашению об именовании.</span><span class="sxs-lookup"><span data-stu-id="10e5b-180">To prevent vault upgrade failure, be sure to observe the naming convention carefully.</span></span>
    >
    ><span data-ttu-id="10e5b-181">Например:</span><span class="sxs-lookup"><span data-stu-id="10e5b-181">For example:</span></span>
    >
    ><span data-ttu-id="10e5b-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span><span class="sxs-lookup"><span data-stu-id="10e5b-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span></span>

<span data-ttu-id="10e5b-183">Также можно выполнить следующий скрипт.</span><span class="sxs-lookup"><span data-stu-id="10e5b-183">Alternatively, you can run the following script.</span></span> <span data-ttu-id="10e5b-184">Введите значения обязательных параметров.</span><span class="sxs-lookup"><span data-stu-id="10e5b-184">Enter the values for the required parameters.</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for the following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. <span data-ttu-id="10e5b-185">Сценарий PowerShell предложит ввести учетные данные.</span><span class="sxs-lookup"><span data-stu-id="10e5b-185">The PowerShell script prompts you to enter your credentials.</span></span> <span data-ttu-id="10e5b-186">Введите их дважды — для учетной записи классической модели развертывания и учетной записи Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="10e5b-186">Enter them twice, once for the classic deployment model account and once for the Azure Resource Manager account.</span></span>

2. <span data-ttu-id="10e5b-187">После ввода учетных данных скрипт запустит проверку, чтобы убедиться, что настройка инфраструктуры соответствует необходимым требованиям, упомянутым ранее.</span><span class="sxs-lookup"><span data-stu-id="10e5b-187">After you've entered your credentials, the script runs a check to determine whether your infrastructure setup meets the previously mentioned requirements.</span></span>

3. <span data-ttu-id="10e5b-188">После успешной проверки вам будет предложено продолжить обновление хранилища.</span><span class="sxs-lookup"><span data-stu-id="10e5b-188">After the prerequisites have been checked and confirmed, you are prompted to proceed with the vault upgrade.</span></span> <span data-ttu-id="10e5b-189">Процесс обновления начнет обновление хранилища.</span><span class="sxs-lookup"><span data-stu-id="10e5b-189">The upgrade process starts upgrading your vault.</span></span> <span data-ttu-id="10e5b-190">Обновление может занять от 15 до 30 минут.</span><span class="sxs-lookup"><span data-stu-id="10e5b-190">The entire upgrade can take 15 to 30 minutes to complete.</span></span>

4. <span data-ttu-id="10e5b-191">По завершении обновления можно войти в обновленное хранилище на новом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="10e5b-191">After the upgrade has been completed successfully, you can access the upgraded vault in the new Azure portal.</span></span>

## <a name="post-upgrade-vault-management"></a><span data-ttu-id="10e5b-192">Управление хранилищем после обновления</span><span class="sxs-lookup"><span data-stu-id="10e5b-192">Post-upgrade vault management</span></span>

### <a name="replicate-by-using-azure-site-recovery-in-the-recovery-services-vault"></a><span data-ttu-id="10e5b-193">Репликация в хранилище служб восстановления с помощью Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="10e5b-193">Replicate by using Azure Site Recovery in the Recovery Services vault</span></span>

* <span data-ttu-id="10e5b-194">Теперь можно защитить виртуальные машины Azure в разных регионах.</span><span class="sxs-lookup"><span data-stu-id="10e5b-194">You can now protect your Azure VMs from one region to another.</span></span> <span data-ttu-id="10e5b-195">Дополнительные сведения см. в статье [Репликация виртуальных машин Azure между регионами с помощью Azure Site Recovery](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="10e5b-195">For more information, see [Replicate Azure VMs between regions with Azure Site Recovery](site-recovery-azure-to-azure.md).</span></span>

* <span data-ttu-id="10e5b-196">Дополнительные сведения о репликации виртуальных машин VMware в Azure см. в статье [Репликация виртуальных машин VMware в Azure с помощью Site Recovery](vmware-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="10e5b-196">For more information about replicating VMware VMs to Azure, see [Replicate VMware VMs to Azure with Site Recovery](vmware-walkthrough-overview.md).</span></span>

* <span data-ttu-id="10e5b-197">Дополнительные сведения о репликации виртуальных машин Hyper-V (без VMM) в Azure см. в статье [Репликация виртуальных машин Hyper-V (без VMM) в Azure](hyper-v-site-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="10e5b-197">For more information about replicating Hyper-V VMs (without VMM) to Azure, see [Replicate Hyper-V virtual machines (without VMM) to Azure](hyper-v-site-walkthrough-overview.md).</span></span>

* <span data-ttu-id="10e5b-198">Дополнительные сведения о репликации виртуальных машин Hyper-V (с VMM) в Azure см. в статье [Репликация виртуальных машин Hyper-V из облаков VMM в Azure с помощью Site Recovery на портале Azure](vmm-to-azure-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="10e5b-198">For more information about replicating Hyper-V VMs (with VMM) to Azure, see [Replicate Hyper-V virtual machines in VMM clouds to Azure using Site Recovery in the Azure portal](vmm-to-azure-walkthrough-overview.md).</span></span>

* <span data-ttu-id="10e5b-199">Дополнительные сведения о репликации виртуальных машин Hyper-V (с VMM) на дополнительный сайт см. в статье [Репликация виртуальных машин Hyper-V из облаков VMM на вторичный сайт VMM | Microsoft Azure](site-recovery-vmm-to-vmm.md).</span><span class="sxs-lookup"><span data-stu-id="10e5b-199">For more information about replicating Hyper-VMs (with VMM) to a secondary site, see [Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site using the Azure portal](site-recovery-vmm-to-vmm.md).</span></span>

* <span data-ttu-id="10e5b-200">Дополнительные сведения о репликации виртуальных машин VMware на дополнительный сайт см. в статье [Репликация локальных виртуальных машин VMware или физических серверов на вторичный сайт с помощью классического портала Azure](site-recovery-vmware-to-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="10e5b-200">For more information about replicating VMware VMs to a secondary site, see [Replicate on-premises VMware virtual machines or physical servers to a secondary site in the classic Azure portal](site-recovery-vmware-to-vmware.md).</span></span>

### <a name="view-your-replicated-items"></a><span data-ttu-id="10e5b-201">Просмотр реплицированных элементов</span><span class="sxs-lookup"><span data-stu-id="10e5b-201">View your replicated items</span></span>

<span data-ttu-id="10e5b-202">На следующем изображении показана страница панели мониторинга хранилища служб восстановления с ключевыми сущностями для хранилища.</span><span class="sxs-lookup"><span data-stu-id="10e5b-202">The following image shows the Recovery Services vault dashboard page that displays key entities for the vault.</span></span> <span data-ttu-id="10e5b-203">Чтобы просмотреть список защищенных сущностей в хранилище, щелкните **Site Recovery** > **Реплицированные элементы**.</span><span class="sxs-lookup"><span data-stu-id="10e5b-203">To view a list of protected entities in the vault, select **Site Recovery** > **Replicated items**.</span></span>


![Реплицированные элементы](./media/upgrade-site-recovery-vaults/replicateditems.png)

<span data-ttu-id="10e5b-205">На следующем изображении показан рабочий процесс просмотра реплицированных элементов и команда **отработки отказа** для запуска отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="10e5b-205">The following image shows the workflow for viewing your replicated items and the **Failover** command for initiating a failover.</span></span>

![Реплицированные элементы](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a><span data-ttu-id="10e5b-207">Просмотр параметров репликации</span><span class="sxs-lookup"><span data-stu-id="10e5b-207">View your replication settings</span></span>

<span data-ttu-id="10e5b-208">В хранилище Site Recovery для каждой группы защиты настроены частота копирования, хранение точки восстановления, согласованные на уровне приложения моментальные снимки и другие параметры репликации.</span><span class="sxs-lookup"><span data-stu-id="10e5b-208">In the Site Recovery vault, each protection group is configured with copy frequency, recovery point retention, frequency of application consistent snapshots, and other replication settings.</span></span> <span data-ttu-id="10e5b-209">В хранилище служб восстановления эти параметры настраиваются как политика репликации.</span><span class="sxs-lookup"><span data-stu-id="10e5b-209">In the Recovery Services vault, these settings are configured as a replication policy.</span></span> <span data-ttu-id="10e5b-210">Имя политики является именем группы защиты или *primarycloud_Policy*.</span><span class="sxs-lookup"><span data-stu-id="10e5b-210">The name of the policy is the name of the protection group or the *primarycloud_Policy*.</span></span>

<span data-ttu-id="10e5b-211">Дополнительные сведения о политике репликации см. в статье [Управление политикой репликации для VMware в Azure](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="10e5b-211">For more information about replication policy, see [Manage replication policy for VMware to Azure](site-recovery-setup-replication-settings-vmware.md).</span></span>
