---
title: "aaaCreate отдельный кластер с виртуальными машинами Azure под управлением Windows | Документы Microsoft"
description: "Узнайте, как toocreate кластеру Azure Service Fabric на виртуальных машинах Azure под управлением Windows Server и управлять им."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: ryanwi;chackdan
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: 8900204fe69887a7a0ca54b06e0d32534421bcfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a>Создание автономного кластера Service Fabric с тремя узлами на базе виртуальных машин Azure под управлением Windows Server
В этой статье описывается, как toocreate a кластера на основе Windows Azure виртуальных машин (ВМ) с помощью hello автономный установщик Service Fabric для Windows Server. Hello сценария является особым случаем [Создание и управление ими в кластере под управлением Windows Server](service-fabric-cluster-creation-for-windows-server.md) которых виртуальные машины hello [виртуальные машины Azure под управлением Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), однако вы не создаете [Azure облачный кластер Service Fabric](service-fabric-cluster-creation-via-portal.md). различие Hello в следующих этот шаблон является этого кластера Service Fabric автономный hello созданные hello следующие шаги полностью управляется вами, тогда как hello фабрике Azure облачной службы кластеров, управляемых и обновляются по hello Service Fabric поставщик ресурсов.

## <a name="steps-toocreate-hello-standalone-cluster"></a>Hello автономного действия toocreate кластера
1. Войдите в портал Azure toohello и создания новой виртуальной Машины центра обработки данных Windows Server 2016 или Windows Server 2012 R2 Datacenter в группе ресурсов. Прочитать статью hello [создания ВМ Windows на портал Azure hello](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) для получения дополнительных сведений.
2. Добавьте пару дополнительные виртуальные машины toohello одну группу ресурсов. Убедитесь в каждой из виртуальных машин hello имеет hello же имя пользователя администратора и пароль при создании. После создания вы увидите все три виртуальные машины в hello одной виртуальной сети.
3. Подключение tooeach из hello виртуальных машин и отключение брандмауэра Windows с помощью hello hello [диспетчера сервера, локального сервера мониторинга](https://technet.microsoft.com/library/jj134147.aspx). Это гарантирует, что hello сетевой трафик может обмениваться данными между компьютерами hello. При машины подключенных tooeach получить hello IP-адрес, откройте командную строку и введите `ipconfig`. Также можно увидеть hello IP адрес каждого компьютера, на портале hello, выбрав hello ресурсов виртуальной сети для группы ресурсов hello и проверка hello сетевых интерфейсов, созданных для каждого из этих компьютеров.
4. Подключите tooone из hello виртуальных машин и тест, который можно проверить связь hello другие две виртуальных машины успешно.
5. Подключение tooone из hello виртуальных машин и [загрузить hello изолированный пакет Service Fabric для Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) в новую папку на hello машинные и извлеките hello.
6. Откройте hello *ClusterConfig.Unsecure.MultiMachine.json* в Блокноте и изменить каждый узел с IP-адресами hello трех машин hello. Изменение имени кластера hello вверху hello и сохраните файл hello.  Ниже показан частичного пример hello манифеста кластера.
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. Если необходимо реализовать этот toobe безопасного кластера, решить hello меры безопасности, необходимо будет toouse и выполнить инструкции раздела hello hello связанные ссылки: [сертификатов X509](service-fabric-windows-cluster-x509-security.md) или [безопасности Windows](service-fabric-windows-cluster-windows-security.md). Если установка hello кластера с помощью средств безопасности Windows, необходимо будет tooset копирование toomanage контроллера домена Active Directory. Обратите внимание, что использование компьютера контроллера домена в качестве узла Service Fabric не поддерживается.
8. Откройте окно [PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise). Перейдите в папку toohello, где извлечены hello загруженный автономный установщик пакет и сохранить файл конфигурации кластера hello. Выполните hello, следуя кластера hello toodeploy команды PowerShell:
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

Hello скрипта удаленно настраивает кластер Service Fabric hello и следует сообщать о ходе выполнения как развертывания выполняет накат до.

9. После около минуты, можно проверить, если hello кластер является работоспособным, подключившись toohello Service Fabric Explorer с помощью одного компьютера hello IP-адресов, например с помощью `http://10.1.0.5:19080/Explorer/index.html`. 

## <a name="next-steps"></a>Дальнейшие действия
* [Создание автономных кластеров Service Fabric в Windows Server или Linux](service-fabric-deploy-anywhere.md)
* [Добавление или удаление кластера Service Fabric автономные узлы tooa](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [Параметры конфигурации для автономного кластера Windows](service-fabric-cluster-manifest.md)
* [Защита автономного кластера под управлением Windows с помощью системы безопасности Windows](service-fabric-windows-cluster-windows-security.md)
* [Защита автономного кластера под управлением Windows с помощью сертификатов](service-fabric-windows-cluster-x509-security.md)

