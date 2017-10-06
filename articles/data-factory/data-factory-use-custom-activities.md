---
title: "aaaUse настраиваемых действий в конвейере фабрики данных Azure"
description: "Узнайте, как toocreate настраиваемые действия и использовать их из конвейера фабрики данных Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 23e33727b2160541ab40938ffd911fdd484b3daa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a>Использование настраиваемых действий в конвейере фабрики данных Azure

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Действие Hive](data-factory-hive-activity.md) 
> * [Действие Pig](data-factory-pig-activity.md)
> * [Действие MapReduce](data-factory-map-reduce.md)
> * [Потоковая активность Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Действие Spark](data-factory-spark.md)
> * [Действие выполнения пакета машинного обучения](data-factory-azure-ml-batch-execution-activity.md)
> * [Действие "Обновить ресурс" в службе машинного обучения](data-factory-azure-ml-update-resource-activity.md)
> * [Действие хранимой процедуры](data-factory-stored-proc-activity.md)
> * [Действие U-SQL в Data Lake Analytics](data-factory-usql-activity.md)
> * [Настраиваемое действие .NET](data-factory-use-custom-activities.md)

Существует два типа действий, которые можно использовать в конвейере фабрики данных Azure.

- [Действия перемещения данных](data-factory-data-movement-activities.md) toomove данных между [поддерживается хранилищ данных источника и приемника](data-factory-data-movement-activities.md#supported-data-stores-and-formats).
- [Действия преобразования данных](data-factory-data-transformation-activities.md) tootransform данных с помощью службы Azure HDInsight, пакетной службы Azure и машинного обучения Azure вычислений. 

toomove данные из хранилища данных, который не поддерживает фабрики данных, создайте **пользовательское действие** собственные перемещение логики и использование hello действием данных в конвейере. Аналогичным образом tootransform и обработки данных в виде, не поддерживается службой фабрики данных, создать пользовательское действие с свою собственную логику для преобразования данных и использования hello действия в конвейере. 

Можно настроить toorun настраиваемого действия на **пакетной службы Azure** пула виртуальных машин или на основе Windows **Azure HDInsight** кластера. При использовании пакетной службы Azure можно использовать только имеющийся пул пакетной службы Azure. А при использовании HDInsight можно применить имеющийся кластер HDInsight или кластер, который автоматически создается для вас по запросу в среде выполнения.  

Hello следующее пошаговое руководство содержит пошаговые инструкции по созданию настраиваемого действия .NET и использованию пользовательское действие hello в конвейере. пошаговом руководстве Hello **пакетной службы Azure** связанной службы. toouse Azure HDInsight вместо связанной службы, создания связанной службы типа **HDInsight** (собственный кластер HDInsight) или **HDInsightOnDemand** (фабрики данных создает кластер HDInsight по запросу). Затем настройте toouse пользовательское действие hello связанной службы HDInsight. В разделе [HDInsight Azure используйте связанные службы](#use-hdinsight-compute-service) разделе подробные сведения о работе Azure HDInsight toorun hello пользовательского действия.

> [!IMPORTANT]
> - пользовательские действия .NET Hello выполняются только на кластеры HDInsight под управлением Windows. Обойти это ограничение — toouse hello кода toorun пользовательские действия уменьшить карты Java в кластере HDInsight под управлением Linux. Другой вариант — toouse пула виртуальных машин toorun настраиваемые действия вместо использования кластера HDInsight.
> - Это не возможные toouse шлюз управления данными из источников данных в локальной tooaccess настраиваемого действия. В настоящее время [шлюз управления данными](data-factory-data-management-gateway.md) поддерживает только действие копирования hello и действие хранимой процедуры в фабрике данных.   

## <a name="walkthrough-create-a-custom-activity"></a>Пошаговое руководство по созданию настраиваемого действия
### <a name="prerequisites"></a>Предварительные требования
* Visual Studio 2012/2013/2015
* Скачайте и установите пакет [Azure .NET SDK](https://azure.microsoft.com/downloads/)

### <a name="azure-batch-prerequisites"></a>Предварительные требования для пакетной службы Azure
В пошаговом руководстве hello выполнения настраиваемых действий .NET с помощью пакетной службы Azure как вычислительные ресурсы. **Пакет Azure** — это платформа службы для выполнения крупномасштабных параллельных и высокопроизводительных вычислительных (систем HPC) приложения эффективно работает в облаке hello. Пакет Azure планирует интенсивных вычислительных рабочих toorun управляемого **коллекции виртуальных машин**, и может автоматически масштабирование вычислительных потребностей hello toomeet ресурсы заданий. В разделе [основы пакетной службы Azure] [ batch-technical-overview] статье подробный обзор hello пакетной службы Azure.

В учебнике hello создайте учетную запись пакетной службы Azure с помощью пула виртуальных машин. Ниже приведены шаги hello.

1. Создание **учетной записи пакетной службы** с помощью hello [портал Azure](http://portal.azure.com). Инструкции см. в статье [Создание учетной записи пакетной службы Azure на портале Azure][batch-create-account].
2. Запишите имя учетной записи пакетной службы Azure hello, ключ учетной записи, URI и имя пула. При необходимости toocreate связанной пакетной службы Azure.
    1. На домашней странице приветствия для учетной записи пакетной службы Azure, вы видите **URL-адрес** в hello следующий формат: `https://myaccount.westus.batch.azure.com`. В этом примере **myaccount** — имя учетной записи пакетной службы Azure hello hello. URI, используемого в определении службы hello связаны — hello URL-адрес без имени hello hello учетной записи. Например, `https://<region>.batch.azure.com`.
    2. Нажмите кнопку **ключей** hello левого меню, а также копировать hello **первичный ключ доступа**.
    3. toouse существующий пул, нажмите кнопку **пулы** в меню "hello" и запишите hello **идентификатор** hello пула. Если у вас нет существующего пула, переместите toohello следующий шаг.     
2. Создайте **пул пакетной службы Azure**.

   1. В hello [портал Azure](https://portal.azure.com), нажмите кнопку **Обзор** в hello в левом меню и нажмите кнопку **учетные записи пакетного**.
   2. Выберите ваш hello tooopen учетной записи пакетной службы Azure **пакетной учетной записи** колонку.
   3. Щелкните элемент **Пулы** .
   4. В hello **пулы** колонке нажмите кнопку Добавить на панель инструментов hello tooadd пул.
      1. Введите идентификатор пула hello (идентификатор пула). Примечание hello **идентификатор пула hello**; необходимо при создании решения hello фабрики данных.
      2. Укажите **Windows Server 2012 R2** для приветствия семейство операционных систем.
      3. Выберите **Ценовая категория для узлов**.
      4. Введите **2** как значение для hello **выделенной целевой** параметр.
      5. Введите **2** как значение для hello **Max задач на каждом узле** параметр.
   5. Нажмите кнопку **ОК** toocreate hello пула.
   6. Запишите hello **идентификатор** hello пула. 



### <a name="high-level-steps"></a>Пошаговые действия
Ниже приведены два hello высокоуровневые действия, выполняемых в рамках этого пошагового руководства. 

1. Создайте пользовательское действие, содержащее простую логику преобразования и обработки данных.
2. Создайте фабрику данных Azure с конвейером, который использует пользовательское действие hello.

### <a name="create-a-custom-activity"></a>Создать настраиваемое действие.
Создание toocreate .NET пользовательское действие, **библиотеки классов .NET** проекта с классом, который реализует **IDotNetActivity** интерфейса. У этого интерфейса есть только один метод [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) , и его сигнатура такова.

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


метод Hello принимает четыре параметра:

- **linkedServices** — Это свойство является Перечислимый список служб хранилища данных связанной ссылается наборы данных ввода вывода для действия "hello".   
- **наборы данных**. Это свойство является Перечислимый список наборов данных ввода вывода для действия "hello". Можно использовать этот параметр tooget hello расположения и схем, определенных путем наборов входных и выходных данных.
- **activity** — Это свойство представляет текущее действие hello. Его можно использовать tooaccess расширенные свойства, связанные с пользовательское действие hello. Дополнительные сведения см. в разделе [Доступ к расширенным свойствам](#access-extended-properties).
- **logger** — Этот объект позволяет писать комментарии отладки этой рабочей области в hello входа пользователя для hello конвейера.

метод Hello возвращает словарь, который может быть настраиваемых действий используется toochain друг с другом в будущем hello. Эта функция еще не реализован, чтобы возвращаемые пустой словарь из метода hello.  

### <a name="procedure"></a>Описание процедуры
1. Создайте проект **библиотеки классов .NET** .
   <ol type="a">
     <li>Запустите <b>Visual Studio 2017</b>, <b>Visual Studio 2015</b>, <b>Visual Studio 2013</b> или <b>Visual Studio 2012</b>.</li>
     <li>Нажмите кнопку <b>файл</b>, слишком точки<b>New</b>и нажмите кнопку <b>проекта</b>.</li>
     <li>Разверните раздел <b>Шаблоны</b> и выберите <b>Visual C#</b>. В этом пошаговом руководстве вы используете C#, но можно использовать любой .NET языка toodevelop hello пользовательского действия.</li>
     <li>Выберите <b>библиотеки классов</b> hello списке типов проекта на hello вправо. В VS 2017 выберите <b>Библиотека классов (.NET Framework)</b> .</li>
     <li>Введите <b>MyDotNetActivity</b> для hello <b>имя</b>.</li>
     <li>Выберите <b>C:\ADFGetStarted</b> для hello <b>расположение</b>.</li>
     <li>Нажмите кнопку <b>ОК</b> toocreate hello проекта.</li>
   </ol>
2.Нажмите кнопку **средства**, слишком точки**диспетчера пакетов NuGet**и нажмите кнопку **консоль диспетчера пакетов**.
3. В hello консоль диспетчера пакетов, выполните следующие команды tooimport hello **Microsoft.Azure.Management.DataFactories**.

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. Импорт hello **хранилища Azure** пакета NuGet в проекте toohello.

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > Запуск службы фабрики данных требуется версия hello 4.3 WindowsAzure.Storage. При добавлении tooa ссылка более позднюю версию сборки хранилища Azure в проект пользовательского действия, появится сообщение об ошибке при выполнении действия hello. Ошибка tooresolve hello, в разделе [изоляции домена приложения](#appdomain-isolation) раздела. 
5. Добавьте следующее hello **с помощью** инструкций toohello исходного файла в проекте hello.

    ```csharp

    // Comment these lines if using VS 2017
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    // --------------------

    // Comment these lines if using <= VS 2015
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    // ---------------------

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. Изменение имени hello объекта hello **имен** слишком**MyDotNetActivityNS**.

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. Изменить имя hello класса hello слишком**MyDotNetActivity** и производными hello **IDotNetActivity** интерфейс, как показано в hello, следующий фрагмент кода:

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. Реализуйте (Добавить) hello **Execute** метод hello **IDotNetActivity** интерфейс toohello **MyDotNetActivity** hello класса и скопируйте следующий образец кода toohello метода.

    Hello следующий пример считает hello число вхождений hello условие поиска («Microsoft») в каждый BLOB-объект, связанный с срез данных.

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
    /// </summary>
    
    public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
    {
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // toolog information, use hello logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get hello input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables toohold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from hello dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and hello other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get hello first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using hello same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get hello connection string in hello linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get hello folder path from hello input dataset definition
        string folderPath = GetFolderPath(inputDataset);
        string output = string.Empty; // for use later.
    
        // create storage client for input. Pass hello connection string.
        CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
        CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
        // initialize hello continuation token before using it in hello do-while loop.
        BlobContinuationToken continuationToken = null;
        do
        {   // get hello list of input blobs from hello input storage client object.
            BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                     true,
                                     BlobListingDetails.Metadata,
                                     null,
                                     continuationToken,
                                     null,
                                     null);
    
            // Calculate method returns hello number of occurrences of
            // hello search term (“Microsoft”) in each blob associated
               // with hello data slice. definition of hello method is shown in hello next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for hello output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get hello folder path from hello output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log hello output folder path 
        logger.Write("Writing blob toohello folder: {0}", folderPath);
    
        // create a storage object for hello output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write hello name of hello file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log hello output file name
        logger.Write("output blob URI: {0}", outputBlobUri.ToString());

        // create a blob and upload hello output text.
        CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
        logger.Write("Writing {0} toohello output blob", output);
        outputBlob.UploadText(output);
    
        // hello dictionary can be used toochain custom activities together in hello future.
        // This feature is not implemented yet, so just return an empty dictionary.  
    
        return new Dictionary<string, string>();
    }
    ```
9. Добавьте следующие вспомогательные методы hello: 

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    
    private static string GetFolderPath(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }

        // get type properties of hello dataset 
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello folder path found in hello type properties
        return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.   
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }
    
        // get type properties of hello dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello blob/file name in hello type properties
        return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
        string output = string.Empty;
        logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
        foreach (IListBlobItem listBlobItem in Bresult.Results)
        {
            CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
            if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
            {
                string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
                logger.Write("input blob text: {0}", blobText);
                string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
                var matchQuery = from word in source
                                 where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                 select word;
                int wordCount = matchQuery.Count();
                output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
            }
        }
        return output;
    }
    ```

    Hello GetFolderPath метод возвращает hello путь toohello папки, hello набор данных указывает tooand hello GetFileName метод возвращает hello имя hello большого двоичного объекта или файла, hello указывает набор данных. Если вы havefolderPath определяет использование переменных, например {Year}, {Month} возвращает {Day} и т.д., метод hello hello строку как есть и без их замены на значений времени выполнения. Дополнительные сведения о доступе к SliceStart, SliceEnd и т. д. см. в разделе [Доступ к расширенным свойствам](#access-extended-properties).    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    метод Calculate Hello вычисляет hello число экземпляров ключевое слово Microsoft во входных файлах hello (большие двоичные объекты в папке hello). условие поиска Hello («Microsoft») жестко закодирована в коде hello.
10. Скомпилируйте проект hello. Нажмите кнопку **построения** из hello меню и выберите пункт **построить решение**.

    > [!IMPORTANT]
    > Набор 4.5.2 версии .NET Framework в качестве hello целевой платформы для проекта: щелкните правой кнопкой мыши проект hello и нажмите кнопку **свойства** tooset hello требуемой версии .NET framework. Фабрика данных не поддерживает настраиваемые действия, скомпилированные для более поздних версий, чем .NET Framework 4.5.2.

11. Запустите **Проводник**и перейдите в слишком**bin\debug** или **bin\release** папку, в зависимости от типа hello сборки.
12. Создать ZIP-файл **MyDotNetActivity.zip** , содержащий все двоичные файлы hello в hello <project folder>папку \bin\Debug. Включить hello **MyDotNetActivity.pdb** так, чтобы получить дополнительные сведения, такие как номер строки в исходном коде hello, вызвавшего проблему hello, если произошел сбой. 

    > [!IMPORTANT]
    > Все файлы в ZIP-файле hello hello, пользовательское действие hello должен быть в hello **верхнего уровня** с нет вложенных папок.

    ![Двоичные выходные файлы](./media/data-factory-use-custom-activities/Binaries.png)
14. Создайте контейнер больших двоичных объектов **customactivitycontainer**, если он еще не создан. 
15. Загрузите MyDotNetActivity.zip как customactivitycontainer toohello большого двоичного объекта в **общего назначения** хранилище больших двоичных объектов (хранилище больших двоичных объектов не горячей/стильной), который ссылается AzureStorageLinkedService.  

> [!IMPORTANT]
> Если добавить этот проект tooa .NET действия решение в Visual Studio, которое содержит проект фабрики данных и добавьте проект действия too.NET ссылку из проекта приложения hello фабрики данных, не обязательно tooperform hello последних двух этапов создания вручную Hello ZIP-файл и передать его в хранилище toohello общего назначения больших двоичных объектов. При публикации сущностей фабрики данных, с помощью Visual Studio следующие действия в процессе публикации hello происходит автоматически. Дополнительные сведения см. в разделе [Проект фабрики данных в Visual Studio](#data-factory-project-in-visual-studio).

## <a name="create-a-pipeline-with-custom-activity"></a>Создание конвейера с настраиваемым действием
После создания пользовательского действия и отправить hello ZIP-файл с контейнер больших двоичных объектов tooa двоичные файлы в **общего назначения** учетной записи хранилища Azure. В этом разделе создается фабрикой данных Azure с конвейером, который использует пользовательское действие hello.

Hello входного набора данных для пользовательского действия hello представляет большие двоичные объекты (файлы) в папке customactivityinput hello adftutorial контейнера в хранилище больших двоичных объектов hello. Hello выходной набор данных для действия "hello" представляет выходные данные больших двоичных объектов в папке customactivityoutput hello adftutorial контейнера в хранилище больших двоичных объектов hello.

Создание **файла file.txt** файл с hello следующие содержимого и передать его слишком**customactivityinput** папки hello **adftutorial** контейнера. Создание контейнера adftutorial hello, если он еще не существует. 

```
test custom activity Microsoft test custom activity Microsoft
```

Папка входных данных Hello соответствует tooa среза в фабрике данных Azure, даже если папка hello имеет два или более файлов. При обработке каждого среза конвейером hello пользовательское действие hello выполняет итерацию всех больших двоичных объектов hello в hello папка входных данных для этого среза.

Вы увидите, что один выходной файл в папке adftutorial\customactivityoutput hello с одной или нескольких строк (то же, как количество больших двоичных объектов в папке входной hello):

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
```


Ниже приведены шаги hello, выполняемых в этом разделе.

1. Создание **фабрики данных**.
2. Создание **связанные службы** для hello пула виртуальных машин, на какие hello настраиваемое действие выполняется, а hello хранилища Azure, содержащий hello большие двоичные объекты ввода вывода.
3. Создать входной и выходной **наборы данных** , представляющие вход и выход пользовательское действие hello.
4. Создание **конвейера** , использующий настраиваемое действие hello.

> [!NOTE]
> Создать hello **файла file.txt** и отправьте его tooa контейнер больших двоичных объектов, если это еще не сделано. См. инструкции в предшествующих раздел hello.   

### <a name="step-1-create-hello-data-factory"></a>Шаг 1: Создание фабрики данных hello
1. После входа в систему toohello портал Azure, hello следующие шаги:
   1. Нажмите кнопку **NEW** hello левом меню.
   2. Нажмите кнопку **данные + аналитика** в hello **New** колонку.
   3. Нажмите кнопку **фабрики данных** на hello **анализа данных** колонку.
   
    ![Меню создания фабрики данных Azure](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. В hello **новую фабрику данных** колонке введите **CustomActivityFactory** для hello имя. Имя фабрики данных Azure hello Hello должно быть глобально уникальным. При получении ошибки hello: **имя фабрики данных «CustomActivityFactory» недоступен**, измените имя hello hello фабрики данных (например, **yournameCustomActivityFactory**) и попробуйте создать еще раз.

    ![Колонка создания фабрики данных Azure](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. Щелкните **Имя группы ресурсов**, чтобы выбрать имеющуюся группу ресурсов, или создайте группу ресурсов.
4. Убедитесь, что вы используете правильный hello **подписки** и **область** место hello данных фабрики toobe создан.
5. Нажмите кнопку **создать** на hello **новую фабрику данных** колонку.
6. Вы видите hello фабрики данных, создаваемого в hello **мониторинга** из hello портал Azure.
7. После успешного создания фабрики данных hello, вы видите колонке hello фабрики данных, в котором отображается содержимое фабрики данных hello hello.
    
    ![Колонка "Фабрика данных"](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a>Шаг 2. Создание связанных служб
Связанные службы связывание хранилищ данных или фабрики данных Azure tooan службы вычислений. На этом шаге связать учетную запись хранилища Azure и фабрики данных tooyour учетной записи пакетной службы Azure.

#### <a name="create-azure-storage-linked-service"></a>Создание связанной службы хранения Azure
1. Щелкните hello **автор и развернуть** плитки приветствия **ФАБРИКИ данных** колонке **CustomActivityFactory**. Вы увидите hello редактор фабрики данных.
2. Нажмите кнопку **новое хранилище данных** hello панели команд и выберите **хранилища Azure**. Вы увидите hello скрипта JSON для создания хранилища Azure связанная служба в редакторе hello.
    
    !["Новое хранилище данных" — "Служба хранилища Azure"](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. Замените `<accountname>` с именем вашей учетной записи хранилища Azure и `<accountkey>` с ключом доступа hello учетной записи хранилища Azure. toolearn tooget хранилищем доступом ключа, см. в разделе [ключи доступа Просмотр, копирование и повторное создание хранилища](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

    ![Связанная служба хранилища Azure](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. Нажмите кнопку **развернуть** на панели toodeploy hello связаны службы hello команд.

#### <a name="create-azure-batch-linked-service"></a>Создание связанной пакетной службы Azure
1. В hello редактор фабрики данных, нажмите кнопку **... Дополнительные** на панели команд hello, нажмите кнопку **новые вычислительные**, а затем выберите **пакетной службы Azure** меню "hello".

    !["Новое вычисление" — "Пакет Azure"](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. Внести следующие изменения скрипта JSON toohello hello:

   1. Укажите имя учетной записи пакетной службы Azure для hello **accountName** свойство. Hello **URL-адрес** из hello **колонке учетной записи пакетной службы Azure** в hello следующий формат: `http://accountname.region.batch.azure.com`. Для hello **batchUri** свойство в hello JSON, вы должны tooremove `accountname.` из URL-адрес и используйте hello hello `accountname` для hello `accountName` свойства JSON.
   2. Укажите ключ учетной записи пакетной службы Azure hello для hello **accessKey** свойство.
   3. Укажите имя hello hello пула, созданного в рамках предварительных требований для hello **poolName** свойство. Можно также указать идентификатор hello пула hello вместо имени hello hello пула.
   4. Укажите URI пакета Azure для hello **batchUri** свойство. Пример: `https://westus.batch.azure.com`.  
   5. Укажите hello **AzureStorageLinkedService** для hello **linkedServiceName** свойство.

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       Для hello **poolName** свойства, можно также указать идентификатор hello пула hello вместо имени hello hello пула.

      > [!IMPORTANT]
      > Hello служба фабрики данных не поддерживает параметр по требованию для пакетной службы Azure, как для HDInsight. Пул пакетной службы Azure можно использовать только в фабрике данных Azure.   
    

### <a name="step-3-create-datasets"></a>Шаг 3. Создание наборов данных
На этом шаге создания наборов данных toorepresent входных и выходных данных.

#### <a name="create-input-dataset"></a>Создание входного набора данных
1. В hello **редактор** hello фабрики данных, щелкните **... Дополнительные** на панели команд hello, нажмите кнопку **новый набор данных**, а затем выберите **хранилища больших двоичных объектов Azure** hello раскрывающегося меню.
2. Замените hello JSON в правой области hello hello, следующий фрагмент JSON:

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
         },
         "availability": {
             "frequency": "Hour",
             "interval": 1
         },
         "external": true,
         "policy": {}
     }
    }
    ```

   Позже в этом пошаговом руководстве вы создадите конвейер со временем начала 2016-11-16T00:00:00Z и временем окончания 2016-11-16T05:00:00Z. Запланированные tooproduce данных — час, поэтому существуют пять фрагменты ввода вывода (между **00**: -> 00:00 **05**: 00:00).

   Hello **частоты** и **интервал** для hello входного набора данных задается слишком**час** и **1**, что означает, что hello ввода фрагмент доступен Каждый час. В этом примере это hello же файла (файла file.txt) в hello intputfolder.

   Ниже приведены hello временем начала для каждого среза, представленного SliceStart системной переменной в hello выше фрагменте кода JSON.
3. Нажмите кнопку **развернуть** hello toocreate инструментов и развернуть hello **InputDataset**. Подтвердите, что вы видите hello **таблица СОЗДАНА успешно** сообщение hello заголовке hello редактора.

#### <a name="create-an-output-dataset"></a>Создание выходного набора данных
1. В hello **редактор фабрики данных**, нажмите кнопку **... Дополнительные** на панели команд hello, нажмите кнопку **новый набор данных**, а затем выберите **хранилища больших двоичных объектов Azure**.
2. Замените скрипт JSON hello в правой области hello hello следующий скрипт JSON:

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
                "partitionedBy": [
                    {
                        "name": "slice",
                        "value": {
                            "type": "DateTime",
                            "date": "SliceStart",
                            "format": "yyyy-MM-dd-HH"
                        }
                    }
                ]
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

     Расположение выходных данных — **adftutorial/customactivityoutput/** и имя выходного файла гггг мм дд HH.txt, где гггг мм дд чч — hello года, месяца, даты и часа hello среза, созданных. Подробную информацию см. в [справочнике разработчика фабрики данных Azure][adf-developer-reference].

    Для каждого входного среза данных создается выходной большой двоичный объект или файл. Ниже в таблице приведены имена, которые даются выходным файлам для каждого среза. Все hello выходные файлы создаются в одной папке выходных данных: **adftutorial\customactivityoutput**.

   | Срез | Время начала | Выходной файл |
   |:--- |:--- |:--- |
   | 1 |2016-11-16T00:00:00 |2016-11-16-00.txt |
   | 2 |2016-11-16T01:00:00 |2016-11-16-01.txt |
   | 3 |2016-11-16T02:00:00 |2016-11-16-02.txt |
   | 4 |2016-11-16T03:00:00 |2016-11-16-03.txt |
   | 5 |2016-11-16T04:00:00 |2016-11-16-04.txt |

    Помните, что все файлы hello в папке ввода являются частью фрагмента с временем начала hello, упомянутых выше. При обработке этого среза пользовательское действие hello просматривает каждый файл и создает строку в выходной файл hello с hello число вхождений условие поиска («Microsoft»). Имеется три файла в hello inputfolder, есть три строки в hello выходной файл для каждого среза почасовой: 2016-11-16-00.txt 2016-11-16:01:00:00.txt, и т. д.
3. toodeploy hello **OutputDataset**, нажмите кнопку **развернуть** на панели команд hello.

### <a name="create-and-run-a-pipeline-that-uses-hello-custom-activity"></a>Создание и выполнение конвейера, который использует пользовательское действие hello
1. В hello редактор фабрики данных, нажмите кнопку **... Дополнительные**, а затем выберите **новый конвейер** на панели команд hello. 
2. Замените hello JSON в правой области hello hello следующий скрипт JSON:

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    Обратите внимание hello после точки.

   * **Параллелизм** задано слишком**2** , чтобы два фрагменты обрабатываются параллельно, 2 виртуальные машины в пуле пакетной службы Azure hello.
   * Имеется одно действие в разделе действий hello и имеет тип: **DotNetActivity**.
   * **AssemblyName** задано имя toohello hello DLL: **MyDotnetActivity.dll**.
   * **EntryPoint** задано слишком**MyDotNetActivityNS.MyDotNetActivity**.
   * **PackageLinkedService** задано слишком**AzureStorageLinkedService** , который указывает хранилище больших двоичных объектов toohello, содержащий ZIP-файл пользовательское действие hello. При использовании различных учетных записей хранилища Azure для ввода вывода файлов и hello ZIP-файл пользовательских действий, можно создать другой связанной службой хранилища Azure. В этой статье предполагается, что вы используете hello учетную запись хранилища Azure.
   * **PackageFile** задано слишком**customactivitycontainer/MyDotNetActivity.zip**. Он имеет формат hello: containerforthezip/nameofthezip.zip.
   * пользовательское действие Hello принимает **InputDataset** в качестве входного и **OutputDataset** в качестве выходных данных.
   * Свойство linkedServiceName Hello пользовательское действие hello указывает toohello **AzureBatchLinkedService**, который сообщает фабрики данных Azure, пользовательское действие hello должен toorun на виртуальных машинах Azure пакета.
   * **isPaused** задано слишком**false** по умолчанию. конвейер Hello немедленно выполняется в этом примере, поскольку запуска среза hello в прошлом hello. Можно задать это свойство tootrue toopause hello конвейера и задайте для него toorestart toofalse назад.
   * Hello **запустить** время и **окончания** время **пять** часы друг от друга и фрагменты создаются каждый час, поэтому пять фрагменты, созданные с помощью конвейера hello.
3. toodeploy hello конвейера, нажмите кнопку **развернуть** на панели команд hello.

### <a name="monitor-hello-pipeline"></a>Монитор hello конвейера
1. В колонке фабрики данных hello в hello портала Azure щелкните **схема**.

    ![Плитка "Схема"](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. В hello представление диаграммы щелкните hello OutputDataset.

    ![Представление схемы](./media/data-factory-use-custom-activities/diagram.png)
3. Вы увидите, что hello пять срезы выходных данных находятся в состоянии готовности hello. Если они не находятся в состоянии готовности hello, они еще не были созданы еще. 

   ![Выходные срезы](./media/data-factory-use-custom-activities/OutputSlices.png)
4. Убедитесь, что hello выходные файлы создаются в хранилище больших двоичных объектов hello в hello **adftutorial** контейнера.

   ![выходные данные настраиваемого действия][image-data-factory-ouput-from-custom-activity]
5. При открытии hello выходной файл, вы увидите hello выходной аналогичные toohello следующие выходные данные:

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
    ```
6. Используйте hello [портал Azure] [ azure-preview-portal] или toomonitor командлеты Azure PowerShell вашей фабрики данных, конвейеры и наборов данных. Можно видеть сообщения от hello **ActivityLogger** в коде hello пользовательское действие hello в журналах hello (в частности пользователя 0.log), которые можно загрузить с портала hello или с помощью командлетов.

   ![скачивание журналов из настраиваемого действия][image-data-factory-download-logs-from-custom-activity]

Подробные указания по мониторингу наборов данных и конвейеров см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими](data-factory-monitor-manage-pipelines.md).      

## <a name="data-factory-project-in-visual-studio"></a>Проект фабрики данных в Visual Studio  
Можно создать и опубликовать сущности фабрики данных, используя Visual Studio вместо портала Azure. Подробные сведения о создании и публикации сущностей фабрики данных с помощью Visual Studio, в разделе [построение первой конвейер с помощью Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) и [копирования данных из больших двоичных объектов Azure tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) статьи.

Здравствуйте, следующие дополнительные шаги при создании фабрики данных проекта в Visual Studio:
 
1. Добавьте hello фабрики данных проекта toohello Visual Studio решение, содержащее проект пользовательского действия hello. 
2. Добавьте проект действия .NET toohello ссылку из проекта hello фабрики данных. Щелкните правой кнопкой мыши проект фабрики данных, укажите слишком**добавить**и нажмите кнопку **ссылка**. 
3. В hello **добавить ссылку** диалоговое окно, выберите hello **MyDotNetActivity** проекта, а затем нажмите кнопку **ОК**.
4. Построение и публикация решения hello.

    > [!IMPORTANT]
    > При публикации сущностей фабрики данных, в ZIP-файл автоматически создается и — контейнер больших двоичных объектов отправленного toohello: customactivitycontainer. Если контейнер больших двоичных объектов hello не существует, она будет создана автоматически слишком.  


## <a name="data-factory-and-batch-integration"></a>Интеграция фабрики данных и пакетной службы
Служба фабрики данных Hello создает задание в пакетной службы Azure с именем hello: **adf poolname: задание xxx**. Нажмите кнопку **заданий** из меню слева hello. 

![Фабрика данных Azure — задания пакетной службы](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

Такое задание создается для каждого запуска действия среза. Если есть пять готов toobe фрагменты обработки, пять задачи создаются в рамках этого задания. Если существует несколько вычислительных узлов в hello пула, два или более фрагментов могут выполняться параллельно. Если вычислений hello максимальное число задач в набор узлов слишком > 1, вы также можете более одного фрагмента, работающих на hello же вычислений.

![Фабрика данных Azure — задачи задания пакетной службы](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

Привет, следующая схема иллюстрирует hello связь между задачами фабрики данных Azure и пакета.

![Фабрика данных и пакетная служба](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a>Устранение ошибок
Устранение неполадок состоит из нескольких базовых методов:

1. Если появится следующая ошибка hello, возможно, используется активная/стильной хранилища больших двоичных объектов вместо хранения общего назначения BLOB-объектов Azure. Отправка файла tooa hello zip **общего назначения учетной записи хранилища Azure**. 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of hello specified Azure Blob(s).
    ``` 
2. Если следующая ошибка hello, убедитесь, что hello имя класса hello в имя соответствует hello hello CS файла, указанное для hello **EntryPoint** свойство hello конвейера JSON. В пошаговом руководстве hello, является именем класса hello: MyDotNetActivity и hello точки входа в hello JSON: MyDotNetActivityNS. **MyDotNetActivity**.

    ```
    MyDotNetActivity assembly does not exist or doesn't implement hello type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   При совпадении имен hello, убедитесь, что все двоичные файлы hello в hello **корневую папку** hello ZIP-файла. То есть при открытии hello ZIP-файл, вы увидите все файлы hello в корневой папке hello, а не все вложенные папки.   
3. Если входной срез hello не задано слишком**готовности**, подтвердите правильность структуры hello папка входных данных и **файла file.txt** существует в папках входной hello.
3. В hello **Execute** метод настраиваемого действия, используйте hello **IActivityLogger** toolog сведения об объекте, которая позволяет выполнять устранение неполадок. Hello в журнал сообщения отображаются в файлах журнала пользователя hello (один или несколько файлов с именем: 0.log пользователя, пользователь 1.log, 2.log пользователя, и т. д.).

   В hello **OutputDataset** колонка, щелкните hello срез toosee hello **СРЕЗ данных** колонку для этого среза. Для этого среза будет указано значение **Запуски операции** . Должна появиться при выполнении среза hello одного действия. Если нажать кнопку запуска на панели команд hello, можно запустить другое действие запуска для hello того же фрагмента.

   При нажатии кнопки при выполнении действия hello, вы видите hello **сведения о выполнении действия** колонка со списком файлов журнала. Вы увидите сообщение регистрируется в файле user_0.log hello. При возникновении ошибки, так как число повторных попыток hello задано too3 hello конвейера или действия JSON см запуске три действия. При нажатии кнопки при выполнении действия hello, вы видите что tootroubleshoot hello ошибки можно просмотреть файлы журнала hello.

   В списке hello файлов журнала щелкните hello **0.log пользователя**. В правой панели hello являются hello результатов с помощью hello **IActivityLogger.Write** метод. Если вы не видите всех сообщений, проверьте наличие дополнительных файлов журнала user_1.log, user_2.log и т. д. В противном случае — код hello возможно произошел сбой после последнего hello в журнал сообщения.

   Кроме того, проверьте файл **system-0.log** на наличие любых системных сообщений об ошибках или исключений.
4. Включить hello **PDB** файлов в ZIP-файле hello таким образом, что сведения об ошибке hello сведения например **стека вызовов** при возникновении ошибки.
5. Все файлы в ZIP-файле hello hello, пользовательское действие hello должен быть в hello **верхнего уровня** с нет вложенных папок.
6. Убедитесь, что hello **assemblyName** (MyDotNetActivity.dll) **entryPoint**(MyDotNetActivityNS.MyDotNetActivity) **packageFile** (customactivitycontainer / MyDotNetActivity.zip) и **packageLinkedService** (должен указывать toohello **общего назначения**хранилище больших двоичных объектов, содержащий hello ZIP-файл) значения toocorrect.
7. Исправления ошибок и хотите hello срез tooreprocess щелкните правой кнопкой мыши срез hello в hello **OutputDataset** колонку и нажмите кнопку **запуска**.
8. Если появится следующая ошибка hello, вы используете пакет hello хранилища Azure версии > 4.3.0. Запуск службы фабрики данных требуется версия hello 4.3 WindowsAzure.Storage. В разделе [изоляции домена приложения](#appdomain-isolation) статьи для обхода, если необходимо использовать hello более позднюю версию сборки хранилища Azure. 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by hello target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    При использовании версии hello 4.3.0 пакета хранилища Azure удалите hello существующей ссылки tooAzure хранилища пакета версии > 4.3.0. Выполните следующую команду из консоли диспетчера пакетов NuGet hello. 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    Построение проекта hello. Удалите Azure.Storage сборки версии > 4.3.0 из папки bin\Debug hello. Создайте ZIP-файл с двоичные файлы и PDB-файл hello. Замените старый ZIP-файл hello в контейнер больших двоичных объектов hello (customactivitycontainer). Запустите hello срезы, сбой (щелкните правой кнопкой мыши срез и нажмите кнопку Выполнить).   
8. пользовательское действие Hello не использует hello **app.config** файл из пакета. Таким образом Если код считывает все строки подключения из файла конфигурации hello, он не работает во время выполнения. Здравствуйте, рекомендуется при использовании пакета Azure, toohold все секреты в **Azure KeyVault**, использовать службы на основе сертификата субъекта tooprotect hello **keyvault**и распространить сертификат hello tooAzure пула. Здравствуйте настраиваемых действий .NET, то можно получить доступ к секретные данные из hello KeyVault во время выполнения. Это решение является универсальным решением и масштабируется tooany тип секретного кода, а не только строку подключения.

   Отсутствует простой обходной путь (но не рекомендуется): можно создать **связанная служба Azure SQL** параметры строки соединения, создать набор данных, использует hello связанной службы и цепочки hello dataset в виде пустой входного набора данных toohello настраиваемых действий .NET. После этого можно доступа hello связаны строки подключения службы в коде пользовательское действие hello.  

## <a name="update-custom-activity"></a>Обновление пользовательского действия
При обновлении кода hello для пользовательское действие hello, сборки, а также отправить hello ZIP-файл, содержащий новое хранилище больших двоичных объектов toohello двоичных файлов.

## <a name="appdomain-isolation"></a>Изоляция домена приложения
. В разделе [Cross образец AppDomain](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) , которое показывает, как toocreate пользовательского действия, которое не является ограниченное tooassembly версии, используемые запуска фабрики данных hello (пример: WindowsAzure.Storage версии 4.3.0, Newtonsoft.Json v6.0.x, и т. д.).

## <a name="access-extended-properties"></a>Доступ к расширенным свойствам
Расширенные свойства можно объявить в действие hello JSON, как показано в следующих образец hello:

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


В примере hello имеется два расширенные свойства: **SliceStart** и **с именем DataFactoryName**. Hello SliceStart основано на hello SliceStart системной переменной. Список поддерживаемых системных переменных см. [в этом разделе](data-factory-functions-variables.md). Hello с именем DataFactoryName значение жестко tooCustomActivityFactory.

tooaccess эти расширенные свойства в hello **Execute** метод toohello аналогичные кода используйте следующий код:

```csharp
// tooget extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// toolog all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a>Автомасштабирование пакетной службы Azure
Можно также создать пул пакетной службы Azure с использованием функции **автомасштабирования** . Например можно создать пул пакет azure с 0 выделенных виртуальных машин и формулу автомасштабирования на основе количества hello ожидающих задач. 

Образец формулы Hello позволяет достичь следующих поведение hello: при создании пула hello, он начинается с 1 виртуальной Машины. Метрика $PendingTasks определяет hello число задач в запущена + active (в очереди) состояние.  Hello формула находит hello среднее число ожидающих задач в hello последние 180 секунд и соответствующим образом задает параметром TargetDedicated. Благодаря этому значение TargetDedicated никогда не превысит 25 виртуальных машин. Таким образом как отправлены новые задачи, пул автоматически увеличивается и как задачи завершаются, виртуальные машины становятся свободного один за другим и автоматическое масштабирование hello уменьшается этих виртуальных машин. startingNumberOfVMs и maxNumberofVMs могут быть скорректированное tooyour потребностей.

Формула автоматического масштабирования:

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

Дополнительные сведения см. в статье [Автоматическое масштабирование вычислительных узлов в пуле пакетной службы Azure](../batch/batch-automatic-scaling.md).

Если пул hello используется по умолчанию hello [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello пакетная служба может занять 15-30 минут tooprepare hello виртуальной Машины перед запуском пользовательское действие hello.  Если пул hello использует разные autoScaleEvaluationInterval, hello пакетная служба может получить autoScaleEvaluationInterval + 10 минут.

## <a name="use-hdinsight-compute-service"></a>Использование службы вычислений HDInsight
В пошаговом руководстве hello использовать пользовательское действие hello toorun пакетной службы Azure compute. Также можно использовать собственный кластер HDInsight под управлением Windows или использовать фабрику данных создайте по требованию кластера HDInsight под управлением Windows, и запуска в кластере HDInsight hello пользовательское действие hello. Здесь перечислены hello высокоуровневые действия для использования кластера HDInsight.

> [!IMPORTANT]
> пользовательские действия .NET Hello выполняются только на кластеры HDInsight под управлением Windows. Обойти это ограничение — toouse hello кода toorun пользовательские действия уменьшить карты Java в кластере HDInsight под управлением Linux. Другой вариант — toouse пула виртуальных машин toorun настраиваемые действия вместо использования кластера HDInsight.
 

1. Создайте связанную службу Azure HDInsight.   
2. Использование HDInsight связанная служба вместо **AzureBatchLinkedService** в hello конвейера JSON.

Если требуется, чтобы tootest его с помощью hello пошагового руководства, изменение **запустить** и **окончания** времени для конвейера hello, благодаря чему можно протестировать hello сценарий с hello службы Azure HDInsight.

#### <a name="create-azure-hdinsight-linked-service"></a>Создание связанной службы Azure HDInsight
Hello служба фабрики данных Azure поддерживает создание кластера по требованию и использовать его tooprocess ввода tooproduce выходных данных. Также можно использовать собственный кластер tooperform hello таким же. Когда вы используете кластер HDInsight по запросу, для каждого среза создается отдельный кластер. В то время как при использовании кластера HDInsight hello кластер готов tooprocess немедленно hello среза. Таким образом при использовании кластера по запросу, может отсутствовать hello выходных данных сразу, как при использовании собственных кластера.

> [!NOTE]
> Во время выполнения экземпляра действия .NET работает только на один рабочий узел в кластере HDInsight hello; он не может быть масштабированный toorun на нескольких узлах. Несколько экземпляров действия .NET могут выполняться параллельно на разных узлах кластера HDInsight hello.
>
>

##### <a name="toouse-an-on-demand-hdinsight-cluster"></a>toouse кластер HDInsight по требованию
1. В hello **портал Azure**, нажмите кнопку **автор и развернуть** на домашней странице hello фабрики данных.
2. В hello редактор фабрики данных, нажмите кнопку **новые вычислительные** из hello командной строке и выберите **кластер HDInsight по требованию** меню "hello".
3. Внести следующие изменения скрипта JSON toohello hello:

   1. Для hello **значение clusterSize** свойство, укажите размер кластера HDInsight hello hello.
   2. Для hello **timeToLive** свойство, укажите, как долго hello клиента может простаивать перед его удалением.
   3. Для hello **версии** свойство, укажите требуется toouse версии HDInsight hello. Если исключить это свойство используется последняя версия hello.  
   4. Для hello **linkedServiceName**, укажите **AzureStorageLinkedService**.

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```

    > [!IMPORTANT]
    > пользовательские действия .NET Hello выполняются только на кластеры HDInsight под управлением Windows. Обойти это ограничение — toouse hello кода toorun пользовательские действия уменьшить карты Java в кластере HDInsight под управлением Linux. Другой вариант — toouse пула виртуальных машин toorun настраиваемые действия вместо использования кластера HDInsight.

4. Нажмите кнопку **развернуть** на панели toodeploy hello связаны службы hello команд.

##### <a name="toouse-your-own-hdinsight-cluster"></a>toouse кластеру HDInsight:
1. В hello **портал Azure**, нажмите кнопку **автор и развернуть** на домашней странице hello фабрики данных.
2. В hello **редактор фабрики данных**, нажмите кнопку **новые вычислительные** из hello командной строке и выберите **кластера HDInsight** меню "hello".
3. Внести следующие изменения скрипта JSON toohello hello:

   1. Для hello **clusterUri** свойство, введите URL-адрес hello HDInsight. Например, https://<clustername>.azurehdinsight.net/     
   2. Для hello **UserName** свойство, введите имя пользователя hello, обладающего кластера HDInsight toohello доступа.
   3. Для hello **пароль** свойство, введите пароль hello hello пользователя.
   4. Для hello **LinkedServiceName** свойство, введите **AzureStorageLinkedService**.
4. Нажмите кнопку **развернуть** на панели toodeploy hello связаны службы hello команд.

Дополнительные сведения см. в статье [Связанные службы вычислений](data-factory-compute-linked-services.md).

В hello **конвейера JSON**, используйте HDInsight (по запросу или собственные) связанной службы:

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="create-a-custom-activity-by-using-net-sdk"></a>Создание пользовательского действия с помощью пакета SDK для .NET
В пошаговом руководстве hello в этой статье создать фабрику данных с конвейером, который использует пользовательское действие hello с помощью портала Azure hello. Привет, следующий код показывает, как toocreate hello фабрики данных, используя пакет SDK для .NET. Можно найти дополнительные сведения об использовании пакета SDK tooprogrammatically Конвейеры создаются в hello [создать конвейер с действием копирования с помощью интерфейса API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md) статьи. 

```csharp
using System;
using System.Configuration;
using System.Collections.ObjectModel;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.Azure;
using Microsoft.Azure.Management.DataFactories;
using Microsoft.Azure.Management.DataFactories.Models;
using Microsoft.Azure.Management.DataFactories.Common.Models;

using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Collections.Generic;

namespace DataFactoryAPITestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // create data factory management client

            // TODO: replace ADFTutorialResourceGroup with hello name of your resource group.
            string resourceGroupName = "ADFTutorialResourceGroup";

            // TODO: replace APITutorialFactory with a name that is globally unique. For example: APITutorialFactory04212017
            string dataFactoryName = "APITutorialFactory";

            TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
                ConfigurationManager.AppSettings["SubscriptionId"],
                GetAuthorizationHeader().Result);

            Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

            DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);

            Console.WriteLine("Creating a data factory");
            client.DataFactories.CreateOrUpdate(resourceGroupName,
                new DataFactoryCreateOrUpdateParameters()
                {
                    DataFactory = new DataFactory()
                    {
                        Name = dataFactoryName,
                        Location = "westus",
                        Properties = new DataFactoryProperties()
                    }
                }
            );

            // create a linked service for input data store: Azure Storage
            Console.WriteLine("Creating Azure Storage linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureStorageLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: Replace <accountname> and <accountkey> with name and key of your Azure Storage account.
                            new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>")
                        )
                    }
                }
            );

            // create a linked service for output data store: Azure SQL Database
            Console.WriteLine("Creating Azure Batch linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureBatchLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: replace <batchaccountname> and <yourbatchaccountkey> with name and key of your Azure Batch account
                            new AzureBatchLinkedService("<batchaccountname>", "https://westus.batch.azure.com", "<yourbatchaccountkey>", "myazurebatchpool", "AzureStorageLinkedService")
                        )
                    }
                }
            );

            // create input and output datasets
            Console.WriteLine("Creating input and output datasets");
            string Dataset_Source = "InputDataset";
            string Dataset_Destination = "OutputDataset";

            Console.WriteLine("Creating input dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Source,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FolderPath = "adftutorial/customactivityinput/",
                                Format = new TextFormat()
                            },
                            External = true,
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },

                            Policy = new Policy() { }
                        }
                    }
                });

            Console.WriteLine("Creating output dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Destination,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FileName = "{slice}.txt",
                                FolderPath = "adftutorial/customactivityoutput/",
                                PartitionedBy = new List<Partition>()
                                {
                                    new Partition()
                                    {
                                        Name = "slice",
                                        Value = new DateTimePartitionValue()
                                        {
                                            Date = "SliceStart",
                                            Format = "yyyy-MM-dd-HH"
                                        }
                                    }
                                }
                            },
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },
                        }
                    }
                });

            Console.WriteLine("Creating a custom activity pipeline");
            DateTime PipelineActivePeriodStartTime = new DateTime(2017, 3, 9, 0, 0, 0, 0, DateTimeKind.Utc);
            DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
            string PipelineName = "ADFTutorialPipelineCustom";

            client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new PipelineCreateOrUpdateParameters()
                {
                    Pipeline = new Pipeline()
                    {
                        Name = PipelineName,
                        Properties = new PipelineProperties()
                        {
                            Description = "Use custom activity",

                            // Initial value for pipeline's active period. With this, you won't need tooset slice status
                            Start = PipelineActivePeriodStartTime,
                            End = PipelineActivePeriodEndTime,
                            IsPaused = false,

                            Activities = new List<Activity>()
                            {
                                new Activity()
                                {
                                    Name = "MyDotNetActivity",
                                    Inputs = new List<ActivityInput>()
                                    {
                                        new ActivityInput() {
                                            Name = Dataset_Source
                                        }
                                    },
                                    Outputs = new List<ActivityOutput>()
                                    {
                                        new ActivityOutput()
                                        {
                                            Name = Dataset_Destination
                                        }
                                    },
                                    LinkedServiceName = "AzureBatchLinkedService",
                                    TypeProperties = new DotNetActivity()
                                    {
                                        AssemblyName = "MyDotNetActivity.dll",
                                        EntryPoint = "MyDotNetActivityNS.MyDotNetActivity",
                                        PackageLinkedService = "AzureStorageLinkedService",
                                        PackageFile = "customactivitycontainer/MyDotNetActivity.zip",
                                        ExtendedProperties = new Dictionary<string, string>()
                                        {
                                            { "SliceStart", "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"}
                                        }
                                    },
                                    Policy = new ActivityPolicy()
                                    {
                                        Concurrency = 2,
                                        ExecutionPriorityOrder = "OldestFirst",
                                        Retry = 3,
                                        Timeout = new TimeSpan(0,0,30,0),
                                        Delay = new TimeSpan()
                                    }
                                }
                            }
                        }
                    }
                });
        }

        public static async Task<string> GetAuthorizationHeader()
        {
            AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
            ClientCredential credential = new ClientCredential(
                ConfigurationManager.AppSettings["ApplicationId"],
                ConfigurationManager.AppSettings["Password"]);
            AuthenticationResult result = await context.AcquireTokenAsync(
                resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                clientCredential: credential);

            if (result != null)
                return result.AccessToken;

            throw new InvalidOperationException("Failed tooacquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a>Отладка настраиваемого действия в Visual Studio
Hello [фабрики данных Azure - локальной среде](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) пример на GitHub включает средство, которое позволяет вам toodebug пользовательские действия .NET в Visual Studio.  


## <a name="sample-custom-activities-on-github"></a>Примеры настраиваемых действий на портале GitHub
| Образец | Результат настраиваемого действия |
| --- | --- |
| [Загрузчик данных HTTP](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample) |Загружает данные из конечной точки HTTP tooAzure хранилища больших двоичных объектов с помощью пользовательского действия C# в фабрике данных. |
| [Пример анализа мнений с помощью Twitter](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |Вызов модели машинного обучения Azure и выполнение анализа мнений, оценки, прогнозирования и т. д. |
| [Запуск скрипта R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample) |Вызов сценария R путем запуска RScript.exe в кластере HDInsight, где уже установлен R. |
| [Действие перекрестного домена приложения .NET](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |Использует разные версии сборки из тех, которые используются с запуска hello фабрики данных |
| [Повторная обработка модели в службах Azure Analysis Services](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  Повторная обработка модели в службах Azure Analysis Services. |

[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: ./media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: ./media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png
