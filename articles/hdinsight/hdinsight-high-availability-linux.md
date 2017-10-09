---
title: "доступность aaaHigh для Hadoop - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как использование дополнительного головного узла позволяет повысить надежность и доступность кластеров HDInsight. Узнайте, как это влияет на службам Hadoop, например, Ambari и Hive, также как tooindividually подключения tooeach головного узла с помощью SSH."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
keywords: "Высокая доступность Hadoop"
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 07/28/2017
ms.author: larryfr
ms.openlocfilehash: 9ff62afe6b63b241cb984225233157219f8d7411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a>Доступность и надежность кластеров Hadoop в HDInsight

Кластеры HDInsight предоставляют два головного узла tooincrease hello доступность и надежность Hadoop служб и заданий, выполняемых.

Платформа Hadoop обеспечивает высокий уровень доступности и надежности, реплицируя службы и данные на нескольких узлах в кластере. Однако стандартные дистрибутивы Hadoop обычно имеют один головной узел. Любой сбой одного головного узла hello может привести к работе toostop кластера hello. HDInsight обеспечивает доступность и надежность два headnodes tooimprove Hadoop.

> [!IMPORTANT]
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="availability-and-reliability-of-nodes"></a>Доступность и надежность узлов

Узлы в кластере HDInsight реализуются с помощью виртуальных машин Azure. Hello следующих разделах рассматриваются типы hello отдельный узел, используемый с HDInsight. 

> [!NOTE]
> Не все типы узлов используются для определенного типа кластера. Например, тип кластера Hadoop не содержит узлы Nimbus. Дополнительные сведения об узлах, используемые типами кластера HDInsight см раздел типы кластера hello hello [кластеров под управлением Linux, создать Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) документа.

### <a name="head-nodes"></a>Головные узлы

tooensure высокую доступность служб Hadoop, HDInsight предоставляет два головного узла. Оба головного узла и запущен в пределах кластера HDInsight hello одновременно. Некоторые службы, например HDFS или YARN, в любой момент времени активны только на одном головном узле. Другие службы, например HiveServer2 или Метахранилища Hive активны на оба головного узла на hello то же время.

Головные узлы (и другие узлы в HDInsight) имеют числовое значение как часть имени узла hello hello узла. Например, `hn0-CLUSTERNAME` или `hn4-CLUSTERNAME`.

> [!IMPORTANT]
> Не связывайте hello числовое значение с ли узел является первичной или вторичной. Hello числовое значение равно только присутствует tooprovide уникальное имя для каждого узла.

### <a name="nimbus-nodes"></a>Узлы Nimbus

Узлы Nimbus доступны с кластерами Storm. узлы Nimbus Hello предоставляют аналогичные функциональные возможности toohello Hadoop JobTracker, распространение и наблюдение за обработкой между узлами рабочих. HDInsight предоставляет два узла Nimbus для кластеров Storm.

### <a name="zookeeper-nodes"></a>Узлы Zookeeper

Узлы [ZooKeeper](http://zookeeper.apache.org/) используются для выбора лидера главных служб на головных узлах, Они также могут использовать tooinsure, что службы, узлы данных (рабочая) и шлюзы знают, какие головного узла не активна на главной службой. По умолчанию в кластере HDInsight предусмотрено три узла ZooKeeper.

### <a name="worker-nodes"></a>Рабочие узлы

Рабочих узлов анализ hello фактические данные после задания отправленной toohello кластера. В случае отказа рабочий узел hello задачу, которая его выполнением могут отправленной tooanother рабочий узел. По умолчанию HDInsight создает четыре рабочих узла. Можно изменить этот номер toosuit потребностей во время и после создания кластера.

### <a name="edge-node"></a>Граничный узел

Граничного узла не активно участвует в анализе данных в пределах кластера hello. Разработчики или специалисты по обработке и анализу данных используют его при работе с Hadoop. Hello edge узел находится в hello одной виртуальной сети Azure как hello другие узлы в кластере hello и прямой доступ к всех остальных узлов. Hello граничного узла можно использовать без учета ресурсов от критических служб Hadoop или задания анализа.

В настоящее время сервер R на HDInsight является hello только кластера тип, предоставляющий граничного узла по умолчанию. Сервер R в HDInsight, используется hello граничного узла код теста R локально на узле hello перед его отправкой toohello кластера для распределенной обработки.

Сведения об использовании граничного узла с типами кластера, отличном от сервера R см. в разделе hello [использовать краевым узлам в HDInsight](hdinsight-apps-use-edge-node.md) документа.

## <a name="accessing-hello-nodes"></a>Доступ к узлам hello

Кластер toohello доступ через hello Интернет обеспечивается через открытые шлюза. Доступ к ограниченной tooconnecting toohello головного узла и (если он существует) hello граничного узла. Наличие нескольких головного узла tooservices доступ, работающих на узлах головного hello не влияют. Hello открытый шлюза маршруты запросов toohello головного узла, на котором размещена hello Запрошенная служба. Например если Ambari в настоящий момент размещен на hello дополнительного головного узла, hello шлюза направляет входящие запросы для узла toothat Ambari.

Доступ через шлюз открытый hello является ограниченной tooport 443 (HTTPS), 22 и 23.

* Порт __443__ — используется tooaccess Ambari и других веб-интерфейса пользователя или интерфейсов API REST, размещенных на hello головного узла.

* Порт __22__ используется tooaccess hello основного головного узла или граничного узла с SSH.

* Порт __23__ — используется tooaccess hello получателей головной узел с SSH. Например `ssh username@mycluster-ssh.azurehdinsight.net` подключается toohello первичного головного узла с именем кластера hello **mycluster**.

Дополнительные сведения об использовании SSH см. в разделе hello [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) документа.

### <a name="internal-fully-qualified-domain-names-fqdn"></a>Внутренние полные доменные имена (FQDN)

Узлы в кластере HDInsight имеют внутренний IP-адрес и полное доменное имя, может осуществляться только из кластера hello. При обращении к службам на кластере hello hello внутренней полное доменное имя или IP-адрес, Ambari tooverify hello IP-адрес или полное доменное имя toouse следует использовать при доступе к службе hello.

Например, hello Oozie службы могут выполняться только на один головной узел и используя hello `oozie` команды из сеанса SSH требуется служба toohello hello URL-адрес. Этот URL-адрес можно получить из Ambari с помощью hello следующую команду:

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

Эта команда возвращает значение аналогичные toohello, выполнив команду, которая содержит URL-адрес toouse hello для внутренних с hello `oozie` команды:

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

Дополнительные сведения о работе с Ambari REST API hello см. в разделе [монитор и управлять HDInsight с помощью API-интерфейса REST Ambari hello](hdinsight-hadoop-manage-ambari-rest-api.md).

### <a name="accessing-other-node-types"></a>Доступ к узлам других типов

Можно подключиться toonodes, которые не напрямую доступны через Интернет hello с помощью hello следующие методы:

* **SSH**: после подключения tooa головного узла с помощью SSH, можно использовать SSH от узлов tooother tooconnect hello головного узла в кластере hello. Дополнительные сведения см. в разделе hello [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) документа.

* **Туннель SSH**: при необходимости tooaccess веб-службы, размещенной на один из узлов hello, которые не предоставляются toohello Интернета, необходимо использовать туннель SSH. Дополнительные сведения см. в разделе hello [использовать туннель SSH с HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) документа.

* **Виртуальная сеть Azure**: Если кластера является частью виртуальной сети Azure, любой ресурс на HDInsight hello же виртуальной сети можно получить доступ всем узлам в кластере hello. Дополнительные сведения см. в разделе hello [HDInsight, расширять и с помощью виртуальной сети Azure](hdinsight-extend-hadoop-virtual-network.md) документа.

## <a name="how-toocheck-on-a-service-status"></a>Как toocheck на состояние службы

toocheck hello состояния служб, работающих на hello головного узла, используйте hello Ambari веб-интерфейса или hello Ambari REST API.

### <a name="ambari-web-ui"></a>Веб-интерфейс Ambari

Hello Ambari веб-интерфейс пользователя может быть просмотрен на https://CLUSTERNAME.azurehdinsight.net. Замените **CLUSTERNAME** с hello имя кластера. Если необходимо, введите учетные данные пользователя hello HTTP для кластера. имя пользователя HTTP по умолчанию Hello **администратора** hello пароль — hello пароль при создании кластера hello.

При поступлении на странице приветствия Ambari, перечислены услуги hello установлен hello левой стороны страницы приветствия.

![Установленные службы](./media/hdinsight-high-availability-linux/services.png)

Существует набор значков, которые могут появиться Далее состояние tooindicate tooa службы. Все оповещения, связанные с tooa службы можно просмотреть при помощи hello **оповещения** ссылку вверху hello страницы приветствия. Дополнительные сведения о его можно выбрать tooview каждой службы.

Страница службы hello предоставляет информацию о hello состояние и конфигурация каждой службы, он не предоставляет сведения, на котором выполняется служба hello головного узла на. tooview этой информации, используйте hello **узлов** ссылку вверху hello страницы приветствия. На этой странице отображаются узлы, находящиеся в кластере hello, в том числе hello головного узла.

![список узлов](./media/hdinsight-high-availability-linux/hosts.png)

Выбор hello ссылку для одного из головного узла hello отображает hello служб и компонентов, работающих на этом узле.

![Состояние компонента](./media/hdinsight-high-availability-linux/nodeservices.png)

Дополнительные сведения об использовании Ambari см. в разделе [мониторинг и управление ими HDInsight с помощью hello Ambari веб-интерфейса](hdinsight-hadoop-manage-ambari.md).

### <a name="ambari-rest-api"></a>Ambari REST API

Hello Ambari REST API доступен через hello Интернета. открытые шлюза Hello HDInsight обрабатывает маршрутизации запросов toohello головного узла, на котором в настоящее время размещается hello REST API.

Можно использовать следующие команды toocheck hello состояния службы через API-Интерфейс REST Ambari hello hello:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* Замените **пароль** с паролем учетной записи пользователя (администратор) hello HTTP.
* Замените **CLUSTERNAME** с именем hello hello кластера.
* Замените **SERVICENAME** именем hello hello службы требуется toocheck hello состояние.

Например, toocheck hello состояние hello **HDFS** на кластер с именем **mycluster**, с паролем **пароль**, следует использовать hello следующую команду:

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

Hello ответ — примерно toohello следующие JSON:

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

Hello URL-адрес показывает, что служба hello в данный момент запущена на головной узел с именем **hn0 CLUSTERNAME**.

Hello состояние показывает, что выполняется служба hello, или **STARTED**.

Если вы не знаете, на кластере hello установленных служб, можно использовать hello, следующая команда tooretrieve списка:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

Дополнительные сведения о работе с Ambari REST API hello см. в разделе [монитор и управлять HDInsight с помощью API-интерфейса REST Ambari hello](hdinsight-hadoop-manage-ambari-rest-api.md).

#### <a name="service-components"></a>Компоненты служб

Службы могут включать компоненты, которые нужно состояние hello toocheck по отдельности. Например HDFS содержит компонент NameNode hello. tooview сведения о компоненте, hello команда будет выглядеть:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

Если вы не знаете, какие компоненты, предоставляемые службой, можно использовать hello, следующая команда tooretrieve списка:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-tooaccess-log-files-on-hello-head-nodes"></a>Как tooaccess файлы журнала на hello головного узла

### <a name="ssh"></a>SSH

При подключенном tooa головного узла через SSH, файлы журнала можно найти в разделе **/var/log**. Например, в папке **/var/log/hadoop-yarn/yarn** содержатся журналы для YARN.

Каждый головной узел может привести уникальный журнал, поэтому следует проверить журналы на обоих hello.

### <a name="sftp"></a>SFTP

Можно подключиться с помощью SSH File Transfer Protocol hello или защиты файла передачи протокол SFTP головного узла toohello и загрузки файлов журнала hello напрямую.

Аналогичные toousing клиент SSH, при подключении toohello кластера, необходимо указать hello SSH учетной записи имя пользователя и hello SSH адрес кластера hello. Например, `sftp username@mycluster-ssh.azurehdinsight.net`. Указать hello пароль для учетной записи hello при появлении запроса или предоставить открытый ключ, с помощью hello `-i` параметра.

После подключения отобразится строка `sftp>` . С помощью этой строки можно переходить в другие каталоги, отправлять и скачивать файлы. Следующие команды hello изменить toohello каталогов, например, **/var/log/hadoop/hdfs** каталог и затем загрузить все файлы в каталоге hello.

    cd /var/log/hadoop/hdfs
    get *

Список доступных команд, введите `help` в hello `sftp>` строки.

> [!NOTE]
> Существуют также графические интерфейсы, позволяющие toovisualize hello файловой системы при подключении с помощью SFTP. Например [MobaXTerm](http://mobaxterm.mobatek.net/) позволяет toobrowse hello файловой системы, с помощью примерно tooWindows интерфейс обозревателя.

### <a name="ambari"></a>Ambari

> [!NOTE]
> файлы, с помощью Ambari журнала tooaccess, необходимо использовать туннель SSH. Hello веб-интерфейсы для отдельных служб hello не предоставляются открыто на hello Интернета. Сведения об использовании туннель SSH см. в разделе hello [использование SSH туннелирование](hdinsight-linux-ambari-ssh-tunnel.md) документа.

Hello Ambari веб-интерфейса выберите службу hello, вы хотите tooview журналы (например, YARN). Затем с помощью **быстрые ссылки** tooselect какие hello tooview головного узла в журналах.

![Использование быстрого связывает tooview журналы](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-tooconfigure-hello-node-size"></a>Как tooconfigure hello размер узла

размер Hello узла может быть выбран только во время создания кластера. Можно найти список hello различных размеров виртуальных Машин для HDInsight на hello [HDInsight странице цен](https://azure.microsoft.com/pricing/details/hdinsight/).

При создании кластера, можно указать размер hello hello узлов. Hello следующее руководство по как с помощью размер hello toospecify hello [портал Azure][preview-portal], [Azure PowerShell][azure-powershell], и hello [Azure CLI][azure-cli]:

* **Портал Azure**: при создании кластера, можно задать размер hello hello кластере узлов hello:

    ![Изображение мастера создания кластера с выбором размера узла](./media/hdinsight-high-availability-linux/headnodesize.png)

* **Azure CLI**: при использовании hello `azure hdinsight cluster create` команды можно задать размер hello hello head, рабочего процесса и ZooKeeper узлов с помощью hello `--headNodeSize`, `--workerNodeSize`, и `--zookeeperNodeSize` параметров.

* **Azure PowerShell**: при использовании hello `New-AzureRmHDInsightCluster` командлета, можно задать размер hello hello head, рабочий и ZooKeeper узлов с помощью hello `-HeadNodeVMSize`, `-WorkerNodeSize`, и `-ZookeeperNodeSize` параметров.

## <a name="next-steps"></a>Дальнейшие действия

Используйте следующие ссылки toolearn больше о действиях, упомянутые в этом документе hello.

* [Справочник по REST Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [Установка и настройка hello Azure CLI](../cli-install-nodejs.md)
* [Установка и настройка Azure PowerShell](/powershell/azure/overview)
* [Управление кластерами HDInsight с помощью Ambari](hdinsight-hadoop-manage-ambari.md)
* [«Подготовка кластеров HDInsight на основе Linux»](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
