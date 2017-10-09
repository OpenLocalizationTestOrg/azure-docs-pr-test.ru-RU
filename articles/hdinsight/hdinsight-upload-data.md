---
title: "aaaUpload данных для заданий Hadoop в HDInsight | Документы Microsoft"
description: "Узнайте, как данные tooupload и доступ для заданий Hadoop в HDInsight с помощью hello Azure CLI, обозреватель хранилища Azure, Azure PowerShell, Командная строка hello Hadoop или Sqoop."
keywords: "etl hadoop, вставка данных в hadoop, загрузка данных hadoop"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 56b913ee-0f9a-4e9f-9eaf-c571f8603dd6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: jgao
ms.openlocfilehash: 15da602085d41c19789e34800f3d9e238d7d1de8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a>Отправка данных для заданий Hadoop в HDInsight
Служба Azure HDInsight — это полнофункциональная распределенная файловая система Hadoop (HDFS), в основе которой лежит хранилище BLOB-объектов Azure. Он разработан вызвать toocustomers единую tooprovide расширение HDFS. Он позволяет hello полный набор компонентов в toooperate экосистема Hadoop hello непосредственно на hello данных, которыми он управляет. Хранилище BLOB-объектов Azure и HDFS — это разные файловые системы, оптимизированные для хранения и обработки данных. Сведения о hello преимущества использования службы хранилища больших двоичных объектов Azure см. в разделе [хранилища больших двоичных объектов Azure для использования с HDInsight][hdinsight-storage].

**Предварительные требования**

Обратите внимание, hello следующие требования перед началом:

* Кластер Azure HDInsight. Инструкции см. в разделе [Приступая к работе с Azure HDInsight][hdinsight-get-started] или [Подготовка кластеров HDInsight][hdinsight-provision].

## <a name="why-blob-storage"></a>Зачем нужно хранилище BLOB-объектов?
Azure HDInsight, кластеры, как правило, развертывать toorun задания MapReduce, а hello кластеров, удаляются после выполнения этих заданий. Поддержание данных hello в кластерах hello HDFS, после завершения вычисления бы дорогих способом toostore эти данные. Хранилище Azure BLOB-объекта — высокой доступности, высокую масштабируемость, высокий уровень производительности, параметр низкой стоимости и совместного использования хранилища для данных, являющихся toobe HDInsight для обработки. Хранение данных в большой двоичный объект включает hello кластеров HDInsight, используемых для вычисления toobe безопасно снята без потери данных.

### <a name="directories"></a>Каталоги
В контейнерах хранилища BLOB-объектов данные хранятся в виде пар «ключ — значение». Иерархия каталогов отсутствует. Здравствуйте, однако «/» можно использовать знак toomake hello имя ключа, он отображается, как если бы файл хранится в структуре каталогов. HDInsight видит эти каталоги так, как если бы они были реальными.

Например, ключ BLOB-объекта может выглядеть следующим образом: *input/log1.txt*. Без фактического «вход» каталог существует, но из-за наличия toohello hello символ «/» в имя ключа hello, он имеет вид hello пути к файлу.

Поэтому, если вы пользуетесь средствами Azure Explorer, вы можете заметить, что некоторые файлы имеют размер 0 байт. Эти файлы служат двум целям.

* Если пустые папки, они указывают hello существования папки hello. Хранилище Azure BLOB-объекта — достаточно некий tooknow, если существует большой двоичный объект, называется foo и панелью, что папку с именем **foo**. Но hello только toosignify способом, называется пустую папку **foo** является этот файл 0 байтов на месте.
* Они содержат, что специальные метаданные, необходимые по hello Hadoop файловой системы, в частности разрешения hello и владельцев папок hello.

## <a name="command-line-utilities"></a>Служебные программы командной строки
Корпорация Майкрософт предоставляет следующие служебные программы toowork с хранилищем больших двоичных объектов Azure hello.

| Средство | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Интерфейс командной строки Azure][azurecli] |✔ |✔ |✔ |
| [Azure PowerShell][azure-powershell] | | |✔ |
| [AzCopy][azure-azcopy] | | |✔ |
| [Команда Hadoop](#commandline) |✔ |✔ |✔ |

> [!NOTE]
> Хотя hello Azure CLI, Azure PowerShell и AzCopy можно использовать из вне Azure, hello Hadoop команда доступна только для кластера HDInsight hello и разрешает только загрузка данных из локальной файловой системе hello в хранилище больших двоичных объектов Azure.
>
>

### <a id="xplatcli"></a>Интерфейс командной строки Azure
Hello Azure CLI — это кросс платформенных средство, которое позволяет вам toomanage Azure службы. Используйте следующие шаги tooupload данных tooAzure BLOB-объекта хранилища hello.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. [Установка и настройка hello Azure CLI для Mac, Linux и Windows](../cli-install-nodejs.md).
2. Откройте командную строку, bash или другие оболочки и использовать hello, следуя tooauthenticate tooyour подписки Azure.

        azure login

    При появлении запроса введите hello имя пользователя и пароль для вашей подписки.
3. Введите hello, следующая команда учетных записей хранения toolist hello для вашей подписки:

        azure storage account list
4. Выберите учетную запись хранения hello, содержащий большой двоичный объект hello нужные toowork с, а затем использовать hello, следующая команда tooretrieve hello ключа для этой учетной записи:

        azure storage account keys list <storage-account-name>

    Команда должна вернуть **первичный** и **вторичный** ключи. Копировать hello **основной** значение ключа, так как он будет использоваться hello дальнейшие действия.
5. Используйте следующие команды tooretrieve список контейнеров больших двоичных объектов в учетной записи хранилища hello hello:

        azure storage container list -a <storage-account-name> -k <primary-key>
6. Используйте следующие команды tooupload hello и загрузите файлы toohello больших двоичных объектов:

   * tooupload файла:

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * toodownload файла:

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> Если вы будете всегда работать с hello же учетную запись хранения, можно задать следующие переменные среды вместо указания учетной записи hello hello и ключа для каждой команды:
>
> * **AZURE\_ХРАНЕНИЯ\_учетной записи**: hello имя учетной записи хранения
> * **AZURE\_ХРАНЕНИЯ\_доступа\_ключ**: hello ключ учетной записи хранения
>
>

### <a id="powershell"></a>Azure PowerShell
Azure PowerShell — это среда сценариев, можно использовать toocontrol и автоматизации развертывания hello и управления ими рабочих нагрузок в Azure. Сведения о настройке вашей рабочей станции toorun Azure PowerShell см. в разделе [Установка и настройка Azure PowerShell](/powershell/azure/overview).

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

**tooupload tooAzure локального файла хранилища больших двоичных объектов**

1. Откройте hello консоли Azure PowerShell, как описано в [Установка и настройка Azure PowerShell](/powershell/azure/overview).
2. Задайте значения hello hello первые пять переменных в hello, выполнив сценарий.

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get hello storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create hello storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy hello file from local workstation toohello Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. Вставить hello в toorun консоли Azure PowerShell hello его toocopy hello файл скрипта.

Примеры PowerShell toowork скрипты, созданные с HDInsight, в разделе [средства HDInsight](https://github.com/blackmist/hdinsight-tools).

### <a id="azcopy"></a>AzCopy
AzCopy — это средство командной строки, разработанные задачу hello toosimplify переноса данных в действие и из учетной записи хранилища Azure. Ее можно использовать отдельно или добавить в существующее приложение. [Скачайте AzCopy][azure-azcopy-download].

Hello синтаксисе AzCopy является:

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

Дополнительные сведения см. в статье [Приступая к работе со служебной программой командной строки AzCopy][azure-azcopy].

### <a id="commandline"></a>Командная строка Hadoop
Командная строка Hello Hadoop полезен только для хранения данных в хранилище больших двоичных объектов при hello данные уже находятся на головном узле кластера hello.

В порядке toouse hello команда Hadoop сначала необходимо подключить toohello головному узлу с помощью одного из следующих методов hello:

* **HDInsight под управлением Windows**: [подключение с помощью удаленного рабочего стола](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)
* **HDInsight под управлением Linux**: подключение с использованием SSH ([hello команды SSH](hdinsight-hadoop-linux-use-ssh-unix.md) или [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))

После подключения можно использовать следующий синтаксис tooupload toostorage файл hello.

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

Например, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`

Поскольку hello по умолчанию файловой системы для HDInsight в хранилище больших двоичных объектов Azure, /example/data.txt на самом деле в хранилище больших двоичных объектов Azure. Можно также ссылаться toohello файл как:

    wasb:///example/data/data.txt

или

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

Список других команд Hadoop, которые работают с файлами, см. на странице [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html).

> [!WARNING]
> В кластерах HBase hello размер блока по умолчанию используется при записи данных — 256 КБ. Это хорошо работает при использовании API HBase или интерфейсы API REST, с помощью hello `hadoop` или `hdfs dfs` более ~ 12 ГБ данных toowrite команды приводит к ошибке. В разделе hello [исключение хранилища для записи в большой двоичный объект](#storageexception) ниже, в разделе для получения дополнительной информации.
>
>

## <a name="graphical-clients"></a>Графические клиенты
Существуют также несколько приложений, которые предоставляют графический интерфейс для работы с хранилищем Azure. Hello ниже приведен список некоторых из этих приложений:

| Клиент | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Microsoft Visual Studio Tools для HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |✔ |✔ |✔ |
| [Azure Storage Explorer;](http://storageexplorer.com/) |✔ |✔ |✔ |
| [Cloud Storage Studio 2;](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |✔ |
| [CloudXplorer;](http://clumsyleaf.com/products/cloudxplorer) | | |✔ |
| [Azure Explorer;](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |✔ |
| [Cyberduck](https://cyberduck.io/) | |✔ |✔ |

### <a name="visual-studio-tools-for-hdinsight"></a>Visual Studio Tools для HDInsight
Дополнительные сведения см. в разделе [Navigate hello связанных ресурсов](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).

### <a id="storageexplorer"></a>Azure Storage Explorer;
*Azure Storage Explorer* — это эффективное средство для проверки и изменения данных hello в BLOB-объектов. Это бесплатный инструмент с открытым кодом. Его можно скачать на сайте [http://storageexplorer.com/](http://storageexplorer.com/). по этой ссылке, а также доступен Hello исходного кода.

Перед использованием средства hello, необходимо знать ключ учетной записи и имени учетной записи хранилища Azure. Инструкции о получении этих сведений в разделе hello» как: просмотр, копирование и повторное создание хранилища ключи доступа» раздел [Create, управления или удалить учетную запись хранения][azure-create-storage-account].

1. Запустите обозреватель хранилищ Azure. Если hello при первом запуске hello обозреватель хранилищ, появится для hello **имя учетной записи _Storage** и **ключ учетной записи хранения**. При запуске его, прежде чем использовать hello **добавить** tooadd новое имя учетной записи хранилища и ключ, нажмите кнопку.

    Введите hello имя и ключ для учетной записи хранилища hello, используемой кластером HDInsight, а затем выберите **ОТКРЫТЬ & Сохранить**.

    ![HDI.AzureStorageExplorer][image-azure-storage-explorer]
2. В списке слева toohello контейнеры интерфейса hello hello щелкните имя hello hello контейнера, которая связана с кластером HDInsight. По умолчанию это имя кластера HDInsight hello hello, но может отличаться, если вы ввели определенное имя при создании кластера hello.
3. Панель инструментов hello выберите значок передачи hello.

    ![Панель инструментов с выделенным значком отправки](./media/hdinsight-upload-data/toolbar.png)
4. Укажите tooupload файл и нажмите кнопку **откройте**. При появлении запроса выберите **отправить** tooupload hello файл toohello корневого контейнера хранилища hello. Если вы хотите tooupload hello tooa конкретных путь к файлу, введите путь hello в hello **назначения** поле, а затем выберите **отправить**.

    ![Диалоговое окно отправки файла](./media/hdinsight-upload-data/fileupload.png)

    После завершения передачи файла hello его можно использовать из заданий в кластере HDInsight hello.

## <a name="mount-azure-blob-storage-as-local-drive"></a>Подключение хранилища больших двоичных объектов как локального диска
Ознакомьтесь с разделом [Подключение хранилища больших двоичных объектов как локального диска](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).

## <a name="services"></a>Службы
### <a name="azure-data-factory"></a>Фабрика данных Azure
Hello служба фабрики данных Azure — это полностью управляемая служба для составления службы перемещения данных хранения, обработки данных и данных в рабочей среде конвейеры упрощенное, масштабируемые и надежные данные.

Фабрика данных Azure можно использовать toomove данных в хранилище больших двоичных объектов Azure, или toocreate конвейеры данных, которые непосредственно используют HDInsight функции например Hive и Pig.

Дополнительные сведения см. в разделе hello [документации фабрики данных Azure](https://azure.microsoft.com/documentation/services/data-factory/).

### <a id="sqoop"></a>Apache Sqoop
Sqoop данные средство, разработанное tootransfer между Hadoop и реляционных баз данных. Он используется tooimport данных из системы управления реляционной базы данных (RDBMS), такие как SQL Server, MySQL или Oracle в hello распределенная файловая система Hadoop (HDFS), преобразовывать данные hello в Hadoop MapReduce или Hive, а затем экспортируйте hello данные обратно в РЕЛЯЦИОННОЙ СУБД.

Дополнительные сведения см. в разделе [Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop].

## <a name="development-sdks"></a>Пакеты SDK для разработки
Хранилище больших двоичных объектов Azure можно получить с помощью пакета Azure SDK с hello следующих языков программирования:

* .NET
* Java
* Node.js
* PHP
* Python
* Ruby

Дополнительные сведения об установке hello Azure SDK см. в разделе [загрузки для Azure](https://azure.microsoft.com/downloads/)

## <a name="troubleshooting"></a>Устранение неполадок
### <a id="storageexception"></a>Исключение хранилища для записи в большой двоичный объект
**Проблема**: при использовании hello `hadoop` или `hdfs dfs` команды toowrite файлы, которые являются ~ 12 ГБ или больше для кластер HBase может возникнуть следующая ошибка hello:

    ERROR azure.NativeAzureFileSystem: Encountered Storage Exception for write on Blob : example/test_large_file.bin._COPYING_ Exception details: null Error Code : RequestBodyTooLarge
    copyFromLocal: java.io.IOException
            at com.microsoft.azure.storage.core.Utility.initIOException(Utility.java:661)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:366)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:350)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:471)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:745)
    Caused by: com.microsoft.azure.storage.StorageException: hello request body is too large and exceeds hello maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

**Причина**: HBase на HDInsight кластеры размер блока по умолчанию tooa 256 КБ, при написании tooAzure хранилища. Хотя этот способ подходит для API-интерфейсов HBase или интерфейсы API REST, он приведет к ошибке при использовании hello `hadoop` или `hdfs dfs` служебные программы командной строки.

**Разрешение**: использование `fs.azure.write.request.size` toospecify больший размер блока. С помощью hello это можно сделать на основе на использование `-D` параметра. Hello ниже приведен пример использования этого параметра с hello `hadoop` команды:

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

Можно также увеличить значение hello `fs.azure.write.request.size` глобально с помощью Ambari. Hello следующие шаги может быть использовано значение toochange hello в hello Ambari веб-интерфейса:

1. В браузере перейдите toohello Ambari веб-интерфейса для кластера. Это https://CLUSTERNAME.azurehdinsight.net, где **CLUSTERNAME** — hello имя кластера.

    При появлении запроса введите имя администратора hello и пароль для hello кластера.
2. Hello слева от оператора экран приветствия, выберите **HDFS**, а затем выберите hello **конфигураций** вкладки.
3. В hello **фильтра...**  введите `fs.azure.write.request.size`. При этом отобразится поле hello и текущее значение в середине hello страницы приветствия.
4. Измените значение hello с новым значением toohello 262144 (256 КБ). Например, 4194304 (4 МБ).

![Изображение изменения значения hello в пользовательском Интерфейсе Ambari Web](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

Дополнительные сведения об использовании Ambari см. в разделе [управление кластерами HDInsight с помощью Ambari веб-интерфейса hello](hdinsight-hadoop-manage-ambari.md).

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы знаете как считывать данные tooget в HDInsight, hello как следующие статьи toolearn tooperform анализа:

* [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]
* [Отправка заданий Hadoop в HDInsight][hdinsight-submit-jobs]
* [Использование Hive с HDInsight][hdinsight-use-hive]
* [Использование Pig с HDInsight][hdinsight-use-pig]

[azure-management-portal]: https://porta.azure.com
[azure-powershell]: http://msdn.microsoft.com/library/windowsazure/jj152841.aspx

[azure-storage-client-library]: /develop/net/how-to-guides/blob-storage/
[azure-create-storage-account]:../storage/common/storage-create-storage-account.md
[azure-azcopy-download]:../storage/common/storage-use-azcopy.md
[azure-azcopy]:../storage/common/storage-use-azcopy.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md

[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[sqldatabase-create-configure]: ../sql-database-create-configure.md

[apache-sqoop-guide]: http://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[azurecli]: ../cli-install-nodejs.md


[image-azure-storage-explorer]: ./media/hdinsight-upload-data/HDI.AzureStorageExplorer.png
[image-ase-addaccount]: ./media/hdinsight-upload-data/HDI.ASEAddAccount.png
[image-ase-blob]: ./media/hdinsight-upload-data/HDI.ASEBlob.png
