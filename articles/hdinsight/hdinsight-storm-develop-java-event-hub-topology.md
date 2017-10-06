---
title: "события aaaProcess из концентраторов событий с Storm на HDInsight с помощью Java | Документы Microsoft"
description: "Дополнительные сведения, создание концентраторов событий данных из топологии Java Storm tooprocess Maven."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 453fa7b0-c8a6-413e-8747-3ac3b71bed86
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/13/2017
ms.author: larryfr
ms.openlocfilehash: 6506f5bc8f6ab0e29350c071a3f84433382038e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a>Обработка событий из службы концентраторов событий Azure с помощью Storm в HDInsight (Java)

Узнайте, как toouse концентраторов событий Azure с Storm на HDInsight. В этом примере использует компоненты на основе Java tooread и запись данных в концентраторы событий Azure.

Концентраторы событий Azure позволяет tooprocess значительные объемы данных из веб-сайтов, приложений и устройств. Hello spout концентратора событий позволяет легко toouse Apache Storm на HDInsight tooanalyze эти данные в режиме реального времени. Можно также написать tooEvent данных концентраторов из Storm с помощью приветствия винта концентраторов событий.

## <a name="prerequisites"></a>Предварительные требования

* Кластер Apache Storm в кластере HDInsight версии 3.6. Дополнительные сведения см. в статье [Руководство по Apache Storm в HDInsight: начало работы с анализом больших объемов данных в HDInsight с помощью примеров Storm Starter](hdinsight-apache-storm-tutorial-get-started-linux.md).

    > [!IMPORTANT]
    > Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [Концентратор событий Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

* Пакет [Oracle Java Developer Kit (JDK) версии 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) или аналогичный пакет, например [OpenJDK](http://openjdk.java.net/).

* [Maven](https://maven.apache.org/download.cgi) — это система сборки проектов Java.

* Текстовый редактор либо интегрированная среда разработки (IDE).

    > [!NOTE]
    > В редакторе или интегрированной среде разработки могут быть предусмотрены специальные функциональные возможности для работы с Maven, не описанные в настоящем документе. Сведения о возможностях hello среды редактирования документации hello hello продукта, которую вы используете.

    * Клиент SSH. Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

* Hello `ssh` и `scp` команд. Это кластер HDInsight toohello toocopy используемых файлов. В Windows вы можете получить их через Bash в Windows 10.

## <a name="understanding-hello-example"></a>Основные сведения о примере hello

Hello [hdinsight java-storm eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) пример содержит две топологии:

Hello `resources/writer.yaml` топологии записывает случайные данные tooan концентратор событий Azure. Hello данные формируются hello `DeviceSpout` компонента, и идентификатор случайных устройства и устройства. Определенное устройство получает команду на передачу идентификатора строки и числового значения.

Три `resources/reader.yaml` топологии считывает данные из концентратора событий (hello данные, записанные в EventHubWriter,) выполняет синтаксический анализ данных JSON hello, а затем регистрирует hello `deviceId` и `deviceValue` данных.

Hello данные форматируются как документ JSON перед его записи tooEvent концентратора и при считывании модулем чтения hello он анализируется из JSON и в кортежи. Hello JSON имеет следующий формат:

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a>Конфигурация проекта

Hello `POM.xml` файл содержит сведения о конфигурации для этого проекта Maven. Ниже приведены интересные участки Hello.

#### <a name="event-hub-components"></a>Компоненты концентратора событий

Hello компонент, который считывает и записывает концентраторов событий tooAzure расположен в hello [HDInsight репозитория](https://github.com/hdinsight/mvn-rep). Здравствуйте, следующие разделы в hello `POM.xml` компонентами hello загрузки файлов из этого репозитория

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a>Hello EventHubs Storm Spout зависимостей

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

Этот XML-документ определяет зависимости для hello eventhubs пакет, который содержит spout на чтение из концентраторов событий и молнии для записи tooit.

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

Этот XML-документ настраивает hello toogenerate выходные файлы проекта Java 8, который используется с HDInsight 3.5 или более поздней версии.

#### <a name="hello-maven-shade-plugin"></a>Здравствуйте, maven оттенок подключаемого модуля.

```xml
<!-- build an uber jar -->
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-shade-plugin</artifactId>
<version>2.3</version>
<configuration>
    <transformers>
    <!-- Keep us from getting a can't overwrite file error -->
    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer"/>
    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer"/>
    </transformers>
    <!-- Keep us from getting a bad signature error -->
    <filters>
    <filter>
        <artifact>*:*</artifact>
        <excludes>
            <exclude>META-INF/*.SF</exclude>
            <exclude>META-INF/*.DSA</exclude>
            <exclude>META-INF/*.RSA</exclude>
        </excludes>
    </filter>
    </filters>
</configuration>
<executions>
    <execution>
    <phase>package</phase>
    <goals>
        <goal>shade</goal>
    </goals>
    </execution>
</executions>
</plugin>
```

Этот XML-документ настраивает hello решения toopackage hello вывода в полный jar. Hello JAR-файл содержит код проекта hello и необходимые зависимости. Он также используется для:

* Переименование файлов лицензии для hello зависимости.
* Исключения групп безопасности и подписей.
* Убедитесь, что несколько реализаций hello же интерфейс объединяются в одну запись.

Эти параметры конфигурации предотвращают ошибки во время выполнения.

#### <a name="topology-definitions"></a>Определения топологии

В этом примере используется hello [определен](https://storm.apache.org/releases/1.1.0/flux.html) framework. Эта платформа использует YAML toodefine hello топологии. Hello основное преимущество состоит в том, что вы не являетесь жесткого кодирования топологии hello в коде Java. Поскольку определение hello YAML, его можно изменить перед отправкой топологии hello без необходимости toorecompile все.

__writer.yaml__:

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure hello Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.write.policy.name}"
      - "${eventhub.write.policy.key}"
      - "${eventhub.namespace}"
      - "servicebus.windows.net"
      - "${eventhub.name}"

spouts:
  - id: "device-emulator-spout"
    className: "com.microsoft.example.DeviceSpout"
    parallelism: ${eventhub.partitions}

bolts:
  - id: "eventhub-bolt"
    className: "org.apache.storm.eventhubs.bolt.EventHubBolt"
    constructorArgs:
      - ref: "eventhubbolt-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through hello components
streams:
  - name: "spout -> eventhub" # just a string used for logging
    from: "device-emulator-spout"
    to: "eventhub-bolt"
    grouping:
        type: SHUFFLE

  - name: "spout -> logger"
    from: "device-emulator-spout"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

__reader.yaml__:

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure hello Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.read.policy.name}"
      - "${eventhub.read.policy.key}"
      - "${eventhub.namespace}"
      - "${eventhub.name}"
      - ${eventhub.partitions}

spouts:
  - id: "eventhub-spout"
    className: "org.apache.storm.eventhubs.spout.EventHubSpout"
    constructorArgs:
      - ref: "eventhubspout-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

bolts:
  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

  # Parses from JSON into tuples
  - id: "parser-bolt"
    className: "com.microsoft.example.ParserBolt"
    parallelism: ${eventhub.partitions}

# How data flows through hello components
streams:
  - name: "spout -> parser" # just a string used for logging
    from: "eventhub-spout"
    to: "parser-bolt"
    grouping:
        type: SHUFFLE

  - name: "parser -> log-bolt"
    from: "parser-bolt"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

#### <a name="tell-hello-topology-about-event-hub"></a>Расскажите о концентратора событий hello топологии

Во время выполнения hello `dev.properties` файл является используется toopass hello концентратора событий конфигурации toohello топологии. Hello следующий пример — содержимое по умолчанию hello hello файла:

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a>Настройка переменных среды

Hello следующие переменные среды можно задать при установке Java и hello JDK на рабочей станции разработки. Тем не менее необходимо проверить, они существуют, и что они содержат правильные значения hello для вашей системы.

* **JAVA_HOME** -должен указывать toohello каталог, где установлен hello среда выполнения Java (JRE). Например, при распределении Unix или Linux, возможно только значение, схожее слишком`/usr/lib/jvm/java-7-oracle`. В Windows он будет иметь значение, схожее слишком`c:\Program Files (x86)\Java\jre1.7`
* **ПУТЬ** -должна содержать hello, следующие пути:

  * **JAVA_HOME** (или эквивалентный путь hello)
  * **JAVA_HOME\bin** (или эквивалентный путь hello)
  * Hello каталог для установки Maven

## <a name="configure-event-hub"></a>Настройка концентраторов Event Hub

Концентраторы событий — hello источника данных для этого примера. Используйте следующие шаги toocreate концентратора событий hello.

1. Из hello [классический портал Azure](https://manage.windowsazure.com)выберите **NEW** > **Service Bus** > **концентратора событий**  >  **Настраиваемое создание**.

2. На hello **добавить новый концентратор событий** экране, введите **имя концентратора событий**. Выберите hello **область** toocreate hello концентратора и затем создать пространство имен или выберите существующий. Наконец, нажмите кнопку hello **стрелка** toocontinue.

    ![страница мастера 1](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > Выберите hello же **расположение** как ваш Storm задержка tooreduce сервера HDInsight и цены.

3. На hello **Настройка концентратора событий** экране, введите hello **секции количество** и **хранение сообщений** значения. В этом примере числу разделов присвойте значение 10, а хранению сообщений — 1. Обратите внимание hello число секций, поскольку это значение требуется более поздней версии.

    ![страница мастера 2](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. После концентратора событий hello hello создан, выберите пространство имен, выберите **концентраторов событий**, а затем выберите концентратор событий hello, которое было создано ранее.
5. Выберите **Настройка**, затем создайте два новых политик доступа с помощью hello следующую информацию:

    <table>
    <tr><th>Имя</th><th>Разрешения</th></tr>
    <tr><td>Модуль записи</td><td>Отправка</td></tr>
    <tr><td>читатель.</td><td>Прослушивание</td></tr>
    </table>

    После создания разрешения hello выберите hello **Сохранить** значок hello нижней части страницы приветствия. Эти политики общего доступа используется tooread и записать tooEvent концентратора.

    ![политики](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. После сохранения политики hello использовать hello **генератор ключей общего доступа** hello нижней части страницы приветствия tooretrieve ключ hello hello **записи** и **чтения** политики. Сохраните эти значения.

## <a name="download-and-build-hello-project"></a>Загрузка и построение проекта hello

1. Загрузите проект hello из GitHub: [hdinsight java-storm eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub). Можно загрузить пакет hello в виде ZIP-архив, или использовать [git](https://git-scm.com/) tooclone проекта hello локально.

2. Изменение hello `dev.properties` файл с конфигурацией hello для концентратора событий.

3. Используйте следующие toobuild и пакет проекта hello hello.

        mvn package

    Эта команда загружает необходимые зависимости построения, и затем пакеты hello проекта. Hello выходные данные, хранящиеся в hello **/target-** каталог как **EventHubExample 1.0-SNAPSHOT.jar**.

## <a name="test-locally"></a>Локальное тестирование

Поскольку эти топологии только чтение и запись tooEvent концентраторы, можно проверить их локально в том случае, если у вас есть [среды разработки Storm](http://storm.apache.org/releases/current/Setting-up-development-environment.html). Используйте следующие шаги toorun локально в среде разработки hello hello.

1. Запустите средство записи hello:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. Запустите средство чтения hello:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * `--local`: Топология выполнения hello в локальном режиме (без распределенных).
> * `-R /writer.yaml`: Загрузки определения топологии hello из hello `resources` упакованных в банке hello. Если топология hello представляет собой файл hello локальной файловой системе, укажите путь tooit hello как последний параметр hello.
> * `--filter dev.properties`: Используется содержимое hello `dev.properties` toofill в значениях hello в определениях топологии hello. Например, `${eventhub.read.policy.name}`.

Выходные данные выглядят toohello журнал консоли при выполнении локально. Используйте __Ctrl + C__ toostop hello топологии.

## <a name="deploy-hello-topologies"></a>Hello топологии развертывания

1. Использование SCP toocopy hello jar пакета tooyour кластера HDInsight. Замените имя пользователя hello пользователя SSH для кластера. Замените ИМЯ_КЛАСТЕРА hello имя кластера HDInsight:

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    Если используется пароль для учетной записи SSH, не запрошенные tooenter hello пароль. При использовании ключа SSH с учетной записью hello, может потребоваться toouse hello `-i` параметр toospecify hello путь toohello файл ключа. Например, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`

    Эта команда копирует hello файл toohello домашний каталог пользователя SSH в кластере hello.

2. После завершения передачи файла hello используйте кластер HDInsight toohello tooconnect SSH. Замените **USERNAME** hello имя входа SSH. Замените **CLUSTERNAME** именем кластера HDInsight.

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > Если используется пароль для учетной записи SSH, не запрошенные tooenter hello пароль. При использовании ключа SSH с учетной записью hello, может потребоваться toouse hello `-i` параметр toospecify hello путь toohello файл ключа. Hello следующем примере загружаются hello закрытый ключ из `~/.ssh/id_rsa`:
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. Используйте следующие команды toostart hello топологии hello:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * `--remote`: Отправляет toohello топологии hello Nimbus службу, которая запускает его на hello рабочих узлов в кластере hello.

4. tooview hello в журнал данных, перейдите в раздел toohttps://CLUSTERNAME.azurehdinsight.net/stormui, где __CLUSTERNAME__ — hello имя кластера HDInsight. Выберите топологии hello и детализацию toohello компонентов. Выберите hello __порт__ входа для экземпляра tooview компонента данных журнала.

5. Используйте следующие команды toostop hello топологии hello.

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a>Удаление кластера

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Дальнейшие действия

* [Примеры топологий для Storm в HDInsight](hdinsight-storm-example-topology.md)
