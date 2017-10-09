---
title: "aaaSet кластера Azure Service Fabric автономный | Документы Microsoft"
description: "Создание кластера автономный разработки с тремя узлами под управлением hello того же компьютера. После завершения этой установки, будет готов toocreate кластер с несколькими компьютерами."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/06/2017
ms.author: dekapur
ms.openlocfilehash: e4d0ea9fc3b8475160bd8ed19fd3716463791cc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a>Создание первого изолированного кластера Service Fabric
Можно создать автономный кластера Service Fabric на виртуальные машины или компьютеры под управлением Windows Server 2012 R2 или Windows Server 2016 в локальной среде или в облаке hello. Краткого руководства помогает toocreate кластера автономный разработки только через несколько минут.  Завершив работу с этим руководством, вы получите работающий на отдельном компьютере кластер с тремя узлами, в который вы можете развертывать приложения.

## <a name="before-you-begin"></a>Перед началом работы
Service Fabric предоставляет программу установки пакета toocreate Service Fabric изолированные кластеры.  [Скачайте пакет установки hello](http://go.microsoft.com/fwlink/?LinkId=730690).  Распакуйте hello установки tooa папку пакета в hello компьютер или виртуальную машину где вы настраиваете кластеру разработки hello.  подробно описаны Hello содержимое пакета установки hello [здесь](service-fabric-cluster-standalone-package-contents.md).

Администратор кластера Hello, развертыванию и настройке кластера hello требуются права администратора на компьютере hello. Пакет Service Fabric нельзя установить на контроллере домена.

## <a name="validate-hello-environment"></a>Проверка среды hello
Hello *TestConfiguration.ps1* сценарий в hello изолированный пакет используется в качестве наиболее toovalidate анализатора соответствия рекомендациям ли кластер может быть развернут в данной среде. [Подготовка к развертыванию](service-fabric-cluster-standalone-deployment-preparation.md) hello перечислены необходимые условия и требования к среде. Выполните сценарий tooverify hello при создании кластера hello разработки:

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-hello-cluster"></a>Создание кластера hello
Некоторые примеры файлов конфигурации кластера устанавливаются вместе с hello пакета установки. *ClusterConfig.Unsecure.DevCluster.json* — простая конфигурация кластера hello: небезопасным, трех узлов кластера, работающих на одном компьютере.  Другие файлы конфигурации описывают кластеры с одним или несколькими компьютерами, защищенными с помощью системы безопасности Windows или сертификатов X.509.  Не требуется toomodify ни один из параметров конфигурации по умолчанию hello в этом учебнике, но просмотрите файл конфигурации hello и ознакомиться с параметрами hello.  Hello **узлы** разделе описываются hello три узла в кластере hello: имя, IP-адрес [тип узла, домен сбоя и домен обновления](service-fabric-cluster-manifest.md#nodes-on-the-cluster).  Hello **свойства** раздел определяет hello [безопасности, уровень надежности, сбор диагностических сведений и типы узлов](service-fabric-cluster-manifest.md#cluster-properties) для hello кластера.

Этот кластер не защищен.  Любой пользователь может анонимно подключиться и выполнять операции управления, поэтому рабочие кластеры нужно обязательно защищать с помощью сертификатов X.509 или средств обеспечения безопасности Windows.  Во время создания кластера только настройки безопасности и не возможные tooenable безопасности после создания кластера hello.  Чтение [защиты кластера](service-fabric-cluster-security.md) toolearn Дополнительные сведения о безопасности кластера Service Fabric.  

toocreate hello разработки трех узлов кластера, запустите hello *CreateServiceFabricCluster.ps1* сценарий из сеанса PowerShell администратора:

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

пакет среды выполнения Service Fabric Hello автоматически загружаются и устанавливаются во время создания кластера.

## <a name="connect-toohello-cluster"></a>Подключите кластер toohello
Теперь кластер с тремя узлами работает. Hello модуля ServiceFabric PowerShell устанавливается вместе с hello среды выполнения.  Можно проверить этот кластер hello выполняется с hello же компьютере или на удаленном компьютере со средой выполнения Service Fabric hello.  Hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлет устанавливает toohello подключения кластера.   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
В разделе [кластера безопасное подключение tooa](service-fabric-connect-to-secure-cluster.md) другие примеры соединения tooa кластера. После подключения кластера toohello, используйте hello [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay командлет список узлов в hello сведения о кластере и состоянии для каждого узла. **Состояние работоспособности** каждого узла должно иметь значение *ОК*.

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-hello-cluster-using-service-fabric-explorer"></a>Визуализация hello кластера с помощью обозревателя Service Fabric
[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) — хорошее средство для визуализации кластера и управления приложениями.  Обозреватель Service Fabric — это служба, который работает в кластере hello, доступ к которому осуществляется с помощью браузера, перейдя по слишком[http://localhost:19080/обозреватель](http://localhost:19080/Explorer). 

панели мониторинга кластера Hello Обзор кластера, в том числе сводную приложения и состояние работоспособности узла. представление узла Hello отображает hello физическую структуру hello кластера. Для каждого узла можно просмотреть, какие приложения были развернуты на этом узле

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-hello-cluster"></a>Удаление кластера hello
tooremove кластера, запустите hello *RemoveServiceFabricCluster.ps1* сценарий PowerShell из папки пакета hello и передайте его в файл конфигурации JSON toohello путь hello. При необходимости можно указать расположение для журнала hello hello операции удаления.

```powershell
# Removes Service Fabric cluster nodes from each computer in hello configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

tooremove hello среда выполнения Service Fabric с компьютера hello, запустите следующий сценарий PowerShell из папки пакета hello hello.

```powershell
# Removes Service Fabric from hello current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда настраивается кластер автономный разработки, попробуйте hello в следующих статьях:
* [Настройте изолированный кластер с несколькими компьютерами](service-fabric-cluster-creation-for-windows-server.md) и включите режим безопасности.
* [Разверните приложения с помощью PowerShell](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png
