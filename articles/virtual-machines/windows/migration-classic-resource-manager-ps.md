---
title: "Миграция в Resource Manager с помощью PowerShell | Документация Майкрософт"
description: "В этой статье последовательно описывается поддерживаемый платформой перенос ресурсов IaaS (виртуальных машин, виртуальных сетей и учетных записей хранения) из классической модели в модель Azure Resource Manager (ARM) с помощью команд Azure PowerShell."
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
ms.openlocfilehash: 489e6cc6bd3c5b36635f5f7e398d08fed681d2e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-iaas-resources-from-classic-to-azure-resource-manager-by-using-azure-powershell"></a><span data-ttu-id="8b1ed-103">Перенос ресурсов IaaS из классической модели в модель Azure Resource Manager с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b1ed-103">Migrate IaaS resources from classic to Azure Resource Manager by using Azure PowerShell</span></span>
<span data-ttu-id="8b1ed-104">Ниже последовательно описано, как использовать команды Azure PowerShell для переноса ресурсов IaaS из классической модели развертывания в модель развертывания с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-104">These steps show you how to use Azure PowerShell commands to migrate infrastructure as a service (IaaS) resources from the classic deployment model to the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="8b1ed-105">Если требуется, можно также перенести ресурсы с помощью [интерфейса командной строки Azure (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8b1ed-105">If you want, you can also migrate resources by using the [Azure Command Line Interface (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span></span>

* <span data-ttu-id="8b1ed-106">Общие сведения о поддерживаемых сценариях переноса см. в разделе [Поддерживаемый платформой перенос ресурсов IaaS из классической модели в модель Azure Resource Manager](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8b1ed-106">For background on supported migration scenarios, see [Platform-supported migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-overview.md).</span></span>
* <span data-ttu-id="8b1ed-107">Подробное руководство и инструкции по переносу см. в разделе [Техническое руководство по поддерживаемому платформой переносу из классической модели в модель Azure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span><span class="sxs-lookup"><span data-stu-id="8b1ed-107">For detailed guidance and a migration walkthrough, see [Technical deep dive on platform-supported migration from classic to Azure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span></span>
* [<span data-ttu-id="8b1ed-108">Распространенные ошибки миграции</span><span class="sxs-lookup"><span data-stu-id="8b1ed-108">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md)

<br>
<span data-ttu-id="8b1ed-109">Ниже приведена блок-схема с последовательностью действий во время переноса.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-109">Here is a flowchart to identify the order in which steps need to be executed during a migration process</span></span>

![Screenshot that shows the migration steps](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a><span data-ttu-id="8b1ed-111">Шаг 1. Планирование миграции</span><span class="sxs-lookup"><span data-stu-id="8b1ed-111">Step 1: Plan for migration</span></span>
<span data-ttu-id="8b1ed-112">Ниже приведено несколько рекомендаций для оценки переноса ресурсов IaaS из классической модели в модель Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic to Resource Manager:</span></span>

* <span data-ttu-id="8b1ed-113">Ознакомьтесь с [поддерживаемыми и неподдерживаемыми компонентами и конфигурациями](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8b1ed-113">Read through the [supported and unsupported features and configurations](migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="8b1ed-114">Если у вас есть виртуальные машины, которые используют неподдерживаемые конфигурации или компоненты, мы рекомендуем отложить перенос до того момента, пока не будет заявлено об их поддержке.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for the configuration/feature support to be announced.</span></span> <span data-ttu-id="8b1ed-115">Также вы можете удалить такую функцию или вынести ее за пределы конфигурации, чтобы выполнить перенос.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-115">Alternatively, if it suits your needs, remove that feature or move out of that configuration to enable migration.</span></span>
* <span data-ttu-id="8b1ed-116">Если у вас есть текущие автоматизированные сценарии, которые развертывают инфраструктуру и приложения, попробуйте создать аналогичную программу установки для миграции с помощью этих сценариев.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-116">If you have automated scripts that deploy your infrastructure and applications today, try to create a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="8b1ed-117">Вы можете также настроить примеры среды с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-117">Alternatively, you can set up sample environments by using the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b1ed-118">В настоящее время не поддерживается перенос шлюзов приложений из классической модели в модель Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-118">Application Gateways are not currently supported for migration from classic to Resource Manager.</span></span> <span data-ttu-id="8b1ed-119">Чтобы перенести классическую виртуальную сеть со шлюзом приложений, удалите этот шлюз перед выполнением операции подготовки для перемещения сети.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-119">To migrate a classic virtual network with an Application gateway, remove the gateway before running a Prepare operation to move the network.</span></span> <span data-ttu-id="8b1ed-120">После завершения переноса повторно подключите шлюз в Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-120">After you complete the migration, reconnect the gateway in Azure Resource Manager.</span></span>
>
><span data-ttu-id="8b1ed-121">Шлюзы ExpressRoute, подключенные к каналам ExpressRoute в другой подписке, перенести автоматически невозможно.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-121">ExpressRoute gateways connecting to ExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="8b1ed-122">В таких случаях удалите шлюз ExpressRoute, перенесите виртуальную сеть и создайте шлюз заново.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-122">In such cases, remove the ExpressRoute gateway, migrate the virtual network and recreate the gateway.</span></span> <span data-ttu-id="8b1ed-123">Дополнительные сведения см. в статье [Перенос каналов ExpressRoute и связанных виртуальных сетей из классической модели развертывания на модель Resource Manager](../../expressroute/expressroute-migration-classic-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="8b1ed-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from the classic to the Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
>
>

## <a name="step-2-install-the-latest-version-of-azure-powershell"></a><span data-ttu-id="8b1ed-124">Шаг 2. Установка последней версии Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b1ed-124">Step 2: Install the latest version of Azure PowerShell</span></span>
<span data-ttu-id="8b1ed-125">Есть два основных способа установки Azure PowerShell — с помощью [коллекции PowerShell](https://www.powershellgallery.com/profiles/azure-sdk/) и [установщика веб-платформы (WebPI)](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="8b1ed-125">There are two main options to install Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) or [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="8b1ed-126">Обновления для установщика веб-платформы выпускаются ежемесячно.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-126">WebPI receives monthly updates.</span></span> <span data-ttu-id="8b1ed-127">Обновления для коллекции PowerShell выпускаются на постоянной основе.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-127">PowerShell Gallery receives updates on a continuous basis.</span></span> <span data-ttu-id="8b1ed-128">В этой статье используется Azure PowerShell 2.1.0.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-128">This article is based on Azure PowerShell version 2.1.0.</span></span>

<span data-ttu-id="8b1ed-129">Инструкции по установке см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8b1ed-129">For installation instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-the-subscription-in-azure-portal"></a><span data-ttu-id="8b1ed-130">Шаг 3. Проверка наличия у вас прав администратора подписки на портале Azure</span><span class="sxs-lookup"><span data-stu-id="8b1ed-130">Step 3: Ensure that you are an administrator for the subscription in Azure portal</span></span>
<span data-ttu-id="8b1ed-131">Чтобы выполнить миграцию, вас нужно добавить как соадминистратора подписки на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8b1ed-131">To perform this migration, you must be added as a co-administrator for the subscription in the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="8b1ed-132">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8b1ed-132">Sign into the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8b1ed-133">В главном меню выберите **Подписка**.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-133">On the Hub menu, select **Subscription**.</span></span> <span data-ttu-id="8b1ed-134">Если вы не видите этот пункт, щелкните **Больше служб**.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-134">If you don't see it, select **More services**.</span></span>
3. <span data-ttu-id="8b1ed-135">Найдите нужную запись подписки, а затем посмотрите на поле **Моя роль**.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-135">Find the appropriate subscription entry, then look at the **MY ROLE** field.</span></span> <span data-ttu-id="8b1ed-136">Для соадминистратора значение должно быть _Администратор учетной записи_.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-136">For a co-administrator, the value should be _Account admin_.</span></span>

<span data-ttu-id="8b1ed-137">Если вам не удалась добавить соадминистратора, обратитесь к администратору или соадминистратору служб для подписки, чтобы вас добавили.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-137">If you are not able to add a co-administrator, then contact a service administrator or co-administrator for the subscription to get yourself added.</span></span>   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a><span data-ttu-id="8b1ed-138">Шаг 4. Настройка подписки и регистрация для миграции</span><span class="sxs-lookup"><span data-stu-id="8b1ed-138">Step 4: Set your subscription and sign up for migration</span></span>
<span data-ttu-id="8b1ed-139">Сначала запустите командную строку PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-139">First, start a PowerShell prompt.</span></span> <span data-ttu-id="8b1ed-140">Для переноса необходимо настроить среду как для классической модели, так и для модели Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-140">For migration, you need to set up your environment for both classic and Resource Manager.</span></span>

<span data-ttu-id="8b1ed-141">Войдите в учетную запись для модели Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-141">Sign in to your account for the Resource Manager model.</span></span>

```powershell
    Login-AzureRmAccount
```

<span data-ttu-id="8b1ed-142">Получите доступные подписки с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-142">Get the available subscriptions by using the following command:</span></span>

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

<span data-ttu-id="8b1ed-143">Задайте подписку Azure для текущего сеанса.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-143">Set your Azure subscription for the current session.</span></span> <span data-ttu-id="8b1ed-144">В этом примере задается имя подписки по умолчанию **My Azure Subscription**.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-144">This example sets the default subscription name to **My Azure Subscription**.</span></span> <span data-ttu-id="8b1ed-145">Замените имя подписки в примере своим собственным значением.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-145">Replace the example subscription name with your own.</span></span>

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> <span data-ttu-id="8b1ed-146">Регистрация — однократное действие, но, прежде чем выполнять миграцию, вам нужно зарегистрироваться.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-146">Registration is a one-time step, but you must do it once before attempting migration.</span></span> <span data-ttu-id="8b1ed-147">Если вы не зарегистрируетесь, отобразится такое сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="8b1ed-147">Without registering, you see the following error message:</span></span>
>
> <span data-ttu-id="8b1ed-148">*Неправильный запрос: Подписка не зарегистрирована для миграции.*</span><span class="sxs-lookup"><span data-stu-id="8b1ed-148">*BadRequest : Subscription is not registered for migration.*</span></span>
>
>

<span data-ttu-id="8b1ed-149">Выполните регистрацию в поставщике ресурсов миграции с помощью приведенной ниже команды.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-149">Register with the migration resource provider by using the following command:</span></span>

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="8b1ed-150">Подождите пять минут для завершения регистрации.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-150">Please wait five minutes for the registration to finish.</span></span> <span data-ttu-id="8b1ed-151">Состояние утверждения регистрации можно проверить, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-151">You can check the status of the approval by using the following command:</span></span>

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="8b1ed-152">Убедитесь, что RegistrationState имеет значение `Registered` , прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-152">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

<span data-ttu-id="8b1ed-153">Теперь войдите в учетную запись для классической модели.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-153">Now sign in to your account for the classic model.</span></span>

```powershell
    Add-AzureAccount
```

<span data-ttu-id="8b1ed-154">Получите доступные подписки с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-154">Get the available subscriptions by using the following command:</span></span>

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

<span data-ttu-id="8b1ed-155">Задайте подписку Azure для текущего сеанса.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-155">Set your Azure subscription for the current session.</span></span> <span data-ttu-id="8b1ed-156">В этом примере задается имя подписки по умолчанию **My Azure Subscription**.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-156">This example sets the default subscription to **My Azure Subscription**.</span></span> <span data-ttu-id="8b1ed-157">Замените имя подписки в примере своим собственным значением.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-157">Replace the example subscription name with your own.</span></span>

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-the-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="8b1ed-158">Шаг 5. Проверка наличия достаточного числа ядер виртуальной машины Azure Resource Manager в регионе Azure текущего развертывания или виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="8b1ed-158">Step 5: Make sure you have enough Azure Resource Manager Virtual Machine cores in the Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="8b1ed-159">Чтобы проверить текущее количество ядер в Azure Resource Manager, можно использовать приведенную ниже команду PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-159">You can use the following PowerShell command to check the current number of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="8b1ed-160">Чтобы узнать больше о квотах ядер, ознакомьтесь с разделом [Ограничения и диспетчер ресурсов Azure](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span><span class="sxs-lookup"><span data-stu-id="8b1ed-160">To learn more about core quotas, see [Limits and the Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span></span>

<span data-ttu-id="8b1ed-161">В этом примере проверяется доступность в регионе **Западная часть США**.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-161">This example checks the availability in the **West US** region.</span></span> <span data-ttu-id="8b1ed-162">Замените регион в примере своим собственным значением.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-162">Replace the example region name with your own.</span></span>

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-to-migrate-your-iaas-resources"></a><span data-ttu-id="8b1ed-163">Шаг 6. Выполнение команд для переноса ресурсов IaaS</span><span class="sxs-lookup"><span data-stu-id="8b1ed-163">Step 6: Run commands to migrate your IaaS resources</span></span>
> [!NOTE]
> <span data-ttu-id="8b1ed-164">Все операции, описанные здесь, являются идемпотентными.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-164">All the operations described here are idempotent.</span></span> <span data-ttu-id="8b1ed-165">Если вы столкнетесь с какой-либо проблемой, не связанной с неподдерживаемой функцией или ошибкой конфигурации, мы рекомендуем повторить подготовку, прервать или зафиксировать текущую операцию.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-165">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry the prepare, abort, or commit operation.</span></span> <span data-ttu-id="8b1ed-166">Платформа попытается повторить это действие.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-166">The platform then tries the action again.</span></span>
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a><span data-ttu-id="8b1ed-167">Шаг. 6.1. Вариант 1. Миграция виртуальных машин в облачную службу (не в виртуальную сеть)</span><span class="sxs-lookup"><span data-stu-id="8b1ed-167">Step 6.1: Option 1 - Migrate virtual machines in a cloud service (not in a virtual network)</span></span>
<span data-ttu-id="8b1ed-168">Получите список облачных служб, выполнив следующую команду, а затем выберите облачную службу для переноса.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-168">Get the list of cloud services by using the following command, and then pick the cloud service that you want to migrate.</span></span> <span data-ttu-id="8b1ed-169">Если виртуальные машины в облачной службе размещены в виртуальной сети или им назначены веб-роли или рабочие роли, то команда возвращает сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-169">If the VMs in the cloud service are in a virtual network or if they have web or worker roles, the command returns an error message.</span></span>

```powershell
    Get-AzureService | ft Servicename
```

<span data-ttu-id="8b1ed-170">Получите имя развертывания для облачной службы.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-170">Get the deployment name for the cloud service.</span></span> <span data-ttu-id="8b1ed-171">В этом примере имя службы — **My Service**.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-171">In this example, the service name is **My Service**.</span></span> <span data-ttu-id="8b1ed-172">Замените имя службы в примере своим собственным значением.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-172">Replace the example service name with your own service name.</span></span>

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

<span data-ttu-id="8b1ed-173">Подготовьте к переносу виртуальные машины в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-173">Prepare the virtual machines in the cloud service for migration.</span></span> <span data-ttu-id="8b1ed-174">Возможно два варианта.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-174">You have two options to choose from.</span></span>

* <span data-ttu-id="8b1ed-175">**Вариант 1. Миграция виртуальных машин в виртуальную сеть, созданную платформой**</span><span class="sxs-lookup"><span data-stu-id="8b1ed-175">**Option 1. Migrate the VMs to a platform-created virtual network**</span></span>

    <span data-ttu-id="8b1ed-176">Во-первых, проверьте возможность переноса облачной службы с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-176">First, validate if you can migrate the cloud service using the following commands:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    <span data-ttu-id="8b1ed-177">Приведенная выше команда отображает все предупреждения и ошибки, которые мешают переносу.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-177">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="8b1ed-178">Если проверка выполнена успешно, то можно переходить к этапу **подготовки** ниже.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-178">If validation is successful, then you can move on to the **Prepare** step:</span></span>

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* <span data-ttu-id="8b1ed-179">**Вариант 2. Миграция виртуальных машин в существующую виртуальную сеть в модели развертывания с помощью Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="8b1ed-179">**Option 2. Migrate to an existing virtual network in the Resource Manager deployment model**</span></span>

    <span data-ttu-id="8b1ed-180">В этом примере группе ресурсов присваивается имя **myResourceGroup**, виртуальной сети — имя **myVirtualNetwork**, а подсети — имя **mySubNet**.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-180">This example sets the resource group name to **myResourceGroup**, the virtual network name to **myVirtualNetwork** and the subnet name to **mySubNet**.</span></span> <span data-ttu-id="8b1ed-181">Замените имена в примере именами своих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-181">Replace the names in the example with the names of your own resources.</span></span>

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    <span data-ttu-id="8b1ed-182">Во-первых, проверьте возможность переноса виртуальной сети с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-182">First, validate if you can migrate the virtual network using the following command:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    <span data-ttu-id="8b1ed-183">Приведенная выше команда отображает все предупреждения и ошибки, которые мешают переносу.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-183">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="8b1ed-184">Если проверка выполнена успешно, то можно переходить к шагу подготовки ниже.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-184">If validation is successful, then you can proceed with the following Prepare step:</span></span>

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

<span data-ttu-id="8b1ed-185">После успешного завершения операции подготовки для одного из перечисленных выше вариантов запросите состояние миграции виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-185">After the Prepare operation succeeds with either of the preceding options, query the migration state of the VMs.</span></span> <span data-ttu-id="8b1ed-186">Убедитесь, что они находятся в состоянии `Prepared` .</span><span class="sxs-lookup"><span data-stu-id="8b1ed-186">Ensure that they are in the `Prepared` state.</span></span>

<span data-ttu-id="8b1ed-187">В этом примере виртуальной машине присваивается имя **myVM**.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-187">This example sets the VM name to **myVM**.</span></span> <span data-ttu-id="8b1ed-188">Замените имя в примере именем своей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-188">Replace the example name with your own VM name.</span></span>

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

<span data-ttu-id="8b1ed-189">Проверьте конфигурацию для подготовленных ресурсов с помощью PowerShell или портала Azure.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-189">Check the configuration for the prepared resources by using either PowerShell or the Azure portal.</span></span> <span data-ttu-id="8b1ed-190">Если вы не готовы к миграции и хотите вернуть предыдущее состояние, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-190">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

<span data-ttu-id="8b1ed-191">Если подготовленная конфигурация вас устраивает, можете продолжить процесс. Выполните следующую команду, чтобы зафиксировать ресурсы.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-191">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="8b1ed-192">Шаг 6.1. Вариант 2. Миграция виртуальных машин в виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="8b1ed-192">Step 6.1: Option 2 - Migrate virtual machines in a virtual network</span></span>

<span data-ttu-id="8b1ed-193">Для миграции виртуальных машин в виртуальной сети переносится сама виртуальная сеть.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-193">To migrate virtual machines in a virtual network, you migrate the virtual network.</span></span> <span data-ttu-id="8b1ed-194">Виртуальные машины автоматически переносятся вместе с ней.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-194">The virtual machines automatically migrate with the virtual network.</span></span> <span data-ttu-id="8b1ed-195">Выберите виртуальную сеть, в которую будете переносить ресурсы.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-195">Pick the virtual network that you want to migrate.</span></span>
> [!NOTE]
> <span data-ttu-id="8b1ed-196">[Перенесите отдельную классическую виртуальную машину](migrate-single-classic-to-resource-manager.md), создав виртуальную машину Resource Manager с управляемыми дисками на основе VHD-файлов (диска ОС и дисков данных) исходной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-196">[Migrate single classic virtual machine](migrate-single-classic-to-resource-manager.md) by creating a new Resource Manager virtual machine with Managed Disks using the VHD (OS and data) files of the virtual machine.</span></span>
<br>

> [!NOTE]
> <span data-ttu-id="8b1ed-197">Имя виртуальной сети может отличаться от приведенного на новом портале.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-197">The virtual network name might be different from what is shown in the new Portal.</span></span> <span data-ttu-id="8b1ed-198">На новом портале Azure отображается имя в формате `[vnet-name]`, но фактическое имя виртуальной сети имеет тип `Group [resource-group-name] [vnet-name]`.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-198">The new Azure Portal displays the name as `[vnet-name]` but the actual virtual network name is of type `Group [resource-group-name] [vnet-name]`.</span></span> <span data-ttu-id="8b1ed-199">Перед выполнением миграции найдите фактическое имя виртуальной сети с помощью команды `Get-AzureVnetSite | Select -Property Name` или просмотрите его на старом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-199">Before migrating, lookup the actual virtual network name using the command `Get-AzureVnetSite | Select -Property Name` or view it in the old Azure Portal.</span></span> 

<span data-ttu-id="8b1ed-200">В этом примере виртуальной сети присваивается имя **myVnet**.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-200">This example sets the virtual network name to **myVnet**.</span></span> <span data-ttu-id="8b1ed-201">Замените имя виртуальной сети в примере своим собственным значением.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-201">Replace the example virtual network name with your own.</span></span>

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> <span data-ttu-id="8b1ed-202">Если в виртуальной сети есть виртуальные машины, веб-роли или рабочие роли с неподдерживаемыми конфигурациями, то отображается сообщение об ошибке проверки.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-202">If the virtual network contains web or worker roles, or VMs with unsupported configurations, you get a validation error message.</span></span>
>
>

<span data-ttu-id="8b1ed-203">Во-первых, проверьте возможность переноса виртуальной сети с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-203">First, validate if you can migrate the virtual network by using the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

<span data-ttu-id="8b1ed-204">Приведенная выше команда отображает все предупреждения и ошибки, которые мешают переносу.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-204">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="8b1ed-205">Если проверка выполнена успешно, то можно переходить к шагу подготовки ниже.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-205">If validation is successful, then you can proceed with the following Prepare step:</span></span>

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

<span data-ttu-id="8b1ed-206">Проверьте конфигурацию для подготовленных виртуальных машин с помощью Azure PowerShell или портала Azure.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-206">Check the configuration for the prepared virtual machines by using either Azure PowerShell or the Azure portal.</span></span> <span data-ttu-id="8b1ed-207">Если вы не готовы к миграции и хотите вернуть предыдущее состояние, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-207">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

<span data-ttu-id="8b1ed-208">Если подготовленная конфигурация вас устраивает, можете продолжить процесс. Выполните следующую команду, чтобы зафиксировать ресурсы.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-208">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a><span data-ttu-id="8b1ed-209">Шаг 6.2. Перенос учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="8b1ed-209">Step 6.2 Migrate a storage account</span></span>
<span data-ttu-id="8b1ed-210">После миграции виртуальных машин рекомендуется перенести учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-210">Once you're done migrating the virtual machines, we recommend you migrate the storage accounts.</span></span>

<span data-ttu-id="8b1ed-211">Прежде чем перенести учетную запись хранения, выполните проверку выполнения предварительных требований.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-211">Before you migrate the storage account, please perform preceding prerequisite checks:</span></span>

* <span data-ttu-id="8b1ed-212">**Перенесите классические виртуальные машины, диски которых хранятся в учетной записи хранения.**</span><span class="sxs-lookup"><span data-stu-id="8b1ed-212">**Migrate classic virtual machines whose disks are stored in the storage account**</span></span>

    <span data-ttu-id="8b1ed-213">Приведенная выше команда возвращает свойства RoleName и DiskName всех дисков классических виртуальных машин в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-213">Preceding command returns RoleName and DiskName properties of all the classic VM disks in the storage account.</span></span> <span data-ttu-id="8b1ed-214">RoleName — это имя виртуальной машины, к которой подключен диск.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-214">RoleName is the name of the virtual machine to which a disk is attached.</span></span> <span data-ttu-id="8b1ed-215">Если приведенная выше команда вернула диски, убедитесь, что виртуальные машины, к которым подключены эти диски, будут перенесены до переноса учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-215">If preceding command returns disks then ensure that virtual machines to which these disks are attached are migrated before migrating the storage account.</span></span>
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* <span data-ttu-id="8b1ed-216">**Удалите неподключенные диски классических виртуальных машин, хранящиеся в учетной записи хранения.**</span><span class="sxs-lookup"><span data-stu-id="8b1ed-216">**Delete unattached classic VM disks stored in the storage account**</span></span>

    <span data-ttu-id="8b1ed-217">Чтобы найти неподключенные диски классических виртуальных машин в учетной записи хранения, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-217">Find unattached classic VM disks in the storage account using following command:</span></span>

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    <span data-ttu-id="8b1ed-218">Если приведенная выше команда вернула диски, удалите их, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-218">If above command returns disks then delete these disks using following command:</span></span>

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* <span data-ttu-id="8b1ed-219">**Удалите образы виртуальных машин, хранящиеся в учетной записи хранения.**</span><span class="sxs-lookup"><span data-stu-id="8b1ed-219">**Delete VM images stored in the storage account**</span></span>

    <span data-ttu-id="8b1ed-220">Приведенная выше команда возвращает все образы виртуальных машин, диск ОС которых хранится в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-220">Preceding command returns all the VM images with OS disk stored in the storage account.</span></span>
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     <span data-ttu-id="8b1ed-221">Приведенная выше команда возвращает все образы виртуальных машин, диски данных которых хранятся в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-221">Preceding command returns all the VM images with data disks stored in the storage account.</span></span>
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    <span data-ttu-id="8b1ed-222">Удалите все образы виртуальных машин, возвращенные приведенными выше командами, с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-222">Delete all the VM images returned by above commands using preceding command:</span></span>
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

<span data-ttu-id="8b1ed-223">Подготовьте каждую учетную запись хранения к переносу, используя следующую команду.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-223">Validate each storage account for migration by using the following command.</span></span> <span data-ttu-id="8b1ed-224">В этом примере имя учетной записи хранения — **myStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-224">In this example, the storage account name is **myStorageAccount**.</span></span> <span data-ttu-id="8b1ed-225">Замените имя в примере именем своей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-225">Replace the example name with the name of your own storage account.</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

<span data-ttu-id="8b1ed-226">Далее необходимо подготовить учетную запись хранения к миграции.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-226">Next step is to Prepare the storage account for migration</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

<span data-ttu-id="8b1ed-227">Проверьте конфигурацию для подготовленной учетной записи хранения с помощью Azure PowerShell или портала Azure.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-227">Check the configuration for the prepared storage account by using either Azure PowerShell or the Azure portal.</span></span> <span data-ttu-id="8b1ed-228">Если вы не готовы к миграции и хотите вернуть предыдущее состояние, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-228">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

<span data-ttu-id="8b1ed-229">Если подготовленная конфигурация вас устраивает, можете продолжить процесс. Выполните следующую команду, чтобы зафиксировать ресурсы.</span><span class="sxs-lookup"><span data-stu-id="8b1ed-229">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a><span data-ttu-id="8b1ed-230">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8b1ed-230">Next steps</span></span>
* [<span data-ttu-id="8b1ed-231">Обзор поддерживаемого платформой переноса ресурсов IaaS из классической модели в модель Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8b1ed-231">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="8b1ed-232">Техническое руководство по поддерживаемому платформой переносу из классической модели в модель Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8b1ed-232">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* <span data-ttu-id="8b1ed-233">[Planning for migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Планирование переноса ресурсов IaaS из классической модели в модель Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="8b1ed-233">[Planning for migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
* [<span data-ttu-id="8b1ed-234">Перенос ресурсов IaaS из классической модели в модель Azure Resource Manager с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="8b1ed-234">Use CLI to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* <span data-ttu-id="8b1ed-235">[Community tools to migrate IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Инструменты сообщества для перемещения ресурсов IaaS из классической модели в модель Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="8b1ed-235">[Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
* [<span data-ttu-id="8b1ed-236">Распространенные ошибки миграции</span><span class="sxs-lookup"><span data-stu-id="8b1ed-236">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="8b1ed-237">Часто задаваемые вопросы о миграции из классической модели в модель Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8b1ed-237">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
