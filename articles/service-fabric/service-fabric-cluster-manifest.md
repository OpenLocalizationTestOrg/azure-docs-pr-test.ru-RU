---
title: "aaaConfigure кластера автономной Azure Service Fabric | Документы Microsoft"
description: "Узнайте, как tooconfigure изолированном или закрытый кластера Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dekapur
ms.openlocfilehash: ce2ad387162a05668bbd3a271c754776fe471850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a>Параметры конфигурации для автономного кластера Windows
В этой статье описывается, как hello кластера Service Fabric автономный заданий с помощью tooconfigure ***ClusterConfig.JSON*** файла. Можно использовать этот файл toospecify сведения hello Service Fabric узлов и IP-адресов, различные типы узлов кластера hello, hello конфигурации безопасности, а также hello топологии сети с точки зрения домены сбоя и обновления для вашего автономного кластер.

При вы [загрузить hello изолированный пакет Service Fabric](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), несколько образцов hello ClusterConfig.JSON файла при отсутствии загруженных tooyour работы. образцы Hello наличие *DevCluster* в именах поможет вам создать кластер с тремя узлами на hello же компьютера, такие как логические узлы. По крайней мере один узел должен быть помечен как первичный. Данный кластер удобен для среды разработки или тестирования, но не предназначен для использования в качестве рабочего кластера. образцы Hello наличие *MultiMachine* в именах, поможет вам создать кластер производственного качества, с каждым узлом на отдельном компьютере.

1. *ClusterConfig.Unsecure.DevCluster.JSON* и *ClusterConfig.Unsecure.MultiMachine.JSON* Показать, как toocreate небезопасные тестирования или производственных кластера соответственно. 
2. *ClusterConfig.Windows.DevCluster.JSON* и *ClusterConfig.Windows.MultiMachine.JSON* Показать, как toocreate или тестовом кластера защищено с помощью [безопасности Windows](service-fabric-windows-cluster-windows-security.md).
3. *ClusterConfig.X509.DevCluster.JSON* и *ClusterConfig.X509.MultiMachine.JSON* Показать, как toocreate или тестовом кластера защищено с помощью [X509 безопасности на основе сертификатов](service-fabric-windows-cluster-x509-security.md). 

Теперь рассмотрим hello различные разделы ***ClusterConfig.JSON*** файла, как показано ниже.

## <a name="general-cluster-configurations"></a>Общие параметры кластера
Они охватывают hello широкий определенной конфигурации кластера, как показано в приведенном ниже фрагменте JSON hello.

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

Можно присвоить понятное имя кластера Service Fabric tooyour назначив toohello **имя** переменной. Hello **clusterConfigurationVersion** — номер версии hello кластера; следует увеличить ее каждый раз, чтобы обновить кластер Service Fabric. Однако следует оставить hello **apiVersion** toohello значение по умолчанию.

<a id="clusternodes"></a>

## <a name="nodes-on-hello-cluster"></a>Узлы в кластере hello
Можно настроить hello узлы в кластере Service Fabric с помощью hello **узлы** раздел, в следующем фрагменте кода показан hello.

    "nodes": [{
        "nodeName": "vm0",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType1",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType2",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],

Кластер Service Fabric должен содержать по крайней мере 3 узла. Можно добавить дополнительные узлы toothis раздел согласно настройки программы установки. Hello в следующей таблице описывается hello параметры конфигурации для каждого узла.

| **Параметр узла** | **Описание** |
| --- | --- |
| nodeName |Можно присвоить любой узел toohello понятное имя. |
| iPAddress |Узнать hello IP-адрес вашего узла, откройте окно командной строки и введите `ipconfig`. Записать hello IPV4-адрес и назначьте его toohello **IP-адрес** переменной. |
| nodeTypeRef |Узлам можно назначить разные типы узла. Hello [типы узлов](#nodetypes) определены в разделе "hello" ниже. |
| faultDomain |Ошибки домены enable Администраторы toodefine hello физических узлах кластера, может вызвать сбой во hello одновременную из-за tooshared физического зависимости. |
| upgradeDomain |Наборы узлов, которые будут закрыты для Service Fabric за обновляется о hello же описывают доменов обновления времени. Можно выбрать какие узлы tooassign toowhich доменов обновления, как они не ограничивается физической требования. |

## <a name="cluster-properties"></a>Свойства кластера
Hello **свойства** раздела hello ClusterConfig.JSON — кластер hello tooconfigure используется следующим образом.

<a id="reliability"></a>

### <a name="reliability"></a>Надежность
Понятие Hello **reliabilityLevel** определяет число hello реплик или экземпляры hello Service Fabric системных служб, которые могут выполняться на основных узлах hello hello кластера. Он определяет hello надежности этих служб и поэтому hello кластера. значение Hello — Вычисляемые системой hello во время создания и обновления кластера.

### <a name="diagnostics"></a>Диагностика
Hello **diagnosticsStore** раздел позволяет вам tooconfigure параметры tooenable диагностики и устранения неполадок узла или сбоя кластера, как показано в следующий фрагмент кода hello. 

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

Hello **метаданные** описание диагностики кластера и может быть задано согласно настройки программы установки. Эти переменные помогают собирать журналы трассировки событий Windows, аварийные дампы и данные счетчиков производительности. Прочитайте статьи [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) и [Трассировка событий Windows](https://msdn.microsoft.com/library/ms751538.aspx), чтобы больше узнать о журналах трассировки событий Windows. Все журналы, в том числе [аварийные дампы](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) и [счетчики производительности](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) может быть расширенный toohello **connectionString** папкой на компьютере. Для хранения данных диагностики можно также использовать *AzureStorage* . Ниже приведен фрагмент кода.

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a>Безопасность
Hello **безопасности** раздел необходим для безопасного автономный кластера Service Fabric. Следующий фрагмент кода Hello показана часть в этом разделе.

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

Hello **метаданные** Описание безопасного кластера и может быть задано согласно настройки программы установки. Hello **ClusterCredentialType** и **ServerCredentialType** определить hello тип безопасности, который будет реализовывать hello кластера и узлов hello. Они могут быть заданы tooeither *X509* для обеспечения безопасности на основе сертификатов или *Windows* для обеспечения безопасности на основе Azure Active Directory. Здравствуйте, остальная часть hello **безопасности** раздел будет основываться на типе hello hello безопасности. Чтение [безопасности на основе сертификатов в кластере автономный](service-fabric-windows-cluster-x509-security.md) или [безопасности Windows в кластере автономный](service-fabric-windows-cluster-windows-security.md) сведения о как toofill out hello остальной части hello **безопасности**раздел.

<a id="nodetypes"></a>

### <a name="node-types"></a>Типы узлов
Hello **nodeTypes** раздел описывает тип hello hello узлов в кластере. Необходимо указать тип хотя бы один узел в кластере, как показано в приведенном ниже фрагменте hello. 

    "nodeTypes": [{
        "name": "NodeType0",
        "clientConnectionEndpointPort": "19000",
        "clusterConnectionEndpointPort": "19001",
        "leaseDriverEndpointPort": "19002"
        "serviceConnectionEndpointPort": "19003",
        "httpGatewayEndpointPort": "19080",
        "reverseProxyEndpointPort": "19081",
        "applicationPorts": {
            "startPort": "20575",
            "endPort": "20605"
        },
        "ephemeralPorts": {
            "startPort": "20606",
            "endPort": "20861"
        },
        "isPrimary": true
    }]

Hello **имя** hello понятное имя для этого типа узла. toocreate узлом этого типа, назначить его понятное имя toohello **nodeTypeRef** переменных для этого узла, как было сказано [выше](#clusternodes). Определения hello конечных точек подключения, которые будут использоваться для каждого типа узла. Для этих конечных точек подключения можно выбрать любой номер порта, если он не конфликтует с другими конечными точками в данном кластере. В кластер с несколькими узлами, будет один или несколько основных узла (т. е. **isPrimary** значение слишком*true*), в зависимости от hello [ **reliabilityLevel** ](#reliability). Чтение [вопросы планирования емкости кластера Service Fabric](service-fabric-cluster-capacity.md) сведения о **nodeTypes** и **reliabilityLevel**и tooknow какие первичной, а hello типы узлов неосновной. 

#### <a name="endpoints-used-tooconfigure-hello-node-types"></a>Типы узлов hello tooconfigure использовать конечные точки
* *clientConnectionEndpointPort* hello порт, используемый кластере toohello tooconnect клиента hello, при использовании интерфейсов API клиента hello. 
* *clusterConnectionEndpointPort* hello порт, по которому узлы hello взаимодействовать друг с другом.
* *leaseDriverEndpointPort* hello порт, используемый с hello кластера аренды драйвер toofind out, если узлы hello все еще активны. 
* *serviceConnectionEndpointPort* hello порт, используемый hello приложений и служб, развернутых на узле, toocommunicate с клиентом hello Service Fabric на данном узле.
* *httpGatewayEndpointPort* hello порт, используемый кластером toohello tooconnect Service Fabric Explorer hello.
* *ephemeralPorts* переопределить hello [динамические порты, используемые hello ОС](https://support.microsoft.com/kb/929851). Service Fabric будет использовать часть эти порты приложения и оставшихся hello будут доступны для hello ОС. Его также потребуется сопоставить этот диапазон toohello существующего диапазона в hello ОС, для любых целей при выборе hello диапазоны для данных в файлах JSON образец hello. Необходимо удостовериться, что hello разницу между началом hello и серверных портов hello имеет по крайней мере 255 toomake. Возможно возникновение конфликтов, если это различие слишком мал, так как этот диапазон используется совместно с hello операционной системы. В разделе hello настроен динамический диапазон портов запустив `netsh int ipv4 show dynamicport tcp`.
* *applicationPorts* hello портов, которые будут использоваться приложениями Service Fabric hello. диапазон портов приложения Hello должно быть достаточно большим, toocover hello конечной точки требования приложений. Этот диапазон должен быть со hello динамический диапазон портов на компьютере hello, т. е. hello *ephemeralPorts* диапазона, как указано в конфигурации hello.  Service Fabric будут использовать каждый раз, когда новые порты являются обязательными, а также Будьте внимательны открыть брандмауэр Windows hello для этих портов. 
* *reverseProxyEndpointPort* — это необязательная конечная точка обратного прокси-сервера. Дополнительные сведения см. в статье [Обратный прокси-сервер Service Fabric](service-fabric-reverseproxy.md). 

### <a name="log-settings"></a>Параметры журнала
Hello **fabricSettings** раздел позволяет вам tooset hello корневые каталоги для hello Service Fabric данных и журналов. Можно изменить только во время создания исходного кластера hello. Ниже приведен фрагмент кода из этого раздела.

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

Рекомендуется использование диска без ОС в качестве hello FabricDataRoot и FabricLogRoot, как она обеспечивает большую надежность от взломов ОС. Обратите внимание, что при настройке только корневой каталог данных hello затем hello журнала корневой помещаются на один уровень ниже корневой каталог данных hello.

### <a name="stateful-reliable-service-settings"></a>Параметры надежной службы с отслеживанием состояния
Hello **KtlLogger** раздел позволяет вам tooset hello глобальные параметры конфигурации для надежного обмена. Дополнительные сведения об этих параметрах см. в разделе [Настройка надежных служб с отслеживанием состояния](service-fabric-reliable-services-configuration.md).
Hello приведенном ниже примере показаны toochange hello hello общего журнала транзакций, которая возвращает созданные tooback коллекций надежных служб с отслеживанием состояния.

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a>Функции надстройки
tooconfigure дополнительных функций, hello apiVersion должен, настроенных как "04-2017' или более поздней версии и addonFeatures должен настроить toobe:

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a>Поддержка контейнеров
Поддержка tooenable контейнера для контейнеров windows server и контейнеров hyper-v для изолированные кластеры, компонент надстройки «DnsService» hello должен toobe включена.


## <a name="next-steps"></a>Дальнейшие действия
После завершения файла ClusterConfig.JSON настроен в соответствии с вашей установки кластера, можно развернуть кластер в следующей статье hello [создание кластера Service Fabric автономный](service-fabric-cluster-creation-for-windows-server.md) и затем продолжить слишком[визуализация кластера с Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).

