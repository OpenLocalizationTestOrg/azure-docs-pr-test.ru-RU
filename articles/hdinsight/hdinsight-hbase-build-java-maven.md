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
# <a name="use-maven-toobuild-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a>Используйте Maven toobuild Java приложений, использующих HBase с HDInsight под управлением Windows (Hadoop)
Узнайте, как toocreate и построения [Apache HBase](http://hbase.apache.org/) приложение Java с помощью Apache Maven. Затем можно используйте приложение hello с Azure HDInsight (Hadoop).

[Maven](http://maven.apache.org/) — это проект управления и понимания программа, позволяющий toobuild программное обеспечение, документация и отчеты для проектов Java. В этой статье вы узнаете, как toouse его toocreate простое приложение Java, создаваемые, запросы и удаляет HBase на кластере Azure HDInsight.

> [!IMPORTANT]
> Hello в данном пошаговом руководстве требуется кластер HDInsight, который использует Windows. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="requirements"></a>Требования
* [Пакет JDK для платформы Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html) версии 7 или более поздней.
* [Maven](http://maven.apache.org/)
* Кластер HDInsight под управлением Windows с HBase

    > [!NOTE]
    > с версиями кластеров HDInsight версии 3.2 и 3.3 протестированы Hello в данном пошаговом руководстве. для кластера HDInsight 3.3, значений по умолчанию Hello в примерах.

## <a name="create-hello-project"></a>Создание проекта hello
1. Из командной строки hello в среде разработки, измените каталоги toohello место, куда toocreate hello проекта, например, `cd code\hdinsight`.
2. Используйте hello **mvn** команду, которая устанавливается вместе с Maven, toogenerate hello формирование шаблонов для проекта hello.

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    Эта команда создает каталог в текущем расположении hello, с именем hello, заданным hello **artifactID** параметра (**hbaseapp** в этом примере.) В этом каталоге содержатся hello следующих элементов:

   * **pom.XML**: hello объектной модели Project ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) содержит сведения и конфигурации, используемой toobuild hello проекта.
   * **src**: hello каталог, содержащий hello **main\java\com\microsoft\examples** каталога, в котором будет создать приложение hello.
3. Удалить hello **src\test\java\com\microsoft\examples\apptest.java** файл, поскольку он не используется в этом примере.

## <a name="update-hello-project-object-model"></a>Обновление hello объектной модели Project
1. Изменить hello **pom.xml** и добавьте следующий код внутри hello hello `<dependencies>` раздела:

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    В этом разделе приведен Maven, hello проекта требуется **hbase клиента** версии **1.1.2**. Во время компиляции Эта зависимость загружается из репозитория Maven по умолчанию hello. Можно использовать hello [Maven центральный репозиторий поиска](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn Дополнительные сведения об этой зависимости.

   > [!IMPORTANT]
   > номер версии Hello должен совпадать hello версия HBase, который входит в состав кластера HDInsight. Используйте следующие таблицы toofind hello правильный номер версии hello.
   >
   >

   | Версия кластера HDInsight | Toouse версия HBase |
   | --- | --- |
   | 3.2 |0.98.4-hadoop2 |
   | 3.3 |1.1.2 |

    Дополнительные сведения о версии HDInsight и компонентов см. в разделе [Каковы hello различных Hadoop компоненты, доступные с HDInsight](hdinsight-component-versioning.md).
2. При использовании с кластером HDInsight 3.3, необходимо добавить следующие toohello hello `<dependencies>` раздела:

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    Эта зависимость будет загружаться hello Финиксе основных компонентов, которые используется версия Hbase 1.1.x.
3. Добавьте следующий код toohello hello **pom.xml** файла. В этом разделе, должны находиться внутри hello `<project>...</project>` тегов в hello файла, например, между `</dependencies>` и `</project>`.

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

    Hello `<resources>` раздел настраивает ресурс (**conf\hbase-site.xml**), содержащий сведения о конфигурации для HBase.

   > [!NOTE]
   > Также можно настроить значения конфигурации непосредственно из кода. См. комментарии hello в hello **CreateTable** для как в следующем примере toodo это.
   >
   >

    Это `<plugins>` раздел настраивает hello [подключаемого модуля компилятора Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) и [подключаемого модуля оттенок Maven](http://maven.apache.org/plugins/maven-shade-plugin/). Компилятор Hello подключаемый модуль — используется toocompile hello топологии. Подключаемый модуль оттенок Hello — дублирования лицензии tooprevent используется в пакете JAR hello, построенного с Maven. Hello используется обусловлено тем, что файлы повторяющиеся лицензии hello приводят к ошибке во время выполнения в кластере HDInsight hello. Использование maven оттенок подключаемого модуля с hello `ApacheLicenseResourceTransformer` реализация предотвращает эту ошибку.

    Hello maven оттенок подключаемый модуль также создает jar полный (или fat JAR-файл), содержащий все зависимости hello, необходимые для приложения hello.
4. Сохранить hello **pom.xml** файла.
5. Создайте новый каталог с именем **conf** в hello **hbaseapp** каталога. В hello **conf** каталога, создайте файл с именем **hbase-site.xml**. Используйте следующие hello как hello содержимое файла hello:

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

    Этот файл будет конфигурации HBase hello используется tooload для кластера HDInsight.

   > [!NOTE]
   > Это минимальный hbase-site.xml-файл и на нем hello bare минимальные значения для кластера HDInsight hello.

6. Сохранить hello **hbase-site.xml** файл.

## <a name="create-hello-application"></a>Создание приложения hello
1. Go toohello **hbaseapp\src\main\java\com\microsoft\examples** каталога и переименования hello app.java файл слишком**CreateTable.java**.
2. Откройте hello **CreateTable.java** и замените существующее содержимое hello hello, следующий код:

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

    Это hello **CreateTable** класс, который будет создана таблица с именем **людей** и ее заполнение некоторых стандартных пользователей.
3. Сохранить hello **CreateTable.java** файла.
4. В hello **hbaseapp\src\main\java\com\microsoft\examples** каталога, создайте новый файл с именем **SearchByEmail.java**. Используйте следующий код как hello содержимое этого файла hello.

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

    Hello **SearchByEmail** класс может быть tooquery используется для строк по адресу электронной почты. Так как он использует регулярное выражение фильтра, чтобы обеспечить строку или регулярное выражение при использовании класса hello.
5. Сохранить hello **SearchByEmail.java** файла.
6. В hello **hbaseapp\src\main\hava\com\microsoft\examples** каталога, создайте новый файл с именем **DeleteTable.java**. Используйте следующий код как hello содержимое этого файла hello.

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

    Этот класс предназначен для очистки в этом примере, отключив и удаление таблицы hello созданные hello **CreateTable** класса.
7. Сохранить hello **DeleteTable.java** файла.

## <a name="build-and-package-hello-application"></a>Сборки и пакет приложения hello
1. Откройте командную строку и измените каталоги toohello **hbaseapp** каталога.
2. Используйте следующие команды toobuild JAR-файл, содержащий приложение hello hello.

        mvn clean package

    Это удаляет все предыдущие артефактов сборки, загружает все зависимости, которые еще не установлены, затем создает и пакеты приложения hello.
3. Когда hello выполнения команды hello **hbaseapp\target** каталог содержит файл с именем **hbaseapp 1.0-SNAPSHOT.jar**.

   > [!NOTE]
   > Hello **hbaseapp 1.0-SNAPSHOT.jar** файл является полный JAR-файл (иногда называется файловой системой fat jar), содержащий все зависимости hello необходимые приложения hello toorun.

## <a name="upload-hello-jar-file-and-start-a-job"></a>Отправка hello JAR-файл и запустить задание
Существует много способов tooupload кластера HDInsight tooyour файла, как описано в [передать данные для заданий Hadoop в HDInsight](hdinsight-upload-data.md). Hello следующие действия с помощью Azure PowerShell.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. После установки и настройки Azure PowerShell создайте файл с именем **hbase-runner.psm1**. Используйте следующие hello как hello содержимое этого файла:

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

    Этот файл содержит два модуля:

   * **Добавить HDInsightFile** -использовать tooHDInsight tooupload файлов
   * **Начало HBaseExample** -используемые классы toorun hello, созданного ранее
2. Сохранить hello **hbase runner.psm1** файла.
3. Откройте новое окно Azure PowerShell, измените каталоги toohello **hbaseapp** каталога, а затем выполнения hello следующую команду.

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    Изменение расположения toohello путь hello hello **hbase runner.psm1** файла, созданного ранее. Эта строка регистрирует модуль hello для этого сеанса Azure PowerShell.
4. Используйте hello следующая команда tooupload hello **hbaseapp 1.0-SNAPSHOT.jar** tooyour кластера HDInsight.

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    Замените **hdinsightclustername** с hello имя кластера HDInsight. Команда Hello отправляет hello **hbaseapp 1.0-SNAPSHOT.jar** toohello **JAR-файлов и пример** расположение в hello основного хранилища для кластера HDInsight.
5. После загрузки файлов hello, используйте следующий hello кода toocreate таблицы с помощью hello **hbaseapp**:

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    Замените **hdinsightclustername** с hello имя кластера HDInsight.

    Эта команда создает таблицу с именем **people** в кластере HDInsight. Эта команда не содержит никаких выходных данных окна консоли «hello».
6. toosearch для записи в таблице hello, hello используйте следующую команду:

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    Замените **hdinsightclustername** с hello имя кластера HDInsight.

    Эта команда использует hello **SearchByEmail** класса toosearch для всех строк, где hello **contactinformation** семейство столбца и hello **электронной почты** столбец, содержащий строку hello **contoso.com**. Должно появиться hello следующие результаты:

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    С помощью **fabrikam.com** для hello `-emailRegex` значение возвращает hello пользователи, имеющие **fabrikam.com** в поле hello электронной почты. Поскольку этот поиск реализуется с помощью обычного фильтра основано на выражении, можно также ввести регулярные выражения, такие как **^ r**, какие операции возвращает, где начинается hello электронной почты с hello буква «r».

## <a name="delete-hello-table"></a>Удалить таблицу hello
После этого пример hello используйте hello следующие команды из сеанса toodelete hello Azure PowerShell hello **людей** таблицы, используемой в этом примере:

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

Замените **hdinsightclustername** с hello имя кластера HDInsight.

## <a name="troubleshooting"></a>Устранение неполадок
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a>При использовании Start-HBaseExample результаты отсутствуют или не получено каких-либо неожиданных результатов.
Используйте hello `-showErr` параметр tooview hello стандартные ошибки (STDERR), созданного во время выполнения задания hello.
