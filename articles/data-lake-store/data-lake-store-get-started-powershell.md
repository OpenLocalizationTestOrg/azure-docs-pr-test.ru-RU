---
title: "aaaUse PowerShell tooget к выполнению хранилища Озера данных Azure | Документы Microsoft"
description: "Использование Azure PowerShell toocreate учетной записи хранилища Озера данных и выполнения основных операций"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 9c958bfd63e412ec0b0a4113a149f61aee026bc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a>Начало работы с хранилищем озера данных Azure с помощью Azure PowerShell
> [!div class="op_single_selector"]
> * [Портал](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [Пакет SDK для .NET](data-lake-store-get-started-net-sdk.md)
> * [Пакет SDK для Java](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Узнайте, как toocreate toouse Azure PowerShell Azure Озера данных хранения учетной записи и выполнения основных операций, таких как создание папками, отправка и загрузка файлов данных, удалите учетную запись, и т. д. Дополнительные сведения о хранилище озера данных см. в [обзоре Data Lake Store](data-lake-store-overview.md).

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать работу с учебником, необходимо иметь следующие hello.

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 или более поздней версии**. В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

## <a name="authentication"></a>Аутентификация
В этой статье используется более простой подход проверки подлинности с помощью которых вы являетесь запрашиваемые tooenter хранилища Озера данных учетные данные учетной записи Azure. Hello доступ уровня хранилища Озера tooData учетной записи и файловая система распространяется уровень доступа hello приветствия вошедшего пользователя. Однако существуют другие методы как хорошо tooauthenticate с хранилища Озера данных, которые являются **проверки подлинности для конечных пользователей** или **проверки подлинности службы для службы**. Инструкции и Дополнительные сведения о том, как tooauthenticate, в разделе [проверки подлинности для конечных пользователей](data-lake-store-end-user-authenticate-using-active-directory.md) или [проверки подлинности службы для службы](data-lake-store-authenticate-using-active-directory.md).

## <a name="create-an-azure-data-lake-store-account"></a>Создание учетной записи хранения озера данных Azure
1. С рабочего стола откройте новое окно Windows PowerShell и введите hello, следующий фрагмент toolog в tooyour учетная запись Azure, задайте hello подписки и регистрации поставщика хранилища Озера данных hello. При toolog запрос, убедитесь, что войти в систему один hello admininistrators/владелец подписки:

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. Учетная запись хранения озера данных Azure связывается с группой ресурсов Azure. Для начала создайте группу ресурсов Azure.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    ![Создание группы ресурсов Azure](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Создание группы ресурсов Azure")
3. Создайте учетную запись хранения озера данных Azure. Hello имя должно содержать только строчные буквы и цифры.

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    ![Создание учетной записи Azure Data Lake Store](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Создание учетной записи Azure Data Lake Store")
4. Убедитесь, что учетная запись hello успешно создан.

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    выходные данные для этого необходимо использовать Hello **True**.

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a>Создание структуры каталогов в хранилище озера данных Azure
Можно создать каталоги под вашей toomanage учетной записи хранилища Озера данных Azure и хранения данных.

1. Укажите корневой каталог.

        $myrootdir = "/"
2. Создайте новую папку с именем **mynewdirectory** в корне указанного hello.

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. Убедитесь, что в этом новом каталоге hello успешно создан.

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    Должна отобразиться выход hello следующим образом:

    ![Проверка каталога](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Проверка каталога")

## <a name="upload-data-tooyour-azure-data-lake-store"></a>Отправка хранилища Озера данных Azure tooyour данных
Можно передать в хранилище Озера данных tooData непосредственно на hello корневого уровня или tooa каталог, созданный в пределах учетной записи hello. фрагменты кода Hello ниже показано, как tooupload некоторые каталог образцов данных toohello (**mynewdirectory**) был создан в предыдущем разделе hello.

Если вы ищете некоторые tooupload образец данных, вы можете получить hello **скорая помощь данных** папку из hello [репозитории Озера данных Azure](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData). Загрузите файл hello и сохранить его в локальный каталог на компьютере, например C:\sampledata\.

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a>Переименование, загрузка и удаление данных из хранилища озера данных
toorename файл hello используйте следующую команду:

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

toodownload файл hello используйте следующую команду:

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

toodelete файл hello используйте следующую команду:

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

При появлении запроса введите **Y** toodelete hello элемента. При наличии более одного файла toodelete, чтобы обеспечить всех hello путей, разделенных точкой с запятой.

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a>Удаление учетной записи хранения озера данных Azure
Используйте следующие команды toodelete hello вашей учетной записи хранилища Озера данных.

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

При появлении запроса введите **Y** учетной записи toodelete hello.

## <a name="performance-guidance-while-using-powershell"></a>Рекомендации по производительности при использовании PowerShell

Ниже приведены наиболее важные параметры, которые могут быть настроенном tooget hello наилучшей производительности при работе с PowerShell toowork с хранилищем данных Озера hello.

| Свойство            | значение по умолчанию | Описание |
|---------------------|---------|-------------|
| PerFileThreadCount  | 10      | Этот параметр включает toochoose hello число параллельных потоков для отправки или загрузки каждого файла. Это число представляет hello максимального количества потоков, которые могут быть распределены на файл, но можно получить меньше потоков в зависимости от вашего сценария (например при отправке файла 1 КБ, вы получите один поток, даже если вы запрашиваете 20 потоков).  |
| ConcurrentFileCount | 10      | Этот параметр предназначен для отправки или скачивания папок. Этот параметр определяет количество одновременных файлы, которые передаются или загружаются в hello. Это число представляет hello максимальное число одновременных файлы, которые можно передать или загрузить за один раз, но можно получить меньше параллелизма в зависимости от вашего сценария (например при отправке два файла, вы получите два передачи файлов, даже при обращении за 15). |

**Пример**

Эта команда загружает файлы с локального диска toohello пользователь хранилища Озера данных Azure с помощью 20 потоков на файл и 100 одновременных файлов.

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-hello-value-tooset-for-these-parameters"></a>Как определить hello tooset значения для этих параметров?

Ниже представлены некоторые полезные рекомендации.

* **Шаг 1: Определение количества общий поток hello** -следует начать с toouse число поток общее расчет hello. Как правило, следует использовать 6 потоков для каждого физического ядра.

        Total thread count = total physical cores * 6

    **Пример**

    При условии, что вы используете hello PowerShell команды из виртуальной Машины D14 имеет 16 ядер

        Total thread count = 16 cores * 6 = 96 threads


* **Шаг 2: Вычисление PerFileThreadCount** -вычислять наших PerFileThreadCount, в зависимости от размера файлов hello hello. Для файлов размером менее 2,5 ГБ нет toochange нет необходимости этот параметр, так как по умолчанию hello 10 достаточно. Для файлов больше 2,5 ГБ 10 потоков следует использовать как hello базы для hello первые 2,5 ГБ и добавьте одному потоку для каждой дополнительной увеличение 256 МБ размера файла. При копировании папки с файлами разного размера рекомендуется разделить их на группы по схожим размерам. Использование файлов разных размеров может привести к снижению производительности. Если это возможно toogroup сходные размеры файлов, необходимо задать PerFileThreadCount основании hello максимальный размер файла.

        PerFileThreadCount = 10 threads for hello first 2.5GB + 1 thread for each additional 256MB increase in file size

    **Пример**

    Предположим, что у вас есть 100 файлов в диапазоне от 1 ГБ too10GB, мы используем hello 10 ГБ, как hello наибольший размер формула, которая будет читаться hello следующим образом файла.

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* **Шаг 3: Вычисление ConcurrentFilecount** -поток общее число использований hello и PerFileThreadCount toocalculate ConcurrentFileCount с учетом hello, следующая формула.

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    **Пример**

    На основе значений пример hello, мы использовали

        96 = 40 * ConcurrentFileCount

    Таким образом **ConcurrentFileCount** — **2.4**, который мы можно округлить слишком**2**.

### <a name="further-tuning"></a>Дополнительные настройки

Могут потребоваться дополнительные настройки из-за диапазон toowork размеры файлов с. Hello выше вычисления работает также в том случае, если все или большинство файлов hello являются более крупными и подробный toohello диапазон 10 ГБ. Однако если у вас есть множество файлов разных размеров (меньше 10 ГБ), можно уменьшить значение параметра PerFileThreadCount. Уменьшая hello PerFileThreadCount, мы увеличим ConcurrentFileCount. Таким образом Если предполагается, что большая часть наших файлов меньшего размера, в диапазоне hello 5 ГБ, мы можем повторно выполните наших вычислений:

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

Таким образом **ConcurrentFileCount** будет теперь 96/20, являющийся 4.8 округлено слишком**4**.

Вы можете продолжить tootune эти параметры, изменение hello **PerFileThreadCount** вверх и вниз в зависимости от распределения hello размер файлов.

### <a name="limitation"></a>Ограничение

* **Количество файлов меньше, чем ConcurrentFileCount**: Если hello число файлов, которые вы отправляете меньше hello **ConcurrentFileCount** , вычисленную, то следует уменьшить  **ConcurrentFileCount** toobe равно toohello число файлов. Можно использовать все остальные потоки tooincrease **PerFileThreadCount**.

* **Слишком много потоков**: Если увеличить поток слишком большого объема без увеличения размер кластера, запустите hello риск снижение производительности. При переключении контекста на hello ЦП может быть конфликтным.

* **Недостаточно параллелизма**: Если параллелизма hello недостаточно, то кластера может быть слишком мал. Можно увеличить hello количество узлов в кластере, в которых можно получить дополнительные параллелизма.

* **Ошибки регулирования.** При слишком высоком уровне параллелизма могут возникнуть ошибки регулирования. Если вы видите ошибки регулирования, следует уменьшению параллелизма hello или свяжитесь с нами.

## <a name="next-steps"></a>Дальнейшие действия
* [Защита данных в хранилище озера данных](data-lake-store-secure-data.md)
* [Использование аналитики озера данных Azure с хранилищем озера данных](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Использование Azure HDInsight с хранилищем озера данных](data-lake-store-hdinsight-hadoop-use-portal.md)

