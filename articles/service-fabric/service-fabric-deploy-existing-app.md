---
title: "aaaDeploy существующего исполняемого tooAzure Service Fabric | Документы Microsoft"
description: "Пошаговое руководство по развертыванию кластера Service Fabric tooa toopackage существующее приложение в качестве гостевой исполняемый файл, поэтому он может быть"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a>Развертывание гостевого исполняемого tooService структуры
В Azure Service Fabric можно запустить как службу приложение любого типа, в том числе приложения Node.js, Java или C++. Service Fabric toothese типов служб называется гостевой исполняемые файлы.

Гостевые исполняемые файлы обрабатываются в Service Fabric как службы без отслеживания состояния. Это значит, что они будут размещены на узлах кластера на основе доступности и других метрик. В этой статье описывается как toopackage и развернуть гостевой кластер Service Fabric tooa исполняемый файл с помощью Visual Studio или программы командной строки.

В этой статье мы охватывают действия hello toopackage гостевой исполняемый файл и разверните его tooService структуры.  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a>Преимущества запуска гостевого исполняемого файла в Service Fabric
Существует несколько преимуществ toorunning гостевой исполняемый объект в кластер Service Fabric.

* обеспечение высокой доступности; Приложения, работающие в среде Service Fabric, отличаются высоким уровнем доступности. Service Fabric обеспечивает выполнение экземпляров приложения.
* Наблюдение за работоспособностью системы. Service Fabric наблюдает за работоспособностью приложений и в случае сбоя предоставляет диагностические данные.   
* Управление жизненным циклом приложений. Помимо обновления без простоев, Service Fabric предоставляет автоматического отката toohello предыдущей версии, если событие работоспособности неправильный отчет во время обновления.    
* Плотность. В кластере, что исключает необходимость hello для каждого приложения toorun на собственное оборудование, можно запускать несколько приложений.
* Возможность обнаружения: С помощью REST можно вызвать toofind служба именования Service Fabric hello другие службы в кластере hello. 

## <a name="samples"></a>Примеры
* [Пример для упаковки и развертывания гостевого исполняемого файла](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Пример двух гостевой исполняемых файлов (C# и nodejs) общения с помощью службы именования hello, с помощью REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a>Обзор файлов манифестов приложений и служб
В рамках развертывания гостевой исполняемый файл, он является полезным toounderstand hello Service Fabric упаковки и развертывания модели как описано в [модель приложения](service-fabric-application-model.md). модель упаковки Service Fabric Hello основывается на двух файлах XML: hello манифесты приложений и служб. Hello определение схемы для hello файлы ApplicationManifest.xml и ServiceManifest.xml должен быть установлен с hello Service Fabric SDK в *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

* **Манифест приложения** hello манифест приложения — приложение hello используется toodescribe. Перечисляются службы hello, составляющих его и другими параметрами, используемые toodefine следует развернуть как одна или несколько служб, например hello число экземпляров.

  В Service Fabric приложение — это единица развертывания и обновления. Приложение может обновляться как одна единица, для которой выполняется управление потенциальными сбоями и откатами. Service Fabric гарантирует, что процесс обновления hello является либо успешно, или при сбое обновления hello не оставляет приложение hello в неизвестном или работает нестабильно состоянии.
* **Манифест службы** манифест службы hello описывает hello компоненты службы. Он включает в себя данные, такие как имя hello и тип службы и его код и конфигурация. Hello манифест службы также содержит некоторые дополнительные параметры, которые можно использовать службу hello tooconfigure после его развертывания.

## <a name="application-package-file-structure"></a>Структура файла пакета приложения
toodeploy приложения tooService структуры приложения hello должны следовать стандартные каталогов. Hello ниже приведен пример этой структуры.

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

Hello ApplicationPackageRoot содержит файл ApplicationManifest.xml hello, определяющий приложение hello. Вложенный каталог для каждой службы в приложение hello — используется toocontain все hello артефакты, необходимые службе hello. Эти подкаталоги будут hello ServiceManifest.xml и, как правило, hello следующие:

* *Code*. Эта папка содержит код службы hello.
* *Config*. Эта папка содержит файл Settings.xml (и другие файлы при необходимости) доступность службы hello во время выполнения tooretrieve определенные параметры конфигурации.
* *Data*. Это дополнительный каталог toostore Дополнительные локальные данные, может потребоваться hello службы. Данные должны быть toostore используется только временных данных. Если необходимо toobe переместить (например, во время отработки отказа), служба hello Service Fabric не копирует и реплицировать изменения toohello каталог данных.

> [!NOTE]
> Нет toocreate hello `config` и `data` каталоги, если они не нужны.
>
>

## <a name="package-an-existing-executable"></a>Упаковка существующего исполняемого файла
При упаковке гостевой исполняемый файл, вы можете либо toouse шаблон проекта Visual Studio или слишком[вручную создать пакет приложения hello](#manually). С помощью Visual Studio, hello структуры пакета приложения и файлы манифеста создаются hello новый шаблон проекта для вас.

> [!TIP]
> toouse Visual Studio — Hello простым способом toopackage существующий исполняемый файл в службу Windows и Linux toouse Yeoman
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a>Использовать toopackage Visual Studio и развертывать существующего исполняемого файла
Visual Studio предоставляет Service Fabric toohelp шаблона службы, можно развернуть гостевой кластер Service Fabric исполняемый tooa.

1. Чтобы создать приложение Service Fabric, выберите **Файл** > **Создать проект**.
2. Выберите **гостевой исполняемый файл** как hello шаблона службы.
3. Нажмите кнопку **Обзор** tooselect hello папка с исполняемый файл и заполните поля на rest hello toocreate hello hello параметров службы.
   * *Поведение пакета кода*. Может быть набор toocopy все содержимое hello toohello вашей папки проекта Visual Studio, это полезно, если hello исполняемый файл не изменяется. Если ожидается, что исполняемый файл toochange hello и динамически требуется hello toopick возможность копирования новые сборки, вы можете toolink toohello папки. При создании проекта приложения hello в Visual Studio, можно использовать связанные папки. Это свяжет toohello источника, откуда в рамках проекта hello, благодаря чему вы tooupdate hello гостевой исполняемый файл в поле назначения источника. Эти обновления становятся частью пакета приложения hello в сборке.
   * *Программа* указывает hello исполняемый файл, который следует запускать службы toostart hello.
   * *Аргументы* указывает hello аргументы, которые должны быть переданы toohello исполняемый файл. Здесь можно указать список параметров с аргументами.
   * *WorkingFolder* указывает hello рабочий каталог для hello процесс, который будет запущен toobe. Можно задать три значения:
     * `CodeBase`Указывает, что hello рабочий каталог будет toobe задать каталог toohello кода в пакете приложения hello (`Code` directory, показанным в hello предшествующий структура файла).
     * `CodePackage`Указывает, что hello рабочий каталог будет toobe задать корень toohello пакета приложения hello (`GuestService1Pkg` показано в предшествующих структура файла hello).
     * `Work`Указывает, что hello файлы помещаются в подкаталог с именем работы.
4. Присвойте службе имя и нажмите кнопку **ОК**.
5. Если службе нужна конечную точку для взаимодействия, теперь можно добавить hello протокол, порт и файле ServiceManifest.xml toohello типа. Например, `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.
6. Теперь можно использовать пакет hello и публикации действия для локального кластера. с помощью отладки hello решения в Visual Studio. Когда все будет готово, можно опубликовать hello приложения tooa удаленного кластера или установить в элемент управления toosource решения hello.
7. Как перейти toohello конце этой статьи toosee tooview гостевой исполняемый файл службы в обозреватель Service Fabric.

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a>Использование Yoeman toopackage и развертывания существующего исполняемого файла в Linux

Hello процедуры для создания и развертывания гостевой исполняемый файл в Linux hello такой же, как развертывание приложения на c# или java.

1. В окне терминала введите `yo azuresfguest`.
2. Присвойте имя приложению.
3. Службы, введите имя и сведения о hello, включая путь к исполняемому hello и hello параметры, которые должны вызываться с использованием.

Yeoman создает пакет приложения с помощью соответствующего приложения hello и файлы манифеста, наряду с установки и удаления скриптов.

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a>Упаковка и развертывание имеющегося исполняемого файла вручную
процесс Hello вручную упаковки гостевой исполняемый файл основан на hello следующие общие шаги:

1. Создайте структуру каталогов пакета hello.
2. Добавьте приложение hello код и файлы конфигурации.
3. Измените файл манифеста службы hello.
4. Измените файл манифеста приложения hello.

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a>Создать структуру каталогов пакета hello
Можно запустить, создание hello структуры каталогов, как описано в предыдущих разделов, hello «Структура файла пакета приложения».

### <a name="add-hello-applications-code-and-configuration-files"></a>Добавление приложения hello код и файлы конфигурации
После создания структуры каталогов hello, можно добавить приложение hello код и файлы конфигурации в группе кода и конфигурации каталогов hello. Можно также создать дополнительные каталоги файлов или подкаталогов в каталогах hello кода или конфигурации.

Service Fabric `xcopy` содержимого hello hello корневому каталогу приложения, поэтому нет предопределенных структуры toouse Кроме создание двух каталогов top, код и параметры. (Вы можете выбрать любые имена. Дополнительные сведения находятся в следующем разделе hello.)

> [!NOTE]
> Убедитесь, что включение всех файлов hello и зависимости, которые hello потребностей приложения. Service Fabric копирует hello содержимого пакета приложения hello на всех узлах в кластере hello, где службы приложения hello находятся toobe будет развернут. Hello пакет должен содержать все кода hello, что hello приложению toorun. Не следует считать зависимости hello уже установлены.
>
>

### <a name="edit-hello-service-manifest-file"></a>Изменить файл манифеста службы hello
Hello следующим шагом является tooedit hello службы файл манифеста tooinclude hello следующую информацию:

* Hello имя типа службы hello. — Это идентификатор, что Service Fabric использует tooidentify службы.
* Hello команда toouse toolaunch hello приложения (ExeHost).
* Любой сценарий, который требуется запустить toobe tooset приложения hello (SetupEntrypoint).

Hello ниже приведен пример `ServiceManifest.xml` файла:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

Hello в следующих разделах рассмотрены различные части файла hello необходимые tooupdate hello.

#### <a name="update-servicetypes"></a>Обновление ServiceTypes
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* Выберите для `ServiceTypeName`любое имя. Hello значение используется в hello `ApplicationManifest.xml` файловой службы tooidentify hello.
* Укажите `UseImplicitHost="true"`. Этот атрибут сообщает Service Fabric, что служба hello основывается на автономное приложение, должно все Service Fabric toodo toolaunch его как процесс и осуществлять мониторинг его состояния.

#### <a name="update-codepackage"></a>Обновление CodePackage
элемент CodePackage Hello указывает расположение hello (и версию) кода hello службы.

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

Hello `Name` элемент — используется toospecify hello имя каталога hello в пакет приложения hello, который содержит код службы hello. `CodePackage`также имеет hello `version` атрибута. Это может быть используется toospecify hello версию кода hello и потенциально может быть использовано код tooupgrade hello службы с помощью инфраструктуры управления жизненным циклом приложения hello в Service Fabric.

#### <a name="optional-update-setupentrypoint"></a>Обновление SetupEntrypoint (необязательно)
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
элемент SetupEntryPoint Hello является исполняемым или пакетным файлом, которая должна выполняться перед запуском кода hello службы используется toospecify. Это необязательный шаг, поэтому она не должна toobe включено, если не требуется инициализация. Hello SetupEntryPoint выполняется каждый раз при перезапуске службы hello.

Имеется только один SetupEntryPoint сценариев установки требуется toobe группируются в одном пакетном файле, если установка приложения hello требует нескольких сценариев. Hello SetupEntryPoint могут выполнять все типы файлов: исполняемых файлов, пакетных файлов и командлеты PowerShell. Подробнее см. в статье [Настройка SetupEntryPoint](service-fabric-application-runas-security.md).

В предыдущих пример hello, hello SetupEntryPoint выполнение пакетного файла вызывается `LaunchConfig.cmd` , расположенного в hello `scripts` подкаталоге каталога кода hello (при условии, что hello WorkingFolder имеет значение tooCodeBase).

#### <a name="update-entrypoint"></a>Обновление EntryPoint
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

Hello `EntryPoint` элемент в файл манифеста службы hello — toospecify используется как toolaunch hello службы. Hello `ExeHost` элемент указывает hello исполняемый файл (и аргументы), следует использовать toolaunch hello службы.

* `Program`Указывает имя hello hello исполняемый файл, который необходимо запустить службу hello.
* `Arguments`Указывает hello аргументы, которые должны быть переданы toohello исполняемый файл. Здесь можно указать список параметров с аргументами.
* `WorkingFolder`Указывает рабочий каталог hello для hello процесс, который будет запущен toobe. Можно задать три значения:
  * `CodeBase`Указывает, что hello рабочий каталог будет toobe задать каталог toohello кода в пакете приложения hello (`Code` каталог в hello предшествующий структура файла).
  * `CodePackage`Указывает, что hello рабочий каталог будет toobe задать корень toohello пакета приложения hello (`GuestService1Pkg` в hello предшествующий структура файла).
    * `Work`Указывает, что hello файлы помещаются в подкаталог с именем работы.

Hello WorkingFolder является полезным tooset hello правильный рабочий каталог для использования относительных путей скриптами либо hello приложения или инициализации.

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a>Обновление конечных точек и регистрация в службе именования для обмена данными
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
В предыдущих пример hello, hello `Endpoint` элемент указывает hello конечных точек, которые могут прослушивать приложения hello. В этом примере hello Node.js приложение прослушивает http через порт 3000.

Кроме того можно попросить Service Fabric toopublish toohello этой конечной точки службы именования, другие службы может обнаруживать адрес toothis hello конечной точки службы. Это позволит вам может toocommunicate toobe между службами исполняемых гостевой.
Hello опубликованных адрес конечной точки — hello формы `UriScheme://IPAddressOrFQDN:Port/PathSuffix`. `UriScheme` и `PathSuffix` являются необязательными атрибутами. `IPAddressOrFQDN`— hello IP-адрес или полное доменное имя узла hello этот исполняемый файл помещается в и вычисляется автоматически.

В hello примере один раз hello служба развернута, в обозреватель Service Fabric см конечной точки аналогично слишком`http://10.1.4.92:3000/myapp/` публикации для экземпляра службы hello. Если используется локальный компьютер, она будет в формате `http://localhost:3000/myapp/`.

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
Можно использовать эти адреса с [обратный прокси-сервер](service-fabric-reverseproxy.md) toocommunicate между службами.

### <a name="edit-hello-application-manifest-file"></a>Изменить файл манифеста приложения hello
После настройки hello `Servicemanifest.xml` файл, необходимо toomake некоторые изменения toohello `ApplicationManifest.xml` файл tooensure, hello правильный тип службы и имя используются.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a>ServiceManifestImport
В hello `ServiceManifestImport` элемента, можно указать одну или несколько служб, которые должны tooinclude в приложение hello. Службы указываются с `ServiceManifestName`, который указывает имя hello hello каталога, в которой hello `ServiceManifest.xml` находится файл.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a>Настройка ведения журнала
Для исполняемых файлов гостя является toofind журналы консоли может toosee полезно toobe out hello сценариев приложения и конфигурации показа ошибок.
Перенаправление консоли можно настроить в hello `ServiceManifest.xml` файла с помощью hello `ConsoleRedirection` элемента.

> [!WARNING]
> Никогда не используйте политику перенаправления консоли hello в приложении, которое развертывается в рабочей среде, так как это может повлиять на приложения hello перехода на другой ресурс. Используйте ее *только* для локальной разработки и отладки.  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

`ConsoleRedirection`можно использовать tooredirect консоли вывода (stdout и stderr) tooa рабочий каталог. Это обеспечивает возможность tooverify hello, нет ли ошибок во время установки hello или выполнение приложения hello в кластер Service Fabric hello.

`FileRetentionCount`Определяет, сколько файлов сохраняются в рабочем каталоге hello. Например, значение 5, означает, что hello для предыдущих выполнений пять hello находятся файлы журналов в рабочем каталоге hello.

`FileMaxSizeInKb`Указывает максимальный размер файлов журнала hello hello.

Файлы журнала сохраняются в одном из рабочих hello службы каталогов. toodetermine, где находятся файлы hello, используйте обозреватель Service Fabric toodetermine службу hello узла, которая выполняется на, и какой рабочий каталог используется. Эта процедура рассмотрена далее в этой статье.

## <a name="deployment"></a>Развертывание
Hello последним этапом является слишком[развертывания приложения](service-fabric-deploy-remove-applications.md). Здравствуйте, следуя показан сценарий PowerShell как toodeploy вашего приложения toohello локальному кластеру разработки, а также запускать новую службу Service Fabric.

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> [Сжатие пакета hello](service-fabric-package-apps.md#compress-a-package) перед копированием toohello хранилища образов, если пакет hello большой или имеет много файлов. Дополнительные сведения см. [здесь](service-fabric-deploy-remove-applications.md#upload-the-application-package).
>

Службу Service Fabric можно развертывать в разных конфигурациях. Например его можно развернуть в качестве одного или нескольких экземпляров, или он может быть развернут таким образом, что имеется один экземпляр службы hello на каждом узле кластера Service Fabric hello.

Hello `InstanceCount` параметр hello `New-ServiceFabricService` командлета — используется toospecify, сколько экземпляров hello службы должны запускаться в кластер Service Fabric hello. Можно задать hello `InstanceCount` значение в зависимости от типа развертываемого приложения hello. Ниже приведены Hello два наиболее распространенных сценариев.

* `InstanceCount = "1"`. В этом случае в кластере hello развертывается только один экземпляр службы hello. Планировщик Service Fabric определяет, какие службы hello узла будет toobe, развернутой на.
* `InstanceCount ="-1"`. В этом случае один экземпляр службы hello развертывается на всех узлах кластера Service Fabric hello. результат Hello наличие одного (и только одного) экземпляр службы hello для каждого узла в кластере hello.

Это полезно конфигурации для клиентских приложений (например, конечную точку REST), так как клиентские приложения должны слишком «подключиться» tooany hello узлов в конечную точку hello toouse кластера hello. Эта конфигурация используется также при, например, все узлы кластера Service Fabric hello подключенных tooa подсистемы балансировки нагрузки. Затем клиентский трафик можно распределить между hello службу, которая выполняется на всех узлах в кластере hello.

## <a name="check-your-running-application"></a>Проверка работающего приложения
В обозреватель Service Fabric определите узел hello, где запущена служба hello. В этом примере она выполняется на узле Node1.

![Узел, на котором запущена служба](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

Если перехода узла toohello и toohello с приложением можно увидеть hello узел важные сведения, включая ее расположение на диске.

![Расположение на диске](./media/service-fabric-deploy-existing-app/locationondisk2.png)

При просмотре каталога toohello с помощью обозревателя серверов можно найти hello рабочий каталог и папки журнала hello службы, как показано на следующий снимок экрана приветствия: 

![Расположение журнала](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы узнали как toopackage гостевой исполняемый файл и развернуть ее tooService структуры. См. следующие статьи для связанной информации и задачи hello.

* [Пример для упаковки и развертывания гостевой исполняемый файл](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), включая предварительный выпуск toohello ссылку средства упаковки hello
* [Пример двух гостевой исполняемых файлов (C# и nodejs) общения с помощью службы именования hello, с помощью REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [Развертывание нескольких пользовательских приложений](service-fabric-deploy-multiple-apps.md)
* [Создание первого приложения Service Fabric в Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md)
