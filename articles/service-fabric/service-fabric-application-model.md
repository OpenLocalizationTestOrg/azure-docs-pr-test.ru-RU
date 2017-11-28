---
title: "Модель приложений Azure Service Fabric | Документация Майкрософт"
description: "Описание моделирования и описания приложений и служб в Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 17a99380-5ed8-4ed9-b884-e9b827431b02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: e30482427b88eb3e58d39075c7f0734664b79aa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="model-an-application-in-service-fabric"></a><span data-ttu-id="5b3a8-103">Моделирование приложения в структуре службы</span><span class="sxs-lookup"><span data-stu-id="5b3a8-103">Model an application in Service Fabric</span></span>
<span data-ttu-id="5b3a8-104">В этой статье приведен обзор модели приложений Azure Service Fabric и описывается, как определить приложение и службу с помощью файлов манифеста.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-104">This article provides an overview of the Azure Service Fabric application model and how to define an application and service via manifest files.</span></span>

## <a name="understand-the-application-model"></a><span data-ttu-id="5b3a8-105">Сведения о модели приложения</span><span class="sxs-lookup"><span data-stu-id="5b3a8-105">Understand the application model</span></span>
<span data-ttu-id="5b3a8-106">Приложение представляет собой коллекцию составляющих его служб, которые выполняют определенные функции.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-106">An application is a collection of constituent services that perform a certain function or functions.</span></span> <span data-ttu-id="5b3a8-107">Служба выполняет завершенную и отдельную функцию и может запускаться и работать независимо от других служб.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-107">A service performs a complete and standalone function and can start and run independently of other services.</span></span>  <span data-ttu-id="5b3a8-108">Она состоит из кода, конфигурации и данных.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-108">A service is composed of code, configuration, and data.</span></span> <span data-ttu-id="5b3a8-109">Для каждой службы код состоит из исполняемых двоичных файлов, конфигурация состоит из параметров службы, которые могут быть загружены во время выполнения, а данные состоят из произвольных статических данных, которые должны обрабатываться рассматриваемой службой.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-109">For each service, code consists of the executable binaries, configuration consists of service settings that can be loaded at run time, and data consists of arbitrary static data to be consumed by the service.</span></span> <span data-ttu-id="5b3a8-110">Каждый компонент в этой иерархической модели приложения может иметь свою версию и обновляться независимо.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-110">Each component in this hierarchical application model can be versioned and upgraded independently.</span></span>

![Модель приложения Service Fabric][appmodel-diagram]

<span data-ttu-id="5b3a8-112">Тип приложения представляет собой отнесение приложения к определенной категории и состоит из пакета типов служб.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-112">An application type is a categorization of an application and consists of a bundle of service types.</span></span> <span data-ttu-id="5b3a8-113">Тип службы представляет собой отнесение службы к определенной категории,</span><span class="sxs-lookup"><span data-stu-id="5b3a8-113">A service type is a categorization of a service.</span></span> <span data-ttu-id="5b3a8-114">которая может обладать различными параметрами и конфигурациями, однако ее основная функция не изменяется.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-114">The categorization can have different settings and configurations, but the core functionality remains the same.</span></span> <span data-ttu-id="5b3a8-115">Экземпляры службы представляют собой различные вариации конфигурации служб, принадлежащих к одному типу.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-115">The instances of a service are the different service configuration variations of the same service type.</span></span>  

<span data-ttu-id="5b3a8-116">Классы (или типы) приложений и служб описываются с помощью XML-файлов (манифесты приложений и служб).</span><span class="sxs-lookup"><span data-stu-id="5b3a8-116">Classes (or "types") of applications and services are described through XML files (application manifests and service manifests).</span></span>  <span data-ttu-id="5b3a8-117">Манифесты представляют собой шаблоны, по которым создаются экземпляры приложений из хранилища образов кластера.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-117">The manifests are the templates against which applications can be instantiated from the cluster's image store.</span></span> <span data-ttu-id="5b3a8-118">Определение схемы для файла ServiceManifest.xml и ApplicationManifest.xml устанавливается с пакетом SDK и средствами для Service Fabric по адресу *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-118">The schema definition for the ServiceManifest.xml and ApplicationManifest.xml file is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

<span data-ttu-id="5b3a8-119">Код для различных экземпляров приложений выполняется как отдельные процессы, даже если они размещены на одном узле структуры службы.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-119">The code for different application instances run as separate processes even when hosted by the same Service Fabric node.</span></span> <span data-ttu-id="5b3a8-120">Кроме того, возможно независимое управление жизненным циклом (например, обновление).</span><span class="sxs-lookup"><span data-stu-id="5b3a8-120">Furthermore, the lifecycle of each application instance can be managed (for example, upgraded) independently.</span></span> <span data-ttu-id="5b3a8-121">На следующей диаграмме показано, что типы приложений состоят из типов служб, которые, в свою очередь, состоят из кода, конфигурации и пакетов данных.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-121">The following diagram shows how application types are composed of service types, which in turn are composed of code, configuration, and data packages.</span></span> <span data-ttu-id="5b3a8-122">Чтобы упростить схему, показаны только пакеты кода, конфигурации или данных для `ServiceType4`, хотя каждый тип службы будет включать некоторые или все из этих типов пакетов.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-122">To simplify the diagram, only the code/config/data packages for `ServiceType4` are shown, though each service type would include some or all those package types.</span></span>

![Типы служб и типы приложений Service Fabric][cluster-imagestore-apptypes]

<span data-ttu-id="5b3a8-124">Два разных файла манифестов используются для описания приложения и служб: манифест служб и манифест приложений.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-124">Two different manifest files are used to describe applications and services: the service manifest and application manifest.</span></span> <span data-ttu-id="5b3a8-125">Манифесты подробно рассматриваются в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-125">Manifests are covered in detail in the following sections.</span></span>

<span data-ttu-id="5b3a8-126">В кластере может работать один или несколько экземпляров службы определенного типа.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-126">There can be one or more instances of a service type active in the cluster.</span></span> <span data-ttu-id="5b3a8-127">Например, в экземплярах служб с отслеживанием состояния или в репликах достигается высокий уровень доступности за счет репликации состояния между репликами, размещенными на разных узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-127">For example, stateful service instances, or replicas, achieve high reliability by replicating state between replicas located on different nodes in the cluster.</span></span> <span data-ttu-id="5b3a8-128">Репликация обеспечивает избыточность, необходимую для обеспечения доступности службы, даже когда на одном из узлов кластера происходит сбой.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-128">Replication essentially provides redundancy for the service to be available even if one node in a cluster fails.</span></span> <span data-ttu-id="5b3a8-129">При использовании [разделенной службы](service-fabric-concepts-partitioning.md) выполняется дальнейшее разделение ее состояния (а также алгоритмов доступа к этому состоянию) на всех узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-129">A [partitioned service](service-fabric-concepts-partitioning.md) further divides its state (and access patterns to that state) across nodes in the cluster.</span></span>

<span data-ttu-id="5b3a8-130">На следующей диаграмме отображается отношение между приложениями и экземплярами службы, разделами и репликами.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-130">The following diagram shows the relationship between applications and service instances, partitions, and replicas.</span></span>

![Разделы и реплики в службе][cluster-application-instances]

> [!TIP]
> <span data-ttu-id="5b3a8-132">Просмотреть структуру приложений в кластере можно с помощью обозревателя Service Fabric, доступного по адресу http://&lt;адрес_кластера&gt;:19080/Explorer.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-132">You can view the layout of applications in a cluster using the Service Fabric Explorer tool available at http://&lt;yourclusteraddress&gt;:19080/Explorer.</span></span> <span data-ttu-id="5b3a8-133">Дополнительные сведения см. в статье [Визуализация кластера с помощью обозревателя Service Fabric](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="5b3a8-133">For more information, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
> 
> 

## <a name="describe-a-service"></a><span data-ttu-id="5b3a8-134">Описание службы</span><span class="sxs-lookup"><span data-stu-id="5b3a8-134">Describe a service</span></span>
<span data-ttu-id="5b3a8-135">Манифест службы декларативно определяет тип и версию службы.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-135">The service manifest declaratively defines the service type and version.</span></span> <span data-ttu-id="5b3a8-136">Он задает метаданные службы, такие как тип службы, свойства работоспособности, метрики балансировки нагрузки, двоичные файлы службы и файлы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-136">It specifies service metadata such as service type, health properties, load-balancing metrics, service binaries, and configuration files.</span></span>  <span data-ttu-id="5b3a8-137">Другими словами, в нем описывается код, конфигурация и пакеты данных, из которых состоит пакет службы, для поддержки одного или нескольких типов служб.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-137">Put another way, it describes the code, configuration, and data packages that compose a service package to support one or more service types.</span></span> <span data-ttu-id="5b3a8-138">Ниже приведен простой пример манифеста служб.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-138">Here is a simple example service manifest:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```

<span data-ttu-id="5b3a8-139">**Версия** представляют собой неструктурированные строки, которые не обрабатываются системой.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-139">**Version** attributes are unstructured strings and not parsed by the system.</span></span> <span data-ttu-id="5b3a8-140">Атрибуты версии используются в целях указания версии каждого компонента для последующего обновления.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-140">Version attributes are used to version each component for upgrades.</span></span>

<span data-ttu-id="5b3a8-141">В атрибуте **ServiceTypes** указывается, какие типы служб поддерживаются пакетами **CodePackages** в этом манифесте.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-141">**ServiceTypes** declares what service types are supported by **CodePackages** in this manifest.</span></span> <span data-ttu-id="5b3a8-142">При создании экземпляра службы в соответствии с одним из этих типов службы все пакеты кода, объявленные в этом манифесте, активируются путем запуска соответствующих точек входа.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-142">When a service is instantiated against one of these service types, all code packages declared in this manifest are activated by running their entry points.</span></span> <span data-ttu-id="5b3a8-143">Запущенные вследствие этого процессы должны зарегистрировать поддерживаемые типы служб во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-143">The resulting processes are expected to register the supported service types at run time.</span></span> <span data-ttu-id="5b3a8-144">Типы служб декларируются на уровне манифеста, а не на уровне пакета кода.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-144">Service types are declared at the manifest level and not the code package level.</span></span> <span data-ttu-id="5b3a8-145">Поэтому при наличии нескольких пакетов кода они все активируются при поиске системой любого из задекларированных типов служб.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-145">So when there are multiple code packages, they are all activated whenever the system looks for any one of the declared service types.</span></span>

<span data-ttu-id="5b3a8-146">**SetupEntryPoint** — это привилегированная точка входа, которая запускается с теми же учетными данными, что и структура службы (обычно это локальная учетная запись *LocalSystem* ), перед тем, как будут запущены любые другие точки входа.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-146">**SetupEntryPoint** is a privileged entry point that runs with the same credentials as Service Fabric (typically the *LocalSystem* account) before any other entry point.</span></span> <span data-ttu-id="5b3a8-147">Исполняемый файл, указанный в точке входа **EntryPoint** , обычно является узлом службы, запускаемым на длительный срок.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-147">The executable specified by **EntryPoint** is typically the long-running service host.</span></span> <span data-ttu-id="5b3a8-148">Наличие отдельной точки входа настройки позволяет избежать необходимости в выполнении узла службы с расширенными правами в течение длительного срока.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-148">The presence of a separate setup entry point avoids having to run the service host with high privileges for extended periods of time.</span></span> <span data-ttu-id="5b3a8-149">Исполняемый файл, указанный в точке входа **EntryPoint**, запускается после успешного выхода из точки **SetupEntryPoint**.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-149">The executable specified by **EntryPoint** is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="5b3a8-150">Даже если произошло непредвиденное завершение работы процесса или его сбой, возникающий вследствие этого, процесс отслеживается и перезапускается (снова начиная с точки входа **SetupEntryPoint**).</span><span class="sxs-lookup"><span data-stu-id="5b3a8-150">If the process ever terminates or crashes, the resulting process is monitored and restarted (beginning again with **SetupEntryPoint**).</span></span>  

<span data-ttu-id="5b3a8-151">Типичные сценарии использования **SetupEntryPoint** относятся к ситуации, когда вы запускаете исполняемый файл перед запуском службы или выполняете операцию с повышенными привилегиями.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-151">Typical scenarios for using **SetupEntryPoint** are when you run an executable before the service starts or you perform an operation with elevated privileges.</span></span> <span data-ttu-id="5b3a8-152">Например:</span><span class="sxs-lookup"><span data-stu-id="5b3a8-152">For example:</span></span>

* <span data-ttu-id="5b3a8-153">Настройка и инициализация переменных среды, необходимых исполняемому файлу службы.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-153">Setting up and initializing environment variables that the service executable needs.</span></span> <span data-ttu-id="5b3a8-154">Это касается не только исполняемых файлов, написанных с использованием моделей программирования Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-154">This is not limited to only executables written via the Service Fabric programming models.</span></span> <span data-ttu-id="5b3a8-155">Например, npm.exe нужны определенные переменные среды, настроенные для развертывания приложения node.js.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-155">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="5b3a8-156">Настройка контроля доступа посредством установки сертификатов безопасности.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-156">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="5b3a8-157">Дополнительные сведения о настройке **SetupEntryPoint** см. в разделе [Настройка политик безопасности для приложения](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="5b3a8-157">For more details on how to configure the **SetupEntryPoint** see [Configure the policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<span data-ttu-id="5b3a8-158">**EnvironmentVariables** содержит список переменных среды, которые заданы для этого пакета кода.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-158">**EnvironmentVariables** provides a list of environment variables that are set for this code package.</span></span> <span data-ttu-id="5b3a8-159">Переменные среды можно переопределить в `ApplicationManifest.xml`, что позволяет указывать разные значения для различных экземпляров службы.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-159">Environmentment variables can be overridden in the `ApplicationManifest.xml` to provide different values for different service instances.</span></span> 

<span data-ttu-id="5b3a8-160">Атрибут **DataPackage** объявляет папку с именем, указанным в атрибуте **Name**, содержащим произвольные статические данные, которые должны обрабатываться процессом во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-160">**DataPackage** declares a folder, named by the **Name** attribute, that contains arbitrary static data to be consumed by the process at run time.</span></span>

<span data-ttu-id="5b3a8-161">**ConfigPackage** объявляет папку с именем, указанным в атрибуте **Name**, которая содержит файл *Settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-161">**ConfigPackage** declares a folder, named by the **Name** attribute, that contains a *Settings.xml* file.</span></span> <span data-ttu-id="5b3a8-162">Файл параметров содержит разделы заданных пользователем параметров пар "ключ — значение", которые считываются процессом во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-162">The settings file contains sections of user-defined, key-value pair settings that the process reads back at run time.</span></span> <span data-ttu-id="5b3a8-163">Во время обновления при изменении одного только атрибута **version** для **ConfigPackage** перезапуск процесса не выполняется.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-163">During an upgrade, if only the **ConfigPackage** **version** has changed, then the running process is not restarted.</span></span> <span data-ttu-id="5b3a8-164">Вместо этого при помощи обратного вызова в процесс передается уведомление о том, что параметры конфигурации изменились, поэтому они были перезагружены в динамическом режиме.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-164">Instead, a callback notifies the process that configuration settings have changed so they can be reloaded dynamically.</span></span> <span data-ttu-id="5b3a8-165">Ниже приведен пример файла *Settings.xml* .</span><span class="sxs-lookup"><span data-stu-id="5b3a8-165">Here is an example *Settings.xml* file:</span></span>

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> <span data-ttu-id="5b3a8-166">Манифест служб может содержать множество пакетов кода, конфигураций и данных.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-166">A service manifest can contain multiple code, configuration, and data packages.</span></span> <span data-ttu-id="5b3a8-167">Версия каждого из них устанавливается независимо.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-167">Each of those can be versioned independently.</span></span>
> 
> 

<!--
For more information about other features supported by service manifests, refer to the following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a><span data-ttu-id="5b3a8-168">Описание приложения</span><span class="sxs-lookup"><span data-stu-id="5b3a8-168">Describe an application</span></span>
<span data-ttu-id="5b3a8-169">Манифест приложения декларативно описывает тип приложения и его версию.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-169">The application manifest declaratively describes the application type and version.</span></span> <span data-ttu-id="5b3a8-170">Он также указывает метаданные композиции службы, такие как стабильные имена, схема секционирования, число экземпляров и коэффициент репликации, политика безопасности и изоляции, ограничения на размещение, переопределения конфигурации и типы входящих в состав служб.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-170">It specifies service composition metadata such as stable names, partitioning scheme, instance count/replication factor, security/isolation policy, placement constraints, configuration overrides, and constituent service types.</span></span> <span data-ttu-id="5b3a8-171">Также в нем описываются домены балансировки нагрузки, в которых размещается приложение.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-171">The load-balancing domains into which the application is placed are also described.</span></span>

<span data-ttu-id="5b3a8-172">Таким образом, манифест приложения описывает элементы на уровне приложения и ссылается на один или несколько манифестов службы, которые составляют тип приложения.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-172">Thus, an application manifest describes elements at the application level and references one or more service manifests to compose an application type.</span></span> <span data-ttu-id="5b3a8-173">Ниже приведен простой пример манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-173">Here is a simple example application manifest:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ApplicationManifest
      ApplicationTypeName="MyApplicationType"
      ApplicationTypeVersion="AppManifestVersion1"
      xmlns="http://schemas.microsoft.com/2011/01/fabric"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example application manifest</Description>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="MyServiceManifest" ServiceManifestVersion="SvcManifestVersion1"/>
    <ConfigOverrides/>
    <EnvironmentOverrides CodePackageRef="MyCode"/>
  </ServiceManifestImport>
  <DefaultServices>
     <Service Name="MyService">
         <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
             <SingletonPartition/>
         </StatelessService>
     </Service>
  </DefaultServices>
</ApplicationManifest>
```

<span data-ttu-id="5b3a8-174">Точно так же, как и в манифестах служб, атрибуты версии **Version** представляют собой неструктурированные строки, которые не анализируются системой.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-174">Like service manifests, **Version** attributes are unstructured strings and are not parsed by the system.</span></span> <span data-ttu-id="5b3a8-175">Атрибуты версии также используются в целях указания версии каждого компонента для последующего обновления.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-175">Version attributes are also used to version each component for upgrades.</span></span>

<span data-ttu-id="5b3a8-176">**ServiceManifestImport** содержит ссылки на манифесты служб, из которых состоит этот тип приложения.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-176">**ServiceManifestImport** contains references to service manifests that compose this application type.</span></span> <span data-ttu-id="5b3a8-177">Импортированные манифесты служб определяют, какие типы служб допустимы для применения в приложении этого типа.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-177">Imported service manifests determine what service types are valid within this application type.</span></span> <span data-ttu-id="5b3a8-178">В ServiceManifestImport можно переопределить значения конфигурации в файле Settings.xml и переменные среды в файле ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-178">Within the ServiceManifestImport, you override configuration values in Settings.xml and environment variables in ServiceManifest.xml files.</span></span> 


<span data-ttu-id="5b3a8-179">**DefaultServices** декларируются экземпляры служб, которые создаются автоматически при создании экземпляра приложения в соответствии с его типом.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-179">**DefaultServices** declares service instances that are automatically created whenever an application is instantiated against this application type.</span></span> <span data-ttu-id="5b3a8-180">Службы по умолчанию используются только для удобства и после создания во всех отношениях действуют как и обычные службы.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-180">Default services are just a convenience and behave like normal services in every respect after they have been created.</span></span> <span data-ttu-id="5b3a8-181">Они обновляются вместе с любыми другими службами в экземпляре приложения, а также могут быть удалены.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-181">They are upgraded along with any other services in the application instance and can be removed as well.</span></span>

> [!NOTE]
> <span data-ttu-id="5b3a8-182">Манифест приложения может содержать несколько импортированных манифестов служб и служб по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-182">An application manifest can contain multiple service manifest imports and default services.</span></span> <span data-ttu-id="5b3a8-183">Каждый импортированный манифест служб может иметь свою версию.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-183">Each service manifest import can be versioned independently.</span></span>
> 
> 

<span data-ttu-id="5b3a8-184">Сведения об использовании разных параметров приложений и служб для отдельных сред см. в статье [Управление параметрами приложения для нескольких сред](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="5b3a8-184">To learn how to maintain different application and service parameters for individual environments, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

<!--
For more information about other features supported by application manifests, refer to the following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a><span data-ttu-id="5b3a8-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5b3a8-185">Next steps</span></span>
<span data-ttu-id="5b3a8-186">[Создайте пакет приложения](service-fabric-package-apps.md) и подготовьте его к развертыванию.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-186">[Package an application](service-fabric-package-apps.md) and make it ready to deploy.</span></span>

<span data-ttu-id="5b3a8-187">В статье [Развертывание и удаление приложений с помощью PowerShell][10] вы узнаете, как управлять экземплярами приложений с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-187">[Deploy and remove applications][10] describes how to use PowerShell to manage application instances.</span></span>

<span data-ttu-id="5b3a8-188">В статье [Управление параметрами приложения для нескольких сред][11] описано, как настроить параметры и переменные среды для различных экземпляров приложений.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-188">[Managing application parameters for multiple environments][11] describes how to configure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="5b3a8-189">В статье [Настройка политик безопасности для приложения][12] содержатся данные о работе служб в соответствии с политиками безопасности, ограничивающими доступ.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-189">[Configure security policies for your application][12] describes how to run services under security policies to restrict access.</span></span>

<span data-ttu-id="5b3a8-190">В статье [Модель размещения Service Fabric][13] рассматривается связь между репликами (или экземплярами) развернутой службы и процессом размещения службы.</span><span class="sxs-lookup"><span data-stu-id="5b3a8-190">[Application hosting models][13] describe relationship between replicas (or instances) of a deployed service and service-host process.</span></span>

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
