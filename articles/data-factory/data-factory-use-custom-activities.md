---
title: "Использование настраиваемых действий в конвейере фабрики данных Azure"
description: "Узнайте, как создавать пользовательские действия и использовать их в конвейере фабрики данных Azure."
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
ms.openlocfilehash: f3d265f31cb653d32076747e586383d67bbccc41
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
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

- [Действия перемещения данных](data-factory-data-movement-activities.md) для перемещения данных между [поддерживаемыми исходными хранилищами данных и хранилищами данных-приемниками](data-factory-data-movement-activities.md#supported-data-stores-and-formats).
- [Действия преобразования данных](data-factory-data-transformation-activities.md) для преобразования данных с помощью служб вычислений, например: в Azure HDInsight, пакетной службе Azure и Машинном обучении Azure. 

Чтобы переместить данные из хранилища данных, которое не поддерживает фабрика данных Azure, или в такое хранилище, можно создать **пользовательское действие** с собственной логикой перемещения данных и использовать это действие в конвейере. Аналогично, чтобы преобразовать или обработать данные способом, который не поддерживается фабрикой данных Azure, создайте пользовательское действие с собственной логикой преобразования данных и используйте это действие в конвейере. 

Вы можете настроить запуск пользовательского действия в пуле виртуальных машин **пакетной службы Azure** или в кластере **Azure HDInsight** на базе Windows. При использовании пакетной службы Azure можно использовать только имеющийся пул пакетной службы Azure. А при использовании HDInsight можно применить имеющийся кластер HDInsight или кластер, который автоматически создается для вас по запросу в среде выполнения.  

В следующем руководстве содержатся пошаговые инструкции по созданию пользовательского действия .NET и его использованию в конвейере. В этом пошаговом руководстве используется связанная **пакетная служба Azure**. Чтобы вместо нее использовалась связанная служба Azure HDInsight, создайте связанную службу типа **HDInsight** (ваш кластер HDInsight) или **HDInsightOnDemand** (фабрика данных создает кластер HDInsight по запросу). Затем настройте пользовательское действие для использования связанной службы HDInsight. Дополнительные сведения об использовании Azure HDInsight для выполнения пользовательского действия приведены в разделе [Использование связанных служб Azure HDInsight](#use-hdinsight-compute-service) .

> [!IMPORTANT]
> - Пользовательские действия .NET выполняются только в кластерах HDInsight на платформе Windows. Чтобы обойти это ограничение, используйте действие Map Reduce для запуска пользовательского кода Java в кластере HDInsight под управлением Linux. Другой вариант — использовать для выполнения пользовательских действий пул виртуальных машин пакетной службы Azure, а не кластер HDInsight.
> - Невозможно использовать шлюз управления данными из пользовательского действия для доступа к локальным источникам данных. В настоящее время [шлюз управления данными](data-factory-data-management-gateway.md) поддерживает действие копирования и действие хранимой процедуры только в фабрике данных.   

## <a name="walkthrough-create-a-custom-activity"></a>Пошаговое руководство по созданию настраиваемого действия
### <a name="prerequisites"></a>Предварительные требования
* Visual Studio 2012/2013/2015
* Скачайте и установите пакет [Azure .NET SDK](https://azure.microsoft.com/downloads/)

### <a name="azure-batch-prerequisites"></a>Предварительные требования для пакетной службы Azure
В этом руководстве вы запустите свои настраиваемые действия .NET с помощью пакетной службы Azure как вычислительные ресурсы. **Пакетная служба Azure** — это служба платформы, которая позволяет эффективно работать с приложениями для крупномасштабных параллельных и высокопроизводительных вычислений (HPC) в облаке. Пакетная служба Azure планирует запуск ресурсоемких вычислительных задач в управляемой **коллекции виртуальных машин** и автоматически масштабирует вычислительные ресурсы, учитывая требования заданий. Подробные сведения о пакетной службе Azure см. в [этой статье][batch-technical-overview].

Для этого руководства создайте учетную запись пакетной службы Azure с пулом виртуальных машин. Для этого выполните следующие действия:

1. Создание **учетной записи пакетной службы Azure** на [портале Azure](http://portal.azure.com). Инструкции см. в статье [Создание учетной записи пакетной службы Azure на портале Azure][batch-create-account].
2. Запишите ключ и имя учетной записи пакетной службы Azure, а также URI и имя пула. Они понадобятся при создании связанной службы пакетной службы Azure.
    1. На домашней странице учетной записи пакетной службы Azure отображается **URL-адрес** в следующем формате: `https://myaccount.westus.batch.azure.com`. В этом примере **myaccount** — это имя учетной записи пакетной службы Azure. URI, используемый в определении связанной службы — это URL-адрес без имени учетной записи. Например, `https://<region>.batch.azure.com`.
    2. В меню слева щелкните **Ключи** и скопируйте значение параметра **Первичный ключ доступа**.
    3. Чтобы использовать имеющийся пул, щелкните **Пулы** в меню и запишите **идентификатор** пула. Если у вас нет пула, перейдите к следующему шагу.     
2. Создайте **пул пакетной службы Azure**.

   1. На [портале Azure](https://portal.azure.com) щелкните **Обзор** в меню слева и выберите **Уч. записи пакетной службы**.
   2. Выберите свою учетную запись пакетной службы Azure, чтобы открыть колонку **Учетная запись пакетной службы** .
   3. Щелкните элемент **Пулы** .
   4. В колонке **Пулы** нажмите кнопку "Добавить" на панели инструментов, чтобы добавить пул.
      1. Введите идентификатор для пула (идентификатор пула). Сохраните **идентификатор пула**. Он понадобится при создании решения фабрики данных.
      2. В качестве параметра семейства операционных систем укажите **Windows Server 2012 R2** .
      3. Выберите **Ценовая категория для узлов**.
      4. Для параметра **Выделенный целевой объект** укажите значение **2**.
      5. Для параметра **Максимальное число заданий на узел** укажите значение **2**.
   5. Нажмите кнопку **ОК** , чтобы создать пул.
   6. Запишите **идентификатор** пула. 



### <a name="high-level-steps"></a>Пошаговые действия
Ниже приведены два высокоуровневых шага, выполняемые в рамках этого пошагового руководства. 

1. Создайте пользовательское действие, содержащее простую логику преобразования и обработки данных.
2. Создайте фабрику данных Azure с конвейером, использующим пользовательское действие.

### <a name="create-a-custom-activity"></a>Создать настраиваемое действие.
Чтобы создать настраиваемое действие .NET, создайте проект **библиотеки классов .NET** с классом, который реализует интерфейс **IDotNetActivity**. У этого интерфейса есть только один метод [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) , и его сигнатура такова.

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


Метод принимает четыре параметра:

- **linkedServices** — Это свойство является перечисляемым списком связанных служб хранилища данных, на которые ссылаются входные и выходные наборы данных для действия.   
- **наборы данных**. Это свойство является перечисляемым списком входных и выходных наборов данных для действия. Этот параметр можно использовать для получения расположений и схем, которые определяются входными и выходными наборами данных.
- **activity** — Это свойство представляет текущее действие. Его можно использовать для доступа к расширенным свойствам, связанным с пользовательским действием. Дополнительные сведения см. в разделе [Доступ к расширенным свойствам](#access-extended-properties).
- **logger** — Этот объект позволяет записывать комментарии отладки, которые отображаются в виде пользовательского журнала для конвейера.

Этот метод возвращает словарь, который можно будет использовать для создания цепочки из настраиваемых действий в будущем. Эта функция еще не реализована, поэтому из метода просто возвращается пустой словарь.  

### <a name="procedure"></a>Описание процедуры
1. Создайте проект **библиотеки классов .NET** .
   <ol type="a">
     <li>Запустите <b>Visual Studio 2017</b>, <b>Visual Studio 2015</b>, <b>Visual Studio 2013</b> или <b>Visual Studio 2012</b>.</li>
     <li>Щелкните <b>Файл</b>, наведите указатель мыши на пункт <b>Создать</b> и щелкните <b>Проект</b>.</li>
     <li>Разверните раздел <b>Шаблоны</b> и выберите <b>Visual C#</b>. В этом руководстве используется язык C#, но для создания настраиваемого действия вы можете использовать любой язык .NET.;</li>
     <li>Выберите тип <b>Библиотека классов</b> из списка типов проектов справа. В VS 2017 выберите <b>Библиотека классов (.NET Framework)</b> .</li>
     <li>В поле <b>Имя</b> введите <b>MyDotNetActivity</b>.</li>
     <li>В качестве <b>расположения</b> укажите <b>C:\ADFGetStarted</b>.</li>
     <li>Нажмите кнопку <b>ОК</b> , чтобы создать проект.</li>
   </ol>
2. Щелкните **Инструменты**, наведите указатель мыши на пункт **Диспетчер пакетов NuGet** и щелкните **Консоль диспетчера пакетов**.
3. В консоли диспетчера пакетов выполните следующую команду, чтобы импортировать пакет **Microsoft.Azure.Management.DataFactories**.

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. Импортируйте пакет NuGet для **службы хранилища Azure** в проект.

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > Средство запуска службы фабрики данных требует пакет WindowsAzure.Storage версии 4.3. Если добавить ссылку в проекте настраиваемого действия в сборку службы хранилища Azure более поздней версии, при выполнении действия возникнет ошибка. Чтобы устранить ее, см. раздел [Изоляция домена приложения](#appdomain-isolation). 
5. Добавьте следующие инструкции с **using** в исходный файл в проекте.

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
6. Измените имя **пространства имен** на **MyDotNetActivityNS**.

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. Измените имя класса на **MyDotNetActivity** и извлеките класс из интерфейса **IDotNetActivity**, как показано в следующем фрагменте кода:

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. Реализуйте (добавьте) метод **Execute** интерфейса **IDotNetActivity** для класса **MyDotNetActivity** и скопируйте следующий пример кода в этот метод.

    Следующий пример подсчитывает количество вхождений поисковой фразы ("Microsoft") в каждый большой двоичный объект, связанный со срезом данных.

    ```csharp
    /// <summary>
    /// Execute method is the only method of IDotNetActivity interface you must implement.
    /// In this sample, the method invokes the Calculate method to perform the core logic.  
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
    
        // to log information, use the logger object
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

        // get the input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables to hold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from the dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and the other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get the first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using the same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get the connection string in the linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get the folder path from the input dataset definition
        string folderPath = GetFolderPath(inputDataset);
        string output = string.Empty; // for use later.
    
        // create storage client for input. Pass the connection string.
        CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
        CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
        // initialize the continuation token before using it in the do-while loop.
        BlobContinuationToken continuationToken = null;
        do
        {   // get the list of input blobs from the input storage client object.
            BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                     true,
                                     BlobListingDetails.Metadata,
                                     null,
                                     continuationToken,
                                     null,
                                     null);
    
            // Calculate method returns the number of occurrences of
            // the search term (“Microsoft”) in each blob associated
               // with the data slice. definition of the method is shown in the next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get the output dataset using the name of the dataset matched to a name in the Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for the output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get the folder path from the output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log the output folder path   
        logger.Write("Writing blob to the folder: {0}", folderPath);
    
        // create a storage object for the output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write the name of the file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log the output file name
        logger.Write("output blob URI: {0}", outputBlobUri.ToString());

        // create a blob and upload the output text.
        CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
        logger.Write("Writing {0} to the output blob", output);
        outputBlob.UploadText(output);
    
        // The dictionary can be used to chain custom activities together in the future.
        // This feature is not implemented yet, so just return an empty dictionary.  
    
        return new Dictionary<string, string>();
    }
    ```
9. Добавьте следующие вспомогательные методы. 

    ```csharp
    /// <summary>
    /// Gets the folderPath value from the input/output dataset.
    /// </summary>
    
    private static string GetFolderPath(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }

        // get type properties of the dataset   
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return the folder path found in the type properties
        return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets the fileName value from the input/output dataset.   
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }
    
        // get type properties of the dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return the blob/file name in the type properties
        return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in the folder, counts the number of instances of search term in the file,
    /// and prepares the output text that is written to the output blob.
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
                output += string.Format("{0} occurrences(s) of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
            }
        }
        return output;
    }
    ```

    Метод GetFolderPath возвращает путь к папке, на которую указывает набор данных, а метод GetFileName — имя большого двоичного объекта или файла, на который указывает набор данных. Если параметр havefolderPath определяется с помощью переменных, таких как {Year}, {Month} {Day} и т. д, то метод возвращает строку как есть, не заменяя эти переменные соответствующими значениями на момент запуска. Дополнительные сведения о доступе к SliceStart, SliceEnd и т. д. см. в разделе [Доступ к расширенным свойствам](#access-extended-properties).    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    Метод Calculate вычисляет количество экземпляров ключевого слова Microsoft во входных файлах (в больших двоичных объектах в папке). Условие поиска (Microsoft) жестко задано в коде.
10. Скомпилируйте проект. В меню щелкните **Построить** и **Построить решение**.

    > [!IMPORTANT]
    > Задайте версию 4.5.2 платформы .NET Framework в качестве целевой для своего проекта: щелкните правой кнопкой мыши проект и выберите **Свойства**, чтобы задать целевую платформу. Фабрика данных не поддерживает настраиваемые действия, скомпилированные для более поздних версий, чем .NET Framework 4.5.2.

11. Запустите **проводник Windows** и перейдите к папке **bin\debug** или **bin\release** в зависимости от типа сборки.
12. Создайте ZIP-файл **MyDotNetActivity.zip**, который содержит все двоичные файлы из папки <project folder>\bin\Debug. Добавьте файл **MyDotNetActivity.pdb**, чтобы в случае сбоя получить дополнительные сведения, например номер строки в исходном коде, вызвавшем ошибку. 

    > [!IMPORTANT]
    > Все файлы в ZIP-файле для настраиваемого действия должны размещаться на **верхнем уровне** без вложенных папок.

    ![Двоичные выходные файлы](./media/data-factory-use-custom-activities/Binaries.png)
14. Создайте контейнер больших двоичных объектов **customactivitycontainer**, если он еще не создан. 
15. Отправьте файл MyDotNetActivity.zip в виде BLOB-объекта в контейнер customactivitycontainer в хранилище BLOB-объектов Azure **общего назначения** (не в "горячее" или "холодное" хранилище BLOB-объектов), на которое ссылается служба AzureStorageLinkedService.  

> [!IMPORTANT]
> Если добавить этот проект действия .NET в решение в Visual Studio, содержащее проект фабрики данных, и добавить ссылку в проект действия .NET из проекта приложения фабрики данных, то не обязательно выполнять два последних шага по созданию ZIP-файла и его добавлению в хранилище BLOB-объектов Azure общего назначения. При публикации сущностей фабрики данных с помощью Visual Studio эти шаги выполняются автоматически в процессе публикации. Дополнительные сведения см. в разделе [Проект фабрики данных в Visual Studio](#data-factory-project-in-visual-studio).

## <a name="create-a-pipeline-with-custom-activity"></a>Создание конвейера с настраиваемым действием
Вы создали пользовательское действие и отправили ZIP-файл с двоичными файлами в контейнер больших двоичных объектов в учетной записи хранения Azure **общего назначения**. В этом разделе вы создадите фабрику данных Azure с конвейером, использующим пользовательское действие.

Входной набор данных для пользовательского действия представляет собой большие двоичные объекты (файлы) в папке customactivityinput контейнера adftutorial в хранилище BLOB-объектов. Выходной набор данных для пользовательского действия представляет собой выходные большие двоичные объекты в папке customactivityoutput контейнера adftutorial в хранилище BLOB-объектов.

Создайте файл **file.txt** со следующим содержимым, а затем отправьте его в папку **customactivityinput** контейнера **adftutorial**. Если контейнер adftutorial еще не существует, создайте его. 

```
test custom activity Microsoft test custom activity Microsoft
```

Входная папка соответствует одному срезу в фабрике данных Azure, даже если она содержит два файла или более. При обработке каждого среза конвейером пользовательское действие выполняет итерацию всех больших двоичных объектов во входной папке для этого среза.

В папке adftutorial\customactivityoutput отображается один выходной файл с одной или несколькими строками (соответствует количеству больших двоичных объектов во входной папке):

```
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2016-11-16-00/file.txt.
```


Ниже приведены шаги, подробно описанные далее в этом разделе.

1. Создание **фабрики данных**.
2. Создание **связанных служб** для пула виртуальных машин пакетной службы Azure, в котором выполняется пользовательское действие, а также экземпляр службы хранилища Azure, содержащей входные и выходные большие двоичные объекты.
3. Создание входных и выходных **наборов данных**, которые представляют собой входные и выходные данные пользовательского действия.
4. Создание **конвейера**, который использует пользовательское действие.

> [!NOTE]
> Создайте файл **file.txt** и передайте его в контейнер больших двоичных объектов, если еще не сделали это. Инструкции см. в предыдущем разделе.   

### <a name="step-1-create-the-data-factory"></a>Шаг 1. Создание фабрики данных
1. Войдите на портал Azure и выполните следующие действия:
   1. В меню слева нажмите кнопку **Создать** .
   2. В колонке **Создание** щелкните **Данные и аналитика**.
   3. Щелкните **Фабрика данных** в колонке **Аналитика данных**.
   
    ![Меню создания фабрики данных Azure](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. В колонке **Создание фабрики данных** в поле "Имя" введите **CustomActivityFactory**. Имя фабрики данных Azure должно быть глобально уникальным. Если возникнет ошибка **Имя фабрики данных CustomActivityFactory недоступно**, измените имя этой фабрики данных (например, на **ваше_имяCustomActivityFactory**) и попробуйте создать ее снова.

    ![Колонка создания фабрики данных Azure](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. Щелкните **Имя группы ресурсов**, чтобы выбрать имеющуюся группу ресурсов, или создайте группу ресурсов.
4. Убедитесь, что используется именно те **подписка** и **регион**, в которых необходимо создать фабрику данных.
5. В колонке **Создание фабрики данных** нажмите кнопку **Создать**.
6. Созданная фабрика данных появится на **панели мониторинга** портала Azure.
7. После создания фабрики данных ее содержимое отобразится в соответствующей колонке.
    
    ![Колонка "Фабрика данных"](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a>Шаг 2. Создание связанных служб
Связанные службы связывают хранилища данных или службы вычислений с фабрикой данных Azure. На этом этапе учетная запись службы хранилища Azure и учетная запись пакетной службы Azure будут связаны с фабрикой данных.

#### <a name="create-azure-storage-linked-service"></a>Создание связанной службы хранения Azure
1. В колонке **Фабрика данных** для **CustomActivityFactory** щелкните элемент **Создание и развертывание**. Отобразится редактор фабрики данных.
2. На панели команд щелкните **Создание хранилища данных** и выберите **Служба хранилища Azure**. В редакторе отобразится сценарий JSON для создания связанной службы хранилища Azure.
    
    !["Новое хранилище данных" — "Служба хранилища Azure"](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. Замените `<accountname>` именем своей учетной записи хранения Azure, а `<accountkey>` — ключом доступа к ней. Сведения о получении ключа доступа к хранилищу см. в разделах о [просмотре, копировании и повторном создании ключей доступа к хранилищу](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

    ![Связанная служба хранилища Azure](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. Чтобы развернуть эту службу, нажмите кнопку **Развернуть** на панели команд.

#### <a name="create-azure-batch-linked-service"></a>Создание связанной пакетной службы Azure
1. В редакторе фабрики данных нажмите кнопку **... Еще** на панели команд, щелкните **Новое вычисление** и выберите в меню пункт **Пакет Azure**.

    !["Новое вычисление" — "Пакет Azure"](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. Внесите следующие изменения в сценарий JSON:

   1. В свойстве **accountName** укажите имя учетной записи пакетной службы Azure. **URL-адрес** из **колонки учетной записи пакетной службы Azure** имеет следующий формат: `http://accountname.region.batch.azure.com`. В свойстве **batchUri** в JSON требуется удалить заполнитель `accountname.` в URL-адресе и использовать значение `accountname` для свойства JSON `accountName`.
   2. В свойстве **accessKey** укажите ключ учетной записи пакетной службы Azure.
   3. В свойстве **poolName** укажите имя пула, созданного при выполнении предварительных требований. Вместо имени пула также можно указать идентификатор пула.
   4. В свойстве **batchUri** укажите универсальный код ресурса (URI) пакетной службы Azure. Пример: `https://westus.batch.azure.com`.  
   5. Для свойства **AzureStorageLinkedService** for the **linkedServiceName** укажите имя учетной записи пакетной службы Azure.

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

       Для свойства **poolName** можно также указать идентификатор пула вместо его имени.

      > [!IMPORTANT]
      > Служба фабрики данных не поддерживает параметр по требованию для пакетной службы Azure, как для HDInsight. Пул пакетной службы Azure можно использовать только в фабрике данных Azure.   
    

### <a name="step-3-create-datasets"></a>Шаг 3. Создание наборов данных
На этом шаге вы создадите наборы данных, которые представляют входные и выходные данные.

#### <a name="create-input-dataset"></a>Создание входного набора данных
1. В **редакторе** фабрики данных щелкните **... Еще** на панели команд, щелкните **Новый набор данных** и выберите в раскрывающемся меню пункт **Хранилище BLOB-объектов Azure**.
2. Замените код JSON в правой области на следующий фрагмент кода JSON:

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

   Позже в этом пошаговом руководстве вы создадите конвейер со временем начала 2016-11-16T00:00:00Z и временем окончания 2016-11-16T05:00:00Z. Данные будут создаваться почасово, поэтому мы получим пять входных и выходных срезов (от **00**:00:00 до **05**:00:00).

   Для параметров **frequency** и **interval** входного набора данных установлены значения **Hour** и **1**. Это означает, что входной срез данных будет создаваться каждый час. В этом примере используется тот же файл (file.txt) в папке intputfolder.

   Это значения времени начала для каждого среза, представленные системной переменной SliceStart в приведенном выше фрагменте кода JSON.
3. На панели инструментов щелкните **Развернуть**, чтобы создать и развернуть **InputDataset**. Убедитесь, что на панели заголовка редактора отображается сообщение **ТАБЛИЦА УСПЕШНО СОЗДАНА** .

#### <a name="create-an-output-dataset"></a>Создание выходного набора данных
1. В **редакторе фабрики данных** нажмите кнопку **... Еще** на панели команд, щелкните **Новый набор данных** и выберите пункт **Хранилище BLOB-объектов Azure**.
2. Замените сценарий JSON в правой области на следующий:

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

     Выходное расположение — **adftutorial/customactivityoutput/**, а имя выходного файла — ГГГГ-ММ-ДД-ЧЧ.txt (где ГГГГ, ММ, ДД и ЧЧ — год, месяц, день и час создания среза). Подробную информацию см. в [справочнике разработчика фабрики данных Azure][adf-developer-reference].

    Для каждого входного среза данных создается выходной большой двоичный объект или файл. Ниже в таблице приведены имена, которые даются выходным файлам для каждого среза. Все выходные файлы создаются в одной выходной папке: **adftutorial\customactivityoutput**.

   | Срез | Время начала | Выходной файл |
   |:--- |:--- |:--- |
   | 1 |2016-11-16T00:00:00 |2016-11-16-00.txt |
   | 2 |2016-11-16T01:00:00 |2016-11-16-01.txt |
   | 3 |2016-11-16T02:00:00 |2016-11-16-02.txt |
   | 4 |2016-11-16T03:00:00 |2016-11-16-03.txt |
   | 5 |2016-11-16T04:00:00 |2016-11-16-04.txt |

    Помните, что все файлы во входной папке являются частью среза со значениями времени начала, указанными выше. Во время обработки этого среза пользовательское действие сканирует каждый файл и создает строку в выходном файле с количеством вхождений условия поиска (Microsoft). Если в папке inputfolder находятся три файла, в выходном файле будут содержаться три строки для каждого почасового среза: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt и т. д.
3. На панели команд нажмите кнопку **Развернуть**, чтобы развернуть **OutputDataset**.

### <a name="create-and-run-a-pipeline-that-uses-the-custom-activity"></a>Создание и запуск конвейера, который использует настраиваемое действие
1. В редакторе фабрики данных нажмите кнопку **... Еще**, а затем нажмите на панели команд кнопку **Новый конвейер**. 
2. Замените сценарий JSON в правой области приведенным ниже.

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

    Обратите внимание на следующие моменты.

   * Для свойства **Concurrency** установлено значение **2**, чтобы два среза параллельно обрабатывались двумя виртуальными машинами в пуле пакетной службы Azure.
   * в разделе действий содержится одно действие типа **DotNetActivity**;
   * В **AssemblyName** задано имя библиотеки DLL **MyDotNetActivity.dll**.
   * В **EntryPoint** — **MyDotNetActivityNS.MyDotNetActivity**.
   * Для параметра **PackageLinkedService** задано значение **AzureStorageLinkedService**, которое указывает на хранилище BLOB-объектов, содержащее ZIP-файл настраиваемого действия. Если для входных и выходных файлов и ZIP-файла настраиваемого действия используются разные учетные записи службы хранилища Azure, необходимо создать другую связанную службу хранилища Azure. В этой статье предполагается использование одной и той же учетной записи хранения Azure.
   * Для **PackageFile** установлено значение **customactivitycontainer/MyDotNetActivity.zip**. Используется формат <контейнер_для_zip-файла>/<имя_zip-файла.zip>.
   * Настраиваемое действие принимает **InputDataset** в качестве входных данных и **OutputDataset** — в качестве выходных данных.
   * Свойство linkedServiceNam настраиваемого действия указывает на свойство **AzureBatchLinkedService**, которое сообщает фабрике данных Azure, что необходимо запустить настраиваемое действие на виртуальных машинах пакетной службы Azure.
   * Для свойства **isPaused** по умолчанию установлено значение **false**. В этом примере конвейер запускается незамедлительно, потому что срезы приходятся на прошлое. Для этого свойства можно задать значение true, чтобы приостановить работу конвейера. Чтобы перезапустить его, нужно снова установить значение false.
   * Разница между временем **начала** и временем **окончания** составляет **пять** часов, а срезы создаются каждый час. Таким образом конвейер создает пять срезов.
3. Чтобы развернуть конвейер, на панели команд нажмите кнопку **Развернуть**.

### <a name="monitor-the-pipeline"></a>Мониторинг конвейера
1. На портале Azure в колонке "Фабрика данных" щелкните **Схема**.

    ![Плитка "Схема"](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. Теперь в представлении схемы щелкните OutputDataset.

    ![Представление схемы](./media/data-factory-use-custom-activities/diagram.png)
3. Вы увидите пять выходных срезов данных в состоянии готовности. Если они не в состоянии готовности, они еще не созданы. 

   ![Выходные срезы](./media/data-factory-use-custom-activities/OutputSlices.png)
4. Убедитесь, что выходные файлы создаются в хранилище больших двоичных объектов в контейнере **adftutorial** .

   ![выходные данные настраиваемого действия][image-data-factory-ouput-from-custom-activity]
5. Если вы откроете выходной файл, вы увидите выходные данные, похожие на следующие:

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2016-11-16-00/file.txt.
    ```
6. Используйте [портал Azure][azure-preview-portal] или командлеты Azure PowerShell для отслеживания состояния фабрики данных, конвейеров и наборов данных. Вы можете просматривать сообщения **ActivityLogger** о настраиваемом действии в журналах (а именно — user-0.log), которые можно скачать на портале или с помощью командлетов.

   ![скачивание журналов из настраиваемого действия][image-data-factory-download-logs-from-custom-activity]

Подробные указания по мониторингу наборов данных и конвейеров см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими](data-factory-monitor-manage-pipelines.md).      

## <a name="data-factory-project-in-visual-studio"></a>Проект фабрики данных в Visual Studio  
Можно создать и опубликовать сущности фабрики данных, используя Visual Studio вместо портала Azure. Подробные сведения о создании и публикации сущностей фабрики данных с помощью Visual Studio см. в статьях [Создание первого конвейера с помощью Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) и [Копирование данных из большого двоичного объекта Azure в SQL Azure](data-factory-copy-activity-tutorial-using-visual-studio.md).

При создании проекта фабрики данных в Visual Studio выполните следующие дополнительные шаги:
 
1. Добавьте проект фабрики данных в решение Visual Studio, содержащее проект настраиваемого действия. 
2. Добавьте ссылку на проект действия .NET из проекта фабрики данных. Щелкните проект фабрики данных правой кнопкой мыши, наведите курсор на команду **Добавить** и щелкните **Ссылка**. 
3. В диалоговом окне **Добавление ссылки** выберите проект **MyDotNetActivity** и нажмите кнопку **ОК**.
4. Выполните сборку и опубликуйте решение.

    > [!IMPORTANT]
    > При публикации сущностей фабрики данных автоматически создается ZIP-файл, который затем передается в контейнер BLOB-объектов customactivitycontainer. Если контейнер BLOB-объектов не существует, то он также создается автоматически.  


## <a name="data-factory-and-batch-integration"></a>Интеграция фабрики данных и пакетной службы
Служба фабрики данных создает в пакетной службе Azure задание с именем **adf-poolname:job-xxx**. В меню слева щелкните **Задания**. 

![Фабрика данных Azure — задания пакетной службы](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

Такое задание создается для каждого запуска действия среза. При наличии пяти срезов, готовых к обработке, в рамках этого задания создаются пять задач. Если в пуле пакетной службы есть несколько вычислительных узлов, два или больше среза могут выполняться параллельно. Если для максимального количества задач на вычислительный узел установлено значение > 1, также можно выполнять сразу несколько срезов в одной среде выполнения приложений.

![Фабрика данных Azure — задачи задания пакетной службы](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

На следующей схеме показана связь между задачами фабрики данных и пакетной службы Azure.

![Фабрика данных и пакетная служба](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a>Устранение ошибок
Устранение неполадок состоит из нескольких базовых методов:

1. Если отображается следующая ошибка, возможно, используется "горячее" или "холодное" хранилище BLOB-объектов вместо хранилища BLOB-объектов Azure общего назначения. Отправьте ZIP-файл в **учетную запись хранения Azure общего назначения**. 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of the specified Azure Blob(s).
    ``` 
2. Если отображается следующая ошибка, убедитесь, что имя класса в CS-файле соответствует имени, указанному для свойства **EntryPoint** в конвейере JSON. В пошаговом руководстве имя класса — MyDotNetActivity, а для свойства EntryPoint в конвейере JSON указано значение MyDotNetActivityNS.**MyDotNetActivity**.

    ```
    MyDotNetActivity assembly does not exist or doesn't implement the type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   Если имена соответствуют, убедитесь, что все двоичные файлы размещены в **корневой папке** ZIP-файла. Это означает, что при открытии ZIP-файла все файлы должны находиться в корневой папке, а не во вложенных.   
3. Если для входного среза данных не установлено значение **Готов**, убедитесь, что структура входной папки правильная и что в ней существует файл **file.txt**.
3. В методе **Execute** настраиваемого действия используйте объект **IActivityLogger**, чтобы записывать в журнал сведения, которые помогут устранить неполадки. Сообщения, записываемые в журналы, появятся в файлах журнала пользователя (один или несколько файлов с именами user-0.log, user-1.log, user-2.log и т. д.).

   В колонке **OutputDataset** щелкните срез, чтобы открыть для него колонку **Срез данных**. Для этого среза будет указано значение **Запуски операции** . Должно выполняться лишь одно действие. Если в командной строке нажать кнопку «Запуск», можно запустить другое действие для этого среза.

   Если щелкнуть выполняемое действие, появится колонка **Подробности о выполнении операции** со списком файлов журнала. Записанные в журнал сообщения можно увидеть в файле user_0.log. Если возникнет ошибка, действие будет выполнено три раза, так как для количества повторных попыток в JSON-файле конвейера или действия задано значение 3. Если щелкнуть выполняемое действие, отобразятся файлы журнала, которые можно использовать для устранения ошибки.

   В списке файлов журнала щелкните **user-0.log**. На панели справа отображаются результаты использования метода **IActivityLogger.Write** . Если вы не видите всех сообщений, проверьте наличие дополнительных файлов журнала user_1.log, user_2.log и т. д. Если нет, сбой в коде, возможно, произошел уже после последнего сообщения, записанного в журнал.

   Кроме того, проверьте файл **system-0.log** на наличие любых системных сообщений об ошибках или исключений.
4. Добавьте **PDB-файл** в ZIP-файл, чтобы в случае возникновения ошибки сведения об ошибке содержали, например, информацию о **стеке вызовов**.
5. Все файлы в ZIP-файле для настраиваемого действия должны размещаться на **верхнем уровне** без вложенных папок.
6. Убедитесь, что для параметров **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip) и **packageLinkedService** (должен указывать на хранилище BLOB-объектов Azure **общего назначения**, содержащее ZIP-файл) установлены правильные значения.
7. Если ошибки устранены и необходимо повторно обработать срез, в колонке **OutputDataset** щелкните срез правой кнопкой мыши и выберите пункт **Запуск**.
8. Если возникла указанная ниже ошибка, это значит, что вы используете пакет службы хранилища Azure более поздней версии, чем 4.3.0. Средство запуска службы фабрики данных требует пакет WindowsAzure.Storage версии 4.3. Сведения о том, что делать, если вам нужно использовать более позднюю версию сборки службы хранилища Azure, см. в разделе [Изоляции домена приложения](#appdomain-isolation). 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    Если вы можете использовать пакет службы хранилища Azure версии 4.3.0, удалите существующую ссылку на пакет Azure.Storage более поздней версии, чем 4.3.0, и выполните следующую команду в консоли диспетчера пакетов Nuget. 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    Создайте проект. Удалите сборку WindowsAzure.Storage более поздней версии, чем 4.3.0, из папки bin\Debug. Создайте ZIP-файл с двоичными файлами и PDB-файлом. Замените старый ZIP-файл в контейнере больших двоичных объектов (customactivitycontainer) созданным. Повторно запустите срезы, в которых произошли сбои (щелкните срез правой кнопкой мыши и выберите пункт "Выполнить").   
8. Настраиваемое действие не использует файл **app.config** из пакета. Поэтому, если код считывает какие-либо строки подключения из файла конфигурации, это не сработает во время выполнения. При использовании пакетной службы Azure рекомендуется хранить все секреты в **хранилище ключей Azure**. Кроме того, следует использовать субъект-службу на основе сертификата для защиты **хранилища ключей** и переместить сертификат в пул пакетной службы Azure. В этом случае пользовательское действие .NET в среде выполнения сможет использовать секреты из хранилища ключей. Это общее решение, которое можно использовать для любого типа секретов, а не только строк подключения.

   Существует и более простое (но не самое лучшее) решение: можно создать **связанную службу SQL Azure** с параметрами строки подключения, набор данных, использующий связанную службу, и привязать его как фиктивный набор входных данных к настраиваемому действию .NET. После этого вы сможете получить доступ к строке подключения связанной службы из кода пользовательского действия.  

## <a name="update-custom-activity"></a>Обновление пользовательского действия
Если вы обновляете код для настраиваемого действия, создайте его и отправьте ZIP-файл, содержащий новые двоичные файлы, в службу хранилища больших двоичных объектов.

## <a name="appdomain-isolation"></a>Изоляция домена приложения
В разделе с [примером перекрестного домена приложения](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) показано, как создать пользовательское действие, которое не ограничено версиями сборок, используемых средством запуска фабрики данных Azure (например, WindowsAzure.Storage версии 4.3.0, Newtonsoft.Json версии 6.0.x и т. д.).

## <a name="access-extended-properties"></a>Доступ к расширенным свойствам
Вы можете объявить расширенные свойства в действии JSON, как показано в примере ниже.

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


В примере есть два расширенных свойства: **SliceStart** и **DataFactoryName**. Значение свойства SliceStart основано на системной переменной SliceStart. Список поддерживаемых системных переменных см. [в этом разделе](data-factory-functions-variables.md). Значение свойства DataFactoryName жестко задано как CustomActivityFactory.

Для доступа к этим расширенным свойствам в методе **Execute** используйте код, аналогичный приведенному ниже.

```csharp
// to get extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// to log all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a>Автомасштабирование пакетной службы Azure
Можно также создать пул пакетной службы Azure с использованием функции **автомасштабирования** . Например, можно создать пул пакетной службы Azure с нулем выделенных виртуальных машин и формулой автоматического масштабирования на основе числа ожидающих задач. 

Приведенный здесь пример формулы обеспечивает следующее поведение: при создании пула он изначально содержит одну виртуальную машину. Метрика $PendingTasks определяет количество задач в состоянии выполнения и активном состоянии (в очереди).  Формула находит среднее число ожидающих выполнения задач за последние 180 секунд и соответствующим образом задает значение TargetDedicated. Благодаря этому значение TargetDedicated никогда не превысит 25 виртуальных машин. Таким образом, по мере поступления новых задач пул автоматически увеличивается, а по мере их завершения виртуальные машины высвобождаются по одной, и функция автоматического масштабирования уменьшает пул. Значения startingNumberOfVMs и maxNumberofVMs можно настроить в соответствии со своими потребностями.

Формула автоматического масштабирования:

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

Дополнительные сведения см. в статье [Автоматическое масштабирование вычислительных узлов в пуле пакетной службы Azure](../batch/batch-automatic-scaling.md).

Если в пуле используется [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx)(значение по умолчанию), пакетной службе может потребоваться 15–30 минут на подготовку виртуальной машины перед выполнением настраиваемого действия.  Если пул использует другое значение autoScaleEvaluationInterval, пакетная служба может затрачивать autoScaleEvaluationInterval плюс 10 минут.

## <a name="use-hdinsight-compute-service"></a>Использование службы вычислений HDInsight
В пошаговом руководстве для запуска пользовательского действия был использован вычислительный ресурс пакетной службы Azure. Также можно использовать собственный кластер HDInsight на базе Windows или создать такой кластер по требованию с помощью фабрики данных и запустить пользовательское действие на кластере HDInsight. Ниже приведены основные шаги для использования кластера HDInsight.

> [!IMPORTANT]
> Пользовательские действия .NET выполняются только в кластерах HDInsight на платформе Windows. Чтобы обойти это ограничение, используйте действие Map Reduce для запуска пользовательского кода Java в кластере HDInsight под управлением Linux. Другой вариант — использовать для выполнения пользовательских действий пул виртуальных машин пакетной службы Azure, а не кластер HDInsight.
 

1. Создайте связанную службу Azure HDInsight.   
2. Используйте связанную службу HDInsight вместо **AzureBatchLinkedService** в конвейере JSON.

Чтобы протестировать сценарий с использованием службы Azure HDInsight в руководстве, измените время **начала** и **окончания** для конвейера.

#### <a name="create-azure-hdinsight-linked-service"></a>Создание связанной службы Azure HDInsight
Служба фабрики данных Azure поддерживает создание кластера по запросу и использует его для обработки входных данных, чтобы создать выходные данные. Вы также можете использовать для этого собственный кластер. Когда вы используете кластер HDInsight по запросу, для каждого среза создается отдельный кластер. Если вы используете собственный кластер HDInsight, он сразу сможет обработать срез. Поэтому при использовании кластера по запросу выходные данные могут выводится не так быстро, как при использовании собственного кластера.

> [!NOTE]
> Во время выполнения экземпляр действия .NET выполняется только на одном рабочем узле в кластере HDInsight; его невозможно расширить для выполнения на нескольких узлах. Несколько экземпляров действия .NET действия могут выполняться параллельно на разных узлах кластера HDInsight.
>
>

##### <a name="to-use-an-on-demand-hdinsight-cluster"></a>Использование кластера HDInsight по запросу
1. На **портале Azure**щелкните **Создать и развернуть** .
2. В редакторе фабрики данных щелкните **Новое вычисление** на панели команд и выберите в меню **On-demand HDInsight cluster** (Кластер HDInsight по запросу).
3. Внесите следующие изменения в сценарий JSON:

   1. В свойстве **clusterSize** укажите размер кластера HDInsight.
   2. В свойстве **timeToLive** укажите, как долго может простаивать клиент, прежде чем он будет удален.
   3. В свойстве **version** укажите версию HDInsight, которую хотите использовать. Если исключить это свойство, будет использоваться последняя версия.  
   4. В свойстве **LinkedServiceName** укажите **AzureStorageLinkedService**.

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
    > Пользовательские действия .NET выполняются только в кластерах HDInsight на платформе Windows. Чтобы обойти это ограничение, используйте действие Map Reduce для запуска пользовательского кода Java в кластере HDInsight под управлением Linux. Другой вариант — использовать для выполнения пользовательских действий пул виртуальных машин пакетной службы Azure, а не кластер HDInsight.

4. Чтобы развернуть эту службу, нажмите кнопку **Развернуть** на панели команд.

##### <a name="to-use-your-own-hdinsight-cluster"></a>Использование собственного кластера HDInsight
1. На **портале Azure**щелкните **Создать и развернуть** .
2. В **редакторе фабрики данных** щелкните **Новое вычисление** на панели команд и выберите в меню **Кластер HDInsight**.
3. Внесите следующие изменения в сценарий JSON:

   1. В свойстве **clusterUri** укажите URL-адрес кластера HDInsight. Например, https://<clustername>.azurehdinsight.net/     
   2. В свойстве **UserName** введите имя пользователя, у которого есть доступ к кластеру HDInsight.
   3. В свойстве **Password** укажите пароль этого пользователя.
   4. В свойстве **LinkedServiceName** укажите **AzureStorageLinkedService**.
4. Чтобы развернуть эту службу, нажмите кнопку **Развернуть** на панели команд.

Дополнительные сведения см. в статье [Связанные службы вычислений](data-factory-compute-linked-services.md).

В **конвейере JSON**используйте связанную службу HDInsight (по запросу или собственную):

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
В этой статье содержится пошаговое руководство, в котором с помощью портала Azure создается фабрика данных с конвейером, использующим настраиваемое действие. В приведенном ниже коде показано, как создать фабрику данных с помощью пакета SDK для .NET. Дополнительные сведения об использовании пакета SDK для программного создания конвейеров см. в статье [Руководство. Создание конвейера с действием копирования с помощью API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md). 

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

            // TODO: replace ADFTutorialResourceGroup with the name of your resource group.
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

                            // Initial value for pipeline's active period. With this, you won't need to set slice status
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

            throw new InvalidOperationException("Failed to acquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a>Отладка настраиваемого действия в Visual Studio
Пример [локальной среды фабрики данных Azure](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) на портале GitHub включает в себя инструмент, который позволяет выполнять отладку настраиваемых действий .NET в Visual Studio.  


## <a name="sample-custom-activities-on-github"></a>Примеры настраиваемых действий на портале GitHub
| Образец | Результат настраиваемого действия |
| --- | --- |
| [Загрузчик данных HTTP](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample) |Загрузка данных из конечной точки HTTP в хранилище BLOB-объектов с помощью настраиваемого действия C# в фабрике данных Azure. |
| [Пример анализа мнений с помощью Twitter](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |Вызов модели машинного обучения Azure и выполнение анализа мнений, оценки, прогнозирования и т. д. |
| [Запуск скрипта R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample) |Вызов сценария R путем запуска RScript.exe в кластере HDInsight, где уже установлен R. |
| [Действие перекрестного домена приложения .NET](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |Использование разных версий сборок, которые используются средством запуска фабрики данных. |
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
