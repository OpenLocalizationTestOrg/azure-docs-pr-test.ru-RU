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
# <a name="model-an-application-in-service-fabric"></a>Моделирование приложения в структуре службы
Это статье представлен обзор модели приложения hello Azure Service Fabric и как toodefine приложения и службы через файлов манифеста.

## <a name="understand-hello-application-model"></a>Понять модель приложения hello
Приложение представляет собой коллекцию составляющих его служб, которые выполняют определенные функции. Служба выполняет завершенную и отдельную функцию и может запускаться и работать независимо от других служб.  Она состоит из кода, конфигурации и данных. Для каждой службы код состоит из исполняемого hello двоичные файлы, Настройка включает в себя параметры службы, которые могут быть загружены во время выполнения и данные состоят из toobe произвольный статические данные, используются службой hello. Каждый компонент в этой иерархической модели приложения может иметь свою версию и обновляться независимо.

![модель приложения Hello Service Fabric][appmodel-diagram]

Тип приложения представляет собой отнесение приложения к определенной категории и состоит из пакета типов служб. Тип службы представляет собой отнесение службы к определенной категории, Hello классификации может иметь различные параметры и конфигурации, но hello hello основные функциональные возможности остаются одинаковыми. Hello экземпляров службы являются hello различные варианты конфигурации из hello же тип службы.  

Классы (или типы) приложений и служб описываются с помощью XML-файлов (манифесты приложений и служб).  Hello манифесты являются шаблонами hello, по которым приложений может быть создан из хранилища образов hello кластера. Hello определение схемы для файла ServiceManifest.xml и ApplicationManifest.xml hello устанавливается вместе с hello Service Fabric SDK и средств слишком*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

Код Hello для экземпляров другое приложение выполняется как отдельные процессы даже если они размещаются в одном узле Service Fabric hello. Кроме того, можно управлять hello жизненного цикла для каждого экземпляра приложения (например, обновлены) независимо друг от друга. Hello следующей схеме показано, как типы приложений состоят из типы служб, которые в свою очередь, состоят из кода, конфигурации и пакетов данных. Схема toosimplify hello, hello пакетов кода/config/данные для `ServiceType4` отображаются, хотя каждого типа службы, включит некоторых или всех типов пакетов.

![Типы служб и типы приложений Service Fabric][cluster-imagestore-apptypes]

Два разных файла манифеста, используется toodescribe приложений и служб: hello манифест службы и манифест приложения. Манифесты подробно описаны в следующих разделах hello.

Может существовать один или несколько экземпляров типа службы активного в кластере hello. Например экземпляры службы с отслеживанием состояния или реплики, достичь высокой надежности, копируя состояние между репликами, расположенными на разных узлах в кластере hello. Репликация по существу обеспечивает избыточность для hello службы toobe доступны, даже в случае сбоя одного узла в кластере. Объект [секционированы службы](service-fabric-concepts-partitioning.md) Далее делит его состояние (и состоянии toothat шаблонов доступа) для узлов кластера hello.

Hello следующей схеме показаны hello связи между приложениями и экземплярами службы, разделы и реплики.

![Разделы и реплики в службе][cluster-application-instances]

> [!TIP]
> Можно просмотреть макет hello приложений в кластере с помощью Service Fabric Explorer средство hello, доступное на http://&lt;yourclusteraddress&gt;: 19080/обозреватель. Дополнительные сведения см. в статье [Визуализация кластера с помощью обозревателя Service Fabric](service-fabric-visualizing-your-cluster.md).
> 
> 

## <a name="describe-a-service"></a>Описание службы
Hello манифест службы декларативно определяет тип службы hello и версии. Он задает метаданные службы, такие как тип службы, свойства работоспособности, метрики балансировки нагрузки, двоичные файлы службы и файлы конфигурации.  Другими словами, он описывает пакеты кода, конфигурации и данных hello, составляющих toosupport пакета службы один или несколько типов служб. Ниже приведен простой пример манифеста служб.

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

**Версия** атрибуты неструктурированных строки и не обработать системой hello. Версия атрибуты являются tooversion используется для обновления каждого компонента.

В атрибуте **ServiceTypes** указывается, какие типы служб поддерживаются пакетами **CodePackages** в этом манифесте. При создании экземпляра службы в соответствии с одним из этих типов службы все пакеты кода, объявленные в этом манифесте, активируются путем запуска соответствующих точек входа. Полученный процессы Hello являются типами службы ожидаемый tooregister hello поддерживается во время выполнения. Служба типы объявляются на уровне манифеста hello и не уровня пакета кода hello. Поэтому при наличии нескольких пакетов кода, они все активируются всякий раз, когда hello система выполняет поиск любого из hello объявленных типов служб.

**SetupEntryPoint** — это точка входа привилегированные, который выполняется с таким же учетные данные как Service Fabric hello (обычно hello *LocalSystem* учетной записи) перед любой другой точки входа. Hello исполняемый файл, указанный с **EntryPoint** обычно является узел службы hello длительное время. наличие Hello точки входа отдельной установки позволяет избежать размещения службы hello toorun с высоким уровнем привилегий на длительное время. Hello исполняемый файл, указанный с **EntryPoint** запускается после **SetupEntryPoint** успешно завершает работу. Если когда-либо процесс hello завершает или аварийно завершает работу, результирующий процесс hello отслеживается и перезапуска (начиная с версии снова **SetupEntryPoint**).  

Типичные сценарии использования **SetupEntryPoint** являются при запуске исполняемого файла до запуска службы hello или выполнять операции с повышенными привилегиями. Например:

* Настройка и инициализация переменных среды, которые hello исполняемый требованиям службы. Это не исполняемые файлы ограниченный tooonly записано с помощью модели программирования hello Service Fabric. Например, npm.exe нужны определенные переменные среды, настроенные для развертывания приложения node.js.
* Настройка контроля доступа посредством установки сертификатов безопасности.

Дополнительные сведения о том, как tooconfigure hello **SetupEntryPoint** разделе [настройки hello политики для точки входа установки службы](service-fabric-application-runas-security.md)

**EnvironmentVariables** содержит список переменных среды, которые заданы для этого пакета кода. Переменные Environmentment могут переопределяться в hello `ApplicationManifest.xml` tooprovide различные значения для различным экземплярам службы. 

**DataPackage** объявляет папку с именем hello **имя** атрибут, содержащий toobe произвольный статических данных используются процессом hello во время выполнения.

**ConfigPackage** объявляет папку с именем hello **имя** атрибут, который содержит *Settings.xml* файла. файл параметров Hello содержит разделы параметры определяемых пользователем, ключ значение пары процесса hello считываются обратно во время выполнения. Во время обновления, если только hello **ConfigPackage** **версии** был изменен, то запуск процесса hello не перезапускается. Вместо этого обратного вызова уведомляет процесс hello, параметры конфигурации были изменены, поэтому их можно загрузить в память динамически. Ниже приведен пример файла *Settings.xml* .

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> Манифест служб может содержать множество пакетов кода, конфигураций и данных. Версия каждого из них устанавливается независимо.
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

## <a name="describe-an-application"></a>Описание приложения
манифест приложения Hello декларативно описывает тип приложения hello и версии. Он также указывает метаданные композиции службы, такие как стабильные имена, схема секционирования, число экземпляров и коэффициент репликации, политика безопасности и изоляции, ограничения на размещение, переопределения конфигурации и типы входящих в состав служб. также описываются домены балансировки нагрузки Hello, в которых размещается приложение hello.

Таким образом манифест приложения описывает элементы на уровне приложения hello и ссылается на один или дополнительные службы манифесты toocompose типа приложения. Ниже приведен простой пример манифеста приложения.

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

Манифесты службы, например **версии** атрибуты неструктурированных строки и не анализируются системой hello. Версия атрибуты являются также используется tooversion каждый компонент для выполнения обновлений.

**ServiceManifestImport** содержит ссылки на tooservice манифесты составляющих этот тип приложения. Импортированные манифесты служб определяют, какие типы служб допустимы для применения в приложении этого типа. В рамках hello ServiceManifestImport переопределить значения конфигурации в Settings.xml и переменных среды в файлах ServiceManifest.xml. 


**DefaultServices** декларируются экземпляры служб, которые создаются автоматически при создании экземпляра приложения в соответствии с его типом. Службы по умолчанию используются только для удобства и после создания во всех отношениях действуют как и обычные службы. Они обновляются вместе с другими службами в экземпляре приложения hello и может быть также удален.

> [!NOTE]
> Манифест приложения может содержать несколько импортированных манифестов служб и служб по умолчанию. Каждый импортированный манифест служб может иметь свою версию.
> 
> 

toomaintain различные приложения и параметры обслуживания для соответствующей среды. в статье toolearn [Управление параметрами приложения для нескольких сред](service-fabric-manage-multiple-environment-app-configuration.md).

<!--
For more information about other features supported by application manifests, refer toohello following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a>Дальнейшие действия
[Упаковка приложения](service-fabric-package-apps.md) и сделать его готовности toodeploy.

[Развертывание и удаление приложений] [ 10] описывает как экземпляры приложения toomanage toouse PowerShell.

[Управление параметрами приложения для нескольких сред] [ 11] описывает способ tooconfigure параметров и переменных среды для экземпляров другого приложения.

[Настройка политик безопасности для приложения] [ 12] описывает, каким образом службы toorun toorestrict политики безопасности доступа.

В статье [Модель размещения Service Fabric][13] рассматривается связь между репликами (или экземплярами) развернутой службы и процессом размещения службы.

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
