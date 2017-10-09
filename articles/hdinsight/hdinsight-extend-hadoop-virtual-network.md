---
title: "aaaExtend HDInsight с помощью виртуальной сети - Azure | Документы Microsoft"
description: "Дополнительные сведения об toouse виртуальной сети Azure tooconnect HDInsight tooother облачных ресурсов, или в центре обработки данных"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: ba80be4d9f280c6c62fa8acc996ef5f921acdbbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a>Расширение возможностей HDInsight с помощью виртуальной сети Azure

Узнайте, как toouse HDInsight с [виртуальной сети Azure](../virtual-network/virtual-networks-overview.md). С помощью виртуальной сети Azure обеспечивает hello следующие сценарии:

* Подключение tooHDInsight непосредственно из локальной сети.

* Подключение HDInsight toodata хранятся в Azure в виртуальной сети.

* Непосредственно доступ к службам Hadoop, которые недоступны в более публично hello Интернета. Например API-интерфейсов Kafka или hello HBase Java API.

> [!WARNING]
> в этом документе сведения Hello требует понимания сети TCP/IP. Если вы не знакомы с конфигурацией сети TCP/IP, следует сотрудничества с пользователями, прежде чем вносить изменения tooproduction сетей.

## <a name="planning"></a>Планирование

Здесь представлены Hello hello вопросы, которые должен ответить при планировании tooinstall HDInsight в виртуальной сети:

* Требуется tooinstall HDInsight в существующей виртуальной сети? Или вы создаете новую сеть?

    При использовании существующей виртуальной сети, может потребоваться toomodify hello сетевой конфигурации перед установкой HDInsight. Дополнительные сведения см. в разделе hello [добавить виртуальную сеть с существующие HDInsight tooan](#existingvnet) раздела.

* Вы хотите tooconnect hello виртуальная сеть, содержащая HDInsight tooanother виртуальной сети или в локальной сети?

    tooeasily работы с ресурсами в сетях может требуется toocreate пользовательские DNS и настройте DNS. Дополнительные сведения см. в разделе hello [подключение нескольких сетей](#multinet) раздела.

* Вы хотите toorestrict перенаправление tooHDInsight входящего и исходящего трафика?

    HDInsight необходимо имеют неограниченный связь с определенных IP-адресов в центре обработки данных Azure hello. Существует несколько портов, которые следует разрешить в брандмауэрах для взаимодействия с клиентами. Дополнительные сведения см. в разделе hello [управлению сетевым трафиком](#networktraffic) раздела.

## <a id="existingvnet"></a>Добавить HDInsight tooan существующей виртуальной сети

Как использовать действия hello в этот раздел toodiscover tooadd новый tooan HDInsight с существующей виртуальной сети Azure.

> [!NOTE]
> В виртуальную сеть невозможно добавить существующий кластер HDInsight.

1. Используется классический или модели развертывания диспетчера ресурсов для hello виртуальной сети?

    Для HDInsight 3.4 и более поздней версии требуется виртуальная сеть диспетчера ресурсов. Для работы более ранних версий HDInsight требовалась классическая виртуальная сеть.

    При наличии существующей сети классической виртуальной сети, необходимо создать виртуальную сеть диспетчера ресурсов и подключитесь hello два. [Подключение классических виртуальных сетей toonew виртуальных сетей](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

    После присоединения, HDInsight установлен в диспетчер ресурсов сети hello могут взаимодействовать с ресурсы в сети классический hello.

2. Используется ли принудительное туннелирование? Принудительное туннелирование — подсеть, требующем исходящего Интернет трафика tooa устройства для проверки и ведение журнала. HDInsight не поддерживает принудительное туннелирование. Перед установкой HDInsight в подсеть либо удалите принудительное туннелирование, либо создайте новую подсеть для HDInsight.

3. Нужны Сетевые группы безопасности, определяемых пользователем маршрутов или виртуальные сетевые устройства toorestrict трафика в или из hello виртуальной сети?

    В качестве управляемой службы HDInsight требуется неограниченный доступ tooseveral IP-адресов в центре обработки данных Azure hello. связь tooallow с этих IP-адресов, обновить существующие группы безопасности сети и определяемых пользователем маршрутов.

    В состав HDInsight входит несколько служб, которые используют различные порты. Не блокируют трафик toothese портов. Список портов tooallow брандмауэрах виртуальных устройств см. в разделе hello [безопасности](#security) раздела.

    toofind существующей конфигурации безопасности, hello используйте следующие команды Azure PowerShell или Azure CLI:

    * Группы безопасности сети

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        Дополнительные сведения см. в разделе hello [Устранение сетевых групп безопасности](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) документа.

        > [!IMPORTANT]
        > Правила группы безопасности сети применяются в порядке, основанном на приоритете правила. применяется первое правило Hello, соответствующую шаблону трафика hello и другие применяются для этого трафика. Порядок правила с максимальными tooleast разрешительным. Дополнительные сведения см. в разделе hello [фильтрации трафика с группами безопасности сети](../virtual-network/virtual-networks-nsg.md) документа.

    * Определяемые пользователем маршруты

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        Дополнительные сведения см. в разделе hello [Устранение маршруты](../virtual-network/virtual-network-routes-troubleshoot-portal.md) документа.

4. Создание кластера HDInsight и выбора hello виртуальной сети Azure во время установки. Выполните шаги hello в следующих toounderstand документы в процессе создания кластера hello hello.

    * [Создание с помощью hello портал Azure HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [Создание кластера HDInsight с использованием Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [Создание кластеров HDInsight с помощью интерфейса командной строки Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [Создание кластеров Hadoop в HDInsight с помощью шаблонов Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > Добавление HDInsight tooa виртуальной сети — это шаг дополнительная настройка. При настройке кластера hello, быть виртуальной сети, что tooselect hello.

## <a id="multinet"></a>Подключение нескольких сетей

сложная задача Hello с несколькими сетевая конфигурация является разрешение имен между сетями hello.

Azure предоставляет разрешение имен для служб Azure, установленных в виртуальной сети. Это разрешение встроенным именем позволяет toohello tooconnect HDInsight следующие ресурсы с помощью полного доменного имени (FQDN):

* Любой ресурс, доступный на hello Интернета. например, microsoft.com, google.com;

* Любые ресурсы, в hello одной виртуальной сети Azure с помощью hello __внутренние имена DNS__ hello ресурса. Например при использовании разрешение имен по умолчанию hello, hello представлены пример внутренней DNS имена назначенного tooHDInsight рабочих узлов:

    * wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net;
    * wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net.

    Оба этих узла могут взаимодействовать напрямую друг с другом и с другими узлами в HDInsight, используя внутренние DNS-имена.

разрешение имен по умолчанию Hello __не__ разрешить HDInsight tooresolve hello имена ресурсов в сетях, которые будут присоединены к домену toohello виртуальной сети. Например, это общие toojoin в локальной сети toohello виртуальной сети. Только hello разрешения имени по умолчанию HDInsight не может обращаться к ресурсам локальной сети hello по имени. Hello противоположной также имеет значение true, ресурсам в локальной сети не доступ к ресурсам в виртуальной сети hello по имени.

> [!WARNING]
> Необходимо создать hello пользовательского DNS-сервера и настроить виртуальную сеть toouse hello его перед созданием hello кластера HDInsight.

tooenable разрешение имен между hello виртуальной сети и ресурсами в сетях, присоединены к домену, необходимо выполнить hello, следующие действия:

1. Создание пользовательского DNS-сервера в виртуальной сети Azure, где планируется tooinstall HDInsight hello.

2. Настройте hello виртуальной сети toouse hello пользовательского DNS-сервера.

3. Найти hello Azure назначать DNS-суффикса для виртуальной сети. Это значение аналогично слишком`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`. Сведения о поиске hello DNS-суффикс в разделе hello [пример: Настройка DNS](#example-dns) раздела.

4. Настройка перенаправления между hello DNS-серверов. Конфигурация Hello зависит от типа hello удаленной сети.

    * Если hello удаленной сети к локальной сети, настройте DNS следующим образом.
        
        * __Пользовательские DNS__ (в виртуальной сети hello):

            * Перенаправлять запросы DNS-суффикс hello hello виртуальной сети toohello Azure рекурсивного сопоставителя (168.63.129.16). Azure обрабатывает запросы к ресурсам в виртуальной сети hello

            * Пересылка всех других запросов toohello локального DNS-сервера. Hello на локальном DNS обрабатывает все остальные запросы на разрешение имен, включая запросы для Интернет-ресурсов как Microsoft.com.

        * __Локальный DNS__: перенаправление запросов для hello виртуальной сети DNS-суффикс toohello пользовательские DNS сервера. Hello пользовательские DNS-сервер переадресует toohello Azure рекурсивного сопоставителя.

        Запросы маршруты этой конфигурации для полные доменные имена, которые содержат hello DNS-суффикс hello виртуальной сети toohello пользовательского DNS-сервера. Все запросы (даже для общедоступных адресов Интернета) обрабатываются hello локального DNS-сервера.

    * Если другой виртуальной сети Azure hello удаленной сети, настройте DNS следующим образом.

        * __Пользовательский DNS-сервер__ (в каждой виртуальной сети):

            * Запросы DNS-суффикс hello hello виртуальных сетей, перенаправляются toohello пользовательские DNS-серверы. для разрешения ресурсов в пределах своей сети отвечает Hello DNS в каждой виртуальной сети.

            * Пересылка всех других запросов toohello Azure рекурсивного сопоставителя. Hello рекурсивного сопоставителя отвечает за разрешает локальные и Интернет-ресурсов.

        Hello DNS-сервер для каждой сети перенаправляет запросы toohello другим, основываясь на DNS-суффикс. Другие запросы разрешаются с помощью hello Azure рекурсивного сопоставителя.

    Пример каждой конфигурации см. в разделе hello [пример: Настройка DNS](#example-dns) раздела.

Дополнительные сведения см. в разделе hello [разрешение имен для виртуальных машин и экземпляров ролей](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) документа.

## <a name="directly-connect-toohadoop-services"></a>Подключение непосредственно tooHadoop служб

Большая часть документации по HDInsight предполагается, что кластер toohello доступ через hello Интернета. Например, возможность подключения кластера toohello в https://CLUSTERNAME.azurehdinsight.net. Этот адрес используется hello открытый шлюз, который недоступен, если вы использовали Nsg или Здравствуйте, UDRs toorestrict доступ из Интернета.

tooconnect tooAmbari и других веб-страницы через hello виртуальную сеть, использовать hello, следующие шаги:

1. hello toodiscover внутренней полные доменные имена (FQDN) узлов кластера HDInsight hello, используйте один из hello следующие методы:

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

    В список узлов, возвращаемых hello найти hello полное доменное имя для hello головного узла и используйте tooAmbari tooconnect hello полных доменных имен и других веб-служб. Например, использовать `http://<headnode-fqdn>:8080` tooaccess Ambari.

    > [!IMPORTANT]
    > Некоторые службы, размещенной на hello головного узла активны только на одном узле одновременно. При попытке доступа к службе на один головной узел и его возвращает ошибку 404, переключение toohello других головного узла.

2. toodetermine hello узел и порт, который доступен на, см. раздел hello [порты, используемые службами Hadoop в HDInsight](./hdinsight-hadoop-port-settings-for-services.md) документа.

## <a id="networktraffic"></a>Управление сетевым трафиком

Сетевой трафик в виртуальные сети Azure можно управлять с помощью hello следующие методы:

* **Сетевых групп безопасности** (NSG) позволяют сети toohello toofilter входящего и исходящего трафика. Дополнительные сведения см. в разделе hello [фильтрации трафика с группами безопасности сети](../virtual-network/virtual-networks-nsg.md) документа.

    > [!WARNING]
    > HDInsight не поддерживает ограничение исходящего трафика.

* **Определяемые пользователем маршруты** (UDR) определяют, как проходит трафик между ресурсами в сети hello. Дополнительные сведения см. в разделе hello [определяемые пользователем маршруты и IP-пересылки](../virtual-network/virtual-networks-udr-overview.md) документа.

* **Сети виртуальных приборов** реплицировать hello функциональные возможности устройства, например брандмауэров и маршрутизаторов. Дополнительные сведения см. в разделе hello [сетевые устройства](https://azure.microsoft.com/solutions/network-appliances) документа.

Как управляемая служба HDInsight требуется неограниченный доступ tooAzure работоспособности и управлять ими в облаке Azure hello. При использовании NSG и UDR необходимо убедиться, что эти службы могут взаимодействовать с HDInsight.

HDInsight предоставляет службы на нескольких портах. При использовании брандмауэра виртуальное устройство, необходимо разрешить трафик через hello порты, используемые для этих служб. Дополнительные сведения см в разделе [требуемые порты] hello.

### <a id="hdinsight-ip"></a>HDInsight с группами безопасности сети и определяемые пользователем маршрутами

Если вы планируете использовать **сетевых групп безопасности** или **определяемых пользователем маршрутов** toocontrol сетевого трафика, выполните следующие действия перед установкой HDInsight hello:

1. Определите hello регион Azure, планирование toouse HDInsight.

2. Определите hello IP-адреса, необходимые для HDInsight. Дополнительные сведения см. в разделе hello [IP-адреса, необходимые для HDInsight](#hdinsight-ip) раздела.

3. Создание или изменение группы безопасности сети hello или определяемых пользователем маршрутов для подсети hello планировать tooinstall HDInsight в.

    * __Сетевых групп безопасности__: Разрешить __входящий__ трафик через порт __443__ с hello IP-адресов.
    * __Определяемые пользователем маршруты__: создание IP-адрес маршрута tooeach и задание hello __тип следующего прыжка__ too__Internet__.

Дополнительные сведения о сетевых групп безопасности и определяемых пользователем маршрутов см. следующие документации hello:

* [группа безопасности сети](../virtual-network/virtual-networks-nsg.md).

* [Определяемые пользователем маршруты](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a>Принудительное туннелирование

Принудительное туннелирование это определяемая пользователем конфигурация маршрутизации, где весь трафик из подсети принудительное tooa определенным сети или в расположении, например в локальной сети. HDInsight __не__поддерживает принудительное туннелирование.

## <a id="hdinsight-ip"></a> Требуемые IP-адреса

> [!IMPORTANT]
> Hello Azure работоспособности и службы управления должен быть доступ toocommunicate с HDInsight. Если вы используете группы безопасности сети и определяемых пользователем маршрутов, разрешите трафик от hello IP-адресов для этих служб tooreach HDInsight.
>
> Если не используется группами безопасности сети или трафик toocontrol определяемых пользователем маршрутов, можно игнорировать в этом разделе.

При использовании групп безопасности сети и определяемых пользователем маршрутов, необходимо разрешить трафик от hello Azure health и tooreach управления службы HDInsight. Используйте следующие hello действия toofind hello IP-адресов, которые должны быть разрешены.

1. Всегда необходимо разрешить трафик от hello следующие IP-адреса:

    | IP-адрес | Разрешенный порт | Направление |
    | ---- | ----- | ----- |
    | 168.61.49.99 | 443 | Входящий трафик |
    | 23.99.5.239 | 443 | Входящий трафик |
    | 168.61.48.131 | 443 | Входящий трафик |
    | 138.91.141.162 | 443 | Входящий трафик |

2. Если ваш HDInsight кластер находится в одном из следующих областей hello, необходимо разрешить трафик от hello IP-адресов для области hello:

    > [!IMPORTANT]
    > Если регион Azure, которую вы используете hello не указан, то используйте только hello четыре IP-адреса из шага 1.

    | Страна | Регион | Разрешенные IP-адреса | Разрешенный порт | Направление |
    | ---- | ---- | ---- | ---- | ----- |
    | Азия | Восточная Азия | 23.102.235.122</br>52.175.38.134 | 443 | Входящий трафик |
    | &nbsp; | Юго-Восточная Азия | 13.76.245.160</br>13.76.136.249 | 443 | Входящий трафик |
    | Австралия | Восточная часть Австралии | 104.210.84.115</br>13.75.152.195 | 443 | Входящий трафик |
    | &nbsp; | Юго-Восточная часть Австралии | 13.77.2.56</br>13.77.2.94 | 443 | Входящий трафик |
    | Бразилия | Южная часть Бразилии | 191.235.84.104</br>191.235.87.113 | 443 | Входящий трафик |
    | Канада | Восточная Канада | 52.229.127.96</br>52.229.123.172 | 443 | Входящий трафик |
    | &nbsp; | Центральная Канада | 52.228.37.66</br>52.228.45.222 | 443 | Входящий трафик |
    | Китай | Север Китая | 42.159.96.170</br>139.217.2.219 | 443 | Входящий трафик |
    | &nbsp; | Восток Китая | 42.159.198.178</br>42.159.234.157 | 443 | Входящий трафик |
    | Европа | Северная Европа | 52.164.210.96</br>13.74.153.132 | 443 | Входящий трафик |
    | &nbsp; | Западная Европа| 52.166.243.90</br>52.174.36.244 | 443 | Входящий трафик |
    | Германия | Центральная Германия | 51.4.146.68</br>51.4.146.80 | 443 | Входящий трафик |
    | &nbsp; | Северо-восточная Германия | 51.5.150.132</br>51.5.144.101 | 443 | Входящий трафик |
    | Индия | Центральная Индия | 52.172.153.209</br>52.172.152.49 | 443 | Входящий трафик |
    | Япония | Восточная часть Японии | 13.78.125.90</br>13.78.89.60 | 443 | Входящий трафик |
    | &nbsp; | Западная часть Японии | 40.74.125.69</br>138.91.29.150 | 443 | Входящий трафик |
    | Корея | Центральная Корея | 52.231.39.142</br>52.231.36.209 | 433 | Входящий трафик |
    | &nbsp; | Южная Корея | 52.231.203.16</br>52.231.205.214 | 443 | Входящий трафик
    | Великобритания | Западная часть Великобритании | 51.141.13.110</br>51.141.7.20 | 443 | Входящий трафик |
    | &nbsp; | Южная часть Великобритании | 51.140.47.39</br>51.140.52.16 | 443 | Входящий трафик |
    | США | Центральный регион США | 13.67.223.215</br>40.86.83.253 | 443 | Входящий трафик |
    | &nbsp; | Северо-центральный регион США | 157.56.8.38</br>157.55.213.99 | 443 | Входящий трафик |
    | &nbsp; | Западно-центральная часть США | 52.161.23.15</br>52.161.10.167 | 443 | Входящий трафик |
    | &nbsp; | Западный регион США 2 | 52.175.211.210</br>52.175.222.222 | 443 | Входящий трафик |

    На hello IP-адреса toouse для Azure для государственных, см. в разделе hello [аналитики Azure государственных + аналитика](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) документа.

3. Если в виртуальной сети используется пользовательский DNS-сервер, необходимо также разрешить доступ с адреса __168.63.129.16__. Этот адрес рекурсивного сопоставителя Azure. Дополнительные сведения см. в разделе hello [разрешение имен для виртуальных машин и роль экземпляров](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) документа.

Дополнительные сведения см. в разделе hello [управлению сетевым трафиком](#networktraffic) раздела.

## <a id="hdinsight-ports"></a> Требуемые порты

Если вы планируете использовать сеть **брандмауэра виртуальное устройство** toosecure hello виртуальной сети, необходимо разрешить исходящий трафик на hello, следующие порты:

* 53
* 443
* 1433
* 11000–11999;
* 14000–14999.

Список портов для определенных служб см. в разделе hello [порты, используемые службами Hadoop в HDInsight](hdinsight-hadoop-port-settings-for-services.md) документа.

Дополнительные сведения о правила брандмауэра для виртуальных устройств см. в разделе hello [сценарий виртуальное устройство](../virtual-network/virtual-network-scenario-udr-gw-nva.md) документа.

## <a id="hdinsight-nsg"></a>Пример: группы безопасности сети с HDInsight

Hello в примерах этого раздела показано, как правила toocreate сетевой группы безопасности, позволяющие toocommunicate HDInsight с hello службы управления Azure. При использовании примеров hello, настройте hello IP адресов toomatch hello из них для hello регион Azure, которую вы используете. Эти сведения можно найти в hello [HDInsight с группами безопасности сети и определяемых пользователем маршрутов](#hdinsight-ip) раздела.

### <a name="azure-resource-management-template"></a>Шаблон управления ресурсами Azure

Hello следующий шаблон управления ресурсами создает виртуальной сети, которая ограничивает входящий трафик, но разрешает трафик с hello IP-адреса, необходимые для HDInsight. Этот шаблон также создает кластер HDInsight в виртуальной сети hello.

* [Развертывание защищенной виртуальной сети Azure и кластера HDInsight Hadoop](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> Изменение IP-адреса hello в этот примере toomatch hello регион Azure, которую вы используете. Эти сведения можно найти в hello [HDInsight с группами безопасности сети и определяемых пользователем маршрутов](#hdinsight-ip) раздела.

### <a name="azure-powershell"></a>Azure PowerShell

Используйте следующий сценарий PowerShell toocreate виртуальной сети, которая ограничивает входящего трафика и разрешает трафик с hello IP-адресов для Северной Европы hello hello.

> [!IMPORTANT]
> Изменение IP-адреса hello в этот примере toomatch hello регион Azure, которую вы используете. Эти сведения можно найти в hello [HDInsight с группами безопасности сети и определяемых пользователем маршрутов](#hdinsight-ip) раздела.

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with hello resource group hello virtual network is in"
$subnetName = "Replace with hello name of hello subnet that you plan toouse for HDInsight"
# Get hello Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get hello region hello Virtual network is in.
$location = $vnet.Location
# Get hello subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for hello HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 52.164.210.96" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "52.164.210.96" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 13.74.153.132" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "13.74.153.132" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 304 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 305 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "blockeverything" `
        -Description "Block everything else" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "*" `
        -SourceAddressPrefix "Internet" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Deny `
        -Priority 500 `
        -Direction Inbound
# Set hello changes toohello security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply hello NSG toohello subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> В этом примере показано, как tooallow tooadd правила входящего трафика на hello необходимых IP-адресов. Не содержит toorestrict правило входящий доступ из других источников.
>
> Hello в следующем примере показано, как доступ к tooenable SSH из Интернета hello:
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a>Инфраструктура CLI Azure

Используйте следующие шаги toocreate виртуальной сети, которая ограничивает входящий трафик, но разрешает трафик с hello IP-адреса, необходимые для HDInsight hello.

1. Следующая команда toocreate новую группу безопасности сети с именем hello используйте `hdisecure`. Замените **RESOURCEGROUPNAME** с группой ресурсов hello, содержащий hello виртуальной сети Azure. Замените **РАСПОЛОЖЕНИЕ** с hello местоположение (регион) был создан этой группы hello в.

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    После создания группы hello вы получите информацию для новой группы hello.

2. Используйте следующие tooadd правила toohello новую группу безопасности сети, разрешить входящий трафик на порте 443 из службы работоспособности и управления Azure HDInsight hello hello. Замените **RESOURCEGROUPNAME** с именем hello hello группы ресурсов, которая содержит hello виртуальной сети Azure.

    > [!IMPORTANT]
    > Изменение IP-адреса hello в этот примере toomatch hello регион Azure, которую вы используете. Эти сведения можно найти в hello [HDInsight с группами безопасности сети и определяемых пользователем маршрутов](#hdinsight-ip) раздела.

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. tooretrieve hello уникальный идентификатор для этой группы безопасности сети, выполните следующую команду hello.

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    Эта команда возвращает аналогичные toohello значение, следующий текст:

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    Используйте двойные кавычки вокруг идентификатор в команду hello, если не дал результатов ожидается hello.

4. Используйте следующие команды tooapply hello безопасности группы tooa подсети hello. Замените hello __GUID__ и __RESOURCEGROUPNAME__ значения с hello тех, которые возвращены из предыдущего шага hello. Замените __VNETNAME__ и __SUBNETNAME__ с именем hello виртуальной сети и подсети, которые должны toocreate.

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    После выполнения этой команды можно установить HDInsight в hello виртуальной сети.

> [!IMPORTANT]
> Эти действия только открыть доступ toohello HDInsight работоспособности и управления службу hello облако Azure. Все другие доступа toohello кластер HDInsight из внешней hello виртуальной сети будет заблокирован. tooenable доступ из внешней hello виртуальной сети, необходимо добавить дополнительные правила группы безопасности сети.
>
> Hello в следующем примере показано, как доступ к tooenable SSH из Интернета hello:
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <a id="example-dns"></a> Пример: конфигурация DNS

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a>Разрешение DNS-имен между виртуальной сетью и подключенной локальной сетью

Этот пример делает hello следующие допущения:

* У вас есть виртуальная сеть Azure, подключенной tooan локальной сети с помощью шлюза VPN.

* Hello пользовательского DNS-сервера в виртуальной сети hello выполняется под hello операционной системы Unix или Linux.

* [Привязать](https://www.isc.org/downloads/bind/) устанавливается на hello пользовательского DNS-сервера.

На hello пользовательского DNS-сервера в виртуальной сети hello:

1. Используйте Azure PowerShell или Azure CLI toofind hello DNS-суффикс hello виртуальной сети:

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. На hello пользовательского DNS-сервера для hello виртуальной сети, используйте hello после текста как содержимое hello hello `/etc/bind/named.conf.local` файла:

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    Замените hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` значение с DNS-суффиксом hello виртуальной сети.

    Эта конфигурация направляет все запросы DNS для DNS-суффикс hello hello виртуальной сети toohello Azure рекурсивного сопоставителя.

2. На hello пользовательского DNS-сервера для hello виртуальной сети, используйте hello после текста как содержимое hello hello `/etc/bind/named.conf.options` файла:

    ```
    // Clients tooaccept requests from
    // TODO: Add hello IP range of hello joined network toothis list
    acl goodclients {
        10.0.0.0/16; # IP address range of hello virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent toohello following
            forwarders {
                192.168.0.1; # Replace with hello IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * Замените hello `10.0.0.0/16` значение с hello диапазон IP-адресов виртуальной сети. Эта запись разрешает запросы на разрешение имен в этом диапазоне.

    * Добавить диапазон IP-адресов hello объекта hello в локальной сети toohello `acl goodclients { ... }` раздела.  запись разрешает запросы разрешения имен из ресурсов в локальной сети hello.
    
    * Замените значение hello `192.168.0.1` hello IP-адрес локального DNS-сервера. Эта запись направляет все другие DNS запросы toohello локального DNS-сервера.

3. Конфигурация toouse hello, перезапустите привязки. Например, `sudo service bind9 restart`.

4. Добавление условной пересылки toohello локальный DNS-сервер. Настройте запросы toosend hello условной пересылки DNS-суффикс hello из шага 1 toohello пользовательского DNS-сервера.

    > [!NOTE]
    > В документации hello программного обеспечения DNS конкретные сведения о том, как tooadd условной пересылки.

После выполнения этих действий, можно подключить tooresources в сети, либо используя полные доменные имена (FQDN). Теперь можно установить HDInsight в виртуальной сети hello.

### <a name="name-resolution-between-two-connected-virtual-networks"></a>Разрешение имен между двумя подключенными виртуальными сетями

Этот пример делает hello следующие допущения:

* Имеется две виртуальных сети Azure, подключенные друг к другу посредством VPN-шлюза или пиринга.

* Hello пользовательского DNS-сервера в обеих сетях выполняется под hello операционной системы Unix или Linux.

* [Привязать](https://www.isc.org/downloads/bind/) устанавливается на hello пользовательские DNS-серверы.

1. Использование Azure PowerShell или Azure CLI toofind hello DNS-суффикс обе виртуальные сети:

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. Используйте hello после текста как содержимое hello hello `/etc/bind/named.config.local` файл на hello пользовательского DNS-сервера. Внести это изменение на hello пользовательского DNS-сервера в обе виртуальные сети.

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello IP address of hello DNS server in hello other virtual network
    };
    ```

    Замените hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` значение с DNS-суффикс hello hello __других__ виртуальной сети. Эта запись будет направлять запросы DNS-суффикс hello toohello удаленной сети hello пользовательские DNS-сервер в этой сети.

3. На hello пользовательские DNS-серверы в обе виртуальные сети, с помощью hello после текста как содержимое hello hello `/etc/bind/named.conf.options` файла:

    ```
    // Clients tooaccept requests from
    acl goodclients {
        10.1.0.0/16; # hello IP address range of one virtual network
        10.0.0.0/16; # hello IP address range of hello other virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            forwarders {
            168.63.129.16;   # Azure recursive resolver         
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * Замените hello `10.0.0.0/16` и `10.1.0.0/16` значения hello IP-адресов виртуальных сетей. Эта запись позволяет ресурсы в каждой сети запросы toomake hello DNS-серверов.

    Запросы, которые не предназначены для DNS-суффиксы hello hello виртуальных сетей (например, microsoft.com) обрабатывается hello Azure рекурсивного сопоставителя.

4. Конфигурация toouse hello, перезапустите привязки. Например, `sudo service bind9 restart` на обоих DNS-серверах.

После выполнения этих действий, можно подключить tooresources в hello виртуальной сети, используя полные доменные имена (FQDN). Теперь можно установить HDInsight в виртуальной сети hello.

## <a name="next-steps"></a>Дальнейшие действия

* Пример конца в конец настройки HDInsight tooconnect tooan локальную сеть, в разделе [HDInsight подключения tooan локальной сети](./connect-on-premises-network.md).

* Дополнительные сведения о виртуальных сетях Azure см. в разделе hello [Обзор виртуальной сети Azure](../virtual-network/virtual-networks-overview.md).

* Дополнительные сведения о группах безопасности сети см. в статье [Фильтрация сетевого трафика с помощью групп безопасности сети](../virtual-network/virtual-networks-nsg.md).

* Дополнительные сведения о пользовательских маршрутах см. в статье [Определяемые пользователем маршруты и IP-пересылка](../virtual-network/virtual-networks-udr-overview.md).