---
title: "aaaCreate кластера Azure Service Fabric автономный | Документы Microsoft"
description: "Создание кластера Azure Service Fabric на любом компьютере (физическом сервере или виртуальной машине) под управлением Windows Server, расположенном в локальной системе или любом облаке."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 31349169-de19-4be6-8742-ca20ac41eb9e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik;dekapur
ms.openlocfilehash: 444970816290a0448d88a8b2082c75eb7a64cb44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a>Создание изолированного кластера под управлением Windows Server
Azure Service Fabric toocreate структуры службы кластеров можно использовать на любой виртуальной машины или компьютеры под управлением Windows Server. Это означает, что вы сможете разворачивать и запускать приложения Service Fabric в любой среде с набором подключенных друг к другу компьютеров с Windows Server как в локальной среде, так и у любого поставщика облачных служб. Предоставляет Service Fabric toocreate пакета установки, кластеров Service Fabric вызывается hello изолированный пакет Windows Server.

В этой статье содержится описание этапов hello для создания автономного кластера Service Fabric.

> [!NOTE]
> Этот изолированный пакет Windows Server сейчас доступен на коммерческой основе и может использоваться для рабочих развертываний. Этот пакет может содержать новые функции Service Fabric, которые находятся на этапе предварительной версии. Прокрутите вниз слишком»[Предварительный просмотр компонентов, включенных в этот пакет](#previewfeatures_anchor).» раздел для списка hello hello функции предварительной версии. Вы можете [загрузить копию hello лицензионное соглашение](http://go.microsoft.com/fwlink/?LinkID=733084) сейчас.
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-hello-service-fabric-for-windows-server-package"></a>Получение поддержки для hello пакет Service Fabric для Windows Server
* Попросите hello сообщества о изолированный пакет Service Fabric hello для Windows Server hello [форум Azure Service Fabric](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).
* Откройте запрос на [техническую поддержку для Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).  Узнайте больше о [профессиональной технической поддержке Майкрософт](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).
* Поддержка для этого пакета также доступна в рамках [поддержки Microsoft Premier](https://support.microsoft.com/en-us/premier).
* Дополнительные сведения см. в разделе [Варианты поддержки Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).
* toocollect журналы в целях поддержки запуска hello [сборщик журналов автономной службы структуры](service-fabric-cluster-standalone-package-contents.md).

<a id="downloadpackage"></a>

## <a name="download-hello-service-fabric-for-windows-server-package"></a>Загрузить пакет Service Fabric для Windows Server hello
кластер toocreate hello, используйте пакет Service Fabric для Windows Server hello (Windows Server 2012 R2 и более поздних) по следующему адресу: <br>
[Ссылка для скачивания изолированного пакета Service Fabric для Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)

Найти подробные сведения о содержимом пакета hello [здесь](service-fabric-cluster-standalone-package-contents.md).

пакет среды выполнения Service Fabric Hello автоматически загружаются во время создания кластера. Если развертывание с компьютера не подключен toohello Интернет, загрузите пакет среды выполнения hello аппаратного здесь: <br>
[Ссылка для скачивания среды выполнения Service Fabric для Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)

Примеры конфигурации изолированного кластера доступны здесь: <br>
[Примеры конфигурации изолированного кластера](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

<a id="createcluster"></a>

## <a name="create-hello-cluster"></a>Создание кластера hello
Service Fabric может быть развернутой tooa кластеру разработки один компьютер с помощью hello *ClusterConfig.Unsecure.DevCluster.json* файл, включенный в [образцы](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).

Распакуйте пакет tooyour hello автономную машину, копировать hello образец конфигурации файла toohello локального компьютера, а затем выполнения hello *CreateServiceFabricCluster.ps1* скрипта через сеанс администратора PowerShell из автономной системы hello папка пакета:
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a>Шаг 1А. Создание незащищенного локального кластера разработки
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

. В разделе hello раздел установки среды [планирование и Подготовка развертывания кластера](service-fabric-cluster-standalone-deployment-preparation.md) для устранения неполадок сведения.

Если завершения выполнения сценариев разработки можно удалить кластер Service Fabric hello hello машины с помощью ссылки toosteps в разделе «[удаления кластера](#removecluster_anchor)». 

### <a name="step-1b-create-a-multi-machine-cluster"></a>Шаг 1Б. Создание кластера с несколькими компьютерами
После планирования hello проверены и действия по подготовке подробно описаны на странице приветствия приведенную ниже ссылку, вы готовы toocreate производственного кластера с использованием файла конфигурации кластера. <br>
[Планирование и подготовка развертывания кластера](service-fabric-cluster-standalone-deployment-preparation.md)

1. Проверить файл конфигурации hello написания, запустив hello *TestConfiguration.ps1* скрипта из папки пакета автономный hello:  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    Вы должны увидеть результат следующего вида. Если hello нижнего поля «Выполнено» возвращается как «True», проверок работоспособности и кластера hello выглядит toobe развертываемых на основе конфигурации ввода hello.

    ```
    Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
    Running Best Practices Analyzer...
    Best Practices Analyzer completed successfully.
    
    LocalAdminPrivilege        : True
    IsJsonValid                : True
    IsCabValid                 : True
    RequiredPortsOpen          : True
    RemoteRegistryAvailable    : True
    FirewallAvailable          : True
    RpcCheckPassed             : True
    NoConflictingInstallations : True
    FabricInstallable          : True
    Passed                     : True
    ```

2. Создание кластера hello: запустите hello *CreateServiceFabricCluster.ps1* кластера Service Fabric hello toodeploy скрипт на каждой машине в конфигурации hello. 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> Развертывание трассировки записываются toohello ВМ/machine запуска сценария CreateServiceFabricCluster.ps1 PowerShell hello. Они находятся во вложенной папке hello DeploymentTraces, на основе в каталоге hello, из которого hello запуска сценария. toosee Если Service Fabric был развернут правильно tooa машины, найти hello установлены файлы в каталоге FabricDataRoot hello, как описано в файле конфигурации кластера hello раздел FabricSettings (по умолчанию c:\ProgramData\SF). Кроме того, процессы FabricHost.exe и Fabric.exe должны отображаться в диспетчере задач.
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a>Шаг 1в. Создание кластера в автономном состоянии (не подключенного к Интернету)
пакет среды выполнения Service Fabric Hello автоматически загружаются при создании кластера. При развертывании toomachines кластера не подключения toohello Интернета, необходимо будет toodownload hello Service Fabric среды выполнения пакета отдельно и предоставить tooit путь hello в момент создания кластера.
Hello пакета среды выполнения может быть загружен отдельно, с другого компьютера подключен toohello Интернета, в [ссылку Загрузить - среда выполнения Service Fabric - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354). Скопируйте hello среды выполнения пакета toowhere вы развертываете hello вне сети кластера из и создание кластера hello, запустив `CreateServiceFabricCluster.ps1` с hello `-FabricRuntimePackagePath` параметр включен, как показано ниже: 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
где `.\ClusterConfig.json` и `.\MicrosoftAzureServiceFabric.cab` соответственно, конфигурация кластера toohello пути hello и hello среды выполнения CAB-файл.


### <a name="step-2-connect-toohello-cluster"></a>Шаг 2: Подключение toohello кластера
tooconnect tooa безопасного кластера, в разделе [Service fabric подключения кластера toosecure](service-fabric-connect-to-secure-cluster.md).

небезопасные кластер tooan tooconnect, запустите следующую команду PowerShell hello:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
Пример:
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a>Шаг 3. Вызов Service Fabric Explorer
Теперь можно подключиться, используя обозреватель Service Fabric либо непосредственно из одной из машин hello http://localhost:19080/Explorer/index.html или удаленно с http://< toohello кластера*IPAddressofaMachine*>: 19080 / Explorer/index.HTML.

## <a name="add-and-remove-nodes"></a>Добавление и удаление узлов
Можно добавить или удалить кластер Service Fabric автономные узлы tooyour при изменении потребностей вашего бизнеса. В разделе [добавления или удаления узлов tooa Service Fabric автономный кластера](service-fabric-cluster-windows-server-add-remove-nodes.md) подробное описание шагов.

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a>Удаление кластера
tooremove кластера, запустите hello *RemoveServiceFabricCluster.ps1* сценарий PowerShell из папки пакета hello и передайте его в файл конфигурации JSON toohello путь hello. При необходимости можно указать расположение для журнала hello hello операции удаления.

Этот сценарий может выполняться на любом компьютере с установленными машины hello tooall доступа администратора, перечисленных в файле конфигурации кластера hello как узлы. машина Hello, этот сценарий выполняется на имеет toobe частью кластера hello.

```
# Removes Service Fabric from each machine in hello configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from hello current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-tooopt-out-of-it"></a>Собираемые данные телеметрии и как tooopt вне его
По умолчанию hello продукта собирает данные телеметрии на hello Service Fabric использования tooimprove hello продукта. Hello анализатора соответствия рекомендациям, работает как часть установки hello проверяет возможность подключения к слишком[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1). Если не удается добиться hello программа установки завершается ошибкой, если отказаться телеметрии.

1. Hello конвейера телеметрии предпринимает следующие данные слишком hello tooupload[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) один раз в день. Передача усилия и никак не повлияет на функциональные возможности кластера hello. Данные телеметрии Hello отправляется только из узла "hello" hello, запускается основной диспетчера отработки отказа. С других узлов данные телеметрии не отправляются.
2. Hello телеметрии состоит из следующих hello.

* количество служб;
* количество типов служб;
* количество приложений;
* количество обновлений приложений;
* количество единиц с отработкой отказа;
* количество единиц со встроенной отработкой отказа;
* количество единиц с неработоспособной отработкой отказа;
* количество реплик;
* количество встроенных реплик;
* количество реплик в режиме ожидания;
* количество автономных реплик;
* длина общей очереди;
* длина очереди запросов;
* длина очереди единиц с отработкой отказа;
* длина очереди фиксаций;
* количество узлов;
* выполнен ли контекст: значение True или False;
* идентификатор кластера — это глобальный уникальный идентификатор, который случайным образом формируется для каждого кластера;
* версия Service Fabric;
* IP-адрес hello виртуальных машин и машин, из какой hello загружается телеметрии

телеметрии toodisable добавьте hello следующие слишком*свойства* в файле config кластера: *enableTelemetry: false*.

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a>Возможности на этапе предварительной версии в этом пакете
Отсутствует.


> [!NOTE]
> Начиная с нового hello [Общедоступной версии hello автономный кластера для Windows Server (версия 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), выпуски toofuture кластера, можно обновить вручную или автоматически. См. слишком[обновление кластера Service Fabric автономная версия](service-fabric-cluster-upgrade-windows-server.md) сведения.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
* [Развертывание и удаление приложений с помощью PowerShell](service-fabric-deploy-remove-applications.md)
* [Параметры конфигурации для автономного кластера Windows](service-fabric-cluster-manifest.md)
* [Добавление или удаление кластера Service Fabric автономные узлы tooa](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) (Обновление версии изолированного кластера Service Fabric)
* [Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server (Создание автономного кластера Service Fabric с тремя узлами на виртуальных машинах Azure под управлением Windows)](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [Защита автономного кластера под управлением Windows с помощью системы безопасности Windows](service-fabric-windows-cluster-windows-security.md)
* [Защита автономного кластера под управлением Windows с помощью сертификатов](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
