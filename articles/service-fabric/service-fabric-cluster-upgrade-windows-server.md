---
title: "aaaUpgrade автономного Azure Service Fabric кластера в Windows Server | Документы Microsoft"
description: "Обновление Azure Service Fabric кода hello и/или конфигурацию, которая запускает кластера Service Fabric автономный, включая настройку hello режим обновления кластера."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 5132795e544b6f0185accedbf5092dcaafd66df0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a>Обновление автономной службы Azure Service Fabric в кластере Windows Server
> [!div class="op_single_selector"]
> * [Кластер Azure](service-fabric-cluster-upgrade.md)
> * [Автономный кластер](service-fabric-cluster-upgrade-windows-server.md)
>
>

Для любой современной системе возможность tooupgrade hello — долгосрочный успех toohello ключа продукта. Кластер Azure Service Fabric — это ресурс, владельцем которого вы являетесь. Этой статье описывается, как сделать убедиться, что данный кластер hello всегда выполняется поддерживаемые версии кода структуры службы и конфигураций.

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a>Элемент управления hello Service Fabric версии, работающей в кластере
tooset Service Fabric, когда корпорация Майкрософт выпускает новую версию набора hello обновляет вашего кластера toodownload **fabricClusterAutoupgradeEnabled** tootrue конфигурации кластера. поддерживаемая версия Service Fabric, которые должны toobe вашего кластера на набор hello tooselect **fabricClusterAutoupgradeEnabled** toofalse конфигурации кластера.

> [!NOTE]
> Кластер должен всегда работать под управлением поддерживаемой версии Service Fabric. Когда корпорация Майкрософт объявляет о выпуске новой версии Service Fabric hello, предыдущей версии hello помечена для окончания поддержки после менее 60 дней с даты hello объявления «hello». Новые выпуски, объявляются [в блоге группы Service Fabric hello](https://blogs.msdn.microsoft.com/azureservicefabric/). Новый выпуск Hello — доступные toochoose на данный момент.
>
>

Новая версия toohello кластера можно обновить только в том случае, если вы используете стиль рабочей конфигурации узла, где каждый узел Service Fabric выделяется на отдельной физической или виртуальной машины. При наличии кластеру разработки, где более чем одним узлом Service Fabric — на отдельной физической или виртуальной машине, необходимо повторно создать кластер hello hello новой версии.

Последнюю версию toohello кластера или поддерживаемая версия Service Fabric, можно обновить два различных рабочих процессов. Кластеры с подключением toodownload hello последнюю версию автоматически — одного рабочего процесса. Hello другой рабочий процесс — для кластеров, у которых нет подключения к toodownload hello последнюю версию, Service Fabric.

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a>Обновление кластеров, которые имеют подключения toodownload hello последнюю кода и конфигурации
Использовать эти действия tooupgrade версии tooa поддерживается кластера, если узлы кластера подключен к Интернету слишком[http://download.microsoft.com](http://download.microsoft.com).

Кластеры с подключением слишком[http://download.microsoft.com](http://download.microsoft.com), корпорация Майкрософт периодически проверяет доступность hello новые версии Service Fabric.

Если доступна новая версия Service Fabric, hello пакет будет загружен локально toohello кластера и Подготовка к обновлению. Кроме того клиент hello tooinform этой новой версии, hello система выводит предупреждение работоспособности явную кластера, аналогичные toohello следующие:

«hello поддержка кластера версии [номер версии] заканчивается на [дата].»

После запуска кластера hello последнюю версию hello hello предупреждение исчезнет.

#### <a name="cluster-upgrade-workflow"></a>Рабочий процесс обновления кластера
После появления предупреждения работоспособности кластера hello hello следующие:

1. Подключите кластер toohello с любого компьютера, которая содержит компьютеры hello tooall доступа администратора, указываются в виде узлов в кластере hello. машина Hello, этот сценарий выполняется на имеет toobe частью кластера hello.

    ```powershell

    ###### connect toohello secure cluster using certs
    $ClusterName= "mysecurecluster.something.com:19000"
    $CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7FG2D630F8F3"
    Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
        -X509Credential `
        -ServerCertThumbprint $CertThumbprint  `
        -FindType FindByThumbprint `
        -FindValue $CertThumbprint `
        -StoreLocation CurrentUser `
        -StoreName My
    ```

2. Получите список hello Service Fabric версий, которые можно обновить до.

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    Вы должны получить аналогичные toothis выходные данные:

    ![Получение версий Service Fabric][getfabversions]
3. Запуска версии доступны обновления tooan кластера с помощью [ServiceFabricClusterUpgrade начала](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   toomonitor hello ход выполнения обновления hello, можно использовать обозреватель Service Fabric или выполнения hello следующую команду Windows PowerShell.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Если политики работоспособности кластера hello не выполняются, выполняется откат обновления hello. toospecify работоспособности пользовательских политик для hello **начала ServiceFabricClusterUpgrade** см. в разделе документации по [ServiceFabricClusterUpgrade начала](https://msdn.microsoft.com/library/mt125872.aspx).

После устранения проблемы hello, приводящие к отката hello инициировать попытку обновления hello, следующие hello же действия как описано выше.

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a>Обновление кластеров, которые имеют <U>без подключения к</u> toodownload hello последнюю кода и конфигурации
Использовать эти действия tooupgrade версии tooa поддерживается кластера, если узлы кластера не подключен к Интернету слишком[http://download.microsoft.com](http://download.microsoft.com).

> [!NOTE]
> При запуске кластера, не подключенной toohello Интернет имеется toolearn toomonitor hello Service Fabric team блог о новом выпуске. система Hello не содержит tooalert предупреждение работоспособности кластера вы нового выпуска.  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a>Автоматическая подготовка и подготовка вручную
Автоматическая загрузка tooenable и регистрацию для последней версии кода hello, настройте служба Service Fabric обновления. См. toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt внутри hello [изолированный пакет](service-fabric-cluster-standalone-package-contents.md) инструкции.
Для ручной процесс следуйте приведенным ниже инструкциям hello.

Измените следующие свойства toofalse, прежде чем начать обновление конфигурации вашей tooset hello кластера конфигурации.

        "fabricClusterAutoupgradeEnabled": false,

См. слишком[ServiceFabricClusterConfigurationUpgrade начала PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) сведения об использовании. Убедитесь, что tooupdate «clusterConfigurationVersion» в JSON перед началом обновления конфигурации hello.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a>Рабочий процесс обновления кластера

1. Запустите Get-ServiceFabricClusterUpgrade в одном из узлов hello в кластере hello и отметьте hello TargetCodeVersion.
2. Выполнения hello следующие данные из подключенного машина internet toolist все обновления совместимые версии с текущей версией hello и загрузите соответствующий пакет из ссылки для загрузки связанного hello hello.

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. Подключите кластер toohello с любого компьютера, которая содержит компьютеры hello tooall доступа администратора, указываются в виде узлов в кластере hello. Нет машины Hello, этот сценарий выполняется на toobe частью кластера hello

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. Скопируйте пакет hello загружаются в хранилище образов кластера hello.

5. Регистрация пакета копируются hello.

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. Запуска версии доступны обновления tooan кластера.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   Можно отслеживать ход выполнения обновления hello на Service Fabric Explorer hello, или можно выполнить следующую команду PowerShell hello.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Если политики работоспособности кластера hello не выполняются, выполняется откат обновления hello. toospecify работоспособности пользовательских политик для hello **начала ServiceFabricClusterUpgrade** см. в разделе документации hello [ServiceFabricClusterUpgrade начала](https://msdn.microsoft.com/library/mt125872.aspx).

После устранения проблемы hello, приводящие к отката hello инициировать попытку обновления hello, следующие hello же действия как описано выше.


## <a name="upgrade-hello-cluster-configuration"></a>Обновление конфигурации кластера hello
Прежде чем начать обновление конфигурации hello, путем выполнения сценария powershell hello в hello изолированный пакет можно проверить новый json конфигурации кластера.

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
или

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

Некоторые конфигурации невозможно обновить, например конечные точки, имена кластеров, IP-адреса узлов и т. д. Это тестирования hello нового кластера конфигурации json для старого hello и приводят к ошибкам в окне Powershell hello при наличии любые проблемы.

Обновление конфигурации кластера tooupgrade hello, запустите **ServiceFabricClusterConfigurationUpgrade начала**. Обработанные домен обновления, домен обновления — обновление конфигурации Hello.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a>Обновление конфигурации сертификата кластера  
Кластер сертификат используется для проверки подлинности между узлами кластера, поэтому перезапись сертификатов hello следует выполнять в внимательно из-за сбоя заблокирует hello связи между узлами кластера.  
Технически поддерживаются три варианта:  

1. Обновление одного сертификата: hello вариант предусматривает обновление "сертификат (основной) -> B сертификата (основной) -> C сертификата (основной) ->...".   
2. Double обновление сертификата: hello вариант предусматривает обновление "-> (основной) сертификата сертификата (основной) и B (дополнительный) -> B сертификата (основной) -> B сертификата (основной) и C (дополнительный) -> C сертификата (основной) ->...".
3. Тип обновления сертификатов: сертификат на основе отпечатка <-> сертификаты на основе конфигурации CommonName. Например, отпечаток сертификата A (основной) и отпечаток B (дополнительный) -> CommonName сертификата C.


## <a name="next-steps"></a>Дальнейшие действия
* Узнайте, как toocustomize некоторые [параметры кластера Service Fabric](service-fabric-cluster-fabric-settings.md).
* Узнайте, каким образом слишком[масштабирования кластера](service-fabric-cluster-scale-up-down.md).
* Узнайте об [обновлениях приложений](service-fabric-application-upgrade.md).

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
