---
title: "Дополнительные разделы об обновлении приложений | Документация Майкрософт"
description: "В этой статье рассматриваются некоторые дополнительные темы, относящиеся к обновлению приложения Service Fabric."
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
ms.openlocfilehash: 8d3b922f3d50b645ac9db2cc879a319df1262e0a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a><span data-ttu-id="7acb5-103">Обновление приложений Service Fabric: дополнительные разделы</span><span class="sxs-lookup"><span data-stu-id="7acb5-103">Service Fabric application upgrade: advanced topics</span></span>
## <a name="adding-or-removing-services-during-an-application-upgrade"></a><span data-ttu-id="7acb5-104">Добавление или удаление служб во время обновления приложения</span><span class="sxs-lookup"><span data-stu-id="7acb5-104">Adding or removing services during an application upgrade</span></span>
<span data-ttu-id="7acb5-105">Если в приложение, которое уже развернуто и опубликовано как обновление, добавляется новая служба, то она добавляется в развернутое приложение Подобные обновления не влияет на какие-либо службы, которые уже были частью приложения.</span><span class="sxs-lookup"><span data-stu-id="7acb5-105">If a new service is added to an application that is already deployed, and published as an upgrade, the new service is added to the deployed application.</span></span>  <span data-ttu-id="7acb5-106">Однако чтобы активировать новую службу, требуется запустить экземпляр службы, который был добавлен.</span><span class="sxs-lookup"><span data-stu-id="7acb5-106">Such an upgrade does not affect any of the services that were already part of the application.</span></span> <span data-ttu-id="7acb5-107">Запуск следует выполнить с помощью командлета `New-ServiceFabricService` .</span><span class="sxs-lookup"><span data-stu-id="7acb5-107">However, an instance of the service that was added must be started for the new service to be active (using the `New-ServiceFabricService` cmdlet).</span></span>

<span data-ttu-id="7acb5-108">В процессе обновления службы также могут быть удалены из приложения.</span><span class="sxs-lookup"><span data-stu-id="7acb5-108">Services can also be removed from an application as part of an upgrade.</span></span> <span data-ttu-id="7acb5-109">Но в этом случае перед продолжением обновления все текущие экземпляры удаляемой службы должны быть остановлены (с помощью командлета `Remove-ServiceFabricService` ).</span><span class="sxs-lookup"><span data-stu-id="7acb5-109">However, all current instances of the to-be-deleted service must be stopped before proceeding with the upgrade (using the `Remove-ServiceFabricService` cmdlet).</span></span>

## <a name="manual-upgrade-mode"></a><span data-ttu-id="7acb5-110">Ручной режим обновления</span><span class="sxs-lookup"><span data-stu-id="7acb5-110">Manual upgrade mode</span></span>
> [!NOTE]
> <span data-ttu-id="7acb5-111">Неотслеживаемый ручной режим должен использоваться только для сбойных или отложенных обновлений.</span><span class="sxs-lookup"><span data-stu-id="7acb5-111">The unmonitored manual mode should be considered only for a failed or suspended upgrade.</span></span> <span data-ttu-id="7acb5-112">Отслеживаемый режим рекомендуется для использования с приложениями Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7acb5-112">The monitored mode is the recommended upgrade mode for Service Fabric applications.</span></span>
>
>

<span data-ttu-id="7acb5-113">Service Fabric обеспечивает применение нескольких режимов обновления для поддержки кластеров разработки и рабочих кластеров.</span><span class="sxs-lookup"><span data-stu-id="7acb5-113">Azure Service Fabric provides multiple upgrade modes to support development and production clusters.</span></span> <span data-ttu-id="7acb5-114">Выбранные варианты развертывания для разных сред могут отличаться.</span><span class="sxs-lookup"><span data-stu-id="7acb5-114">Deployment options chosen may be different for different environments.</span></span>

<span data-ttu-id="7acb5-115">Отслеживаемое последовательное обновление приложений — наиболее распространенный тип обновления, используемого в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="7acb5-115">The monitored rolling application upgrade is the most typical upgrade to use in the production environment.</span></span> <span data-ttu-id="7acb5-116">При определении политики обновления структура служб обеспечивает работоспособность приложения перед продолжением обновления.</span><span class="sxs-lookup"><span data-stu-id="7acb5-116">When the upgrade policy is specified, Service Fabric ensures that the application is healthy before the upgrade proceeds.</span></span>

 <span data-ttu-id="7acb5-117">Администратор приложения может использовать режим ручного последовательного обновления приложений для обеспечения полного контроля над ходом процесса обновления для различных доменов обновления.</span><span class="sxs-lookup"><span data-stu-id="7acb5-117">The application administrator can use the manual rolling application upgrade mode to have total control over the upgrade progress through the various upgrade domains.</span></span> <span data-ttu-id="7acb5-118">Этот режим удобен, когда необходима настраиваемая или сложная политика оценки работоспособности или осуществляется нестандартное обновление (например, приложение уже потеряло некоторые данные).</span><span class="sxs-lookup"><span data-stu-id="7acb5-118">This mode is useful when a customized or complex health evaluation policy is required, or a non-conventional upgrade is happening (for example, the application is already in data loss).</span></span>

<span data-ttu-id="7acb5-119">Наконец, автоматизированное последовательное обновление полезно для сред разработки или тестирования, что обеспечивает быстрый цикл итераций во время разработки службы.</span><span class="sxs-lookup"><span data-stu-id="7acb5-119">Finally, the automated rolling application upgrade is useful for development or testing environments to provide a fast iteration cycle during service development.</span></span>

## <a name="change-to-manual-upgrade-mode"></a><span data-ttu-id="7acb5-120">Переключение в ручной режим обновления</span><span class="sxs-lookup"><span data-stu-id="7acb5-120">Change to manual upgrade mode</span></span>
<span data-ttu-id="7acb5-121">**Ручной.** Остановите обновление приложения на текущем домене обновления и измените режим обновления на Unmonitored Manual (Неотслеживаемый ручной).</span><span class="sxs-lookup"><span data-stu-id="7acb5-121">**Manual**--Stop the application upgrade at the current UD and change the upgrade mode to Unmonitored Manual.</span></span> <span data-ttu-id="7acb5-122">Администратору необходимо вручную вызвать команду **MoveNextApplicationUpgradeDomainAsync**, чтобы продолжить обновление, или запустить откат, начав новое обновление.</span><span class="sxs-lookup"><span data-stu-id="7acb5-122">The administrator needs to manually call **MoveNextApplicationUpgradeDomainAsync** to proceed with the upgrade or trigger a rollback by initiating a new upgrade.</span></span> <span data-ttu-id="7acb5-123">После того как обновление перейдет в ручной режим, оно остается в нем до тех пор, пока не будет запущено новое обновление.</span><span class="sxs-lookup"><span data-stu-id="7acb5-123">Once the upgrade enters into the Manual mode, it stays in the Manual mode until a new upgrade is initiated.</span></span> <span data-ttu-id="7acb5-124">Команда **GetApplicationUpgradeProgressAsync** возвращает FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING.</span><span class="sxs-lookup"><span data-stu-id="7acb5-124">The **GetApplicationUpgradeProgressAsync** command returns FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING.</span></span>

## <a name="upgrade-with-a-diff-package"></a><span data-ttu-id="7acb5-125">Обновление при помощи пакета diff</span><span class="sxs-lookup"><span data-stu-id="7acb5-125">Upgrade with a diff package</span></span>
<span data-ttu-id="7acb5-126">Приложение структуры служб может обновляться путем подготовки полного самостоятельного пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="7acb5-126">A Service Fabric application can be upgraded by provisioning with a full, self-contained application package.</span></span> <span data-ttu-id="7acb5-127">Приложение может также быть обновлено путем использования пакета diff, который содержит только обновленные файлы приложения и манифеста приложения , а также файлы манифеста служб.</span><span class="sxs-lookup"><span data-stu-id="7acb5-127">An application can also be upgraded by using a diff package that contains only the updated application files, the updated application manifest, and the service manifest files.</span></span>

<span data-ttu-id="7acb5-128">Полный пакет приложений содержит все необходимые файлы для запуска и выполнения приложения структуры служб.</span><span class="sxs-lookup"><span data-stu-id="7acb5-128">A full application package contains all the files necessary to start and run a Service Fabric application.</span></span> <span data-ttu-id="7acb5-129">Пакет diff содержит только файлы, которые изменились между последним выделением приложения и текущим обновлением, плюс полные файлы манифеста приложения и служб.</span><span class="sxs-lookup"><span data-stu-id="7acb5-129">A diff package contains only the files that changed between the last provision and the current upgrade, plus the full application manifest and the service manifest files.</span></span> <span data-ttu-id="7acb5-130">Если в макете сборки не удается найти ссылку, указанную в манифесте приложения или манифесте служб, то будет предпринята попытка найти ее в хранилище образов.</span><span class="sxs-lookup"><span data-stu-id="7acb5-130">Any reference in the application manifest or service manifest that can't be found in the build layout is searched for in the image store.</span></span>

<span data-ttu-id="7acb5-131">Для первичной установки приложений в кластер необходимы полные пакеты приложений.</span><span class="sxs-lookup"><span data-stu-id="7acb5-131">Full application packages are required for the first installation of an application to the cluster.</span></span> <span data-ttu-id="7acb5-132">При последующих обновлениях может использоваться либо полный пакет обновлений, либо пакет diff.</span><span class="sxs-lookup"><span data-stu-id="7acb5-132">Subsequent updates can be either a full application package or a diff package.</span></span>

<span data-ttu-id="7acb5-133">Случаи, в которых использование пакета diff является оптимальным.</span><span class="sxs-lookup"><span data-stu-id="7acb5-133">Occasions when using a diff package would be a good choice:</span></span>

* <span data-ttu-id="7acb5-134">Пакет diff предпочтительно применять тогда, когда используется объемный пакет приложения, который ссылается на несколько файлов манифеста службы или на несколько пакетов кода, пакетов конфигурации или пакетов данных.</span><span class="sxs-lookup"><span data-stu-id="7acb5-134">A diff package is preferred when you have a large application package that references several service manifest files and/or several code packages, config packages, or data packages.</span></span>
* <span data-ttu-id="7acb5-135">Использование пакета diff является предпочтительным в случае, если система развертывания формирует структуру сборки напрямую в ходе создания сборки приложения.</span><span class="sxs-lookup"><span data-stu-id="7acb5-135">A diff package is preferred when you have a deployment system that generates the build layout directly from your application build process.</span></span> <span data-ttu-id="7acb5-136">В этом случае, хотя в самом коде ничего не изменилось, новые сборки будут обладать другой контрольной суммой.</span><span class="sxs-lookup"><span data-stu-id="7acb5-136">In this case, even though the code hasn't changed, newly built assemblies get a different checksum.</span></span> <span data-ttu-id="7acb5-137">Использование полного пакета приложения потребует обновления версии всех пакетов кода.</span><span class="sxs-lookup"><span data-stu-id="7acb5-137">Using a full application package would require you to update the version on all code packages.</span></span> <span data-ttu-id="7acb5-138">При использовании пакета diff вы предоставляете только измененные файлы и файлы манифеста, версия которых изменилась.</span><span class="sxs-lookup"><span data-stu-id="7acb5-138">Using a diff package, you only provide the files that changed and the manifest files where the version has changed.</span></span>

<span data-ttu-id="7acb5-139">При обновлении приложения с помощью Visual Studio пакет diff публикуется автоматически.</span><span class="sxs-lookup"><span data-stu-id="7acb5-139">When an application is upgraded using Visual Studio, the diff package is published automatically.</span></span> <span data-ttu-id="7acb5-140">Чтобы создать пакет diff вручную, необходимо обновить манифест приложения и манифесты служб, но только измененные пакеты должны быть включены в финальный пакет приложения.</span><span class="sxs-lookup"><span data-stu-id="7acb5-140">To create a diff package manually, the application manifest, and the service manifests must be updated, but only the changed packages should be included in the final application package.</span></span>

<span data-ttu-id="7acb5-141">К примеру, начнем со следующего приложения (номера версий приведены для простоты понимания):</span><span class="sxs-lookup"><span data-stu-id="7acb5-141">For example, let's start with the following application (version numbers provided for ease of understanding):</span></span>

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="7acb5-142">Предположим, что необходимо обновить только код пакета service1, использующего пакет diff, с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7acb5-142">Now, let's assume you wanted to update only the code package of service1 using a diff package using PowerShell.</span></span> <span data-ttu-id="7acb5-143">Теперь обновленное приложение имеет приведенную ниже структуру папок.</span><span class="sxs-lookup"><span data-stu-id="7acb5-143">Now, your updated application has the following folder structure:</span></span>

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="7acb5-144">В этом случае вы обновляете манифест приложения до версии 2.0.0 и манифест службы для service1 для отражения обновления пакета кода.</span><span class="sxs-lookup"><span data-stu-id="7acb5-144">In this case, you update the application manifest to 2.0.0, and the service manifest for service1 to reflect the code package update.</span></span> <span data-ttu-id="7acb5-145">Структура папок для пакета приложения будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="7acb5-145">The folder for your application package would have the following structure:</span></span>

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a><span data-ttu-id="7acb5-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7acb5-146">Next steps</span></span>
<span data-ttu-id="7acb5-147">[Руководство по обновлению приложений Service Fabric с помощью Visual Studio](service-fabric-application-upgrade-tutorial.md) поможет вам выполнить поэтапное обновление приложения с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7acb5-147">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="7acb5-148">[Обновление приложения с помощью PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) поможет вам выполнить обновление приложения с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7acb5-148">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="7acb5-149">Управление обновлениями приложения осуществляется с помощью [параметров обновления](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="7acb5-149">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="7acb5-150">Узнайте, как использовать [сериализацию данных](service-fabric-application-upgrade-data-serialization.md), чтобы обеспечить совместимость обновлений приложения.</span><span class="sxs-lookup"><span data-stu-id="7acb5-150">Make your application upgrades compatible by learning how to use [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="7acb5-151">Сведения об устранении распространенных проблем при обновлении приложений см. в статье [Устранение неполадок при обновлениях приложений](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="7acb5-151">Fix common problems in application upgrades by referring to the steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
