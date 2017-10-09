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
# <a name="build-java-applications-for-apache-hbase"></a>Создание приложений Java для Apache HBase

Узнайте, как toocreate [Apache HBase](http://hbase.apache.org/) приложение Java. Затем можно используйте приложение hello с HBase на Azure HDInsight.

Hello шаги в этом документе используется [Maven](http://maven.apache.org/) toocreate и построения проекта hello. Maven — это программное обеспечение управления проектами и понимания средство, которое позволяет вам toobuild программное обеспечение, документация и отчеты для проектов Java.

> [!NOTE]
> Hello в данном пошаговом руководстве были недавно протестированных с HDInsight 3.6.

> [!IMPORTANT]
> Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="requirements"></a>Требования

* [Пакет JDK для платформы Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html) версии 8 или более поздней.

    > [!NOTE]
    > Для HDInsight 3.5 и более поздних версий требуется Java 8. Для работы более ранних версий HDInsight требуется Java 7.

* [Maven](http://maven.apache.org/)

* [Кластер Azure HDInsight под управлением Linux с HBase.](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > Hello в данном пошаговом руководстве были проверены с версиями кластеров HDInsight 3.4 и 3.5. значения по умолчанию Hello в примерах предназначены для кластера HDInsight 3.5.

## <a name="create-hello-project"></a>Создание проекта hello

1. Из командной строки hello в среде разработки, измените каталоги toohello место, куда toocreate hello проекта, например, `cd code\hbase`.

2. Используйте hello **mvn** команду, которая устанавливается вместе с Maven, toogenerate hello формирование шаблонов для проекта hello.

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > Если вы используете PowerShell, необходимо заключить hello `-D` параметров в двойные кавычки.
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    Эта команда создает каталог с точно такое же имя, как hello hello **artifactID** параметра (**hbaseapp** в этом примере.) В этом каталоге содержатся hello следующих элементов:

   * **pom.XML**: hello объектной модели Project ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) содержит сведения и конфигурации, используемой toobuild hello проекта.
   * **src**: hello каталог, содержащий hello **main-java/com/microsoft/примеры** каталог, в котором создается приложение hello.

3. Удалить hello `src/test/java/com/microsoft/examples/apptest.java` файла. Он не используется в этом примере.

## <a name="update-hello-project-object-model"></a>Обновление hello объектной модели Project

1. Изменить hello `pom.xml` и добавьте следующий код внутри hello hello `<dependencies>` раздела:

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

    В этом разделе показывает hello проект должен **hbase клиента** и **ядрами Финиксе** компонентов. Во время компиляции эти зависимости загружаются из репозитория Maven по умолчанию hello. Можно использовать hello [Maven центральный репозиторий поиска](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn Дополнительные сведения об этой зависимости.

   > [!IMPORTANT]
   > номер версии Hello hello hbase клиента должна совпадать hello версией, предоставляемого с кластером HDInsight HBase. Используйте следующие таблицы toofind hello правильный номер версии hello.

   | Версия кластера HDInsight | Toouse версия HBase |
   | --- | --- |
   | 3.2 |0.98.4-hadoop2 |
   | 3.3, 3.4, 3.5 и 3.6 |1.1.2 |

    Дополнительные сведения о версии HDInsight и компонентов см. в разделе [Каковы hello различных Hadoop компоненты, доступные с HDInsight](hdinsight-component-versioning.md).

3. Добавьте следующий код toohello hello **pom.xml** файла. Этот текст должен находиться внутри hello `<project>...</project>` тегов в hello файла, например, между `</dependencies>` и `</project>`.

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

    В этом разделе настраивается ресурс (`conf/hbase-site.xml`), который содержит информацию о конфигурации для HBase.

   > [!NOTE]
   > Также можно настроить значения конфигурации непосредственно из кода. См. комментарии hello в hello `CreateTable` примере.

    В этом разделе также настраивает hello [подключаемого модуля компилятора Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) и [подключаемого модуля оттенок Maven](http://maven.apache.org/plugins/maven-shade-plugin/). Компилятор Hello подключаемый модуль — используется toocompile hello топологии. Подключаемый модуль оттенок Hello — дублирования лицензии tooprevent используется в пакете JAR hello, построенного с Maven. Этот подключаемый модуль является ошибкой «повторяющиеся файлы лицензии» используется tooprevent во время выполнения в кластере HDInsight hello. Использование maven оттенок подключаемого модуля с hello `ApacheLicenseResourceTransformer` реализация предотвращает ошибки hello.

    Привет, maven оттенок-подключаемый модуль также создает полный JAR-файл, содержащий все зависимости hello, необходимые для приложения hello.

4. Сохранить hello `pom.xml` файла.

5. Создайте каталог с именем `conf` в hello `hbaseapp` каталога. Этот каталог является используется toohold сведения о конфигурации для подключения tooHBase.

6. Используйте hello следующая команда конфигурации HBase hello toocopy из toohello кластер HBase hello `conf` каталога. Замените `USERNAME` с именем hello SSH имени входа. а `CLUSTERNAME` — именем кластера HDInsight:

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   Дополнительные сведения об использовании `ssh` и `scp` см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="create-hello-application"></a>Создание приложения hello

1. Go toohello `hbaseapp/src/main/java/com/microsoft/examples` каталога и переименования hello app.java файл слишком`CreateTable.java`.

2. Откройте hello `CreateTable.java` и замените существующее содержимое hello hello следующий текст:

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

    Данный пример кода является hello **CreateTable** класс, который создает таблицу с именем **людей** и ее заполнение некоторых стандартных пользователей.

3. Сохранить hello `CreateTable.java` файла.

4. В hello `hbaseapp/src/main/java/com/microsoft/examples` каталога, создайте файл с именем `SearchByEmail.java`. Используйте hello после текста как hello содержимое этого файла:

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

    Hello **SearchByEmail** класс может быть tooquery используется для строк по адресу электронной почты. Так как он использует регулярное выражение фильтра, чтобы обеспечить строку или регулярное выражение при использовании класса hello.

5. Сохранить hello `SearchByEmail.java` файла.

6. В hello `hbaseapp/src/main/hava/com/microsoft/examples` каталога, создайте файл с именем `DeleteTable.java`. Используйте hello после текста как hello содержимое этого файла:

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

    Этот класс очищает hello HBase таблицы, созданные в этом примере отключение и удаление таблицы hello созданные hello `CreateTable` класса.

7. Сохранить hello `DeleteTable.java` файла.

## <a name="build-and-package-hello-application"></a>Сборки и пакет приложения hello

1. Из hello `hbaseapp` каталога, используйте hello следующая команда toobuild JAR-файл, содержащий приложение hello:

    ```bash
    mvn clean package
    ```

    Эта команда выполняет сборку и пакеты hello приложения в JAR-файлу.

2. Когда hello выполнения команды hello `hbaseapp/target` каталог содержит файл с именем `hbaseapp-1.0-SNAPSHOT.jar`.

   > [!NOTE]
   > Hello `hbaseapp-1.0-SNAPSHOT.jar` файл является полный jar. Он содержит все необходимые toorun приложений hello зависимости hello.


## <a name="upload-hello-jar-and-run-jobs-ssh"></a>Отправка hello JAR-ФАЙЛ и запустите задания (SSH)

Здравствуйте, выполнив действия, используйте `scp` toocopy hello JAR toohello первичного головного узла к HBase на HDInsight кластера. Hello `ssh` команда будет использовать tooconnect toohello кластера и выполнить пример hello непосредственно на головном узле hello.

1. tooupload hello jar toohello кластер, hello используйте следующую команду:

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    Замените `USERNAME` с именем hello SSH имени входа. а `CLUSTERNAME` — именем кластера HDInsight.

2. кластер HBase toohello tooconnect, hello используйте следующую команду:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Замените `USERNAME` hello имя входа SSH. а `CLUSTERNAME` — именем кластера HDInsight.

3. к таблице HBase с помощью toocreate hello приложения Java, hello используйте следующую команду:

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    Эта команда создает таблицу HBase с именем **people** и заполняет ее данными.

4. toosearch для адресов электронной почты, которые хранятся в таблице hello, hello используйте следующую команду:

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    Появляется hello следующие результаты:

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. Таблица toodelete hello, hello используйте следующую команду:

    

## <a name="upload-hello-jar-and-run-jobs-powershell"></a>Отправка hello JAR-ФАЙЛ и запустите задания (PowerShell)

Hello действий использовать Azure PowerShell tooupload hello JAR toohello хранилища по умолчанию для кластера HBase. Командлеты HDInsight, то используется toorun hello примеры удаленно.

1. После установки и настройки Azure PowerShell создайте файл с именем `hbase-runner.psm1`. Используйте hello после текста как hello содержимое этого файла:

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

    Этот файл содержит два модуля:

   * **Добавить HDInsightFile** — служат tooupload файлы toohello кластера
   * **Начало HBaseExample** -используемые классы toorun hello, созданного ранее

2. Сохранить hello `hbase-runner.psm1` файла.

3. Откройте новое окно Azure PowerShell, измените каталоги toohello `hbaseapp` каталога, а затем выполнения hello следующую команду:

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    Изменение расположения toohello путь hello hello `hbase-runner.psm1` файла, созданного ранее. Эта команда регистрирует модуль hello Azure PowerShell.

4. Используйте hello следующая команда tooupload hello `hbaseapp-1.0-SNAPSHOT.jar` tooyour кластера.

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    Замените `hdinsightclustername` с hello имя кластера. Команда Hello отправляет hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` расположение в hello основного хранилища для кластера.

5. Здравствуйте, таблицы с помощью toocreate `hbaseapp`, использовать hello следующую команду:

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    Замените `hdinsightclustername` с hello имя кластера.

    Эта команда создает таблицу с именем **people** в HBase в кластере HDInsight. Эта команда не содержит никаких выходных данных окна консоли «hello».

6. toosearch для записи в таблице hello, hello используйте следующую команду:

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    Замените `hdinsightclustername` с hello имя кластера.

    Эта команда использует hello `SearchByEmail` класса toosearch для всех строк, где hello `contactinformation` семейство столбца и hello `email` столбец, содержащий строку hello `contoso.com`. Должно появиться hello следующие результаты:

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    С помощью **fabrikam.com** для hello `-emailRegex` значение возвращает hello пользователи, имеющие **fabrikam.com** в поле hello электронной почты. Также можно использовать регулярные выражения как hello поисковому запросу. Например **^ r** Возвращает адреса, начинающиеся с буквы hello 'r' по электронной почте.

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a>При использовании Start-HBaseExample результаты отсутствуют или не получено каких-либо неожиданных результатов.

Используйте hello `-showErr` параметр tooview hello стандартные ошибки (STDERR), созданного во время выполнения задания hello.

## <a name="delete-hello-table"></a>Удалить таблицу hello

После этого пример hello использовать hello, следуя toodelete hello **людей** таблицы, используемой в этом примере:

__Из сеанса `ssh`__ :

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

__Из Azure PowerShell__:

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a>Дальнейшие действия

[Узнайте, как toouse белка SQL с HBase](hdinsight-hbase-phoenix-squirrel-linux.md)
