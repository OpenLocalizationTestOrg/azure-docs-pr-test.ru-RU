---
title: "модель приложения Service Fabric aaaAzure | Документы Microsoft"
description: "Как toomodel и описание для приложений и служб в Service Fabric."
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
ms.openlocfilehash: 54c4d026e7d556be5f697d4a6f2ee886687e1c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="model-an-application-in-service-fabric"></a><span data-ttu-id="dc8a1-103">Моделирование приложения в структуре службы</span><span class="sxs-lookup"><span data-stu-id="dc8a1-103">Model an application in Service Fabric</span></span>
<span data-ttu-id="dc8a1-104">Это статье представлен обзор модели приложения hello Azure Service Fabric и как toodefine приложения и службы через файлов манифеста.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-104">This article provides an overview of hello Azure Service Fabric application model and how toodefine an application and service via manifest files.</span></span>

## <a name="understand-hello-application-model"></a><span data-ttu-id="dc8a1-105">Понять модель приложения hello</span><span class="sxs-lookup"><span data-stu-id="dc8a1-105">Understand hello application model</span></span>
<span data-ttu-id="dc8a1-106">Приложение представляет собой коллекцию составляющих его служб, которые выполняют определенные функции.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-106">An application is a collection of constituent services that perform a certain function or functions.</span></span> <span data-ttu-id="dc8a1-107">Служба выполняет завершенную и отдельную функцию и может запускаться и работать независимо от других служб.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-107">A service performs a complete and standalone function and can start and run independently of other services.</span></span>  <span data-ttu-id="dc8a1-108">Она состоит из кода, конфигурации и данных.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-108">A service is composed of code, configuration, and data.</span></span> <span data-ttu-id="dc8a1-109">Для каждой службы код состоит из исполняемого hello двоичные файлы, Настройка включает в себя параметры службы, которые могут быть загружены во время выполнения и данные состоят из toobe произвольный статические данные, используются службой hello.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-109">For each service, code consists of hello executable binaries, configuration consists of service settings that can be loaded at run time, and data consists of arbitrary static data toobe consumed by hello service.</span></span> <span data-ttu-id="dc8a1-110">Каждый компонент в этой иерархической модели приложения может иметь свою версию и обновляться независимо.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-110">Each component in this hierarchical application model can be versioned and upgraded independently.</span></span>

![модель приложения Hello Service Fabric][appmodel-diagram]

<span data-ttu-id="dc8a1-112">Тип приложения представляет собой отнесение приложения к определенной категории и состоит из пакета типов служб.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-112">An application type is a categorization of an application and consists of a bundle of service types.</span></span> <span data-ttu-id="dc8a1-113">Тип службы представляет собой отнесение службы к определенной категории,</span><span class="sxs-lookup"><span data-stu-id="dc8a1-113">A service type is a categorization of a service.</span></span> <span data-ttu-id="dc8a1-114">Hello классификации может иметь различные параметры и конфигурации, но hello hello основные функциональные возможности остаются одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-114">hello categorization can have different settings and configurations, but hello core functionality remains hello same.</span></span> <span data-ttu-id="dc8a1-115">Hello экземпляров службы являются hello различные варианты конфигурации из hello же тип службы.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-115">hello instances of a service are hello different service configuration variations of hello same service type.</span></span>  

<span data-ttu-id="dc8a1-116">Классы (или типы) приложений и служб описываются с помощью XML-файлов (манифесты приложений и служб).</span><span class="sxs-lookup"><span data-stu-id="dc8a1-116">Classes (or "types") of applications and services are described through XML files (application manifests and service manifests).</span></span>  <span data-ttu-id="dc8a1-117">Hello манифесты являются шаблонами hello, по которым приложений может быть создан из хранилища образов hello кластера.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-117">hello manifests are hello templates against which applications can be instantiated from hello cluster's image store.</span></span> <span data-ttu-id="dc8a1-118">Hello определение схемы для файла ServiceManifest.xml и ApplicationManifest.xml hello устанавливается вместе с hello Service Fabric SDK и средств слишком*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-118">hello schema definition for hello ServiceManifest.xml and ApplicationManifest.xml file is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

<span data-ttu-id="dc8a1-119">Код Hello для экземпляров другое приложение выполняется как отдельные процессы даже если они размещаются в одном узле Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-119">hello code for different application instances run as separate processes even when hosted by hello same Service Fabric node.</span></span> <span data-ttu-id="dc8a1-120">Кроме того, можно управлять hello жизненного цикла для каждого экземпляра приложения (например, обновлены) независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-120">Furthermore, hello lifecycle of each application instance can be managed (for example, upgraded) independently.</span></span> <span data-ttu-id="dc8a1-121">Hello следующей схеме показано, как типы приложений состоят из типы служб, которые в свою очередь, состоят из кода, конфигурации и пакетов данных.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-121">hello following diagram shows how application types are composed of service types, which in turn are composed of code, configuration, and data packages.</span></span> <span data-ttu-id="dc8a1-122">Схема toosimplify hello, hello пакетов кода/config/данные для `ServiceType4` отображаются, хотя каждого типа службы, включит некоторых или всех типов пакетов.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-122">toosimplify hello diagram, only hello code/config/data packages for `ServiceType4` are shown, though each service type would include some or all those package types.</span></span>

![Типы служб и типы приложений Service Fabric][cluster-imagestore-apptypes]

<span data-ttu-id="dc8a1-124">Два разных файла манифеста, используется toodescribe приложений и служб: hello манифест службы и манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-124">Two different manifest files are used toodescribe applications and services: hello service manifest and application manifest.</span></span> <span data-ttu-id="dc8a1-125">Манифесты подробно описаны в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-125">Manifests are covered in detail in hello following sections.</span></span>

<span data-ttu-id="dc8a1-126">Может существовать один или несколько экземпляров типа службы активного в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-126">There can be one or more instances of a service type active in hello cluster.</span></span> <span data-ttu-id="dc8a1-127">Например экземпляры службы с отслеживанием состояния или реплики, достичь высокой надежности, копируя состояние между репликами, расположенными на разных узлах в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-127">For example, stateful service instances, or replicas, achieve high reliability by replicating state between replicas located on different nodes in hello cluster.</span></span> <span data-ttu-id="dc8a1-128">Репликация по существу обеспечивает избыточность для hello службы toobe доступны, даже в случае сбоя одного узла в кластере.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-128">Replication essentially provides redundancy for hello service toobe available even if one node in a cluster fails.</span></span> <span data-ttu-id="dc8a1-129">Объект [секционированы службы](service-fabric-concepts-partitioning.md) Далее делит его состояние (и состоянии toothat шаблонов доступа) для узлов кластера hello.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-129">A [partitioned service](service-fabric-concepts-partitioning.md) further divides its state (and access patterns toothat state) across nodes in hello cluster.</span></span>

<span data-ttu-id="dc8a1-130">Hello следующей схеме показаны hello связи между приложениями и экземплярами службы, разделы и реплики.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-130">hello following diagram shows hello relationship between applications and service instances, partitions, and replicas.</span></span>

![Разделы и реплики в службе][cluster-application-instances]

> [!TIP]
> <span data-ttu-id="dc8a1-132">Можно просмотреть макет hello приложений в кластере с помощью Service Fabric Explorer средство hello, доступное на http://&lt;yourclusteraddress&gt;: 19080/обозреватель.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-132">You can view hello layout of applications in a cluster using hello Service Fabric Explorer tool available at http://&lt;yourclusteraddress&gt;:19080/Explorer.</span></span> <span data-ttu-id="dc8a1-133">Дополнительные сведения см. в статье [Визуализация кластера с помощью обозревателя Service Fabric](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="dc8a1-133">For more information, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
> 
> 

## <a name="describe-a-service"></a><span data-ttu-id="dc8a1-134">Описание службы</span><span class="sxs-lookup"><span data-stu-id="dc8a1-134">Describe a service</span></span>
<span data-ttu-id="dc8a1-135">Hello манифест службы декларативно определяет тип службы hello и версии.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-135">hello service manifest declaratively defines hello service type and version.</span></span> <span data-ttu-id="dc8a1-136">Он задает метаданные службы, такие как тип службы, свойства работоспособности, метрики балансировки нагрузки, двоичные файлы службы и файлы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-136">It specifies service metadata such as service type, health properties, load-balancing metrics, service binaries, and configuration files.</span></span>  <span data-ttu-id="dc8a1-137">Другими словами, он описывает пакеты кода, конфигурации и данных hello, составляющих toosupport пакета службы один или несколько типов служб.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-137">Put another way, it describes hello code, configuration, and data packages that compose a service package toosupport one or more service types.</span></span> <span data-ttu-id="dc8a1-138">Ниже приведен простой пример манифеста служб.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-138">Here is a simple example service manifest:</span></span>

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

<span data-ttu-id="dc8a1-139">**Версия** атрибуты неструктурированных строки и не обработать системой hello.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-139">**Version** attributes are unstructured strings and not parsed by hello system.</span></span> <span data-ttu-id="dc8a1-140">Версия атрибуты являются tooversion используется для обновления каждого компонента.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-140">Version attributes are used tooversion each component for upgrades.</span></span>

<span data-ttu-id="dc8a1-141">В атрибуте **ServiceTypes** указывается, какие типы служб поддерживаются пакетами **CodePackages** в этом манифесте.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-141">**ServiceTypes** declares what service types are supported by **CodePackages** in this manifest.</span></span> <span data-ttu-id="dc8a1-142">При создании экземпляра службы в соответствии с одним из этих типов службы все пакеты кода, объявленные в этом манифесте, активируются путем запуска соответствующих точек входа.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-142">When a service is instantiated against one of these service types, all code packages declared in this manifest are activated by running their entry points.</span></span> <span data-ttu-id="dc8a1-143">Полученный процессы Hello являются типами службы ожидаемый tooregister hello поддерживается во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-143">hello resulting processes are expected tooregister hello supported service types at run time.</span></span> <span data-ttu-id="dc8a1-144">Служба типы объявляются на уровне манифеста hello и не уровня пакета кода hello.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-144">Service types are declared at hello manifest level and not hello code package level.</span></span> <span data-ttu-id="dc8a1-145">Поэтому при наличии нескольких пакетов кода, они все активируются всякий раз, когда hello система выполняет поиск любого из hello объявленных типов служб.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-145">So when there are multiple code packages, they are all activated whenever hello system looks for any one of hello declared service types.</span></span>

<span data-ttu-id="dc8a1-146">**SetupEntryPoint** — это точка входа привилегированные, который выполняется с таким же учетные данные как Service Fabric hello (обычно hello *LocalSystem* учетной записи) перед любой другой точки входа.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-146">**SetupEntryPoint** is a privileged entry point that runs with hello same credentials as Service Fabric (typically hello *LocalSystem* account) before any other entry point.</span></span> <span data-ttu-id="dc8a1-147">Hello исполняемый файл, указанный с **EntryPoint** обычно является узел службы hello длительное время.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-147">hello executable specified by **EntryPoint** is typically hello long-running service host.</span></span> <span data-ttu-id="dc8a1-148">наличие Hello точки входа отдельной установки позволяет избежать размещения службы hello toorun с высоким уровнем привилегий на длительное время.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-148">hello presence of a separate setup entry point avoids having toorun hello service host with high privileges for extended periods of time.</span></span> <span data-ttu-id="dc8a1-149">Hello исполняемый файл, указанный с **EntryPoint** запускается после **SetupEntryPoint** успешно завершает работу.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-149">hello executable specified by **EntryPoint** is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="dc8a1-150">Если когда-либо процесс hello завершает или аварийно завершает работу, результирующий процесс hello отслеживается и перезапуска (начиная с версии снова **SetupEntryPoint**).</span><span class="sxs-lookup"><span data-stu-id="dc8a1-150">If hello process ever terminates or crashes, hello resulting process is monitored and restarted (beginning again with **SetupEntryPoint**).</span></span>  

<span data-ttu-id="dc8a1-151">Типичные сценарии использования **SetupEntryPoint** являются при запуске исполняемого файла до запуска службы hello или выполнять операции с повышенными привилегиями.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-151">Typical scenarios for using **SetupEntryPoint** are when you run an executable before hello service starts or you perform an operation with elevated privileges.</span></span> <span data-ttu-id="dc8a1-152">Например:</span><span class="sxs-lookup"><span data-stu-id="dc8a1-152">For example:</span></span>

* <span data-ttu-id="dc8a1-153">Настройка и инициализация переменных среды, которые hello исполняемый требованиям службы.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-153">Setting up and initializing environment variables that hello service executable needs.</span></span> <span data-ttu-id="dc8a1-154">Это не исполняемые файлы ограниченный tooonly записано с помощью модели программирования hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-154">This is not limited tooonly executables written via hello Service Fabric programming models.</span></span> <span data-ttu-id="dc8a1-155">Например, npm.exe нужны определенные переменные среды, настроенные для развертывания приложения node.js.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-155">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="dc8a1-156">Настройка контроля доступа посредством установки сертификатов безопасности.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-156">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="dc8a1-157">Дополнительные сведения о том, как tooconfigure hello **SetupEntryPoint** разделе [настройки hello политики для точки входа установки службы](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="dc8a1-157">For more details on how tooconfigure hello **SetupEntryPoint** see [Configure hello policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<span data-ttu-id="dc8a1-158">**EnvironmentVariables** содержит список переменных среды, которые заданы для этого пакета кода.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-158">**EnvironmentVariables** provides a list of environment variables that are set for this code package.</span></span> <span data-ttu-id="dc8a1-159">Переменные Environmentment могут переопределяться в hello `ApplicationManifest.xml` tooprovide различные значения для различным экземплярам службы.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-159">Environmentment variables can be overridden in hello `ApplicationManifest.xml` tooprovide different values for different service instances.</span></span> 

<span data-ttu-id="dc8a1-160">**DataPackage** объявляет папку с именем hello **имя** атрибут, содержащий toobe произвольный статических данных используются процессом hello во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-160">**DataPackage** declares a folder, named by hello **Name** attribute, that contains arbitrary static data toobe consumed by hello process at run time.</span></span>

<span data-ttu-id="dc8a1-161">**ConfigPackage** объявляет папку с именем hello **имя** атрибут, который содержит *Settings.xml* файла.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-161">**ConfigPackage** declares a folder, named by hello **Name** attribute, that contains a *Settings.xml* file.</span></span> <span data-ttu-id="dc8a1-162">файл параметров Hello содержит разделы параметры определяемых пользователем, ключ значение пары процесса hello считываются обратно во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-162">hello settings file contains sections of user-defined, key-value pair settings that hello process reads back at run time.</span></span> <span data-ttu-id="dc8a1-163">Во время обновления, если только hello **ConfigPackage** **версии** был изменен, то запуск процесса hello не перезапускается.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-163">During an upgrade, if only hello **ConfigPackage** **version** has changed, then hello running process is not restarted.</span></span> <span data-ttu-id="dc8a1-164">Вместо этого обратного вызова уведомляет процесс hello, параметры конфигурации были изменены, поэтому их можно загрузить в память динамически.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-164">Instead, a callback notifies hello process that configuration settings have changed so they can be reloaded dynamically.</span></span> <span data-ttu-id="dc8a1-165">Ниже приведен пример файла *Settings.xml* .</span><span class="sxs-lookup"><span data-stu-id="dc8a1-165">Here is an example *Settings.xml* file:</span></span>

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> <span data-ttu-id="dc8a1-166">Манифест служб может содержать множество пакетов кода, конфигураций и данных.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-166">A service manifest can contain multiple code, configuration, and data packages.</span></span> <span data-ttu-id="dc8a1-167">Версия каждого из них устанавливается независимо.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-167">Each of those can be versioned independently.</span></span>
> 
> 

<!--
For more information about other features supported by service manifests, refer toohello following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a><span data-ttu-id="dc8a1-168">Описание приложения</span><span class="sxs-lookup"><span data-stu-id="dc8a1-168">Describe an application</span></span>
<span data-ttu-id="dc8a1-169">манифест приложения Hello декларативно описывает тип приложения hello и версии.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-169">hello application manifest declaratively describes hello application type and version.</span></span> <span data-ttu-id="dc8a1-170">Он также указывает метаданные композиции службы, такие как стабильные имена, схема секционирования, число экземпляров и коэффициент репликации, политика безопасности и изоляции, ограничения на размещение, переопределения конфигурации и типы входящих в состав служб.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-170">It specifies service composition metadata such as stable names, partitioning scheme, instance count/replication factor, security/isolation policy, placement constraints, configuration overrides, and constituent service types.</span></span> <span data-ttu-id="dc8a1-171">также описываются домены балансировки нагрузки Hello, в которых размещается приложение hello.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-171">hello load-balancing domains into which hello application is placed are also described.</span></span>

<span data-ttu-id="dc8a1-172">Таким образом манифест приложения описывает элементы на уровне приложения hello и ссылается на один или дополнительные службы манифесты toocompose типа приложения.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-172">Thus, an application manifest describes elements at hello application level and references one or more service manifests toocompose an application type.</span></span> <span data-ttu-id="dc8a1-173">Ниже приведен простой пример манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-173">Here is a simple example application manifest:</span></span>

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

<span data-ttu-id="dc8a1-174">Манифесты службы, например **версии** атрибуты неструктурированных строки и не анализируются системой hello.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-174">Like service manifests, **Version** attributes are unstructured strings and are not parsed by hello system.</span></span> <span data-ttu-id="dc8a1-175">Версия атрибуты являются также используется tooversion каждый компонент для выполнения обновлений.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-175">Version attributes are also used tooversion each component for upgrades.</span></span>

<span data-ttu-id="dc8a1-176">**ServiceManifestImport** содержит ссылки на tooservice манифесты составляющих этот тип приложения.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-176">**ServiceManifestImport** contains references tooservice manifests that compose this application type.</span></span> <span data-ttu-id="dc8a1-177">Импортированные манифесты служб определяют, какие типы служб допустимы для применения в приложении этого типа.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-177">Imported service manifests determine what service types are valid within this application type.</span></span> <span data-ttu-id="dc8a1-178">В рамках hello ServiceManifestImport переопределить значения конфигурации в Settings.xml и переменных среды в файлах ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-178">Within hello ServiceManifestImport, you override configuration values in Settings.xml and environment variables in ServiceManifest.xml files.</span></span> 


<span data-ttu-id="dc8a1-179">**DefaultServices** декларируются экземпляры служб, которые создаются автоматически при создании экземпляра приложения в соответствии с его типом.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-179">**DefaultServices** declares service instances that are automatically created whenever an application is instantiated against this application type.</span></span> <span data-ttu-id="dc8a1-180">Службы по умолчанию используются только для удобства и после создания во всех отношениях действуют как и обычные службы.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-180">Default services are just a convenience and behave like normal services in every respect after they have been created.</span></span> <span data-ttu-id="dc8a1-181">Они обновляются вместе с другими службами в экземпляре приложения hello и может быть также удален.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-181">They are upgraded along with any other services in hello application instance and can be removed as well.</span></span>

> [!NOTE]
> <span data-ttu-id="dc8a1-182">Манифест приложения может содержать несколько импортированных манифестов служб и служб по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-182">An application manifest can contain multiple service manifest imports and default services.</span></span> <span data-ttu-id="dc8a1-183">Каждый импортированный манифест служб может иметь свою версию.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-183">Each service manifest import can be versioned independently.</span></span>
> 
> 

<span data-ttu-id="dc8a1-184">toomaintain различные приложения и параметры обслуживания для соответствующей среды. в статье toolearn [Управление параметрами приложения для нескольких сред](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="dc8a1-184">toolearn how toomaintain different application and service parameters for individual environments, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

<!--
For more information about other features supported by application manifests, refer toohello following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a><span data-ttu-id="dc8a1-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dc8a1-185">Next steps</span></span>
<span data-ttu-id="dc8a1-186">[Упаковка приложения](service-fabric-package-apps.md) и сделать его готовности toodeploy.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-186">[Package an application](service-fabric-package-apps.md) and make it ready toodeploy.</span></span>

<span data-ttu-id="dc8a1-187">[Развертывание и удаление приложений] [ 10] описывает как экземпляры приложения toomanage toouse PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-187">[Deploy and remove applications][10] describes how toouse PowerShell toomanage application instances.</span></span>

<span data-ttu-id="dc8a1-188">[Управление параметрами приложения для нескольких сред] [ 11] описывает способ tooconfigure параметров и переменных среды для экземпляров другого приложения.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-188">[Managing application parameters for multiple environments][11] describes how tooconfigure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="dc8a1-189">[Настройка политик безопасности для приложения] [ 12] описывает, каким образом службы toorun toorestrict политики безопасности доступа.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-189">[Configure security policies for your application][12] describes how toorun services under security policies toorestrict access.</span></span>

<span data-ttu-id="dc8a1-190">В статье [Модель размещения Service Fabric][13] рассматривается связь между репликами (или экземплярами) развернутой службы и процессом размещения службы.</span><span class="sxs-lookup"><span data-stu-id="dc8a1-190">[Application hosting models][13] describe relationship between replicas (or instances) of a deployed service and service-host process.</span></span>

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
