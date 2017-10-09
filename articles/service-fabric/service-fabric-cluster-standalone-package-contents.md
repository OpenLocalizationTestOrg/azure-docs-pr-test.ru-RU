---
title: "aaaAzure автономный пакет Service Fabric для Windows Server | Документы Microsoft"
description: "Описание и содержимое hello Azure Service Fabric автономного пакета для Windows Server."
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik
ms.openlocfilehash: e4c6cb9128d659144e559fcad06bb78c9969dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="contents-of-service-fabric-standalone-package-for-windows-server"></a>Содержимое изолированного пакета Service Fabric для Windows Server
В hello [загрузки](http://go.microsoft.com/fwlink/?LinkId=730690) Service Fabric изолированный пакет, вы найдете hello следующие файлы:

| **Имя файла** | **Краткое описание** |
| --- | --- |
| CreateServiceFabricCluster.ps1 |Скрипт PowerShell, который создает hello кластера с использованием параметров hello в ClusterConfig.json. |
| RemoveServiceFabricCluster.ps1 |Сценарий PowerShell, который удаляет в кластер, использующий параметры hello в ClusterConfig.json. |
| AddNode.ps1 |Сценарий PowerShell для добавления в узел tooan существующие развертывания кластера на текущем компьютере hello. |
| RemoveNode.ps1 |Сценарий PowerShell для удаления узла из существующего развертывания кластера из hello текущего компьютера. |
| CleanFabric.ps1 |Сценарий PowerShell для очистки автономной установки Service Fabric off hello текущего компьютера. Предыдущие установки MSI должны быть удалены с помощью собственной связанной программы удаления. |
| TestConfiguration.ps1 |Сценарий PowerShell для анализа hello инфраструктуры, как указано в hello Cluster.json. |
| DownloadServiceFabricRuntimePackage.ps1 |Сценарий PowerShell, используемого для загрузки hello последнюю версию среды выполнения пакета за пределами диапазона, в сценариях, где не hello развертывании машины с подключением toohello Интернета. |
| DeploymentComponentsAutoextractor.exe |Самораспаковывающийся архив, содержащий компоненты развертывания используется hello сценарии автономного пакета. |
| EULA_ENU.txt |Hello условия лицензионного соглашения для hello используйте Microsoft Azure Service Fabric автономного пакета Windows Server. Вы можете [загрузить копию hello лицензионное соглашение](http://go.microsoft.com/fwlink/?LinkID=733084) сейчас. |
| Readme.txt |Toohello ссылку заметки о выпуске и основные инструкции по установке. Это подмножество hello инструкции в этом документе. |
| ThirdPartyNotice.rtf |Уведомления о сторонних разработчиков программного обеспечения в пакете hello. |
| Tools\Microsoft.Azure.ServiceFabric.WindowsServer.SupportPackage.zip |При запуске в трассировке toocollect и передачи запросу StandaloneLogCollector.exe регистрирует tooMicrosoft в целях поддержки. |
| Tools\ServiceFabricUpdateService.zip |Это средство используется tooenable автоматическое обновление кода для кластеров, в которых нет доступа к Интернету. Дополнительные сведения см. [здесь](service-fabric-cluster-upgrade-windows-server.md).|

**Шаблоны** 
| **Имя файла** | **Краткое описание** |
| --- | --- |
| ClusterConfig.Unsecure.DevCluster.json |Файл образца конфигурации кластера, содержащий параметры hello небезопасном, тремя узлами одним компьютером (или виртуальных машин) разработки кластера, включая hello сведения для каждого узла в кластере hello. |
| ClusterConfig.Unsecure.MultiMachine.json |Файл образца конфигурации кластера, содержащий параметры hello кластера защищена, несколькими компьютерами (или виртуальной машины), включая hello сведения для каждого компьютера в кластере hello. |
| ClusterConfig.Windows.DevCluster.json |Файл образца конфигурации кластера, содержащий все hello параметров для одной машины безопасная и трех узлов (или виртуальных машин) кластеру разработки, включая сведения о hello для каждого узла, который находится в кластере hello. Hello кластера обеспечивается с помощью [удостоверений Windows](https://msdn.microsoft.com/library/ff649396.aspx). |
| ClusterConfig.Windows.MultiMachine.json |Файл образца конфигурации кластера, содержащий все параметры hello для безопасной, несколькими компьютерами (или кластер виртуальных машин) с использованием безопасности Windows, включая сведения о hello для каждой машины, которая находится в кластере безопасного hello. Hello кластера обеспечивается с помощью [удостоверений Windows](https://msdn.microsoft.com/library/ff649396.aspx). |
| ClusterConfig.x509.DevCluster.json |Файл образца конфигурации кластера, содержащий все параметры hello безопасная и трех узлов одним компьютером (или виртуальных машин) разработки кластер, включая сведения о hello для каждого узла в кластере hello. Hello кластера защищается с помощью x509 сертификаты. |
| ClusterConfig.x509.MultiMachine.json |Образец файла конфигурации кластера, содержащий все параметры hello для hello безопасна, несколькими компьютерами (или кластер виртуальных машин), включая сведения о hello для каждого узла в кластере безопасного hello. Hello кластера защищается с помощью x509 сертификаты. |
| ClusterConfig.gMSA.Windows.MultiMachine.json |Образец файла конфигурации кластера, содержащий все параметры hello для hello безопасна, несколькими компьютерами (или кластер виртуальных машин), включая сведения о hello для каждого узла в кластере безопасного hello. Hello кластера защищается с помощью [групповых управляемых учетных записей служб](https://technet.microsoft.com/en-us/library/jj128431(v=ws.11).aspx). |

## <a name="cluster-configuration-samples"></a>Примеры конфигурации кластера
Последние версии шаблонов конфигурации кластера можно найти на странице GitHub hello: [образцы настройки кластера автономный](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).

## <a name="independent-runtime-package"></a>Независимый пакет среды выполнения
последнюю версию среды выполнения пакета Hello загружается автоматически во время развертывания кластера из [ссылку Загрузить - среда выполнения Service Fabric - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).

## <a name="related"></a>Сопутствующие материалы
* [Создание изолированного кластера Azure Service Fabric](service-fabric-cluster-creation-for-windows-server.md)
* [Сценарии защиты кластера Service Fabric](service-fabric-windows-cluster-windows-security.md)
