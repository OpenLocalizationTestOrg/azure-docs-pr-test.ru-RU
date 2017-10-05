---
title: "Клиент Java HBase для Azure HDInsight | Документация Майкрософт"
description: "Сведения об использовании Apache Maven для создания приложения Java для Apache HBase и его последующем развертывании в HBase в Azure HDInsight."
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
ms.openlocfilehash: 03c88397e36c0fc7f19410e49f6b6f1a607659f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="build-java-applications-for-apache-hbase"></a><span data-ttu-id="6ff1e-103">Создание приложений Java для Apache HBase</span><span class="sxs-lookup"><span data-stu-id="6ff1e-103">Build Java applications for Apache HBase</span></span>

<span data-ttu-id="6ff1e-104">Узнайте, как создать приложение [Apache HBase](http://hbase.apache.org/) в среде Java.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-104">Learn how to create an [Apache HBase](http://hbase.apache.org/) application in Java.</span></span> <span data-ttu-id="6ff1e-105">Затем вы будете использовать приложение с HBase в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-105">Then use the application with HBase on Azure HDInsight.</span></span>

<span data-ttu-id="6ff1e-106">В этом руководстве используется [Maven](http://maven.apache.org/) для создания и сборки проекта.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-106">The steps in this document use [Maven](http://maven.apache.org/) to create and build the project.</span></span> <span data-ttu-id="6ff1e-107">Maven — это инструмент для управления и повышения обозримости проектов программного обеспечения, позволяющий создавать ПО, документацию и отчеты для проектов Java.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-107">Maven is a software project management and comprehension tool that allows you to build software, documentation, and reports for Java projects.</span></span>

> [!NOTE]
> <span data-ttu-id="6ff1e-108">Действия, описанные в этом документе, в последний раз были протестированы с помощью HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-108">The steps in this document were most recently tested with HDInsight 3.6.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ff1e-109">Для выполнения действий, описанных в этом документе, необходим кластер HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-109">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="6ff1e-110">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6ff1e-111">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6ff1e-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="6ff1e-112">Требования</span><span class="sxs-lookup"><span data-stu-id="6ff1e-112">Requirements</span></span>

* <span data-ttu-id="6ff1e-113">[Пакет JDK для платформы Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html) версии 8 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-113">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 or later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6ff1e-114">Для HDInsight 3.5 и более поздних версий требуется Java 8.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-114">HDInsight 3.5 and greater requires Java 8.</span></span> <span data-ttu-id="6ff1e-115">Для работы более ранних версий HDInsight требуется Java 7.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-115">Earlier versions of HDInsight require Java 7.</span></span>

* [<span data-ttu-id="6ff1e-116">Maven</span><span class="sxs-lookup"><span data-stu-id="6ff1e-116">Maven</span></span>](http://maven.apache.org/)

* [<span data-ttu-id="6ff1e-117">Кластер Azure HDInsight под управлением Linux с HBase.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-117">A Linux-based Azure HDInsight cluster with HBase</span></span>](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > <span data-ttu-id="6ff1e-118">Действия, описанные в этом документе, выполнялись с версиями кластера HDInsight 3.4 и 3.5.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-118">The steps in this document have been tested with HDInsight cluster versions 3.4 and 3.5.</span></span> <span data-ttu-id="6ff1e-119">Значения по умолчанию в примерах предназначены для кластера HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-119">The default values provided in examples are for a HDInsight 3.5 cluster.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="6ff1e-120">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="6ff1e-120">Create the project</span></span>

1. <span data-ttu-id="6ff1e-121">Из командной строки вашей среды разработки измените каталоги на расположение, где вы хотите создать проект. Например, `cd code\hbase`.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-121">From the command line in your development environment, change directories to the location where you want to create the project, for example, `cd code\hbase`.</span></span>

2. <span data-ttu-id="6ff1e-122">Используйте команду **mvn** , которая будет установлена вместе с Maven, для создания шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-122">Use the **mvn** command, which is installed with Maven, to generate the scaffolding for the project.</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > <span data-ttu-id="6ff1e-123">При использовании PowerShell параметры `-D` необходимо заключить в кавычки.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-123">If you are using PowerShell, you must enclose the `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="6ff1e-124">При этом будет создан каталог, имя которого будет совпадать с именем параметра **artifactID** (в нашем случае **hbaseapp**). Этот каталог содержит следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="6ff1e-124">This command creates a directory with the same name as the **artifactID** parameter (**hbaseapp** in this example.) This directory contains the following items:</span></span>

   * <span data-ttu-id="6ff1e-125">**pom.xml** — это модель объекта проекта ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)), которая содержит информацию и подробности конфигурации, учитывающиеся при сборке проекта;</span><span class="sxs-lookup"><span data-stu-id="6ff1e-125">**pom.xml**:  The Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used to build the project.</span></span>
   * <span data-ttu-id="6ff1e-126">**src** — каталог, содержащий каталог **main/java/com/microsoft/examples**, в котором создается приложение.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-126">**src**: The directory that contains the **main/java/com/microsoft/examples** directory, where you author the application.</span></span>

3. <span data-ttu-id="6ff1e-127">Удалите файл `src/test/java/com/microsoft/examples/apptest.java`.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-127">Delete the `src/test/java/com/microsoft/examples/apptest.java` file.</span></span> <span data-ttu-id="6ff1e-128">Он не используется в этом примере.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-128">It is not be used in this example.</span></span>

## <a name="update-the-project-object-model"></a><span data-ttu-id="6ff1e-129">Обновление модели объекта проекта</span><span class="sxs-lookup"><span data-stu-id="6ff1e-129">Update the Project Object Model</span></span>

1. <span data-ttu-id="6ff1e-130">Измените файл `pom.xml`, добавив в раздел `<dependencies>` следующий код:</span><span class="sxs-lookup"><span data-stu-id="6ff1e-130">Edit the `pom.xml` file and add the following code inside the `<dependencies>` section:</span></span>

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

    <span data-ttu-id="6ff1e-131">В этом разделе показано, что для проекта требуются компоненты **hbase-client** и **phoenix-core**.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-131">This section indicates that the project needs **hbase-client** and **phoenix-core** components.</span></span> <span data-ttu-id="6ff1e-132">При компиляции эти зависимости скачиваются из репозитория Maven по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-132">At compile time, these dependencies are downloaded from the default Maven repository.</span></span> <span data-ttu-id="6ff1e-133">Можно воспользоваться [поиском в центральном репозитории Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) , чтобы получить дополнительную информацию об этой зависимости.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-133">You can use the [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) to learn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="6ff1e-134">Номер версии hbase-client должен соответствовать версии HBase, которая поставляется с кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-134">The version number of the hbase-client must match the version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="6ff1e-135">Воспользуйтесь следующей таблицей, чтобы найти правильный номер версии.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-135">Use the following table to find the correct version number.</span></span>

   | <span data-ttu-id="6ff1e-136">Версия кластера HDInsight</span><span class="sxs-lookup"><span data-stu-id="6ff1e-136">HDInsight cluster version</span></span> | <span data-ttu-id="6ff1e-137">Используемая версия HBase</span><span class="sxs-lookup"><span data-stu-id="6ff1e-137">HBase version to use</span></span> |
   | --- | --- |
   | <span data-ttu-id="6ff1e-138">3.2</span><span class="sxs-lookup"><span data-stu-id="6ff1e-138">3.2</span></span> |<span data-ttu-id="6ff1e-139">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="6ff1e-139">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="6ff1e-140">3.3, 3.4, 3.5 и 3.6</span><span class="sxs-lookup"><span data-stu-id="6ff1e-140">3.3, 3.4, 3.5, and 3.6</span></span> |<span data-ttu-id="6ff1e-141">1.1.2</span><span class="sxs-lookup"><span data-stu-id="6ff1e-141">1.1.2</span></span> |

    <span data-ttu-id="6ff1e-142">Дополнительные сведения о версиях и компонентах HDInsight см. в статье [Что представляют собой различные компоненты Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="6ff1e-142">For more information on HDInsight versions and components, see [What are the different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>

3. <span data-ttu-id="6ff1e-143">Добавьте в файл **pom.xml** следующий код.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-143">Add the following code to the **pom.xml** file.</span></span> <span data-ttu-id="6ff1e-144">Эти строки должны находиться в файле внутри тегов `<project>...</project>` (например, между тегами `</dependencies>` и `</project>`).</span><span class="sxs-lookup"><span data-stu-id="6ff1e-144">This text must be inside the `<project>...</project>` tags in the file, for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="6ff1e-145">В этом разделе настраивается ресурс (`conf/hbase-site.xml`), который содержит информацию о конфигурации для HBase.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-145">This section configures a resource (`conf/hbase-site.xml`) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6ff1e-146">Также можно настроить значения конфигурации непосредственно из кода.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-146">You can also set configuration values via code.</span></span> <span data-ttu-id="6ff1e-147">Ознакомьтесь с комментариями к примеру `CreateTable`.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-147">See the comments in the `CreateTable` example.</span></span>

    <span data-ttu-id="6ff1e-148">В разделе также будут настроены подключаемые модули [компилятора Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) и[Maven Shade](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="6ff1e-148">This section also configures the [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="6ff1e-149">Подключаемый модуль компилятора используется для компиляции топологии.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-149">The compiler plug-in is used to compile the topology.</span></span> <span data-ttu-id="6ff1e-150">Подключаемый модуль shade используется для предотвращения дублирования лицензии в JAR-файле, собранном Maven.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-150">The shade plug-in is used to prevent license duplication in the JAR package that is built by Maven.</span></span> <span data-ttu-id="6ff1e-151">Этот подключаемый модуль используется для предотвращения ошибки с дублированием файлов лицензий, которая появляется во время выполнения на кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-151">This plugin is used to prevent a "duplicate license files" error at run time on the HDInsight cluster.</span></span> <span data-ttu-id="6ff1e-152">Использование maven-shade-plugin с реализацией `ApacheLicenseResourceTransformer` позволяет избежать этой ошибки.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-152">Using maven-shade-plugin with the `ApacheLicenseResourceTransformer` implementation prevents the error.</span></span>

    <span data-ttu-id="6ff1e-153">maven-shade-plugin также создает так называемый uber jar, который содержит все зависимости, требуемые для приложения.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-153">The maven-shade-plugin also produces an uber jar that contains all the dependencies required by the application.</span></span>

4. <span data-ttu-id="6ff1e-154">Сохраните файл `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-154">Save the `pom.xml` file.</span></span>

5. <span data-ttu-id="6ff1e-155">Создайте каталог с именем `conf` в каталоге `hbaseapp`.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-155">Create a directory named `conf` in the `hbaseapp` directory.</span></span> <span data-ttu-id="6ff1e-156">Этот каталог будет использоваться для хранения сведений о конфигурации для подключения к HBase.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-156">This directory is used to hold configuration information for connecting to HBase.</span></span>

6. <span data-ttu-id="6ff1e-157">Для копирования конфигурации HBase из кластера HBase в каталог `conf` используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-157">Use the following command to copy the HBase configuration from the HBase cluster to the `conf` directory.</span></span> <span data-ttu-id="6ff1e-158">Замените `USERNAME` именем пользователя SSH,</span><span class="sxs-lookup"><span data-stu-id="6ff1e-158">Replace `USERNAME` with the name of your SSH login.</span></span> <span data-ttu-id="6ff1e-159">а `CLUSTERNAME` — именем кластера HDInsight:</span><span class="sxs-lookup"><span data-stu-id="6ff1e-159">Replace `CLUSTERNAME` with your HDInsight cluster name:</span></span>

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   <span data-ttu-id="6ff1e-160">Дополнительные сведения об использовании `ssh` и `scp` см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6ff1e-160">For more information on using `ssh` and `scp`, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-the-application"></a><span data-ttu-id="6ff1e-161">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="6ff1e-161">Create the application</span></span>

1. <span data-ttu-id="6ff1e-162">Перейдите к каталогу `hbaseapp/src/main/java/com/microsoft/examples` и переименуйте файл app.java в `CreateTable.java`.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-162">Go to the `hbaseapp/src/main/java/com/microsoft/examples` directory and rename the app.java file to `CreateTable.java`.</span></span>

2. <span data-ttu-id="6ff1e-163">Откройте файл `CreateTable.java` и замените имеющееся содержимое следующим текстом:</span><span class="sxs-lookup"><span data-stu-id="6ff1e-163">Open the `CreateTable.java` file and replace the existing contents with the following text:</span></span>

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

        //Linux-based HDInsight clusters use /hbase-unsecure as the znode parent
        config.set("zookeeper.znode.parent","/hbase-unsecure");

        // create an admin object using the config
        HBaseAdmin admin = new HBaseAdmin(config);

        // create the table...
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

        // Add each person to the table
        //   Use the `name` column family for the name
        //   Use the `contactinfo` column family for the email
        for (int i = 0; i< people.length; i++) {
            Put person = new Put(Bytes.toBytes(people[i][0]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
            person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
            table.put(person);
        }
        // flush commits and close the table
        table.flushCommits();
        table.close();
        }
    }
   ```

    <span data-ttu-id="6ff1e-164">Это код класса **CreateTable**, который создает таблицу с именем **people** и заполняет ее заранее определенными пользователями.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-164">This code is the **CreateTable** class, which creates a table named **people** and populate it with some predefined users.</span></span>

3. <span data-ttu-id="6ff1e-165">Сохраните файл `CreateTable.java`.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-165">Save the `CreateTable.java` file.</span></span>

4. <span data-ttu-id="6ff1e-166">В каталоге `hbaseapp/src/main/java/com/microsoft/examples` создайте файл с именем `SearchByEmail.java`.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-166">In the `hbaseapp/src/main/java/com/microsoft/examples` directory, create a file named `SearchByEmail.java`.</span></span> <span data-ttu-id="6ff1e-167">В качестве содержимого файла добавьте следующий текст:</span><span class="sxs-lookup"><span data-stu-id="6ff1e-167">Use the following text as the contents of this file:</span></span>

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

        // Use GenericOptionsParser to get only the parameters to the class
        // and not all the parameters passed (when using WebHCat for example)
        String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
        if (otherArgs.length != 1) {
            System.out.println("usage: [regular expression]");
            System.exit(-1);
        }

        // Open the table
        HTable table = new HTable(config, "people");

        // Define the family and qualifiers to be used
        byte[] contactFamily = Bytes.toBytes("contactinfo");
        byte[] emailQualifier = Bytes.toBytes("email");
        byte[] nameFamily = Bytes.toBytes("name");
        byte[] firstNameQualifier = Bytes.toBytes("first");
        byte[] lastNameQualifier = Bytes.toBytes("last");

        // Create a regex filter
        RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
        // Attach the regex filter to a filter
        //   for the email column
        SingleColumnValueFilter filter = new SingleColumnValueFilter(
            contactFamily,
            emailQualifier,
            CompareOp.EQUAL,
            emailFilter
        );

        // Create a scan and set the filter
        Scan scan = new Scan();
        scan.setFilter(filter);

        // Get the results
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

    <span data-ttu-id="6ff1e-168">Класс **SearchByEmail** можно использовать для запроса строк по адресу электронной почты.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-168">The **SearchByEmail** class can be used to query for rows by email address.</span></span> <span data-ttu-id="6ff1e-169">При использовании класса можно задавать либо строку, либо регулярное выражение, так как используется фильтр регулярных выражений.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-169">Because it uses a regular expression filter, you can provide either a string or a regular expression when using the class.</span></span>

5. <span data-ttu-id="6ff1e-170">Сохраните файл `SearchByEmail.java`.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-170">Save the `SearchByEmail.java` file.</span></span>

6. <span data-ttu-id="6ff1e-171">В каталоге `hbaseapp/src/main/hava/com/microsoft/examples` создайте файл с именем `DeleteTable.java`.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-171">In the `hbaseapp/src/main/hava/com/microsoft/examples` directory, create a file named `DeleteTable.java`.</span></span> <span data-ttu-id="6ff1e-172">В качестве содержимого файла добавьте следующий текст:</span><span class="sxs-lookup"><span data-stu-id="6ff1e-172">Use the following text as the contents of this file:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;

    public class DeleteTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Create an admin object using the config
        HBaseAdmin admin = new HBaseAdmin(config);

        // Disable, and then delete the table
        admin.disableTable("people");
        admin.deleteTable("people");
        }
    }
   ```

    <span data-ttu-id="6ff1e-173">Этот класс предназначен, только чтобы очистить таблицы HBase, созданные в данном примере, отключив и удалив таблицу, созданную классом `CreateTable`.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-173">This class cleans up the HBase tables created in this example by disabling and dropping the table created by the `CreateTable` class.</span></span>

7. <span data-ttu-id="6ff1e-174">Сохраните файл `DeleteTable.java`.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-174">Save the `DeleteTable.java` file.</span></span>

## <a name="build-and-package-the-application"></a><span data-ttu-id="6ff1e-175">Сборка и создание пакета приложения</span><span class="sxs-lookup"><span data-stu-id="6ff1e-175">Build and package the application</span></span>

1. <span data-ttu-id="6ff1e-176">Выполните следующую команду из каталога `hbaseapp`, чтобы собрать JAR-файл, содержащий приложение:</span><span class="sxs-lookup"><span data-stu-id="6ff1e-176">From the `hbaseapp` directory, use the following command to build a JAR file that contains the application:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="6ff1e-177">Эта команда создает и упаковывает приложение в JAR-файл.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-177">This command builds and packages the application into a .jar file.</span></span>

2. <span data-ttu-id="6ff1e-178">После выполнения команды каталог `hbaseapp/target` будет содержать файл с именем `hbaseapp-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-178">When the command completes, the `hbaseapp/target` directory contains a file named `hbaseapp-1.0-SNAPSHOT.jar`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6ff1e-179">Файл `hbaseapp-1.0-SNAPSHOT.jar` относится к типу uber jar.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-179">The `hbaseapp-1.0-SNAPSHOT.jar` file is an uber jar.</span></span> <span data-ttu-id="6ff1e-180">Он содержит все зависимости, необходимые для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-180">It contains all the dependencies required to run the application.</span></span>


## <a name="upload-the-jar-and-run-jobs-ssh"></a><span data-ttu-id="6ff1e-181">Передача JAR-файла и запуск заданий (SSH)</span><span class="sxs-lookup"><span data-stu-id="6ff1e-181">Upload the JAR and run jobs (SSH)</span></span>

<span data-ttu-id="6ff1e-182">В следующих действиях используется команда `scp` для копирования JAR-файла в головной узел HBase в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-182">The following steps use `scp` to copy the JAR to the primary head node of your HBase on HDInsight cluster.</span></span> <span data-ttu-id="6ff1e-183">С помощью команды `ssh` выполняется подключение к кластеру; пример запускается непосредственно на головном узле.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-183">The `ssh` command is then used to connect to the cluster and run the example directly on the head node.</span></span>

1. <span data-ttu-id="6ff1e-184">Чтобы отправить JAR-файл в кластер, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6ff1e-184">To upload the jar to the cluster, use the following command:</span></span>

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="6ff1e-185">Замените `USERNAME` именем пользователя SSH,</span><span class="sxs-lookup"><span data-stu-id="6ff1e-185">Replace `USERNAME` with the name of your SSH login.</span></span> <span data-ttu-id="6ff1e-186">а `CLUSTERNAME` — именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-186">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

2. <span data-ttu-id="6ff1e-187">Чтобы подключиться к кластеру HBase, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6ff1e-187">To connect to the HBase cluster, use the following command:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="6ff1e-188">Замените `USERNAME` именем для входа SSH,</span><span class="sxs-lookup"><span data-stu-id="6ff1e-188">Replace `USERNAME` the name of your SSH login.</span></span> <span data-ttu-id="6ff1e-189">а `CLUSTERNAME` — именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-189">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

3. <span data-ttu-id="6ff1e-190">Чтобы создать таблицу HBase с помощью приложения Java, воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="6ff1e-190">To create an HBase table using the Java application, use the following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    <span data-ttu-id="6ff1e-191">Эта команда создает таблицу HBase с именем **people** и заполняет ее данными.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-191">This command creates a HBase table named **people**, and populates it with data.</span></span>

4. <span data-ttu-id="6ff1e-192">Для поиска адресов электронной почты, хранящихся в этой таблице, воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="6ff1e-192">To search for email addresses stored in the table, use the following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    <span data-ttu-id="6ff1e-193">Вы получите следующие результаты:</span><span class="sxs-lookup"><span data-stu-id="6ff1e-193">You receive the following results:</span></span>

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. <span data-ttu-id="6ff1e-194">Чтобы удалить таблицу, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6ff1e-194">To delete the table, use the following command:</span></span>

    

## <a name="upload-the-jar-and-run-jobs-powershell"></a><span data-ttu-id="6ff1e-195">Передача JAR-файла и запуск заданий (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="6ff1e-195">Upload the JAR and run jobs (PowerShell)</span></span>

<span data-ttu-id="6ff1e-196">Далее используется Azure PowerShell для передачи JAR-файла в хранилище по умолчанию для кластера HBase.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-196">The following steps use Azure PowerShell to upload the JAR to the default storage for your HBase cluster.</span></span> <span data-ttu-id="6ff1e-197">Затем командлеты HDInsight используются для удаленного запуска примеров.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-197">HDInsight cmdlets are then used to run the examples remotely.</span></span>

1. <span data-ttu-id="6ff1e-198">После установки и настройки Azure PowerShell создайте файл с именем `hbase-runner.psm1`.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-198">After installing and configuring Azure PowerShell, create a file named `hbase-runner.psm1`.</span></span> <span data-ttu-id="6ff1e-199">В качестве содержимого файла добавьте следующий текст:</span><span class="sxs-lookup"><span data-stu-id="6ff1e-199">Use the following text as the contents of this file:</span></span>

   ```powershell
    <#
    .SYNOPSIS
    Copies a file to the primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory to the blob container for
    the HDInsight cluster.
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
    #The class to run
    [Parameter(Mandatory = $true)]
    [String]$className,

    #The name of the HDInsight cluster
    [Parameter(Mandatory = $true)]
    [String]$clusterName,

    #Only used when using SearchByEmail
    [Parameter(Mandatory = $false)]
    [String]$emailRegex,

    #Use if you want to see stderr output
    [Parameter(Mandatory = $false)]
    [Switch]$showErr
    )

    Set-StrictMode -Version 3

    # Is the Azure module installed?
    FindAzure

    # Get the login for the HDInsight cluster
    $creds=Get-Credential -Message "Enter the login for the cluster" -UserName "admin"

    # The JAR
    $jarFile = "wasb:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

    # The job definition
    $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
        -JarFile $jarFile `
        -ClassName $className `
        -Arguments $emailRegex

    # Get the job output
    $job = Start-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobDefinition $jobDefinition `
        -HttpCredential $creds
    Write-Host "Wait for the job to complete ..." -ForegroundColor Green
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
    Write-Host "Display the standard output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds
    }

    <#
    .SYNOPSIS
    Copies a file to the primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory to the blob container for
    the HDInsight cluster.
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
            #The path to the local file.
            [Parameter(Mandatory = $true)]
            [String]$localPath,

            #The destination path and file name, relative to the root of the container.
            [Parameter(Mandatory = $true)]
            [String]$destinationPath,

            #The name of the HDInsight cluster
            [Parameter(Mandatory = $true)]
            [String]$clusterName,

            #If specified, overwrites existing files without prompting
            [Parameter(Mandatory = $false)]
            [Switch]$force
        )

        Set-StrictMode -Version 3

        # Is the Azure module installed?
        FindAzure

        # Get authentication for the cluster
        $creds=Get-Credential

        # Does the local path exist?
        if (-not (Test-Path $localPath))
        {
            throw "Source path '$localPath' does not exist."
        }

        # Get the primary storage container
        $storage = GetStorage -clusterName $clusterName

        # Upload file to storage, overwriting existing files if -force was used.
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
            throw "No active Azure subscription found! If you have a subscription, use the Login-AzureRmAccount cmdlet to login to your subscription."
        }
    }

    function GetStorage {
        param(
            [Parameter(Mandatory = $true)]
            [String]$clusterName
        )
        $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
        # Does the cluster exist?
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
        # Get the resource group, in case we need that
        $return.resourceGroup = $resourceGroup
        # Get the storage context, as we can't depend
        # on using the default storage context
        $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        # Get the container, so we know where to
        # find/store blobs
        $return.container = $container
        # Return storage accounts to support finding all accounts for
        # a cluster
        $return.storageAccount = $storageAccountName
        $return.storageAccountKey = $storageAccountKey

        return $return
    }
    # Only export the verb-phrase things
    export-modulemember *-*
   ```

    <span data-ttu-id="6ff1e-200">Этот файл содержит два модуля:</span><span class="sxs-lookup"><span data-stu-id="6ff1e-200">This file contains two modules:</span></span>

   * <span data-ttu-id="6ff1e-201">**Add-HDInsightFile** — используется для загрузки файлов в кластер;</span><span class="sxs-lookup"><span data-stu-id="6ff1e-201">**Add-HDInsightFile** - used to upload files to the cluster</span></span>
   * <span data-ttu-id="6ff1e-202">**Start-HBaseExample** — используется для запуска классов, созданных ранее.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-202">**Start-HBaseExample** - used to run the classes created earlier</span></span>

2. <span data-ttu-id="6ff1e-203">Сохраните файл `hbase-runner.psm1`.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-203">Save the `hbase-runner.psm1` file.</span></span>

3. <span data-ttu-id="6ff1e-204">Откройте окно Azure PowerShell, измените каталоги на каталог `hbaseapp`, а затем выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6ff1e-204">Open a new Azure PowerShell window, change directories to the `hbaseapp` directory, and then run the following command:</span></span>

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    <span data-ttu-id="6ff1e-205">Измените путь на место расположения созданного ранее файла `hbase-runner.psm1`.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-205">Change the path to the location of the `hbase-runner.psm1` file created earlier.</span></span> <span data-ttu-id="6ff1e-206">Эта команда регистрирует модуль в Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-206">This command registers the module with Azure PowerShell.</span></span>

4. <span data-ttu-id="6ff1e-207">Воспользуйтесь следующей командой, чтобы отправить файл `hbaseapp-1.0-SNAPSHOT.jar` в ваш кластер.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-207">Use the following command to upload the `hbaseapp-1.0-SNAPSHOT.jar` to your cluster.</span></span>

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    <span data-ttu-id="6ff1e-208">Замените `hdinsightclustername` именем кластера.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-208">Replace `hdinsightclustername` with the name of your cluster.</span></span> <span data-ttu-id="6ff1e-209">Команда отправляет файл `hbaseapp-1.0-SNAPSHOT.jar` в расположение `example/jars` в главном хранилище кластера.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-209">The command uploads the `hbaseapp-1.0-SNAPSHOT.jar` to the `example/jars` location in the primary storage for your cluster.</span></span>

5. <span data-ttu-id="6ff1e-210">Чтобы создать таблицу с помощью `hbaseapp`, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6ff1e-210">To create a table using the `hbaseapp`, use the following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    <span data-ttu-id="6ff1e-211">Замените `hdinsightclustername` именем кластера.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-211">Replace `hdinsightclustername` with the name of your cluster.</span></span>

    <span data-ttu-id="6ff1e-212">Эта команда создает таблицу с именем **people** в HBase в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-212">This command creates a table named **people** in HBase on your HDInsight cluster.</span></span> <span data-ttu-id="6ff1e-213">Эта команда не отображает какие-либо выходные данные в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-213">This command does not show any output in the console window.</span></span>

6. <span data-ttu-id="6ff1e-214">Для осуществления поиска записей таблицы используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6ff1e-214">To search for entries in the table, use the following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    <span data-ttu-id="6ff1e-215">Замените `hdinsightclustername` именем кластера.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-215">Replace `hdinsightclustername` with the name of your cluster.</span></span>

    <span data-ttu-id="6ff1e-216">Будет использован класс `SearchByEmail` для поиска всех строк, у которых значение семейства столбцов `contactinformation` и столбца `email` содержит строку `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-216">This command uses the `SearchByEmail` class to search for any rows where the `contactinformation` column family and the `email` column, contains the string `contoso.com`.</span></span> <span data-ttu-id="6ff1e-217">Вы получите следующие результаты:</span><span class="sxs-lookup"><span data-stu-id="6ff1e-217">You should receive the following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="6ff1e-218">Использование **fabrikam.com** для значения `-emailRegex` вернет список пользователей, у которых имеется строка **fabrikam.com** в поле электронного адреса.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-218">Using **fabrikam.com** for the `-emailRegex` value returns the users that have **fabrikam.com** in the email field.</span></span> <span data-ttu-id="6ff1e-219">В качестве поискового запроса также можно использовать регулярные выражения.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-219">You can also use regular expressions as the search term.</span></span> <span data-ttu-id="6ff1e-220">Например, **^r** возвращает адреса электронной почты, начинающиеся с буквы r.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-220">For example, **^r** returns email addresses that begin with the letter 'r'.</span></span>

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="6ff1e-221">При использовании Start-HBaseExample результаты отсутствуют или не получено каких-либо неожиданных результатов.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-221">No results or unexpected results when using Start-HBaseExample</span></span>

<span data-ttu-id="6ff1e-222">Используйте параметр `-showErr` для просмотра стандартной ошибки (STDERR), выдаваемой при выполнении задания.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-222">Use the `-showErr` parameter to view the standard error (STDERR) that is produced while running the job.</span></span>

## <a name="delete-the-table"></a><span data-ttu-id="6ff1e-223">Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="6ff1e-223">Delete the table</span></span>

<span data-ttu-id="6ff1e-224">Завершив работу с примером, удалите таблицу **people**, используя следующую команду в сеансе Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6ff1e-224">When you are done with the example, use the following to delete the **people** table used in this example:</span></span>

<span data-ttu-id="6ff1e-225">__Из сеанса `ssh`__ :</span><span class="sxs-lookup"><span data-stu-id="6ff1e-225">__From an `ssh` session__:</span></span>

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

<span data-ttu-id="6ff1e-226">__Из Azure PowerShell__:</span><span class="sxs-lookup"><span data-stu-id="6ff1e-226">__From Azure PowerShell__:</span></span>

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a><span data-ttu-id="6ff1e-227">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6ff1e-227">Next steps</span></span>

[<span data-ttu-id="6ff1e-228">Использование Apache Phoenix с кластерами HBase под управлением Linux в HDInsight</span><span class="sxs-lookup"><span data-stu-id="6ff1e-228">Learn how to use SQuirreL SQL with HBase</span></span>](hdinsight-hbase-phoenix-squirrel-linux.md)
