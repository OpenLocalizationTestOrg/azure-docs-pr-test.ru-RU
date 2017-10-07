---
title: "aaaBuild приложении Java HBase для Azure HDInsight под управлением Windows | Документы Microsoft"
description: "Узнайте, как toouse приложения Apache HBase Apache Maven toobuild на языке Java, затем развернуть его tooa кластера Azure HDInsight под управлением Windows."
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
ms.openlocfilehash: 33c2f3d12cb6a17b5406817e8bcd3accff239517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-maven-toobuild-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a><span data-ttu-id="78508-103">Используйте Maven toobuild Java приложений, использующих HBase с HDInsight под управлением Windows (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="78508-103">Use Maven toobuild Java applications that use HBase with Windows-based HDInsight (Hadoop)</span></span>
<span data-ttu-id="78508-104">Узнайте, как toocreate и построения [Apache HBase](http://hbase.apache.org/) приложение Java с помощью Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="78508-104">Learn how toocreate and build an [Apache HBase](http://hbase.apache.org/) application in Java by using Apache Maven.</span></span> <span data-ttu-id="78508-105">Затем можно используйте приложение hello с Azure HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="78508-105">Then use hello application with Azure HDInsight (Hadoop).</span></span>

<span data-ttu-id="78508-106">[Maven](http://maven.apache.org/) — это проект управления и понимания программа, позволяющий toobuild программное обеспечение, документация и отчеты для проектов Java.</span><span class="sxs-lookup"><span data-stu-id="78508-106">[Maven](http://maven.apache.org/) is a software project management and comprehension tool that allows you toobuild software, documentation, and reports for Java projects.</span></span> <span data-ttu-id="78508-107">В этой статье вы узнаете, как toouse его toocreate простое приложение Java, создаваемые, запросы и удаляет HBase на кластере Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78508-107">In this article, you learn how toouse it toocreate a basic Java application that that creates, queries, and deletes an HBase table on an Azure HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78508-108">Hello в данном пошаговом руководстве требуется кластер HDInsight, который использует Windows.</span><span class="sxs-lookup"><span data-stu-id="78508-108">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="78508-109">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="78508-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="78508-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="78508-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="78508-111">Требования</span><span class="sxs-lookup"><span data-stu-id="78508-111">Requirements</span></span>
* <span data-ttu-id="78508-112">[Пакет JDK для платформы Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html) версии 7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="78508-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 or later</span></span>
* [<span data-ttu-id="78508-113">Maven</span><span class="sxs-lookup"><span data-stu-id="78508-113">Maven</span></span>](http://maven.apache.org/)
* <span data-ttu-id="78508-114">Кластер HDInsight под управлением Windows с HBase</span><span class="sxs-lookup"><span data-stu-id="78508-114">A Windows-based HDInsight cluster with HBase</span></span>

    > [!NOTE]
    > <span data-ttu-id="78508-115">с версиями кластеров HDInsight версии 3.2 и 3.3 протестированы Hello в данном пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="78508-115">hello steps in this document have been tested with HDInsight cluster versions 3.2 and 3.3.</span></span> <span data-ttu-id="78508-116">для кластера HDInsight 3.3, значений по умолчанию Hello в примерах.</span><span class="sxs-lookup"><span data-stu-id="78508-116">hello default values provided in examples are for a HDInsight 3.3 cluster.</span></span>

## <a name="create-hello-project"></a><span data-ttu-id="78508-117">Создание проекта hello</span><span class="sxs-lookup"><span data-stu-id="78508-117">Create hello project</span></span>
1. <span data-ttu-id="78508-118">Из командной строки hello в среде разработки, измените каталоги toohello место, куда toocreate hello проекта, например, `cd code\hdinsight`.</span><span class="sxs-lookup"><span data-stu-id="78508-118">From hello command line in your development environment, change directories toohello location where you want toocreate hello project, for example, `cd code\hdinsight`.</span></span>
2. <span data-ttu-id="78508-119">Используйте hello **mvn** команду, которая устанавливается вместе с Maven, toogenerate hello формирование шаблонов для проекта hello.</span><span class="sxs-lookup"><span data-stu-id="78508-119">Use hello **mvn** command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    <span data-ttu-id="78508-120">Эта команда создает каталог в текущем расположении hello, с именем hello, заданным hello **artifactID** параметра (**hbaseapp** в этом примере.) В этом каталоге содержатся hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="78508-120">This command creates a directory in hello current location, with hello name specified by hello **artifactID** parameter (**hbaseapp** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="78508-121">**pom.XML**: hello объектной модели Project ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) содержит сведения и конфигурации, используемой toobuild hello проекта.</span><span class="sxs-lookup"><span data-stu-id="78508-121">**pom.xml**:  hello Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used toobuild hello project.</span></span>
   * <span data-ttu-id="78508-122">**src**: hello каталог, содержащий hello **main\java\com\microsoft\examples** каталога, в котором будет создать приложение hello.</span><span class="sxs-lookup"><span data-stu-id="78508-122">**src**: hello directory that contains hello **main\java\com\microsoft\examples** directory, where you will author hello application.</span></span>
3. <span data-ttu-id="78508-123">Удалить hello **src\test\java\com\microsoft\examples\apptest.java** файл, поскольку он не используется в этом примере.</span><span class="sxs-lookup"><span data-stu-id="78508-123">Delete hello **src\test\java\com\microsoft\examples\apptest.java** file because it is not used in this example.</span></span>

## <a name="update-hello-project-object-model"></a><span data-ttu-id="78508-124">Обновление hello объектной модели Project</span><span class="sxs-lookup"><span data-stu-id="78508-124">Update hello Project Object Model</span></span>
1. <span data-ttu-id="78508-125">Изменить hello **pom.xml** и добавьте следующий код внутри hello hello `<dependencies>` раздела:</span><span class="sxs-lookup"><span data-stu-id="78508-125">Edit hello **pom.xml** file and add hello following code inside hello `<dependencies>` section:</span></span>

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    <span data-ttu-id="78508-126">В этом разделе приведен Maven, hello проекта требуется **hbase клиента** версии **1.1.2**.</span><span class="sxs-lookup"><span data-stu-id="78508-126">This section tells Maven that hello project requires **hbase-client** version **1.1.2**.</span></span> <span data-ttu-id="78508-127">Во время компиляции Эта зависимость загружается из репозитория Maven по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="78508-127">At compile time, this dependency is downloaded from hello default Maven repository.</span></span> <span data-ttu-id="78508-128">Можно использовать hello [Maven центральный репозиторий поиска](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn Дополнительные сведения об этой зависимости.</span><span class="sxs-lookup"><span data-stu-id="78508-128">You can use hello [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="78508-129">номер версии Hello должен совпадать hello версия HBase, который входит в состав кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78508-129">hello version number must match hello version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="78508-130">Используйте следующие таблицы toofind hello правильный номер версии hello.</span><span class="sxs-lookup"><span data-stu-id="78508-130">Use hello following table toofind hello correct version number.</span></span>
   >
   >

   | <span data-ttu-id="78508-131">Версия кластера HDInsight</span><span class="sxs-lookup"><span data-stu-id="78508-131">HDInsight cluster version</span></span> | <span data-ttu-id="78508-132">Toouse версия HBase</span><span class="sxs-lookup"><span data-stu-id="78508-132">HBase version toouse</span></span> |
   | --- | --- |
   | <span data-ttu-id="78508-133">3.2</span><span class="sxs-lookup"><span data-stu-id="78508-133">3.2</span></span> |<span data-ttu-id="78508-134">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="78508-134">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="78508-135">3.3</span><span class="sxs-lookup"><span data-stu-id="78508-135">3.3</span></span> |<span data-ttu-id="78508-136">1.1.2</span><span class="sxs-lookup"><span data-stu-id="78508-136">1.1.2</span></span> |

    <span data-ttu-id="78508-137">Дополнительные сведения о версии HDInsight и компонентов см. в разделе [Каковы hello различных Hadoop компоненты, доступные с HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="78508-137">For more information on HDInsight versions and components, see [What are hello different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>
2. <span data-ttu-id="78508-138">При использовании с кластером HDInsight 3.3, необходимо добавить следующие toohello hello `<dependencies>` раздела:</span><span class="sxs-lookup"><span data-stu-id="78508-138">If you are using an HDInsight 3.3 cluster, you must also add hello following toohello `<dependencies>` section:</span></span>

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    <span data-ttu-id="78508-139">Эта зависимость будет загружаться hello Финиксе основных компонентов, которые используется версия Hbase 1.1.x.</span><span class="sxs-lookup"><span data-stu-id="78508-139">This dependency will load hello phoenix-core components, which are used by Hbase version 1.1.x.</span></span>
3. <span data-ttu-id="78508-140">Добавьте следующий код toohello hello **pom.xml** файла.</span><span class="sxs-lookup"><span data-stu-id="78508-140">Add hello following code toohello **pom.xml** file.</span></span> <span data-ttu-id="78508-141">В этом разделе, должны находиться внутри hello `<project>...</project>` тегов в hello файла, например, между `</dependencies>` и `</project>`.</span><span class="sxs-lookup"><span data-stu-id="78508-141">This section must be inside hello `<project>...</project>` tags in hello file, for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="78508-142">Hello `<resources>` раздел настраивает ресурс (**conf\hbase-site.xml**), содержащий сведения о конфигурации для HBase.</span><span class="sxs-lookup"><span data-stu-id="78508-142">hello `<resources>` section configures a resource (**conf\hbase-site.xml**) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="78508-143">Также можно настроить значения конфигурации непосредственно из кода.</span><span class="sxs-lookup"><span data-stu-id="78508-143">You can also set configuration values via code.</span></span> <span data-ttu-id="78508-144">См. комментарии hello в hello **CreateTable** для как в следующем примере toodo это.</span><span class="sxs-lookup"><span data-stu-id="78508-144">See hello comments in hello **CreateTable** example that follows for how toodo this.</span></span>
   >
   >

    <span data-ttu-id="78508-145">Это `<plugins>` раздел настраивает hello [подключаемого модуля компилятора Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) и [подключаемого модуля оттенок Maven](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="78508-145">This `<plugins>` section configures hello [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="78508-146">Компилятор Hello подключаемый модуль — используется toocompile hello топологии.</span><span class="sxs-lookup"><span data-stu-id="78508-146">hello compiler plug-in is used toocompile hello topology.</span></span> <span data-ttu-id="78508-147">Подключаемый модуль оттенок Hello — дублирования лицензии tooprevent используется в пакете JAR hello, построенного с Maven.</span><span class="sxs-lookup"><span data-stu-id="78508-147">hello shade plug-in is used tooprevent license duplication in hello JAR package that is built by Maven.</span></span> <span data-ttu-id="78508-148">Hello используется обусловлено тем, что файлы повторяющиеся лицензии hello приводят к ошибке во время выполнения в кластере HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="78508-148">hello reason this is used is that hello duplicate license files cause an error at run time on hello HDInsight cluster.</span></span> <span data-ttu-id="78508-149">Использование maven оттенок подключаемого модуля с hello `ApacheLicenseResourceTransformer` реализация предотвращает эту ошибку.</span><span class="sxs-lookup"><span data-stu-id="78508-149">Using maven-shade-plugin with hello `ApacheLicenseResourceTransformer` implementation prevents this error.</span></span>

    <span data-ttu-id="78508-150">Hello maven оттенок подключаемый модуль также создает jar полный (или fat JAR-файл), содержащий все зависимости hello, необходимые для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="78508-150">hello maven-shade-plugin also produces an uber jar (or fat jar) that contains all hello dependencies required by hello application.</span></span>
4. <span data-ttu-id="78508-151">Сохранить hello **pom.xml** файла.</span><span class="sxs-lookup"><span data-stu-id="78508-151">Save hello **pom.xml** file.</span></span>
5. <span data-ttu-id="78508-152">Создайте новый каталог с именем **conf** в hello **hbaseapp** каталога.</span><span class="sxs-lookup"><span data-stu-id="78508-152">Create a new directory named **conf** in hello **hbaseapp** directory.</span></span> <span data-ttu-id="78508-153">В hello **conf** каталога, создайте файл с именем **hbase-site.xml**.</span><span class="sxs-lookup"><span data-stu-id="78508-153">In hello **conf** directory, create a file named **hbase-site.xml**.</span></span> <span data-ttu-id="78508-154">Используйте следующие hello как hello содержимое файла hello:</span><span class="sxs-lookup"><span data-stu-id="78508-154">Use hello following as hello contents of hello file:</span></span>

        <?xml version="1.0"?>
        <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
        <!--
        /**
          * Copyright 2010 hello Apache Software Foundation
          *
          * Licensed toohello Apache Software Foundation (ASF) under one
          * or more contributor license agreements.  See hello NOTICE file
          * distributed with this work for additional information
          * regarding copyright ownership.  hello ASF licenses this file
          * tooyou under hello Apache License, Version 2.0 (the
          * "License"); you may not use this file except in compliance
          * with hello License.  You may obtain a copy of hello License at
          *
          *     http://www.apache.org/licenses/LICENSE-2.0
          *
          * Unless required by applicable law or agreed tooin writing, software
          * distributed under hello License is distributed on an "AS IS" BASIS,
          * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
          * See hello License for hello specific language governing permissions and
          * limitations under hello License.
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

    <span data-ttu-id="78508-155">Этот файл будет конфигурации HBase hello используется tooload для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78508-155">This file will be used tooload hello HBase configuration for an HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="78508-156">Это минимальный hbase-site.xml-файл и на нем hello bare минимальные значения для кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="78508-156">This is a minimal hbase-site.xml file, and it contains hello bare minimum settings for hello HDInsight cluster.</span></span>

6. <span data-ttu-id="78508-157">Сохранить hello **hbase-site.xml** файл.</span><span class="sxs-lookup"><span data-stu-id="78508-157">Save hello **hbase-site.xml** file.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="78508-158">Создание приложения hello</span><span class="sxs-lookup"><span data-stu-id="78508-158">Create hello application</span></span>
1. <span data-ttu-id="78508-159">Go toohello **hbaseapp\src\main\java\com\microsoft\examples** каталога и переименования hello app.java файл слишком**CreateTable.java**.</span><span class="sxs-lookup"><span data-stu-id="78508-159">Go toohello **hbaseapp\src\main\java\com\microsoft\examples** directory and rename hello app.java file too**CreateTable.java**.</span></span>
2. <span data-ttu-id="78508-160">Откройте hello **CreateTable.java** и замените существующее содержимое hello hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="78508-160">Open hello **CreateTable.java** file and replace hello existing contents with hello following code:</span></span>

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
            // hello following sets hello znode root for Linux-based HDInsight
            //config.set("zookeeper.znode.parent","/hbase-unsecure");

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

    <span data-ttu-id="78508-161">Это hello **CreateTable** класс, который будет создана таблица с именем **людей** и ее заполнение некоторых стандартных пользователей.</span><span class="sxs-lookup"><span data-stu-id="78508-161">This is hello **CreateTable** class, which will create a table named **people** and populate it with some predefined users.</span></span>
3. <span data-ttu-id="78508-162">Сохранить hello **CreateTable.java** файла.</span><span class="sxs-lookup"><span data-stu-id="78508-162">Save hello **CreateTable.java** file.</span></span>
4. <span data-ttu-id="78508-163">В hello **hbaseapp\src\main\java\com\microsoft\examples** каталога, создайте новый файл с именем **SearchByEmail.java**.</span><span class="sxs-lookup"><span data-stu-id="78508-163">In hello **hbaseapp\src\main\java\com\microsoft\examples** directory, create a new file named **SearchByEmail.java**.</span></span> <span data-ttu-id="78508-164">Используйте следующий код как hello содержимое этого файла hello.</span><span class="sxs-lookup"><span data-stu-id="78508-164">Use hello following code as hello contents of this file:</span></span>

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

            // Create a new regex filter
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

    <span data-ttu-id="78508-165">Hello **SearchByEmail** класс может быть tooquery используется для строк по адресу электронной почты.</span><span class="sxs-lookup"><span data-stu-id="78508-165">hello **SearchByEmail** class can be used tooquery for rows by email address.</span></span> <span data-ttu-id="78508-166">Так как он использует регулярное выражение фильтра, чтобы обеспечить строку или регулярное выражение при использовании класса hello.</span><span class="sxs-lookup"><span data-stu-id="78508-166">Because it uses a regular expression filter, you can provide either a string or a regular expression when using hello class.</span></span>
5. <span data-ttu-id="78508-167">Сохранить hello **SearchByEmail.java** файла.</span><span class="sxs-lookup"><span data-stu-id="78508-167">Save hello **SearchByEmail.java** file.</span></span>
6. <span data-ttu-id="78508-168">В hello **hbaseapp\src\main\hava\com\microsoft\examples** каталога, создайте новый файл с именем **DeleteTable.java**.</span><span class="sxs-lookup"><span data-stu-id="78508-168">In hello **hbaseapp\src\main\hava\com\microsoft\examples** directory, create a new file named **DeleteTable.java**.</span></span> <span data-ttu-id="78508-169">Используйте следующий код как hello содержимое этого файла hello.</span><span class="sxs-lookup"><span data-stu-id="78508-169">Use hello following code as hello contents of this file:</span></span>

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

    <span data-ttu-id="78508-170">Этот класс предназначен для очистки в этом примере, отключив и удаление таблицы hello созданные hello **CreateTable** класса.</span><span class="sxs-lookup"><span data-stu-id="78508-170">This class is for cleaning up this example by disabling and dropping hello table created by hello **CreateTable** class.</span></span>
7. <span data-ttu-id="78508-171">Сохранить hello **DeleteTable.java** файла.</span><span class="sxs-lookup"><span data-stu-id="78508-171">Save hello **DeleteTable.java** file.</span></span>

## <a name="build-and-package-hello-application"></a><span data-ttu-id="78508-172">Сборки и пакет приложения hello</span><span class="sxs-lookup"><span data-stu-id="78508-172">Build and package hello application</span></span>
1. <span data-ttu-id="78508-173">Откройте командную строку и измените каталоги toohello **hbaseapp** каталога.</span><span class="sxs-lookup"><span data-stu-id="78508-173">Open a command prompt and change directories toohello **hbaseapp** directory.</span></span>
2. <span data-ttu-id="78508-174">Используйте следующие команды toobuild JAR-файл, содержащий приложение hello hello.</span><span class="sxs-lookup"><span data-stu-id="78508-174">Use hello following command toobuild a JAR file that contains hello application:</span></span>

        mvn clean package

    <span data-ttu-id="78508-175">Это удаляет все предыдущие артефактов сборки, загружает все зависимости, которые еще не установлены, затем создает и пакеты приложения hello.</span><span class="sxs-lookup"><span data-stu-id="78508-175">This cleans any previous build artifacts, downloads any dependencies that have not already been installed, then builds and packages hello application.</span></span>
3. <span data-ttu-id="78508-176">Когда hello выполнения команды hello **hbaseapp\target** каталог содержит файл с именем **hbaseapp 1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="78508-176">When hello command completes, hello **hbaseapp\target** directory contains a file named **hbaseapp-1.0-SNAPSHOT.jar**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="78508-177">Hello **hbaseapp 1.0-SNAPSHOT.jar** файл является полный JAR-файл (иногда называется файловой системой fat jar), содержащий все зависимости hello необходимые приложения hello toorun.</span><span class="sxs-lookup"><span data-stu-id="78508-177">hello **hbaseapp-1.0-SNAPSHOT.jar** file is an uber jar (sometimes called a fat jar,) which contains all hello dependencies required toorun hello application.</span></span>

## <a name="upload-hello-jar-file-and-start-a-job"></a><span data-ttu-id="78508-178">Отправка hello JAR-файл и запустить задание</span><span class="sxs-lookup"><span data-stu-id="78508-178">Upload hello JAR file and start a job</span></span>
<span data-ttu-id="78508-179">Существует много способов tooupload кластера HDInsight tooyour файла, как описано в [передать данные для заданий Hadoop в HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="78508-179">There are many ways tooupload a file tooyour HDInsight cluster, as described in [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span> <span data-ttu-id="78508-180">Hello следующие действия с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="78508-180">hello following steps use Azure PowerShell.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. <span data-ttu-id="78508-181">После установки и настройки Azure PowerShell создайте файл с именем **hbase-runner.psm1**.</span><span class="sxs-lookup"><span data-stu-id="78508-181">After installing and configuring Azure PowerShell, create a new file named **hbase-runner.psm1**.</span></span> <span data-ttu-id="78508-182">Используйте следующие hello как hello содержимое этого файла:</span><span class="sxs-lookup"><span data-stu-id="78508-182">Use hello following as hello contents of this file:</span></span>

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

    <span data-ttu-id="78508-183">Этот файл содержит два модуля:</span><span class="sxs-lookup"><span data-stu-id="78508-183">This file contains two modules:</span></span>

   * <span data-ttu-id="78508-184">**Добавить HDInsightFile** -использовать tooHDInsight tooupload файлов</span><span class="sxs-lookup"><span data-stu-id="78508-184">**Add-HDInsightFile** - used tooupload files tooHDInsight</span></span>
   * <span data-ttu-id="78508-185">**Начало HBaseExample** -используемые классы toorun hello, созданного ранее</span><span class="sxs-lookup"><span data-stu-id="78508-185">**Start-HBaseExample** - used toorun hello classes created earlier</span></span>
2. <span data-ttu-id="78508-186">Сохранить hello **hbase runner.psm1** файла.</span><span class="sxs-lookup"><span data-stu-id="78508-186">Save hello **hbase-runner.psm1** file.</span></span>
3. <span data-ttu-id="78508-187">Откройте новое окно Azure PowerShell, измените каталоги toohello **hbaseapp** каталога, а затем выполнения hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="78508-187">Open a new Azure PowerShell window, change directories toohello **hbaseapp** directory, and then run hello following command.</span></span>

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    <span data-ttu-id="78508-188">Изменение расположения toohello путь hello hello **hbase runner.psm1** файла, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="78508-188">Change hello path toohello location of hello **hbase-runner.psm1** file created earlier.</span></span> <span data-ttu-id="78508-189">Эта строка регистрирует модуль hello для этого сеанса Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="78508-189">This registers hello module for this Azure PowerShell session.</span></span>
4. <span data-ttu-id="78508-190">Используйте hello следующая команда tooupload hello **hbaseapp 1.0-SNAPSHOT.jar** tooyour кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78508-190">Use hello following command tooupload hello **hbaseapp-1.0-SNAPSHOT.jar** tooyour HDInsight cluster.</span></span>

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    <span data-ttu-id="78508-191">Замените **hdinsightclustername** с hello имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78508-191">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="78508-192">Команда Hello отправляет hello **hbaseapp 1.0-SNAPSHOT.jar** toohello **JAR-файлов и пример** расположение в hello основного хранилища для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78508-192">hello command uploads hello **hbaseapp-1.0-SNAPSHOT.jar** toohello **example/jars** location in hello primary storage for your HDInsight cluster.</span></span>
5. <span data-ttu-id="78508-193">После загрузки файлов hello, используйте следующий hello кода toocreate таблицы с помощью hello **hbaseapp**:</span><span class="sxs-lookup"><span data-stu-id="78508-193">After hello files are uploaded, use hello following code toocreate a table using hello **hbaseapp**:</span></span>

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    <span data-ttu-id="78508-194">Замените **hdinsightclustername** с hello имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78508-194">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="78508-195">Эта команда создает таблицу с именем **people** в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78508-195">This command creates a new table named **people** in your HDInsight cluster.</span></span> <span data-ttu-id="78508-196">Эта команда не содержит никаких выходных данных окна консоли «hello».</span><span class="sxs-lookup"><span data-stu-id="78508-196">This command does not show any output in hello console window.</span></span>
6. <span data-ttu-id="78508-197">toosearch для записи в таблице hello, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="78508-197">toosearch for entries in hello table, use hello following command:</span></span>

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    <span data-ttu-id="78508-198">Замените **hdinsightclustername** с hello имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78508-198">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="78508-199">Эта команда использует hello **SearchByEmail** класса toosearch для всех строк, где hello **contactinformation** семейство столбца и hello **электронной почты** столбец, содержащий строку hello **contoso.com**. Должно появиться hello следующие результаты:</span><span class="sxs-lookup"><span data-stu-id="78508-199">This command uses hello **SearchByEmail** class toosearch for any rows where hello **contactinformation** column family and hello **email** column, contains hello string **contoso.com**. You should receive hello following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="78508-200">С помощью **fabrikam.com** для hello `-emailRegex` значение возвращает hello пользователи, имеющие **fabrikam.com** в поле hello электронной почты.</span><span class="sxs-lookup"><span data-stu-id="78508-200">Using **fabrikam.com** for hello `-emailRegex` value returns hello users that have **fabrikam.com** in hello email field.</span></span> <span data-ttu-id="78508-201">Поскольку этот поиск реализуется с помощью обычного фильтра основано на выражении, можно также ввести регулярные выражения, такие как **^ r**, какие операции возвращает, где начинается hello электронной почты с hello буква «r».</span><span class="sxs-lookup"><span data-stu-id="78508-201">Since this search is implemented by using a regular expression-based filter, you can also enter regular expressions, such as **^r**, which returns entries where hello email begins with hello letter 'r'.</span></span>

## <a name="delete-hello-table"></a><span data-ttu-id="78508-202">Удалить таблицу hello</span><span class="sxs-lookup"><span data-stu-id="78508-202">Delete hello table</span></span>
<span data-ttu-id="78508-203">После этого пример hello используйте hello следующие команды из сеанса toodelete hello Azure PowerShell hello **людей** таблицы, используемой в этом примере:</span><span class="sxs-lookup"><span data-stu-id="78508-203">When you are done with hello example, use hello following command from hello Azure PowerShell session toodelete hello **people** table used in this example:</span></span>

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

<span data-ttu-id="78508-204">Замените **hdinsightclustername** с hello имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78508-204">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="78508-205">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="78508-205">Troubleshooting</span></span>
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="78508-206">При использовании Start-HBaseExample результаты отсутствуют или не получено каких-либо неожиданных результатов.</span><span class="sxs-lookup"><span data-stu-id="78508-206">No results or unexpected results when using Start-HBaseExample</span></span>
<span data-ttu-id="78508-207">Используйте hello `-showErr` параметр tooview hello стандартные ошибки (STDERR), созданного во время выполнения задания hello.</span><span class="sxs-lookup"><span data-stu-id="78508-207">Use hello `-showErr` parameter tooview hello standard error (STDERR) that is produced while running hello job.</span></span>
