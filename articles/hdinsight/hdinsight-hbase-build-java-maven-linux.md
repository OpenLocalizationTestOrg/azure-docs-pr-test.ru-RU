---
title: "Клиент aaaJava HBase - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse приложения Apache HBase Apache Maven toobuild на языке Java, затем развернуть его tooHBase на Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: 
ms.assetid: 1d1ed180-e0f4-4d1c-b5ea-72e0eda643bc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 41ef92b2900280dd59089c4fa40686c44133b337
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-java-applications-for-apache-hbase"></a><span data-ttu-id="7ad5b-103">Создание приложений Java для Apache HBase</span><span class="sxs-lookup"><span data-stu-id="7ad5b-103">Build Java applications for Apache HBase</span></span>

<span data-ttu-id="7ad5b-104">Узнайте, как toocreate [Apache HBase](http://hbase.apache.org/) приложение Java.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-104">Learn how toocreate an [Apache HBase](http://hbase.apache.org/) application in Java.</span></span> <span data-ttu-id="7ad5b-105">Затем можно используйте приложение hello с HBase на Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-105">Then use hello application with HBase on Azure HDInsight.</span></span>

<span data-ttu-id="7ad5b-106">Hello шаги в этом документе используется [Maven](http://maven.apache.org/) toocreate и построения проекта hello.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-106">hello steps in this document use [Maven](http://maven.apache.org/) toocreate and build hello project.</span></span> <span data-ttu-id="7ad5b-107">Maven — это программное обеспечение управления проектами и понимания средство, которое позволяет вам toobuild программное обеспечение, документация и отчеты для проектов Java.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-107">Maven is a software project management and comprehension tool that allows you toobuild software, documentation, and reports for Java projects.</span></span>

> [!NOTE]
> <span data-ttu-id="7ad5b-108">Hello в данном пошаговом руководстве были недавно протестированных с HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-108">hello steps in this document were most recently tested with HDInsight 3.6.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ad5b-109">Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-109">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="7ad5b-110">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7ad5b-111">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7ad5b-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="7ad5b-112">Требования</span><span class="sxs-lookup"><span data-stu-id="7ad5b-112">Requirements</span></span>

* <span data-ttu-id="7ad5b-113">[Пакет JDK для платформы Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html) версии 8 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-113">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 or later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7ad5b-114">Для HDInsight 3.5 и более поздних версий требуется Java 8.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-114">HDInsight 3.5 and greater requires Java 8.</span></span> <span data-ttu-id="7ad5b-115">Для работы более ранних версий HDInsight требуется Java 7.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-115">Earlier versions of HDInsight require Java 7.</span></span>

* [<span data-ttu-id="7ad5b-116">Maven</span><span class="sxs-lookup"><span data-stu-id="7ad5b-116">Maven</span></span>](http://maven.apache.org/)

* [<span data-ttu-id="7ad5b-117">Кластер Azure HDInsight под управлением Linux с HBase.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-117">A Linux-based Azure HDInsight cluster with HBase</span></span>](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > <span data-ttu-id="7ad5b-118">Hello в данном пошаговом руководстве были проверены с версиями кластеров HDInsight 3.4 и 3.5.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-118">hello steps in this document have been tested with HDInsight cluster versions 3.4 and 3.5.</span></span> <span data-ttu-id="7ad5b-119">значения по умолчанию Hello в примерах предназначены для кластера HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-119">hello default values provided in examples are for a HDInsight 3.5 cluster.</span></span>

## <a name="create-hello-project"></a><span data-ttu-id="7ad5b-120">Создание проекта hello</span><span class="sxs-lookup"><span data-stu-id="7ad5b-120">Create hello project</span></span>

1. <span data-ttu-id="7ad5b-121">Из командной строки hello в среде разработки, измените каталоги toohello место, куда toocreate hello проекта, например, `cd code\hbase`.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-121">From hello command line in your development environment, change directories toohello location where you want toocreate hello project, for example, `cd code\hbase`.</span></span>

2. <span data-ttu-id="7ad5b-122">Используйте hello **mvn** команду, которая устанавливается вместе с Maven, toogenerate hello формирование шаблонов для проекта hello.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-122">Use hello **mvn** command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > <span data-ttu-id="7ad5b-123">Если вы используете PowerShell, необходимо заключить hello `-D` параметров в двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-123">If you are using PowerShell, you must enclose hello `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="7ad5b-124">Эта команда создает каталог с точно такое же имя, как hello hello **artifactID** параметра (**hbaseapp** в этом примере.) В этом каталоге содержатся hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-124">This command creates a directory with hello same name as hello **artifactID** parameter (**hbaseapp** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="7ad5b-125">**pom.XML**: hello объектной модели Project ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) содержит сведения и конфигурации, используемой toobuild hello проекта.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-125">**pom.xml**:  hello Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used toobuild hello project.</span></span>
   * <span data-ttu-id="7ad5b-126">**src**: hello каталог, содержащий hello **main-java/com/microsoft/примеры** каталог, в котором создается приложение hello.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-126">**src**: hello directory that contains hello **main/java/com/microsoft/examples** directory, where you author hello application.</span></span>

3. <span data-ttu-id="7ad5b-127">Удалить hello `src/test/java/com/microsoft/examples/apptest.java` файла.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-127">Delete hello `src/test/java/com/microsoft/examples/apptest.java` file.</span></span> <span data-ttu-id="7ad5b-128">Он не используется в этом примере.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-128">It is not be used in this example.</span></span>

## <a name="update-hello-project-object-model"></a><span data-ttu-id="7ad5b-129">Обновление hello объектной модели Project</span><span class="sxs-lookup"><span data-stu-id="7ad5b-129">Update hello Project Object Model</span></span>

1. <span data-ttu-id="7ad5b-130">Изменить hello `pom.xml` и добавьте следующий код внутри hello hello `<dependencies>` раздела:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-130">Edit hello `pom.xml` file and add hello following code inside hello `<dependencies>` section:</span></span>

   ```xml
    <dependency>
        <groupId>org.apache.hbase</groupId>
        <artifactId>hbase-client</artifactId>
        <version>1.1.2</version>
    </dependency>
    <dependency>
        <groupId>org.apache.phoenix</groupId>
        <artifactId>phoenix-core</artifactId>
        <version>4.4.0-HBase-1.1</version>
    </dependency>
   ```

    <span data-ttu-id="7ad5b-131">В этом разделе показывает hello проект должен **hbase клиента** и **ядрами Финиксе** компонентов.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-131">This section indicates that hello project needs **hbase-client** and **phoenix-core** components.</span></span> <span data-ttu-id="7ad5b-132">Во время компиляции эти зависимости загружаются из репозитория Maven по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-132">At compile time, these dependencies are downloaded from hello default Maven repository.</span></span> <span data-ttu-id="7ad5b-133">Можно использовать hello [Maven центральный репозиторий поиска](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn Дополнительные сведения об этой зависимости.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-133">You can use hello [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="7ad5b-134">номер версии Hello hello hbase клиента должна совпадать hello версией, предоставляемого с кластером HDInsight HBase.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-134">hello version number of hello hbase-client must match hello version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="7ad5b-135">Используйте следующие таблицы toofind hello правильный номер версии hello.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-135">Use hello following table toofind hello correct version number.</span></span>

   | <span data-ttu-id="7ad5b-136">Версия кластера HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ad5b-136">HDInsight cluster version</span></span> | <span data-ttu-id="7ad5b-137">Toouse версия HBase</span><span class="sxs-lookup"><span data-stu-id="7ad5b-137">HBase version toouse</span></span> |
   | --- | --- |
   | <span data-ttu-id="7ad5b-138">3.2</span><span class="sxs-lookup"><span data-stu-id="7ad5b-138">3.2</span></span> |<span data-ttu-id="7ad5b-139">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="7ad5b-139">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="7ad5b-140">3.3, 3.4, 3.5 и 3.6</span><span class="sxs-lookup"><span data-stu-id="7ad5b-140">3.3, 3.4, 3.5, and 3.6</span></span> |<span data-ttu-id="7ad5b-141">1.1.2</span><span class="sxs-lookup"><span data-stu-id="7ad5b-141">1.1.2</span></span> |

    <span data-ttu-id="7ad5b-142">Дополнительные сведения о версии HDInsight и компонентов см. в разделе [Каковы hello различных Hadoop компоненты, доступные с HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="7ad5b-142">For more information on HDInsight versions and components, see [What are hello different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>

3. <span data-ttu-id="7ad5b-143">Добавьте следующий код toohello hello **pom.xml** файла.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-143">Add hello following code toohello **pom.xml** file.</span></span> <span data-ttu-id="7ad5b-144">Этот текст должен находиться внутри hello `<project>...</project>` тегов в hello файла, например, между `</dependencies>` и `</project>`.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-144">This text must be inside hello `<project>...</project>` tags in hello file, for example, between `</dependencies>` and `</project>`.</span></span>

   ```xml
    <build>
        <sourceDirectory>src</sourceDirectory>
        <resources>
        <resource>
            <directory>${basedir}/conf</directory>
            <filtering>false</filtering>
            <includes>
            <include>hbase-site.xml</include>
            </includes>
        </resource>
        </resources>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.3</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
            </configuration>
            </plugin>
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
        </plugins>
    </build>
   ```

    <span data-ttu-id="7ad5b-145">В этом разделе настраивается ресурс (`conf/hbase-site.xml`), который содержит информацию о конфигурации для HBase.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-145">This section configures a resource (`conf/hbase-site.xml`) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7ad5b-146">Также можно настроить значения конфигурации непосредственно из кода.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-146">You can also set configuration values via code.</span></span> <span data-ttu-id="7ad5b-147">См. комментарии hello в hello `CreateTable` примере.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-147">See hello comments in hello `CreateTable` example.</span></span>

    <span data-ttu-id="7ad5b-148">В этом разделе также настраивает hello [подключаемого модуля компилятора Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) и [подключаемого модуля оттенок Maven](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="7ad5b-148">This section also configures hello [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="7ad5b-149">Компилятор Hello подключаемый модуль — используется toocompile hello топологии.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-149">hello compiler plug-in is used toocompile hello topology.</span></span> <span data-ttu-id="7ad5b-150">Подключаемый модуль оттенок Hello — дублирования лицензии tooprevent используется в пакете JAR hello, построенного с Maven.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-150">hello shade plug-in is used tooprevent license duplication in hello JAR package that is built by Maven.</span></span> <span data-ttu-id="7ad5b-151">Этот подключаемый модуль является ошибкой «повторяющиеся файлы лицензии» используется tooprevent во время выполнения в кластере HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-151">This plugin is used tooprevent a "duplicate license files" error at run time on hello HDInsight cluster.</span></span> <span data-ttu-id="7ad5b-152">Использование maven оттенок подключаемого модуля с hello `ApacheLicenseResourceTransformer` реализация предотвращает ошибки hello.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-152">Using maven-shade-plugin with hello `ApacheLicenseResourceTransformer` implementation prevents hello error.</span></span>

    <span data-ttu-id="7ad5b-153">Привет, maven оттенок-подключаемый модуль также создает полный JAR-файл, содержащий все зависимости hello, необходимые для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-153">hello maven-shade-plugin also produces an uber jar that contains all hello dependencies required by hello application.</span></span>

4. <span data-ttu-id="7ad5b-154">Сохранить hello `pom.xml` файла.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-154">Save hello `pom.xml` file.</span></span>

5. <span data-ttu-id="7ad5b-155">Создайте каталог с именем `conf` в hello `hbaseapp` каталога.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-155">Create a directory named `conf` in hello `hbaseapp` directory.</span></span> <span data-ttu-id="7ad5b-156">Этот каталог является используется toohold сведения о конфигурации для подключения tooHBase.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-156">This directory is used toohold configuration information for connecting tooHBase.</span></span>

6. <span data-ttu-id="7ad5b-157">Используйте hello следующая команда конфигурации HBase hello toocopy из toohello кластер HBase hello `conf` каталога.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-157">Use hello following command toocopy hello HBase configuration from hello HBase cluster toohello `conf` directory.</span></span> <span data-ttu-id="7ad5b-158">Замените `USERNAME` с именем hello SSH имени входа.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-158">Replace `USERNAME` with hello name of your SSH login.</span></span> <span data-ttu-id="7ad5b-159">а `CLUSTERNAME` — именем кластера HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-159">Replace `CLUSTERNAME` with your HDInsight cluster name:</span></span>

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   <span data-ttu-id="7ad5b-160">Дополнительные сведения об использовании `ssh` и `scp` см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7ad5b-160">For more information on using `ssh` and `scp`, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="7ad5b-161">Создание приложения hello</span><span class="sxs-lookup"><span data-stu-id="7ad5b-161">Create hello application</span></span>

1. <span data-ttu-id="7ad5b-162">Go toohello `hbaseapp/src/main/java/com/microsoft/examples` каталога и переименования hello app.java файл слишком`CreateTable.java`.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-162">Go toohello `hbaseapp/src/main/java/com/microsoft/examples` directory and rename hello app.java file too`CreateTable.java`.</span></span>

2. <span data-ttu-id="7ad5b-163">Откройте hello `CreateTable.java` и замените существующее содержимое hello hello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-163">Open hello `CreateTable.java` file and replace hello existing contents with hello following text:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;
    import org.apache.hadoop.hbase.HTableDescriptor;
    import org.apache.hadoop.hbase.TableName;
    import org.apache.hadoop.hbase.HColumnDescriptor;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Put;
    import org.apache.hadoop.hbase.util.Bytes;

    public class CreateTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Example of setting zookeeper values for HDInsight
        // in code instead of an hbase-site.xml file
        //
        // config.set("hbase.zookeeper.quorum",
        //            "zookeepernode0,zookeepernode1,zookeepernode2");
        //config.set("hbase.zookeeper.property.clientPort", "2181");
        //config.set("hbase.cluster.distributed", "true");
        //
        //NOTE: Actual zookeeper host names can be found using Ambari:
        //curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts"

        //Linux-based HDInsight clusters use /hbase-unsecure as hello znode parent
        config.set("zookeeper.znode.parent","/hbase-unsecure");

        // create an admin object using hello config
        HBaseAdmin admin = new HBaseAdmin(config);

        // create hello table...
        HTableDescriptor tableDescriptor = new HTableDescriptor(TableName.valueOf("people"));
        // ... with two column families
        tableDescriptor.addFamily(new HColumnDescriptor("name"));
        tableDescriptor.addFamily(new HColumnDescriptor("contactinfo"));
        admin.createTable(tableDescriptor);

        // define some people
        String[][] people = {
            { "1", "Marcel", "Haddad", "marcel@fabrikam.com"},
            { "2", "Franklin", "Holtz", "franklin@contoso.com" },
            { "3", "Dwayne", "McKee", "dwayne@fabrikam.com" },
            { "4", "Rae", "Schroeder", "rae@contoso.com" },
            { "5", "Rosalie", "burton", "rosalie@fabrikam.com"},
            { "6", "Gabriela", "Ingram", "gabriela@contoso.com"} };

        HTable table = new HTable(config, "people");

        // Add each person toohello table
        //   Use hello `name` column family for hello name
        //   Use hello `contactinfo` column family for hello email
        for (int i = 0; i< people.length; i++) {
            Put person = new Put(Bytes.toBytes(people[i][0]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
            person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
            table.put(person);
        }
        // flush commits and close hello table
        table.flushCommits();
        table.close();
        }
    }
   ```

    <span data-ttu-id="7ad5b-164">Данный пример кода является hello **CreateTable** класс, который создает таблицу с именем **людей** и ее заполнение некоторых стандартных пользователей.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-164">This code is hello **CreateTable** class, which creates a table named **people** and populate it with some predefined users.</span></span>

3. <span data-ttu-id="7ad5b-165">Сохранить hello `CreateTable.java` файла.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-165">Save hello `CreateTable.java` file.</span></span>

4. <span data-ttu-id="7ad5b-166">В hello `hbaseapp/src/main/java/com/microsoft/examples` каталога, создайте файл с именем `SearchByEmail.java`.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-166">In hello `hbaseapp/src/main/java/com/microsoft/examples` directory, create a file named `SearchByEmail.java`.</span></span> <span data-ttu-id="7ad5b-167">Используйте hello после текста как hello содержимое этого файла:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-167">Use hello following text as hello contents of this file:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Scan;
    import org.apache.hadoop.hbase.client.ResultScanner;
    import org.apache.hadoop.hbase.client.Result;
    import org.apache.hadoop.hbase.filter.RegexStringComparator;
    import org.apache.hadoop.hbase.filter.SingleColumnValueFilter;
    import org.apache.hadoop.hbase.filter.CompareFilter.CompareOp;
    import org.apache.hadoop.hbase.util.Bytes;
    import org.apache.hadoop.util.GenericOptionsParser;

    public class SearchByEmail {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Use GenericOptionsParser tooget only hello parameters toohello class
        // and not all hello parameters passed (when using WebHCat for example)
        String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
        if (otherArgs.length != 1) {
            System.out.println("usage: [regular expression]");
            System.exit(-1);
        }

        // Open hello table
        HTable table = new HTable(config, "people");

        // Define hello family and qualifiers toobe used
        byte[] contactFamily = Bytes.toBytes("contactinfo");
        byte[] emailQualifier = Bytes.toBytes("email");
        byte[] nameFamily = Bytes.toBytes("name");
        byte[] firstNameQualifier = Bytes.toBytes("first");
        byte[] lastNameQualifier = Bytes.toBytes("last");

        // Create a regex filter
        RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
        // Attach hello regex filter tooa filter
        //   for hello email column
        SingleColumnValueFilter filter = new SingleColumnValueFilter(
            contactFamily,
            emailQualifier,
            CompareOp.EQUAL,
            emailFilter
        );

        // Create a scan and set hello filter
        Scan scan = new Scan();
        scan.setFilter(filter);

        // Get hello results
        ResultScanner results = table.getScanner(scan);
        // Iterate over results and print  values
        for (Result result : results ) {
            String id = new String(result.getRow());
            byte[] firstNameObj = result.getValue(nameFamily, firstNameQualifier);
            String firstName = new String(firstNameObj);
            byte[] lastNameObj = result.getValue(nameFamily, lastNameQualifier);
            String lastName = new String(lastNameObj);
            System.out.println(firstName + " " + lastName + " - ID: " + id);
            byte[] emailObj = result.getValue(contactFamily, emailQualifier);
            String email = new String(emailObj);
            System.out.println(firstName + " " + lastName + " - " + email + " - ID: " + id);
        }
        results.close();
        table.close();
        }
    }
   ```

    <span data-ttu-id="7ad5b-168">Hello **SearchByEmail** класс может быть tooquery используется для строк по адресу электронной почты.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-168">hello **SearchByEmail** class can be used tooquery for rows by email address.</span></span> <span data-ttu-id="7ad5b-169">Так как он использует регулярное выражение фильтра, чтобы обеспечить строку или регулярное выражение при использовании класса hello.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-169">Because it uses a regular expression filter, you can provide either a string or a regular expression when using hello class.</span></span>

5. <span data-ttu-id="7ad5b-170">Сохранить hello `SearchByEmail.java` файла.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-170">Save hello `SearchByEmail.java` file.</span></span>

6. <span data-ttu-id="7ad5b-171">В hello `hbaseapp/src/main/hava/com/microsoft/examples` каталога, создайте файл с именем `DeleteTable.java`.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-171">In hello `hbaseapp/src/main/hava/com/microsoft/examples` directory, create a file named `DeleteTable.java`.</span></span> <span data-ttu-id="7ad5b-172">Используйте hello после текста как hello содержимое этого файла:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-172">Use hello following text as hello contents of this file:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;

    public class DeleteTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Create an admin object using hello config
        HBaseAdmin admin = new HBaseAdmin(config);

        // Disable, and then delete hello table
        admin.disableTable("people");
        admin.deleteTable("people");
        }
    }
   ```

    <span data-ttu-id="7ad5b-173">Этот класс очищает hello HBase таблицы, созданные в этом примере отключение и удаление таблицы hello созданные hello `CreateTable` класса.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-173">This class cleans up hello HBase tables created in this example by disabling and dropping hello table created by hello `CreateTable` class.</span></span>

7. <span data-ttu-id="7ad5b-174">Сохранить hello `DeleteTable.java` файла.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-174">Save hello `DeleteTable.java` file.</span></span>

## <a name="build-and-package-hello-application"></a><span data-ttu-id="7ad5b-175">Сборки и пакет приложения hello</span><span class="sxs-lookup"><span data-stu-id="7ad5b-175">Build and package hello application</span></span>

1. <span data-ttu-id="7ad5b-176">Из hello `hbaseapp` каталога, используйте hello следующая команда toobuild JAR-файл, содержащий приложение hello:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-176">From hello `hbaseapp` directory, use hello following command toobuild a JAR file that contains hello application:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="7ad5b-177">Эта команда выполняет сборку и пакеты hello приложения в JAR-файлу.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-177">This command builds and packages hello application into a .jar file.</span></span>

2. <span data-ttu-id="7ad5b-178">Когда hello выполнения команды hello `hbaseapp/target` каталог содержит файл с именем `hbaseapp-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-178">When hello command completes, hello `hbaseapp/target` directory contains a file named `hbaseapp-1.0-SNAPSHOT.jar`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7ad5b-179">Hello `hbaseapp-1.0-SNAPSHOT.jar` файл является полный jar.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-179">hello `hbaseapp-1.0-SNAPSHOT.jar` file is an uber jar.</span></span> <span data-ttu-id="7ad5b-180">Он содержит все необходимые toorun приложений hello зависимости hello.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-180">It contains all hello dependencies required toorun hello application.</span></span>


## <a name="upload-hello-jar-and-run-jobs-ssh"></a><span data-ttu-id="7ad5b-181">Отправка hello JAR-ФАЙЛ и запустите задания (SSH)</span><span class="sxs-lookup"><span data-stu-id="7ad5b-181">Upload hello JAR and run jobs (SSH)</span></span>

<span data-ttu-id="7ad5b-182">Здравствуйте, выполнив действия, используйте `scp` toocopy hello JAR toohello первичного головного узла к HBase на HDInsight кластера.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-182">hello following steps use `scp` toocopy hello JAR toohello primary head node of your HBase on HDInsight cluster.</span></span> <span data-ttu-id="7ad5b-183">Hello `ssh` команда будет использовать tooconnect toohello кластера и выполнить пример hello непосредственно на головном узле hello.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-183">hello `ssh` command is then used tooconnect toohello cluster and run hello example directly on hello head node.</span></span>

1. <span data-ttu-id="7ad5b-184">tooupload hello jar toohello кластер, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-184">tooupload hello jar toohello cluster, use hello following command:</span></span>

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="7ad5b-185">Замените `USERNAME` с именем hello SSH имени входа.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-185">Replace `USERNAME` with hello name of your SSH login.</span></span> <span data-ttu-id="7ad5b-186">а `CLUSTERNAME` — именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-186">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

2. <span data-ttu-id="7ad5b-187">кластер HBase toohello tooconnect, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-187">tooconnect toohello HBase cluster, use hello following command:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="7ad5b-188">Замените `USERNAME` hello имя входа SSH.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-188">Replace `USERNAME` hello name of your SSH login.</span></span> <span data-ttu-id="7ad5b-189">а `CLUSTERNAME` — именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-189">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

3. <span data-ttu-id="7ad5b-190">к таблице HBase с помощью toocreate hello приложения Java, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-190">toocreate an HBase table using hello Java application, use hello following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    <span data-ttu-id="7ad5b-191">Эта команда создает таблицу HBase с именем **people** и заполняет ее данными.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-191">This command creates a HBase table named **people**, and populates it with data.</span></span>

4. <span data-ttu-id="7ad5b-192">toosearch для адресов электронной почты, которые хранятся в таблице hello, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-192">toosearch for email addresses stored in hello table, use hello following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    <span data-ttu-id="7ad5b-193">Появляется hello следующие результаты:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-193">You receive hello following results:</span></span>

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. <span data-ttu-id="7ad5b-194">Таблица toodelete hello, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-194">toodelete hello table, use hello following command:</span></span>

    

## <a name="upload-hello-jar-and-run-jobs-powershell"></a><span data-ttu-id="7ad5b-195">Отправка hello JAR-ФАЙЛ и запустите задания (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="7ad5b-195">Upload hello JAR and run jobs (PowerShell)</span></span>

<span data-ttu-id="7ad5b-196">Hello действий использовать Azure PowerShell tooupload hello JAR toohello хранилища по умолчанию для кластера HBase.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-196">hello following steps use Azure PowerShell tooupload hello JAR toohello default storage for your HBase cluster.</span></span> <span data-ttu-id="7ad5b-197">Командлеты HDInsight, то используется toorun hello примеры удаленно.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-197">HDInsight cmdlets are then used toorun hello examples remotely.</span></span>

1. <span data-ttu-id="7ad5b-198">После установки и настройки Azure PowerShell создайте файл с именем `hbase-runner.psm1`.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-198">After installing and configuring Azure PowerShell, create a file named `hbase-runner.psm1`.</span></span> <span data-ttu-id="7ad5b-199">Используйте hello после текста как hello содержимое этого файла:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-199">Use hello following text as hello contents of this file:</span></span>

   ```powershell
    <#
    .SYNOPSIS
    Copies a file toohello primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory toohello blob container for
    hello HDInsight cluster.
    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.CreateTable"
    -clusterName "MyHDInsightCluster"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "contoso.com"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "^r" -showErr
    #>

    function Start-HBaseExample {
    [CmdletBinding(SupportsShouldProcess = $true)]
    param(
    #hello class toorun
    [Parameter(Mandatory = $true)]
    [String]$className,

    #hello name of hello HDInsight cluster
    [Parameter(Mandatory = $true)]
    [String]$clusterName,

    #Only used when using SearchByEmail
    [Parameter(Mandatory = $false)]
    [String]$emailRegex,

    #Use if you want toosee stderr output
    [Parameter(Mandatory = $false)]
    [Switch]$showErr
    )

    Set-StrictMode -Version 3

    # Is hello Azure module installed?
    FindAzure

    # Get hello login for hello HDInsight cluster
    $creds=Get-Credential -Message "Enter hello login for hello cluster" -UserName "admin"

    # hello JAR
    $jarFile = "wasb:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

    # hello job definition
    $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
        -JarFile $jarFile `
        -ClassName $className `
        -Arguments $emailRegex

    # Get hello job output
    $job = Start-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobDefinition $jobDefinition `
        -HttpCredential $creds
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds
    if($showErr)
    {
    Write-Host "STDERR"
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds `
                -DisplayOutputType StandardError
    }
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds
    }

    <#
    .SYNOPSIS
    Copies a file toohello primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory toohello blob container for
    hello HDInsight cluster.
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    -Container "MyContainer"
    #>

    function Add-HDInsightFile {
        [CmdletBinding(SupportsShouldProcess = $true)]
        param(
            #hello path toohello local file.
            [Parameter(Mandatory = $true)]
            [String]$localPath,

            #hello destination path and file name, relative toohello root of hello container.
            [Parameter(Mandatory = $true)]
            [String]$destinationPath,

            #hello name of hello HDInsight cluster
            [Parameter(Mandatory = $true)]
            [String]$clusterName,

            #If specified, overwrites existing files without prompting
            [Parameter(Mandatory = $false)]
            [Switch]$force
        )

        Set-StrictMode -Version 3

        # Is hello Azure module installed?
        FindAzure

        # Get authentication for hello cluster
        $creds=Get-Credential

        # Does hello local path exist?
        if (-not (Test-Path $localPath))
        {
            throw "Source path '$localPath' does not exist."
        }

        # Get hello primary storage container
        $storage = GetStorage -clusterName $clusterName

        # Upload file toostorage, overwriting existing files if -force was used.
        Set-AzureStorageBlobContent -File $localPath `
            -Blob $destinationPath `
            -force:$force `
            -Container $storage.container `
            -Context $storage.context
    }

    function FindAzure {
        # Is there an active Azure subscription?
        $sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
        if(-not($sub))
        {
            throw "No active Azure subscription found! If you have a subscription, use hello Login-AzureRmAccount cmdlet toologin tooyour subscription."
        }
    }

    function GetStorage {
        param(
            [Parameter(Mandatory = $true)]
            [String]$clusterName
        )
        $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
        # Does hello cluster exist?
        if (!$hdi)
        {
            throw "HDInsight cluster '$clusterName' does not exist."
        }
        # Create a return object for context & container
        $return = @{}
        $storageAccounts = @{}

        # Get storage information
        $resourceGroup = $hdi.ResourceGroup
        $storageAccountName=$hdi.DefaultStorageAccount.split('.')[0]
        $container=$hdi.DefaultStorageContainer
        $storageAccountKey=(Get-AzureRmStorageAccountKey `
            -Name $storageAccountName `
        -ResourceGroupName $resourceGroup)[0].Value
        # Get hello resource group, in case we need that
        $return.resourceGroup = $resourceGroup
        # Get hello storage context, as we can't depend
        # on using hello default storage context
        $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        # Get hello container, so we know where to
        # find/store blobs
        $return.container = $container
        # Return storage accounts toosupport finding all accounts for
        # a cluster
        $return.storageAccount = $storageAccountName
        $return.storageAccountKey = $storageAccountKey

        return $return
    }
    # Only export hello verb-phrase things
    export-modulemember *-*
   ```

    <span data-ttu-id="7ad5b-200">Этот файл содержит два модуля:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-200">This file contains two modules:</span></span>

   * <span data-ttu-id="7ad5b-201">**Добавить HDInsightFile** — служат tooupload файлы toohello кластера</span><span class="sxs-lookup"><span data-stu-id="7ad5b-201">**Add-HDInsightFile** - used tooupload files toohello cluster</span></span>
   * <span data-ttu-id="7ad5b-202">**Начало HBaseExample** -используемые классы toorun hello, созданного ранее</span><span class="sxs-lookup"><span data-stu-id="7ad5b-202">**Start-HBaseExample** - used toorun hello classes created earlier</span></span>

2. <span data-ttu-id="7ad5b-203">Сохранить hello `hbase-runner.psm1` файла.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-203">Save hello `hbase-runner.psm1` file.</span></span>

3. <span data-ttu-id="7ad5b-204">Откройте новое окно Azure PowerShell, измените каталоги toohello `hbaseapp` каталога, а затем выполнения hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-204">Open a new Azure PowerShell window, change directories toohello `hbaseapp` directory, and then run hello following command:</span></span>

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    <span data-ttu-id="7ad5b-205">Изменение расположения toohello путь hello hello `hbase-runner.psm1` файла, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-205">Change hello path toohello location of hello `hbase-runner.psm1` file created earlier.</span></span> <span data-ttu-id="7ad5b-206">Эта команда регистрирует модуль hello Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-206">This command registers hello module with Azure PowerShell.</span></span>

4. <span data-ttu-id="7ad5b-207">Используйте hello следующая команда tooupload hello `hbaseapp-1.0-SNAPSHOT.jar` tooyour кластера.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-207">Use hello following command tooupload hello `hbaseapp-1.0-SNAPSHOT.jar` tooyour cluster.</span></span>

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    <span data-ttu-id="7ad5b-208">Замените `hdinsightclustername` с hello имя кластера.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-208">Replace `hdinsightclustername` with hello name of your cluster.</span></span> <span data-ttu-id="7ad5b-209">Команда Hello отправляет hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` расположение в hello основного хранилища для кластера.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-209">hello command uploads hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` location in hello primary storage for your cluster.</span></span>

5. <span data-ttu-id="7ad5b-210">Здравствуйте, таблицы с помощью toocreate `hbaseapp`, использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-210">toocreate a table using hello `hbaseapp`, use hello following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    <span data-ttu-id="7ad5b-211">Замените `hdinsightclustername` с hello имя кластера.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-211">Replace `hdinsightclustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="7ad5b-212">Эта команда создает таблицу с именем **people** в HBase в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-212">This command creates a table named **people** in HBase on your HDInsight cluster.</span></span> <span data-ttu-id="7ad5b-213">Эта команда не содержит никаких выходных данных окна консоли «hello».</span><span class="sxs-lookup"><span data-stu-id="7ad5b-213">This command does not show any output in hello console window.</span></span>

6. <span data-ttu-id="7ad5b-214">toosearch для записи в таблице hello, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-214">toosearch for entries in hello table, use hello following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    <span data-ttu-id="7ad5b-215">Замените `hdinsightclustername` с hello имя кластера.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-215">Replace `hdinsightclustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="7ad5b-216">Эта команда использует hello `SearchByEmail` класса toosearch для всех строк, где hello `contactinformation` семейство столбца и hello `email` столбец, содержащий строку hello `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-216">This command uses hello `SearchByEmail` class toosearch for any rows where hello `contactinformation` column family and hello `email` column, contains hello string `contoso.com`.</span></span> <span data-ttu-id="7ad5b-217">Должно появиться hello следующие результаты:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-217">You should receive hello following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="7ad5b-218">С помощью **fabrikam.com** для hello `-emailRegex` значение возвращает hello пользователи, имеющие **fabrikam.com** в поле hello электронной почты.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-218">Using **fabrikam.com** for hello `-emailRegex` value returns hello users that have **fabrikam.com** in hello email field.</span></span> <span data-ttu-id="7ad5b-219">Также можно использовать регулярные выражения как hello поисковому запросу.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-219">You can also use regular expressions as hello search term.</span></span> <span data-ttu-id="7ad5b-220">Например **^ r** Возвращает адреса, начинающиеся с буквы hello 'r' по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-220">For example, **^r** returns email addresses that begin with hello letter 'r'.</span></span>

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="7ad5b-221">При использовании Start-HBaseExample результаты отсутствуют или не получено каких-либо неожиданных результатов.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-221">No results or unexpected results when using Start-HBaseExample</span></span>

<span data-ttu-id="7ad5b-222">Используйте hello `-showErr` параметр tooview hello стандартные ошибки (STDERR), созданного во время выполнения задания hello.</span><span class="sxs-lookup"><span data-stu-id="7ad5b-222">Use hello `-showErr` parameter tooview hello standard error (STDERR) that is produced while running hello job.</span></span>

## <a name="delete-hello-table"></a><span data-ttu-id="7ad5b-223">Удалить таблицу hello</span><span class="sxs-lookup"><span data-stu-id="7ad5b-223">Delete hello table</span></span>

<span data-ttu-id="7ad5b-224">После этого пример hello использовать hello, следуя toodelete hello **людей** таблицы, используемой в этом примере:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-224">When you are done with hello example, use hello following toodelete hello **people** table used in this example:</span></span>

<span data-ttu-id="7ad5b-225">__Из сеанса `ssh`__ :</span><span class="sxs-lookup"><span data-stu-id="7ad5b-225">__From an `ssh` session__:</span></span>

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

<span data-ttu-id="7ad5b-226">__Из Azure PowerShell__:</span><span class="sxs-lookup"><span data-stu-id="7ad5b-226">__From Azure PowerShell__:</span></span>

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a><span data-ttu-id="7ad5b-227">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7ad5b-227">Next steps</span></span>

[<span data-ttu-id="7ad5b-228">Узнайте, как toouse белка SQL с HBase</span><span class="sxs-lookup"><span data-stu-id="7ad5b-228">Learn how toouse SQuirreL SQL with HBase</span></span>](hdinsight-hbase-phoenix-squirrel-linux.md)
