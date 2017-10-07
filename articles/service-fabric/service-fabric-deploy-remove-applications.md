---
title: "развертывание приложения Service Fabric aaaAzure | Документы Microsoft"
description: "Как toodeploy и удаление приложений в Service Fabric, с помощью PowerShell."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 3de9c6a937ee7b29bf9ec86d6e9e631487797507
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a>Развертывание и удаление приложений с помощью PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [API-интерфейсы FabricClient](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

После [создания пакета приложения][10] его можно развернуть в кластере Azure Service Fabric. Развертывание включает hello следующие три шага:

1. Отправка хранилища образов toohello пакета приложения hello
2. Регистрация типа приложения hello
3. Создание экземпляра приложения hello

После развертывания приложения и экземпляр работает в кластере hello, можно удалить экземпляр приложения hello и его тип приложения. Удаление toocompletely приложение из кластера hello включает в себя hello следующие шаги:

1. Удалить (или) запущен экземпляр приложения hello
2. Отмена регистрации типа приложения hello, если оно больше не требуется
3. Удаление пакета приложения hello из хранилища образов hello

Если вы используете [Visual Studio для развертывания и отладки приложений](service-fabric-publish-app-remote-cluster.md) в кластере локальной разработки все hello описанные выше шаги автоматически обрабатываются с помощью сценария PowerShell.  Этот скрипт находится в hello *сценариев* папку проекта приложения hello. В этой статье приведены фона действиями этот скрипт, чтобы можно было выполнять hello и те же операции вне Visual Studio. 
 
## <a name="connect-toohello-cluster"></a>Подключите кластер toohello
Перед выполнением любых команд PowerShell в этой статье, всегда начинаются с помощью [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) кластера Service Fabric toohello tooconnect. tooconnect toohello локальному кластеру разработки, выполните hello ниже:

```powershell
PS C:\>Connect-ServiceFabricCluster
```

Примеры соединения tooa удаленного кластера или кластера, защищенные с помощью Azure Active Directory, X509 сертификаты или Windows Active Directory см. в разделе [кластера безопасное подключение tooa](service-fabric-connect-to-secure-cluster.md).

## <a name="upload-hello-application-package"></a>Отправить пакет приложения hello
Отправка пакета приложения hello помещает его в расположении, доступном из внутренних компонентов Service Fabric.
Пакет приложения hello tooverify локально, используйте hello [ServiceFabricApplicationPackage тест](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) командлета.

Hello [ServiceFabricApplicationPackage копирования](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) команда передачи hello хранилище образов кластера toohello пакета приложения.
Hello **Get ImageStoreConnectionStringFromClusterManifest** , который является частью модуля Service Fabric SDK PowerShell hello, — используется tooget hello изображение хранение строки подключения.  hello SDK tooimport модуль, запустите:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Предположим, вы собрали и упаковали в Visual Studio 2015 приложение с именем *MyApplication*. По умолчанию имя типа приложения hello, перечисленные в hello ApplicationManifest.xml является «MyApplicationType».  Hello пакет приложения, который содержит манифест необходимые приложения hello, манифесты и пакеты кода/config/данные, находится в *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\ MyApplication\MyApplication\pkg\Debug*. 

Hello следующая команда перечисляет hello содержимого пакета приложения hello:

```powershell
PS C:\> $path = 'C:\Users\<user\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug'
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
│   ApplicationManifest.xml
│
└───Stateless1Pkg
    │   ServiceManifest.xml
    │
    ├───Code
    │       Microsoft.ServiceFabric.Data.dll
    │       Microsoft.ServiceFabric.Data.Interfaces.dll
    │       Microsoft.ServiceFabric.Internal.dll
    │       Microsoft.ServiceFabric.Internal.Strings.dll
    │       Microsoft.ServiceFabric.Services.dll
    │       ServiceFabricServiceModel.dll
    │       Stateless1.exe
    │       Stateless1.exe.config
    │       Stateless1.pdb
    │       System.Fabric.dll
    │       System.Fabric.Strings.dll
    │
    └───Config
            Settings.xml
```

Если пакет приложения hello большой или имеет большое количество файлов, вы можете [Сжать](service-fabric-package-apps.md#compress-a-package). Hello сжатие приводит к уменьшению размера hello и hello количеством файлов.
Hello побочным эффектом является hello, регистрация и Отмена регистрации типа приложения работают быстрее. Время передачи могут работать медленнее в настоящее время, особенно в том случае, если включен пакет hello toocompress времени hello. 

пакет, используйте toocompress hello же [ServiceFabricApplicationPackage копирования](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) команды. Сжатие может выполняться отдельно в передаче, с помощью hello `SkipCopy` флаг или вместе с hello операции передачи. Применить сжатие к сжатому пакету невозможно.
toouncompress сжатый пакет, используйте hello же [копирования ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) с hello `UncompressPackage` переключения.

Hello следующий командлет сжимает hello пакета, не копируя его toohello хранилища образов. Hello пакет теперь содержит ZIP-файл для hello `Code` и `Config` пакетов. манифесты службы hello приложения Hello и являются не ZIP-, так как они требуются для многих внутренних операций (например, пакет управления доступом приложения имя и версия извлечения типа для определенных проверок). Архивировать манифесты hello сделает эти операции неэффективно.

```
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -CompressPackage -SkipCopy
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
|   ApplicationManifest.xml
|
└───Stateless1Pkg
       Code.zip
       Config.zip
       ServiceManifest.xml
```

Для больших пакетов приложений hello сжатие экономит время. Для получения наилучших результатов используйте быстрый SSD-диск. время сжатия Hello и hello размер сжатого пакета hello также зависят от содержимого пакета hello.
Например вот сжатия статистики для некоторых пакетов, в которых Показать начальной hello и hello размер сжатого пакета с временем сжатия hello.

|Исходный размер (МБ)|Число файлов|Время сжатия|Размер сжатого пакета (МБ)|
|----------------:|---------:|---------------:|---------------------------:|
|100|100|00:00:03.3547592|60|
|512|100|00:00:16.3850303|307|
|1024|500|00:00:32.5907950|615|
|2048|1000|00:01:04.3775554|1231|
|5012|100|00:02:45.2951288|3074|

После сжатия пакета может быть загруженного tooone или несколько Service Fabric кластеров при необходимости. механизм развертывания Hello же сжатые и несжатые пакетов. Если пакет hello сжаты, таким образом сохраняется в хранилище образов кластера hello и сжимаются на узле hello перед запуском приложения hello.


Hello следующий пример передает hello хранилища образов toohello пакета, в папку с именем «MyApplicationV1»:

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

Hello **Get ImageStoreConnectionStringFromClusterManifest** , который является частью модуля Service Fabric SDK PowerShell hello, — используется tooget hello изображение хранение строки подключения.  hello SDK tooimport модуль, запустите:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Если вы не укажете hello *- ApplicationPackagePathInImageStore* параметров пакета приложения hello копируется в папку «Debug» hello в хранилище образов hello.

Hello время, затрачиваемое tooupload пакета зависит от нескольких факторов. Некоторые из этих факторов, hello число файлов в пакет hello, размер пакета hello и размеры файлов hello. Hello скорость сетевого подключения между исходным компьютером hello и кластер Service Fabric hello также влияет на время передачи hello. Здравствуйте, время ожидания по умолчанию для [ServiceFabricApplicationPackage копирования](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) составляет 30 минут.
В зависимости от Здравствуйте описываются факторы, возможно, время ожидания tooincrease hello. При сжатии пакета hello в вызове hello копирования необходимо tooalso рассмотрим hello время сжатия.

В разделе [понять строка подключения хранилища изображения hello](service-fabric-image-store-connection-string.md) Дополнительные сведения о хранилище образов hello и image хранение строки подключения.

## <a name="register-hello-application-package"></a>Регистрация пакета приложения hello
Тип приложения Hello и версии, объявленные в манифесте приложения hello, становятся доступны для использования при регистрации пакета приложения hello. Hello система считывает переданный на предыдущем шаге hello пакет hello, проверяет пакет hello, обрабатывает содержимое пакета hello и копирует расположение внутреннего системного tooan hello обработки пакета.  

Запустите hello [ServiceFabricApplicationType регистра](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) tooregister командлет hello типа приложения в кластере hello и сделать его доступным для развертывания:

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

«MyApplicationV1» является папкой hello в хранилище образов hello, где находится пакет приложения hello. Тип приложения Hello с именем «MyApplicationType» и версией «1.0.0» (оба находятся в манифесте приложения hello) зарегистрирован в кластере hello.

Hello [ServiceFabricApplicationType регистра](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) команда возвращает только после hello система имеет пакет приложения успешно зарегистрирован hello. Как долго принимает регистрации зависит от размера hello и содержимого пакета приложения hello. При необходимости hello **- TimeoutSec** параметр можно использовать toosupply более длительного времени ожидания (hello время ожидания по умолчанию — 60 секунд).

При наличии большого приложения пакета или при возникновении тайм-ауты использовать hello **- Async** параметра. Команда Hello возвращает hello кластера принимает команды hello регистрации и обработки hello продолжается при необходимости.
Hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) команда выводит список всех версий типа успешно зарегистрированного приложения и состояние их регистрации. После завершения регистрации hello toodetermine этой команды можно использовать.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-hello-application"></a>Создание приложения hello
Можно создать приложение с любой версии типа приложения, который успешно зарегистрирован с помощью hello [New ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) командлета. Имя каждого приложения Hello должно начинаться с hello *«fabric: «* схему и должны быть уникальными для каждого экземпляра приложения. Также создаются все службы по умолчанию, определенных в манифесте приложения hello объекта тип целевого приложения hello.

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
Для каждой версии зарегистрированного типа приложения можно создать несколько экземпляров приложения. Каждый экземпляр выполняется изолированно, используя собственный рабочий каталог и процесс.

toosee имени приложения и службы работают в кластере hello, запустите hello [Get ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) и [Get ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) командлетов:

```powershell
PS C:\> Get-ServiceFabricApplication  

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Ok
ApplicationParameters  : {}

PS C:\> Get-ServiceFabricApplication | Get-ServiceFabricService

ServiceName            : fabric:/MyApp/Stateless1
ServiceKind            : Stateless
ServiceTypeName        : Stateless1Type
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
ServiceStatus          : Active
HealthState            : Ok
```

## <a name="remove-an-application"></a>Удаление приложения
При экземпляр приложения больше не нужен, можно окончательно удалить его по имени, используя hello [ServiceFabricApplication удаление](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) командлета. [Удаление ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) автоматически удаляет все службы, которые принадлежат toohello приложения также, без возможности восстановления, удаляя все состояния службы. 

> [!WARNING]
> Эта операция необратима, и вы не сможете восстановить состояние приложения.

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a>Отмена регистрации типа приложения
При определенной версии типа приложения больше не нужен, необходимо отменить регистрацию с помощью hello тип приложения hello [Unregister ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) командлета. Отмена регистрации неиспользуемые приложения типы выпуски пространства, используемого хранилища образов hello. Регистрацию типа приложения можно отменить в том случае, если на его основе не были созданы экземпляры приложений и нет ссылающихся на него незавершенных обновлений приложений.

Запустите [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) типы приложения hello toosee в настоящее время зарегистрированы в кластере hello:

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

Запустите [Unregister ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister приложения определенного типа:

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-hello-image-store"></a>Удаление пакета приложения из хранилища образов hello
Если пакета приложения больше не нужен, его можно удалить из hello образа хранилища toofree системные ресурсы.

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a>Устранение неполадок
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a>Команда Copy-ServiceFabricApplicationPackage запрашивает строку ImageStoreConnectionString
пакет Service Fabric SDK среды Hello должна уже иметь hello правильно настроить значения по умолчанию. Но при необходимости hello строка ImageStoreConnectionString для всех команд должны соответствует значению hello, hello кластер Service Fabric. Hello строка ImageStoreConnectionString можно найти в манифесте кластера hello, полученные при помощи hello [Get ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) и Get-ImageStoreConnectionStringFromClusterManifest команды:

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

Hello **Get ImageStoreConnectionStringFromClusterManifest** , который является частью модуля Service Fabric SDK PowerShell hello, — используется tooget hello изображение хранение строки подключения.  hello SDK tooimport модуль, запустите:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Строка ImageStoreConnectionString Hello можно найти в манифесте кластера hello:

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

В разделе [понять строка подключения хранилища изображения hello](service-fabric-image-store-connection-string.md) Дополнительные сведения о хранилище образов hello и image хранение строки подключения.

### <a name="deploy-large-application-package"></a>Развертывание пакета приложения большего размера
Проблема. Время ожидания выполнения команды [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) истекает для пакета большого приложения (несколько ГБ).
Попробуйте выполнить следующее.
- Задайте большее время ожидания для команды [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) с помощью параметра `TimeoutSec`. По умолчанию hello время ожидания составляет 30 минут.
- Проверьте hello сетевого подключения между исходным компьютером и кластера. Если используется медленное подключение hello, рассмотрите возможность использования на машине для улучшения подключения к сети.
Если hello клиентский компьютер находится в другом регионе hello кластера, рекомендуется использовать клиентский компьютер в регионе, подробный или же hello кластера.
- Проверьте, достигнуто ли внешнее регулирование. Например при хранилища azure настроенных toouse hello хранилища образов может регулирование передачи.

Проблема. Загрузка пакета завершена успешно, но время ожидания для выполнения команды [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) истекает. Попробуйте выполнить следующее.
- [Сжатие пакета hello](service-fabric-package-apps.md#compress-a-package) перед копированием toohello хранилища образов.
Hello Сжатие уменьшает размер hello и запускать hello число файлов, который в свою очередь, снижает объем трафика в hello и работать, Service Fabric. операции выгрузки Hello может требоваться (особенно при включении hello сжатия времени), однако скорости регистрации и отмены регистрации типа приложения hello.
- Задайте большее время ожидания для выполнения команды [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) с помощью параметра `TimeoutSec`.
- Задайте параметр `Async` для команды [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps). Команда Hello возвращает hello кластера принимает команды hello и hello регистрация типа приложения hello продолжается асинхронно. По этой причине нет нет необходимости toospecify большее значение времени ожидания в данном случае. Hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) команда выводит список всех версий типа успешно зарегистрированного приложения и состояние их регистрации. После завершения регистрации hello toodetermine этой команды можно использовать.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a>Развертывание пакета приложения с несколькими файлами
Проблема. Время ожидания для выполнения команды [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) истекает для пакета приложения с несколькими файлами (несколько тысяч).
Попробуйте выполнить следующее.
- [Сжатие пакета hello](service-fabric-package-apps.md#compress-a-package) перед копированием toohello хранилища образов. Hello Сжатие уменьшает число hello файлов.
- Задайте большее время ожидания для выполнения команды [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) с помощью параметра `TimeoutSec`.
- Задайте параметр `Async` для команды [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps). Команда Hello возвращает hello кластера принимает команды hello и hello регистрация типа приложения hello продолжается асинхронно.
По этой причине нет нет необходимости toospecify большее значение времени ожидания в данном случае. Hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) команда выводит список всех версий типа успешно зарегистрированного приложения и состояние их регистрации. После завершения регистрации hello toodetermine этой команды можно использовать.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a>Дальнейшие действия
[Обновление приложения Service Fabric](service-fabric-application-upgrade.md)

[Общие сведения о работоспособности Service Fabric](service-fabric-health-introduction.md)

[Диагностика и устранение неполадок службы Service Fabric](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Моделирование приложения в Service Fabric](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
