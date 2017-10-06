---
title: "aaaUse Kafka Apache с Storm на HDInsight - Azure | Документы Microsoft"
description: "Платформа Apache Kafka устанавливается вместе с Apache Storm в службе HDInsight. Узнайте, как toowrite tooKafka и затем прочитать из него, используя hello KafkaBolt и KafkaSpout компоненты, предоставляемые с Storm. Также узнаете, как toouse hello toodefine framework меняется и отправить Storm топологии."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a>Совместное использование Apache Kafka (предварительная версия) и Storm в HDInsight

Узнайте, как tooread Apache Storm toouse из и записи tooApache Kafka. Этот пример также демонстрирует, как данные toosave из toohello топологии Storm HDFS-совместимой файловой системы, используемый HDInsight.

> [!NOTE]
> Hello в данном пошаговом руководстве создайте другой группы ресурсов Azure, которая содержит как Storm на HDInsight и Kafka в кластере HDInsight. Эти кластеры, что оба, расположенного внутри виртуальной сети Azure, что позволяет hello toodirectly кластер Storm взаимодействовать с hello Kafka кластера.
> 
> После завершения шагов hello в этом документе помните toodelete hello кластеров tooavoid лишних расходов.

## <a name="get-hello-code"></a>Получение кода hello

Hello код для примера hello, используемые в этом документе доступен на [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).

toocompile этого проекта требуется следующая конфигурация для среды разработки hello:

* Пакет [Java JDK](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 1.8 или более поздней версии. Для HDInsight 3.5 или более поздней версии требуется Java 8.

* [Maven 3.x](https://maven.apache.org/download.cgi)

* Такой клиент SSH (требуется hello `ssh` и `scp` команд) — сведения в разделе [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* Текстовый редактор или интегрированная среда разработки.

Hello следующие переменные среды можно задать при установке Java и hello JDK на рабочей станции разработки. Тем не менее необходимо проверить, они существуют, и что они содержат правильные значения hello для вашей системы.

* `JAVA_HOME`-должен указывать toohello каталог, где hello JDK установлен.
* `PATH`-должен содержать hello, следующие пути:
  
    * `JAVA_HOME`(или эквивалентный путь hello).
    * `JAVA_HOME\bin`(или эквивалентный путь hello).
    * Hello каталоге установки Maven.

## <a name="create-hello-clusters"></a>Создавать кластеры hello

Kafka Apache на HDInsight не предоставляет доступа toohello Kafka брокеры через общедоступный Интернет hello. Все, что Здравствуйте, обсуждения tooKafka должен находиться в одной виртуальной сети Azure hello в виде узлов hello Kafka кластера. В этом примере hello Kafka и Storm кластеры расположены в виртуальной сети Azure. Hello следующей схеме показаны связи потоки между кластерами hello:

![Схема кластеров Storm и Kafka в виртуальной сети Azure](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> Другие службы в кластере hello такие, как можно получить через SSH и Ambari hello Интернета. Дополнительные сведения о hello открытых портов, доступных с HDInsight см. в разделе [порты и URI, используемый HDInsight](hdinsight-hadoop-port-settings-for-services.md).

Можно создать виртуальную сеть Azure, Kafka, и Storm кластеры вручную, но это проще toouse шаблона диспетчера ресурсов Azure. Используйте hello следующие шаги toodeploy виртуальной сети Azure, Kafka, и Storm кластеры tooyour подписки Azure.

1. Используйте hello toosign кнопки в tooAzure и Привет открыть шаблон в hello портал Azure.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    Hello шаблона Azure Resource Manager находится в каталоге **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**. Создает hello следующие ресурсы:
    
    * Группа ресурсов Azure
    * Виртуальная сеть Azure
    * Учетная запись хранения Azure
    * Kafka в HDInsight версии 3.6 (три рабочих узла)
    * Storm в HDInsight версии 3.6 (три рабочих узла)

  > [!WARNING]
  > доступность tooguarantee Kafka на HDInsight, кластер должен содержать по крайней мере три рабочих узлов. Этот шаблон создает кластер Kafka, содержащий три рабочих узла.

2. Hello используйте следующие рекомендации toopopulate hello записей на hello **развертывания пользовательского** колонки:
   
    ![Настраиваемое развертывание в HDInsight](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * **Группа ресурсов.** Создайте новую группу ресурсов или выберите существующую. Эта группа содержит кластер HDInsight hello.
   
    * **Расположение**: выберите расположение территориально закрыть tooyou.

    * **Базовые имена кластеров**: это значение используется как базовое имя hello для кластеров Storm и Kafka hello. Например, если ввести **hdi**, будет создан кластер Storm **storm-hdi** и кластер Kafka **kafka-hdi**.
   
    * **Имя входа пользователя кластера**: hello имя пользователя администратора для hello Storm и Kafka кластеров.
   
    * **Имя входа пароль кластера**: hello пароль пользователя администратора для кластеров Storm и Kafka hello.
    
    * **Имя пользователя SSH**: hello toocreate пользователя SSH для hello Storm и Kafka кластеров.
    
    * **Пароль SSH**: hello пароль пользователя SSH hello для hello Storm и Kafka кластеров.

3. Hello чтения **условий**, а затем выберите **я принимаю условия toohello, указанных выше**.

4. Наконец, проверьте **toodashboard ПИН-код** , а затем выберите **покупки**. Занимает около 20 минут toocreate hello кластеров.

После создания ресурсов hello отображается колонке hello hello группы ресурсов.

![Колонки группы ресурсов для виртуальной сети hello и кластеров](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> Обратите внимание, что имена hello hello кластеров HDInsight **базовым ИМЕНЕМ storm** и **базовое имя kafka**, где базовое имя — имя hello указано toohello шаблона. Использовать эти имена на последующих этапах при подключении toohello кластеров.

## <a name="understanding-hello-code"></a>Общие сведения о коде hello

Этот проект содержит две топологии:

* **KafkaWriter**: определяется hello **writer.yaml** файл, в этой топологии записывает tooKafka случайных предложений, с помощью hello в состав Apache Storm KafkaBolt.

    Данная топология использует пользовательский **SentenceSpout** предложений случайных toogenerate компонента.

* **KafkaReader**: определяется hello **reader.yaml** файла, в этой топологии считывает данные из Kafka с помощью hello в состав Apache Storm KafkaSpout, то журналы hello toostdout данных.

    В этой топологии использует hello Storm HdfsBolt toowrite данные toodefault хранилища для кластера Storm hello.
### <a name="flux"></a>Flux

топологии Hello определяются с помощью [меняется](https://storm.apache.org/releases/1.1.0/flux.html). Поток был введен в Storm 0.10.x, а также конфигурация топологии hello tooseparate из кода hello. Для топологий, которые используют framework определен hello hello топологии определяется в файле YAML. Hello YAML файл может быть частью hello топологии. Он также может быть автономный файл, используемый при отправке hello топологии. Flux также поддерживает подстановку переменных во время выполнения, которая используется в этом примере.

Hello следующие параметры устанавливаются во время выполнения для следующих топологий:

* `${kafka.topic}`: имя hello hello Kafka раздел, в котором топологии hello чтения и записи.

* `${kafka.broker.hosts}`: hello размещается, отслеживающим Kafka hello и запустить на. При написании tooKafka сведения broker Hello используется hello KafkaBolt.

* `${kafka.zookeeper.hosts}`: hello узлов, выполняющееся в Zookeeper hello Kafka кластера.

Дополнительные сведения о топологиях Flux см. на странице [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).

## <a name="download-and-compile-hello-project"></a>Загрузите и скомпилируйте проект hello

1. В среде разработки загрузите проект hello из [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), откройте командную строку и измените расположение toohello каталоги, загруженный проект hello.

2. Из hello **hdinsight storm-java kafka** каталога, используйте hello следующую команду toocompile hello проекта и создайте пакет для развертывания:

  ```bash
  mvn clean package
  ```

    процесс Hello пакета создается файл с именем `KafkaTopology-1.0-SNAPSHOT.jar` в hello `target` каталога.

3. Используйте следующие команды toocopy hello пакета tooyour Storm в кластере HDInsight hello. Замените **USERNAME** с именем пользователя hello SSH для hello кластера. Замените **базовым ИМЕНЕМ** с базовым именем hello использовалась при создании кластера hello.

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    При появлении запроса введите пароль hello, используемый при создании кластеров hello.

## <a name="configure-hello-topology"></a>Настройка топологии hello

1. Используйте один из следующих методов toodiscover hello hello Kafka broker узлов:

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > Hello Bash предполагается, что `$CLUSTERNAME` содержит hello имя кластера HDInsight hello. Также предполагается, что [jq](https://stedolan.github.io/jq/) установлен. При появлении запроса введите hello пароль для учетной записи входа hello кластера.

    Hello возвращаемое значение аналогичные toohello следующий текст:

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > Хотя может быть более двух узлов брокера для кластера, не обязательно tooprovide полный список всех узлов tooclients. Достаточно указать один или два.

2. Используйте один из hello следующие методы toodiscover hello Kafka Zookeeper узлов.

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > Hello Bash предполагается, что `$CLUSTERNAME` содержит hello имя кластера HDInsight hello. Также предполагается, что [jq](https://stedolan.github.io/jq/) установлен. При появлении запроса введите hello пароль для учетной записи входа hello кластера.

    Hello возвращаемое значение аналогичные toohello следующий текст:

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > При наличии более двух узлов Zookeeper, tooprovide полный список всех узлов tooclients не обязательно. Достаточно указать один или два.

    Сохраните это значение, так как оно будет использовано позже.

3. Изменить hello `dev.properties` файл в корневой hello hello проекта. Добавьте hello брокера и Zookeeper узлов сведения toohello совпадающие строки в этом файле. Hello в примере настраивается с помощью значений образец hello hello предыдущих шагах:

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. Сохранить hello `dev.properties` файл и затем с помощью hello следующие команды tooupload его toohello Storm кластера:

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    Замените **USERNAME** с именем пользователя hello SSH для hello кластера. Замените **базовым ИМЕНЕМ** с базовым именем hello использовалась при создании кластера hello.

## <a name="start-hello-writer"></a>Запуск модуля записи hello

1. Используйте следующие tooconnect toohello Storm кластера с помощью SSH hello. Замените **USERNAME** с именем пользователя hello SSH, используемые при создании кластера hello. Замените **базовым ИМЕНЕМ** с базовым именем hello, используемый при создании кластера hello.

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    При появлении запроса введите пароль hello, используемый при создании кластеров hello.
   
    См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. В hello SSH-подключения используйте hello, следующая команда toocreate hello Kafka раздел, используемый hello топологии:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    Замените `$KAFKAZKHOSTS` с hello Zookeeper размещения информации, полученной в предыдущем разделе hello.

2. В кластер Storm toohello подключения SSH hello используйте следующие команды toostart hello записи топологии hello:

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    используются следующие параметры Hello, используемые с данной командой.

    * `org.apache.storm.flux.Flux`: Используется tooconfigure меняется и выполнение в этой топологии.

    * `--remote`: Отправьте tooNimbus топологии hello. Топология Hello распределяется по hello рабочих узлов в кластере hello.

    * `-R /writer.yaml`: Использование hello `writer.yaml` файл tooconfigure hello топологии. `-R`Указывает, что этот ресурс включен в hello jar-файл. Он находится в корне hello hello jar, поэтому `/writer.yaml` — tooit путь hello.

    * `--filter`: Заполнения записей в hello `writer.yaml` топологии с использованием значений в hello `dev.properties` файла. Например, hello значение hello `kafka.topic` запись в файле hello — используется tooreplace hello `${kafka.topic}` запись в определении топологии hello.

5. После запуска hello топологии, используйте hello следующая команда tooverify, записывает данные toohello Kafka раздела:

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    Замените `$KAFKAZKHOSTS` с hello Zookeeper размещения информации, полученной в предыдущем разделе hello.

    Эта команда использует сценарий, поставляемых с Kafka toomonitor hello раздела. Через некоторое время он запущен возвращение случайных предложения, которые были записаны toohello раздела. Hello вывода будет примерно toohello следующий пример:

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    Используйте сочетание клавиш Ctrl + c toostop hello скрипта.

## <a name="start-hello-reader"></a>Запустите средство чтения hello

1. В кластер Storm toohello сеанс SSH hello используйте следующие команды toostart hello чтения топологии hello:

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. После запуска топологии hello, откройте hello Storm пользовательского интерфейса. Этот веб-интерфейс расположен по адресу https://storm-BASENAME.azurehdinsight.net/stormui. Замените __базовым ИМЕНЕМ__ с базовым именем hello использовалась при создании кластера hello. 

    При появлении запроса, используйте имя входа администратора hello (по умолчанию, `admin`) и пароль, используемый при создании кластера hello. Можно увидеть примерно toohello веб-страницы, следующие изображения:

    ![Пользовательский интерфейс Storm](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. Hello Storm пользовательского интерфейса, выберите hello __kafka чтения__ ссылку в hello __топологии Сводка__ статьи toodisplay сведения о hello __kafka чтения__ топологии.

    ![Топология Аннотация hello Storm пользовательского веб-интерфейса](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. toodisplay сведения об экземплярах hello компонента средства ведения журнала молнии hello, выберите hello __молнии средства ведения журнала__ ссылку в hello __винты (все время)__ раздела.

    ![Средства ведения журнала молнии ссылку в разделе винты hello](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. В hello __исполнителей__ выберите ссылку в hello __порт__ столбца toodisplay запись сведений об этом экземпляре компонента hello.

    ![Ссылка Executors](./media/hdinsight-apache-storm-with-kafka/executors.png)

    Hello журнала содержит журнал hello чтение данных из раздела Kafka hello. Hello сведения в журнале hello — примерно toohello следующий текст:

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a>Остановить hello топологии

Из кластера Storm toohello сеансу SSH используйте следующие команды toostop hello Storm топологии hello:

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a>Удалить кластер hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

С момента создания hello в данном пошаговом руководстве кластеров в Здравствуйте одной группе ресурсов Azure, можно удалить группу ресурсов hello в hello портал Azure. Удаление группы ресурсов hello удаляет все ресурсы, созданные после этого документа.

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные примеры топологий, которые можно использовать со Storm в HDInsight, см. в статье [Примеры топологий и компонентов Storm для Apache Storm в HDInsight](hdinsight-storm-example-topology.md).

Сведения о развертывании и мониторинге топологий в HDInsight под управлением Linux см. в статье [Развертывание топологий Apache Storm в HDInsight под управлением Linux и управление ими](hdinsight-storm-deploy-monitor-topology-linux.md).