---
title: "Обновление автономного кластера Azure Service Fabric в Windows Server | Документы Майкрософт"
description: "Обновление кода и (или) конфигурации Azure Service Fabric, под управлением которой работает автономный кластер Service Fabric, включая изменение режима обновления кластера."
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
ms.date: 10/15/2017
ms.author: dekapur
ms.openlocfilehash: c95c1827d0433dcb61eace34e7a905a5610c7781
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-cluster-on-windows-server"></a>Обновление автономного кластера Azure Service Fabric в Windows Server 
> [!div class="op_single_selector"]
> * [Кластер Azure](service-fabric-cluster-upgrade.md)
> * [Автономный кластер](service-fabric-cluster-upgrade-windows-server.md)
>
>

Для любой современной системы возможность обновления является ключом к успеху вашего продукта в долгосрочной перспективе. Кластер Azure Service Fabric — это ресурс, владельцем которого вы являетесь. В этой статье описывается, как настроить в кластере выполнение только поддерживаемых версий кода и конфигураций Service Fabric.

## <a name="control-the-service-fabric-version-that-runs-on-your-cluster"></a>Управление версией Service Fabric в кластере
Чтобы настроить кластер для скачивания обновлений Service Fabric после того, как корпорация Майкрософт выпускает новую версию, присвойте параметру кластера fabricClusterAutoupgradeEnabled значение *true*. Чтобы выбрать поддерживаемую версию Service Fabric для кластера, присвойте параметру кластера fabricClusterAutoupgradeEnabled значение *false*.

> [!NOTE]
> Кластер должен всегда работать под управлением поддерживаемой версии Service Fabric. Когда корпорация Майкрософт объявляет о выпуске новой версии Service Fabric, для предыдущей версии определяется срок завершения жизненного цикла. Этот срок составляет по меньшей мере 60 дней с даты объявления. О доступности новых выпусков сообщается в [блоге группы разработчиков Service Fabric](https://blogs.msdn.microsoft.com/azureservicefabric/), после чего вы можете их использовать.
>
>

Кластер можно обновить до новой версии, только если используется конфигурация узла с настройками рабочей среды, где каждый узел Service Fabric выделяется для отдельного физического или виртуального устройства. Если несколько узлов Service Fabric выполняется на отдельном физическом компьютере или виртуальной машине в кластере разработки, то нужно удалить такой кластер и создать его заново с использованием новой версии.

Обновить кластер до последней или поддерживаемой версии Service Fabric можно с помощью двух разных рабочих процессов. Один используется для кластеров с возможностью подключения для автоматического скачивания последней версии. Другой рабочий процесс используется для кластеров без возможности подключения для скачивания последней версии Service Fabric.

### <a name="upgrade-clusters-that-have-connectivity-to-download-the-latest-code-and-configuration"></a>Обновление кластеров с возможностью подключения для скачивания последней версии кода и конфигурации
Выполните приведенные ниже действия, чтобы обновить до поддерживаемой версии кластер с возможностью интернет-подключения к [Центру загрузки Майкрософт](http://download.microsoft.com).

Для кластеров с возможностью подключения к [Центру загрузки Майкрософт](http://download.microsoft.com) корпорация Майкрософт рекомендует периодически проверять наличие новых версий Service Fabric.

Когда выходит новая версия Service Fabric, пакет скачивается в кластер и начинается подготовка к обновлению. Наряду с информированием клиентов о доступности новой версии система выдает явное предупреждение о состоянии работоспособности кластера следующего содержания:

"Поддержка текущей версии кластера [номер версии] заканчивается [дата]".

После запуска последней версии кластера это предупреждение исчезнет.

#### <a name="cluster-upgrade-workflow"></a>Рабочий процесс обновления кластера
Как только вы увидите предупреждение о работоспособности кластера, сделайте следующее:

1. Подключитесь к кластеру с любой виртуальной машины, на которой есть доступ администратора ко всем ВМ, перечисленным в качестве узлов в файле конфигурации кластера. Компьютер, на котором выполняется этот скрипт, может и не входить в кластер.

    ```powershell

    ###### connect to the secure cluster using certs
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

2. Получите список версий Service Fabric, до которых можно выполнить обновление.

    ```powershell

    ###### Get the list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    Должен отобразиться результат следующего вида.

    ![Получение версий Service Fabric][getfabversions]
3. Запустите обновление кластера до доступной версии с помощью команды Windows PowerShell [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   За ходом обновления можно следить в Service Fabric Explorer. Также можно выполнить следующую команду PowerShell:

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Если требования политик работоспособности кластера не соблюдаются, выполняется откат обновления. О том, как указать пользовательские политики работоспособности для команды Start-ServiceFabricClusterUpgrade, можно узнать [из соответствующей документации](https://msdn.microsoft.com/library/mt125872.aspx).

Устранив проблемы, которые привели к откату, запустите обновление снова, выполнив уже описанные действия.

### <a name="upgrade-clusters-that-have-no-connectivity-to-download-the-latest-code-and-configuration"></a>Обновление кластеров *без возможности подключения* для скачивания последней версии кода и конфигурации
Выполните следующие действия, чтобы обновить до поддерживаемой версии кластер без возможности интернет-подключения к [Центру загрузки Майкрософт](http://download.microsoft.com).

> [!NOTE]
> Если вы используете кластер без возможности подключения к Интернету, вам потребуется отслеживать блог команды разработчиков Service Fabric, чтобы узнавать о новых выпусках. Система не будет показывать предупреждения о работоспособности кластера, чтобы оповещать вас о новых выпусках.  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a>Автоматическая подготовка и подготовка вручную
Чтобы включить автоматические операции скачивания и регистрации для получения последней версии кода, настройте службу обновления Service Fabric. Инструкции см. в файле Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt в [изолированном пакете](service-fabric-cluster-standalone-package-contents.md).
Для выполнения операций вручную сделайте следующее.

Прежде чем начать обновление конфигурации, измените конфигурацию кластера, присвоив следующему свойству значение *false*:

        "fabricClusterAutoupgradeEnabled": false,

См. дополнительные сведения об использовании [команды PowerShell Start-ServiceFabricClusterConfigurationUpgrade](https://msdn.microsoft.com/en-us/library/mt788302.aspx). Обязательно обновите параметр clusterConfigurationVersion в JSON, прежде чем запускать обновление конфигурации.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

```

#### <a name="cluster-upgrade-workflow"></a>Рабочий процесс обновления кластера

1. Выполните командлет Get-ServiceFabricClusterUpgrade на одном из узлов в кластере и запишите значение TargetCodeVersion.

2. Выполните следующую команду с компьютера, подключенного к Интернету, чтобы получить список всех версий, совместимых с обновлением, для текущей версии и скачайте соответствующий пакет с помощью связанных ссылок для загрузки.

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. Подключитесь к кластеру с любой виртуальной машины, на которой есть доступ администратора ко всем ВМ, перечисленным в качестве узлов в файле конфигурации кластера. Компьютер, на котором выполняется этот скрипт, может и не входить в кластер.

    ```powershell

   ###### Get the list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of the .cab file including the path to it> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. Скопируйте скачанный пакет в хранилище образов кластера.

5. Зарегистрируйте скопированный пакет.

    ```powershell

    ###### Get the list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of the .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. Запустите обновление кластера до доступной версии.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   За ходом обновления можно следить в Service Fabric Explorer. Можно также выполнить следующую команду PowerShell:

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Если требования политик работоспособности кластера не соблюдаются, выполняется откат обновления. О том, как указать пользовательские политики работоспособности для команды Start-ServiceFabricClusterUpgrade, можно узнать из [соответствующей документации](https://msdn.microsoft.com/library/mt125872.aspx).

Устранив проблемы, которые привели к откату, запустите обновление снова, выполнив уже описанные действия.


## <a name="upgrade-the-cluster-configuration"></a>Обновление конфигурации кластера
Прежде чем начинать обновление конфигурации, можно протестировать новый JSON-файл конфигурации кластера, выполнив следующий скрипт PowerShell в изолированном пакете:

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path to the new Configuration File> -OldClusterConfigFilePath <Path to the old Configuration File>

```
Также можно выполнить этот скрипт:

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path to the new Configuration File> -OldClusterConfigFilePath <Path to the old Configuration File> -FabricRuntimePackagePath <Path to the .cab file which you want to test the configuration against>

```

Некоторые конфигурации невозможно обновить, например конечные точки, имена кластеров, IP-адреса узлов и т. д. Мы протестируем новый JSON-файл конфигурации кластера, используя старый файл. При наличии каких-либо проблем в окне PowerShell отобразятся сведения об ошибках.

Чтобы обновить конфигурацию кластера, выполните команду Start-ServiceFabricClusterConfigurationUpgrade. Обновление конфигурации обрабатывает домен обновления.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

```

### <a name="cluster-certificate-config-upgrade"></a>Обновление конфигурации сертификата кластера  
Сертификат кластера используется для аутентификации между узлами кластера. Смену сертификата следует выполнять с особой осторожностью, так как в случае сбоя заблокируется связь между узлами кластера.

Технически поддерживаются четыре варианта:  

* Однократное обновление сертификата. Путь обновления: ''сертификат А (основной) -> сертификат B (основной) -> сертификат C (основной) ->…''.

* Двойное обновление сертификата. Путь обновления ''сертификат А (основной) -> сертификат А (основной) и В (дополнительный) -> сертификат В (основной) -> сертификат В (основной) и С (дополнительный) -> сертификат C (основной)->…''.

* Тип обновления сертификатов: сертификат на основе отпечатка <-> сертификаты на основе конфигурации CommonName. Например, отпечаток сертификата A (основной) и отпечаток B (дополнительный) -> CommonName сертификата C.

* Обновление отпечатка издателя сертификата. Путь обновления "общее имя сертификата — A, отпечаток издателя — IT1 (основной) > общее имя сертификата — A, отпечаток издателя — IT1, IT2 (основной) > общее имя сертификата — A, отпечаток издателя — IT2 (основной)".


## <a name="next-steps"></a>Дальнейшие действия
* Узнайте, как настроить некоторые [параметры кластера Service Fabric](service-fabric-cluster-fabric-settings.md).
* Ознакомьтесь с концепцией [масштабирования кластера](service-fabric-cluster-scale-up-down.md).
* Узнайте об [обновлениях приложений](service-fabric-application-upgrade.md).

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
