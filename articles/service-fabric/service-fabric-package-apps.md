---
title: "приложение Azure Service Fabric aaaPackage | Документы Microsoft"
description: "Как toopackage приложения перед развертыванием tooa кластера Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: b3918e1e25e532acdc9440855213e1fa364ea000
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="package-an-application"></a>Создание пакета приложения
В этой статье описывается как toopackage приложения Service Fabric и подготовить ее для развертывания.

## <a name="package-layout"></a>Макет пакета
манифест приложения Hello, один или несколько манифесты службы и другие необходимые пакеты, файлы могут быть организованы в определенном макете для развертывания в кластер Service Fabric. манифесты пример Hello в этой статье, потребуется toobe организованы в hello следующая структура каталогов:

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
```

Hello папки с именами toomatch hello **имя** атрибуты каждого элемента. Например, если hello манифест службы содержится два пакета кода с именами hello **MyCodeA** и **MyCodeB**, а затем две папки с одноименными будет содержать hello hello необходимые двоичные файлы для каждого кода пакет.

## <a name="use-setupentrypoint"></a>Использование SetupEntryPoint
Типичные сценарии использования **SetupEntryPoint** составляют случаи, когда требуется toorun исполняемый файл до запуска службы hello или требуется tooperform операции с повышенными привилегиями. Например:

* Настройка и инициализация переменных среды, которые hello исполняемый требованиям службы. Это не исполняемые файлы ограниченный tooonly записано с помощью модели программирования hello Service Fabric. Например, npm.exe нужны определенные переменные среды, настроенные для развертывания приложения node.js.
* Настройка контроля доступа посредством установки сертификатов безопасности.

Дополнительные сведения о том, как tooconfigure hello **SetupEntryPoint**, в разделе [настройки hello политики для точки входа установки службы](service-fabric-application-runas-security.md)

<a id="Package-App"></a>
## <a name="configure"></a>Настройка
### <a name="build-a-package-by-using-visual-studio"></a>Создание пакета с помощью Visual Studio
Если вы используете Visual Studio 2015 toocreate приложения, можно использовать hello пакета tooautomatically команда создания пакета, который соответствует hello макета, описанных выше.

toocreate пакета, щелкните правой кнопкой мыши проект приложения hello в обозревателе решений и выберите команду пакет hello, как показано ниже:

![Создание пакета приложения с помощью Visual Studio][vs-package-command]

После завершения упаковки hello расположение hello пакета можно найти в hello **вывода** окна. Привет упаковкой шаг выполняется автоматически при выполнении развертывания или отладки приложения в Visual Studio.

### <a name="build-a-package-by-command-line"></a>Создание пакета с помощью командной строки
Это также возможно tooprogrammatically пакета приложения с помощью `msbuild.exe`. Кулисами hello, Visual Studio выполняется его так же hello выходных данных.

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-hello-package"></a>Тестовый пакет hello
Структура пакета hello локально с помощью PowerShell можно проверить с помощью hello [ServiceFabricApplicationPackage тест](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) команды.
Эта команда проверит манифест на наличие ошибок при анализе, а также все ссылки. Эта команда проверяет только правильность структурных hello hello каталогов и файлов в пакете hello.
Он не проверяет любые hello кода или данных содержимое пакета после проверки того, что имеются все необходимые файлы.

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : hello EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

Эта ошибка показывает, что hello *MySetup.bat* файла, на который ссылается манифест службы hello **SetupEntryPoint** отсутствует пакет кода hello. После добавления отсутствующего файла hello проверки приложения hello проходит успешно:

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat

PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
True
PS D:\temp>
```

Если для приложения определены [параметры приложения](service-fabric-manage-multiple-environment-app-configuration.md), их можно передать в командлет [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) для полной проверки.

Если вы знаете hello кластера, где будут развертываться приложения hello, рекомендуется передать hello `ImageStoreConnectionString` параметра. В этом случае пакет hello также проверяется с использованием предыдущих версий приложения hello, которые уже запущены в кластере hello. Например, можно обнаружить проверки hello ли пакет с hello же версии, но различное содержимое уже был развернут.  

Как только приложение hello упакован должным образом и проходит проверку, оценки на основе размера hello и hello число файлов, при необходимости сжатия.

## <a name="compress-a-package"></a>Сжатие пакета
Если пакет содержит большое число файлов или имеет большой размер, можно выполнить сжатие пакета для более быстрого развертывания. Сжатие уменьшает число файлов и размер пакета hello hello.
Для пакета приложений сжатые [передача пакета приложения hello](service-fabric-deploy-remove-applications.md#upload-the-application-package) может занять больше по сравнению toouploading hello несжатый пакет (специально сжатия времени с учетом), но [регистрации](service-fabric-deploy-remove-applications.md#register-the-application-package) и [Отмена регистрации типа приложения hello](service-fabric-deploy-remove-applications.md#unregister-an-application-type) работают быстрее для пакета сжатых приложений.

механизм развертывания Hello же сжатые и несжатые пакетов. Если пакет hello сжаты, таким образом сохраняется в хранилище образов кластера hello и сжимаются на узле hello перед запуском приложения hello.
Сжатие Hello hello сжатая версия заменяет hello допустимый пакет Service Fabric. Папка Hello должны разрешать разрешения на запись. Если выполнить сжатие для уже сжатого пакета, никаких изменений не происходит.

Пакет можно сжать, выполнив команду Powershell hello [копирования ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) с `CompressPackage` переключения. Можно распаковать hello пакета с hello же с помощью `UncompressPackage` переключения.

Hello следующая команда сжимает hello пакета, не копируя его toohello хранилище образов. Можно скопировать tooone сжатый пакет или несколько кластеров Service Fabric, при необходимости, с помощью [копирования ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) без hello `SkipCopy` флаг.
Hello пакет теперь содержит ZIP-файл для hello `code`, `config`, и `data` пакетов. манифест приложения Hello и манифесты hello не ZIP-, так как они требуются для многих внутренних операций (например, пакет управления доступом приложения имя и версия извлечения типа для определенных проверок).
Архивировать манифесты hello сделает эти операции неэффективно.

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -CompressPackage -SkipCopy

PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
       ServiceManifest.xml
       MyCode.zip
       MyConfig.zip
       MyData.zip

```

Кроме того, можно сжимать и скопировать hello пакет с [ServiceFabricApplicationPackage копирования](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) за один шаг.
Если hello пакет имеет большой размер, укажите время tooallow достаточно высокое время ожидания для сжатия пакета hello и hello передачи toohello кластера.
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

На внутреннем уровне Service Fabric вычисляет контрольные суммы для hello пакетов приложений для проверки. При использовании сжатия, hello контрольные суммы вычисляются на hello ZIP-версии каждого пакета.
Если вы скопировали несжатую версию пакета приложения, и требуется toouse сжатия для hello того же пакета, необходимо изменить hello версий hello `code`, `config`, и `data` пакеты tooavoid ошибка контрольной суммы. Если пакеты hello не меняются, вместо изменения версии hello, можно использовать [подготовки diff](service-fabric-application-upgrade-advanced.md). Этот параметр, не включайте hello без изменения пакета вместо ссылок на него манифест службы hello.

Аналогичным образом Если вы отправили сжатая версия пакета hello и требуется toouse пакет без сжатия, необходимо обновить hello версии tooavoid hello ошибка контрольной суммы.

Hello пакет теперь упакованные правильно, проверяется и сжатые (при необходимости), поэтому она не готова для [развертывания](service-fabric-deploy-remove-applications.md) tooone или дополнительные Service Fabric кластерах.

### <a name="compress-packages-when-deploying-using-visual-studio"></a>Сжатие пакетов при развертывании с помощью Visual Studio
Пакеты toocompress Visual Studio для развертывания, можно настроить путем добавления hello `CopyPackageParameters` tooyour элемент профиль публикации, задайте hello `CompressPackage` атрибут слишком`true`.

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a>Дальнейшие действия
[Развертывание и удаление приложений] [ 10] описывает как экземпляры приложения toomanage toouse PowerShell

[Управление параметрами приложения для нескольких сред] [ 11] описывает способ tooconfigure параметров и переменных среды для экземпляров другого приложения.

[Настройка политик безопасности для приложения] [ 12] описывает, каким образом службы toorun toorestrict политики безопасности доступа.

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
