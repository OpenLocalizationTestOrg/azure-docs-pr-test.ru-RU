---
title: "aaaCreate MapReduce Java для Hadoop - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse приложения MapReduce Apache Maven toocreate на языке Java, запустите его с Hadoop в Azure HDInsight."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
ms.assetid: 9ee6384c-cb61-4087-8273-fb53fa27c1c3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 903a57a482395f7da79002188399a4d6288ff0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a>Разработка программ MapReduce на Java для Hadoop в HDInsight

Узнайте, как toouse приложения MapReduce Apache Maven toocreate на языке Java, запустите его с Hadoop в Azure HDInsight.

> [!NOTE]
> Этот пример в последний раз был протестирован с помощью HDInsight 3.6.

## <a name="prerequisites"></a>Предварительные требования

* Пакет [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 или более поздней версии (или эквивалентный пакет, например OpenJDK).
    
    > [!NOTE]
    > Для HDInsight 3.4 и более ранних версий используйте Java 7. В HDInsight 3.5 и более поздних версиях используется Java 8.

* [Apache Maven](http://maven.apache.org/)

## <a name="configure-development-environment"></a>Настройка среды разработки

Hello следующие переменные среды можно задать при установке Java и hello JDK. Тем не менее необходимо проверить, они существуют, и что они содержат правильные значения hello для вашей системы.

* `JAVA_HOME`-должен указывать toohello каталог, где установлен hello среда выполнения Java (JRE). Например, в системе OS X, Unix или Linux, он должен иметь значение аналогичные слишком`/usr/lib/jvm/java-7-oracle`. В Windows он будет иметь значение, схожее слишком`c:\Program Files (x86)\Java\jre1.7`

* `PATH`-должен содержать hello, следующие пути:
  
  * `JAVA_HOME`(или эквивалентный путь hello)

  * `JAVA_HOME\bin`(или эквивалентный путь hello)

  * Hello каталог для установки Maven

## <a name="create-a-maven-project"></a>Создание проекта Maven

1. Сеанс терминала или командной строки в среде разработки измените каталоги toohello место toostore этого проекта.

2. Используйте hello `mvn` команду, которая устанавливается вместе с Maven, toogenerate hello формирование шаблонов для проекта hello.

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > Если вы используете PowerShell, необходимо заключить hello `-D` параметров в двойные кавычки.
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    Эта команда создает каталог с именем hello, заданным hello `artifactID` параметра (**wordcountjava** в этом примере.) В этом каталоге содержатся hello следующих элементов:

   * `pom.xml`-hello [модель объекта проекта (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) , содержащий сведения и сведения о конфигурации используется toobuild hello проекта.

   * `src`-hello каталог, содержащий приложение hello.

3. Удалить hello `src/test/java/org/apache/hadoop/examples/apptest.java` файла. Он не используется в этом примере.

## <a name="add-dependencies"></a>Добавление зависимостей

1. Изменить hello `pom.xml` и добавьте следующий текст внутри hello hello `<dependencies>` раздела:
   
   ```xml
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-examples</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-client-common</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-common</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
   ```

    Это означает, что требуются библиотеки (перечисленные в параметре &lt;artifactId\>) определенной версии (указанной в параметре &lt;version\>). Во время компиляции эти зависимости загружаются из репозитория Maven по умолчанию hello. Можно использовать hello [поиска репозитория Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview дополнительные.
   
    Hello `<scope>provided</scope>` сообщает Maven, эти зависимости, не должно быть упаковано с помощью приложения hello оговоренных кластером HDInsight hello во время выполнения.

    > [!IMPORTANT]
    > Здравствуй, используемой должен соответствовать версии hello присутствует в кластере Hadoop. Дополнительные сведения о версиях см. в разделе hello [управление версиями компонента HDInsight](hdinsight-component-versioning.md) документа.

2. Добавьте следующие toohello hello `pom.xml` файла. Этот текст должен находиться внутри hello `<project>...</project>` теги в файле hello, например между `</dependencies>` и `</project>`.

   ```xml
    <build>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
            <transformers>
                <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                </transformer>
            </transformers>
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
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.6.1</version>
            <configuration>
            <source>1.8</source>
            <target>1.8</target>
            </configuration>
        </plugin>
        </plugins>
    </build>
   ```

    Hello первый подключаемый модуль настраивает hello [подключаемого модуля оттенок Maven](http://maven.apache.org/plugins/maven-shade-plugin/), который будет использоваться toobuild uberjar (иногда называемых fatjar), который содержит зависимости, необходимые для приложения hello. Он также препятствует дублированию лицензий в рамках пакета jar hello, что может вызвать проблемы в некоторых системах.

    второй подключаемый модуль Hello настраивает hello целевой версии Java.

    > [!NOTE]
    > Для HDInsight 3.4 и более ранних версий используйте Java 7. В HDInsight 3.5 и более поздних версиях используется Java 8.

3. Сохранить hello `pom.xml` файла.

## <a name="create-hello-mapreduce-application"></a>Создание приложения hello MapReduce

1. Go toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` каталога и переименования hello `App.java` файла слишком`WordCount.java`.

2. Откройте hello `WordCount.java` файл в текстовом редакторе и замените содержимое hello hello следующий текст:
   
    ```java
    package org.apache.hadoop.examples;

    import java.io.IOException;
    import java.util.StringTokenizer;
    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.fs.Path;
    import org.apache.hadoop.io.IntWritable;
    import org.apache.hadoop.io.Text;
    import org.apache.hadoop.mapreduce.Job;
    import org.apache.hadoop.mapreduce.Mapper;
    import org.apache.hadoop.mapreduce.Reducer;
    import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
    import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
    import org.apache.hadoop.util.GenericOptionsParser;

    public class WordCount {

        public static class TokenizerMapper
            extends Mapper<Object, Text, Text, IntWritable>{

        private final static IntWritable one = new IntWritable(1);
        private Text word = new Text();

        public void map(Object key, Text value, Context context
                        ) throws IOException, InterruptedException {
            StringTokenizer itr = new StringTokenizer(value.toString());
            while (itr.hasMoreTokens()) {
            word.set(itr.nextToken());
            context.write(word, one);
            }
        }
    }

    public static class IntSumReducer
            extends Reducer<Text,IntWritable,Text,IntWritable> {
        private IntWritable result = new IntWritable();

        public void reduce(Text key, Iterable<IntWritable> values,
                            Context context
                            ) throws IOException, InterruptedException {
            int sum = 0;
            for (IntWritable val : values) {
            sum += val.get();
            }
            result.set(sum);
            context.write(key, result);
        }
    }

    public static void main(String[] args) throws Exception {
        Configuration conf = new Configuration();
        String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
        if (otherArgs.length != 2) {
            System.err.println("Usage: wordcount <in> <out>");
            System.exit(2);
        }
        Job job = new Job(conf, "word count");
        job.setJarByClass(WordCount.class);
        job.setMapperClass(TokenizerMapper.class);
        job.setCombinerClass(IntSumReducer.class);
        job.setReducerClass(IntSumReducer.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);
        FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
        FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
        System.exit(job.waitForCompletion(true) ? 0 : 1);
        }
    }
    ```
   
    Имя пакета hello уведомление `org.apache.hadoop.examples` и имя класса hello `WordCount`. При отправке задания MapReduce hello использовать эти имена.

3. Сохраните файл hello.

## <a name="build-hello-application"></a>Создание приложения hello

1. Изменить toohello `wordcountjava` каталога, если вы еще не существует.

2. Используйте следующую команду, toobuild БАНКЕ файла, содержащего приложения hello hello.

   ```
   mvn clean package
   ```

    Эта команда удаляет все предыдущие артефактов сборки, загружает все зависимости, которые не уже установлены, и затем собирает и приложение hello пакета.

3. После hello завершения выполнения команды hello `wordcountjava/target` каталог содержит файл с именем `wordcountjava-1.0-SNAPSHOT.jar`.
   
   > [!NOTE]
   > Hello `wordcountjava-1.0-SNAPSHOT.jar` файл uberjar, который содержит не только задания WordCount hello, однако также требует зависимости, которые hello задания во время выполнения.

## <a id="upload"></a>Отправка hello jar

Используйте следующие команды tooupload hello jar файл toohello HDInsight головному узлу hello.

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for hello cluster. Replace __CLUSTERNAME__ with hello HDInsight cluster name.

Эта команда копирует файлы hello из hello локальной системы toohello головного узла. Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="run"></a>Запустить задание MapReduce hello в Hadoop

1. Подключиться с помощью SSH tooHDInsight. Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Из сеанса SSH hello используйте следующие команды toorun hello MapReduce приложения hello:
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    Эта команда запускает hello приложения WordCount MapReduce. входной файл Hello `/example/data/gutenberg/davinci.txt`, и выходной каталог hello `/example/data/wordcountout`. Входной файл hello и выходные данные, хранимые toohello хранилища по умолчанию для кластера hello.

3. После завершения задания hello, используйте следующие результаты выполнения команды tooview hello hello:
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    Должно появиться список ключевых слов и количества с аналогичные toohello значения следующий текст:
   
        zeal    1
        zelus   1
        zenith  2

## <a id="nextsteps"></a>Дальнейшие действия

В этом документе вы узнали как toodevelop задание Java MapReduce. См. следующие документы для других способов toowork с HDInsight hello.

* [Использование Hive с HDInsight][hdinsight-use-hive]
* [Использование Pig с HDInsight][hdinsight-use-pig]
* [Использование MapReduce с HDInsight](hdinsight-use-mapreduce.md)

Дополнительные сведения см. также: hello [центра разработчиков Java](https://azure.microsoft.com/develop/java/).

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[powershell-PSCredential]: http://social.technet.microsoft.com/wiki/contents/articles/4546.working-with-passwords-secure-strings-and-credentials-in-windows-powershell.aspx

