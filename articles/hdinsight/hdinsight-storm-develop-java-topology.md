---
title: "aaaApache Storm пример топологии Java - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toocreate Apache Storm топологии на Java, создав слово подсчета топологии."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "apache storm, пример apache storm, storm java, пример топологии storm"
ms.assetid: a8838f29-9c08-4fd9-99ef-26655d1bf6d7
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 54fa9dc3c93ddad83ac861f3101f50f80117d804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a>Создание топологии Apache Storm на языке Java

Узнайте, как toocreate топологии на основе Java применения Apache Storm. Вы создадите топологию Storm, реализующую приложение подсчета слов. Используется проект hello Maven toobuild и пакета. Затем вы узнаете, как с помощью топологии hello toodefine hello framework определен.

> [!NOTE]
> framework определен Hello Storm 0.10.0 или более поздних версий. Storm 0.10.0 доступна в HDInsight 3.3 и 3.4.

После завершения шагов hello в этом документе, можно развернуть hello топологии tooApache Storm на HDInsight.

> [!NOTE]
> Полную версию создан в этом документе примеры топологии Storm hello доступен на [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).

## <a name="prerequisites"></a>Предварительные требования

* [Java Developer Kit (JDK) версии 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* [Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): система сборки проектов для Java.

* Текстовый редактор или интегрированная среда разработки.

## <a name="configure-environment-variables"></a>Настройка переменных среды

Hello следующие переменные среды можно задать при установке Java и hello JDK. Тем не менее необходимо проверить, они существуют, и что они содержат правильные значения hello для вашей системы.

* **JAVA_HOME** -должен указывать toohello каталог, где установлен hello среда выполнения Java (JRE). Например, при распределении Unix или Linux, возможно только значение, схожее слишком`/usr/lib/jvm/java-7-oracle`. В Windows он будет иметь значение, схожее слишком`c:\Program Files (x86)\Java\jre1.7`

* **ПУТЬ** -должна содержать hello, следующие пути:

  * **JAVA_HOME** (или эквивалентный путь hello)

  * **JAVA_HOME\bin** (или эквивалентный путь hello)

  * Hello каталог для установки Maven

## <a name="create-a-maven-project"></a>Создание проекта Maven

Из командной строки hello, используйте hello следующая команда toocreate Maven проект с именем **WordCount**:

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> При использовании PowerShell параметры `-D` необходимо заключить в кавычки.
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

Эта команда создает каталог с именем `WordCount` hello текущей позиции, которая содержит базовый проект Maven. Hello `WordCount` каталог содержит hello следующих элементов:

* `pom.xml`: Содержит параметры для проекта Maven hello.
* `src\main\java\com\microsoft\example` содержит код приложения;
* `src\test\java\com\microsoft\example` содержит тесты для приложения. 

### <a name="remove-hello-generated-example-code"></a>Удалить созданные hello пример кода

Удалите тест создан hello и файлы приложения hello:

* **src\test\java\com\microsoft\example\AppTest.java**;
* **src\main\java\com\microsoft\example\App.java**.

## <a name="add-maven-repositories"></a>Добавление репозиториев Maven

HDInsight основан на hello Hortonworks Data Platform (HDP), поэтому мы рекомендуем использовать hello Hortonworks репозитория toodownload зависимостей для проектов Apache Storm. В hello __pom.xml__ файл, добавьте следующий XML-код после hello hello `<url>http://maven.apache.org</url>` строки:

```xml
<repositories>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPReleases</id>
        <name>HDP Releases</name>
        <url>http://repo.hortonworks.com/content/repositories/releases/</url>
        <layout>default</layout>
    </repository>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPJetty</id>
        <name>Hadoop Jetty</name>
        <url>http://repo.hortonworks.com/content/repositories/jetty-hadoop/</url>
        <layout>default</layout>
    </repository>
</repositories>
```

## <a name="add-properties"></a>Добавление свойств

Maven позволяет toodefine значения на уровне проекта, называются свойствами. В hello __pom.xml__, добавьте следующий текст после hello hello `</repositories>` строки:

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from hello Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

Теперь можно использовать это значение в других разделах hello `pom.xml`. Например, при определении версии hello Storm компонентов, можно использовать `${storm.version}` вместо жесткого программирования значение.

## <a name="add-dependencies"></a>Добавление зависимостей

Добавьте зависимость для компонентов Storm. Откройте hello `pom.xml` и добавьте следующий код в hello hello `<dependencies>` раздела:

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of hello jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

Во время компиляции, Maven использует этот toolook сведения `storm-core` в репозиторий Maven hello. Сначала выполняет поиск в репозитории hello на локальном компьютере. Если файлы hello не существует, Maven загружает их из открытого репозитория Maven hello и сохраняет их в локальном хранилище hello.

> [!NOTE]
> Обратите внимание hello `<scope>provided</scope>` строки в этом разделе. Этот параметр указывает Maven tooexclude **storm-core** из любые JAR-файлы, которые создаются, так как она задается системой hello.

## <a name="build-configuration"></a>Конфигурация построения

Подключаемые модули maven разрешить toocustomize hello этапы построения проекта hello. Например, способ компиляции проекта hello или как toopackage его в JAR-файл. Откройте hello `pom.xml` и добавьте следующий код непосредственно над hello hello `</project>` строки.

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

Этот раздел представляет используется tooadd подключаемые модули, ресурсы и другие параметры конфигурации сборки. Полную справочную hello **pom.xml** файла см. в разделе [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).

### <a name="add-plug-ins"></a>Добавление подключаемых модулей

Для топологий Apache Storm реализовано на языке Java, hello [подключаемый модуль Maven Exec](http://www.mojohaus.org/exec-maven-plugin/) полезно, так как она допускает tooeasily выполнение топологии hello локально в среде разработки. Добавьте следующие toohello hello `<plugins>` раздел hello `pom.xml` файл подключаемого модуля Exec Maven hello tooinclude:

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>1.4.0</version>
    <executions>
    <execution>
    <goals>
        <goal>exec</goal>
    </goals>
    </execution>
    </executions>
    <configuration>
    <executable>java</executable>
    <includeProjectDependencies>true</includeProjectDependencies>
    <includePluginDependencies>false</includePluginDependencies>
    <classpathScope>compile</classpathScope>
    <mainClass>${storm.topology}</mainClass>
    <cleanupDaemonThreads>false</cleanupDaemonThreads> 
    </configuration>
</plugin>
```

Другой полезные подключаемый модуль hello [Apache Maven компилятора, подключаемый модуль](http://maven.apache.org/plugins/maven-compiler-plugin/), который будет использоваться toochange параметры компиляции. изменения Hello hello версии Java, использующего Maven для hello исходного и конечного приложения.

* Для HDInsight __3,4 или более ранней версии__, задать hello источник и целевой too__1.7__ версии Java.

* Для HDInsight __3.5__, задать hello источник и целевой too__1.8__ версии Java.

Добавить после текста hello hello `<plugins>` раздел hello `pom.xml` файл подключаемого модуля Apache Maven компилятора hello tooinclude. В этом примере указывает 1.8, поэтому hello целевой HDInsight версии 3.5.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.3</version>
    <configuration>
    <source>1.8</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

### <a name="configure-resources"></a>Настройка ресурсов

раздел ресурсов Hello позволяет ресурсы не кода tooinclude например файлов конфигурации, необходимых компонентов в топологии hello. Например, добавьте после текста hello hello `<resources>` раздел hello "pom.xml файла.

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

В этом примере добавляется каталог ресурсов hello в корневой hello hello проекта (`${basedir}`) как расположение, содержащий ресурсы и включает hello файл с именем `log4j2.xml`. Этот файл является используется tooconfigure, какие сведения записываются hello топологии.

## <a name="create-hello-topology"></a>Создание топологии hello

Топология Apache Storm на платформе Java состоит из трех компонентов, которые необходимо создать или указать как зависимость.

* **Spouts**: считывает данные из внешних источников и выдает потоков данных в топологии hello.

* **Сита**— выполнение обработки потоков, поступающих из воронок или других сит, и создание одного или нескольких потоков.

* **Топология**: Определяет, как hello spouts и винты упорядочиваются и предоставляет точку входа hello hello топологии.

### <a name="create-hello-spout"></a>Создание hello spout

Здравствуйте tooreduce требования к настройке внешних источников данных, выполнив spout просто выдает случайных предложений. Это измененная версия spout, который входит в состав hello [примеры начального уровня Storm](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).

> [!NOTE]
> Пример spout, который считывает данные из внешнего источника данных см. следующие примеры hello:
>
> * [TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java)— пример воронки, считывающей информацию из Twitter.
> * [Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka)— воронка, считывающая информацию из Kafka.

Для hello spout, создайте файл с именем `RandomSentenceSpout.java` в hello `src\main\java\com\microsoft\example` hello каталог и использовать следующий код Java как hello содержимое:

```java
package com.microsoft.example;

import org.apache.storm.spout.SpoutOutputCollector;
import org.apache.storm.task.TopologyContext;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseRichSpout;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Values;
import org.apache.storm.utils.Utils;

import java.util.Map;
import java.util.Random;

//This spout randomly emits sentences
public class RandomSentenceSpout extends BaseRichSpout {
  //Collector used tooemit output
  SpoutOutputCollector _collector;
  //Used toogenerate a random number
  Random _rand;

  //Open is called when an instance of hello class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set hello instance collector toohello one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data toohello stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //hello sentences that are randomly emitted
    String[] sentences = new String[]{ "hello cow jumped over hello moon", "an apple a day keeps hello doctor away",
        "four score and seven years ago", "snow white and hello seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit hello sentence
    _collector.emit(new Values(sentence));
  }

  //Ack is not implemented since this is a basic example
  @Override
  public void ack(Object id) {
  }

  //Fail is not implemented since this is a basic example
  @Override
  public void fail(Object id) {
  }

  //Declare hello output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> Несмотря на то, что данная топология использует только один spout, другие могут иметь несколько, веб-канала данных из различных источников в топологию hello.

### <a name="create-hello-bolts"></a>Создание винты hello

Винты обрабатывать hello обработки данных. Эта топология включает два сита.

* **SplitSentence**: разделяет hello предложений, генерируемой **RandomSentenceSpout** на отдельные слова.

* **WordCount**— подсчитывает частоту употребления каждого слова.

> [!NOTE]
> Винты можно выполнять никаких действий, например, вычисления, сохранения или взаимодействии компонентов tooexternal.

Создайте два новых файла `SplitSentence.java` и `WordCount.java` в hello `src\main\java\com\microsoft\example` каталога. Используйте hello после текста как hello содержимое для hello файлов:

#### <a name="splitsentence"></a>SplitSentence

```java
package com.microsoft.example;

import java.text.BreakIterator;

import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class SplitSentence extends BaseBasicBolt {

  //Execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get hello sentence content from hello tuple
    String sentence = tuple.getString(0);
    //An iterator tooget each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give hello iterator hello sentence
    boundary.setText(sentence);
    //Find hello beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it toohello output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get hello word
      String word=sentence.substring(start,end);
      //If a word is whitespace characters, replace it with empty
      word=word.replaceAll("\\s+","");
      //if it's an actual word, emit it
      if (!word.equals("")) {
        collector.emit(new Values(word));
      }
    }
  }

  //Declare that emitted tuples contain a word field
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word"));
  }
}
```

#### <a name="wordcount"></a>WordCount

```java
package com.microsoft.example;

import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;

import org.apache.storm.Constants;
import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;
import org.apache.storm.Config;

// For logging
import org.apache.logging.log4j.Logger;
import org.apache.logging.log4j.LogManager;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class WordCount extends BaseBasicBolt {
  //Create logger for this class
  private static final Logger logger = LogManager.getLogger(WordCount.class);
  //For holding words and counts
  Map<String, Integer> counts = new HashMap<String, Integer>();
  //How often tooemit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default too60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used tootrigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //If it's a tick tuple, emit all words and counts
    if(tuple.getSourceComponent().equals(Constants.SYSTEM_COMPONENT_ID)
            && tuple.getSourceStreamId().equals(Constants.SYSTEM_TICK_STREAM_ID)) {
      for(String word : counts.keySet()) {
        Integer count = counts.get(word);
        collector.emit(new Values(word, count));
        logger.info("Emitting a count of " + count + " for word " + word);
      }
    } else {
      //Get hello word contents from hello tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment hello count and store it
      count++;
      counts.put(word, count);
    }
  }

  //Declare that this emits a tuple containing two fields; word and count
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word", "count"));
  }
}
```

### <a name="define-hello-topology"></a>Определение топологии hello

Топология Hello связывает hello spouts и болтов вместе в граф, который определяет порядок обмена данными между компонентами hello. Он также предоставляет указания параллелизма, которые Storm используется при создании экземпляров компонентов hello в кластере hello.

Hello следующем рисунке показана базовая диаграмма графа hello компонентов для реализации этой топологии.

![Схема отображение hello spouts и болтов упорядочение](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

tooimplement Здравствуйте топологии, создайте файл с именем `WordCountTopology.java` в hello `src\main\java\com\microsoft\example` каталога. Используйте следующий пример кода Java как hello содержимое файла hello hello.

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for hello topology
  public static void main(String[] args) throws Exception {
  //Used toobuild hello topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add hello spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add hello SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes toohello spout, and equally distributes
    //tuples (sentences) across instances of hello SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add hello counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes toohello split bolt, and
    //ensures that hello same word is sent toohello same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set toofalse toodisable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint tooset hello number of workers
      conf.setNumWorkers(3);
      //submit hello topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap hello maximum number of executors that can be spawned
      //for a component too3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used toorun locally
      LocalCluster cluster = new LocalCluster();
      //submit hello topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down hello cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a>Настройка журнала

Storm использует Apache Log4j toolog сведения. Если ведение журнала не задан, топологии hello выдает диагностические сведения. toocontrol регистрируемых сведений, создайте файл с именем `log4j2.xml` в hello `resources` каталога. Используйте следующий XML-код в виде hello содержимое файла hello hello.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
<Appenders>
    <Console name="STDOUT" target="SYSTEM_OUT">
        <PatternLayout pattern="%d{HH:mm:ss} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
</Appenders>
<Loggers>
    <Logger name="com.microsoft.example" level="trace" additivity="false">
        <AppenderRef ref="STDOUT"/>
    </Logger>
    <Root level="error">
        <Appender-Ref ref="STDOUT"/>
    </Root>
</Loggers>
</Configuration>
```

Этот XML-документ настраивает новое средство ведения журнала для hello `com.microsoft.example` класс, который включает в себя компоненты hello в данном примере топологии. Установка уровня Hello tootrace для данного средства ведения журнала, включающую в себя каких данных испускаемый компоненты в этой топологии.

Hello `<Root level="error">` раздел настраивает hello корневой уровень ведения журнала (все, что не поддерживается в `com.microsoft.example`) tooonly сведения об ошибке журнала.

Дополнительные сведения о настройке ведения журнала с помощью Log4j см. по адресу [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).

> [!NOTE]
> Storm 0.10.0 и более поздних версий использует Log4j 2.x. В предыдущих версиях Storm использовался выпуск Log4j 1.x, в котором для настройки журнала применялся другой формат. Сведения о конфигурации старые hello. в разделе [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).

## <a name="test-hello-topology-locally"></a>Топология hello тестов локально

После сохранения файлов hello, используйте hello следующая команда tootest топологии hello локально.

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

Во время их выполнения топологии hello отображает информацию о запуске. Hello следующий текст является примером count в формате word hello:

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

Этот пример журнала указывает это слово hello «и» было выдано 113 раз. Hello количество продолжает toogo вверх, пока выполняется hello топологии, поскольку hello spout постоянно выдает hello одного предложения.

Между отправлениями данных о словах и их количестве проходит 5 секунд. Hello **WordCount** настроен компонент tooonly опускать сведения о прибытии кортеж делений. Он запрашивает доставку таких кортежей каждые 5 секунд.

## <a name="convert-hello-topology-tooflux"></a>Преобразовать tooFlux топологии hello

Поток — это новая платформа с Storm 0.10.0 и более поздних версий, позволяющий конфигурации tooseparate от реализации. Компоненты по-прежнему определяются на языке Java, но определяются с помощью файла YAML hello топологии. Пакет определения топологии по умолчанию вместе с проектом или использовать отдельный файл при отправке hello топологии. При отправке tooStorm топологии hello, можно использовать переменные среды или значения toopopulate файлы конфигурации в hello YAML определения топологии.

файл YAML Hello определяет hello toouse компоненты топологии hello и hello потока данных между ними. Можно включить файл YAML как часть hello jar-файл, или можно использовать внешний файл YAML.

Дополнительные сведения о платформе Flux см. в статье, посвященной [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).

> [!WARNING]
> Из-за tooa [ошибки (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) с урагана 1.0.1, может потребоваться tooinstall [среды разработки Storm](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun топологии определен локально.

1. Переместить hello `WordCountTopology.java` файл из проекта hello. Ранее этот файл определен hello топологии, но не требуется с меняется.

2. В hello `resources` каталога, создайте файл с именем `topology.yaml`. Используйте hello после текста как hello содержимое этого файла.

        name: "wordcount"       # friendly name for hello topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for hello number of workers toocreate
        
        spouts:                 # Spout definitions
        - id: "sentence-spout"
            className: "com.microsoft.example.RandomSentenceSpout"
            parallelism: 1      # parallelism hint
        
        bolts:                  # Bolt definitions
        - id: "splitter-bolt"
            className: "com.microsoft.example.SplitSentence"
            parallelism: 1
         
        - id: "counter-bolt"
            className: "com.microsoft.example.WordCount"
            constructorArgs:
                - 10
            parallelism: 1
        
        streams:                # Stream definitions
            - name: "Spout --> Splitter" # name isn't used (placeholder for logging, UI, etc.)
            from: "sentence-spout"       # hello stream emitter
            to: "splitter-bolt"          # hello stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) toogroup on

3. Сделать следующие изменения toohello hello `pom.xml` файла.
   
   * Добавьте следующие новые зависимости в hello hello `<dependencies>` раздела:
     
        ```xml
        <!-- Add a dependency on hello Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * Добавить подключаемый модуль toohello следующие hello `<plugins>` раздела. Этот подключаемый модуль обрабатывает hello Создание пакета (jar-файл) для проекта hello и применяет определенные tooFlux некоторые преобразования при создании пакета hello.
     
        ```xml
        <!-- build an uber jar -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
                <transformers>
                    <!-- Keep us from getting a "can't overwrite file error" -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer" />
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer" />
                    <!-- We're using Flux, so refer tooit as main -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                        <mainClass>org.apache.storm.flux.Flux</mainClass>
                    </transformer>
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

   * В hello **exec maven подключаемый модуль** `<configuration>` измените значение hello `<mainClass>` слишком`org.apache.storm.flux.Flux`. Этот параметр позволяет toohandle меняется локальное выполнение топологии hello в разработке.

   * В hello `<resources>` добавьте следующие toohello hello `<includes>`. Этот XML-документ включает файл YAML hello, который определяет топологию hello в рамках проекта hello.

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-hello-flux-topology-locally"></a>Топология меняется hello тестов локально

1. Используйте следующие toocompile hello и выполните топологии меняется hello, с помощью Maven:

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    Если вы используете PowerShell hello используйте следующую команду:

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > Эта команда не выполняется, если топология использует ресурсы Storm 1.0.1. Причиной этого является ошибка [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055). Вместо этого [установить ураган в среде разработки](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) и hello используйте следующую информацию.

    Если у вас есть [установленных ураган в среде разработки](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), можно использовать следующие команды вместо hello:

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    Hello `--local` выполняется топологии hello в локальном режиме в среде разработки. Hello `-R /topology.yaml` использует hello `topology.yaml` файл ресурсов из hello jar файл toodefine hello топологии.

    Во время их выполнения топологии hello отображает информацию о запуске. После текста Hello приведен пример выходных данных hello.

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    Пакеты со сведениями журналов отправляются раз в 10 секунд.

2. Создайте копию hello `topology.yaml` файл из проекта hello. Имя нового файла hello `newtopology.yaml`. В hello `newtopology.yaml` файла, найдите следующую hello и измените значение hello `10` слишком`5`. Этот интервал hello изменения изменения между выдача пакетов слова идет от too5 10 секунд.

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. toorun hello topology, use hello following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    Или, если в среде разработки имеется Storm, вы можете выполнить следующую команду.

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    Изменение hello `/path/to/newtopology.yaml` toohello путь toohello newtopology.yaml файл, созданный на предыдущем шаге hello. Эта команда использует hello newtopology.yaml как определения топологии hello. Поскольку мы не включили hello `compile` параметр Maven использует версию hello hello проекта, созданного в предыдущих шагах.

    Здравствуйте, один раз запускается топологии, вы заметите, что hello время между обработкой пакетов порожденную изменила значение hello tooreflect в newtopology.yaml. Вы можете увидеть, можно изменить конфигурацию с помощью файла YAML без необходимости toorecompile hello топологии.

Дополнительные сведения об этих и других возможностях framework определен hello см. в разделе [меняется (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).

## <a name="trident"></a>Trident

Trident — это высокоуровневая абстракция, предоставляемая Storm. Он поддерживает обработку с отслеживанием состояний. Основное преимущество Hello Trident — что оно гарантирует каждого сообщения, вводит топологии hello обрабатывается только один раз. Без использования Trident топология только гарантирует, что каждое сообщение обрабатывается по крайней мере один раз. Существуют также другие отличия, например встроенные компоненты, которые можно использовать вместо создания сит. На самом деле элементы bolt заменяются не столь общими компонентами, например фильтрами, проекциями и функциями.

Приложения Trident можно создавать с помощью проектов Maven. Использовать hello же основные шаги, представленные ранее в этой статье — только код hello отличается. Trident также (в данный момент) нельзя с framework определен hello.

Дополнительные сведения о Trident см. в разделе hello [Обзор API Trident](http://storm.apache.org/documentation/Trident-API-Overview.html).

Пример приложения Trident см. в статье [Определение популярных тем в Twitter с помощью Apache Storm в HDInsight](hdinsight-storm-twitter-trending.md).

## <a name="next-steps"></a>Дальнейшие действия

Вы узнали, как toocreate Storm топологии с помощью Java. Теперь ознакомьтесь со следующими статьями.

* [Развертывание топологий Apache Storm в HDInsight и управление ими](hdinsight-storm-deploy-monitor-topology.md)

* [Разработка топологий для Apache Storm в HDInsight на C# с помощью Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

Другие примеры топологий Storm см. в статье [Примеры топологий и компонентов Storm для Apache Storm в HDInsight](hdinsight-storm-example-topology.md).

