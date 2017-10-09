---
title: "виртуальные машины aaaMigrate tooResource диспетчера с помощью Azure CLI | Документы Microsoft"
description: "Этой статье рассматриваются hello поддерживается платформой миграции ресурсов от классических tooAzure диспетчера ресурсов с помощью Azure CLI"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 0b11f4bb1b4658b3e88bf7629147ed953b678556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-cli"></a><span data-ttu-id="31a0f-103">Перенос ресурсов IaaS в классическом tooAzure диспетчера ресурсов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="31a0f-103">Migrate IaaS resources from classic tooAzure Resource Manager by using Azure CLI</span></span>
<span data-ttu-id="31a0f-104">Следующие шаги показывают, как toouse Azure командной строки (CLI) команды toomigrate инфраструктуры как услуги (IaaS) ресурсы из hello классической модели toohello диспетчера ресурсов Azure развертывания модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="31a0f-104">These steps show you how toouse Azure command-line interface (CLI) commands toomigrate infrastructure as a service (IaaS) resources from hello classic deployment model toohello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="31a0f-105">статья Hello требует hello [Azure CLI](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="31a0f-105">hello article requires hello [Azure CLI](../../cli-install-nodejs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="31a0f-106">Все операции hello, описанные здесь являются идемпотентными.</span><span class="sxs-lookup"><span data-stu-id="31a0f-106">All hello operations described here are idempotent.</span></span> <span data-ttu-id="31a0f-107">Если имеются неполадки, отличные от неподдерживаемое свойство или ошибка конфигурации, рекомендуется повторить попытку hello подготовки, отмены или фиксации операции.</span><span class="sxs-lookup"><span data-stu-id="31a0f-107">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry hello prepare, abort, or commit operation.</span></span> <span data-ttu-id="31a0f-108">Затем платформа Hello пытается hello действие еще раз.</span><span class="sxs-lookup"><span data-stu-id="31a0f-108">hello platform will then try hello action again.</span></span>
> 
> 

<br>
<span data-ttu-id="31a0f-109">Ниже приведен порядок hello tooidentify блок-схемы, в котором действия требуется toobe выполнен во время процесса миграции</span><span class="sxs-lookup"><span data-stu-id="31a0f-109">Here is a flowchart tooidentify hello order in which steps need toobe executed during a migration process</span></span>

![Снимок экрана, показывающий шагов миграции hello](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a><span data-ttu-id="31a0f-111">Шаг 1. Подготовка к переносу</span><span class="sxs-lookup"><span data-stu-id="31a0f-111">Step 1: Prepare for migration</span></span>
<span data-ttu-id="31a0f-112">Вот несколько рекомендаций, рекомендуется при оценке миграции IaaS ресурсов от классических tooResource диспетчера.</span><span class="sxs-lookup"><span data-stu-id="31a0f-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic tooResource Manager:</span></span>

* <span data-ttu-id="31a0f-113">Прочтите hello [списка неподдерживаемых конфигураций или функции](../windows/migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="31a0f-113">Read through hello [list of unsupported configurations or features](../windows/migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="31a0f-114">При наличии виртуальных машин, использующих неподдерживаемые конфигурации или компоненты, рекомендуется отложить hello/конфигурация компонентов поддержки toobe было объявлено.</span><span class="sxs-lookup"><span data-stu-id="31a0f-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for hello feature/configuration support toobe announced.</span></span> <span data-ttu-id="31a0f-115">Кроме того можно удалить эти компоненты или выйти из миграции tooenable этой конфигурации, если он соответствует вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="31a0f-115">Alternatively, you can remove that feature or move out of that configuration tooenable migration if it suits your needs.</span></span>
* <span data-ttu-id="31a0f-116">Если у вас есть автоматизированные скрипты, которые сегодня развертывание инфраструктуры и приложений, попробуйте toocreate аналогичную программу установки теста с помощью этих скриптов для миграции.</span><span class="sxs-lookup"><span data-stu-id="31a0f-116">If you have automated scripts that deploy your infrastructure and applications today, try toocreate a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="31a0f-117">Кроме того можно настроить образец сред с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="31a0f-117">Alternatively, you can set up sample environments by using hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31a0f-118">Шлюзы приложений для миграции с классической tooResource Manager в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="31a0f-118">Application Gateways are not currently supported for migration from classic tooResource Manager.</span></span> <span data-ttu-id="31a0f-119">Перед запуском сети hello toomove операции подготовки toomigrate классической виртуальной сети с шлюза приложения, удалить шлюз hello.</span><span class="sxs-lookup"><span data-stu-id="31a0f-119">toomigrate a classic virtual network with an Application gateway, remove hello gateway before running a Prepare operation toomove hello network.</span></span> <span data-ttu-id="31a0f-120">После завершения миграции hello переподключение hello шлюза в диспетчере ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="31a0f-120">After you complete hello migration, reconnect hello gateway in Azure Resource Manager.</span></span> 
>
><span data-ttu-id="31a0f-121">Шлюзов ExpressRoute подключение tooExpressRoute цепи в другую подписку невозможно перенести автоматически.</span><span class="sxs-lookup"><span data-stu-id="31a0f-121">ExpressRoute gateways connecting tooExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="31a0f-122">В таких случаях удалить шлюз ExpressRoute hello, миграция виртуальной сети hello и повторного создания шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="31a0f-122">In such cases, remove hello ExpressRoute gateway, migrate hello virtual network and recreate hello gateway.</span></span> <span data-ttu-id="31a0f-123">См. в разделе [перенести ExpressRoute каналов и связанные виртуальные сети из модели развертывания диспетчера ресурсов hello классический toohello](../../expressroute/expressroute-migration-classic-resource-manager.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="31a0f-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from hello classic toohello Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
> 
> 

## <a name="step-2-set-your-subscription-and-register-hello-provider"></a><span data-ttu-id="31a0f-124">Шаг 2: Задайте подписку и регистрации поставщика hello</span><span class="sxs-lookup"><span data-stu-id="31a0f-124">Step 2: Set your subscription and register hello provider</span></span>
<span data-ttu-id="31a0f-125">Для сценариев миграции tooset необходимо настроить среду для обоих классический и диспетчер ресурсов.</span><span class="sxs-lookup"><span data-stu-id="31a0f-125">For migration scenarios, you need tooset up your environment for both classic and Resource Manager.</span></span> <span data-ttu-id="31a0f-126">[Установите интерфейс командной строки Azure](../../cli-install-nodejs.md) (Azure CLI) и [выберите подписку](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="31a0f-126">[Install Azure CLI](../../cli-install-nodejs.md) and [select your subscription](../../xplat-cli-connect.md).</span></span>

<span data-ttu-id="31a0f-127">Учетная запись входа tooyour.</span><span class="sxs-lookup"><span data-stu-id="31a0f-127">Sign-in tooyour account.</span></span>

    azure login

<span data-ttu-id="31a0f-128">Здравствуйте, выберите подписку Azure, используя следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="31a0f-128">Select hello Azure subscription by using hello following command.</span></span>

    azure account set "<azure-subscription-name>"

> [!NOTE]
> <span data-ttu-id="31a0f-129">Регистрация заключается в один раз шаги но нуждается toobe один раз, прежде чем миграции.</span><span class="sxs-lookup"><span data-stu-id="31a0f-129">Registration is a one time step but it needs toobe done once before attempting migration.</span></span> <span data-ttu-id="31a0f-130">Без регистрации вы увидите сообщение об ошибке после hello</span><span class="sxs-lookup"><span data-stu-id="31a0f-130">Without registering you'll see hello following error message</span></span> 
> 
> <span data-ttu-id="31a0f-131">*Неправильный запрос: Подписка не зарегистрирована для миграции.*</span><span class="sxs-lookup"><span data-stu-id="31a0f-131">*BadRequest : Subscription is not registered for migration.*</span></span> 
> 
> 

<span data-ttu-id="31a0f-132">Зарегистрировать поставщик ресурсов hello миграции с помощью hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="31a0f-132">Register with hello migration resource provider by using hello following command.</span></span> <span data-ttu-id="31a0f-133">Обратите внимание, что в некоторых случаях время ожидания этой команды истекает. Тем не менее будет успешной регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="31a0f-133">Note that in some cases, this command times out. However, hello registration will be successful.</span></span>

    azure provider register Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="31a0f-134">Подождите пять минут для регистрации toofinish hello.</span><span class="sxs-lookup"><span data-stu-id="31a0f-134">Please wait five minutes for hello registration toofinish.</span></span> <span data-ttu-id="31a0f-135">Можно проверить состояние hello hello утверждения с помощью hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="31a0f-135">You can check hello status of hello approval by using hello following command.</span></span> <span data-ttu-id="31a0f-136">Убедитесь, что RegistrationState имеет значение `Registered` , прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="31a0f-136">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

    azure provider show Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="31a0f-137">Теперь, переключитесь CLI toohello `asm` режим.</span><span class="sxs-lookup"><span data-stu-id="31a0f-137">Now switch CLI toohello `asm` mode.</span></span>

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="31a0f-138">Шаг 3: Убедитесь, что недостаточно ядер виртуальная машина Azure Resource Manager hello Azure область текущего развертывания или виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="31a0f-138">Step 3: Make sure you have enough Azure Resource Manager Virtual Machine cores in hello Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="31a0f-139">Для этого шага необходимо tooswitch слишком`arm` режим.</span><span class="sxs-lookup"><span data-stu-id="31a0f-139">For this step you'll need tooswitch too`arm` mode.</span></span> <span data-ttu-id="31a0f-140">Для этого hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="31a0f-140">Do this with hello following command.</span></span>

```
azure config mode arm
```

<span data-ttu-id="31a0f-141">Можно использовать следующие CLI команда toocheck hello текущее количество ядер, имеющегося в диспетчере ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="31a0f-141">You can use hello following CLI command toocheck hello current amount of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="31a0f-142">toolearn Дополнительные сведения об основных квоты, в разделе [ограничения и hello диспетчера ресурсов Azure](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span><span class="sxs-lookup"><span data-stu-id="31a0f-142">toolearn more about core quotas, see [Limits and hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span></span>

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

<span data-ttu-id="31a0f-143">После завершения проверки того, этот шаг, можно переключиться обратно слишком`asm` режим.</span><span class="sxs-lookup"><span data-stu-id="31a0f-143">Once you're done verifying this step, you can switch back too`asm` mode.</span></span>

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a><span data-ttu-id="31a0f-144">Шаг 4. Вариант 1: миграция виртуальных машин в облачной службе</span><span class="sxs-lookup"><span data-stu-id="31a0f-144">Step 4: Option 1 - Migrate virtual machines in a cloud service</span></span>
<span data-ttu-id="31a0f-145">Получение списка hello облачные службы, используя следующую команду hello и подбору hello облачной службы, которые должны toomigrate.</span><span class="sxs-lookup"><span data-stu-id="31a0f-145">Get hello list of cloud services by using hello following command, and then pick hello cloud service that you want toomigrate.</span></span> <span data-ttu-id="31a0f-146">Обратите внимание, что если hello виртуальных машин в облачной службе hello в виртуальной сети или если они имеют рабочих и веб-роли, вы получите сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="31a0f-146">Note that if hello VMs in hello cloud service are in a virtual network or if they have web/worker roles, you will get an error message.</span></span>

    azure service list

<span data-ttu-id="31a0f-147">Запустите следующую имя команды tooget hello развертывания для облачной службы hello из подробный вывод hello hello.</span><span class="sxs-lookup"><span data-stu-id="31a0f-147">Run hello following command tooget hello deployment name for hello cloud service from hello verbose output.</span></span> <span data-ttu-id="31a0f-148">В большинстве случаев hello имя развертывания является hello то же, что имя облачной службы hello.</span><span class="sxs-lookup"><span data-stu-id="31a0f-148">In most cases, hello deployment name is hello same as hello cloud service name.</span></span>

    azure service show <serviceName> -vv

<span data-ttu-id="31a0f-149">Во-первых проверки, при переносе hello облачной службы, с помощью hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="31a0f-149">First, validate if you can migrate hello cloud service using hello following commands:</span></span>

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

<span data-ttu-id="31a0f-150">Подготовка виртуальных машин hello в облачную службу hello для миграции.</span><span class="sxs-lookup"><span data-stu-id="31a0f-150">Prepare hello virtual machines in hello cloud service for migration.</span></span> <span data-ttu-id="31a0f-151">У вас есть два toochoose параметры из.</span><span class="sxs-lookup"><span data-stu-id="31a0f-151">You have two options toochoose from.</span></span>

<span data-ttu-id="31a0f-152">Toomigrate hello виртуальные машины tooa платформы созданную виртуальную сеть, используйте следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="31a0f-152">If you want toomigrate hello VMs tooa platform-created virtual network, use hello following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

<span data-ttu-id="31a0f-153">Tooan toomigrate существующую виртуальную сеть в модели развертывания диспетчера ресурсов hello, используйте следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="31a0f-153">If you want toomigrate tooan existing virtual network in hello Resource Manager deployment model, use hello following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

<span data-ttu-id="31a0f-154">После подготовки hello операция завершилась успешно, можно просмотреть hello подробный вывод tooget hello состояние миграции hello виртуальные машины и убедитесь, что они находятся в hello `Prepared` состояния.</span><span class="sxs-lookup"><span data-stu-id="31a0f-154">After hello prepare operation is successful, you can look through hello verbose output tooget hello migration state of hello VMs and ensure that they are in hello `Prepared` state.</span></span>

    azure vm show <vmName> -vv

<span data-ttu-id="31a0f-155">Проверьте конфигурацию hello для hello подготовить ресурсы с помощью CLI или hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="31a0f-155">Check hello configuration for hello prepared resources by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="31a0f-156">Если вы не готовы к миграции и требуется toogo задней toohello старое состояние, используйте следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="31a0f-156">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure service deployment abort-migration <serviceName> <deploymentName>

<span data-ttu-id="31a0f-157">Если хорошее hello подготовленного конфигурации, можно перемещаться вперед и зафиксировать hello ресурсы с помощью hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="31a0f-157">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="31a0f-158">Шаг 4. Вариант 2: миграция виртуальных машин в виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="31a0f-158">Step 4: Option 2 -  Migrate virtual machines in a virtual network</span></span>
<span data-ttu-id="31a0f-159">Подбор hello виртуальной сети, которые должны toomigrate.</span><span class="sxs-lookup"><span data-stu-id="31a0f-159">Pick hello virtual network that you want toomigrate.</span></span> <span data-ttu-id="31a0f-160">Обратите внимание, что если виртуальная сеть hello содержит рабочих и веб-ролей или виртуальных машин с неподдерживаемых конфигураций, вы получите сообщение об ошибке проверки.</span><span class="sxs-lookup"><span data-stu-id="31a0f-160">Note that if hello virtual network contains web/worker roles or VMs with unsupported configurations, you will get a validation error message.</span></span>

<span data-ttu-id="31a0f-161">Получите все виртуальные сети hello в подписке hello, используя следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="31a0f-161">Get all hello virtual networks in hello subscription by using hello following command.</span></span>

    azure network vnet list

<span data-ttu-id="31a0f-162">Hello результат будет выглядеть примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="31a0f-162">hello output will look something like this:</span></span>

![Снимок экрана приветствия командной строки с выделенным именем hello всю виртуальную сеть.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

<span data-ttu-id="31a0f-164">В приведенном выше примере hello, hello **virtualNetworkName** — полное имя hello **«Classicubuntu16 classicubuntu16 группы»**.</span><span class="sxs-lookup"><span data-stu-id="31a0f-164">In hello above example, hello **virtualNetworkName** is hello entire name **"Group classicubuntu16 classicubuntu16"**.</span></span>

<span data-ttu-id="31a0f-165">Во-первых проверки, при переносе hello виртуальной сети с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="31a0f-165">First, validate if you can migrate hello virtual network using hello following command:</span></span>

```shell
azure network vnet validate-migration <virtualNetworkName>
```

<span data-ttu-id="31a0f-166">Подготовьте hello виртуальной сети по своему усмотрению для миграции с помощью hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="31a0f-166">Prepare hello virtual network of your choice for migration by using hello following command.</span></span>

    azure network vnet prepare-migration <virtualNetworkName>

<span data-ttu-id="31a0f-167">Проверьте конфигурацию hello для hello подготовить виртуальные машины с помощью CLI или hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="31a0f-167">Check hello configuration for hello prepared virtual machines by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="31a0f-168">Если вы не готовы к миграции и требуется toogo задней toohello старое состояние, используйте следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="31a0f-168">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure network vnet abort-migration <virtualNetworkName>

<span data-ttu-id="31a0f-169">Если хорошее hello подготовленного конфигурации, можно перемещаться вперед и зафиксировать hello ресурсы с помощью hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="31a0f-169">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a><span data-ttu-id="31a0f-170">Шаг 5. Перенос учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="31a0f-170">Step 5: Migrate a storage account</span></span>
<span data-ttu-id="31a0f-171">После завершения переноса виртуальных машин hello, мы рекомендуем перенести hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="31a0f-171">Once you're done migrating hello virtual machines, we recommend you migrate hello storage account.</span></span>

<span data-ttu-id="31a0f-172">Подготовка учетной записи хранилища hello для миграции с помощью hello следующую команду</span><span class="sxs-lookup"><span data-stu-id="31a0f-172">Prepare hello storage account for migration by using hello following command</span></span>

    azure storage account prepare-migration <storageAccountName>

<span data-ttu-id="31a0f-173">Проверьте конфигурацию hello для hello подготовить учетную запись хранения с помощью CLI или hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="31a0f-173">Check hello configuration for hello prepared storage account by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="31a0f-174">Если вы не готовы к миграции и требуется toogo задней toohello старое состояние, используйте следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="31a0f-174">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure storage account abort-migration <storageAccountName>

<span data-ttu-id="31a0f-175">Если хорошее hello подготовленного конфигурации, можно перемещаться вперед и зафиксировать hello ресурсы с помощью hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="31a0f-175">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a><span data-ttu-id="31a0f-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="31a0f-176">Next steps</span></span>

* [<span data-ttu-id="31a0f-177">Общие сведения о миграции поддерживаются платформы IaaS ресурсов от классических tooAzure диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="31a0f-177">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="31a0f-178">Технические близкое знакомство с платформа поддерживается перенос из классической tooAzure диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="31a0f-178">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="31a0f-179">Планирование миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="31a0f-179">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="31a0f-180">Использовать ресурсы IaaS PowerShell toomigrate из классической tooAzure диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="31a0f-180">Use PowerShell toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="31a0f-181">Средства сообщества соблюдения миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="31a0f-181">Community tools for assisting with migration of IaaS resources from classic tooAzure Resource Manager</span></span>](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="31a0f-182">Распространенные ошибки миграции</span><span class="sxs-lookup"><span data-stu-id="31a0f-182">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="31a0f-183">Просмотрите hello наиболее часто задаваемые вопросы о миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="31a0f-183">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
