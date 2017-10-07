---
title: "aaaMigrate tooResource диспетчера с помощью PowerShell | Документы Microsoft"
description: "Этой статье рассматриваются hello поддерживается платформой миграции ресурсов IaaS, например виртуальные машины (VM), виртуальных сетей (Vnet) и учетные записи хранения из классического tooAzure диспетчера ресурсов (ARM) с помощью команд Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2b3dff9b-2e99-4556-acc5-d75ef234af9c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: b5b2987da292f1c241be71a354b0c2e1a96a07c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-powershell"></a><span data-ttu-id="d4d33-103">Перенос ресурсов IaaS в классическом tooAzure диспетчера ресурсов с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4d33-103">Migrate IaaS resources from classic tooAzure Resource Manager by using Azure PowerShell</span></span>
<span data-ttu-id="d4d33-104">Следующие шаги показывают, как toouse Azure PowerShell команды toomigrate инфраструктуры как услуги (IaaS) ресурсы из hello классической модели toohello диспетчера ресурсов Azure развертывания модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="d4d33-104">These steps show you how toouse Azure PowerShell commands toomigrate infrastructure as a service (IaaS) resources from hello classic deployment model toohello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="d4d33-105">Если требуется, можно переносить ресурсы с помощью hello [интерфейс командной строки Azure (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d4d33-105">If you want, you can also migrate resources by using hello [Azure Command Line Interface (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span></span>

* <span data-ttu-id="d4d33-106">Основные сведения о поддерживаемых сценариев миграции см. в разделе [поддерживаемые платформой миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d4d33-106">For background on supported migration scenarios, see [Platform-supported migration of IaaS resources from classic tooAzure Resource Manager](migration-classic-resource-manager-overview.md).</span></span>
* <span data-ttu-id="d4d33-107">Подробные инструкции и пошаговое руководство по миграции см. в разделе [технические близкое знакомство с платформа поддерживается перенос из классической tooAzure диспетчера ресурсов](migration-classic-resource-manager-deep-dive.md).</span><span class="sxs-lookup"><span data-stu-id="d4d33-107">For detailed guidance and a migration walkthrough, see [Technical deep dive on platform-supported migration from classic tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span></span>
* [<span data-ttu-id="d4d33-108">Распространенные ошибки миграции</span><span class="sxs-lookup"><span data-stu-id="d4d33-108">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md)

<br>
<span data-ttu-id="d4d33-109">Ниже приведен порядок hello tooidentify блок-схемы, в котором действия требуется toobe выполнен во время процесса миграции</span><span class="sxs-lookup"><span data-stu-id="d4d33-109">Here is a flowchart tooidentify hello order in which steps need toobe executed during a migration process</span></span>

![Снимок экрана, показывающий шагов миграции hello](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a><span data-ttu-id="d4d33-111">Шаг 1. Планирование миграции</span><span class="sxs-lookup"><span data-stu-id="d4d33-111">Step 1: Plan for migration</span></span>
<span data-ttu-id="d4d33-112">Вот несколько рекомендаций, рекомендуется при оценке миграции IaaS ресурсов от классических tooResource диспетчера.</span><span class="sxs-lookup"><span data-stu-id="d4d33-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic tooResource Manager:</span></span>

* <span data-ttu-id="d4d33-113">Прочтите hello [поддерживаемые и неподдерживаемые функции и настройки](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d4d33-113">Read through hello [supported and unsupported features and configurations](migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="d4d33-114">При наличии виртуальных машин, использующих неподдерживаемые конфигурации или компоненты, рекомендуется отложить hello конфигурации или компонент поддержки toobe было объявлено.</span><span class="sxs-lookup"><span data-stu-id="d4d33-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for hello configuration/feature support toobe announced.</span></span> <span data-ttu-id="d4d33-115">Кроме того если он соответствует вашим потребностям, удалить эти компоненты или можно вывести из миграции tooenable этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d4d33-115">Alternatively, if it suits your needs, remove that feature or move out of that configuration tooenable migration.</span></span>
* <span data-ttu-id="d4d33-116">Если у вас есть автоматизированные скрипты, которые сегодня развертывание инфраструктуры и приложений, попробуйте toocreate аналогичную программу установки теста с помощью этих скриптов для миграции.</span><span class="sxs-lookup"><span data-stu-id="d4d33-116">If you have automated scripts that deploy your infrastructure and applications today, try toocreate a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="d4d33-117">Кроме того можно настроить образец сред с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d4d33-117">Alternatively, you can set up sample environments by using hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4d33-118">Шлюзы приложений для миграции с классической tooResource Manager в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="d4d33-118">Application Gateways are not currently supported for migration from classic tooResource Manager.</span></span> <span data-ttu-id="d4d33-119">Перед запуском сети hello toomove операции подготовки toomigrate классической виртуальной сети с шлюза приложения, удалить шлюз hello.</span><span class="sxs-lookup"><span data-stu-id="d4d33-119">toomigrate a classic virtual network with an Application gateway, remove hello gateway before running a Prepare operation toomove hello network.</span></span> <span data-ttu-id="d4d33-120">После завершения миграции hello переподключение hello шлюза в диспетчере ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="d4d33-120">After you complete hello migration, reconnect hello gateway in Azure Resource Manager.</span></span>
>
><span data-ttu-id="d4d33-121">Шлюзов ExpressRoute подключение tooExpressRoute цепи в другую подписку невозможно перенести автоматически.</span><span class="sxs-lookup"><span data-stu-id="d4d33-121">ExpressRoute gateways connecting tooExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="d4d33-122">В таких случаях удалить шлюз ExpressRoute hello, миграция виртуальной сети hello и повторного создания шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="d4d33-122">In such cases, remove hello ExpressRoute gateway, migrate hello virtual network and recreate hello gateway.</span></span> <span data-ttu-id="d4d33-123">См. в разделе [перенести ExpressRoute каналов и связанные виртуальные сети из модели развертывания диспетчера ресурсов hello классический toohello](../../expressroute/expressroute-migration-classic-resource-manager.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="d4d33-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from hello classic toohello Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
>
>

## <a name="step-2-install-hello-latest-version-of-azure-powershell"></a><span data-ttu-id="d4d33-124">Шаг 2: Установите последнюю версию Azure PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="d4d33-124">Step 2: Install hello latest version of Azure PowerShell</span></span>
<span data-ttu-id="d4d33-125">Существует два основных варианта tooinstall Azure PowerShell: [коллекции PowerShell](https://www.powershellgallery.com/profiles/azure-sdk/) или [установщика веб-платформы (WebPI)](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="d4d33-125">There are two main options tooinstall Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) or [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="d4d33-126">Обновления для установщика веб-платформы выпускаются ежемесячно.</span><span class="sxs-lookup"><span data-stu-id="d4d33-126">WebPI receives monthly updates.</span></span> <span data-ttu-id="d4d33-127">Обновления для коллекции PowerShell выпускаются на постоянной основе.</span><span class="sxs-lookup"><span data-stu-id="d4d33-127">PowerShell Gallery receives updates on a continuous basis.</span></span> <span data-ttu-id="d4d33-128">В этой статье используется Azure PowerShell 2.1.0.</span><span class="sxs-lookup"><span data-stu-id="d4d33-128">This article is based on Azure PowerShell version 2.1.0.</span></span>

<span data-ttu-id="d4d33-129">Инструкции по установке см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d4d33-129">For installation instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-hello-subscription-in-azure-portal"></a><span data-ttu-id="d4d33-130">Шаг 3: Убедитесь, что вы являетесь администратором для hello подписки на портале Azure</span><span class="sxs-lookup"><span data-stu-id="d4d33-130">Step 3: Ensure that you are an administrator for hello subscription in Azure portal</span></span>
<span data-ttu-id="d4d33-131">tooperform завершения миграции вы должны добавляться как соадминистратора подписки hello в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d4d33-131">tooperform this migration, you must be added as a co-administrator for hello subscription in hello [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="d4d33-132">Вход в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d4d33-132">Sign into hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d4d33-133">Выберите меню концентратора hello **подписки**.</span><span class="sxs-lookup"><span data-stu-id="d4d33-133">On hello Hub menu, select **Subscription**.</span></span> <span data-ttu-id="d4d33-134">Если вы не видите этот пункт, щелкните **Больше служб**.</span><span class="sxs-lookup"><span data-stu-id="d4d33-134">If you don't see it, select **More services**.</span></span>
3. <span data-ttu-id="d4d33-135">Найдите запись hello нужную подписку, а затем просмотрите hello **Мои РОЛИ** поля.</span><span class="sxs-lookup"><span data-stu-id="d4d33-135">Find hello appropriate subscription entry, then look at hello **MY ROLE** field.</span></span> <span data-ttu-id="d4d33-136">Для совместного администратора hello значение должно быть _администратор учетной записи_.</span><span class="sxs-lookup"><span data-stu-id="d4d33-136">For a co-administrator, hello value should be _Account admin_.</span></span>

<span data-ttu-id="d4d33-137">Если вы не могли tooadd соадминистратора, обратитесь администратором служб или соадминистратора для hello подписки tooget самостоятельно добавить.</span><span class="sxs-lookup"><span data-stu-id="d4d33-137">If you are not able tooadd a co-administrator, then contact a service administrator or co-administrator for hello subscription tooget yourself added.</span></span>   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a><span data-ttu-id="d4d33-138">Шаг 4. Настройка подписки и регистрация для миграции</span><span class="sxs-lookup"><span data-stu-id="d4d33-138">Step 4: Set your subscription and sign up for migration</span></span>
<span data-ttu-id="d4d33-139">Сначала запустите командную строку PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d4d33-139">First, start a PowerShell prompt.</span></span> <span data-ttu-id="d4d33-140">Для миграции, необходимо tooset настройку среды для обоих классический и диспетчер ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d4d33-140">For migration, you need tooset up your environment for both classic and Resource Manager.</span></span>

<span data-ttu-id="d4d33-141">Учетная запись tooyour для диспетчера ресурсов модели hello для входа.</span><span class="sxs-lookup"><span data-stu-id="d4d33-141">Sign in tooyour account for hello Resource Manager model.</span></span>

```powershell
    Login-AzureRmAccount
```

<span data-ttu-id="d4d33-142">Получить hello доступные подписки с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d4d33-142">Get hello available subscriptions by using hello following command:</span></span>

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

<span data-ttu-id="d4d33-143">Задайте подписки Azure для hello текущего сеанса.</span><span class="sxs-lookup"><span data-stu-id="d4d33-143">Set your Azure subscription for hello current session.</span></span> <span data-ttu-id="d4d33-144">В этом примере задает hello имя подписки по умолчанию слишком**Моя подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="d4d33-144">This example sets hello default subscription name too**My Azure Subscription**.</span></span> <span data-ttu-id="d4d33-145">Замените имя подписки пример hello свои собственные.</span><span class="sxs-lookup"><span data-stu-id="d4d33-145">Replace hello example subscription name with your own.</span></span>

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> <span data-ttu-id="d4d33-146">Регистрация — однократное действие, но, прежде чем выполнять миграцию, вам нужно зарегистрироваться.</span><span class="sxs-lookup"><span data-stu-id="d4d33-146">Registration is a one-time step, but you must do it once before attempting migration.</span></span> <span data-ttu-id="d4d33-147">Без регистрации, вы видите hello следующие сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="d4d33-147">Without registering, you see hello following error message:</span></span>
>
> <span data-ttu-id="d4d33-148">*Неправильный запрос: Подписка не зарегистрирована для миграции.*</span><span class="sxs-lookup"><span data-stu-id="d4d33-148">*BadRequest : Subscription is not registered for migration.*</span></span>
>
>

<span data-ttu-id="d4d33-149">Зарегистрируйте поставщик ресурсов hello миграции с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d4d33-149">Register with hello migration resource provider by using hello following command:</span></span>

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="d4d33-150">Подождите пять минут для регистрации toofinish hello.</span><span class="sxs-lookup"><span data-stu-id="d4d33-150">Please wait five minutes for hello registration toofinish.</span></span> <span data-ttu-id="d4d33-151">Можно проверить состояние hello hello утверждения с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d4d33-151">You can check hello status of hello approval by using hello following command:</span></span>

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="d4d33-152">Убедитесь, что RegistrationState имеет значение `Registered` , прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="d4d33-152">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

<span data-ttu-id="d4d33-153">Теперь войдите в учетную запись tooyour для hello классической модели.</span><span class="sxs-lookup"><span data-stu-id="d4d33-153">Now sign in tooyour account for hello classic model.</span></span>

```powershell
    Add-AzureAccount
```

<span data-ttu-id="d4d33-154">Получить hello доступные подписки с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d4d33-154">Get hello available subscriptions by using hello following command:</span></span>

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

<span data-ttu-id="d4d33-155">Задайте подписки Azure для hello текущего сеанса.</span><span class="sxs-lookup"><span data-stu-id="d4d33-155">Set your Azure subscription for hello current session.</span></span> <span data-ttu-id="d4d33-156">В этом примере задает подписку по умолчанию hello слишком**Моя подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="d4d33-156">This example sets hello default subscription too**My Azure Subscription**.</span></span> <span data-ttu-id="d4d33-157">Замените имя подписки пример hello свои собственные.</span><span class="sxs-lookup"><span data-stu-id="d4d33-157">Replace hello example subscription name with your own.</span></span>

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="d4d33-158">Шаг 5: Убедитесь, что недостаточно ядер виртуальная машина Azure Resource Manager hello Azure область текущего развертывания или виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="d4d33-158">Step 5: Make sure you have enough Azure Resource Manager Virtual Machine cores in hello Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="d4d33-159">Можно использовать следующие PowerShell команды toocheck hello текущее количество ядер, имеющегося в диспетчере ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d4d33-159">You can use hello following PowerShell command toocheck hello current number of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="d4d33-160">toolearn Дополнительные сведения об основных квоты, в разделе [ограничения и hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span><span class="sxs-lookup"><span data-stu-id="d4d33-160">toolearn more about core quotas, see [Limits and hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span></span>

<span data-ttu-id="d4d33-161">В этом примере проверяется доступность hello в hello **Запад США** области.</span><span class="sxs-lookup"><span data-stu-id="d4d33-161">This example checks hello availability in hello **West US** region.</span></span> <span data-ttu-id="d4d33-162">Замените имя области пример hello свои собственные.</span><span class="sxs-lookup"><span data-stu-id="d4d33-162">Replace hello example region name with your own.</span></span>

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-toomigrate-your-iaas-resources"></a><span data-ttu-id="d4d33-163">Шаг 6: Проведение команды toomigrate ресурсов IaaS</span><span class="sxs-lookup"><span data-stu-id="d4d33-163">Step 6: Run commands toomigrate your IaaS resources</span></span>
> [!NOTE]
> <span data-ttu-id="d4d33-164">Все операции hello, описанные здесь являются идемпотентными.</span><span class="sxs-lookup"><span data-stu-id="d4d33-164">All hello operations described here are idempotent.</span></span> <span data-ttu-id="d4d33-165">Если имеются неполадки, отличные от неподдерживаемое свойство или ошибка конфигурации, рекомендуется повторить попытку hello подготовки, отмены или фиксации операции.</span><span class="sxs-lookup"><span data-stu-id="d4d33-165">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry hello prepare, abort, or commit operation.</span></span> <span data-ttu-id="d4d33-166">Платформа Hello пытается hello действие еще раз.</span><span class="sxs-lookup"><span data-stu-id="d4d33-166">hello platform then tries hello action again.</span></span>
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a><span data-ttu-id="d4d33-167">Шаг. 6.1. Вариант 1. Миграция виртуальных машин в облачную службу (не в виртуальную сеть)</span><span class="sxs-lookup"><span data-stu-id="d4d33-167">Step 6.1: Option 1 - Migrate virtual machines in a cloud service (not in a virtual network)</span></span>
<span data-ttu-id="d4d33-168">Получение списка hello облачные службы, используя следующую команду hello и подбору hello облачной службы, которые должны toomigrate.</span><span class="sxs-lookup"><span data-stu-id="d4d33-168">Get hello list of cloud services by using hello following command, and then pick hello cloud service that you want toomigrate.</span></span> <span data-ttu-id="d4d33-169">Если hello виртуальных машин в облачной службе hello находятся в виртуальной сети или если они имеют рабочих и веб-роли, hello команда возвращает сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="d4d33-169">If hello VMs in hello cloud service are in a virtual network or if they have web or worker roles, hello command returns an error message.</span></span>

```powershell
    Get-AzureService | ft Servicename
```

<span data-ttu-id="d4d33-170">Получите имя hello развертывания для облачной службы hello.</span><span class="sxs-lookup"><span data-stu-id="d4d33-170">Get hello deployment name for hello cloud service.</span></span> <span data-ttu-id="d4d33-171">В этом примере — имя службы hello **Мои службы**.</span><span class="sxs-lookup"><span data-stu-id="d4d33-171">In this example, hello service name is **My Service**.</span></span> <span data-ttu-id="d4d33-172">Замените имя службы имя службы пример hello.</span><span class="sxs-lookup"><span data-stu-id="d4d33-172">Replace hello example service name with your own service name.</span></span>

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

<span data-ttu-id="d4d33-173">Подготовка виртуальных машин hello в облачную службу hello для миграции.</span><span class="sxs-lookup"><span data-stu-id="d4d33-173">Prepare hello virtual machines in hello cloud service for migration.</span></span> <span data-ttu-id="d4d33-174">У вас есть два toochoose параметры из.</span><span class="sxs-lookup"><span data-stu-id="d4d33-174">You have two options toochoose from.</span></span>

* <span data-ttu-id="d4d33-175">**Вариант 1. Перенос hello виртуальные машины tooa платформы созданную виртуальную сеть**</span><span class="sxs-lookup"><span data-stu-id="d4d33-175">**Option 1. Migrate hello VMs tooa platform-created virtual network**</span></span>

    <span data-ttu-id="d4d33-176">Во-первых проверки, при переносе hello облачной службы, с помощью hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="d4d33-176">First, validate if you can migrate hello cloud service using hello following commands:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    <span data-ttu-id="d4d33-177">Hello предыдущая команда отображает все предупреждения и ошибки, блокирующие миграции.</span><span class="sxs-lookup"><span data-stu-id="d4d33-177">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="d4d33-178">Если проверка прошла успешно, то можно переместить на toohello **Подготовка** шаг:</span><span class="sxs-lookup"><span data-stu-id="d4d33-178">If validation is successful, then you can move on toohello **Prepare** step:</span></span>

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* <span data-ttu-id="d4d33-179">**Вариант 2. Перенос tooan существующую виртуальную сеть в модели развертывания диспетчера ресурсов hello**</span><span class="sxs-lookup"><span data-stu-id="d4d33-179">**Option 2. Migrate tooan existing virtual network in hello Resource Manager deployment model**</span></span>

    <span data-ttu-id="d4d33-180">В этом примере задает hello имя группы ресурсов слишком**myResourceGroup**, hello имя виртуальной сети слишком**myVirtualNetwork** и hello имя подсети слишком**mySubNet**.</span><span class="sxs-lookup"><span data-stu-id="d4d33-180">This example sets hello resource group name too**myResourceGroup**, hello virtual network name too**myVirtualNetwork** and hello subnet name too**mySubNet**.</span></span> <span data-ttu-id="d4d33-181">Замените имена hello в примере hello hello имена собственные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d4d33-181">Replace hello names in hello example with hello names of your own resources.</span></span>

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    <span data-ttu-id="d4d33-182">Во-первых проверки, при переносе hello виртуальной сети с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d4d33-182">First, validate if you can migrate hello virtual network using hello following command:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    <span data-ttu-id="d4d33-183">Hello предыдущая команда отображает все предупреждения и ошибки, блокирующие миграции.</span><span class="sxs-lookup"><span data-stu-id="d4d33-183">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="d4d33-184">Если проверка прошла успешно, то вы можете перейти с hello после шага подготовки:</span><span class="sxs-lookup"><span data-stu-id="d4d33-184">If validation is successful, then you can proceed with hello following Prepare step:</span></span>

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

<span data-ttu-id="d4d33-185">После успешного завершения операции подготовки hello с любой из предыдущих параметров hello опросить состояние миграции hello hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d4d33-185">After hello Prepare operation succeeds with either of hello preceding options, query hello migration state of hello VMs.</span></span> <span data-ttu-id="d4d33-186">Убедитесь, что они находятся в hello `Prepared` состояния.</span><span class="sxs-lookup"><span data-stu-id="d4d33-186">Ensure that they are in hello `Prepared` state.</span></span>

<span data-ttu-id="d4d33-187">В этом примере задает hello имя виртуальной Машины слишком**myVM**.</span><span class="sxs-lookup"><span data-stu-id="d4d33-187">This example sets hello VM name too**myVM**.</span></span> <span data-ttu-id="d4d33-188">Замените имя образца hello собственное имя виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d4d33-188">Replace hello example name with your own VM name.</span></span>

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

<span data-ttu-id="d4d33-189">Проверьте конфигурацию hello для подготовки ресурсов с помощью PowerShell или портал Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="d4d33-189">Check hello configuration for hello prepared resources by using either PowerShell or hello Azure portal.</span></span> <span data-ttu-id="d4d33-190">Если вы не готовы к миграции и требуется toogo задней toohello старое состояние, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d4d33-190">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

<span data-ttu-id="d4d33-191">Если хорошее hello подготовленного конфигурации, можно перемещаться вперед и зафиксировать hello ресурсы с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d4d33-191">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="d4d33-192">Шаг 6.1. Вариант 2. Миграция виртуальных машин в виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="d4d33-192">Step 6.1: Option 2 - Migrate virtual machines in a virtual network</span></span>

<span data-ttu-id="d4d33-193">toomigrate виртуальные машины в виртуальной сети, переносе hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="d4d33-193">toomigrate virtual machines in a virtual network, you migrate hello virtual network.</span></span> <span data-ttu-id="d4d33-194">с помощью виртуальной сети hello автоматически перенести Hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d4d33-194">hello virtual machines automatically migrate with hello virtual network.</span></span> <span data-ttu-id="d4d33-195">Подбор hello виртуальной сети, которые должны toomigrate.</span><span class="sxs-lookup"><span data-stu-id="d4d33-195">Pick hello virtual network that you want toomigrate.</span></span>
> [!NOTE]
> <span data-ttu-id="d4d33-196">[Миграция одной виртуальной машины для классического](migrate-single-classic-to-resource-manager.md) путем создания новой виртуальной машины диспетчера ресурсов с дисками, управляемых с помощью hello (операционной системы и данных) файлы VHD hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d4d33-196">[Migrate single classic virtual machine](migrate-single-classic-to-resource-manager.md) by creating a new Resource Manager virtual machine with Managed Disks using hello VHD (OS and data) files of hello virtual machine.</span></span>
<br>

> [!NOTE]
> <span data-ttu-id="d4d33-197">имя виртуальной сети Hello может отличаться от приведенного в hello нового портала.</span><span class="sxs-lookup"><span data-stu-id="d4d33-197">hello virtual network name might be different from what is shown in hello new Portal.</span></span> <span data-ttu-id="d4d33-198">Hello новый портал Azure отображает hello с названием `[vnet-name]` hello фактическое виртуального сетевого имени, то типа `Group [resource-group-name] [vnet-name]`.</span><span class="sxs-lookup"><span data-stu-id="d4d33-198">hello new Azure Portal displays hello name as `[vnet-name]` but hello actual virtual network name is of type `Group [resource-group-name] [vnet-name]`.</span></span> <span data-ttu-id="d4d33-199">Перед миграцией подстановки hello фактическое виртуального сетевого имени с помощью команды hello `Get-AzureVnetSite | Select -Property Name` или просматривать его в hello старый портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d4d33-199">Before migrating, lookup hello actual virtual network name using hello command `Get-AzureVnetSite | Select -Property Name` or view it in hello old Azure Portal.</span></span> 

<span data-ttu-id="d4d33-200">В этом примере задает hello имя виртуальной сети слишком**myVnet**.</span><span class="sxs-lookup"><span data-stu-id="d4d33-200">This example sets hello virtual network name too**myVnet**.</span></span> <span data-ttu-id="d4d33-201">Замените имя виртуальной сети пример hello свои собственные.</span><span class="sxs-lookup"><span data-stu-id="d4d33-201">Replace hello example virtual network name with your own.</span></span>

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> <span data-ttu-id="d4d33-202">Если hello виртуальной сети содержит веб- или рабочих ролей или виртуальных машин с неподдерживаемых конфигураций, вы получите сообщение об ошибке проверки.</span><span class="sxs-lookup"><span data-stu-id="d4d33-202">If hello virtual network contains web or worker roles, or VMs with unsupported configurations, you get a validation error message.</span></span>
>
>

<span data-ttu-id="d4d33-203">Во-первых проверки, при переносе hello виртуальной сети с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d4d33-203">First, validate if you can migrate hello virtual network by using hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

<span data-ttu-id="d4d33-204">Hello предыдущая команда отображает все предупреждения и ошибки, блокирующие миграции.</span><span class="sxs-lookup"><span data-stu-id="d4d33-204">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="d4d33-205">Если проверка прошла успешно, то вы можете перейти с hello после шага подготовки:</span><span class="sxs-lookup"><span data-stu-id="d4d33-205">If validation is successful, then you can proceed with hello following Prepare step:</span></span>

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

<span data-ttu-id="d4d33-206">Проверьте конфигурацию hello для подготовки виртуальных машин с помощью Azure PowerShell или портал Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="d4d33-206">Check hello configuration for hello prepared virtual machines by using either Azure PowerShell or hello Azure portal.</span></span> <span data-ttu-id="d4d33-207">Если вы не готовы к миграции и требуется toogo задней toohello старое состояние, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d4d33-207">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

<span data-ttu-id="d4d33-208">Если хорошее hello подготовленного конфигурации, можно перемещаться вперед и зафиксировать hello ресурсы с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d4d33-208">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a><span data-ttu-id="d4d33-209">Шаг 6.2. Перенос учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="d4d33-209">Step 6.2 Migrate a storage account</span></span>
<span data-ttu-id="d4d33-210">После завершения переноса виртуальных машин hello, мы рекомендуем перенести учетные записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="d4d33-210">Once you're done migrating hello virtual machines, we recommend you migrate hello storage accounts.</span></span>

<span data-ttu-id="d4d33-211">Прежде чем переносить hello учетной записи хранилища, выполните перед проверки предварительных требований:</span><span class="sxs-lookup"><span data-stu-id="d4d33-211">Before you migrate hello storage account, please perform preceding prerequisite checks:</span></span>

* <span data-ttu-id="d4d33-212">**Перенос классических виртуальных машин, чьи диски хранятся в учетной записи хранения hello**</span><span class="sxs-lookup"><span data-stu-id="d4d33-212">**Migrate classic virtual machines whose disks are stored in hello storage account**</span></span>

    <span data-ttu-id="d4d33-213">Предшествующий команда возвращает RoleName и DiskName свойства всех дисков виртуальной Машины классический hello в учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="d4d33-213">Preceding command returns RoleName and DiskName properties of all hello classic VM disks in hello storage account.</span></span> <span data-ttu-id="d4d33-214">RoleName — имя hello toowhich виртуальной машины hello подключенный диск.</span><span class="sxs-lookup"><span data-stu-id="d4d33-214">RoleName is hello name of hello virtual machine toowhich a disk is attached.</span></span> <span data-ttu-id="d4d33-215">Если предшествующие команда возвращает дисков убедитесь перед миграцией переносятся, toowhich виртуальных машин, эти диски подключены hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="d4d33-215">If preceding command returns disks then ensure that virtual machines toowhich these disks are attached are migrated before migrating hello storage account.</span></span>
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* <span data-ttu-id="d4d33-216">**Удаление неприкрепленные классический дисков виртуальной Машины хранятся в учетной записи хранилища hello**</span><span class="sxs-lookup"><span data-stu-id="d4d33-216">**Delete unattached classic VM disks stored in hello storage account**</span></span>

    <span data-ttu-id="d4d33-217">Находите неприкрепленные классический дисков ВМ в хранилище hello учетной записи с помощью следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d4d33-217">Find unattached classic VM disks in hello storage account using following command:</span></span>

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    <span data-ttu-id="d4d33-218">Если приведенная выше команда вернула диски, удалите их, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d4d33-218">If above command returns disks then delete these disks using following command:</span></span>

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* <span data-ttu-id="d4d33-219">**Удаление образов виртуальных Машин, хранятся в учетной записи хранилища hello**</span><span class="sxs-lookup"><span data-stu-id="d4d33-219">**Delete VM images stored in hello storage account**</span></span>

    <span data-ttu-id="d4d33-220">Предшествующий команда возвращает все образы виртуальных Машин hello с диском ОС, хранятся в учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="d4d33-220">Preceding command returns all hello VM images with OS disk stored in hello storage account.</span></span>
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     <span data-ttu-id="d4d33-221">Предшествующий команда возвращает все образы виртуальных Машин hello с дисками данных, хранящихся в учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="d4d33-221">Preceding command returns all hello VM images with data disks stored in hello storage account.</span></span>
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    <span data-ttu-id="d4d33-222">Удалите все образы виртуальных Машин hello, возвращаемый выше команд с помощью предыдущей команды.</span><span class="sxs-lookup"><span data-stu-id="d4d33-222">Delete all hello VM images returned by above commands using preceding command:</span></span>
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

<span data-ttu-id="d4d33-223">Проверьте каждую учетную запись хранилища для миграции с помощью hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d4d33-223">Validate each storage account for migration by using hello following command.</span></span> <span data-ttu-id="d4d33-224">В этом примере — имя учетной записи хранения hello **myStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="d4d33-224">In this example, hello storage account name is **myStorageAccount**.</span></span> <span data-ttu-id="d4d33-225">Замените имя пример hello hello имя учетной записи.</span><span class="sxs-lookup"><span data-stu-id="d4d33-225">Replace hello example name with hello name of your own storage account.</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

<span data-ttu-id="d4d33-226">Следующим шагом является tooPrepare hello учетной записи хранилища для миграции</span><span class="sxs-lookup"><span data-stu-id="d4d33-226">Next step is tooPrepare hello storage account for migration</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

<span data-ttu-id="d4d33-227">Проверьте конфигурацию hello для подготовки учетной записи хранилища с помощью Azure PowerShell или портал Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="d4d33-227">Check hello configuration for hello prepared storage account by using either Azure PowerShell or hello Azure portal.</span></span> <span data-ttu-id="d4d33-228">Если вы не готовы к миграции и требуется toogo задней toohello старое состояние, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d4d33-228">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

<span data-ttu-id="d4d33-229">Если хорошее hello подготовленного конфигурации, можно перемещаться вперед и зафиксировать hello ресурсы с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d4d33-229">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a><span data-ttu-id="d4d33-230">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d4d33-230">Next steps</span></span>
* [<span data-ttu-id="d4d33-231">Общие сведения о миграции поддерживаются платформы IaaS ресурсов от классических tooAzure диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="d4d33-231">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="d4d33-232">Технические близкое знакомство с платформа поддерживается перенос из классической tooAzure диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="d4d33-232">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="d4d33-233">Планирование миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="d4d33-233">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="d4d33-234">Использовать ресурсы IaaS toomigrate CLI из классической tooAzure диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="d4d33-234">Use CLI toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="d4d33-235">Средства сообщества соблюдения миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="d4d33-235">Community tools for assisting with migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="d4d33-236">Распространенные ошибки миграции</span><span class="sxs-lookup"><span data-stu-id="d4d33-236">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="d4d33-237">Просмотрите hello наиболее часто задаваемые вопросы о миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="d4d33-237">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
