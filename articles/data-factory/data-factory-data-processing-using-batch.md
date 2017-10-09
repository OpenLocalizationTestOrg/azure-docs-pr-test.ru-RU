---
title: "aaaProcess крупномасштабных наборы данных, с помощью фабрики данных и пакет | Документы Microsoft"
description: "Описывает, как конвейер tooprocess огромное количество данных в фабрике данных Azure с помощью возможности параллельной обработки пакетной службы Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a>Обработка больших наборов данных с помощью фабрики данных и пакетной службы
В этой статье описывается архитектура простого решения, которое автоматически и по расписанию перемещает и обрабатывает большие наборы данных. Он также предоставляет решение hello tooimplement Пошаговое руководство с начала до конца, с помощью фабрики данных Azure и пакета Azure.

Эта статья длиннее обычной статьи, так как в ней содержится пошаговое руководство для всего примера решения. Если новый tooBatch и фабрики данных можно узнать об этих службах и о том, как они работают вместе. Если вы знаете, какое-либо службы hello и проектирование/архитектуры решения, вам может сосредоточиться только на hello [архитектура](#architecture-of-sample-solution) статье hello и если вы разрабатываете прототип или решения, вы также можете tootry out Пошаговые инструкции в hello [Пошаговое руководство](#implementation-of-sample-solution). Мы приветствуем ваши комментарии об этой статье и использовании ее содержимого.

Во-первых давайте взглянем на как фабрику данных и пакет служб может помочь с обработкой больших наборов данных в облаке hello.     

## <a name="why-azure-batch"></a>Сведения о пакетной службе Azure
Пакет Azure позволяет приложениям крупномасштабных параллельных и высокопроизводительных вычислительных систем (HPC) toorun эффективно работает в облаке hello. Она является службой платформы, которая планирует toorun работы с большим объемом вычислений в управляемой коллекции виртуальных машин и может автоматически масштабирование вычислительных потребностей hello toomeet ресурсы заданий.

С hello пакетная служба можно определить tooexecute Azure вычислительные ресурсы приложения в параллельном режиме, а в масштабе. Можно запустить по требованию или по расписанию заданий и нет необходимости toomanually создания, настройки и управления кластера HPC, отдельных виртуальных машин, виртуальных сетей или сложных заданий и инфраструктуре планирования задач.

См. следующие статьи, если вы не знакомы с пакетной службы Azure, он помогает обеспечивать понимание архитектуры и внедрению hello hello решения, описанные в этой статье hello.   

* [Основные сведения о пакетной службе Azure](../batch/batch-technical-overview.md)
* [Обзор функций пакетной службы](../batch/batch-api-basics.md)

(необязательно) toolearn Дополнительные сведения о пакетной службы Azure, в разделе hello [план обучения для пакетной службы Azure](https://azure.microsoft.com/documentation/learning-paths/batch/).

## <a name="why-azure-data-factory"></a>Сведения о фабрике данных Azure
Фабрика данных — службы интеграции облачных данных, которая координирует и автоматизирует процессы hello перемещения и преобразования данных. С помощью hello служба фабрики данных, можно создать управляемые данные конвейеры, перемещения данных из локальных и облачных данных сохраняет tooa централизованное хранилище данных (например: хранилища больших двоичных объектов) и процесс или преобразования данных с помощью служб, таких как Azure HDInsight и Azure Машинное обучение. Можно также планировать toorun конвейеры данных в мониторе и запланированных способом (ежечасно, ежедневно, еженедельно, т. д.) и управлять ими в tooidentify Обзор проблемы и предпринять действия.

См. следующие статьи, если вы не знакомы с фабрикой данных Azure, он помогает обеспечивать понимание архитектуры и внедрению hello hello решения, описанные в этой статье hello.  

* [Общие сведения о службе фабрики данных Azure](data-factory-introduction.md)
* [Построение конвейера данных](data-factory-build-your-first-pipeline.md)   

(необязательно) toolearn Дополнительные сведения о фабрики данных Azure, в разделе hello [план обучения для фабрики данных Azure](https://azure.microsoft.com/documentation/learning-paths/data-factory/).

## <a name="data-factory-and-batch-together"></a>Совместное использование фабрики данных и пакетной службы
Фабрика данных включает встроенные действия, такие как действие копирования toocopy или перемещения данных из источника данных хранить tooa целевое хранилище данных и данные tooprocess действие Hive, с использованием кластеров Hadoop (HDInsight) в Azure. Список поддерживаемых действий преобразования см. в [этой статье](data-factory-data-transformation-activities.md).

Также позволяет вам toocreate пользовательских действий .NET toomove или процесс данных с помощью собственной логики и выполните эти действия для кластера Azure HDInsight или пула виртуальных машин. При использовании пакета Azure можно настроить hello пула tooauto масштабирование (Добавление или удаление виртуальных машин на основе рабочей нагрузки hello) на основе формулы, указываемые.     

## <a name="architecture-of-sample-solution"></a>Архитектура примера решения
Несмотря на то, что архитектура hello, описанных в этой статье предназначен для простого решения, это применимо toocomplex сценариев, таких как рисков или моделирование финансовых служб, обработка изображений и подготовки к просмотру и генома анализа.

Hello диаграмме 1) как фабрика данных управляет перемещение данных и обработки и (2) как пакетной службы Azure обрабатывает hello данных параллельных способом. Загрузка и Здравствуй, мир схемы для простоты обращения (11 x 17 дюймов. или А3): [Управление данными и высокопроизводительными вычислениями с помощью пакетной службы и фабрики данных Azure](http://go.microsoft.com/fwlink/?LinkId=717686).

[![Схема обработки данных большого объема](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)

Hello ниже приведены основные этапы процесса hello hello. Hello решение включает в себя код и объяснения toobuild hello решения начала до конца.

1. **Настройка пула вычислительных узлов (виртуальные машины) для пакетной службы Azure**. Можно указать hello числом узлов и размер каждого узла.
2. **Создание экземпляра фабрики данных Azure** , для которого настраиваются сущности, представляющие хранилище BLOB-объектов, службу вычислений пакетной службы Azure, входные и выходные данные, а также рабочий процесс и конвейер с действиями, позволяющими перемещать и преобразовывать данные.
3. **Создание настраиваемого действия .NET в конвейере данных фабрики hello**. Действие Hello-пользовательского кода, выполняемого на hello пула.
4. **Сохранение больших объемов входных данных в виде больших двоичных объектов в службе хранилища Azure**. Данные при этом разделяются на логические срезы (обычно по времени).
5. **Фабрика данных копирует данные, которые обрабатываются параллельно** toohello вторичное расположение.
6. **Фабрики данных выполняется с помощью пула hello, выделенной с помощью пакета пользовательское действие hello**. Действия в фабрике данных могут выполняться параллельно. В каждом действии обрабатывается один срез данных. Hello результаты хранятся в хранилище Azure.
7. **Фабрика данных перемещает hello окончательные результаты tooa третье расположение**, либо для распространения приложения, либо для дальнейшей обработки другими средствами.

## <a name="implementation-of-sample-solution"></a>Реализация примера решения
Образец Hello решения намеренно простые и является tooshow вы как toouse фабрику данных и пакета вместе tooprocess наборов данных. решение Hello просто подсчитывает hello число вхождений условие поиска («Microsoft») во входных файлах, организованных во временных рядах. Он выводит файлы toooutput число hello.

**Время**: Если вы знакомы с основами Azure, фабрике данных и пакет и иметь завершенного hello предварительные требования, перечисленные ниже, по нашим оценкам, это решение принимает toocomplete 1 – 2 часов.

### <a name="prerequisites"></a>Предварительные требования
#### <a name="azure-subscription"></a>Подписка Azure.
Если у вас нет подписки Azure, то всего за несколько минут можно создать бесплатную пробную учетную запись. Узнайте больше о [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="azure-storage-account"></a>Учетная запись хранения Azure.
Использовать учетную запись хранилища Azure для хранения данных hello в этом учебнике. Если у вас нет учетной записи хранения Azure, ознакомьтесь с разделом [Создание учетной записи хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account). Образец Hello решения используется хранилище больших двоичных объектов.

#### <a name="azure-batch-account"></a>Учетная запись пакетной службы Azure
Создать учетную запись пакетной службы Azure с помощью hello [портал Azure](http://manage.windowsazure.com/). Ознакомьтесь со статьей [Создание учетной записи пакетной службы Azure и управление ею](../batch/batch-account-create-portal.md). Обратите внимание, hello пакетной службы Azure имя и ключ учетной записи учетную запись. Можно также использовать [New AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) toocreate командлет учетной записи пакетной службы Azure. Подробные инструкции по использованию этого командлета см. в статье [Приступая к работе с командлетами PowerShell пакетной службы Azure](../batch/batch-powershell-cmdlets-get-started.md).

Образец Hello решения использует данные tooprocess пакетной службы Azure (косвенно с помощью конвейера фабрики данных Azure) в виде параллельных в пуле вычислительных узлов (управляемой коллекции виртуальных машин).

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a>Пул виртуальных машин пакетной службы Azure
Создайте **пул пакетной службы Azure** с как минимум 2 вычислительными узлами.

1. В hello [портал Azure](https://portal.azure.com), нажмите кнопку **Обзор** в hello в левом меню и нажмите кнопку **учетные записи пакетного**.
2. Выберите ваш hello tooopen учетной записи пакетной службы Azure **пакетной учетной записи** колонку.
3. Щелкните элемент **Пулы** .
4. В hello **пулы** колонке нажмите кнопку Добавить на панель инструментов hello tooadd пул.
   1. Введите идентификатор пула hello (**идентификатор пула**). Примечание hello **идентификатор пула hello**; необходимо при создании решения hello фабрики данных.
   2. Укажите **Windows Server 2012 R2** для приветствия семейство операционных систем.
   3. Выберите **Ценовая категория для узлов**.
   4. Введите **2** как значение для hello **выделенной целевой** параметр.
   5. Введите **2** как значение для hello **Max задач на каждом узле** параметр.
   6. Нажмите кнопку **ОК** toocreate hello пула.

#### <a name="azure-storage-explorer"></a>обозреватель хранилищ Azure
[Azure Storage Explorer 6 (инструмент)](https://azurestorageexplorer.codeplex.com/) или [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (от ClumsyLeaf Software). Используйте эти средства для проверки и изменения данных hello в проектах хранилища Azure, включая hello журналы приложений, размещенных в облаке.

1. Создайте контейнер **mycontainer** с закрытым доступом (без анонимного доступа).
2. Если вы используете **CloudXplorer**, создавать папки и подпапки с hello следующие структуры:

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   `Inputfolder`и `outputfolder` — это папки верхнего уровня в `mycontainer`. Hello `inputfolder` содержит подпапки с метки даты и времени (гггг-мм-дд-ЧЧ).

   Если вы используете **обозреватель хранилищ Azure**, в следующем шаге hello необходимы tooupload файлы с именами: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` и т. д. Этот шаг автоматически создаются папки hello.
3. Создайте текстовый файл **файла file.txt** на компьютере с содержимым, которое содержит ключевое слово hello **Microsoft**. Например, test custom activity Microsoft test custom activity Microsoft.
4. Отправьте файл toohello hello, после ввода папок в хранилище больших двоичных объектов.

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   Если вы используете **обозреватель хранилищ Azure**, отправьте файл hello **файла file.txt** слишком**mycontainer**. Нажмите кнопку **копирования** на toocreate инструментов hello копию hello большого двоичного объекта. В hello **копирования BLOB-объекта** диалоговое окно, изменение hello **имя BLOB-объекта назначения** слишком`inputfolder/2015-11-16-00/file.txt`. Повторите этот шаг toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` и т. д. Это действие автоматически создает папки hello.
5. Создайте другой контейнер с именем: `customactivitycontainer`. Необходимо отправить контейнер toothis hello пользовательское действие ZIP-файла.

#### <a name="visual-studio"></a>Visual Studio
Установите Microsoft Visual Studio 2012 или более поздней версии toocreate hello пользовательского пакета действие toobe используется в hello решения фабрики данных.

### <a name="high-level-steps-toocreate-hello-solution"></a>Пошаговые инструкции по toocreate hello решения
1. Создание пользовательского действия, содержащего логику обработки данных hello.
2. Создайте фабрикой данных Azure, который использует пользовательское действие hello:

### <a name="create-hello-custom-activity"></a>Создание настраиваемого действия hello
Фабрика данных пользовательское действие Hello — основа hello в этом образце решения. Образец Hello решения использует пакетной службы Azure toorun hello пользовательского действия. В разделе [использовать настраиваемые действия в конвейере фабрики данных Azure](data-factory-use-custom-activities.md) для hello основные сведения toodevelop настраиваемые действия и использовать их в фабрике данных Azure конвейеров.

toocreate .NET пользовательского действия, которое можно использовать в конвейере фабрики данных Azure необходимо toocreate **библиотеки классов .NET** проекта с классом, который реализует **IDotNetActivity** интерфейса. У этого интерфейса только один метод — **Execute**. Вот hello сигнатура метода hello.

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

метод Hello имеет несколько ключевых компонентов, необходимо toounderstand.

* метод Hello принимает четыре параметра:

  1. **linkedServices** — Перечислимый список связанных служб, связывающих источники данных ввода вывода (например: хранилища больших двоичных объектов) toohello фабрики данных. В этом примере присутствует только одна связанная служба (служба хранилища Azure), которая используется для входных и выходных данных.
  2. **наборы данных**. это перечисляемый список наборов данных. Можно использовать этот параметр tooget hello расположения и схем, определенных путем наборов входных и выходных данных.
  3. **activity** — Этот параметр представляет hello текущей вычислений сущности - в этом случае пакетной службы Azure.
  4. **logger** — Hello средства ведения журнала позволяет создавать комментарии отладки поверхности, как «User» журнала для hello hello конвейера.
* метод Hello возвращает словарь, который может быть настраиваемых действий используется toochain друг с другом в будущем hello. Эта функция еще не реализован, чтобы возвращаемые пустой словарь из метода hello.

#### <a name="procedure-create-hello-custom-activity"></a>Процедура: Создание настраиваемого действия hello
1. Создайте проект библиотеки классов .NET в Visual Studio:

   1. Запустите **Visual Studio 2012,** /**Visual Studio 2013 или Visual Studio 2015**.
   2. Нажмите кнопку **файл**, слишком точки**New**и нажмите кнопку **проекта**.
   3. Разверните раздел **Шаблоны** и выберите **Visual C#\#**. В этом пошаговом руководстве используется C\#, но можно использовать любой .NET языка toodevelop hello пользовательского действия.
   4. Выберите **библиотеки классов** hello списке типов проекта на hello вправо.
   5. Введите **MyDotNetActivity** для hello **имя**.
   6. Выберите **C:\\ADF** для hello **расположение**. Создайте папку hello **ADF** , если он не существует.
   7. Нажмите кнопку **ОК** toocreate hello проекта.
2. Нажмите кнопку **средства**, слишком точки**диспетчера пакетов NuGet**и нажмите кнопку **консоль диспетчера пакетов**.
3. В hello **консоль диспетчера пакетов**, выполните следующие команды tooimport hello **Microsoft.Azure.Management.DataFactories**.

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. Импорт hello **хранилища Azure** пакета NuGet в проекте toohello. Этот пакет необходимо так, как использовать API-Интерфейс хранилища больших двоичных объектов hello в этом образце.

    ```powershell
    Install-Package Azure.Storage
    ```
5. Добавьте следующее hello **с помощью** директивы toohello исходный файл в проекте hello.

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. Изменение имени hello объекта hello **имен** слишком**MyDotNetActivityNS**.

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. Изменение имени hello класса hello слишком**MyDotNetActivity** и производными hello **IDotNetActivity** интерфейс, как показано ниже.

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. Реализуйте (Добавить) hello **Execute** метод hello **IDotNetActivity** интерфейс toohello **MyDotNetActivity** hello класса и скопируйте следующий образец кода toohello метода. В разделе hello [выполнить метод](#execute-method) чтобы пояснения для hello логику, используемую в этом методе.

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
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
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
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
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
9. Добавьте следующий вспомогательный класс toohello методы hello. Эти методы вызываются hello **Execute** метод. Здравствуйте, самое главное, **Calculate** метод изолирует hello код, выполняющий перебор элементов каждого большого двоичного объекта.

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
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
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
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
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
    Hello **GetFolderPath** метод возвращает папку toohello hello, hello tooand точки набора данных hello **GetFileName** метод возвращает имя hello hello большого двоичного объекта или файла, который hello указывает набор данных.

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    Hello **Calculate** метод вычисляет hello число экземпляров ключевое слово **Microsoft** во входных файлах hello (большие двоичные объекты в папке hello). условие поиска Hello («Microsoft») жестко закодирована в коде hello.

1. Скомпилируйте проект hello. Нажмите кнопку **построения** из hello меню и выберите пункт **построить решение**.
2. Запустите **Проводник**и перейдите в слишком**bin\\отладки** или **bin\\выпуска** папку, в зависимости от типа hello сборки.
3. Создать ZIP-файл **MyDotNetActivity.zip** , содержащий все двоичные файлы hello в hello  **\\bin\\отладки** папки. Вы можете tooinclude hello MyDotNetActivity. **pdb** так, чтобы получить дополнительные сведения, такие как номер строки в исходном коде hello, вызвавшего проблему hello, когда происходит сбой.

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. Отправка **MyDotNetActivity.zip** как контейнер больших двоичных объектов blob toohello: `customactivitycontainer` в hello Azure хранилище больших двоичных объектов, hello **StorageLinkedService** связанная служба в hello  **ADFTutorialDataFactory** использует. Создание контейнера больших двоичных объектов hello `customactivitycontainer` , если он еще не существует.

#### <a name="execute-method"></a>Метод Execute
Этот раздел содержит дополнительные сведения и заметки о hello код в метод Execute hello.

1. члены Hello для прохода по коллекции входных hello находятся в hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) пространства имен. Прохода по коллекции hello больших двоичных объектов, необходимо использовать hello **BlobContinuationToken** класса. По сути, необходимо использовать оператор do-во время цикла с маркером hello в качестве механизма hello для выхода из цикла hello. Дополнительные сведения см. в разделе [как toouse хранилища BLOB-объектов из .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Базовый цикл выглядит так:

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   См. в документации hello для hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) метод подробные сведения.
2. Hello для работы по hello набор больших двоичных объектов логически переходит в hello делать код-цикла while. В hello **Execute** метод, выполните hello-а цикл передает hello список больших двоичных объектов с именем метода tooa **Calculate**. метод Hello возвращает строковую переменную с именем **вывода** итерацию все большие двоичные объекты hello в сегменте hello, hello результат.

   Он возвращает hello число вхождений hello условие поиска (**Microsoft**) в большом двоичном объекте hello передан toohello **Calculate** метод.

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. Здравствуйте, один раз **Calculate** метод проделал рабочих hello, оно должно быть написано tooa новый большой двоичный объект. Поэтому для каждого набора больших двоичных объектов, обработанных новый большой двоичный объект может иметь с результатами hello. новый большой двоичный объект toowrite tooa, первый поиска hello выходной набор данных.

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. Привет код также вызывает вспомогательный метод: **GetFolderPath** путь к папке hello tooretrieve (имя контейнера хранилища hello).

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   Hello **GetFolderPath** приведения hello объекта DataSet tooan AzureBlobDataSet, который имеет свойство с именем FolderPath.

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. hello вызовы кода Hello **GetFileName** метод tooretrieve hello имя файла (blob). Код Hello-аналогичные toohello выше путь к папке hello tooget кода.

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. Имя файла hello Hello записывается, создав объект URI. конструктор URI Hello использует hello **BlobEndpoint** имя контейнера hello tooreturn свойства. путь и имя папки Hello добавляются tooconstruct hello вывода URI большого двоичного объекта.  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. будет записана Hello имя файла hello и теперь можно написать hello выходной строки из hello **Calculate** новый большой двоичный объект метод tooa:

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a>Создание фабрики данных hello
В hello [создать пользовательское действие hello](#create-the-custom-activity) вы создали настраиваемых действий и hello загруженный ZIP-файл с двоичные файлы и hello PDB файла tooan контейнера больших двоичных объектов. В этом разделе создайте Azure **фабрики данных** с **конвейера** , использующий hello **пользовательское действие**.

Здравствуйте входного набора данных для пользовательское действие hello представляет hello большие двоичные объекты (файлы) в папке входной hello (`mycontainer\\inputfolder`) в хранилище больших двоичных объектов. Hello выходной набор данных для hello действие представляет hello выходных данных BLOB-объектов в выходной папке hello (`mycontainer\\outputfolder`) в хранилище больших двоичных объектов.

Удалите один или несколько файлов в папках входной hello:

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

Например удалите один файл (file.txt) с hello, следуя содержимое в каждую из папки hello.

```
test custom activity Microsoft test custom activity Microsoft
```

Каждая папка входных данных соответствует tooa среза в фабрике данных Azure, даже если папка hello имеет 2 или более файлов. При обработке каждого среза конвейером hello пользовательское действие hello выполняет итерацию всех больших двоичных объектов hello в hello папка входных данных для этого среза.

Вы увидите, что пять выходных файлов с hello же содержимого. Например выходной файл hello не может обрабатывать файл hello в папке hello 2015-11-16-00 имеет hello после содержимого:

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

Если удалить несколько файлов (file.txt, file2.txt, file3.txt) с hello же toohello входной папки содержимого см. в разделе hello после содержимого в выходной файл для hello. Каждая папка (2015-11-16-00, т. д.) соответствует tooa среза в этом образце, даже если папка hello имеет несколько входных файлов.

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

Hello выходной файл имеет три строк, по одной на каждый входной файл (blob) в папке hello, связанные с hello среза (2015-11-16-00).

Такая задача создается для каждого запуска действия. В этом примере имеется только одно действие в конвейере hello. Если срез обрабатывается конвейером hello, пользовательское действие hello работает на срез hello tooprocess пакетной службы Azure. Так как имеется 5 срезов (каждому срезу может соответствовать несколько больших двоичных объектов или файлов), в пакетной службе Azure создано 5 задач. Это фактически hello настраиваемое действие, которое выполняется при запуске задачи в пакете.

Привет, пошаговое руководство содержит дополнительные сведения.

#### <a name="step-1-create-hello-data-factory"></a>Шаг 1: Создание фабрики данных hello
1. После входа в toohello [портал Azure](https://portal.azure.com/), hello следующие действия:

   1. Нажмите кнопку **NEW** hello левом меню.
   2. Нажмите кнопку **данные + аналитика** в hello **New** колонку.
   3. Нажмите кнопку **фабрики данных** на hello **анализа данных** колонку.
2. В hello **новую фабрику данных** колонке введите **CustomActivityFactory** для hello имя. Имя фабрики данных Azure hello Hello должно быть глобально уникальным. При получении ошибки hello: **имя фабрики данных «CustomActivityFactory» недоступен**, измените имя hello hello фабрики данных (например, **yournameCustomActivityFactory**) и попробуйте создать еще раз.
3. Щелкните **Имя группы ресурсов**, чтобы выбрать имеющуюся группу ресурсов, или создайте группу ресурсов.
4. Убедитесь, что вы используете hello правильные подписки и региона, место hello данных фабрики toobe создан.
5. Нажмите кнопку **создать** на hello **новую фабрику данных** колонку.
6. Вы видите hello фабрики данных, создаваемого в hello **мониторинга** из hello портал Azure.
7. После успешного создания фабрики данных hello, отображается страница фабрики данных hello, в котором отображается содержимое фабрики данных hello hello.

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a>Шаг 2. Создание связанных служб
Связанные службы связывание хранилищ данных или фабрики данных Azure tooan службы вычислений. На этом шаге связать ваш **хранилища Azure** учетной записи и **пакетной службы Azure** фабрики данных tooyour учетной записи.

#### <a name="create-azure-storage-linked-service"></a>Создание связанной службы хранения Azure
1. Щелкните hello **автор и развернуть** плитки приветствия **ФАБРИКИ данных** колонке **CustomActivityFactory**. Вы увидите hello редактор фабрики данных.
2. Нажмите кнопку **новое хранилище данных** hello панели команд и выберите **хранилища Azure.** Вы увидите hello скрипта JSON для создания хранилища Azure связанная служба в редакторе hello.

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. Замените **имя учетной записи** с именем hello вашей учетной записи хранилища Azure и **ключ учетной записи** с ключом доступа hello hello учетной записи хранилища Azure. toolearn tooget хранилищем доступом ключа, см. в разделе [ключи доступа Просмотр, копирование и повторное создание хранилища](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

4. Нажмите кнопку **развернуть** на панели toodeploy hello связаны службы hello команд.

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a>Создание связанной пакетной службы Azure
На этом шаге создания связанной службы для вашего **пакетной службы Azure** учетной записи, используемые toorun hello фабрики данных пользовательского действия.

1. Нажмите кнопку **новые вычислительные** hello панели команд и выберите **пакетной службы Azure.** Вы увидите hello скрипта JSON для создания пакета Azure связанная служба в редакторе hello.
2. В hello скрипта JSON:

   1. Замените **имя учетной записи** с именем hello учетной записи пакетной службы Azure.
   2. Замените **ключ доступа** с ключом доступа hello hello учетной записи пакетной службы.
   3. Введите идентификатор hello пула hello hello **poolName** свойства**.** Для этого свойства можно задать имя пула или идентификатор пула.
   4. Введите раздел hello URI для hello **batchUri** свойства JSON.

      > [!IMPORTANT]
      > Hello **URL-адрес** из hello **колонке учетной записи пакетной службы Azure** в hello следующий формат: \<accountname\>.\< область\>. batch.azure.com. Для hello **batchUri** свойство в hello JSON необходимо слишком**удалить «accountname».** с URL-адреса hello. Пример: `"batchUri": "https://eastus.batch.azure.com"`.
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      Для hello **poolName** свойства, можно также указать идентификатор hello пула hello вместо имени hello hello пула.

      > [!NOTE]
      > Hello служба фабрики данных не поддерживает параметр по требованию для пакетной службы Azure, как для HDInsight. Пул пакетной службы Azure можно использовать только в фабрике данных Azure.
      >
      >
   5. Укажите **StorageLinkedService** для hello **linkedServiceName** свойство. Эта связанная служба, созданный на предыдущем шаге hello. Это хранилище используется в качестве промежуточной области для файлов и журналов.
3. Нажмите кнопку **развернуть** на панели toodeploy hello связаны службы hello команд.

#### <a name="step-3-create-datasets"></a>Шаг 3. Создание наборов данных
На этом шаге создания наборов данных toorepresent входных и выходных данных.

#### <a name="create-input-dataset"></a>Создание входного набора данных
1. В hello **редактор** hello фабрики данных, щелкните **новый набор данных** кнопки на панели инструментов hello и щелкните **хранилища больших двоичных объектов Azure** hello раскрывающегося меню.
2. Замените hello JSON в правой области hello hello, следующий фрагмент JSON:

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
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

    Позже в этом пошаговом руководстве вы создадите конвейер со временем начала 2015-11-16T00:00:00Z и временем окончания 2015-11-16T05:00:00Z. Это данные, запланированных tooproduce **каждый час**, поэтому 5 срезов ввода вывода (между **00**: 00:00 -\> **05**: 00:00).

    Hello **частоты** и **интервал** для hello входного набора данных задается слишком**час** и **1**, что означает, что hello ввода фрагмент доступен Каждый час.

    Ниже приведены временем начала hello для каждого сегмента, представленными в **SliceStart** системной переменной в hello выше фрагменте кода JSON.

    | **Срез** | **Время начала**          |
    |-----------|-------------------------|
    | 1         | 2015-11-16T**00**:00:00 |
    | 2         | 2015-11-16T**01**:00:00 |
    | 3         | 2015-11-16T**02**:00:00 |
    | 4.         | 2015-11-16T**03**:00:00 |
    | 5         | 2015-11-16T**04**:00:00 |

    Hello **folderPath** вычисляется с помощью hello года, месяца, дня и часа часть время начала среза hello (**SliceStart**). Таким образом Вот как папка входных данных — сопоставленных tooa срез.

    | **Срез** | **Время начала**          | **Входная папка**  |
    |-----------|-------------------------|-------------------|
    | 1         | 2015-11-16T**00**:00:00 | 2015-11-16-**00** |
    | 2         | 2015-11-16T**01**:00:00 | 2015-11-16-**01** |
    | 3         | 2015-11-16T**02**:00:00 | 2015-11-16-**02** |
    | 4.         | 2015-11-16T**03**:00:00 | 2015-11-16-**03** |
    | 5         | 2015-11-16T**04**:00:00 | 2015-11-16-**04** |

1. Нажмите кнопку **развернуть** hello toocreate инструментов и развернуть hello **InputDataset** таблицы.

#### <a name="create-output-dataset"></a>Создание выходного набора данных
На этом шаге создается другой набор данных типа AzureBlob toorepresent hello выходных данных.

1. В hello **редактор** hello фабрики данных, щелкните **новый набор данных** кнопки на панели инструментов hello и щелкните **хранилища больших двоичных объектов Azure** hello раскрывающегося меню.
2. Замените hello JSON в правой области hello hello, следующий фрагмент JSON:

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
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

    Для каждого входного среза данных создается выходной большой двоичный объект или файл. Ниже в таблице приведены имена, которые даются выходным файлам для каждого среза. Все hello выходные файлы создаются в одной папке выходных данных: `mycontainer\\outputfolder`.

    | **Срез** | **Время начала**          | **Выходной файл**       |
    |-----------|-------------------------|-----------------------|
    | 1         | 2015-11-16T**00**:00:00 | 2015-11-16-**00.txt** |
    | 2         | 2015-11-16T**01**:00:00 | 2015-11-16-**01.txt** |
    | 3         | 2015-11-16T**02**:00:00 | 2015-11-16-**02.txt** |
    | 4.         | 2015-11-16T**03**:00:00 | 2015-11-16-**03.txt** |
    | 5         | 2015-11-16T**04**:00:00 | 2015-11-16-**04.txt** |

    Помните, что все hello файлы в папке ввода (например: 2015-11-16-00) являются частью фрагмента с временем начала hello: 2015-11-16-00. При обработке этого среза пользовательское действие hello просматривает каждый файл и создает строку в выходной файл hello с hello число вхождений условие поиска («Microsoft»). Если имеется три файла в папке hello 2015-11-16-00, существует три строки в выходной файл для hello: 2015-11-16-00.txt.

1. Нажмите кнопку **развернуть** hello toocreate инструментов и развернуть hello **OutputDataset**.

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a>Шаг 4: Создание и запуск конвейера hello с помощью настраиваемых действий
На этом шаге создания конвейера от одного действия, пользовательское действие hello, созданную ранее.

> [!IMPORTANT]
> Если вы еще не загрузили hello **файла file.txt** tooinput папки в контейнер больших двоичных объектов hello, сделать это перед созданием конвейера hello. Hello **isPaused** свойству toofalse hello конвейера JSON, поэтому конвейера hello немедленно выполняется как hello **запустить** дата находится в прошлом hello.
>
>

1. В hello редактор фабрики данных, нажмите кнопку **новый конвейер** на панели команд hello. Если команда hello не отображается, нажмите кнопку **... (Многоточие)**  toosee его.
2. Замените hello JSON в правой области hello hello следующий скрипт JSON:

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   Обратите внимание hello после точки.

   * Имеется только одно действие в конвейере hello и типа: **DotNetActivity**.
   * **AssemblyName** задано имя toohello hello DLL: **MyDotNetActivity.dll**.
   * **EntryPoint** задано слишком**MyDotNetActivityNS.MyDotNetActivity**. По сути, это фрагмент кода \<пространство_имен\>.\<имя_класса\>.
   * **PackageLinkedService** задано слишком**StorageLinkedService** , который указывает хранилище больших двоичных объектов toohello, содержащий ZIP-файл пользовательское действие hello. При использовании различных учетных записей хранилища Azure для файлов ввода вывода и ZIP-файл пользовательское действие hello, у вас есть toocreate другого хранилища Azure связанной службы. В этой статье предполагается, что вы используете hello учетную запись хранилища Azure.
   * **PackageFile** задано слишком**customactivitycontainer/MyDotNetActivity.zip**. Он имеет формат hello: \<containerforthezip\>/\<nameofthezip.zip\>.
   * пользовательское действие Hello принимает **InputDataset** в качестве входного и **OutputDataset** в качестве выходных данных.
   * Hello **linkedServiceName** свойство пользовательское действие hello указывает toohello **AzureBatchLinkedService**, который сообщает фабрики данных Azure, пользовательское действие hello должен toorun на пакетной службы Azure.
   * Hello **параллелизма** параметр важен. При использовании значения по умолчанию hello, равное 1, даже если у вас есть 2 или вычислительные узлы в пуле пакетной службы Azure hello, срезы hello обрабатываются одна за другой. Таким образом вы не пользуетесь преимуществами возможности параллельной обработки hello пакетной службы Azure. Если задать **параллелизма** tooa чем выше значение, например 2, это означает, что срезы (соответствует tootwo задач в пакетной службы Azure) могут одновременно обрабатываться в hello же время, в этом случае обе виртуальные машины hello в hello пула используются пакетной службы Azure. Таким образом свойства hello параллелизма соответствующим образом.
   * По умолчанию на виртуальной машине в любой момент времени будет выполняться только одна задача (один срез). Hello причина том, что по умолчанию hello **максимально задачи на виртуальную Машину** задано too1 для пула пакетной службы Azure. В рамках предварительных требований, созданный пул с этой too2 набор свойств, двумя фрагменты фабрики данных может выполняться на виртуальной Машине в hello то же время.

    -   **isPaused** свойству toofalse по умолчанию. конвейер Hello немедленно выполняется в этом примере, поскольку запуска среза hello в прошлом hello. Можно задать это свойство tootrue toopause hello конвейера и задайте для него toorestart toofalse назад.

    -   Hello **запустить** время и **окончания** значения времени приведены пять часов друг от друга и фрагменты создаются каждый час, поэтому пять фрагменты, созданные с помощью конвейера hello.

1. Нажмите кнопку **развернуть** на панели toodeploy hello конвейера hello команд.

#### <a name="step-5-test-hello-pipeline"></a>Шаг 5: Тестирование hello конвейера
На этом шаге теста hello конвейера путем перемещения файлов в папки входной hello. Начнем с конвейером тестирования hello с одного файла в одну папку ввода.

1. В колонке фабрики данных hello в hello портала Azure щелкните **схема**.

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. В представлении диаграммы hello, дважды щелкните набор входных данных: **InputDataset**.

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. Вы увидите hello **InputDataset** колонка с все пять срезы готова. Обратите внимание hello **время НАЧАЛА СРЕЗА** и **время окончания СРЕЗА** для каждого среза.

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. В hello **представление диаграммы**, нажмите кнопку **OutputDataset**.
5. Вы увидите, hello пять срезы выходных данных находятся в состоянии готовности hello, если они уже были созданы.

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. Используйте Azure портала tooview hello **задачи** связанные с hello **фрагменты** и увидеть, какие виртуальной Машины выполнялось каждый фрагмент. Дополнительные сведения см. в разделе [Интеграция фабрики данных и пакетной службы](#data-factory-and-batch-integration).
7. Вы увидите выходные файлы hello в hello `outputfolder` из `mycontainer` в Azure хранилище больших двоичных объектов.

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   Должно появиться пять выходных файлов, по одному на каждый входной срез. Каждый из hello выходной файл должен иметь содержимого аналогичные toohello следующие выходные данные:

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   Hello следующей схеме показано сопоставление tootasks в пакете Azure фрагменты hello фабрики данных. В этом примере срез запускался всего один раз.

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. Теперь давайте попробуем использовать несколько файлов в папке. Создание файлов: **file2.txt**, **file3.txt**, **file4.txt**, и **file5.txt** с hello же содержимого, как и file.txt в папке hello: **2015-11-06-01**.
9. В выходной папке hello **удаление** hello выходной файл: **2015-11-16-01.txt**.
10. Теперь в hello **OutputDataset** колонка, щелкните правой кнопкой мыши срез hello с **время НАЧАЛА СРЕЗА** значение слишком**11/16/2015 01:00:00 AM**и нажмите кнопку **запуска**toorerun или повторно-process hello среза. Теперь hello фрагмент содержит пять файлов вместо одного файла.

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. После запуска среза hello и она находится в состоянии **готовности**, проверьте содержимое hello в hello выходной файл для этого среза (**2015-11-16-01.txt**) в hello `outputfolder` из `mycontainer` в хранилище BLOB-объектов. Строку для каждого файла фрагмента hello следует.

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> Если не был удален hello выходной файл 2015-11-16-01.txt перед попыткой с пять входных файлов, можно увидеть, одну строку от предыдущего фрагмента hello запуска и пять строк из текущего среза hello запуска. По умолчанию hello содержимого — присоединенных toooutput файл, если он уже существует.
>
>

#### <a name="data-factory-and-batch-integration"></a>Интеграция фабрики данных и пакетной службы
Служба фабрики данных Hello создает задание в пакетной службы Azure с именем hello: `adf-poolname:job-xxx`.

![Фабрика данных Azure — задания пакетной службы](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

Задачи в задании hello создается для каждого фрагмента запуска действия. При наличии 10 готов toobe фрагменты обработки, 10 задачи создаются в задании hello. Может иметь более одного фрагмента выполняется параллельно, если имеется несколько вычислительных узлов в пуле hello. Если максимальное число задач hello в вычислений слишком набор узлов > 1, может быть больше, чем один срез, работающих на hello же вычислений.

В этом примере имеется пять срезов, что соответствует пяти задачам в пакетной службе Azure. С hello **параллелизма** значение слишком**5** в hello конвейера JSON в фабрике данных Azure и **максимально задачи на виртуальную Машину** значение слишком**2** в пакете Azure пул с **2** ВМ, hello задачи выполняется быстро (проверьте время начала и окончания для задач).

Используйте hello портала tooview hello пакетного задания и его задачи, связанные с hello **фрагменты** и увидеть, какие виртуальной Машины выполнялось каждый фрагмент.

![Фабрика данных Azure — задачи задания пакетной службы](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a>Отладка hello конвейера
Отладка состоит из нескольких базовых методов:

1. Если входной срез hello не задано слишком**готовности**, убедитесь, что папка входных данных структуры hello указано правильно и file.txt существует в папках входной hello.

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. В hello **Execute** метод настраиваемого действия, используйте hello **IActivityLogger** toolog сведения об объекте, которая позволяет выполнять устранение неполадок. Hello в журнал сообщения отображаются в hello пользователя\_0. файла журнала.

   В hello **OutputDataset** колонка, щелкните hello срез toosee hello **СРЕЗ данных** колонку для этого среза. Для этого среза будет указано значение **Запуски операции** . Должна появиться при выполнении среза hello одного действия. Если щелкнуть **запуска** hello панели команд, вы можете запустить другое действие запуска для hello того же фрагмента.

   При нажатии кнопки при выполнении действия hello, вы видите hello **сведения о выполнении действия** колонка со списком файлов журнала. Вы видите сообщения в журнале в hello **пользователя\_журнала 0.** файла. При возникновении ошибки, так как число повторных попыток hello задано too3 hello конвейера или действия JSON см запуске три действия. При нажатии кнопки при выполнении действия hello, вы видите что tootroubleshoot hello ошибки можно просмотреть файлы журнала hello.

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   В списке hello файлов журнала щелкните hello **0.log пользователя**. В правой панели hello являются hello результатов с помощью hello **IActivityLogger.Write** метод.

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   Проверьте файл system-0.log на наличие любых системных сообщений об ошибках или исключений.

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. Включить hello **PDB** файлов в ZIP-файле hello таким образом, что сведения об ошибке hello сведения например **стека вызовов** при возникновении ошибки.
4. Все файлы в ZIP-файле hello hello, пользовательское действие hello должен быть в hello **верхнего уровня** с без вложенных папок.

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. Убедитесь, что hello **assemblyName** (MyDotNetActivity.dll) **entryPoint** (MyDotNetActivityNS.MyDotNetActivity) **packageFile** (customactivitycontainer / MyDotNetActivity.zip) и **packageLinkedService** (следует точка toohello Azure хранилище больших двоичных объектов, содержащий hello ZIP-файл) значения toocorrect.
6. Исправления ошибок и хотите hello срез tooreprocess щелкните правой кнопкой мыши срез hello в hello **OutputDataset** колонку и нажмите кнопку **запуска**.

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > В хранилище BLOB-объектов Azure появится **контейнер** с именем `adfjobs`. Этот контейнер не удаляется автоматически, но ее можно безопасно удалить после завершения тестирования решения hello. Аналогичным образом hello решения фабрики данных создает пакет Azure **задания** с именем: `adf-\<pool ID/name\>:job-0000000001`. После выполнения тестов hello решение при необходимости можно удалить это задание.
   >
   >
7. пользовательское действие Hello не использует hello **app.config** файл из пакета. Таким образом Если код считывает все строки подключения из файла конфигурации hello, он не работает во время выполнения. Здравствуйте, рекомендуется при использовании пакета Azure, toohold все секреты в **Azure KeyVault**, используйте keyvault hello tooprotect участника службы на основе сертификатов и распространять hello пула tooAzure сертификат. Здравствуйте настраиваемых действий .NET, то можно получить доступ к секретные данные из hello KeyVault во время выполнения. Это решение универсальные и масштабируется tooany тип секретного кода, а не только строку подключения.

    Отсутствует простой обходной путь (но не рекомендуется): можно создать **связанная служба Azure SQL** параметры строки соединения, создать набор данных, использует hello связанной службы и цепочки hello dataset в виде пустой входного набора данных toohello настраиваемых действий .NET. После этого можно доступа hello связаны строки подключения службы в коде пользовательское действие hello и он должен корректно работать во время выполнения.  

#### <a name="extend-hello-sample"></a>Расширение образца hello
Можно расширить этот пример toolearn Дополнительные сведения о функции фабрики данных Azure и пакета Azure. Например срезы tooprocess в другой диапазон дат, hello следующие шаги:

1. Добавьте следующие вложенные папки в hello hello `inputfolder`: 2015-11-16-05 2015-11-16-06 201-11-16-07, 2011-11-16-08, 2015-11-16-09 и поместите входные файлы в этих папках. Изменить hello время окончания для конвейера hello из `2015-11-16T05:00:00Z` слишком`2015-11-16T10:00:00Z`. В hello **представление диаграммы**, дважды щелкните hello **InputDataset**и убедитесь, что готовы входные срезы hello. Дважды щелкните **OuptutDataset** toosee состояние hello срезы выходных данных. Если они находятся в состоянии готовности, проверьте папку вывода hello hello выходные файлы.
2. Увеличение или уменьшение hello **параллелизма** параметр toounderstand о том, как она влияет на производительность hello решения, особенно hello обработки, которое происходит в пакетной службы Azure. (См. шаг 4: Создание и запуск конвейера hello для получения дополнительных сведений об hello **параллелизма** параметр.)
3. Создайте пул с большим или меньшим значением для параметра **Maximum tasks per VM** (Максимальное число задач на виртуальную машину). toouse hello новый созданный пул, hello обновления связанной пакетной службы Azure в решении hello фабрики данных. (См. шаг 4: Создание и запуск конвейера hello для получения дополнительных сведений об hello **максимально задачи на виртуальную Машину** параметр.)
4. Создайте пул пакетной службы Azure с использованием функции **автомасштабирования** . Автоматическое масштабирование вычислительных узлов в пуле пакетной службы Azure — hello динамическую настройку вычислительной мощности, используемую приложением. 

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
5. В решении образец hello hello **Execute** метод вызывает hello **Calculate** метода, который обрабатывает входные данные срез tooproduce срез данных выходные данные. Можно написать собственный метод tooprocess входные данные и замените вызов метода Calculate hello в методе Execute hello tooyour вызова метода.

### <a name="next-steps-consume-hello-data"></a>Дальнейшие действия: использовать данные hello
После обработки данных их можно использовать в интерактивных инструментах, например в **Microsoft Power BI**. Ниже приведены ссылки toohelp понять Power BI и как toouse его в Azure:

* [Изучение набора данных в Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [Приступая к работе с Power BI Desktop hello](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [Обновление данных в Power BI](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [Общая информация об Azure и Power BI](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a>Ссылки
* [Фабрика данных Azure](https://azure.microsoft.com/documentation/services/data-factory/)

  * [Введение tooAzure служба фабрики данных](data-factory-introduction.md)
  * [Начало работы с фабрикой данных Azure](data-factory-build-your-first-pipeline.md)
  * [Использование настраиваемых действий в конвейере фабрики данных Azure](data-factory-use-custom-activities.md)
* [Пакетная служба Azure](https://azure.microsoft.com/documentation/services/batch/)

  * [Основные сведения о пакетной службе Azure](../batch/batch-technical-overview.md)
  * [Обзор функций пакетной службы Azure](../batch/batch-api-basics.md)
  * [Создание и управление учетной записью пакетной службы Azure в hello портал Azure](../batch/batch-account-create-portal.md)
  * [Начало работы с библиотекой Пакетной службы Azure для .NET](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
