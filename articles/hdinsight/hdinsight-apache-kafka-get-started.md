---
title: "aaaStart с Kafka Apache - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toocreate Kafka Apache кластера в Azure HDInsight. Узнайте, как toocreate разделы, подписчиков и потребителей."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 43585abf-bec1-4322-adde-6db21de98d7f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: b93299d88dc2cf9a9764662509308ff75fd74474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a>Приступая к работе с Apache Kafka (предварительная версия) в HDInsight

Узнайте, как toocreate и использовать [Apache Kafka](https://kafka.apache.org) кластера Azure HDInsight. Kafka — это распределенная платформа потоковой передачи с открытым кодом, которая доступна в HDInsight. Он часто используется как брокер обмена сообщениями, как она предоставляет функциональность, аналогичную tooa публикации подписки очереди сообщений.

> [!NOTE]
> Сейчас в HDInsight доступны две версии Kafka: 0.9.0 (HDInsight 3.4) и 0.10.0 (HDInsight 3.5 и 3.6). Hello в этом документе предполагается, что вы используете Kafka на HDInsight 3.6.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a>Создание кластера Kafka

Используйте следующие шаги toocreate Kafka в кластере HDInsight hello.

1. Из hello [портал Azure](https://portal.azure.com)выберите **+ создать**, **аналитики + аналитика**, а затем выберите **HDInsight**.
   
    ![Создание кластера HDInsight](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. Из **основы**, введите hello следующую информацию:

    * **Имя кластера**: hello имя кластера HDInsight hello.
    * **Подписки**: выберите toouse hello подписки.
    * **Кластер пользователя для входа** и **входа пароль кластера**: hello входа при доступе к hello кластера по протоколу HTTPS. Можно использовать эти учетные данные tooaccess службы как hello Ambari веб-интерфейса или REST API.
    * **Secure Shell (SSH) username**: hello имя входа, используемое при доступе к hello кластера через SSH. По умолчанию hello пароль является hello то же, что пароль имени входа hello кластера.
    * **Группа ресурсов**: hello ресурсов группы toocreate hello кластера.
    * **Расположение**: hello регион Azure toocreate hello кластера.
   
 ![Выберите подписку.](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. Выберите **кластера типа**, и выполнив hello набора значений из **конфигурации кластера**:
   
    * **Тип кластера**: Kafka.

    * **Версия**: Kafka 0.10.0 (HDI 3.6).

    * **Ценовая категория кластера**: "Стандартный".
     
 Наконец, используйте hello **выберите** кнопку toosave параметры.
     
 ![Выбор типа кластера](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. После выбора типа hello кластера использовать hello __выберите__ tooset hello кластера тип кнопки. Затем используйте hello __Далее__ кнопку toofinish базовой конфигурации.

5. В колонке **Хранилище** выберите или создайте учетную запись хранения. Hello в данном пошаговом руководстве можно оставьте hello другие поля в значения по умолчанию hello. Используйте hello __Далее__ кнопку toosave хранилища конфигурации.

    ![Задайте параметры учетной записи хранилища hello для HDInsight](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. Из __приложения (необязательно)__выберите __Далее__ toocontinue. Для этого примера приложения не требуются.

7. Из __размер кластера__выберите __Далее__ toocontinue.

    > [!WARNING]
    > доступность tooguarantee Kafka на HDInsight, кластер должен содержать по крайней мере три рабочих узлов.

    ![Набор hello Kafka размер кластера](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > Hello **дисков на рабочий узел** элементов управления для ввода hello масштабируемость Kafka на HDInsight. См. дополнительные сведения о [настройке объема хранилища и степени масштабируемости Kafka в HDInsight](hdinsight-apache-kafka-scalability.md).

8. Из __Дополнительные параметры__выберите __Далее__ toocontinue.

9. Из hello **Сводка**, проверьте конфигурацию hello для hello кластера. Используйте hello __изменить__ связывает toochange все параметры, которые являются неправильными. Наконец используйте the__Create__ кнопку toocreate hello кластера.
   
    ![Сводка по конфигурации кластера](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > Он может занять too20 минут toocreate hello кластера.

## <a name="connect-toohello-cluster"></a>Подключите кластер toohello

> [!IMPORTANT]
> При выполнении hello, выполнив действия, необходимо использовать такой клиент SSH. Дополнительные сведения см. в разделе hello [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) документа.

В клиентском приложении используйте SSH tooconnect toohello кластера:

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

Замените **SSHUSER** с именем пользователя SSH hello, указанный во время создания кластера. Замените **CLUSTERNAME** с именем hello hello кластера.

При появлении запроса введите hello пароль, используемый для hello SSH учетной записи.

См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="getkafkainfo"></a>Получение сведений узла Zookeeper и Broker hello

При работе с Kafka, необходимо знать два значения узла; Hello *Zookeeper* узлов и hello *Broker* узлов. Эти узлы используются с hello Kafka API и многие hello программ, поставляемых вместе с Kafka.

Используйте следующие переменные среды toocreate шаги, которые содержат сведения об узле hello hello. Эти переменные используются в hello в данном пошаговом руководстве.

1. Из кластера toohello подключения SSH, используйте hello следующая команда tooinstall hello `jq` программы. Эта программа используется tooparse документов JSON и используется при получении сведений о хосте broker hello:
   
    ```bash
    sudo apt -y install jq
    ```

2. переменные среды hello tooset сведениями получено из Ambari hello используйте следующие команды:

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > Задать `CLUSTERNAME=` toohello имя hello Kafka кластера. Задать `PASSWORD=` toohello пароль имени входа (для администратора), используемый при создании кластера hello.

    Hello следующий текст является примером hello содержимое `$KAFKAZKHOSTS`:
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    Hello следующий текст является примером hello содержимое `$KAFKABROKERS`:
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > Hello `cut` команда является список используемых tootrim hello записей узлов tootwo узлов. Полный список tooprovide hello узлов не обязательно при создании потребителя Kafka или производителем.
   
    > [!WARNING]
    > Не следует полагаться на hello сведения, возвращаемые из этого сеанса tooalways быть точным. При масштабировании кластера hello новый брокеры добавляются или удаляются. Если происходит сбой и заменяется узла, может измениться hello имя узла для узла hello.
    >
    > Незадолго до его использовать tooensure имеют недопустимые данные, должны извлекать сведения hello Zookeeper и broker узлов.

## <a name="create-a-topic"></a>Создание раздела

Kafka хранит потоки данных в категориях, называемых *разделами*. В SSH подключения tooa кластера головному узлу используйте сценарий, в состав Kafka toocreate раздела:

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

Эта команда устанавливает подключение с помощью узла hello, хранящихся в tooZookeeper `$KAFKAZKHOSTS`и затем создать Kafka раздел с именем **тестирования**. Вы можете подтвердить эту статью hello был создан с помощью hello следующие статьи, посвященные toolist сценария:

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

Hello выходные данные этой команды список Kafka разделов, который содержит hello **тестирования** раздела.

## <a name="produce-and-consume-records"></a>Создание и использование записей

Kafka хранит *записи* в разделах. Записи создаются *производителями*, а используются *потребителями*. Производители извлекают записи из *брокеров* Kafka. Каждый рабочий узел в кластере HDInsight — это брокер Kafka.

Используйте следующие шаги toostore записи в разделе тестирования hello, созданной ранее и затем читать их с помощью объекта-получателя hello.

1. Из сеанса SSH hello используйте сценарий, предоставленный службой Kafka toowrite записей toohello раздела:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    Вы не возвращаются toohello запрос после этой команды. Вместо этого введите несколько текстовых сообщений, а затем использовать **сочетание клавиш Ctrl + C** toostop отправки toohello раздела. Каждая строка отправляется как отдельная запись.

2. Используйте сценарий, в состав Kafka tooread записи из раздела hello:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    Эта команда извлекает записи hello из раздела hello и отображает их. С помощью `--from-beginning` сообщает toostart hello потребителя с начала hello hello потока, поэтому загружаются все записи.

3. Используйте __сочетание клавиш Ctrl + C__ toostop hello потребителя.

## <a name="producer-and-consumer-api"></a>API производителя и потребителя

Вы можете также программно создавать и использовать записей с помощью hello [Kafka API-интерфейсы](http://kafka.apache.org/documentation#api). toobuild Java производителя и потребителя, используйте hello, выполнив действия из среды разработки.

> [!IMPORTANT]
> Необходимо иметь следующие компоненты, установленные в среде разработки hello.
>
> * [Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) или эквивалент, например OpenJDK.
>
> * [Apache Maven](http://maven.apache.org/)
>
> * SSH-клиента и hello `scp` команды. Дополнительные сведения см. в разделе hello [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) документа.

1. Загрузить примеры hello из [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started). Например производителем и потребителем hello, используйте проект hello в hello `Producer-Consumer` каталога. Данный пример содержит следующие классы hello.
   
    * **Запустите** -начинается hello потребителя или производителем.

    * **Производитель** -раздел toohello 1 000 000 записей хранилищ.

    * **Потребитель** -считывает записи из раздела hello.

2. toocreate JAR-файл пакета, изменение расположения toohello каталоги hello `Producer-Consumer` hello каталог и использовать следующую команду:

    ```
    mvn clean package
    ```

    Эта команда создает каталог с именем `target`, который содержит файл с именем `kafka-producer-consumer-1.0-SNAPSHOT.jar`.

3. Используйте hello следующими командами toocopy hello `kafka-producer-consumer-1.0-SNAPSHOT.jar` кластера HDInsight tooyour файла:
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    Замените **SSHUSER** пользователю hello SSH для кластера и замените **CLUSTERNAME** с hello имя кластера. При появлении запроса введите пароль hello hello пользователя SSH.

4. Здравствуйте, один раз `scp` команды завершения копирования файла hello, подключите toohello кластер с помощью SSH. Используйте следующие команды toowrite записей toohello тестировать раздел hello.

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. После завершения процесса hello, используйте следующую команду tooread из раздела hello hello:
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    чтение, а также количество записей, записей Hello отображается. Вы можете увидеть несколько более 1 000 000, регистрируются в журнале как отправлено несколько раздел toohello записи, с помощью скрипта на предыдущем шаге.

6. Используйте __сочетание клавиш Ctrl + C__ tooexit hello потребителя.

### <a name="multiple-consumers"></a>Несколько потребителей

При считывании записей объект-получатель Kafka использует группу объектов-получателей. Использование hello же группы с несколькими потребителями результаты нагрузки балансировки операций чтения из раздела. Каждый пользователь в группе hello получает часть записей hello. toosee, этот процесс в действии hello используйте следующие шаги:

1. Открытие нового SSH сеанса toohello кластера, у вас есть два из них. В каждом сеансе использовать hello следующие toostart потребителя с hello таким же Идентификатором группы потребителей:
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    Эта команда запускает объекта-получателя с помощью идентификатора группы hello `mygroup`.

    > [!NOTE]
    > Использование команд hello в hello [получить hello Zookeeper и Broker сведения об узле](#getkafkainfo) tooset раздел `$KAFKABROKERS` для этого сеанса SSH.

2. Смотрите, как каждый сеанс счетчики hello получаемые им записи из раздела hello. всего Hello обоих сеансов следует hello же, как ранее полученный от одного потребителя.

Использование клиентов в одной группе осуществляется при помощи hello секций для раздела hello приветствия. Для hello `test` раздел, созданный ранее, он имеет восемь секции. Если открыть восьми сеансов SSH и запуска объекта-получателя во всех сеансах, каждый потребитель считывает записи из одной секции для раздела hello.

> [!IMPORTANT]
> Число экземпляров потребителя, входящих в группу потребителей, должно соответствовать числу секций. В этом примере одной группе потребителей может содержать вверх tooeight потребителей, так как это hello количество секций в разделе hello. Но у вас может быть несколько групп объектов-получателей, в каждую из которых входит не более восьми из них.

Записей, хранимых в Kafka хранятся в порядке hello, в котором они поступают в секции. tooachieve в упорядоченной доставки для записей *внутри секции*, создать группу потребителей, где hello число экземпляров потребителя соответствует hello число секций. tooachieve в упорядоченной доставки для записей *hello раздела*, создать группу потребителей с помощью только одного потребителя экземпляра.

## <a name="streaming-api"></a>API для потоковой передачи

Hello потоковой передачи API была добавлена tooKafka в версии 0.10.0; более ранних версиях используют Apache Spark или ураган для обработки потока.

1. Если это еще не сделано, Загрузите примеры hello из [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour среды разработки. Hello пример потоковой передачи, используйте проект hello в hello `streaming` каталога.
   
    Этот проект содержит только один класс `Stream`, который считывает записи из hello `test` раздел создан ранее. Он выполняет подсчет слов hello чтения и передает каждый tooa раздел word и счетчик с именем `wordcounts`. Hello `wordcounts` раздел создается позднее в этом разделе.

2. Из командной строки hello в среде разработки, изменить расположение каталогов toohello hello `Streaming` каталог, а затем используйте hello, следующая команда toocreate JAR-файл пакета:

    ```bash
    mvn clean package
    ```

    Эта команда создает каталог с именем `target`, который содержит файл с именем `kafka-streaming-1.0-SNAPSHOT.jar`.

3. Используйте hello следующими командами toocopy hello `kafka-streaming-1.0-SNAPSHOT.jar` кластера HDInsight tooyour файла:
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    Замените **SSHUSER** пользователю hello SSH для кластера и замените **CLUSTERNAME** с hello имя кластера. При появлении запроса введите пароль hello hello пользователя SSH.

4. Здравствуйте, один раз `scp` команды завершения копирования файла hello, подключитесь toohello кластера с помощью SSH и воспользуйтесь hello, следующая команда toocreate hello `wordcounts` раздела:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. Теперь можно запустите hello потоковой передачи процесса с помощью hello следующую команду:
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    Эта команда запускает hello потоковой передачи процесса в фоновом режиме hello.

6. Используйте hello следующая команда toohello сообщения toosend `test` раздела. Эти сообщения обрабатываются hello пример потоковой передачи:
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. Используйте hello следующие выходные данные команды tooview hello записывается toohello `wordcounts` раздел по hello потоковой передачи процесса:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > tooview hello данных, необходимо сообщить ключом hello tooprint hello и toouse десериализатор hello hello ключ и значение. Имя ключа Hello — слово hello и значение ключа hello содержится счетчик hello.
   
    Hello выходных данных аналогичные toohello следующий текст:
   
        dwarfs  13635
        ago     13664
        snow    13636
        dwarfs  13636
        ago     13665
        a       13803
        ago     13666
        a       13804
        ago     13667
        ago     13668
        jumped  13640
        jumped  13641
        a       13805
        snow    13637
   
    > [!NOTE]
    > Hello счетчик увеличивается каждый раз, когда встречается слово.

7. Использовать hello __сочетание клавиш Ctrl + C__ tooexit hello потребителя, а затем использовать hello `fg` команда toobring hello потоковой передачи переднего плана задней toohello фоновой задачи. Используйте __сочетание клавиш Ctrl + C__ tooexit он также.

## <a name="delete-hello-cluster"></a>Удалить кластер hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Устранение неполадок

Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Дальнейшие действия

В этом документе вы узнали основы работы с Apache Kafka на HDInsight hello. Используйте следующие toolearn Дополнительные сведения о работе с Kafka hello.

* [High availability of your data with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-high-availability.md) (Высокий уровень доступности данных с Apache Kafka (предварительная версия) в HDInsight)
* [Configure storage and scalability for Apache Kafka on HDInsight](hdinsight-apache-kafka-scalability.md) (Настройка объема хранилища и степени масштабируемости для Apache Kafka в HDInsight)
* [Документация по Apache Kafka](http://kafka.apache.org/documentation.html) на сайте kafka.apache.org
* [Используйте MirrorMaker toocreate реплику Kafka в HDInsight](hdinsight-apache-kafka-mirroring.md)
* [Совместное использование Apache Kafka (предварительная версия) и Storm в HDInsight](hdinsight-apache-storm-with-kafka.md)
* [Совместное использование Apache Spark и Kafka (предварительная версия) в HDInsight](hdinsight-apache-spark-with-kafka.md)
* [Подключение через виртуальную сеть Azure tooKafka](hdinsight-apache-kafka-connect-vpn-gateway.md)
