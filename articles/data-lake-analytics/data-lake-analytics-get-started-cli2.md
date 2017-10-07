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
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a><span data-ttu-id="ff2dc-103">Начало работы с Azure Data Lake Analytics при помощи Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ff2dc-103">Get started with Azure Data Lake Analytics using Azure CLI 2.0</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="ff2dc-104">В этом руководстве вам предстоит разработать задание, которое считывает файл с разделителями-табуляциями (TSV) и преобразует его в файл с разделителями-запятыми (CSV).</span><span class="sxs-lookup"><span data-stu-id="ff2dc-104">In this tutorial, you develop a job that reads a tab separated values (TSV) file and converts it into a comma-separated values (CSV) file.</span></span> <span data-ttu-id="ff2dc-105">toogo через hello поддерживается же учебника при помощи других средств, используйте hello раскрывающегося списка в верхней части hello этого раздела.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-105">toogo through hello same tutorial using other supported tools, use hello dropdown list on hello top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff2dc-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ff2dc-106">Prerequisites</span></span>
<span data-ttu-id="ff2dc-107">Прежде чем начать работу с учебником, необходимо иметь hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ff2dc-107">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="ff2dc-108">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-108">**An Azure subscription**.</span></span> <span data-ttu-id="ff2dc-109">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff2dc-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ff2dc-110">**Azure CLI 2.0**.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-110">**Azure CLI 2.0**.</span></span> <span data-ttu-id="ff2dc-111">См. статью [Установка и настройка интерфейса командной строки Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ff2dc-111">See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="ff2dc-112">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="ff2dc-112">Log in tooAzure</span></span>

<span data-ttu-id="ff2dc-113">toolog в tooyour подписки Azure:</span><span class="sxs-lookup"><span data-stu-id="ff2dc-113">toolog in tooyour Azure subscription:</span></span>

```
azurecli
az login
```

<span data-ttu-id="ff2dc-114">Запрошенный toobrowse tooa URL-адрес и введите код проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-114">You are requested toobrowse tooa URL, and enter an authentication code.</span></span>  <span data-ttu-id="ff2dc-115">И следуйте инструкциям tooenter hello учетные данные.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-115">And then follow hello instructions tooenter your credentials.</span></span>

<span data-ttu-id="ff2dc-116">После входа hello входа команда перечисляет подписки.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-116">Once you have logged in, hello login command lists your subscriptions.</span></span>

<span data-ttu-id="ff2dc-117">toouse конкретной подписки:</span><span class="sxs-lookup"><span data-stu-id="ff2dc-117">toouse a specific subscription:</span></span>

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="ff2dc-118">Создание учетной записи аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="ff2dc-118">Create Data Lake Analytics account</span></span>
<span data-ttu-id="ff2dc-119">Для выполнения любых заданий требуется учетная запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-119">You need a Data Lake Analytics account before you can run any jobs.</span></span> <span data-ttu-id="ff2dc-120">toocreate учетную запись аналитики Озера данных, необходимо указать hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ff2dc-120">toocreate a Data Lake Analytics account, you must specify hello following items:</span></span>

* <span data-ttu-id="ff2dc-121">**Группа ресурсов Azure**.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-121">**Azure Resource Group**.</span></span> <span data-ttu-id="ff2dc-122">В группе ресурсов Azure необходимо создать учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-122">A Data Lake Analytics account must be created within an Azure Resource group.</span></span> <span data-ttu-id="ff2dc-123">[Диспетчер ресурсов Azure](../azure-resource-manager/resource-group-overview.md) позволяет toowork с ресурсами hello в приложении в качестве группы.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you toowork with hello resources in your application as a group.</span></span> <span data-ttu-id="ff2dc-124">Можно развернуть, обновить или удалить все ресурсы hello для вашего приложения, в один, согласованной операции.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-124">You can deploy, update, or delete all of hello resources for your application in a single, coordinated operation.</span></span>  

<span data-ttu-id="ff2dc-125">toolist hello групп ресурсов в подписке:</span><span class="sxs-lookup"><span data-stu-id="ff2dc-125">toolist hello existing resource groups under your subscription:</span></span>

```
az group list
```

<span data-ttu-id="ff2dc-126">toocreate новая группа ресурсов:</span><span class="sxs-lookup"><span data-stu-id="ff2dc-126">toocreate a new resource group:</span></span>

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* <span data-ttu-id="ff2dc-127">**Имя учетной записи Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-127">**Data Lake Analytics account name**.</span></span> <span data-ttu-id="ff2dc-128">Каждой учетной записи Data Lake Analytics присвоено имя.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-128">Each Data Lake Analytics account has a name.</span></span>
* <span data-ttu-id="ff2dc-129">**Расположение.**</span><span class="sxs-lookup"><span data-stu-id="ff2dc-129">**Location**.</span></span> <span data-ttu-id="ff2dc-130">Используйте одну из hello центрах обработки данных Azure, которые поддерживает аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-130">Use one of hello Azure data centers that supports Data Lake Analytics.</span></span>
* <span data-ttu-id="ff2dc-131">**Учетная запись Data Lake Store по умолчанию** — каждая учетная запись Data Lake Analytics содержит учетную запись Data Lake Store по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-131">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span>

<span data-ttu-id="ff2dc-132">toolist hello хранилища Озера данных учетная запись:</span><span class="sxs-lookup"><span data-stu-id="ff2dc-132">toolist hello existing Data Lake Store account:</span></span>

```
az dls account list
```

<span data-ttu-id="ff2dc-133">toocreate новую учетную запись хранилища Озера данных:</span><span class="sxs-lookup"><span data-stu-id="ff2dc-133">toocreate a new Data Lake Store account:</span></span>

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

<span data-ttu-id="ff2dc-134">Используйте следующий синтаксис toocreate учетную запись аналитики Озера данных hello.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-134">Use hello following syntax toocreate a Data Lake Analytics account:</span></span>

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

<span data-ttu-id="ff2dc-135">После создания учетной записи, можно использовать следующие учетные записи hello toolist команды hello и Показать сведения об учетной записи:</span><span class="sxs-lookup"><span data-stu-id="ff2dc-135">After creating an account, you can use hello following commands toolist hello accounts and show account details:</span></span>

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a><span data-ttu-id="ff2dc-136">Отправка хранилища Озера данных tooData</span><span class="sxs-lookup"><span data-stu-id="ff2dc-136">Upload data tooData Lake Store</span></span>
<span data-ttu-id="ff2dc-137">В этом руководстве обрабатываются некоторые журналы поиска.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-137">In this tutorial, you process some search logs.</span></span>  <span data-ttu-id="ff2dc-138">Hello поиска журнала могут храниться в хранилище Озера данных или хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-138">hello search log can be stored in either Data Lake store or Azure Blob storage.</span></span>

<span data-ttu-id="ff2dc-139">Hello портал Azure предоставляет пользовательский интерфейс для копирования некоторые образец данных файлов toohello по умолчанию хранилище Озера данных учетной записи, которая содержит поиск файла журнала.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-139">hello Azure portal provides a user interface for copying some sample data files toohello default Data Lake Store account, which include a search log file.</span></span> <span data-ttu-id="ff2dc-140">В разделе [Подготовка данных источника](data-lake-analytics-get-started-portal.md) tooupload hello данных toohello по умолчанию хранилище Озера данных учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-140">See [Prepare source data](data-lake-analytics-get-started-portal.md) tooupload hello data toohello default Data Lake Store account.</span></span>

<span data-ttu-id="ff2dc-141">tooupload файлов с помощью CLI версии 2.0, hello используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="ff2dc-141">tooupload files using CLI 2.0, use hello following commands:</span></span>

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

<span data-ttu-id="ff2dc-142">Из аналитики озера данных также доступно хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-142">Data Lake Analytics can also access Azure Blob storage.</span></span>  <span data-ttu-id="ff2dc-143">Для передачи больших двоичных объектов хранилища данных tooAzure, см. [использование hello Azure CLI со службой хранилища Azure](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ff2dc-143">For uploading data tooAzure Blob storage, see [Using hello Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>

## <a name="submit-data-lake-analytics-jobs"></a><span data-ttu-id="ff2dc-144">Отправка заданий аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="ff2dc-144">Submit Data Lake Analytics jobs</span></span>
<span data-ttu-id="ff2dc-145">Аналитика Озера данных заданий Hello записываются в hello языка U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-145">hello Data Lake Analytics jobs are written in hello U-SQL language.</span></span> <span data-ttu-id="ff2dc-146">toolearn Дополнительные сведения о U-SQL, в разделе [приступить к работе с языком U SQL](data-lake-analytics-u-sql-get-started.md) и [eence U-SQL языка](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="ff2dc-146">toolearn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language eence](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="ff2dc-147">**toocreate сценарий задания аналитики Озера данных**</span><span class="sxs-lookup"><span data-stu-id="ff2dc-147">**toocreate a Data Lake Analytics job script**</span></span>

<span data-ttu-id="ff2dc-148">Создайте текстовый файл с следующий скрипт U-SQL и сохраните текстовый файл hello tooyour-рабочей станции:</span><span class="sxs-lookup"><span data-stu-id="ff2dc-148">Create a text file with following U-SQL script, and save hello text file tooyour workstation:</span></span>

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

<span data-ttu-id="ff2dc-149">Этот скрипт U-SQL считывает hello источник данных файла с помощью **Extractors.Tsv()**, а затем создает файл csv с помощью **Outputters.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-149">This U-SQL script reads hello source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span>

<span data-ttu-id="ff2dc-150">Не изменяйте hello два пути, если скопировать hello исходный файл в другое расположение.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-150">Don't modify hello two paths unless you copy hello source file into a different location.</span></span>  <span data-ttu-id="ff2dc-151">Аналитика Озера данных создает hello выходную папку, если он не существует.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-151">Data Lake Analytics creates hello output folder if it doesn't exist.</span></span>

<span data-ttu-id="ff2dc-152">Это проще toouse относительных путей для файлов, хранящихся в учетных записях хранилища Озера данных по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-152">It is simpler toouse relative paths for files stored in default Data Lake Store accounts.</span></span> <span data-ttu-id="ff2dc-153">Также можно использовать абсолютные пути.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-153">You can also use absolute paths.</span></span>  <span data-ttu-id="ff2dc-154">Например:</span><span class="sxs-lookup"><span data-stu-id="ff2dc-154">For example:</span></span>

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

<span data-ttu-id="ff2dc-155">Необходимо использовать абсолютные пути файлов tooaccess в связанные учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-155">You must use absolute paths tooaccess files in linked Storage accounts.</span></span>  <span data-ttu-id="ff2dc-156">Hello для файлов, хранящихся в связанной учетной записи хранилища Azure используется синтаксис:</span><span class="sxs-lookup"><span data-stu-id="ff2dc-156">hello syntax for files stored in linked Azure Storage account is:</span></span>

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> <span data-ttu-id="ff2dc-157">Контейнер больших двоичных объектов Azure с общедоступными большими двоичными объектами не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-157">Azure Blob container with public blobs are not supported.</span></span>      
> <span data-ttu-id="ff2dc-158">Контейнер больших двоичных объектов Azure с общедоступными контейнерами не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-158">Azure Blob container with public containers are not supported.</span></span>      
>

<span data-ttu-id="ff2dc-159">**toosubmit заданий**</span><span class="sxs-lookup"><span data-stu-id="ff2dc-159">**toosubmit jobs**</span></span>

<span data-ttu-id="ff2dc-160">Используйте следующий синтаксис toosubmit задания hello.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-160">Use hello following syntax toosubmit a job.</span></span>

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

<span data-ttu-id="ff2dc-161">Например:</span><span class="sxs-lookup"><span data-stu-id="ff2dc-161">For example:</span></span>

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

<span data-ttu-id="ff2dc-162">**toolist заданий и отображения сведений о задании**</span><span class="sxs-lookup"><span data-stu-id="ff2dc-162">**toolist jobs and show job details**</span></span>

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

<span data-ttu-id="ff2dc-163">**toocancel заданий**</span><span class="sxs-lookup"><span data-stu-id="ff2dc-163">**toocancel jobs**</span></span>

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a><span data-ttu-id="ff2dc-164">Получение результатов задания</span><span class="sxs-lookup"><span data-stu-id="ff2dc-164">Retrieve job results</span></span>

<span data-ttu-id="ff2dc-165">После завершения задания можно использовать следующие команды toolist hello выходные файлы hello и загрузки файлов hello:</span><span class="sxs-lookup"><span data-stu-id="ff2dc-165">After a job is completed, you can use hello following commands toolist hello output files, and download hello files:</span></span>

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

<span data-ttu-id="ff2dc-166">Например:</span><span class="sxs-lookup"><span data-stu-id="ff2dc-166">For example:</span></span>

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a><span data-ttu-id="ff2dc-167">Конвейеры и повторения</span><span class="sxs-lookup"><span data-stu-id="ff2dc-167">Pipelines and recurrences</span></span>

<span data-ttu-id="ff2dc-168">**Получение сведений о конвейерах и повторениях**</span><span class="sxs-lookup"><span data-stu-id="ff2dc-168">**Get information about pipelines and recurrences**</span></span>

<span data-ttu-id="ff2dc-169">Используйте hello `az dla job pipeline` команд, сведения о конвейере hello toosee ранее переданных заданий.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-169">Use hello `az dla job pipeline` commands toosee hello pipeline information previously submitted jobs.</span></span>

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

<span data-ttu-id="ff2dc-170">Используйте hello `az dla job recurrence` команды toosee hello повторений для ранее отправленные задания.</span><span class="sxs-lookup"><span data-stu-id="ff2dc-170">Use hello `az dla job recurrence` commands toosee hello recurrence information for previously submitted jobs.</span></span>

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a><span data-ttu-id="ff2dc-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ff2dc-171">Next steps</span></span>

* <span data-ttu-id="ff2dc-172">hello toosee 2.0 CLI аналитика Озера данных справочный документ, в разделе [аналитики Озера данных](https://docs.microsoft.com/cli/azure/dla).</span><span class="sxs-lookup"><span data-stu-id="ff2dc-172">toosee hello Data Lake Analytics CLI 2.0 reference document, see [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span></span>
* <span data-ttu-id="ff2dc-173">hello toosee 2.0 CLI хранилища Озера данных справочный документ, в разделе [хранилища Озера данных](https://docs.microsoft.com/cli/azure/dls).</span><span class="sxs-lookup"><span data-stu-id="ff2dc-173">toosee hello Data Lake Store CLI 2.0 reference document, see [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span></span>
* <span data-ttu-id="ff2dc-174">в разделе toosee более сложный запрос, [веб-сайта анализ журналов с помощью аналитики Озера данных Azure](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="ff2dc-174">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
