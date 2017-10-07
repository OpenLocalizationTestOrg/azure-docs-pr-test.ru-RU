---
title: "разделы Apache Kafka aaaMirror - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse Apache Kafka зеркального отображения компонентов toomaintain Kafka в кластере HDInsight из реплики можно использовать зеркальное отображение разделов tooa вторичного кластера."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 015d276e-f678-4f2b-9572-75553c56625b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: 5ace0251d7402d4d7d9b28726e253ce7091a87ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-mirrormaker-tooreplicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a>Подразделы MirrorMaker tooreplicate Apache Kafka с Kafka на HDInsight (Предварительная версия)

Узнайте, как toouse Apache Kafka зеркального отображения компонента tooreplicate разделы tooa вторичного кластера. Зеркальное отображение может быть выполнялся как непрерывный процесс, или использован периодически как метод переноса данных из одного кластера tooanother.

В этом примере зеркальное отображение — разделы используется tooreplicate между двумя кластерами HDInsight. Оба кластеров находится в виртуальной сети Azure в hello одного региона.

> [!WARNING]
> Зеркальное отображение не может считаться означает tooachieve отказоустойчивости. смещения tooitems Hello в разделе различаются hello источника и назначения кластеров, поэтому клиенты не могут использовать два hello попеременно.
>
> Если отказоустойчивость, следует настроить репликацию разделов hello в рамках кластера. Дополнительные сведения см. в статье по [началу работы с Kafka в HDInsight](hdinsight-apache-kafka-get-started.md).

## <a name="how-kafka-mirroring-works"></a>Как работает зеркальное отображение Kafka

Работает зеркальное отображение с помощью средства (часть Apache Kafka) tooconsume hello MirrorMaker записывает сведения в разделах, посвященных hello исходного кластера, а затем создать локальную копию hello целевом кластере. MirrorMaker использует один (или более) *потребителей* считывания hello исходного кластера и *производитель* , который записывает toohello локальной (назначение) кластера.

Привет, следующая схема иллюстрирует процесс hello зеркального отображения:

![Схема процесса зеркального отображения hello](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

Kafka Apache на HDInsight не предоставляет доступа toohello Kafka службы через hello общедоступный Интернет. Производители Kafka или потребители должны находиться в hello одной виртуальной сети Azure hello в виде узлов кластера Kafka hello. В этом примере hello Kafka источника и назначения кластеров находятся в виртуальной сети Azure. Hello следующей схеме показаны связи потоки между кластерами hello:

![Схема исходного и целевого кластеров Kafka в виртуальной сети Azure](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

Hello источника и назначения кластеров могут быть разными в hello числа узлов и секций и смещения в пределах hello разделы также различаются. Зеркальное отображение поддерживает hello значение ключа, который используется для секционирования, поэтому порядок записей сохраняются отдельно для каждого ключа.

### <a name="mirroring-across-network-boundaries"></a>Зеркальное отображение в пределах сети

Если вам требуется toomirror между кластерами Kafka в разных сетях, существует hello следующие дополнительные вопросы:

* **Шлюзы**: hello сети должны быть toocommunicate доступ на уровне TCPIP hello.

* **Разрешение имен**: hello Kafka кластеров в каждой сети должен быть другие возможности tooconnect tooeach с помощью имен узлов. Это может потребоваться на сервере доменных имен (DNS) в каждой сети, настроить toohello tooforward запросы других сетей.

    При создании виртуальной сети Azure, вместо hello, предоставленные автоматического DNS с hello сети, необходимо указать пользовательский DNS сервера и hello IP-адрес для сервера hello. После hello создания виртуальной сети вы необходимо затем создания виртуальной машине Azure, который использует этот IP-адрес, а затем установить и настроить программное обеспечение DNS на нем.

    > [!WARNING]
    > Создайте и настройте hello пользовательского DNS-сервера, перед установкой HDInsight в hello виртуальной сети. Нет никаких дополнительных настроек, необходимых для HDInsight toouse hello DNS-сервер настроен для hello виртуальной сети.

Дополнительные сведения о подключении двух виртуальных сетей Azure см. в статье [Настройка подключения между виртуальными сетями в развертывании Resource Manager с помощью PowerShell](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).

## <a name="create-kafka-clusters"></a>Создание кластеров Kafka

Можно создать виртуальную сеть Azure и Kafka кластеры вручную, но это проще toouse шаблона диспетчера ресурсов Azure. Следующие шаги toodeploy hello виртуальной сети Azure и используйте два tooyour кластеры Kafka подписки Azure.

1. Используйте hello toosign кнопки в tooAzure и Привет открыть шаблон в hello портал Azure.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    Hello шаблона Azure Resource Manager находится в каталоге **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.

    > [!WARNING]
    > доступность tooguarantee Kafka на HDInsight, кластер должен содержать по крайней мере три рабочих узлов. Этот шаблон создает кластер Kafka, содержащий три рабочих узла.

2. После записи hello toopopulate сведений на hello hello используйте **развертывания пользовательского** колонки:
    
    ![Настраиваемое развертывание в HDInsight](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * **Группа ресурсов.** Создайте новую группу ресурсов или выберите существующую. Эта группа содержит кластер HDInsight hello.

    * **Расположение**: выберите расположение территориально закрыть tooyou.
     
    * **Базовые имена кластеров**: это значение используется в качестве hello базовое имя для hello Kafka кластеров. Например, введя значение **hdi**, вы создадите кластеры с именами **source-hdi** и **dest-hdi**.

    * **Имя входа пользователя кластера**: hello имя пользователя администратора для hello источника и назначения Kafka кластеров.

    * **Имя входа пароль кластера**: hello пароль пользователя admin для hello источника и назначения Kafka кластеров.

    * **Имя пользователя SSH**: hello toocreate пользователя SSH для hello источника и назначения Kafka кластеров.

    * **Пароль SSH**: hello пароль пользователя SSH hello для hello источника и назначения Kafka кластеров.

3. Hello чтения **условий**, а затем выберите **я принимаю условия toohello, указанных выше**.

4. Наконец, проверьте **toodashboard ПИН-код** , а затем выберите **покупки**. Занимает около 20 минут toocreate hello кластеров.

После создания ресурсов hello предпринимается колонке перенаправленный tooa hello группы ресурсов, содержащий кластеров hello и панели мониторинга.

![Колонки группы ресурсов для виртуальной сети hello и кластеров](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> Обратите внимание, что имена hello hello кластеров HDInsight **базовое имя источника** и **базовым ИМЕНЕМ dest**, где базовое имя — имя hello указано toohello шаблона. Использовать эти имена на последующих этапах при подключении toohello кластеров.

## <a name="create-topics"></a>Создание разделов

1. Подключение toohello **источника** кластера с помощью SSH:

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    Замените **sshuser** с именем пользователя hello SSH, используемые при создании кластера hello. Замените **базовым ИМЕНЕМ** с базовым именем hello, используемый при создании кластера hello.

    См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Используйте hello следующими командами toofind hello Zookeeper узлов для hello исходного кластера:

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get hello zookeeper hosts for hello source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with hello password for hello cluster.

    Replace `$CLUSTERNAME` with hello name of hello source cluster.

3. toocreate a topic named `testtopic`, use hello following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. Следующая команда tooverify, hello разделе hello используйте был создан:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    содержит ответ Hello `testtopic`.

4. Hello используйте следующую информацию tooview hello Zookeeper узла для этого (hello **источника**) кластера:

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    Возвращает сведения аналогичные toohello следующий текст:

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    Сохраните эти сведения. Он используется в следующем разделе hello.

## <a name="configure-mirroring"></a>Настройка зеркального отображения

1. Подключение toohello **назначения** кластера с помощью другого сеанса SSH:

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    Замените **sshuser** с именем пользователя hello SSH, используемые при создании кластера hello. Замените **базовым ИМЕНЕМ** с базовым именем hello, используемый при создании кластера hello.

    См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Используйте hello следующая команда toocreate `consumer.properties` файл, который описывает способ toocommunicate с hello **источника** кластера:

    ```bash
    nano consumer.properties
    ```

    Используйте hello после текста как содержимое hello hello `consumer.properties` файла:

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    Замените **SOURCE_ZKHOSTS** к hello Zookeeper узлов сведения из hello **источника** кластера.

    Этот файл описывает hello потребителя сведения toouse при чтении из источника hello Kafka кластера. Дополнительные сведения о конфигурации получателя см. в [этом разделе](https://kafka.apache.org/documentation#consumerconfigs) на сайте kafka.apache.org.

    toosave hello файла, используйте **Ctrl + X**, **Y**, а затем **ввод**.

3. Прежде чем настраивать hello производитель, который обменивается данными с hello целевого кластера, необходимо найти hello broker узлов для hello **назначения** кластера. Используйте следующие команды tooretrieve hello эти сведения:

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    Замените `$PASSWORD` с паролем учетной записи (администратор) hello входа для hello кластера.

    Замените `$CLUSTERNAME` с именем hello hello целевого кластера.

    Эти команды возвращают аналогичные toohello следующие сведения:

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. Используйте hello, следуя toocreate `producer.properties` файл, который описывает как toocommunicate с hello **назначения** кластера:

    ```bash
    nano producer.properties
    ```

    Используйте hello после текста как содержимое hello hello `producer.properties` файла:

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    Замените **DEST_BROKERS** hello broker данными из предыдущего шага hello.

    Дополнительные сведения о конфигурации производителя см. в [этом разделе](https://kafka.apache.org/documentation#producerconfigs) на сайте kafka.apache.org.

## <a name="start-mirrormaker"></a>Запуск MirrorMaker

1. Из toohello подключения SSH hello **назначения** кластер, используйте hello, следуйте процедуре MirrorMaker hello toostart команды:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    Hello параметры, используемые в данном примере это:

    * **--consumer.config**: hello файл, содержащий свойства потребителя. Эти свойства являются используется toocreate потребителя, который считывает данные из hello *источника* Kafka кластера.

    * **--producer.config**: hello файл, содержащий свойства производителя. Эти свойства являются используется toocreate производитель, который записывает toohello *назначения* Kafka кластера.

    * **--белого списка**: список разделов, которые MirrorMaker выполняется репликация из кластера toohello hello источник назначения.

    * **--num.streams**: hello количество потоков toocreate потребителя.

 Во время запуска MirrorMaker возвращает сведения аналогичные toohello следующий текст:

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. Из toohello подключения SSH hello **источника** кластера, используется следующая команда toostart производитель hello и отправки сообщений toohello раздела:

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    Замените `$PASSWORD` с пароль для входа (администратор) hello для hello исходного кластера.

    Замените `$CLUSTERNAME` с именем hello hello исходного кластера.

     При переходе в пустую строку с курсором введите несколько текстовых сообщений. Раздел toohello отправляется на hello **источника** кластера. По завершении использования **сочетание клавиш Ctrl + C** tooend hello производитель процесса.

3. Из toohello подключения SSH hello **назначения** кластер, используйте **сочетание клавиш Ctrl + C** tooend hello MirrorMaker процесса. Затем используйте hello следующими командами tooverify hello, `testtopic` разделе была создана, и эти данные в разделе hello была зеркальной реплицированных toothis:

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    Замените `$PASSWORD` с пароль для входа (администратор) hello для hello целевого кластера.

    Замените `$CLUSTERNAME` с именем hello hello целевого кластера.

    Hello список разделов теперь включает `testtopic`, оно создается при MirrorMaster отражает hello раздел из кластера toohello hello источник назначения. Hello сообщения, полученные из раздела hello, так же, как введенные в исходном кластере hello hello.

## <a name="delete-hello-cluster"></a>Удалить кластер hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

С момента создания hello в данном пошаговом руководстве кластеров в Здравствуйте одной группе ресурсов Azure, можно удалить группу ресурсов hello в hello портал Azure. Удаление группы ресурсов hello удаляет все ресурсы, созданные после этого документа, hello виртуальной сети Azure и учетной записи хранения, используемые в кластерах hello.

## <a name="next-steps"></a>Дальнейшие действия

В этом документе вы узнали, как toouse MirrorMaker toocreate реплику Kafka кластера. Используйте следующие ссылки toodiscover hello других способов toowork с Kafka:

* [Документация по Apache Kafka MirrorMaker](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) на сайте cwiki.apache.org.
* [Get started with Apache Kafka on HDInsight (preview)](hdinsight-apache-kafka-get-started.md) (Приступая к работе с Apache Kafka в HDInsight (предварительная версия))
* [Совместное использование Apache Spark и Kafka (предварительная версия) в HDInsight](hdinsight-apache-spark-with-kafka.md)
* [Совместное использование Apache Kafka (предварительная версия) и Storm в HDInsight](hdinsight-apache-storm-with-kafka.md)
* [Подключение через виртуальную сеть Azure tooKafka](hdinsight-apache-kafka-connect-vpn-gateway.md)
