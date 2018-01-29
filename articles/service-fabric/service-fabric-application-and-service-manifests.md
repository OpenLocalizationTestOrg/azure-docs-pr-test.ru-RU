---
title: "Описания Azure Service Fabric приложения и службы | Документы Microsoft"
description: "Описывает, как манифесты, используются для описания структуры службы приложений и служб."
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
ms.date: 12/07/2017
ms.author: ryanwi
ms.openlocfilehash: 8e0cf78aef7e973188ce9581ec94f012f6ecde90
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="service-fabric-application-and-service-manifests"></a>Манифестов службы и приложения Service Fabric
В этой статье описывается как Service Fabric приложения и службы будут определены и с версиями, с помощью файлов ApplicationManifest.xml и ServiceManifest.xml.  Схема XML для этих файлов манифеста документирован в [ServiceFabricServiceModel.xsd документации по схеме](service-fabric-service-model-schema.md).

## <a name="describe-a-service-in-servicemanifestxml"></a>Описания службы в файле ServiceManifest.xml
Манифест службы декларативно определяет тип и версию службы. Он задает метаданные службы, такие как тип службы, свойства работоспособности, метрики балансировки нагрузки, двоичные файлы службы и файлы конфигурации.  Другими словами, в нем описывается код, конфигурация и пакеты данных, из которых состоит пакет службы, для поддержки одного или нескольких типов служб. Манифест службы может содержать несколько кода, конфигурации и пакетов данных, которые можно использовать с версиями независимо друг от друга. Вот манифест службы для веб-интерфейса службы ASP.NET Core из [голосования образец приложения](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart):

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="VotingWebPkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType. 
         This name must match the string used in RegisterServiceType call in Program.cs. -->
    <StatelessServiceType ServiceTypeName="VotingWebType" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <ExeHost>
        <Program>VotingWeb.exe</Program>
        <WorkingFolder>CodePackage</WorkingFolder>
      </ExeHost>
    </EntryPoint>
  </CodePackage>

  <!-- Config package is the contents of the Config directoy under PackageRoot that contains an 
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="8080" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

**Версия** представляют собой неструктурированные строки, которые не обрабатываются системой. Атрибуты версии используются в целях указания версии каждого компонента для последующего обновления.

В атрибуте **ServiceTypes** указывается, какие типы служб поддерживаются пакетами **CodePackages** в этом манифесте. При создании экземпляра службы в соответствии с одним из этих типов службы все пакеты кода, объявленные в этом манифесте, активируются путем запуска соответствующих точек входа. Запущенные вследствие этого процессы должны зарегистрировать поддерживаемые типы служб во время выполнения. Типы служб декларируются на уровне манифеста, а не на уровне пакета кода. Поэтому при наличии нескольких пакетов кода они все активируются при поиске системой любого из задекларированных типов служб.

Исполняемый файл, указанный в точке входа **EntryPoint** , обычно является узлом службы, запускаемым на длительный срок. **SetupEntryPoint** — это привилегированная точка входа, которая запускается с теми же учетными данными, что и структура службы (обычно это локальная учетная запись *LocalSystem* ), перед тем, как будут запущены любые другие точки входа.  Наличие отдельной точки входа настройки позволяет избежать необходимости в выполнении узла службы с расширенными правами в течение длительного срока. Исполняемый файл, указанный в точке входа **EntryPoint**, запускается после успешного выхода из точки **SetupEntryPoint**. Даже если произошло непредвиденное завершение работы процесса или его сбой, возникающий вследствие этого, процесс отслеживается и перезапускается (снова начиная с точки входа **SetupEntryPoint**).  

Типичные сценарии использования **SetupEntryPoint** относятся к ситуации, когда вы запускаете исполняемый файл перед запуском службы или выполняете операцию с повышенными привилегиями. Например: 

* Настройка и инициализация переменных среды, необходимых исполняемому файлу службы. Это касается не только исполняемых файлов, написанных с использованием моделей программирования Service Fabric. Например, npm.exe нужны определенные переменные среды, настроенные для развертывания приложения node.js.
* Настройка контроля доступа посредством установки сертификатов безопасности.

Дополнительные сведения о настройке **SetupEntryPoint** см. в статье [Настройка политик безопасности для приложения](service-fabric-application-runas-security.md).

**EnvironmentVariables** (а не значение в предыдущем примере) содержит список переменных среды, заданные для этого пакета кода. Переменные среды могут переопределяться в `ApplicationManifest.xml` позволяет предоставлять разные значения для различным экземплярам службы. 

**DataPackage** папки, названный объявляет (а не значение в предыдущем примере) **имя** атрибут, содержащий произвольный статические данные для использования во время выполнения процесса.

**ConfigPackage** объявляет папку с именем, указанным в атрибуте **Name**, которая содержит файл *Settings.xml*. Файл параметров содержит разделы заданных пользователем параметров пар "ключ — значение", которые считываются процессом во время выполнения. Во время обновления при изменении одного только атрибута **version** для **ConfigPackage** перезапуск процесса не выполняется. Вместо этого при помощи обратного вызова в процесс передается уведомление о том, что параметры конфигурации изменились, поэтому они были перезагружены в динамическом режиме. Ниже приведен пример файла *Settings.xml* .

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

**Ресурсы**, такие как конечные точки, которые используются службой для быть объявлен или изменен без изменения скомпилированный код.  Доступ к ресурсам, которые указаны в манифесте службы можно управлять через **SecurityGroup** в манифесте приложения.  Когда **конечная точка** ресурс определен в манифесте службы, Service Fabric назначает порты из диапазона портов зарезервированные приложения, если порт не указан явно.  Дополнительные сведения о [Указание или переопределение ресурсы конечной точки](service-fabric-service-manifest-resources.md).


<!--
For more information about other features supported by service manifests, refer to the following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application-in-applicationmanifestxml"></a>Описания приложения в файле ApplicationManifest.xml
Манифест приложения декларативно описывает тип приложения и его версию. Он также указывает метаданные композиции службы, такие как стабильные имена, схема секционирования, число экземпляров и коэффициент репликации, политика безопасности и изоляции, ограничения на размещение, переопределения конфигурации и типы входящих в состав служб. Также в нем описываются домены балансировки нагрузки, в которых размещается приложение.

Таким образом, манифест приложения описывает элементы на уровне приложения и ссылается на один или несколько манифестов службы, которые составляют тип приложения. Вот манифест приложения для [голосования образец приложения](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart):

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="VotingType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Parameters>
    <Parameter Name="VotingData_MinReplicaSetSize" DefaultValue="3" />
    <Parameter Name="VotingData_PartitionCount" DefaultValue="1" />
    <Parameter Name="VotingData_TargetReplicaSetSize" DefaultValue="3" />
    <Parameter Name="VotingWeb_InstanceCount" DefaultValue="-1" />
  </Parameters>
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion 
       should match the Name and Version attributes of the ServiceManifest element defined in the 
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="VotingDataPkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
  </ServiceManifestImport>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="VotingWebPkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
  </ServiceManifestImport>
  <DefaultServices>
    <!-- The section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using the 
         ServiceFabric PowerShell module.
         
         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
    <Service Name="VotingData">
      <StatefulService ServiceTypeName="VotingDataType" TargetReplicaSetSize="[VotingData_TargetReplicaSetSize]" MinReplicaSetSize="[VotingData_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[VotingData_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    <Service Name="VotingWeb" ServicePackageActivationMode="ExclusiveProcess">
      <StatelessService ServiceTypeName="VotingWebType" InstanceCount="[VotingWeb_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

Точно так же, как и в манифестах служб, атрибуты версии **Version** представляют собой неструктурированные строки, которые не анализируются системой. Атрибуты версии также используются в целях указания версии каждого компонента для последующего обновления.

**Параметры** определяет параметры, используемые в манифесте приложения. Можно указать значения этих параметров, при приложения instatiated можно переопределить, приложения или параметры конфигурации для службы.  Значение параметра по умолчанию используется в том случае, если значение не изменяется во время создания экземпляра приложения. Сведения об использовании разных параметров приложений и служб для отдельных сред см. в статье [Управление параметрами приложения для нескольких сред](service-fabric-manage-multiple-environment-app-configuration.md).

**ServiceManifestImport** содержит ссылки на манифесты служб, из которых состоит этот тип приложения. Манифест приложения может содержать несколько импорта манифеста службы, каждый из них могут поддерживать управление версиями независимо друг от друга. Импортированные манифесты служб определяют, какие типы служб допустимы для применения в приложении этого типа. В ServiceManifestImport можно переопределить значения конфигурации в файле Settings.xml и переменные среды в файле ServiceManifest.xml. **Политики** (не задано в предыдущем примере) для привязки конечной точки, безопасности и доступа и пакета управления доступом можно задать в манифестах импортированных службы.  Дополнительные сведения см. в разделе [Настройка политик безопасности для приложения](service-fabric-application-runas-security.md).

**DefaultServices** декларируются экземпляры служб, которые создаются автоматически при создании экземпляра приложения в соответствии с его типом. Службы по умолчанию используются только для удобства и после создания во всех отношениях действуют как и обычные службы. Они обновляются вместе с любыми другими службами в экземпляре приложения, а также могут быть удалены. Манифест приложения может содержать несколько служб по умолчанию.

**Сертификаты** (а не значение в предыдущем примере) объявляет сертификаты, используемые для [настроить конечные точки HTTPS](service-fabric-service-manifest-resources.md#example-specifying-an-https-endpoint-for-your-service) или [шифрования секретов в манифесте приложения](service-fabric-application-secret-management.md).

**Политики** (а не значение в предыдущем примере) описывает сбор журналов, [выполнения по умолчанию](service-fabric-application-runas-security.md), [работоспособности](service-fabric-health-introduction.md#health-policies), и [безопасности access](service-fabric-application-runas-security.md) политики, задаваемые в уровень приложения.

**Субъекты** (не задано в предыдущем примере) описывают субъектов безопасности (пользователей или группы), необходимые для [выполнения службы и ресурсы служба безопасного](service-fabric-application-runas-security.md).  Субъекты упоминаются в **политики** разделы.





<!--
For more information about other features supported by application manifests, refer to the following articles:

*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a>Дальнейшие действия
- [Создайте пакет приложения](service-fabric-package-apps.md) и подготовьте его к развертыванию.
- [Развертывание и удаление приложений](service-fabric-deploy-remove-applications.md).
- [Настройка параметров и переменных среды для другого приложения экземпляров](service-fabric-manage-multiple-environment-app-configuration.md).
- [Настройка политик безопасности для приложения](service-fabric-application-runas-security.md).
- [Настройка конечных точек HTTPS](service-fabric-service-manifest-resources.md#example-specifying-an-https-endpoint-for-your-service).
- [Шифрования секретов в манифест приложения](service-fabric-application-secret-management.md)

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png



