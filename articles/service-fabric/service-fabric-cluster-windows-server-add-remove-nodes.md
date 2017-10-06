---
title: "aaaAdd или удаление кластера Service Fabric узлы tooa автономный | Документы Microsoft"
description: "Узнайте, как tooadd или удалите tooan узлы Azure Service Fabric кластера на физическом компьютере или виртуальной машине под управлением Windows Server, которая может быть локальной или в любом облаке."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: dekapur
ms.openlocfilehash: 1da908ad9840faa052e0b4021bc2d4ce732b02bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a>Добавление или удаление узлов tooa автономный Service Fabric кластера под управлением Windows Server
После того как вы [кластер Service Fabric автономный создан на компьютерах Windows Server](service-fabric-cluster-creation-for-windows-server.md), могут изменяться вашим потребностям и может потребоваться tooadd или удаления узлов кластера tooyour. Эта статья содержит подробные инструкции tooachieve это. Обратите внимание, что добавление и удаление узлов в кластерах локальной разработки не поддерживается.

## <a name="add-nodes-tooyour-cluster"></a>Добавление узлов кластера tooyour
1. Hello подготовки виртуальной Машины или компьютер, tooadd tooyour кластера hello выполните действия, упомянутые в hello [hello Подготовка компьютеров для развертывания кластера компоненты hello toomeet](service-fabric-cluster-creation-for-windows-server.md) раздела
2. Определите, какой домен сбоя и домен обновления являются постоянной tooadd этой виртуальной Машины и машины
3. Удаленного рабочего стола (RDP) к hello виртуальной Машины или компьютер, что tooadd toohello кластера
4. Копирование или [загрузить hello изолированный пакет для структуры службы Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello ВМ/machine и распакуйте пакет hello
5. Запустите Powershell с повышенными привилегиями и перейдите в расположение toohello hello распакованную пакета
6. Запустите hello *AddNode.ps1* сценария с параметрами hello, описывающие новый узел tooadd hello. Приведенный ниже пример Hello добавляет новый узел с именем VM5, с типом NodeType0 и IP-адрес 182.17.34.52, UD1 и fd: / dc1/r0. Hello *ExistingClusterConnectionEndPoint* уже конечная точка подключения для узла в существующий кластер hello, которой может быть IP-адрес hello *любой* узла в кластере hello.

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    Когда сценарий hello завершает работу, можно проверить, добавлен ли hello новый узел, выполнив hello [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) командлета.

7. tooensure согласованности на разных узлах кластера hello, необходимо произвести обновление конфигурации. Запустите [Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello последний файл конфигурации и добавить hello вновь добавленный узел слишком раздел «Узлы». Также рекомендуется tooalways есть hello последняя конфигурация кластера в случае hello необходимые tooredploy кластер с hello одной конфигурации.

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. Запустите [ServiceFabricClusterConfigurationUpgrade начала](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello обновления.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    Можно отслеживать ход выполнения обновления hello на Service Fabric Explorer hello. Кроме того, с этой же целью можно выполнить команду [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps).

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a>Добавление tooclusters узлов, настроенного с использованием групповой управляемой учетной записи Windows
Для кластеров, настроенных с помощью групповой управляемой учетной записи службы (https://technet.microsoft.com/library/hh831782.aspx), можно добавить новый узел, используя обновление конфигурации.
1. Запустите [Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) на любом из существующих узлов hello tooget hello последний файл конфигурации и добавление сведений об о hello нового узла требуется tooadd раздела узлов «hello». Убедитесь, что новый узел hello входит в состав hello же группы управляемую учетную запись. Этой учетной записи нужно назначить роль "Администратор" на всех компьютерах.

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. Запустите [ServiceFabricClusterConfigurationUpgrade начала](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello обновления.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    Можно отслеживать ход выполнения обновления hello на Service Fabric Explorer hello. Кроме того, с этой же целью можно выполнить команду [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps).

### <a name="add-node-types-tooyour-cluster"></a>Добавление узла типы tooyour кластера
В заказ tooadd нового типа узлов, изменить вашей конфигурации tooinclude hello новый тип узла в разделе «NodeTypes» в разделе «Свойства» и начать настройку обновление с помощью [ServiceFabricClusterConfigurationUpgrade начала](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps). После завершения обновления hello, можно добавить новый кластер tooyour узлы с этим типом узла.

## <a name="remove-nodes-from-your-cluster"></a>Удаление узлов из кластера
Можно удалить узел из кластера с помощью обновления конфигурации в следующих способом hello:

1. Запустите [Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello последний файл конфигурации и *удалить* hello узел из раздела «Узлов».
Добавить hello «NodesToBeRemoved» параметр слишком «Setup» раздел в разделе «FabricSettings». Hello «value» должно быть разделенный запятыми список имен узлов, узлов, которые требуется удалить toobe.

    ```
         "fabricSettings": [
            {
            "name": "Setup",
            "parameters": [
                {
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
                },
                {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
                },
                {
                "name": "NodesToBeRemoved",
                "value": "vm0, vm1"
                }
            ]
            }
        ]
    ```
2. Запустите [ServiceFabricClusterConfigurationUpgrade начала](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello обновления.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    Можно отслеживать ход выполнения обновления hello на Service Fabric Explorer hello. Кроме того, с этой же целью можно выполнить команду [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps).

> [!NOTE]
> При удалении узлов может выполниться несколько обновлений. Некоторые узлы будут отмечены `IsSeedNode=”true”` тега и могут быть идентифицированы с помощью запроса к кластеру hello манифеста с помощью `Get-ServiceFabricClusterManifest`. Удаление таких узлов может потребоваться дольше, чем другие, поскольку узлы hello начальное значение будет иметь toobe перемещаются в таких сценариях. Hello кластера должен поддерживать как минимум 3 узлы типа первичного узла.
> 
> 

### <a name="remove-node-types-from-your-cluster"></a>Удаление типов узлов из кластера
Перед удалением типа узла, проверьте правильность, если все узлы, ссылающимся на тип узла hello. Удалите эти узлы перед удалением hello соответствующий тип узла. После удаления всех соответствующих узлов можно удалить hello NodeType из конфигурации кластера hello и начать настройку обновление с помощью [ServiceFabricClusterConfigurationUpgrade начала](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).


### <a name="replace-primary-nodes-of-your-cluster"></a>Замена основных узлов кластера
Hello замены основного узлов должно быть выполнено одного узла за другим, а не удалите и добавьте их в пакетах.


## <a name="next-steps"></a>Дальнейшие действия
* [Параметры конфигурации для автономного кластера Windows](service-fabric-cluster-manifest.md)
* [Защита автономного кластера под управлением Windows с помощью сертификатов](service-fabric-windows-cluster-x509-security.md)
* [Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server (Создание автономного кластера Service Fabric с тремя узлами на виртуальных машинах Azure под управлением Windows)](service-fabric-cluster-creation-with-windows-azure-vms.md)

