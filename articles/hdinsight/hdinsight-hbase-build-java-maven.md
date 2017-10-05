---
title: "Создание приложения Java HBase для кластеров Azure HDInsight под управлением Windows | Документация Майкрософт"
description: "Узнайте, как использовать Apache Maven для создания приложения Java для Apache HBase и его последующего развертывания в кластере Azure HDInsight на основе Windows."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f4a4e02-45ab-40dd-842b-3ec034f256c9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 59c9af5a91b107e68a676f02fe5a936f955b22fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-maven-to-build-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a><span data-ttu-id="2c672-103">Использование Maven для выполнения сборки приложений Java, которые используют HBase с HDInsight (Hadoop) под управлением Windows</span><span class="sxs-lookup"><span data-stu-id="2c672-103">Use Maven to build Java applications that use HBase with Windows-based HDInsight (Hadoop)</span></span>
<span data-ttu-id="2c672-104">Вы узнаете, как создать приложение [Apache HBase](http://hbase.apache.org/) на Java и выполнить его сборку с использованием Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="2c672-104">Learn how to create and build an [Apache HBase](http://hbase.apache.org/) application in Java by using Apache Maven.</span></span> <span data-ttu-id="2c672-105">Затем вы будете использовать приложение с Azure HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="2c672-105">Then use the application with Azure HDInsight (Hadoop).</span></span>

<span data-ttu-id="2c672-106">[Maven](http://maven.apache.org/) — это инструмент для управления и повышения обозримости проектов программного обеспечения, позволяющее создавать ПО, документацию и отчеты для проектов Java.</span><span class="sxs-lookup"><span data-stu-id="2c672-106">[Maven](http://maven.apache.org/) is a software project management and comprehension tool that allows you to build software, documentation, and reports for Java projects.</span></span> <span data-ttu-id="2c672-107">Из данной статьи вы узнаете, как использовать его для создания базового приложения Java, которое формирует запросы и удаляет таблицу HBase в кластере Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c672-107">In this article, you learn how to use it to create a basic Java application that that creates, queries, and deletes an HBase table on an Azure HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c672-108">Для выполнения действий, описанных в этом документе, необходим кластер HDInsight, который использует Windows.</span><span class="sxs-lookup"><span data-stu-id="2c672-108">The steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="2c672-109">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="2c672-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2c672-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="2c672-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="2c672-111">Требования</span><span class="sxs-lookup"><span data-stu-id="2c672-111">Requirements</span></span>
* <span data-ttu-id="2c672-112">[Пакет JDK для платформы Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html) версии 7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="2c672-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 or later</span></span>
* [<span data-ttu-id="2c672-113">Maven</span><span class="sxs-lookup"><span data-stu-id="2c672-113">Maven</span></span>](http://maven.apache.org/)
* <span data-ttu-id="2c672-114">Кластер HDInsight под управлением Windows с HBase</span><span class="sxs-lookup"><span data-stu-id="2c672-114">A Windows-based HDInsight cluster with HBase</span></span>

    > [!NOTE]
    > <span data-ttu-id="2c672-115">Действия, описанные в этом документе, были проверены для версий кластера HDInsight 3.2 и 3.3.</span><span class="sxs-lookup"><span data-stu-id="2c672-115">The steps in this document have been tested with HDInsight cluster versions 3.2 and 3.3.</span></span> <span data-ttu-id="2c672-116">Значения по умолчанию в примерах предназначены для кластера HDInsight 3.3.</span><span class="sxs-lookup"><span data-stu-id="2c672-116">The default values provided in examples are for a HDInsight 3.3 cluster.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="2c672-117">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="2c672-117">Create the project</span></span>
1. <span data-ttu-id="2c672-118">Из командной строки вашей среды разработки измените каталоги на расположение, где вы хотите создать проект. Например, `cd code\hdinsight`.</span><span class="sxs-lookup"><span data-stu-id="2c672-118">From the command line in your development environment, change directories to the location where you want to create the project, for example, `cd code\hdinsight`.</span></span>
2. <span data-ttu-id="2c672-119">Используйте команду **mvn** , которая будет установлена вместе с Maven, для создания шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="2c672-119">Use the **mvn** command, which is installed with Maven, to generate the scaffolding for the project.</span></span>

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    <span data-ttu-id="2c672-120">При этом в текущем расположении будет создан каталог с именем, указанным в параметре **artifactID** (в нашем случае **hbaseapp**). Этот каталог содержит следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="2c672-120">This command creates a directory in the current location, with the name specified by the **artifactID** parameter (**hbaseapp** in this example.) This directory contains the following items:</span></span>

   * <span data-ttu-id="2c672-121">**pom.xml** — это модель объекта проекта ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)), которая содержит информацию и подробности конфигурации, учитывающиеся при сборке проекта;</span><span class="sxs-lookup"><span data-stu-id="2c672-121">**pom.xml**:  The Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used to build the project.</span></span>
   * <span data-ttu-id="2c672-122">**src** — каталог, содержащий каталог **main\java\com\microsoft\examples**, в котором будет создаваться приложение.</span><span class="sxs-lookup"><span data-stu-id="2c672-122">**src**: The directory that contains the **main\java\com\microsoft\examples** directory, where you will author the application.</span></span>
3. <span data-ttu-id="2c672-123">Удалите файл **src\test\java\com\microsoft\examples\apptest.java**, так как он не используется в этом примере.</span><span class="sxs-lookup"><span data-stu-id="2c672-123">Delete the **src\test\java\com\microsoft\examples\apptest.java** file because it is not used in this example.</span></span>

## <a name="update-the-project-object-model"></a><span data-ttu-id="2c672-124">Обновление модели объекта проекта</span><span class="sxs-lookup"><span data-stu-id="2c672-124">Update the Project Object Model</span></span>
1. <span data-ttu-id="2c672-125">Откройте для редактирования файл **pom.xml** и добавьте следующий код в раздел `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="2c672-125">Edit the **pom.xml** file and add the following code inside the `<dependencies>` section:</span></span>

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    <span data-ttu-id="2c672-126">Этот раздел указывает Maven, что для проекта требуется **hbase-client** версии **1.1.2**.</span><span class="sxs-lookup"><span data-stu-id="2c672-126">This section tells Maven that the project requires **hbase-client** version **1.1.2**.</span></span> <span data-ttu-id="2c672-127">При компиляции эта зависимость скачивается из репозитория Maven по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2c672-127">At compile time, this dependency is downloaded from the default Maven repository.</span></span> <span data-ttu-id="2c672-128">Можно воспользоваться [поиском в центральном репозитории Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) , чтобы получить дополнительную информацию об этой зависимости.</span><span class="sxs-lookup"><span data-stu-id="2c672-128">You can use the [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) to learn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="2c672-129">Номер версии должен соответствовать версии HBase, которая поставляется с кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c672-129">The version number must match the version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="2c672-130">Воспользуйтесь следующей таблицей, чтобы найти правильный номер версии.</span><span class="sxs-lookup"><span data-stu-id="2c672-130">Use the following table to find the correct version number.</span></span>
   >
   >

   | <span data-ttu-id="2c672-131">Версия кластера HDInsight</span><span class="sxs-lookup"><span data-stu-id="2c672-131">HDInsight cluster version</span></span> | <span data-ttu-id="2c672-132">Используемая версия HBase</span><span class="sxs-lookup"><span data-stu-id="2c672-132">HBase version to use</span></span> |
   | --- | --- |
   | <span data-ttu-id="2c672-133">3.2</span><span class="sxs-lookup"><span data-stu-id="2c672-133">3.2</span></span> |<span data-ttu-id="2c672-134">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="2c672-134">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="2c672-135">3.3</span><span class="sxs-lookup"><span data-stu-id="2c672-135">3.3</span></span> |<span data-ttu-id="2c672-136">1.1.2</span><span class="sxs-lookup"><span data-stu-id="2c672-136">1.1.2</span></span> |

    <span data-ttu-id="2c672-137">Дополнительные сведения о версиях и компонентах HDInsight см. в статье [Что представляют собой различные компоненты Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="2c672-137">For more information on HDInsight versions and components, see [What are the different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>
2. <span data-ttu-id="2c672-138">При использовании кластера HDInsight 3.3 необходимо также добавить в раздел `<dependencies>` следующий код.</span><span class="sxs-lookup"><span data-stu-id="2c672-138">If you are using an HDInsight 3.3 cluster, you must also add the following to the `<dependencies>` section:</span></span>

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    <span data-ttu-id="2c672-139">Эта зависимость загрузит компоненты phoenix-core, которые используются версией Hbase 1.1.x.</span><span class="sxs-lookup"><span data-stu-id="2c672-139">This dependency will load the phoenix-core components, which are used by Hbase version 1.1.x.</span></span>
3. <span data-ttu-id="2c672-140">Добавьте в файл **pom.xml** следующий код.</span><span class="sxs-lookup"><span data-stu-id="2c672-140">Add the following code to the **pom.xml** file.</span></span> <span data-ttu-id="2c672-141">Этот раздел должен находиться в файле внутри тегов `<project>...</project>`, например между `</dependencies>` и `</project>`.</span><span class="sxs-lookup"><span data-stu-id="2c672-141">This section must be inside the `<project>...</project>` tags in the file, for example, between `</dependencies>` and `</project>`.</span></span>

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
                    <source>1.7</source>
                    <target>1.7</target>
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

    <span data-ttu-id="2c672-142">В разделе `<resources>` настраивается ресурс (**conf\hbase-site.xml**), который содержит информацию о конфигурации для HBase.</span><span class="sxs-lookup"><span data-stu-id="2c672-142">The `<resources>` section configures a resource (**conf\hbase-site.xml**) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2c672-143">Также можно настроить значения конфигурации непосредственно из кода.</span><span class="sxs-lookup"><span data-stu-id="2c672-143">You can also set configuration values via code.</span></span> <span data-ttu-id="2c672-144">См. комментарии к примеру **CreateTable** ниже, чтобы узнать, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="2c672-144">See the comments in the **CreateTable** example that follows for how to do this.</span></span>
   >
   >

    <span data-ttu-id="2c672-145">В разделе `<plugins>` будут настроены подключаемые модули [компилятора Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) и [Maven Shade](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="2c672-145">This `<plugins>` section configures the [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="2c672-146">Подключаемый модуль компилятора используется для компиляции топологии.</span><span class="sxs-lookup"><span data-stu-id="2c672-146">The compiler plug-in is used to compile the topology.</span></span> <span data-ttu-id="2c672-147">Подключаемый модуль shade используется для предотвращения дублирования лицензии в JAR-файле, собранном Maven.</span><span class="sxs-lookup"><span data-stu-id="2c672-147">The shade plug-in is used to prevent license duplication in the JAR package that is built by Maven.</span></span> <span data-ttu-id="2c672-148">Причина — дублирующиеся файлы лицензий вызывают ошибку выполнения на кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c672-148">The reason this is used is that the duplicate license files cause an error at run time on the HDInsight cluster.</span></span> <span data-ttu-id="2c672-149">Использование maven-shade-plugin с реализацией `ApacheLicenseResourceTransformer` предотвращает возникновение этой ошибки.</span><span class="sxs-lookup"><span data-stu-id="2c672-149">Using maven-shade-plugin with the `ApacheLicenseResourceTransformer` implementation prevents this error.</span></span>

    <span data-ttu-id="2c672-150">maven-shade-plugin также создает так называемый uber jar (или fat jar), который содержит все зависимости, требуемые для приложения.</span><span class="sxs-lookup"><span data-stu-id="2c672-150">The maven-shade-plugin also produces an uber jar (or fat jar) that contains all the dependencies required by the application.</span></span>
4. <span data-ttu-id="2c672-151">Сохраните файл **pom.xml** .</span><span class="sxs-lookup"><span data-stu-id="2c672-151">Save the **pom.xml** file.</span></span>
5. <span data-ttu-id="2c672-152">Создайте каталог с именем **conf** в каталоге **hbaseapp**.</span><span class="sxs-lookup"><span data-stu-id="2c672-152">Create a new directory named **conf** in the **hbaseapp** directory.</span></span> <span data-ttu-id="2c672-153">В каталоге **conf** создайте файл с именем **hbase-site.xml**.</span><span class="sxs-lookup"><span data-stu-id="2c672-153">In the **conf** directory, create a file named **hbase-site.xml**.</span></span> <span data-ttu-id="2c672-154">Добавьте в этот файл следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="2c672-154">Use the following as the contents of the file:</span></span>

        <?xml version="1.0"?>
        <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
        <!--
        /**
          * Copyright 2010 The Apache Software Foundation
          *
          * Licensed to the Apache Software Foundation (ASF) under one
          * or more contributor license agreements.  See the NOTICE file
          * distributed with this work for additional information
          * regarding copyright ownership.  The ASF licenses this file
          * to you under the Apache License, Version 2.0 (the
          * "License"); you may not use this file except in compliance
          * with the License.  You may obtain a copy of the License at
          *
          *     http://www.apache.org/licenses/LICENSE-2.0
          *
          * Unless required by applicable law or agreed to in writing, software
          * distributed under the License is distributed on an "AS IS" BASIS,
          * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
          * See the License for the specific language governing permissions and
          * limitations under the License.
          */
        -->
        <configuration>
          <property>
            <name>hbase.cluster.distributed</name>
            <value>true</value>
          </property>
          <property>
            <name>hbase.zookeeper.quorum</name>
            <value>zookeeper0,zookeeper1,zookeeper2</value>
          </property>
          <property>
            <name>hbase.zookeeper.property.clientPort</name>
            <value>2181</value>
          </property>
        </configuration>

    <span data-ttu-id="2c672-155">Этот файл будет использоваться для загрузки конфигурации HBase для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c672-155">This file will be used to load the HBase configuration for an HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2c672-156">Это минимально возможный файл hbase-site.xml, содержащий лишь самые минимальные настройки для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c672-156">This is a minimal hbase-site.xml file, and it contains the bare minimum settings for the HDInsight cluster.</span></span>

6. <span data-ttu-id="2c672-157">Сохраните файл **hbase-site.xml**.</span><span class="sxs-lookup"><span data-stu-id="2c672-157">Save the **hbase-site.xml** file.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="2c672-158">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="2c672-158">Create the application</span></span>
1. <span data-ttu-id="2c672-159">Перейдите в каталог **hbaseapp\src\main\java\com\microsoft\examples** и переименуйте файл app.java в **CreateTable.java**.</span><span class="sxs-lookup"><span data-stu-id="2c672-159">Go to the **hbaseapp\src\main\java\com\microsoft\examples** directory and rename the app.java file to **CreateTable.java**.</span></span>
2. <span data-ttu-id="2c672-160">Откройте файл **CreateTable.java** и замените имеющееся содержимое следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="2c672-160">Open the **CreateTable.java** file and replace the existing contents with the following code:</span></span>

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
            // The following sets the znode root for Linux-based HDInsight
            //config.set("zookeeper.znode.parent","/hbase-unsecure");

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

    <span data-ttu-id="2c672-161">Это класс **CreateTable**, который создает таблицу с именем **people** и заполняет ее некими заранее определенными пользователями.</span><span class="sxs-lookup"><span data-stu-id="2c672-161">This is the **CreateTable** class, which will create a table named **people** and populate it with some predefined users.</span></span>
3. <span data-ttu-id="2c672-162">Сохраните файл **CreateTable.java**.</span><span class="sxs-lookup"><span data-stu-id="2c672-162">Save the **CreateTable.java** file.</span></span>
4. <span data-ttu-id="2c672-163">В каталоге **hbaseapp\src\main\java\com\microsoft\examples** создайте файл с именем **SearchByEmail.java**.</span><span class="sxs-lookup"><span data-stu-id="2c672-163">In the **hbaseapp\src\main\java\com\microsoft\examples** directory, create a new file named **SearchByEmail.java**.</span></span> <span data-ttu-id="2c672-164">Используйте следующий код в качестве содержимого этого файла:</span><span class="sxs-lookup"><span data-stu-id="2c672-164">Use the following code as the contents of this file:</span></span>

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

            // Create a new regex filter
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

    <span data-ttu-id="2c672-165">Класс **SearchByEmail** можно использовать для запроса строк по адресу электронной почты.</span><span class="sxs-lookup"><span data-stu-id="2c672-165">The **SearchByEmail** class can be used to query for rows by email address.</span></span> <span data-ttu-id="2c672-166">При использовании класса можно задавать либо строку, либо регулярное выражение, так как используется фильтр регулярных выражений.</span><span class="sxs-lookup"><span data-stu-id="2c672-166">Because it uses a regular expression filter, you can provide either a string or a regular expression when using the class.</span></span>
5. <span data-ttu-id="2c672-167">Сохраните файл **SearchByEmail.java**.</span><span class="sxs-lookup"><span data-stu-id="2c672-167">Save the **SearchByEmail.java** file.</span></span>
6. <span data-ttu-id="2c672-168">В каталоге **hbaseapp\src\main\hava\com\microsoft\examples** создайте файл с именем **DeleteTable.java**.</span><span class="sxs-lookup"><span data-stu-id="2c672-168">In the **hbaseapp\src\main\hava\com\microsoft\examples** directory, create a new file named **DeleteTable.java**.</span></span> <span data-ttu-id="2c672-169">Используйте следующий код в качестве содержимого этого файла:</span><span class="sxs-lookup"><span data-stu-id="2c672-169">Use the following code as the contents of this file:</span></span>

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

    <span data-ttu-id="2c672-170">Этот класс предназначен лишь для того, чтобы очистить данный пример, отключив и удалив таблицу, созданную классом **CreateTable**.</span><span class="sxs-lookup"><span data-stu-id="2c672-170">This class is for cleaning up this example by disabling and dropping the table created by the **CreateTable** class.</span></span>
7. <span data-ttu-id="2c672-171">Сохраните файл **DeleteTable.java**.</span><span class="sxs-lookup"><span data-stu-id="2c672-171">Save the **DeleteTable.java** file.</span></span>

## <a name="build-and-package-the-application"></a><span data-ttu-id="2c672-172">Сборка и создание пакета приложения</span><span class="sxs-lookup"><span data-stu-id="2c672-172">Build and package the application</span></span>
1. <span data-ttu-id="2c672-173">Откройте командную строку и измените каталоги на каталог **hbaseapp**.</span><span class="sxs-lookup"><span data-stu-id="2c672-173">Open a command prompt and change directories to the **hbaseapp** directory.</span></span>
2. <span data-ttu-id="2c672-174">Выполните следующую команду, чтобы собрать JAR-файл, содержащий приложение:</span><span class="sxs-lookup"><span data-stu-id="2c672-174">Use the following command to build a JAR file that contains the application:</span></span>

        mvn clean package

    <span data-ttu-id="2c672-175">При этом будут удалены остатки предыдущих сборок, скачаны все неустановленные на текущий момент зависимости, затем будет произведена сборка и создание пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="2c672-175">This cleans any previous build artifacts, downloads any dependencies that have not already been installed, then builds and packages the application.</span></span>
3. <span data-ttu-id="2c672-176">Когда команда будет выполнена, в каталоге **hbaseapp\target** появится файл с именем **hbaseapp-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="2c672-176">When the command completes, the **hbaseapp\target** directory contains a file named **hbaseapp-1.0-SNAPSHOT.jar**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2c672-177">Файл **hbaseapp-1.0-SNAPSHOT.jar** относится к типу uber jar (другое название — fat jar) и содержит все зависимости, необходимые для работы приложения.</span><span class="sxs-lookup"><span data-stu-id="2c672-177">The **hbaseapp-1.0-SNAPSHOT.jar** file is an uber jar (sometimes called a fat jar,) which contains all the dependencies required to run the application.</span></span>

## <a name="upload-the-jar-file-and-start-a-job"></a><span data-ttu-id="2c672-178">Передача JAR-файла и запуск задания</span><span class="sxs-lookup"><span data-stu-id="2c672-178">Upload the JAR file and start a job</span></span>
<span data-ttu-id="2c672-179">Существует множество способов передачи файла в ваш кластер HDInsight, они описаны в разделе [Отправка данных для заданий Hadoop в HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="2c672-179">There are many ways to upload a file to your HDInsight cluster, as described in [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span> <span data-ttu-id="2c672-180">В следующих действиях используется Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2c672-180">The following steps use Azure PowerShell.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. <span data-ttu-id="2c672-181">После установки и настройки Azure PowerShell создайте файл с именем **hbase-runner.psm1**.</span><span class="sxs-lookup"><span data-stu-id="2c672-181">After installing and configuring Azure PowerShell, create a new file named **hbase-runner.psm1**.</span></span> <span data-ttu-id="2c672-182">Используйте следующее в качестве содержимого этого файла:</span><span class="sxs-lookup"><span data-stu-id="2c672-182">Use the following as the contents of this file:</span></span>

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

    <span data-ttu-id="2c672-183">Этот файл содержит два модуля:</span><span class="sxs-lookup"><span data-stu-id="2c672-183">This file contains two modules:</span></span>

   * <span data-ttu-id="2c672-184">**Add-HDInsightFile** — используется для загрузки файлов в HDInsight;</span><span class="sxs-lookup"><span data-stu-id="2c672-184">**Add-HDInsightFile** - used to upload files to HDInsight</span></span>
   * <span data-ttu-id="2c672-185">**Start-HBaseExample** — используется для запуска классов, созданных ранее.</span><span class="sxs-lookup"><span data-stu-id="2c672-185">**Start-HBaseExample** - used to run the classes created earlier</span></span>
2. <span data-ttu-id="2c672-186">Сохраните файл **hbase-runner.psm1**.</span><span class="sxs-lookup"><span data-stu-id="2c672-186">Save the **hbase-runner.psm1** file.</span></span>
3. <span data-ttu-id="2c672-187">Откройте окно Azure PowerShell, измените каталоги на каталог **hbaseapp**, а затем выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="2c672-187">Open a new Azure PowerShell window, change directories to the **hbaseapp** directory, and then run the following command.</span></span>

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    <span data-ttu-id="2c672-188">Измените путь на место расположения созданного ранее файла **hbase-runner.psm1**.</span><span class="sxs-lookup"><span data-stu-id="2c672-188">Change the path to the location of the **hbase-runner.psm1** file created earlier.</span></span> <span data-ttu-id="2c672-189">При этой модуль будет зарегистрирован для текущего сеанса Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2c672-189">This registers the module for this Azure PowerShell session.</span></span>
4. <span data-ttu-id="2c672-190">Чтобы загрузить **hbaseapp-1.0-SNAPSHOT.jar** на ваш кластер HDInsight, воспользуйтесь следующей командой.</span><span class="sxs-lookup"><span data-stu-id="2c672-190">Use the following command to upload the **hbaseapp-1.0-SNAPSHOT.jar** to your HDInsight cluster.</span></span>

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    <span data-ttu-id="2c672-191">Замените **hdinsightclustername** на имя своего кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c672-191">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span> <span data-ttu-id="2c672-192">Команда передаст **hbaseapp-1.0-SNAPSHOT.jar** в каталог **example/jars**, расположенный в основном хранилище для вашего кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c672-192">The command uploads the **hbaseapp-1.0-SNAPSHOT.jar** to the **example/jars** location in the primary storage for your HDInsight cluster.</span></span>
5. <span data-ttu-id="2c672-193">После передачи файлов создайте таблицу с помощью **hbaseapp**, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="2c672-193">After the files are uploaded, use the following code to create a table using the **hbaseapp**:</span></span>

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    <span data-ttu-id="2c672-194">Замените **hdinsightclustername** на имя своего кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c672-194">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="2c672-195">Эта команда создает таблицу с именем **people** в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c672-195">This command creates a new table named **people** in your HDInsight cluster.</span></span> <span data-ttu-id="2c672-196">Эта команда не отображает какие-либо выходные данные в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="2c672-196">This command does not show any output in the console window.</span></span>
6. <span data-ttu-id="2c672-197">Для осуществления поиска записей таблицы используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2c672-197">To search for entries in the table, use the following command:</span></span>

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    <span data-ttu-id="2c672-198">Замените **hdinsightclustername** на имя своего кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c672-198">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="2c672-199">Будет использован класс **SearchByEmail** для поиска всех строк, у которых значение семейства столбцов **contactinformation** и столбца **email** содержит строку **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="2c672-199">This command uses the **SearchByEmail** class to search for any rows where the **contactinformation** column family and the **email** column, contains the string **contoso.com**.</span></span> <span data-ttu-id="2c672-200">Вы получите следующие результаты:</span><span class="sxs-lookup"><span data-stu-id="2c672-200">You should receive the following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="2c672-201">Использование **fabrikam.com** для значения `-emailRegex` вернет список пользователей, у которых имеется строка **fabrikam.com** в поле электронного адреса.</span><span class="sxs-lookup"><span data-stu-id="2c672-201">Using **fabrikam.com** for the `-emailRegex` value returns the users that have **fabrikam.com** in the email field.</span></span> <span data-ttu-id="2c672-202">Так как поиск реализован на базе фильтра регулярных выражений, можно использовать также и их. Например, если задать **^r**, то будут возвращены записи, у которых электронный адрес начинается с буквы r.</span><span class="sxs-lookup"><span data-stu-id="2c672-202">Since this search is implemented by using a regular expression-based filter, you can also enter regular expressions, such as **^r**, which returns entries where the email begins with the letter 'r'.</span></span>

## <a name="delete-the-table"></a><span data-ttu-id="2c672-203">Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="2c672-203">Delete the table</span></span>
<span data-ttu-id="2c672-204">Завершив работу с примером, удалите больше не нужную таблицу **people**, используя следующую команду в сеансе Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2c672-204">When you are done with the example, use the following command from the Azure PowerShell session to delete the **people** table used in this example:</span></span>

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

<span data-ttu-id="2c672-205">Замените **hdinsightclustername** на имя своего кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c672-205">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2c672-206">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="2c672-206">Troubleshooting</span></span>
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="2c672-207">При использовании Start-HBaseExample результаты отсутствуют или не получено каких-либо неожиданных результатов.</span><span class="sxs-lookup"><span data-stu-id="2c672-207">No results or unexpected results when using Start-HBaseExample</span></span>
<span data-ttu-id="2c672-208">Используйте параметр `-showErr` для просмотра стандартной ошибки (STDERR), выдаваемой при выполнении задания.</span><span class="sxs-lookup"><span data-stu-id="2c672-208">Use the `-showErr` parameter to view the standard error (STDERR) that is produced while running the job.</span></span>
