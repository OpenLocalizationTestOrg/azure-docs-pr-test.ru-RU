---
title: "aaaJava определяемой пользователем функции (UDF) с Hive в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как toocreate на основе Java определяемой пользователем функции (UDF), который работает с Hive. В этом примере определяемая пользователем Функция преобразует таблицу toolowercase строки текста."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 8d4f8efe-2f01-4a61-8619-651e873c7982
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 392b4cfb73299d2f6c1e8e825a4201b48d501388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a><span data-ttu-id="6d5f8-104">Работа с определяемыми пользователем функциями Java с использованием Hive в HDInsight</span><span class="sxs-lookup"><span data-stu-id="6d5f8-104">Use a Java UDF with Hive in HDInsight</span></span>

<span data-ttu-id="6d5f8-105">Узнайте, как toocreate на основе Java определяемой пользователем функции (UDF), который работает с Hive.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-105">Learn how toocreate a Java-based user-defined function (UDF) that works with Hive.</span></span> <span data-ttu-id="6d5f8-106">Hello Java определяемой пользователем функции в этом примере преобразует таблицу символов нижнего регистра tooall строки текста.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-106">hello Java UDF in this example converts a table of text strings tooall-lowercase characters.</span></span>

## <a name="requirements"></a><span data-ttu-id="6d5f8-107">Требования</span><span class="sxs-lookup"><span data-stu-id="6d5f8-107">Requirements</span></span>

* <span data-ttu-id="6d5f8-108">Кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-108">An HDInsight cluster</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="6d5f8-109">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6d5f8-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6d5f8-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

    <span data-ttu-id="6d5f8-111">Большинство действий, описываемых в этой статье, можно выполнять в кластерах как на основе Windows, так и на основе Linux.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-111">Most steps in this document work on both Windows- and Linux-based clusters.</span></span> <span data-ttu-id="6d5f8-112">Однако hello этапы tooupload hello скомпилирован кластера toohello определяемой пользователем функции и запустить его, определенных кластеров на основе tooLinux.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-112">However, hello steps used tooupload hello compiled UDF toohello cluster and run it are specific tooLinux-based clusters.</span></span> <span data-ttu-id="6d5f8-113">Tooinformation, который может использоваться с кластерами под управлением Windows, приводятся соответствующие ссылки.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-113">Links are provided tooinformation that can be used with Windows-based clusters.</span></span>

* <span data-ttu-id="6d5f8-114">Пакет [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 или более поздней версии (или эквивалентный пакет, например OpenJDK).</span><span class="sxs-lookup"><span data-stu-id="6d5f8-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)</span></span>

* [<span data-ttu-id="6d5f8-115">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="6d5f8-115">Apache Maven</span></span>](http://maven.apache.org/)

* <span data-ttu-id="6d5f8-116">Текстовый редактор или Java IDE.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-116">A text editor or Java IDE</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6d5f8-117">При создании hello Python файлы на клиенте Windows, необходимо использовать редактор, который использует LF в качестве конца строки.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-117">If you create hello Python files on a Windows client, you must use an editor that uses LF as a line ending.</span></span> <span data-ttu-id="6d5f8-118">Если вы не уверены, использует ли редактора LF или CRLF, в разделе hello [Устранение неполадок](#troubleshooting) раздел для действия по удалению hello символов CR.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-118">If you are not sure whether your editor uses LF or CRLF, see hello [Troubleshooting](#troubleshooting) section for steps on removing hello CR character.</span></span>

## <a name="create-an-example-java-udf"></a><span data-ttu-id="6d5f8-119">Создание примера определяемой пользователем функции Java</span><span class="sxs-lookup"><span data-stu-id="6d5f8-119">Create an example Java UDF</span></span> 

1. <span data-ttu-id="6d5f8-120">Из командной строки используйте следующие toocreate новый проект Maven hello.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-120">From a command line, use hello following toocreate a new Maven project:</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > <span data-ttu-id="6d5f8-121">При использовании PowerShell необходимо поместить в кавычки hello параметров.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-121">If you are using PowerShell, you must put quotes around hello parameters.</span></span> <span data-ttu-id="6d5f8-122">Например, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-122">For example, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span></span>

    <span data-ttu-id="6d5f8-123">Эта команда создает каталог с именем **exampleudf**, которая содержит проект Maven hello.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-123">This command creates a directory named **exampleudf**, which contains hello Maven project.</span></span>

2. <span data-ttu-id="6d5f8-124">После создания проекта hello удалить hello **exampleudf/src/test** каталогом, созданным в рамках проекта hello.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-124">Once hello project has been created, delete hello **exampleudf/src/test** directory that was created as part of hello project.</span></span>

3. <span data-ttu-id="6d5f8-125">Откройте hello **exampleudf/pom.xml**и заменить существующий hello `<dependencies>` запись с hello следующий XML-код:</span><span class="sxs-lookup"><span data-stu-id="6d5f8-125">Open hello **exampleudf/pom.xml**, and replace hello existing `<dependencies>` entry with hello following XML:</span></span>

    ```xml
    <dependencies>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-client</artifactId>
            <version>2.7.3</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.hive</groupId>
            <artifactId>hive-exec</artifactId>
            <version>1.2.1</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>
    ```

    <span data-ttu-id="6d5f8-126">Эти записи указывают версию hello Hadoop и Hive, входящий в состав HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-126">These entries specify hello version of Hadoop and Hive included with HDInsight 3.5.</span></span> <span data-ttu-id="6d5f8-127">Можно найти сведения о версиях hello Hadoop и Hive, предоставляемую с HDInsight hello [управление версиями компонента HDInsight](hdinsight-component-versioning.md) документа.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-127">You can find information on hello versions of Hadoop and Hive provided with HDInsight from hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

    <span data-ttu-id="6d5f8-128">Добавить `<build>` раздел перед hello `</project>` строку hello конец файла hello.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-128">Add a `<build>` section before hello `</project>` line at hello end of hello file.</span></span> <span data-ttu-id="6d5f8-129">В этом разделе, должны иметь hello следующий XML-код:</span><span class="sxs-lookup"><span data-stu-id="6d5f8-129">This section should contain hello following XML:</span></span>

    ```xml
    <build>
        <plugins>
            <!-- build for Java 1.8. This is required by HDInsight 3.5  -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.3</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
            <!-- build an uber jar -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>2.3</version>
                <configuration>
                    <!-- Keep us from getting a can't overwrite file error -->
                    <transformers>
                        <transformer
                                implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                        </transformer>
                        <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer">
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
        </plugins>
    </build>
    ```

    <span data-ttu-id="6d5f8-130">Эти записи определяют, как toobuild hello проекта.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-130">These entries define how toobuild hello project.</span></span> <span data-ttu-id="6d5f8-131">В частности, hello версию Java, hello проекте используется и как toobuild uberjar для развертывания кластера toohello.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-131">Specifically, hello version of Java that hello project uses and how toobuild an uberjar for deployment toohello cluster.</span></span>

    <span data-ttu-id="6d5f8-132">Сохраните файл hello, когда были внесены изменения hello.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-132">Save hello file once hello changes have been made.</span></span>

4. <span data-ttu-id="6d5f8-133">Переименуйте **exampleudf/src/main/java/com/microsoft/examples/App.java** слишком**ExampleUDF.java**, а затем откройте файл hello в редакторе.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-133">Rename **exampleudf/src/main/java/com/microsoft/examples/App.java** too**ExampleUDF.java**, and then open hello file in your editor.</span></span>

5. <span data-ttu-id="6d5f8-134">Замените содержимое hello hello **ExampleUDF.java** следующие hello-файл, а затем сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-134">Replace hello contents of hello **ExampleUDF.java** file with hello following, then save hello file.</span></span>

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of hello UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of hello input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If hello value is null, return a null
            if(input == null)
                return null;
            // Lowercase hello input string and return it
            return input.toLowerCase();
        }
    }
    ```

    <span data-ttu-id="6d5f8-135">Этот код реализует определяемой пользователем функции, которая принимает строковое значение и возвращает версия hello строки в нижний регистр.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-135">This code implements a UDF that accepts a string value, and returns a lowercase version of hello string.</span></span>

## <a name="build-and-install-hello-udf"></a><span data-ttu-id="6d5f8-136">Создание и установка hello определяемой пользователем функции.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-136">Build and install hello UDF</span></span>

1. <span data-ttu-id="6d5f8-137">Используйте следующие команды toocompile hello и пакета hello определяемой пользователем функции:</span><span class="sxs-lookup"><span data-stu-id="6d5f8-137">Use hello following command toocompile and package hello UDF:</span></span>

    ```bash
    mvn compile package
    ```

    <span data-ttu-id="6d5f8-138">Эта команда выполняет сборку и пакеты hello определяемой пользователем функции в hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` файла.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-138">This command builds and packages hello UDF into hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` file.</span></span>

2. <span data-ttu-id="6d5f8-139">Используйте hello `scp` команда toocopy hello файл toohello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-139">Use hello `scp` command toocopy hello file toohello HDInsight cluster.</span></span>

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    <span data-ttu-id="6d5f8-140">Замените `myuser` с hello SSH учетной записи пользователя для кластера.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-140">Replace `myuser` with hello SSH user account for your cluster.</span></span> <span data-ttu-id="6d5f8-141">Замените `mycluster` с именем кластера hello.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-141">Replace `mycluster` with hello cluster name.</span></span> <span data-ttu-id="6d5f8-142">Если вы использовали hello toosecure пароль учетной записи SSH, не требуется запрашиваемые tooenter hello пароль.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-142">If you used a password toosecure hello SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="6d5f8-143">Если используется сертификат, то может потребоваться toouse hello `-i` параметр toospecify hello файл закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-143">If you used a certificate, you may need toouse hello `-i` parameter toospecify hello private key file.</span></span>

3. <span data-ttu-id="6d5f8-144">Подключите кластер toohello с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-144">Connect toohello cluster using SSH.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="6d5f8-145">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6d5f8-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

4. <span data-ttu-id="6d5f8-146">Из сеанса SSH hello скопируйте файл tooHDInsight hello jar хранилища.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-146">From hello SSH session, copy hello jar file tooHDInsight storage.</span></span>

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-hello-udf-from-hive"></a><span data-ttu-id="6d5f8-147">Использовать hello определяемой пользователем функции из куста</span><span class="sxs-lookup"><span data-stu-id="6d5f8-147">Use hello UDF from Hive</span></span>

1. <span data-ttu-id="6d5f8-148">Используйте следующие toostart hello Beeline клиента из сеанса SSH hello hello.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-148">Use hello following toostart hello Beeline client from hello SSH session.</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="6d5f8-149">Эта команда предполагает, что используется по умолчанию hello **администратора** для учетной записи входа hello для кластера.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-149">This command assumes that you used hello default of **admin** for hello login account for your cluster.</span></span>

2. <span data-ttu-id="6d5f8-150">Как только будет выполнен переход на hello `jdbc:hive2://localhost:10001/>` запрос, введите следующие tooHive определяемой пользователем функции hello tooadd hello и вывести ее в качестве функции.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-150">Once you arrive at hello `jdbc:hive2://localhost:10001/>` prompt, enter hello following tooadd hello UDF tooHive and expose it as a function.</span></span>

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > <span data-ttu-id="6d5f8-151">Предполагается, что хранилище Azure хранилища по умолчанию для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-151">This example assumes that Azure Storage is default storage for hello cluster.</span></span> <span data-ttu-id="6d5f8-152">Если кластер использует хранилище Озера данных вместо этого, измените hello `wasb:///` значение слишком`adl:///`.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-152">If your cluster uses Data Lake Store instead, change hello `wasb:///` value too`adl:///`.</span></span>

3. <span data-ttu-id="6d5f8-153">Используйте значения tooconvert определяемой пользователем функции hello, полученные из строк регистром toolower таблицы.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-153">Use hello UDF tooconvert values retrieved from a table toolower case strings.</span></span>

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    <span data-ttu-id="6d5f8-154">Этот запрос, выбирает hello платформы устройств (Android, Windows, iOS, т. д.) из таблицы hello преобразовании случая toolower строку hello и их отображения.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-154">This query selects hello device platform (Android, Windows, iOS, etc.) from hello table, convert hello string toolower case, and then display them.</span></span> <span data-ttu-id="6d5f8-155">Hello выходные данные отображаются как toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="6d5f8-155">hello output appears similar toohello following text:</span></span>

        +----------+--+
        |   _c0    |
        +----------+--+
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        +----------+--+

## <a name="next-steps"></a><span data-ttu-id="6d5f8-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6d5f8-156">Next steps</span></span>

<span data-ttu-id="6d5f8-157">Другие способы toowork с Hive, в разделе [используйте Hive с HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="6d5f8-157">For other ways toowork with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="6d5f8-158">Дополнительные сведения о функциях Hive User-Defined см. в разделе [Hive операторы и определяемые пользователем функции](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) разделе вики-сайте Hive hello в программами.</span><span class="sxs-lookup"><span data-stu-id="6d5f8-158">For more information on Hive User-Defined Functions, see [Hive Operators and User-Defined Functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section of hello Hive wiki at apache.org.</span></span>
