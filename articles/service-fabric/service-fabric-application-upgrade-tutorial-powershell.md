---
title: "обновление приложения Fabric aaaService с помощью PowerShell | Документы Microsoft"
description: "В этой статье рассматриваются возможности hello развертывания приложения Service Fabric, изменения кода hello и развертывание обновления с помощью PowerShell."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 9bc75748-96b0-49ca-8d8a-41fe08398f25
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: f31212264de45c3b257a0efafb75c10c279b989f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-using-powershell"></a>Обновление приложения Service Fabric с помощью PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
> * [Visual Studio](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

наиболее часто используемые Hello и обновления рекомендуется отслеживать hello последовательного обновления.  Azure Service Fabric отслеживает работоспособность hello приложения hello обновляется на основе набора политик работоспособности. После обновления домен обновления (UD) Service Fabric оценки работоспособности приложения hello и выполняется следующий домен обновления toohello либо происходит сбой обновления hello в зависимости от политик работоспособности hello.

Обновление наблюдаемые приложения выполняются с помощью hello управляемые или собственные интерфейсы API, PowerShell или REST. Инструкции по обновлению с помощью Visual Studio см. в статье [Руководство по обновлению приложений Service Fabric с помощью Visual Studio](service-fabric-application-upgrade-tutorial.md).

Мониторинг Service Fabric последовательное обновление администратор приложения hello позволяет настроить политики оценки работоспособности hello, что Service Fabric использует toodetermine, если приложение hello находится в работоспособном состоянии. Кроме того hello администратор может настроить toobe действие hello, выполняемое при сбое оценки работоспособности hello (например, выполнив к автоматическому откату.) В этом разделе рассматриваются отслеживаемых обновления для одного из образцов SDK hello, которые использует PowerShell. Hello следующее видео Microsoft Virtual Academy также поможет выполнить обновление приложения:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=OrHJH66yC_6406218965">
<img src="./media/service-fabric-application-upgrade-tutorial-powershell/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="step-1-build-and-deploy-hello-visual-objects-sample"></a>Шаг 1: Построение и развертывание образца hello визуальных объектов
Создавать и публиковать приложения hello, щелкнув правой кнопкой мыши проект приложения hello, **VisualObjectsApplication,** и выбрав hello **публикации** команды.  Дополнительные сведения см. в [руководстве по обновлению приложений Service Fabric](service-fabric-application-upgrade-tutorial.md).  Кроме того можно использовать PowerShell toodeploy приложения.

> [!NOTE]
> Прежде чем любые команды Service Fabric hello может использоваться в PowerShell, необходимо сначала tooconnect toohello кластера с помощью hello `Connect-ServiceFabricCluster` командлета. Аналогичным образом предполагается, что приветствия кластера уже настроена на локальном компьютере. См. в статье hello [Настройка среды разработки Service Fabric](service-fabric-get-started.md).
> 
> 

После построения проекта hello в Visual Studio, можно использовать команду PowerShell hello [ServiceFabricApplicationPackage копирования](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) toocopy hello приложения пакета toohello ImageStore. Пакет приложения hello tooverify локально, используйте hello [ServiceFabricApplicationPackage тест](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) командлета. Hello следующим шагом является tooregister hello toohello Service Fabric среда выполнения приложения с помощью hello [ServiceFabricApplicationPackage регистра](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) командлета. Hello последний шаг — toostart экземпляр приложения hello с помощью hello [New ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) командлета.  Эти три шага, hello аналогом toousing **развернуть** пункта меню в Visual Studio.

Теперь вы можете использовать [Service Fabric Explorer tooview hello кластера и hello приложения](service-fabric-visualizing-your-cluster.md). Hello приложение имеет веб-службу, которая может быть навигацию tooin Internet Explorer, введя [http://localhost: 8081/visualobjects](http://localhost:8081/visualobjects) в адресную строку hello.  Вы увидите некоторые плавающей визуальных объектов перемещения на экране приветствия.  Кроме того, можно использовать [Get ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) toocheck состояние приложения hello.

## <a name="step-2-update-hello-visual-objects-sample"></a>Шаг 2: Обновление визуальных объектов образец hello
Можно заметить, что с версией hello, которое было развернуто на шаге 1, hello визуальных объектов не поворачиваются. Давайте обновление tooone этого приложения, где также вращать hello визуальных объектов.

Выберите проект VisualObjects.ActorService hello в hello VisualObjects решения и откройте файл StatefulVisualObjectActor.cs hello. Переход в этот файл метод toohello `MoveObject`, закомментируйте `this.State.Move()`и раскомментируйте `this.State.Move(true)`. Это изменение поворачивает hello объекты после обновления службы hello.

Также нужны tooupdate hello *ServiceManifest.xml* файлу (в PackageRoot) для проекта hello **VisualObjects.ActorService**. Обновление hello *CodePackage* hello too2.0 версии службы и hello соответствующие строки в hello *ServiceManifest.xml* файла.
Hello Visual Studio можно использовать *редактирование файлов манифеста* параметр после правой кнопкой мыши на изменения в файле манифеста hello toomake hello решения.

После внесения изменений hello, hello манифест должен выглядеть hello следующим образом (выделенные фрагменты Показать изменения hello):

```xml
<ServiceManifestName="VisualObjects.ActorService" Version="2.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

<CodePackageName="Code" Version="2.0">
```

Теперь hello *ApplicationManifest.xml* файла (вложенной hello **VisualObjects** проекта под hello **VisualObjects** решения) — обновленных tooversion 2.0 hello  **VisualObjects.ActorService** проекта. Кроме того версия приложения hello-обновленные too2.0.0.0 с 1.0.0.0. Hello *ApplicationManifest.xml* следует выглядят hello следующий фрагмент кода:

```xml
<ApplicationManifestxmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="VisualObjects" ApplicationTypeVersion="2.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

 <ServiceManifestRefServiceManifestName="VisualObjects.ActorService" ServiceManifestVersion="2.0" />
```


Теперь построения проекта hello, выбрав только hello **ActorService** проект, щелкнув правой кнопкой мыши и выбрав hello **построения** в Visual Studio. При выборе **перестроить все**, необходимо обновить hello версий для всех проектов, так как код hello изменились. Далее, давайте hello пакета обновленное приложение, щелкнув правой кнопкой мыши ***VisualObjectsApplication***, выбрав hello службы структуры меню и выбрав **пакета**. При этом должен создаться пакет приложения, пригодный для развертывания.  Обновленные приложения в случае готовности toobe развертывания.

## <a name="step-3--decide-on-health-policies-and-upgrade-parameters"></a>Шаг 3. Определение политик работоспособности и параметров обновления
Ознакомьтесь с hello [параметров обновления приложения](service-fabric-application-upgrade-parameters.md) и hello [процесс обновления](service-fabric-application-upgrade.md) tooget хорошо понимать различных обновить параметры, значения времени ожидания и применяется критерий работоспособности hello . В этом пошаговом руководстве критерий оценки работоспособности службы hello toohello по умолчанию (и не рекомендуется) значения, которые означает, что все службы и экземпляры должны быть *работоспособное* после обновления hello.  

Тем не менее, давайте увеличить hello *HealthCheckStableDuration* too60 секунд (что hello службы находятся в работоспособном состоянии, по крайней мере 20 секунд до toohello происходит обновление hello Далее измените домена).  Давайте также задать hello *UpgradeDomainTimeout* toobe 1200 секунд и hello *UpgradeTimeout* toobe 3000 секунд.

Наконец, давайте также задать hello *UpgradeFailureAction* toorollback. Этот параметр требует Service Fabric tooroll назад hello приложения toohello предыдущей версии, при обнаружении проблем во время обновления hello. Таким образом при запуске обновления hello (на шаге 4), hello заданы следующие параметры являются:

FailureAction = Rollback

HealthCheckStableDurationSec = 60

UpgradeDomainTimeoutSec = 1200

UpgradeTimeout = 3000

## <a name="step-4-prepare-application-for-upgrade"></a>Шаг 4. Подготовка приложения к обновлению
Теперь приложение hello создается и готов toobe обновлена. Если открыть окно PowerShell с правами администратора и ввести команду [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), в нем отобразится информация о том, что вы развернули приложение типа **VisualObjects** версии 1.0.0.0.  

Hello пакета приложения хранится в следующих hello относительный путь, где распакованные hello Service Fabric SDK - *Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug*. В этом каталоге, где хранится пакет приложения hello следует найти папку «Пакет». Проверьте tooensure hello отметки времени, что это последнюю сборку hello (возможно, потребуется соответствующим образом, а также пути hello toomodify).

Теперь давайте hello копирования обновление пакета приложения toohello ImageStore структуры службы (места хранения пакетов приложения hello, Service Fabric). Здравствуйте, параметр *ApplicationPackagePathInImageStore* информирует о том, где можно найти пакет приложения hello Service Fabric. Мы поместили приложения hello обновлен «VisualObjects\_V2» с hello следующую команду (возможно, потребуется пути toomodify снова соответствующим образом).

```powershell
Copy-ServiceFabricApplicationPackage  -ApplicationPackagePath .\Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug\Package
-ImageStoreConnectionString fabric:ImageStore   -ApplicationPackagePathInImageStore "VisualObjects\_V2"
```

Hello следующим шагом является приложение, используя Service Fabric, которое может выполняться hello tooregister [ServiceFabricApplicationType регистра](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) команды:

```powershell
Register-ServiceFabricApplicationType -ApplicationPathInImageStore "VisualObjects\_V2"
```

Если hello предыдущая команда не работает, скорее всего, необходимо повторное построение всех служб. Как указано в шаге 2, может иметь tooupdate вашей версии веб-службы.

## <a name="step-5-start-hello-application-upgrade"></a>Шаг 5: Запуск обновления приложения hello
Теперь мы все приложения hello toostart набор обновления с помощью hello [ServiceFabricApplicationUpgrade начала](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) команды:

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/VisualObjects -ApplicationTypeVersion 2.0.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000   -FailureAction Rollback -Monitored
```


Hello имя приложения hello же, как оно было описано в hello *ApplicationManifest.xml* файла. Service Fabric использует это имя tooidentify, какое приложение обновляется начало. Если задать слишком короткий toobe тайм-ауты hello, может появиться сообщение об ошибке, состояния hello проблему. См. toohello при устранении неполадок или увеличить тайм-ауты hello.

Теперь, как hello продолжается обновления приложения, вы можете отслеживать ее с помощью Service Fabric Explorer или с помощью hello [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) команду PowerShell: 

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/VisualObjects
```

Через несколько минут, состояние hello, полученный с помощью hello, предшествующий команду PowerShell должна выглядеть следующим образом, все домены обновления были обновлены («завершено»). И вы должны найти что запустили поворот hello визуальных объектов в окне обозревателя!

Обновление с версии 2 tooversion 3 или с версии 2 tooversion 1 в качестве упражнения можно попробовать. Переход с версии 2 tooversion 1 также считается обновления. Работать с тайм-аутов и toomake политики работоспособности самостоятельно ознакомиться с ними. При развертывании кластера Azure tooan hello набор toobe необходимость параметры соответствующим образом. Это хороший tooset hello тайм-ауты достаточно экономно.

## <a name="next-steps"></a>Дальнейшие действия
[Руководство по обновлению приложений Service Fabric с помощью Visual Studio](service-fabric-application-upgrade-tutorial.md) поможет вам выполнить поэтапное обновление приложения с помощью Visual Studio.

Управление обновлениями приложения осуществляется с помощью [параметров обновления](service-fabric-application-upgrade-parameters.md).

Обеспечить совместимость на обновление приложения путем изучения как toouse [сериализации данных](service-fabric-application-upgrade-data-serialization.md).

Узнайте, как toouse расширенные функции при обновлении приложения с помощью ссылки слишком[дополнительные разделы](service-fabric-application-upgrade-advanced.md).

Исправьте распространенных проблем в обновлений приложений с помощью ссылки действия toohello в [Устранение неполадок обновлений приложений](service-fabric-application-upgrade-troubleshooting.md).

