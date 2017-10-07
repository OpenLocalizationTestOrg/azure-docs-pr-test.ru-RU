---
title: "aaaGet к выполнению аналитики Озера данных Azure, с помощью Azure CLI 2.0 | Документы Microsoft"
description: "Узнайте, как создать задание аналитики Озера данных с помощью U-SQL toocreate hello интерфейс командной строки Azure 2.0 toouse учетную запись аналитики Озера данных и отправить задание hello. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: jgao
ms.openlocfilehash: c4e91c0d3526e4932c2948c0a326d4cedc985791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a>Начало работы с Azure Data Lake Analytics при помощи Azure CLI 2.0
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

В этом руководстве вам предстоит разработать задание, которое считывает файл с разделителями-табуляциями (TSV) и преобразует его в файл с разделителями-запятыми (CSV). toogo через hello поддерживается же учебника при помощи других средств, используйте hello раскрывающегося списка в верхней части hello этого раздела.

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать работу с учебником, необходимо иметь hello следующих элементов:

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Azure CLI 2.0**. См. статью [Установка и настройка интерфейса командной строки Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="log-in-tooazure"></a>Войдите в tooAzure

toolog в tooyour подписки Azure:

```
azurecli
az login
```

Запрошенный toobrowse tooa URL-адрес и введите код проверки подлинности.  И следуйте инструкциям tooenter hello учетные данные.

После входа hello входа команда перечисляет подписки.

toouse конкретной подписки:

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a>Создание учетной записи аналитики озера данных
Для выполнения любых заданий требуется учетная запись Data Lake Analytics. toocreate учетную запись аналитики Озера данных, необходимо указать hello следующих элементов:

* **Группа ресурсов Azure**. В группе ресурсов Azure необходимо создать учетную запись Data Lake Analytics. [Диспетчер ресурсов Azure](../azure-resource-manager/resource-group-overview.md) позволяет toowork с ресурсами hello в приложении в качестве группы. Можно развернуть, обновить или удалить все ресурсы hello для вашего приложения, в один, согласованной операции.  

toolist hello групп ресурсов в подписке:

```
az group list
```

toocreate новая группа ресурсов:

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* **Имя учетной записи Data Lake Analytics**. Каждой учетной записи Data Lake Analytics присвоено имя.
* **Расположение.** Используйте одну из hello центрах обработки данных Azure, которые поддерживает аналитики Озера данных.
* **Учетная запись Data Lake Store по умолчанию** — каждая учетная запись Data Lake Analytics содержит учетную запись Data Lake Store по умолчанию.

toolist hello хранилища Озера данных учетная запись:

```
az dls account list
```

toocreate новую учетную запись хранилища Озера данных:

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

Используйте следующий синтаксис toocreate учетную запись аналитики Озера данных hello.

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

После создания учетной записи, можно использовать следующие учетные записи hello toolist команды hello и Показать сведения об учетной записи:

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a>Отправка хранилища Озера данных tooData
В этом руководстве обрабатываются некоторые журналы поиска.  Hello поиска журнала могут храниться в хранилище Озера данных или хранилище BLOB-объектов Azure.

Hello портал Azure предоставляет пользовательский интерфейс для копирования некоторые образец данных файлов toohello по умолчанию хранилище Озера данных учетной записи, которая содержит поиск файла журнала. В разделе [Подготовка данных источника](data-lake-analytics-get-started-portal.md) tooupload hello данных toohello по умолчанию хранилище Озера данных учетной записи.

tooupload файлов с помощью CLI версии 2.0, hello используйте следующие команды:

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

Из аналитики озера данных также доступно хранилище больших двоичных объектов Azure.  Для передачи больших двоичных объектов хранилища данных tooAzure, см. [использование hello Azure CLI со службой хранилища Azure](../storage/common/storage-azure-cli.md).

## <a name="submit-data-lake-analytics-jobs"></a>Отправка заданий аналитики озера данных
Аналитика Озера данных заданий Hello записываются в hello языка U-SQL. toolearn Дополнительные сведения о U-SQL, в разделе [приступить к работе с языком U SQL](data-lake-analytics-u-sql-get-started.md) и [eence U-SQL языка](http://go.microsoft.com/fwlink/?LinkId=691348).

**toocreate сценарий задания аналитики Озера данных**

Создайте текстовый файл с следующий скрипт U-SQL и сохраните текстовый файл hello tooyour-рабочей станции:

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

Этот скрипт U-SQL считывает hello источник данных файла с помощью **Extractors.Tsv()**, а затем создает файл csv с помощью **Outputters.Csv()**.

Не изменяйте hello два пути, если скопировать hello исходный файл в другое расположение.  Аналитика Озера данных создает hello выходную папку, если он не существует.

Это проще toouse относительных путей для файлов, хранящихся в учетных записях хранилища Озера данных по умолчанию. Также можно использовать абсолютные пути.  Например:

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

Необходимо использовать абсолютные пути файлов tooaccess в связанные учетные записи хранения.  Hello для файлов, хранящихся в связанной учетной записи хранилища Azure используется синтаксис:

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> Контейнер больших двоичных объектов Azure с общедоступными большими двоичными объектами не поддерживается.      
> Контейнер больших двоичных объектов Azure с общедоступными контейнерами не поддерживается.      
>

**toosubmit заданий**

Используйте следующий синтаксис toosubmit задания hello.

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

Например:

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

**toolist заданий и отображения сведений о задании**

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

**toocancel заданий**

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a>Получение результатов задания

После завершения задания можно использовать следующие команды toolist hello выходные файлы hello и загрузки файлов hello:

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

Например:

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a>Конвейеры и повторения

**Получение сведений о конвейерах и повторениях**

Используйте hello `az dla job pipeline` команд, сведения о конвейере hello toosee ранее переданных заданий.

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

Используйте hello `az dla job recurrence` команды toosee hello повторений для ранее отправленные задания.

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a>Дальнейшие действия

* hello toosee 2.0 CLI аналитика Озера данных справочный документ, в разделе [аналитики Озера данных](https://docs.microsoft.com/cli/azure/dla).
* hello toosee 2.0 CLI хранилища Озера данных справочный документ, в разделе [хранилища Озера данных](https://docs.microsoft.com/cli/azure/dls).
* в разделе toosee более сложный запрос, [веб-сайта анализ журналов с помощью аналитики Озера данных Azure](data-lake-analytics-analyze-weblogs.md).
