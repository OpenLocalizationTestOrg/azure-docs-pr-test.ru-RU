---
title: "aaaConvert toomicroservices приложений облачных служб Azure | Документы Microsoft"
description: "В этом руководстве сравнивает облачных служб Web и рабочих ролей и toohelp Service Fabric службы без сохранения состояния миграции из облачных служб tooService структуры."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 5880ebb3-8b54-4be8-af4b-95a1bc082603
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c43b11623b2ba7f6069782a8b7e030c82572a6e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="guide-tooconverting-web-and-worker-roles-tooservice-fabric-stateless-services"></a>Руководство по tooconverting Web and Worker Roles tooService структуры службы без сохранения состояния
В этой статье описывается как toomigrate вашей облачной службы Web and Worker Roles tooService структуры службы без сохранения состояния. Это простейший способ переноса hello из облачных служб tooService структуры hello приложений которого общая архитектура будет toostay примерно таким же.

## <a name="cloud-service-project-tooservice-fabric-application-project"></a>Облако проект приложения Fabric tooService проекта служб
 Проекта облачной службы и проект приложения Fabric Service имеют схожую структуру и оба представляют Привет развертывания модульных для приложения — то есть, каждый из них определяет полный пакет hello, развернутых toorun приложения. Проект облачной службы содержит веб-роли или рабочие роли (одну или несколько). Подобным образом содержит несколько служб и проект приложения Service Fabric. 

Hello различие заключается в том couples проекта облачной службы hello hello развертывания приложений с помощью развертывания виртуальной Машины и таким образом, содержит параметры конфигурации виртуальной Машины, в то время как проект приложения Fabric Application hello только определяет приложение, которое будет развертываться набор tooa существующих виртуальных машин в кластере Service Fabric. самого кластера Service Fabric Hello развертывается только один раз, либо посредством шаблона диспетчера ресурсов либо через портал Azure hello и несколько Service Fabric, приложения могут быть развернуты tooit.

![Сравнение проекта облачных служб и проекта Service Fabric][3]

## <a name="worker-role-toostateless-service"></a>Служба toostateless рабочей роли
По существу рабочей роли представляет рабочей нагрузки без отслеживания состояния, то есть каждый экземпляр рабочей нагрузки hello идентична и запросы могут быть перенаправленное tooany экземпляра в любое время. Каждый экземпляр не является ожидаемым tooremember hello предыдущего запроса. Состояние данной рабочей нагрузке hello работает с управляемых хранилищем внешнего состояния, например табличного хранилища Azure или Azure DB документа. В платформе Service Fabric рабочей нагрузке этого типа соответствует служба без отслеживания состояния. Hello простой подход toomigrating tooService рабочей роли фабрики должен выполнять преобразование tooa кода рабочей роли службы без отслеживания состояния.

![TooStateless рабочей роли службы][4]

## <a name="web-role-toostateless-service"></a>Веб-службы роли toostateless
Аналогичные tooWorker роли веб-роли также представляет рабочей нагрузки без отслеживания состояния, и поэтому концептуально слишком может быть сопоставленных tooa службы без отслеживания состояния Service Fabric. В отличие от веб-ролей, платформа Service Fabric не поддерживает IIS. toomigrate веб-приложения из службы без отслеживания состояния tooa веб-роль требует первый скользящего tooa веб-платформа, может быть резидентным и не зависит от System.Web, например ASP.NET Core 1 или IIS.

| **Приложения** | **Поддерживаются** | **Путь перехода** |
| --- | --- | --- |
| Веб-формы ASP.NET |Нет |Преобразовать tooASP.NET основы 1 MVC |
| ASP.NET MVC 3 |С переносом |Обновления tooASP.NET основы 1 MVC |
| Веб-API ASP.NET |С переносом |Использование автономно размещаемого сервера или компонента ASP.NET Core 1 |
| ASP.NET Core 1 |Да |Недоступно |

## <a name="entry-point-api-and-lifecycle"></a>Жизненный цикл и интерфейс API точки входа
Рабочая роль и интерфейсы API службы Service Fabric дают возможность использовать похожие точки входа. 

| **Точка входа** | **Рабочая роль** | **Служба Service Fabric** |
| --- | --- | --- |
| Обработка |`Run()` |`RunAsync()` |
| Запуск виртуальной машины |`OnStart()` |Недоступно |
| Остановка виртуальной машины |`OnStop()` |Недоступно |
| Открытие прослушивателя для запросов клиентов |Недоступно |<ul><li> `CreateServiceInstanceListener()` для служб без отслеживания состояния</li><li>`CreateServiceReplicaListener()` для служб с отслеживанием состояния</li></ul> |

### <a name="worker-role"></a>Рабочая роль
```C#

using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
        }

        public override bool OnStart()
        {
        }

        public override void OnStop()
        {
        }
    }
}

```

### <a name="service-fabric-stateless-service"></a>Служба без отслеживания состояния Service Fabric
```C#

using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace Stateless1
{
    public class Stateless1 : StatelessService
    {
        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
        }

        protected override Task RunAsync(CancellationToken cancelServiceInstance)
        {
        }
    }
}

```

Во время обработки которых toobegin имеют Переопределение основной «запуск». Службы Service Fabric объединяют `Run`, `Start` и `Stop` в одну точку входа, `RunAsync`. Службы должны начать работать после `RunAsync` начинается и прекратить работу при hello `RunAsync` сигнал CancellationToken метода. 

Существует несколько ключевых различий между жизненного цикла hello и временем существования рабочих ролей и Service Fabric служб:

* **Жизненный цикл:** hello Главное отличие — что рабочая роль является виртуальной Машины и его жизненного цикла равноценных toohello виртуальную Машину, которая включает в себя события, запускает и останавливает hello виртуальной Машины. Служба Service Fabric имеет жизненного цикла, отдельном от hello жизненный цикл виртуальной Машины, поэтому он не включает события для при hello размещения виртуальной Машины или запуске компьютера или остановка, как они не связаны.
* **Время существования:** экземпляра рабочей роли будут обновляться при hello `Run` метод завершает работу. Hello `RunAsync` методы в службе Service Fabric тем не менее можно запустить toocompletion и hello экземпляр службы будет работать. 

Службам, которые прослушивают запросы клиента, платформа Service Fabric дает возможность использовать пользовательскую точку входа настройки связи. Hello RunAsync и точка входа связи переопределяются необязательно в Service Fabric служб - службы может выбрать tooonly прослушивания tooclient запросы или только запустить цикл обработки или оба - которых именно hello RunAsync метод может быть tooexit без перезапуск экземпляра службы hello, так как он может по-прежнему toolisten для клиентских запросов.

## <a name="application-api-and-environment"></a>Интерфейс API и среда приложения
Среда облачные службы Hello API предоставляет сведения и функциональные возможности для hello текущего экземпляра виртуальной Машины, а также сведения о других экземпляров ролей виртуальной Машины. Service Fabric предоставляет сведения, связанные с tooits среды выполнения и некоторые сведения об узле hello службы сейчас выполняется. 

| **Задача среды** | **Облачные службы** | **Service Fabric** |
| --- | --- | --- |
| Параметры конфигурации и изменение уведомления |`RoleEnvironment` |`CodePackageActivationContext` |
| Локальное хранилище |`RoleEnvironment` |`CodePackageActivationContext` |
| Сведения о конечной точке |`RoleInstance` <ul><li>Текущий экземпляр: `RoleEnvironment.CurrentRoleInstance`</li><li>Другие роли и экземпляр: `RoleEnvironment.Roles`</li> |<ul><li>`NodeContext` для адреса текущего узла</li><li>`FabricClient` и `ServicePartitionResolver` для обнаружения конечной точки службы</li> |
| Эмуляция среды |`RoleEnvironment.IsEmulated` |Недоступно |
| Событие одновременного изменения |`RoleEnvironment` |Недоступно |

## <a name="configuration-settings"></a>Параметры конфигурации
Параметры конфигурации в облачных службах задаются для роли ВМ и применяются tooall экземпляры этой роли виртуальной Машины. Эти параметры представляют собой пары "ключ — значение", заданные в файлах ServiceConfiguration.*.cscfg. Получить к ним прямой доступ можно через RoleEnvironment. В Service Fabric параметры применяются по отдельности tooeach службы и приложения tooeach вместо tooa виртуальной Машины, так как виртуальная машина может размещаться несколько служб и приложений. Служба состоит из трех пакетов:

* **Код:** содержит hello исполняемых файлов службы, двоичные файлы, библиотеки DLL и другие файлы toorun необходимых для работы служб.
* **Конфигурация:** все файлы конфигурации и параметры для службы.
* **Данные:** статические данные файлы, связанные со службой hello.

Каждый из этих пакетов можно отдельно обновить, в том числе до определенной версии. Службы, аналогичные tooCloud, пакет конфигурации может осуществляться программно через API и события, доступные toonotify службы hello изменения конфигурации пакета. Файл Settings.xml может использоваться для ключа и значения конфигурации и программный доступ аналогичные toohello разделе параметров приложения из файла App.config. Однако, в отличие от облачных служб, пакет конфигурации Service Fabric может содержать любые файлы конфигурации в любом формате, будь то XML, JSON, YAML или пользовательский двоичный формат. 

### <a name="accessing-configuration"></a>Получение доступа к конфигурации
#### <a name="cloud-services"></a>Облачные службы
Доступ к параметрам конфигурации из файла ServiceConfiguration.*.cscfg можно получить с помощью атрибута `RoleEnvironment`. Эти параметры являются глобально доступной tooall экземпляры роли в hello же развертывании облачной службы.

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a>Service Fabric
Каждая служба имеет отдельный пакет конфигурации. Не существует встроенного механизма, который предназначен для глобальных параметров конфигурации, доступных всем приложениям кластера. При использовании Service Fabric специальные Settings.xml конфигурации файл конфигурации пакета, значения в Settings.xml могут быть перезаписаны на уровне приложения hello, внося изменения в параметры уровня приложения невозможно.

Параметры конфигурации являются обращений для каждого экземпляра службы через службу hello `CodePackageActivationContext`.

```C#

ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");

// Access Settings.xml
KeyedCollection<string, ConfigurationProperty> parameters = configPackage.Settings.Sections["MyConfigSection"].Parameters;

string value = parameters["Key"]?.Value;

// Access custom configuration file:
using (StreamReader reader = new StreamReader(Path.Combine(configPackage.Path, "CustomConfig.json")))
{
    MySettings settings = JsonConvert.DeserializeObject<MySettings>(reader.ReadToEnd());
}

```

### <a name="configuration-update-events"></a>События обновления конфигурации
#### <a name="cloud-services"></a>Облачные службы
Hello `RoleEnvironment.Changed` событие является используется toonotify все экземпляры роли, когда изменение происходит в среде hello, например изменение конфигурации. Это используется tooconsume обновлений конфигурации без перезапуска экземпляров роли или перезапуска рабочего процесса.

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get hello list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a>Service Fabric
Каждый из трех типов пакета hello в службе - кода, конфигурации и данных - имеют события, уведомляющие экземпляр службы обновлена, добавлении или удалении пакета. Служба может содержать несколько пакетов каждого типа. Например, служба может иметь несколько пакетов конфигурации, для каждого из которых можно задать версию и каждый из которых можно обновлять. 

Эти события являются доступными tooconsume изменения в пакеты служб без перезапуска экземпляра службы hello.

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a>Задачи при запуске
Задачи при запуске — это действия, выполняемые перед запуском приложения. Задачи запуска — типовыми toorun сценариев установки, с использованием повышенных привилегий. Эти задачи поддерживаются и облачными службами, и платформой Service Fabric. Hello основное отличие заключается в, в облачных службах, задачи запуска — равноценных tooa виртуальной Машины, так как он является частью экземпляра роли, а в Service Fabric задачи запуска — tooa связанные службы, которая не является равноценных tooany конкретной виртуальной Машины.

| Облачные службы | Service Fabric |
| --- | --- | --- |
| Расположение конфигурации |ServiceDefinition.csdef |
| Привилегии |Ограниченные или повышенные |
| Виртуализация |Простая, фоновая, на переднем плане |

### <a name="cloud-services"></a>Облачные службы
В облачных службах точка входа для запуска настраивается для каждой роли в файле ServiceDefintion.csdef. 

```xml

<ServiceDefinition>
    <Startup>
        <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
            <Environment>
                <Variable name="MyVersionNumber" value="1.0.0.0" />
            </Environment>
        </Task>
    </Startup>
    ...
</ServiceDefinition>

```

### <a name="service-fabric"></a>Service Fabric
В Service Fabric точка входа для запуска настраивается для каждой роли в файле ServiceManifest.xml.

```xml

<ServiceManifest>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>Startup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    ...
</ServiceManifest>

``` 

## <a name="a-note-about-development-environment"></a>Примечание о среде разработки
Облачные службы и Service Fabric интегрированного в Visual Studio с помощью шаблонов проектов и поддержка для отладки, настройке и развертыванию локально и tooAzure. Кроме того, облачные службы и платформа Service Fabric дают возможность пользоваться локальной средой выполнения разработки. Hello различие состоит в том, пока hello облачной службы среды выполнения разработки эмулирует hello среды Azure, в котором она выполняется, Service Fabric не использовать симулятор — он использует hello завершения среда выполнения Service Fabric. Hello Service Fabric, среда выполнения на локальном компьютере разработчика hello одной среде, работающей в рабочей среде.

## <a name="next-steps"></a>Дальнейшие действия
Более подробные сведения о надежных структуры службы и hello фундаментальные различия между облачными службами и toounderstand архитектуры приложения Service Fabric, как tootake преимуществами hello полный набор возможностей Service Fabric.

* [Начало работы со службами Reliable Services в Service Fabric](service-fabric-reliable-services-quick-start.md)
* [Руководство по концептуальной toohello различия между облачными службами и Service Fabric](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
