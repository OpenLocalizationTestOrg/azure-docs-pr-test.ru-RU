---
title: "aaaManage нескольких средах в Service Fabric | Документы Microsoft"
description: "Service Fabric приложений может выполняться в кластерах, диапазон которых варьируется от одной машины toothousands машин. В некоторых случаях необходимо tooconfigure приложения по-разному для этих различных средах. В этой статье рассматриваются как toodefine параметров другого приложения для среды."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: mikkelhegn
ms.openlocfilehash: 2b3327e0e1a3bbd35a50835e720619f308b1b501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a><span data-ttu-id="f3ccd-105">Управление параметрами приложения для нескольких сред</span><span class="sxs-lookup"><span data-stu-id="f3ccd-105">Manage application parameters for multiple environments</span></span>
<span data-ttu-id="f3ccd-106">Можно создавать кластеры Azure Service Fabric с помощью любой из одного toomany тысяч машин.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-106">You can create Azure Service Fabric clusters by using anywhere from one toomany thousands of machines.</span></span> <span data-ttu-id="f3ccd-107">Хотя двоичные файлы приложения могут выполняться без изменения через этот широкий спектр сред, часто требуется приложение hello tooconfigure по-разному, в зависимости от числа hello машины, которые необходимо развернуть.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-107">While application binaries can run without modification across this wide spectrum of environments, you often want tooconfigure hello application differently, depending on hello number of machines you're deploying to.</span></span>

<span data-ttu-id="f3ccd-108">В качестве простого примера рассмотрим параметр `InstanceCount` для службы без отслеживания состояния.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-108">As a simple example, consider `InstanceCount` for a stateless service.</span></span> <span data-ttu-id="f3ccd-109">При запуске приложения в Azure, обычно можно tooset этот параметр toohello специальное значение «-1».</span><span class="sxs-lookup"><span data-stu-id="f3ccd-109">When you are running applications in Azure, you generally want tooset this parameter toohello special value of "-1".</span></span> <span data-ttu-id="f3ccd-110">Эта конфигурация гарантирует, что служба запущена на каждом узле кластера hello (или в тип узла hello при установке ограничения на размещение каждого узла).</span><span class="sxs-lookup"><span data-stu-id="f3ccd-110">This configuration ensures that your service is running on every node in hello cluster (or every node in hello node type if you have set a placement constraint).</span></span> <span data-ttu-id="f3ccd-111">Однако эта конфигурация не подходит для кластера с одним компьютером, так как не может иметь несколько процессов, прослушивание hello же конечную точку на одном компьютере.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-111">However, this configuration is not suitable for a single-machine cluster since you cannot have multiple processes listening on hello same endpoint on a single machine.</span></span> <span data-ttu-id="f3ccd-112">Вместо этого обычно устанавливается `InstanceCount` слишком «1».</span><span class="sxs-lookup"><span data-stu-id="f3ccd-112">Instead, you typically set `InstanceCount` too"1".</span></span>

## <a name="specifying-environment-specific-parameters"></a><span data-ttu-id="f3ccd-113">Выбор параметров среды</span><span class="sxs-lookup"><span data-stu-id="f3ccd-113">Specifying environment-specific parameters</span></span>
<span data-ttu-id="f3ccd-114">проблемы конфигурации toothis Hello решений — это набор служб по умолчанию с параметрами и файлы параметров приложения, заполните значения этих параметров для данной среды.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-114">hello solution toothis configuration issue is a set of parameterized default services and application parameter files that fill in those parameter values for a given environment.</span></span> <span data-ttu-id="f3ccd-115">По умолчанию службы и параметры приложения настроены в приложения hello и манифесты службы.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-115">Default services and application parameters are configured in hello application and service manifests.</span></span> <span data-ttu-id="f3ccd-116">Hello определение схемы для файлов ServiceManifest.xml и ApplicationManifest.xml hello устанавливается вместе с hello Service Fabric SDK и средств слишком*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-116">hello schema definition for hello ServiceManifest.xml and ApplicationManifest.xml files is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

### <a name="default-services"></a><span data-ttu-id="f3ccd-117">Службы по умолчанию</span><span class="sxs-lookup"><span data-stu-id="f3ccd-117">Default services</span></span>
<span data-ttu-id="f3ccd-118">Приложения Service Fabric состоят из коллекции экземпляров службы.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-118">Service Fabric applications are made up of a collection of service instances.</span></span> <span data-ttu-id="f3ccd-119">Возможно, что toocreate пустого приложения и динамическое создание всех экземпляров службы, большинство приложений имеют набор основных служб, которые всегда должны быть созданы при создании экземпляра приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-119">While it is possible for you toocreate an empty application and then create all service instances dynamically, most applications have a set of core services that should always be created when hello application is instantiated.</span></span> <span data-ttu-id="f3ccd-120">Это ссылка tooas «службы по умолчанию».</span><span class="sxs-lookup"><span data-stu-id="f3ccd-120">These are referred tooas "default services".</span></span> <span data-ttu-id="f3ccd-121">Они указаны в манифесте приложения hello, с заполнителями для конфигурации-среду, включенных в квадратных скобках:</span><span class="sxs-lookup"><span data-stu-id="f3ccd-121">They are specified in hello application manifest, with placeholders for per-environment configuration included in square brackets:</span></span>

```xml
  <DefaultServices>
      <Service Name="Stateful1">
          <StatefulService
              ServiceTypeName="Stateful1Type"
              TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
              MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

              <UniformInt64Partition
                  PartitionCount="[Stateful1_PartitionCount]"
                  LowKey="-9223372036854775808"
                  HighKey="9223372036854775807"
              />
        </StatefulService>
    </Service>
  </DefaultServices>
```

<span data-ttu-id="f3ccd-122">Каждый из hello именованные параметры должны быть определены в элемент Parameters hello манифеста приложения hello:</span><span class="sxs-lookup"><span data-stu-id="f3ccd-122">Each of hello named parameters must be defined within hello Parameters element of hello application manifest:</span></span>

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

<span data-ttu-id="f3ccd-123">Атрибут DefaultValue Hello указывает toobe значение hello, используемого в hello отсутствия более конкретные параметра для данной среды.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-123">hello DefaultValue attribute specifies hello value toobe used in hello absence of a more-specific parameter for a given environment.</span></span>

> [!NOTE]
> <span data-ttu-id="f3ccd-124">Не все параметры экземпляра службы подходят для конфигурации среды.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-124">Not all service instance parameters are suitable for per-environment configuration.</span></span> <span data-ttu-id="f3ccd-125">В приведенном выше примере hello hello LowKey и HighKey для схемы секционирования hello службы задаются значения для всех экземпляров службы hello с момента hello секции диапазона является функцией домена данных hello не hello среды.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-125">In hello example above, hello LowKey and HighKey values for hello service's partitioning scheme are explicitly defined for all instances of hello service since hello partition range is a function of hello data domain, not hello environment.</span></span>
> 
> 

### <a name="per-environment-service-configuration-settings"></a><span data-ttu-id="f3ccd-126">Параметры конфигурации службы в среде</span><span class="sxs-lookup"><span data-stu-id="f3ccd-126">Per-environment service configuration settings</span></span>
<span data-ttu-id="f3ccd-127">Hello [модель приложения Service Fabric](service-fabric-application-model.md) включает службы tooinclude конфигурации пакетов, содержащих пользовательские пары ключей и значений, которые доступны для чтения во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-127">hello [Service Fabric application model](service-fabric-application-model.md) enables services tooinclude configuration packages that contain custom key-value pairs that are readable at run time.</span></span> <span data-ttu-id="f3ccd-128">Hello значения этих параметров может также отличаться друг от друга среды, указав `ConfigOverride` в манифесте приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-128">hello values of these settings can also be differentiated by environment by specifying a `ConfigOverride` in hello application manifest.</span></span>

<span data-ttu-id="f3ccd-129">Предположим, что следующий параметр в файле Config\Settings.xml hello для hello hello `Stateful1` службы:</span><span class="sxs-lookup"><span data-stu-id="f3ccd-129">Suppose that you have hello following setting in hello Config\Settings.xml file for hello `Stateful1` service:</span></span>

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
<span data-ttu-id="f3ccd-130">создать toooverride это значение для пары среды и конкретных приложений `ConfigOverride` при импорте манифест службы hello в манифесте приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-130">toooverride this value for a specific application/environment pair, create a `ConfigOverride` when you import hello service manifest in hello application manifest.</span></span>

```xml
  <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
<span data-ttu-id="f3ccd-131">Как показано выше, позднее среда может настроить этот параметр.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-131">This parameter can then be configured by environment as shown above.</span></span> <span data-ttu-id="f3ccd-132">Это можно сделать путем его объявления hello параметры из раздела манифеста приложения hello и указания значений, относящихся к среде в файлах параметров приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-132">You can do this by declaring it in hello parameters section of hello application manifest and specifying environment-specific values in hello application parameter files.</span></span>

> [!NOTE]
> <span data-ttu-id="f3ccd-133">В случае hello параметров конфигурации службы существуют три места, где можно задать значение hello ключа: пакет конфигурации службы hello, манифест приложения hello и файле параметров приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-133">In hello case of service configuration settings, there are three places where hello value of a key can be set: hello service configuration package, hello application manifest, and hello application parameter file.</span></span> <span data-ttu-id="f3ccd-134">Service Fabric будет всегда из файла параметров приложения hello сначала выберите (Если указано), затем hello манифест приложения и наконец hello конфигурации пакета.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-134">Service Fabric will always choose from hello application parameter file first (if specified), then hello application manifest, and finally hello configuration package.</span></span>
> 
> 

### <a name="setting-and-using-environment-variables"></a><span data-ttu-id="f3ccd-135">Настройка и использование переменных среды</span><span class="sxs-lookup"><span data-stu-id="f3ccd-135">Setting and using environment variables</span></span> 
<span data-ttu-id="f3ccd-136">Можно указать и задание переменных среды в файле ServiceManifest.xml hello, а затем переопределить их в файл ApplicationManifest.xml hello отдельно для каждого экземпляра.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-136">You can specify and set environment variables in hello ServiceManifest.xml file and then override these in hello ApplicationManifest.xml file on a per instance basis.</span></span>
<span data-ttu-id="f3ccd-137">Hello приведенном ниже примере показаны две переменные среды, задать один со значением и переопределении hello других.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-137">hello example below shows two environment variables, one with a value set and hello other is overridden.</span></span> <span data-ttu-id="f3ccd-138">Можно использовать значения переменных среды tooset в hello таким же способом, они были использованы для переопределения конфигурации параметров приложения.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-138">You can use application parameters tooset environment variables values in hello same way that these were used for config overrides.</span></span>

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
<span data-ttu-id="f3ccd-139">переменные среды toooverride hello в hello ApplicationManifest.xml пакет кода hello ссылку в hello ServiceManifest с hello `EnvironmentOverrides` элемента.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-139">toooverride hello environment variables in hello ApplicationManifest.xml, reference hello code package in hello ServiceManifest with hello `EnvironmentOverrides` element.</span></span>

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 <span data-ttu-id="f3ccd-140">После создания экземпляра службы с именем hello можно обращаться к переменным среды hello из кода.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-140">Once hello named service instance is created you can access hello environment variables from code.</span></span> <span data-ttu-id="f3ccd-141">Например в C# можно сделать следующее hello</span><span class="sxs-lookup"><span data-stu-id="f3ccd-141">e.g. In C# you can do hello following</span></span>

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a><span data-ttu-id="f3ccd-142">Переменные среды Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f3ccd-142">Service Fabric environment variables</span></span>
<span data-ttu-id="f3ccd-143">В Service Fabric есть встроенные переменные среды, задаваемые для каждого экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-143">Service Fabric has built in environment variables set for each service instance.</span></span> <span data-ttu-id="f3ccd-144">Hello полный список переменных среды ниже, где hello в полужирным являются hello те, которые будут использоваться в службе, hello других, используемые средой выполнения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-144">hello full list of environment variables is below, where hello ones in bold are hello ones that you will use in your service, hello other being used by Service Fabric runtime.</span></span> 

* <span data-ttu-id="f3ccd-145">Fabric_ApplicationHostId</span><span class="sxs-lookup"><span data-stu-id="f3ccd-145">Fabric_ApplicationHostId</span></span>
* <span data-ttu-id="f3ccd-146">Fabric_ApplicationHostType</span><span class="sxs-lookup"><span data-stu-id="f3ccd-146">Fabric_ApplicationHostType</span></span>
* <span data-ttu-id="f3ccd-147">Fabric_ApplicationId</span><span class="sxs-lookup"><span data-stu-id="f3ccd-147">Fabric_ApplicationId</span></span>
* <span data-ttu-id="f3ccd-148">**Fabric_ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="f3ccd-148">**Fabric_ApplicationName**</span></span>
* <span data-ttu-id="f3ccd-149">Fabric_CodePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="f3ccd-149">Fabric_CodePackageInstanceId</span></span>
* <span data-ttu-id="f3ccd-150">**Fabric_CodePackageName**</span><span class="sxs-lookup"><span data-stu-id="f3ccd-150">**Fabric_CodePackageName**</span></span>
* <span data-ttu-id="f3ccd-151">**Fabric_Endpoint_[имя_вашей_службы]TypeEndpoint**</span><span class="sxs-lookup"><span data-stu-id="f3ccd-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span></span>
* <span data-ttu-id="f3ccd-152">**Fabric_Folder_App_Log**</span><span class="sxs-lookup"><span data-stu-id="f3ccd-152">**Fabric_Folder_App_Log**</span></span>
* <span data-ttu-id="f3ccd-153">**Fabric_Folder_App_Temp**</span><span class="sxs-lookup"><span data-stu-id="f3ccd-153">**Fabric_Folder_App_Temp**</span></span>
* <span data-ttu-id="f3ccd-154">**Fabric_Folder_App_Work**</span><span class="sxs-lookup"><span data-stu-id="f3ccd-154">**Fabric_Folder_App_Work**</span></span>
* <span data-ttu-id="f3ccd-155">**Fabric_Folder_Application**</span><span class="sxs-lookup"><span data-stu-id="f3ccd-155">**Fabric_Folder_Application**</span></span>
* <span data-ttu-id="f3ccd-156">Fabric_NodeId</span><span class="sxs-lookup"><span data-stu-id="f3ccd-156">Fabric_NodeId</span></span>
* <span data-ttu-id="f3ccd-157">**Fabric_NodeIPOrFQDN**</span><span class="sxs-lookup"><span data-stu-id="f3ccd-157">**Fabric_NodeIPOrFQDN**</span></span>
* <span data-ttu-id="f3ccd-158">**Fabric_NodeName**</span><span class="sxs-lookup"><span data-stu-id="f3ccd-158">**Fabric_NodeName**</span></span>
* <span data-ttu-id="f3ccd-159">Fabric_RuntimeConnectionAddress</span><span class="sxs-lookup"><span data-stu-id="f3ccd-159">Fabric_RuntimeConnectionAddress</span></span>
* <span data-ttu-id="f3ccd-160">Fabric_ServicePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="f3ccd-160">Fabric_ServicePackageInstanceId</span></span>
* <span data-ttu-id="f3ccd-161">Fabric_ServicePackageName</span><span class="sxs-lookup"><span data-stu-id="f3ccd-161">Fabric_ServicePackageName</span></span>
* <span data-ttu-id="f3ccd-162">Fabric_ServicePackageVersionInstance</span><span class="sxs-lookup"><span data-stu-id="f3ccd-162">Fabric_ServicePackageVersionInstance</span></span>
* <span data-ttu-id="f3ccd-163">FabricPackageFileName</span><span class="sxs-lookup"><span data-stu-id="f3ccd-163">FabricPackageFileName</span></span>

<span data-ttu-id="f3ccd-164">Hello belows кода показано, как toolist hello переменные среды Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f3ccd-164">hello code belows shows how toolist hello Service Fabric environment variables</span></span>
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
<span data-ttu-id="f3ccd-165">Hello ниже приведены примеры переменных среды для типа приложения вызывается `GuestExe.Application` с типом службы вызывается `FrontEndService` при запуске на компьютере локальной разработки.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-165">hello following are examples of environment variables for an application type called `GuestExe.Application` with a service type called `FrontEndService` when run on your local dev machine.</span></span>

* <span data-ttu-id="f3ccd-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span><span class="sxs-lookup"><span data-stu-id="f3ccd-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span></span>
* <span data-ttu-id="f3ccd-167">**Fabric_CodePackageName = Code**</span><span class="sxs-lookup"><span data-stu-id="f3ccd-167">**Fabric_CodePackageName = Code**</span></span>
* <span data-ttu-id="f3ccd-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span><span class="sxs-lookup"><span data-stu-id="f3ccd-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span></span>
* <span data-ttu-id="f3ccd-169">**Fabric_NodeIPOrFQDN = localhost**</span><span class="sxs-lookup"><span data-stu-id="f3ccd-169">**Fabric_NodeIPOrFQDN = localhost**</span></span>
* <span data-ttu-id="f3ccd-170">**Fabric_NodeName = _Node_2**</span><span class="sxs-lookup"><span data-stu-id="f3ccd-170">**Fabric_NodeName = _Node_2**</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="f3ccd-171">Файлы параметров приложений</span><span class="sxs-lookup"><span data-stu-id="f3ccd-171">Application parameter files</span></span>
<span data-ttu-id="f3ccd-172">проект приложения Hello Service Fabric может включать один или несколько файлов параметров приложения.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-172">hello Service Fabric application project can include one or more application parameter files.</span></span> <span data-ttu-id="f3ccd-173">Каждый из них определяет hello конкретные значения для параметров hello, которые определены в манифесте приложения hello:</span><span class="sxs-lookup"><span data-stu-id="f3ccd-173">Each of them defines hello specific values for hello parameters that are defined in hello application manifest:</span></span>

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="3" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
<span data-ttu-id="f3ccd-174">По умолчанию новое приложение включает три файла параметров приложения: Local.1Node.xml, Local.5Node.xml и Cloud.xml.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-174">By default, a new application includes three application parameter files, named Local.1Node.xml, Local.5Node.xml, and Cloud.xml:</span></span>

![Файлы параметров приложения в обозревателе решений][app-parameters-solution-explorer]

<span data-ttu-id="f3ccd-176">файл параметров toocreate просто скопируйте существующий и присвойте ему новое имя.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-176">toocreate a parameter file, simply copy and paste an existing one and give it a new name.</span></span>

## <a name="identifying-environment-specific-parameters-during-deployment"></a><span data-ttu-id="f3ccd-177">Определение параметров среды во время развертывания</span><span class="sxs-lookup"><span data-stu-id="f3ccd-177">Identifying environment-specific parameters during deployment</span></span>
<span data-ttu-id="f3ccd-178">Во время развертывания необходимо toochoose hello соответствующий параметр файла tooapply с приложением.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-178">At deployment time, you need toochoose hello appropriate parameter file tooapply with your application.</span></span> <span data-ttu-id="f3ccd-179">Это можно сделать через диалоговое окно публикации hello в Visual Studio или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-179">You can do this through hello Publish dialog in Visual Studio or through PowerShell.</span></span>

### <a name="deploy-from-visual-studio"></a><span data-ttu-id="f3ccd-180">Развертывание из Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f3ccd-180">Deploy from Visual Studio</span></span>
<span data-ttu-id="f3ccd-181">При публикации приложения в Visual Studio можно выбрать из списка hello файлов доступный параметр.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-181">You can choose from hello list of available parameter files when you publish your application in Visual Studio.</span></span>

![Выберите файл параметров в диалоговом окне публикации hello][publishdialog]

### <a name="deploy-from-powershell"></a><span data-ttu-id="f3ccd-183">Развертывание из PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3ccd-183">Deploy from PowerShell</span></span>
<span data-ttu-id="f3ccd-184">Hello `Deploy-FabricApplication.ps1` сценарий PowerShell, включенных в шаблон проекта приложения hello принимает профиля публикации как параметр и hello PublishProfile содержит файл параметров приложения toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="f3ccd-184">hello `Deploy-FabricApplication.ps1` PowerShell script included in hello application project template accepts a publish profile as a parameter and hello PublishProfile contains a reference toohello application parameters file.</span></span>

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a><span data-ttu-id="f3ccd-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f3ccd-185">Next steps</span></span>
<span data-ttu-id="f3ccd-186">toolearn Дополнительные сведения о некоторых hello основные понятия, описанные в этом разделе в статье hello [Технический обзор Service Fabric](service-fabric-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f3ccd-186">toolearn more about some of hello core concepts that are discussed in this topic, see hello [Service Fabric technical overview](service-fabric-technical-overview.md).</span></span> <span data-ttu-id="f3ccd-187">Сведения о других возможностях управления приложениями, доступными в Visual Studio, см. в статье [Использование Visual Studio для упрощения создания приложений Service Fabric и управления ими](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="f3ccd-187">For information about other app management capabilities that are available in Visual Studio, see [Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
