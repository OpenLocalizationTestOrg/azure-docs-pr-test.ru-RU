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
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a><span data-ttu-id="e23a5-103">Разработка программ MapReduce на Java для Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="e23a5-103">Develop Java MapReduce programs for Hadoop on HDInsight</span></span>

<span data-ttu-id="e23a5-104">Узнайте, как toouse приложения MapReduce Apache Maven toocreate на языке Java, запустите его с Hadoop в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e23a5-104">Learn how toouse Apache Maven toocreate a Java-based MapReduce application, then run it with Hadoop on Azure HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="e23a5-105">Этот пример в последний раз был протестирован с помощью HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="e23a5-105">This example was most recently tested on HDInsight 3.6.</span></span>

## <span data-ttu-id="e23a5-106"><a name="prerequisites"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e23a5-106"><a name="prerequisites"></a>Prerequisites</span></span>

* <span data-ttu-id="e23a5-107">Пакет [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 или более поздней версии (или эквивалентный пакет, например OpenJDK).</span><span class="sxs-lookup"><span data-stu-id="e23a5-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="e23a5-108">Для HDInsight 3.4 и более ранних версий используйте Java 7.</span><span class="sxs-lookup"><span data-stu-id="e23a5-108">HDInsight versions 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="e23a5-109">В HDInsight 3.5 и более поздних версиях используется Java 8.</span><span class="sxs-lookup"><span data-stu-id="e23a5-109">HDInsight 3.5 and greater uses Java 8.</span></span>

* [<span data-ttu-id="e23a5-110">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="e23a5-110">Apache Maven</span></span>](http://maven.apache.org/)

## <a name="configure-development-environment"></a><span data-ttu-id="e23a5-111">Настройка среды разработки</span><span class="sxs-lookup"><span data-stu-id="e23a5-111">Configure development environment</span></span>

<span data-ttu-id="e23a5-112">Hello следующие переменные среды можно задать при установке Java и hello JDK.</span><span class="sxs-lookup"><span data-stu-id="e23a5-112">hello following environment variables may be set when you install Java and hello JDK.</span></span> <span data-ttu-id="e23a5-113">Тем не менее необходимо проверить, они существуют, и что они содержат правильные значения hello для вашей системы.</span><span class="sxs-lookup"><span data-stu-id="e23a5-113">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="e23a5-114">`JAVA_HOME`-должен указывать toohello каталог, где установлен hello среда выполнения Java (JRE).</span><span class="sxs-lookup"><span data-stu-id="e23a5-114">`JAVA_HOME` - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="e23a5-115">Например, в системе OS X, Unix или Linux, он должен иметь значение аналогичные слишком`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="e23a5-115">For example, on an OS X, Unix or Linux system, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="e23a5-116">В Windows он будет иметь значение, схожее слишком`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="e23a5-116">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="e23a5-117">`PATH`-должен содержать hello, следующие пути:</span><span class="sxs-lookup"><span data-stu-id="e23a5-117">`PATH` - should contain hello following paths:</span></span>
  
  * <span data-ttu-id="e23a5-118">`JAVA_HOME`(или эквивалентный путь hello)</span><span class="sxs-lookup"><span data-stu-id="e23a5-118">`JAVA_HOME` (or hello equivalent path)</span></span>

  * <span data-ttu-id="e23a5-119">`JAVA_HOME\bin`(или эквивалентный путь hello)</span><span class="sxs-lookup"><span data-stu-id="e23a5-119">`JAVA_HOME\bin` (or hello equivalent path)</span></span>

  * <span data-ttu-id="e23a5-120">Hello каталог для установки Maven</span><span class="sxs-lookup"><span data-stu-id="e23a5-120">hello directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="e23a5-121">Создание проекта Maven</span><span class="sxs-lookup"><span data-stu-id="e23a5-121">Create a Maven project</span></span>

1. <span data-ttu-id="e23a5-122">Сеанс терминала или командной строки в среде разработки измените каталоги toohello место toostore этого проекта.</span><span class="sxs-lookup"><span data-stu-id="e23a5-122">From a terminal session, or command line in your development environment, change directories toohello location you want toostore this project.</span></span>

2. <span data-ttu-id="e23a5-123">Используйте hello `mvn` команду, которая устанавливается вместе с Maven, toogenerate hello формирование шаблонов для проекта hello.</span><span class="sxs-lookup"><span data-stu-id="e23a5-123">Use hello `mvn` command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > <span data-ttu-id="e23a5-124">Если вы используете PowerShell, необходимо заключить hello `-D` параметров в двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="e23a5-124">If you are using PowerShell, you must enclose hello `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="e23a5-125">Эта команда создает каталог с именем hello, заданным hello `artifactID` параметра (**wordcountjava** в этом примере.) В этом каталоге содержатся hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="e23a5-125">This command creates a directory with hello name specified by hello `artifactID` parameter (**wordcountjava** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="e23a5-126">`pom.xml`-hello [модель объекта проекта (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) , содержащий сведения и сведения о конфигурации используется toobuild hello проекта.</span><span class="sxs-lookup"><span data-stu-id="e23a5-126">`pom.xml` - hello [Project Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) that contains information and configuration details used toobuild hello project.</span></span>

   * <span data-ttu-id="e23a5-127">`src`-hello каталог, содержащий приложение hello.</span><span class="sxs-lookup"><span data-stu-id="e23a5-127">`src` - hello directory that contains hello application.</span></span>

3. <span data-ttu-id="e23a5-128">Удалить hello `src/test/java/org/apache/hadoop/examples/apptest.java` файла.</span><span class="sxs-lookup"><span data-stu-id="e23a5-128">Delete hello `src/test/java/org/apache/hadoop/examples/apptest.java` file.</span></span> <span data-ttu-id="e23a5-129">Он не используется в этом примере.</span><span class="sxs-lookup"><span data-stu-id="e23a5-129">It is not used in this example.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="e23a5-130">Добавление зависимостей</span><span class="sxs-lookup"><span data-stu-id="e23a5-130">Add dependencies</span></span>

1. <span data-ttu-id="e23a5-131">Изменить hello `pom.xml` и добавьте следующий текст внутри hello hello `<dependencies>` раздела:</span><span class="sxs-lookup"><span data-stu-id="e23a5-131">Edit hello `pom.xml` file and add hello following text inside hello `<dependencies>` section:</span></span>
   
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

    <span data-ttu-id="e23a5-132">Это означает, что требуются библиотеки (перечисленные в параметре &lt;artifactId\>) определенной версии (указанной в параметре &lt;version\>).</span><span class="sxs-lookup"><span data-stu-id="e23a5-132">This defines required libraries (listed within &lt;artifactId\>) with a specific version (listed within &lt;version\>).</span></span> <span data-ttu-id="e23a5-133">Во время компиляции эти зависимости загружаются из репозитория Maven по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="e23a5-133">At compile time, these dependencies are downloaded from hello default Maven repository.</span></span> <span data-ttu-id="e23a5-134">Можно использовать hello [поиска репозитория Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview дополнительные.</span><span class="sxs-lookup"><span data-stu-id="e23a5-134">You can use hello [Maven repository search](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview more.</span></span>
   
    <span data-ttu-id="e23a5-135">Hello `<scope>provided</scope>` сообщает Maven, эти зависимости, не должно быть упаковано с помощью приложения hello оговоренных кластером HDInsight hello во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="e23a5-135">hello `<scope>provided</scope>` tells Maven that these dependencies should not be packaged with hello application, as they are provided by hello HDInsight cluster at run-time.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e23a5-136">Здравствуй, используемой должен соответствовать версии hello присутствует в кластере Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e23a5-136">hello version used should match hello version of Hadoop present on your cluster.</span></span> <span data-ttu-id="e23a5-137">Дополнительные сведения о версиях см. в разделе hello [управление версиями компонента HDInsight](hdinsight-component-versioning.md) документа.</span><span class="sxs-lookup"><span data-stu-id="e23a5-137">For more information on versions, see hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

2. <span data-ttu-id="e23a5-138">Добавьте следующие toohello hello `pom.xml` файла.</span><span class="sxs-lookup"><span data-stu-id="e23a5-138">Add hello following toohello `pom.xml` file.</span></span> <span data-ttu-id="e23a5-139">Этот текст должен находиться внутри hello `<project>...</project>` теги в файле hello, например между `</dependencies>` и `</project>`.</span><span class="sxs-lookup"><span data-stu-id="e23a5-139">This text must be inside hello `<project>...</project>` tags in hello file; for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="e23a5-140">Hello первый подключаемый модуль настраивает hello [подключаемого модуля оттенок Maven](http://maven.apache.org/plugins/maven-shade-plugin/), который будет использоваться toobuild uberjar (иногда называемых fatjar), который содержит зависимости, необходимые для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e23a5-140">hello first plugin configures hello [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/), which is used toobuild an uberjar (sometimes called a fatjar), which contains dependencies required by hello application.</span></span> <span data-ttu-id="e23a5-141">Он также препятствует дублированию лицензий в рамках пакета jar hello, что может вызвать проблемы в некоторых системах.</span><span class="sxs-lookup"><span data-stu-id="e23a5-141">It also prevents duplication of licenses within hello jar package, which can cause problems on some systems.</span></span>

    <span data-ttu-id="e23a5-142">второй подключаемый модуль Hello настраивает hello целевой версии Java.</span><span class="sxs-lookup"><span data-stu-id="e23a5-142">hello second plugin configures hello target Java version.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e23a5-143">Для HDInsight 3.4 и более ранних версий используйте Java 7.</span><span class="sxs-lookup"><span data-stu-id="e23a5-143">HDInsight 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="e23a5-144">В HDInsight 3.5 и более поздних версиях используется Java 8.</span><span class="sxs-lookup"><span data-stu-id="e23a5-144">HDInsight 3.5 and greater uses Java 8.</span></span>

3. <span data-ttu-id="e23a5-145">Сохранить hello `pom.xml` файла.</span><span class="sxs-lookup"><span data-stu-id="e23a5-145">Save hello `pom.xml` file.</span></span>

## <a name="create-hello-mapreduce-application"></a><span data-ttu-id="e23a5-146">Создание приложения hello MapReduce</span><span class="sxs-lookup"><span data-stu-id="e23a5-146">Create hello MapReduce application</span></span>

1. <span data-ttu-id="e23a5-147">Go toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` каталога и переименования hello `App.java` файла слишком`WordCount.java`.</span><span class="sxs-lookup"><span data-stu-id="e23a5-147">Go toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` directory and rename hello `App.java` file too`WordCount.java`.</span></span>

2. <span data-ttu-id="e23a5-148">Откройте hello `WordCount.java` файл в текстовом редакторе и замените содержимое hello hello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="e23a5-148">Open hello `WordCount.java` file in a text editor and replace hello contents with hello following text:</span></span>
   
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
   
    <span data-ttu-id="e23a5-149">Имя пакета hello уведомление `org.apache.hadoop.examples` и имя класса hello `WordCount`.</span><span class="sxs-lookup"><span data-stu-id="e23a5-149">Notice hello package name is `org.apache.hadoop.examples` and hello class name is `WordCount`.</span></span> <span data-ttu-id="e23a5-150">При отправке задания MapReduce hello использовать эти имена.</span><span class="sxs-lookup"><span data-stu-id="e23a5-150">You use these names when you submit hello MapReduce job.</span></span>

3. <span data-ttu-id="e23a5-151">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="e23a5-151">Save hello file.</span></span>

## <a name="build-hello-application"></a><span data-ttu-id="e23a5-152">Создание приложения hello</span><span class="sxs-lookup"><span data-stu-id="e23a5-152">Build hello application</span></span>

1. <span data-ttu-id="e23a5-153">Изменить toohello `wordcountjava` каталога, если вы еще не существует.</span><span class="sxs-lookup"><span data-stu-id="e23a5-153">Change toohello `wordcountjava` directory, if you are not already there.</span></span>

2. <span data-ttu-id="e23a5-154">Используйте следующую команду, toobuild БАНКЕ файла, содержащего приложения hello hello.</span><span class="sxs-lookup"><span data-stu-id="e23a5-154">Use hello following command toobuild a JAR file containing hello application:</span></span>

   ```
   mvn clean package
   ```

    <span data-ttu-id="e23a5-155">Эта команда удаляет все предыдущие артефактов сборки, загружает все зависимости, которые не уже установлены, и затем собирает и приложение hello пакета.</span><span class="sxs-lookup"><span data-stu-id="e23a5-155">This command cleans any previous build artifacts, downloads any dependencies that have not already been installed, and then builds and package hello application.</span></span>

3. <span data-ttu-id="e23a5-156">После hello завершения выполнения команды hello `wordcountjava/target` каталог содержит файл с именем `wordcountjava-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="e23a5-156">Once hello command finishes, hello `wordcountjava/target` directory contains a file named `wordcountjava-1.0-SNAPSHOT.jar`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e23a5-157">Hello `wordcountjava-1.0-SNAPSHOT.jar` файл uberjar, который содержит не только задания WordCount hello, однако также требует зависимости, которые hello задания во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="e23a5-157">hello `wordcountjava-1.0-SNAPSHOT.jar` file is an uberjar, which contains not only hello WordCount job, but also dependencies that hello job requires at runtime.</span></span>

## <span data-ttu-id="e23a5-158"><a id="upload"></a>Отправка hello jar</span><span class="sxs-lookup"><span data-stu-id="e23a5-158"><a id="upload"></a>Upload hello jar</span></span>

<span data-ttu-id="e23a5-159">Используйте следующие команды tooupload hello jar файл toohello HDInsight головному узлу hello.</span><span class="sxs-lookup"><span data-stu-id="e23a5-159">Use hello following command tooupload hello jar file toohello HDInsight headnode:</span></span>

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for hello cluster. Replace __CLUSTERNAME__ with hello HDInsight cluster name.

<span data-ttu-id="e23a5-160">Эта команда копирует файлы hello из hello локальной системы toohello головного узла.</span><span class="sxs-lookup"><span data-stu-id="e23a5-160">This command copies hello files from hello local system toohello head node.</span></span> <span data-ttu-id="e23a5-161">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e23a5-161">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="e23a5-162"><a name="run"></a>Запустить задание MapReduce hello в Hadoop</span><span class="sxs-lookup"><span data-stu-id="e23a5-162"><a name="run"></a>Run hello MapReduce job on Hadoop</span></span>

1. <span data-ttu-id="e23a5-163">Подключиться с помощью SSH tooHDInsight.</span><span class="sxs-lookup"><span data-stu-id="e23a5-163">Connect tooHDInsight using SSH.</span></span> <span data-ttu-id="e23a5-164">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e23a5-164">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="e23a5-165">Из сеанса SSH hello используйте следующие команды toorun hello MapReduce приложения hello:</span><span class="sxs-lookup"><span data-stu-id="e23a5-165">From hello SSH session, use hello following command toorun hello MapReduce application:</span></span>
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    <span data-ttu-id="e23a5-166">Эта команда запускает hello приложения WordCount MapReduce.</span><span class="sxs-lookup"><span data-stu-id="e23a5-166">This command starts hello WordCount MapReduce application.</span></span> <span data-ttu-id="e23a5-167">входной файл Hello `/example/data/gutenberg/davinci.txt`, и выходной каталог hello `/example/data/wordcountout`.</span><span class="sxs-lookup"><span data-stu-id="e23a5-167">hello input file is `/example/data/gutenberg/davinci.txt`, and hello output directory is `/example/data/wordcountout`.</span></span> <span data-ttu-id="e23a5-168">Входной файл hello и выходные данные, хранимые toohello хранилища по умолчанию для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="e23a5-168">Both hello input file and output are stored toohello default storage for hello cluster.</span></span>

3. <span data-ttu-id="e23a5-169">После завершения задания hello, используйте следующие результаты выполнения команды tooview hello hello:</span><span class="sxs-lookup"><span data-stu-id="e23a5-169">Once hello job completes, use hello following command tooview hello results:</span></span>
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    <span data-ttu-id="e23a5-170">Должно появиться список ключевых слов и количества с аналогичные toohello значения следующий текст:</span><span class="sxs-lookup"><span data-stu-id="e23a5-170">You should receive a list of words and counts, with values similar toohello following text:</span></span>
   
        zeal    1
        zelus   1
        zenith  2

## <span data-ttu-id="e23a5-171"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e23a5-171"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="e23a5-172">В этом документе вы узнали как toodevelop задание Java MapReduce.</span><span class="sxs-lookup"><span data-stu-id="e23a5-172">In this document, you have learned how toodevelop a Java MapReduce job.</span></span> <span data-ttu-id="e23a5-173">См. следующие документы для других способов toowork с HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="e23a5-173">See hello following documents for other ways toowork with HDInsight.</span></span>

* <span data-ttu-id="e23a5-174">[Использование Hive с HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="e23a5-174">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="e23a5-175">[Использование Pig с HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="e23a5-175">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* [<span data-ttu-id="e23a5-176">Использование MapReduce с HDInsight</span><span class="sxs-lookup"><span data-stu-id="e23a5-176">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="e23a5-177">Дополнительные сведения см. также: hello [центра разработчиков Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="e23a5-177">For more information, see also hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

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

