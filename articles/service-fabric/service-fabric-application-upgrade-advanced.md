---
title: "aaaAdvanced обновить разделы приложений | Документы Microsoft"
description: "В этой статье рассматриваются некоторые дополнительные разделы, касающиеся tooupgrading приложения Service Fabric."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar;chackdan
ms.openlocfilehash: bdaf3db6209c574d39f57e0bf9951fad5ad1cbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a><span data-ttu-id="fe069-103">Обновление приложений Service Fabric: дополнительные разделы</span><span class="sxs-lookup"><span data-stu-id="fe069-103">Service Fabric application upgrade: advanced topics</span></span>
## <a name="adding-or-removing-services-during-an-application-upgrade"></a><span data-ttu-id="fe069-104">Добавление или удаление служб во время обновления приложения</span><span class="sxs-lookup"><span data-stu-id="fe069-104">Adding or removing services during an application upgrade</span></span>
<span data-ttu-id="fe069-105">Если это новая служба добавляется tooan приложения, который должен быть развернут и опубликован как обновление, новую службу hello — добавлены toohello развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="fe069-105">If a new service is added tooan application that is already deployed, and published as an upgrade, hello new service is added toohello deployed application.</span></span>  <span data-ttu-id="fe069-106">Такие обновления не влияет на все hello служб, которые уже были частью приложения hello.</span><span class="sxs-lookup"><span data-stu-id="fe069-106">Such an upgrade does not affect any of hello services that were already part of hello application.</span></span> <span data-ttu-id="fe069-107">Тем не менее, должен быть запущен экземпляр службы hello, который был добавлен для hello новой службы toobe active (с помощью hello `New-ServiceFabricService` командлет).</span><span class="sxs-lookup"><span data-stu-id="fe069-107">However, an instance of hello service that was added must be started for hello new service toobe active (using hello `New-ServiceFabricService` cmdlet).</span></span>

<span data-ttu-id="fe069-108">В процессе обновления службы также могут быть удалены из приложения.</span><span class="sxs-lookup"><span data-stu-id="fe069-108">Services can also be removed from an application as part of an upgrade.</span></span> <span data-ttu-id="fe069-109">Тем не менее, все текущие экземпляры hello удален в предстоит службы должна быть остановлена перед тем как продолжить обновление hello (с помощью hello `Remove-ServiceFabricService` командлет).</span><span class="sxs-lookup"><span data-stu-id="fe069-109">However, all current instances of hello to-be-deleted service must be stopped before proceeding with hello upgrade (using hello `Remove-ServiceFabricService` cmdlet).</span></span>

## <a name="manual-upgrade-mode"></a><span data-ttu-id="fe069-110">Ручной режим обновления</span><span class="sxs-lookup"><span data-stu-id="fe069-110">Manual upgrade mode</span></span>
> [!NOTE]
> <span data-ttu-id="fe069-111">только для неудачных или ожидающего обновления должны быть рассмотрены Hello не отслеживается в ручном режиме.</span><span class="sxs-lookup"><span data-stu-id="fe069-111">hello unmonitored manual mode should be considered only for a failed or suspended upgrade.</span></span> <span data-ttu-id="fe069-112">режим отслеживаемых Hello является hello рекомендуется режим обновления для приложения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fe069-112">hello monitored mode is hello recommended upgrade mode for Service Fabric applications.</span></span>
>
>

<span data-ttu-id="fe069-113">Azure Service Fabric предоставляет несколько режимов обновления кластеров toosupport разработки и эксплуатации.</span><span class="sxs-lookup"><span data-stu-id="fe069-113">Azure Service Fabric provides multiple upgrade modes toosupport development and production clusters.</span></span> <span data-ttu-id="fe069-114">Выбранные варианты развертывания для разных сред могут отличаться.</span><span class="sxs-lookup"><span data-stu-id="fe069-114">Deployment options chosen may be different for different environments.</span></span>

<span data-ttu-id="fe069-115">последовательное обновление приложения Hello отслеживаемых является наиболее типичных обновления toouse hello в рабочей среде hello.</span><span class="sxs-lookup"><span data-stu-id="fe069-115">hello monitored rolling application upgrade is hello most typical upgrade toouse in hello production environment.</span></span> <span data-ttu-id="fe069-116">При обновлении hello указана политика, Service Fabric гарантирует, что приложение hello работоспособное для продолжения обновления hello.</span><span class="sxs-lookup"><span data-stu-id="fe069-116">When hello upgrade policy is specified, Service Fabric ensures that hello application is healthy before hello upgrade proceeds.</span></span>

 <span data-ttu-id="fe069-117">Здравствуйте, администратор приложения можно использовать последовательное приложения режим обновления toohave полный контроль над ходом hello через hello различных доменов обновления вручную hello.</span><span class="sxs-lookup"><span data-stu-id="fe069-117">hello application administrator can use hello manual rolling application upgrade mode toohave total control over hello upgrade progress through hello various upgrade domains.</span></span> <span data-ttu-id="fe069-118">Этот режим удобен при политики работоспособности специальную или сложных вычислений не требуется или не обычной обновление происходит (например, приложение hello уже потери данных).</span><span class="sxs-lookup"><span data-stu-id="fe069-118">This mode is useful when a customized or complex health evaluation policy is required, or a non-conventional upgrade is happening (for example, hello application is already in data loss).</span></span>

<span data-ttu-id="fe069-119">Наконец hello автоматические обновления приложения полезен для разработки и тестирования среды tooprovide быстрого итерации цикла во время разработки службы.</span><span class="sxs-lookup"><span data-stu-id="fe069-119">Finally, hello automated rolling application upgrade is useful for development or testing environments tooprovide a fast iteration cycle during service development.</span></span>

## <a name="change-toomanual-upgrade-mode"></a><span data-ttu-id="fe069-120">Режим обновления toomanual изменений</span><span class="sxs-lookup"><span data-stu-id="fe069-120">Change toomanual upgrade mode</span></span>
<span data-ttu-id="fe069-121">**Вручную**--обновление приложения hello Stop на hello UD и изменить текущий hello обновление tooUnmonitored режим вручную.</span><span class="sxs-lookup"><span data-stu-id="fe069-121">**Manual**--Stop hello application upgrade at hello current UD and change hello upgrade mode tooUnmonitored Manual.</span></span> <span data-ttu-id="fe069-122">Hello администратор должен вызов toomanually **MoveNextApplicationUpgradeDomainAsync** tooproceed с hello обновление или запускать команду rollback с началом нового обновления.</span><span class="sxs-lookup"><span data-stu-id="fe069-122">hello administrator needs toomanually call **MoveNextApplicationUpgradeDomainAsync** tooproceed with hello upgrade or trigger a rollback by initiating a new upgrade.</span></span> <span data-ttu-id="fe069-123">После обновления hello вводит в ручном режиме hello, он остается в ручном режиме hello до запуска нового обновления.</span><span class="sxs-lookup"><span data-stu-id="fe069-123">Once hello upgrade enters into hello Manual mode, it stays in hello Manual mode until a new upgrade is initiated.</span></span> <span data-ttu-id="fe069-124">Hello **GetApplicationUpgradeProgressAsync** команда возвращает СТРУКТУРЫ\_приложения\_обновление\_состояние\_ЧЕРЕДУЮЩИМСЯ\_вперед\_ожидание.</span><span class="sxs-lookup"><span data-stu-id="fe069-124">hello **GetApplicationUpgradeProgressAsync** command returns FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING.</span></span>

## <a name="upgrade-with-a-diff-package"></a><span data-ttu-id="fe069-125">Обновление при помощи пакета diff</span><span class="sxs-lookup"><span data-stu-id="fe069-125">Upgrade with a diff package</span></span>
<span data-ttu-id="fe069-126">Приложение структуры служб может обновляться путем подготовки полного самостоятельного пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="fe069-126">A Service Fabric application can be upgraded by provisioning with a full, self-contained application package.</span></span> <span data-ttu-id="fe069-127">Также можно обновить приложения с помощью diff пакет, содержащий только файлы приложения hello обновлен, hello обновить манифест приложения, а файлы манифеста службы hello.</span><span class="sxs-lookup"><span data-stu-id="fe069-127">An application can also be upgraded by using a diff package that contains only hello updated application files, hello updated application manifest, and hello service manifest files.</span></span>

<span data-ttu-id="fe069-128">Полноценное приложение пакет содержит все необходимые toostart файлы hello и запускать приложения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fe069-128">A full application package contains all hello files necessary toostart and run a Service Fabric application.</span></span> <span data-ttu-id="fe069-129">Разница между пакет содержит только файлы hello, которые изменились в последней подготовки hello и текущее обновление hello, а также манифест полного приложения hello и hello службы файлов манифеста.</span><span class="sxs-lookup"><span data-stu-id="fe069-129">A diff package contains only hello files that changed between hello last provision and hello current upgrade, plus hello full application manifest and hello service manifest files.</span></span> <span data-ttu-id="fe069-130">Любая ссылка в манифесте приложения hello или манифест службы, который не удается найти в макете сборки hello поиск в хранилище образов hello.</span><span class="sxs-lookup"><span data-stu-id="fe069-130">Any reference in hello application manifest or service manifest that can't be found in hello build layout is searched for in hello image store.</span></span>

<span data-ttu-id="fe069-131">Пакеты полной приложений являются обязательными для установки первой hello кластера toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="fe069-131">Full application packages are required for hello first installation of an application toohello cluster.</span></span> <span data-ttu-id="fe069-132">При последующих обновлениях может использоваться либо полный пакет обновлений, либо пакет diff.</span><span class="sxs-lookup"><span data-stu-id="fe069-132">Subsequent updates can be either a full application package or a diff package.</span></span>

<span data-ttu-id="fe069-133">Случаи, в которых использование пакета diff является оптимальным.</span><span class="sxs-lookup"><span data-stu-id="fe069-133">Occasions when using a diff package would be a good choice:</span></span>

* <span data-ttu-id="fe069-134">Пакет diff предпочтительно применять тогда, когда используется объемный пакет приложения, который ссылается на несколько файлов манифеста службы или на несколько пакетов кода, пакетов конфигурации или пакетов данных.</span><span class="sxs-lookup"><span data-stu-id="fe069-134">A diff package is preferred when you have a large application package that references several service manifest files and/or several code packages, config packages, or data packages.</span></span>
* <span data-ttu-id="fe069-135">Разница между пакета является предпочтительным при наличии в системе развертывания, приводит к возникновению ошибки построения макета hello непосредственно из процесса построения приложения.</span><span class="sxs-lookup"><span data-stu-id="fe069-135">A diff package is preferred when you have a deployment system that generates hello build layout directly from your application build process.</span></span> <span data-ttu-id="fe069-136">Таким образом несмотря на то, что код hello не изменился, созданный сборки получают разные контрольные.</span><span class="sxs-lookup"><span data-stu-id="fe069-136">In this case, even though hello code hasn't changed, newly built assemblies get a different checksum.</span></span> <span data-ttu-id="fe069-137">С помощью пакета полного приложения потребуется вы tooupdate hello версии на все пакеты кода.</span><span class="sxs-lookup"><span data-stu-id="fe069-137">Using a full application package would require you tooupdate hello version on all code packages.</span></span> <span data-ttu-id="fe069-138">С помощью пакета diff, можно указать только hello файлов, которые изменены и файлы манифеста hello с измененной версии hello.</span><span class="sxs-lookup"><span data-stu-id="fe069-138">Using a diff package, you only provide hello files that changed and hello manifest files where hello version has changed.</span></span>

<span data-ttu-id="fe069-139">При обновлении приложения с помощью Visual Studio, автоматически публикуется hello diff пакета.</span><span class="sxs-lookup"><span data-stu-id="fe069-139">When an application is upgraded using Visual Studio, hello diff package is published automatically.</span></span> <span data-ttu-id="fe069-140">toocreate пакета diff hello вручную, манифест приложения и манифестов hello служб должны быть обновлены, но только hello изменены пакеты должны быть включены в пакет конечного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="fe069-140">toocreate a diff package manually, hello application manifest, and hello service manifests must be updated, but only hello changed packages should be included in hello final application package.</span></span>

<span data-ttu-id="fe069-141">Например начнем с hello следующие приложения (для простоты понимания номера версий):</span><span class="sxs-lookup"><span data-stu-id="fe069-141">For example, let's start with hello following application (version numbers provided for ease of understanding):</span></span>

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="fe069-142">Теперь предположим, что требуется, чтобы tooupdate только hello пакет кода из service1 с помощью копирования пакета с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fe069-142">Now, let's assume you wanted tooupdate only hello code package of service1 using a diff package using PowerShell.</span></span> <span data-ttu-id="fe069-143">Теперь обновленные приложения имеет hello следующая структура папок:</span><span class="sxs-lookup"><span data-stu-id="fe069-143">Now, your updated application has hello following folder structure:</span></span>

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="fe069-144">В этом случае обновление too2.0.0 манифеста приложения hello и hello манифест службы для service1 tooreflect hello код пакета обновления.</span><span class="sxs-lookup"><span data-stu-id="fe069-144">In this case, you update hello application manifest too2.0.0, and hello service manifest for service1 tooreflect hello code package update.</span></span> <span data-ttu-id="fe069-145">Hello папку для пакета приложения будет иметь hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="fe069-145">hello folder for your application package would have hello following structure:</span></span>

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a><span data-ttu-id="fe069-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fe069-146">Next steps</span></span>
<span data-ttu-id="fe069-147">[Руководство по обновлению приложений Service Fabric с помощью Visual Studio](service-fabric-application-upgrade-tutorial.md) поможет вам выполнить поэтапное обновление приложения с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe069-147">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="fe069-148">[Обновление приложения с помощью PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) поможет вам выполнить обновление приложения с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fe069-148">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="fe069-149">Управление обновлениями приложения осуществляется с помощью [параметров обновления](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="fe069-149">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="fe069-150">Обеспечить совместимость на обновление приложения путем изучения как toouse [сериализации данных](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="fe069-150">Make your application upgrades compatible by learning how toouse [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="fe069-151">Исправьте распространенных проблем в обновлений приложений с помощью ссылки действия toohello в [Устранение неполадок обновлений приложений](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="fe069-151">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
