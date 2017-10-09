---
title: "aaaCreate Hive таблиц и загрузки данных из хранилища больших двоичных объектов | Документы Microsoft"
description: "Создание таблиц Hive и загружают данные в таблицы toohive BLOB-объектов"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="62966-103">Создание таблиц Hive и загрузка данных из хранилища BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="62966-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="62966-104">В этой статье рассматриваются общие запросы Hive, которые создают таблицы Hive и загружают данные из хранилищ BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="62966-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="62966-105">Некоторые рекомендации также предоставляется для секционирования таблицы Hive и об использовании производительность запросов форматирования tooimprove hello оптимизированными строк по столбцам (ORC.).</span><span class="sxs-lookup"><span data-stu-id="62966-105">Some guidance is also provided on partitioning Hive tables and on using hello Optimized Row Columnar (ORC) formatting tooimprove query performance.</span></span>

<span data-ttu-id="62966-106">Это **меню** связывает tootopics, описывающие, каким образом данные tooingest в целевых средах, где hello данные могут храниться и обрабатываться во время hello процесса обработки и анализа данных Team (TDSP).</span><span class="sxs-lookup"><span data-stu-id="62966-106">This **menu** links tootopics that describe how tooingest data into target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="62966-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="62966-107">Prerequisites</span></span>
<span data-ttu-id="62966-108">В этой статье предполагается, что вы:</span><span class="sxs-lookup"><span data-stu-id="62966-108">This article assumes that you have:</span></span>

* <span data-ttu-id="62966-109">Создали учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="62966-109">Created an Azure storage account.</span></span> <span data-ttu-id="62966-110">Инструкции см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="62966-110">If you need instructions, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="62966-111">Подготовить настроенные кластеру с hello службы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="62966-111">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span>  <span data-ttu-id="62966-112">Инструкции см. в статье [Настройка кластеров Azure HDInsight Hadoop для процесса обработки и анализа данных группы](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="62966-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="62966-113">Кластер toohello включен удаленный доступ, зарегистрированы и открыть консоль командной строки Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="62966-113">Enabled remote access toohello cluster, logged in, and opened hello Hadoop Command-Line console.</span></span> <span data-ttu-id="62966-114">При необходимости инструкции в разделе [доступа hello головного узла кластера Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="62966-114">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="62966-115">Отправка больших двоичных объектов хранилища данных tooAzure</span><span class="sxs-lookup"><span data-stu-id="62966-115">Upload data tooAzure blob storage</span></span>
<span data-ttu-id="62966-116">Если вы создали виртуальную машину Azure, следуя инструкциям hello в [Настройка виртуальной машины Azure для расширенной аналитики](machine-learning-data-science-setup-virtual-machine.md), этот файл сценария должно было загруженный toohello *C:\\ Пользователи\\\<имя пользователя\>\\документов\\сценарии обработки и анализа данных* каталог на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="62966-116">If you created an Azure virtual machine by following hello instructions provided in [Set up an Azure virtual machine for advanced analytics](machine-learning-data-science-setup-virtual-machine.md), this script file should have been downloaded toohello *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on hello virtual machine.</span></span> <span data-ttu-id="62966-117">Эти запросы Hive нужны только подключаемого модуля в собственных данных схемы и конфигурации хранилища больших двоичных объектов Azure в toobe соответствующие поля hello готова к отправке.</span><span class="sxs-lookup"><span data-stu-id="62966-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in hello appropriate fields toobe ready for submission.</span></span>

<span data-ttu-id="62966-118">Мы предполагаем, что данные hello для куста таблиц находится в **несжатые** табличном формате, а также что hello данных была отправленного toohello по умолчанию (или дополнительных tooan) контейнера учетной записи хранения hello hello кластере Hadoop.</span><span class="sxs-lookup"><span data-stu-id="62966-118">We assume that hello data for Hive tables is in an **uncompressed** tabular format, and that hello data has been uploaded toohello default (or tooan additional) container of hello storage account used by hello Hadoop cluster.</span></span>

<span data-ttu-id="62966-119">Если требуется, чтобы toopractice на hello **NYC такси обработки данных**, необходимо:</span><span class="sxs-lookup"><span data-stu-id="62966-119">If you want toopractice on hello **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="62966-120">**Загрузить** hello 24 [NYC такси обработки данных](http://www.andresmh.com/nyctaxitrips) файлов (12 Trip файлы и файлы 12 тариф авиакомпании),</span><span class="sxs-lookup"><span data-stu-id="62966-120">**download** hello 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="62966-121">**распаковать** все CSV-файлы; а затем</span><span class="sxs-lookup"><span data-stu-id="62966-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="62966-122">**Отправка** их toohello по умолчанию или соответствующего контейнера hello учетной записи хранилища Azure, созданные hello процедуры, описанной в hello [кластеры настройки Azure HDInsight Hadoop для Advanced Analytics процесса и технологии ](machine-learning-data-science-customize-hadoop-cluster.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="62966-122">**upload** them toohello default (or appropriate container) of hello Azure storage account that was created by hello procedure outlined in hello [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="62966-123">Hello процесса tooupload hello .csv файлы toohello контейнер по умолчанию hello учетной записи хранения можно найти в данном [страницы](machine-learning-data-science-process-hive-walkthrough.md#upload).</span><span class="sxs-lookup"><span data-stu-id="62966-123">hello process tooupload hello .csv files toohello default container on hello storage account can be found on this [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span></span>

## <span data-ttu-id="62966-124"><a name="submit"></a>Каким образом запросы Hive toosubmit</span><span class="sxs-lookup"><span data-stu-id="62966-124"><a name="submit"></a>How toosubmit Hive queries</span></span>
<span data-ttu-id="62966-125">Инструменты для отправки запросов Hive:</span><span class="sxs-lookup"><span data-stu-id="62966-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="62966-126">Отправка запросов Hive через командную строку Hadoop в головной узел кластера Hadoop</span><span class="sxs-lookup"><span data-stu-id="62966-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="62966-127">Отправки запросов Hive с hello редактор Hive</span><span class="sxs-lookup"><span data-stu-id="62966-127">Submit Hive queries with hello Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="62966-128">Отправка запросов Hive с помощью команд PowerShell Azure</span><span class="sxs-lookup"><span data-stu-id="62966-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="62966-129">Запросы Hive похожи на SQL.</span><span class="sxs-lookup"><span data-stu-id="62966-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="62966-130">Если вы знакомы с SQL, может оказаться hello [Hive для Памятка пользователей SQL](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) полезно.</span><span class="sxs-lookup"><span data-stu-id="62966-130">If you are familiar with SQL, you may find hello [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="62966-131">При отправке запроса Hive, можно также управлять назначением hello hello вывод запросов Hive будь hello экрана или tooa локальный файл на головном узле hello или tooan BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="62966-131">When submitting a Hive query, you can also control hello destination of hello output from Hive queries, whether it be on hello screen or tooa local file on hello head node or tooan Azure blob.</span></span>

### <span data-ttu-id="62966-132"><a name="headnode"></a> 1. Отправка запросов Hive через командную строку Hadoop в головной узел кластера Hadoop</span><span class="sxs-lookup"><span data-stu-id="62966-132"><a name="headnode"></a> 1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="62966-133">Если hello Hive запроса является сложным, передается непосредственно в hello головного узла кластера Hadoop hello обычно приводит toofaster, поворачивать, чем отправка его с помощью редактора, Hive или скриптов Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62966-133">If hello Hive query is complex, submitting it directly in hello head node of hello Hadoop cluster typically leads toofaster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="62966-134">Войдите в toohello головного узла кластера Hadoop hello, откройте hello Hadoop командной строки на рабочем столе hello hello головного узла и введите команду `cd %hive_home%\bin`.</span><span class="sxs-lookup"><span data-stu-id="62966-134">Log in toohello head node of hello Hadoop cluster, open hello Hadoop Command Line on hello desktop of hello head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="62966-135">В командной строки Hadoop hello имеется запросов Hive toosubmit тремя способами:</span><span class="sxs-lookup"><span data-stu-id="62966-135">You have three ways toosubmit Hive queries in hello Hadoop Command Line:</span></span>

* <span data-ttu-id="62966-136">напрямую;</span><span class="sxs-lookup"><span data-stu-id="62966-136">directly</span></span>
* <span data-ttu-id="62966-137">с помощью HQL-файлов;</span><span class="sxs-lookup"><span data-stu-id="62966-137">using .hql files</span></span>
* <span data-ttu-id="62966-138">с hello Hive командной консоли</span><span class="sxs-lookup"><span data-stu-id="62966-138">with hello Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="62966-139">Отправка запросов Hive непосредственно из командной строки Hadoop</span><span class="sxs-lookup"><span data-stu-id="62966-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="62966-140">Можно выполнить команду, например `hive -e "<your hive query>;` toosubmit простых запросов Hive непосредственно в Hadoop командной строки.</span><span class="sxs-lookup"><span data-stu-id="62966-140">You can run command like `hive -e "<your hive query>;` toosubmit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="62966-141">Ниже приведен пример, где поле контуров hello красный hello команду, которая отправляет запрос Hive hello и hello зеленой рамке контуров hello вывод запроса Hive hello.</span><span class="sxs-lookup"><span data-stu-id="62966-141">Here is an example, where hello red box outlines hello command that submits hello Hive query, and hello green box outlines hello output from hello Hive query.</span></span>

![Создание рабочей области](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="62966-143">Отправка запросов Hive в HQL-файлах</span><span class="sxs-lookup"><span data-stu-id="62966-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="62966-144">Если запрос Hive hello более сложен и имеет несколько строк, редактирование запросов в командной строке или куст командной консоли не имеет смысла.</span><span class="sxs-lookup"><span data-stu-id="62966-144">When hello Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="62966-145">Альтернативой является toouse текстового редактора в головном узле hello hello Hadoop кластера toosave hello запросов Hive в файле .hql в локальном каталоге hello головного узла.</span><span class="sxs-lookup"><span data-stu-id="62966-145">An alternative is toouse a text editor in hello head node of hello Hadoop cluster toosave hello Hive queries in a .hql file in a local directory of hello head node.</span></span> <span data-ttu-id="62966-146">Затем запрос Hive hello в файле .hql hello могут передаваться с помощью hello `-f` аргумент, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="62966-146">Then hello Hive query in hello .hql file can be submitted by using hello `-f` argument as follows:</span></span>

    hive -f "<path toohello .hql file>"

![Создание рабочей области](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="62966-148">**Отменить вывод состояния хода выполнения запросов Hive на экран**</span><span class="sxs-lookup"><span data-stu-id="62966-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="62966-149">По умолчанию после отправки запроса Hive в Hadoop командной строки hello ход выполнения задания Map/Reduce hello будет выведен на экран.</span><span class="sxs-lookup"><span data-stu-id="62966-149">By default, after Hive query is submitted in Hadoop Command Line, hello progress of hello Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="62966-150">toosuppress Здравствуйте печати экран хода выполнения заданий Map/Reduce hello, можно использовать аргумент `-S` («S» в верхнем регистре) в hello командной строки следующим образом:</span><span class="sxs-lookup"><span data-stu-id="62966-150">toosuppress hello screen print of hello Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in hello command line as follows:</span></span>

    hive -S -f "<path toohello .hql file>"
<span data-ttu-id="62966-151">.</span><span class="sxs-lookup"><span data-stu-id="62966-151">.</span></span>    <span data-ttu-id="62966-152">hive -S -e "<Hive queries>"</span><span class="sxs-lookup"><span data-stu-id="62966-152">hive -S -e "<Hive queries>"</span></span>

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="62966-153">Отправка запросов Hive в командной консоли Hive</span><span class="sxs-lookup"><span data-stu-id="62966-153">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="62966-154">Можно также сначала ввести hello Hive командной консоли, выполнив команду `hive` в Hadoop командной строки и отправки запросов Hive в командной консоли Hive.</span><span class="sxs-lookup"><span data-stu-id="62966-154">You can also first enter hello Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="62966-155">Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="62966-155">Here is an example.</span></span> <span data-ttu-id="62966-156">В этом примере hello две Красные прямоугольники выделения hello команды, используемые tooenter hello командной консоли Hive и hello запроса Hive, отправленного в командной консоли Hive, соответственно.</span><span class="sxs-lookup"><span data-stu-id="62966-156">In this example, hello two red boxes highlight hello commands used tooenter hello Hive command console, and hello Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="62966-157">поле Hello зеленый выделяются hello выходные данные запроса Hive hello.</span><span class="sxs-lookup"><span data-stu-id="62966-157">hello green box highlights hello output from hello Hive query.</span></span>

![Создание рабочей области](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="62966-159">Hello предыдущих примерах непосредственно выходные результаты запроса Hive hello на экране.</span><span class="sxs-lookup"><span data-stu-id="62966-159">hello previous examples directly output hello Hive query results on screen.</span></span> <span data-ttu-id="62966-160">Можно также написать hello вывода tooa локальный файл на головном узле hello, или tooan BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="62966-160">You can also write hello output tooa local file on hello head node, or tooan Azure blob.</span></span> <span data-ttu-id="62966-161">Затем можно использовать другие средства toofurther анализ вывода hello запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="62966-161">Then, you can use other tools toofurther analyze hello output of Hive queries.</span></span>

<span data-ttu-id="62966-162">**Выходного файла локального tooa результаты запроса Hive.**</span><span class="sxs-lookup"><span data-stu-id="62966-162">**Output Hive query results tooa local file.**</span></span>
<span data-ttu-id="62966-163">toooutput Hive запроса результаты tooa локальный каталог на головном узле hello, имеется запрос Hive toosubmit hello в hello Hadoop командной строки следующим образом:</span><span class="sxs-lookup"><span data-stu-id="62966-163">toooutput Hive query results tooa local directory on hello head node, you have toosubmit hello Hive query in hello Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in hello head node>

<span data-ttu-id="62966-164">В следующем примере hello, выходные данные запроса Hive hello записывается в файл `hivequeryoutput.txt` в каталоге `C:\apps\temp`.</span><span class="sxs-lookup"><span data-stu-id="62966-164">In hello following example, hello output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![Создание рабочей области](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="62966-166">**Результаты запроса tooan BLOB-объектов Azure для выходных данных Hive**</span><span class="sxs-lookup"><span data-stu-id="62966-166">**Output Hive query results tooan Azure blob**</span></span>

<span data-ttu-id="62966-167">Кроме того, может выводить результаты запроса tooan BLOB-объектов Azure, в контейнере по умолчанию hello hello кластера Hadoop для hello Hive.</span><span class="sxs-lookup"><span data-stu-id="62966-167">You can also output hello Hive query results tooan Azure blob, within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="62966-168">Hello запрос Hive для это выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="62966-168">hello Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

<span data-ttu-id="62966-169">В следующем примере hello, каталог больших двоичных объектов tooa записываются hello выходные данные запроса Hive `queryoutputdir` внутри контейнера по умолчанию hello hello кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="62966-169">In hello following example, hello output of Hive query is written tooa blob directory `queryoutputdir` within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="62966-170">Здесь требуется только имя папки hello tooprovide без hello имя большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="62966-170">Here, you only need tooprovide hello directory name, without hello blob name.</span></span> <span data-ttu-id="62966-171">Если указать имя каталога и имя большого двоичного объекта, появится следующее сообщение об ошибке: `wasb:///queryoutputdir/queryoutput.txt`.</span><span class="sxs-lookup"><span data-stu-id="62966-171">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![Создание рабочей области](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="62966-173">При открытии hello контейнер по умолчанию для кластера Hadoop hello, с помощью обозревателя хранилищ Azure, как показано в следующий рисунок hello видно hello выходных данных запроса Hive hello.</span><span class="sxs-lookup"><span data-stu-id="62966-173">If you open hello default container of hello Hadoop cluster using Azure Storage Explorer, you can see hello output of hello Hive query as shown in hello following figure.</span></span> <span data-ttu-id="62966-174">Можно применить hello фильтра (выделенная красный прямоугольник) tooonly получить hello большой двоичный объект с указанным буквы в именах.</span><span class="sxs-lookup"><span data-stu-id="62966-174">You can apply hello filter (highlighted by red box) tooonly retrieve hello blob with specified letters in names.</span></span>

![Создание рабочей области](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <span data-ttu-id="62966-176"><a name="hive-editor"></a> 2. Отправки запросов Hive с hello редактор Hive</span><span class="sxs-lookup"><span data-stu-id="62966-176"><a name="hive-editor"></a> 2. Submit Hive queries with hello Hive Editor</span></span>
<span data-ttu-id="62966-177">Можно также использовать hello консоль запросов (редактор куста реестра), введя URL-адрес формы hello *https://&#60; Имя кластера Hadoop >.azurehdinsight.net/Home/HiveEditor* в веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="62966-177">You can also use hello Query Console (Hive Editor) by entering a URL of hello form *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="62966-178">Вы должны быть зарегистрированы hello см. в разделе эту консоль, и поэтому необходимы полномочия кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="62966-178">You must be logged in hello see this console and so you need your Hadoop cluster credentials here.</span></span>

### <span data-ttu-id="62966-179"><a name="ps"></a> 3. Отправка запросов Hive с помощью команд PowerShell Azure</span><span class="sxs-lookup"><span data-stu-id="62966-179"><a name="ps"></a> 3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="62966-180">Можно также использовать запросы Hive toosubmit PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62966-180">You can also use PowerShell toosubmit Hive queries.</span></span> <span data-ttu-id="62966-181">Инструкции см. в статье [Отправка заданий Hadoop в HDInsight](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="62966-181">For instructions, see [Submit Hive jobs using PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span></span>

## <span data-ttu-id="62966-182"><a name="create-tables"></a>Создание базы данных и таблиц Hive</span><span class="sxs-lookup"><span data-stu-id="62966-182"><a name="create-tables"></a>Create Hive database and tables</span></span>
<span data-ttu-id="62966-183">Hello запросов Hive общих в hello [репозитории GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) и могут быть загружены из него.</span><span class="sxs-lookup"><span data-stu-id="62966-183">hello Hive queries are shared in hello [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="62966-184">Ниже приведен запрос Hive hello, создающий таблицу Hive.</span><span class="sxs-lookup"><span data-stu-id="62966-184">Here is hello Hive query that creates a Hive table.</span></span>

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

<span data-ttu-id="62966-185">Ниже приведены описания hello необходимые tooplug в hello поля и другие элементы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="62966-185">Here are hello descriptions of hello fields that you need tooplug in and other configurations:</span></span>

* <span data-ttu-id="62966-186">**&#60; имя базы данных >**: имя базы данных hello, что требуется toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="62966-186">**&#60;database name>**: hello name of hello database that you want toocreate.</span></span> <span data-ttu-id="62966-187">Если необходимо просто база данных по умолчанию hello toouse hello запроса *создать базу данных...*  может быть опущено.</span><span class="sxs-lookup"><span data-stu-id="62966-187">If you just want toouse hello default database, hello query *create database...* can be omitted.</span></span>
* <span data-ttu-id="62966-188">**&#60; имя таблицы >**: hello имя hello таблицы, которая будет toocreate в указанной базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="62966-188">**&#60;table name>**: hello name of hello table that you want toocreate within hello specified database.</span></span> <span data-ttu-id="62966-189">Если требуется база данных по умолчанию hello toouse hello таблицы можно непосредственно ссылаться по *&#60; имя таблицы >* без &#60; имя базы данных >.</span><span class="sxs-lookup"><span data-stu-id="62966-189">If you want toouse hello default database, hello table can be directly referred by *&#60;table name>* without &#60;database name>.</span></span>
* <span data-ttu-id="62966-190">**&#60; разделитель >**: hello разделителя, разделяющий поля в файл toobe hello данные отправлены toohello таблицу Hive.</span><span class="sxs-lookup"><span data-stu-id="62966-190">**&#60;field separator>**: hello separator that delimits fields in hello data file toobe uploaded toohello Hive table.</span></span>
* <span data-ttu-id="62966-191">**&#60; разделитель строк >**: hello разделителя, который разделяет строки в файле данных hello.</span><span class="sxs-lookup"><span data-stu-id="62966-191">**&#60;line separator>**: hello separator that delimits lines in hello data file.</span></span>
* <span data-ttu-id="62966-192">**&#60; место хранения >**: hello расположение хранилища Azure toosave данные hello Hive таблиц.</span><span class="sxs-lookup"><span data-stu-id="62966-192">**&#60;storage location>**: hello Azure storage location toosave hello data of Hive tables.</span></span> <span data-ttu-id="62966-193">Если вы не укажете *РАСПОЛОЖЕНИЕ &#60; место хранения >*, hello базы данных и hello таблицы хранятся в *hive или хранилище или* каталог в контейнере по умолчанию hello hello Hive кластера по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="62966-193">If you do not specify *LOCATION &#60;storage location>*, hello database and hello tables are stored in *hive/warehouse/* directory in hello default container of hello Hive cluster by default.</span></span> <span data-ttu-id="62966-194">Если требуется, чтобы место хранения toospecify hello, место хранения hello имеет toobe внутри контейнера по умолчанию hello hello базы данных и таблиц.</span><span class="sxs-lookup"><span data-stu-id="62966-194">If you want toospecify hello storage location, hello storage location has toobe within hello default container for hello database and tables.</span></span> <span data-ttu-id="62966-195">Это расположение имеет называется контейнер по умолчанию toohello относительное расположение кластера hello в формате hello toobe *"wasb: / / / &#60; каталог 1 > /"* или *"wasb: / / / &#60; каталог 1 > и &#60; каталог 2 > / "*и т. д. После выполнения запроса hello hello относительный каталоги создаются внутри контейнера по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="62966-195">This location has toobe referred as location relative toohello default container of hello cluster in hello format of *'wasb:///&#60;directory 1>/'* or *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. After hello query is executed, hello relative directories are created within hello default container.</span></span>
* <span data-ttu-id="62966-196">**TBLPROPERTIES("SKIP.Header.Line.Count"="1")**: Если hello файла данных строки заголовка, у вас есть tooadd это свойство **в конце hello** из hello *создать таблицу* запроса.</span><span class="sxs-lookup"><span data-stu-id="62966-196">**TBLPROPERTIES("skip.header.line.count"="1")**: If hello data file has a header line, you have tooadd this property **at hello end** of hello *create table* query.</span></span> <span data-ttu-id="62966-197">В противном случае — как таблицу записей toohello загружаются hello заголовков строк.</span><span class="sxs-lookup"><span data-stu-id="62966-197">Otherwise, hello header line is loaded as a record toohello table.</span></span> <span data-ttu-id="62966-198">Если файл данных hello не имеет строку заголовка, эта конфигурация может быть опущено в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="62966-198">If hello data file does not have a header line, this configuration can be omitted in hello query.</span></span>

## <span data-ttu-id="62966-199"><a name="load-data"></a>Загрузка данных tooHive таблиц</span><span class="sxs-lookup"><span data-stu-id="62966-199"><a name="load-data"></a>Load data tooHive tables</span></span>
<span data-ttu-id="62966-200">Ниже приведен запрос Hive hello, которая загружает данные в таблицу Hive.</span><span class="sxs-lookup"><span data-stu-id="62966-200">Here is hello Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="62966-201">**&#60; данные tooblob путь >**: hello в случае таблицу Hive toohello toobe загружен файл hello BLOB-объектов в контейнере по умолчанию hello hello кластера HDInsight Hadoop *&#60; данные tooblob путь >* должен иметь формат hello *"wasb: / / / &#60; каталог, в этом контейнере > и &#60; имя файла большого двоичного объекта >"*.</span><span class="sxs-lookup"><span data-stu-id="62966-201">**&#60;path tooblob data>**: If hello blob file toobe uploaded toohello Hive table is in hello default container of hello HDInsight Hadoop cluster, hello *&#60;path tooblob data>* should be in hello format *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span></span> <span data-ttu-id="62966-202">файл Hello BLOB-объекта также могут быть в дополнительного контейнера hello кластера HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="62966-202">hello blob file can also be in an additional container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="62966-203">В этом случае *&#60; данные tooblob путь >* должен иметь формат hello *"wasb: / / &#60; имя контейнера > @&#60; имя учетной записи хранения >.blob.core.windows.net/ &#60; имя файла большого двоичного объекта >"*.</span><span class="sxs-lookup"><span data-stu-id="62966-203">In this case, *&#60;path tooblob data>* should be in hello format *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="62966-204">Hello таблицы tooHive toobe отправки данных большого двоичного объекта имеет toobe по умолчанию hello или дополнительного контейнера hello учетной записи хранилища для кластера Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="62966-204">hello blob data toobe uploaded tooHive table has toobe in hello default or additional container of hello storage account for hello Hadoop cluster.</span></span> <span data-ttu-id="62966-205">В противном случае hello *загрузки данных* запрос завершается ошибкой, обнаруживших, что нет доступа к данным hello.</span><span class="sxs-lookup"><span data-stu-id="62966-205">Otherwise, hello *LOAD DATA* query fails complaining that it cannot access hello data.</span></span>
  >
  >

## <span data-ttu-id="62966-206"><a name="partition-orc"></a>Дополнительные разделы: секционированные таблицы и хранение данных Hive в формате ORC</span><span class="sxs-lookup"><span data-stu-id="62966-206"><a name="partition-orc"></a>Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="62966-207">Если hello данных имеет большой размер, секционирование таблицы hello предпочтительнее для запросов, которые не требуют tooscan несколько секций таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="62966-207">If hello data is large, partitioning hello table is beneficial for queries that only need tooscan a few partitions of hello table.</span></span> <span data-ttu-id="62966-208">Для экземпляра это данные журнала hello разумного toopartition веб-сайта по дате.</span><span class="sxs-lookup"><span data-stu-id="62966-208">For instance, it is reasonable toopartition hello log data of a web site by dates.</span></span>

<span data-ttu-id="62966-209">В дополнение toopartitioning Hive таблиц, а также данных Hive полезным toostore hello в hello оптимизированными строк по столбцам (формат ORC.).</span><span class="sxs-lookup"><span data-stu-id="62966-209">In addition toopartitioning Hive tables, it is also beneficial toostore hello Hive data in hello Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="62966-210">Дополнительную информацию об использовании формата ORC см. в <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">разделе о том, как использование ORC-файлов повышает производительность при чтении, записи и обработке данных Hive</a>.</span><span class="sxs-lookup"><span data-stu-id="62966-210">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="62966-211">Секционированная таблица</span><span class="sxs-lookup"><span data-stu-id="62966-211">Partitioned table</span></span>
<span data-ttu-id="62966-212">Ниже приведен запрос Hive hello, Создание секционированной таблицы и загружает в нее данные.</span><span class="sxs-lookup"><span data-stu-id="62966-212">Here is hello Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="62966-213">При запросах к секционированным таблицам, рекомендуется tooadd hello секции условие в hello **начало** из hello `where` предложения, как это повышает эффективность поиска значительно hello.</span><span class="sxs-lookup"><span data-stu-id="62966-213">When querying partitioned tables, it is recommended tooadd hello partition condition in hello **beginning** of hello `where` clause as this improves hello efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <span data-ttu-id="62966-214"><a name="orc"></a>Хранение данных Hive в формате ORC</span><span class="sxs-lookup"><span data-stu-id="62966-214"><a name="orc"></a>Store Hive data in ORC format</span></span>
<span data-ttu-id="62966-215">Нельзя загрузить напрямую данных из хранилища BLOB-данных в таблицы Hive, которые хранятся в формате ORC hello.</span><span class="sxs-lookup"><span data-stu-id="62966-215">You cannot directly load data from blob storage into Hive tables that is stored in hello ORC format.</span></span> <span data-ttu-id="62966-216">Ниже приведены шаги, hello, hello требуются tootake tooload данные из Azure BLOB-объектов tooHive таблиц, сохраненных в формате ORC.</span><span class="sxs-lookup"><span data-stu-id="62966-216">Here are hello steps that hello you need tootake tooload data from Azure blobs tooHive tables stored in ORC format.</span></span>

<span data-ttu-id="62966-217">Создайте внешнюю таблицу **ХРАНЯТСЯ как текстовый ФАЙЛ** и загрузить данные из таблицы toohello хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="62966-217">Create an external table **STORED AS TEXTFILE** and load data from blob storage toohello table.</span></span>

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="62966-218">Создание внутренней таблицы с hello одной схеме с внешней таблицы hello в шаге 1, с hello же разделитель полей и сохранить hello данных Hive в формат ORC hello.</span><span class="sxs-lookup"><span data-stu-id="62966-218">Create an internal table with hello same schema as hello external table in step 1, with hello same field delimiter, and store hello Hive data in hello ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="62966-219">Выбор данных из внешней таблицы hello в шаге 1 и вставки в таблицу ORC hello</span><span class="sxs-lookup"><span data-stu-id="62966-219">Select data from hello external table in step 1 and insert into hello ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="62966-220">Если текстовый ФАЙЛ таблицы hello *&#60; имя базы данных >. &#60; имя таблицы внешних текстовый файл >* содержит разделы, в ШАГЕ 3 hello `SELECT * FROM <database name>.<external textfile table name>` команда выбирает hello секции переменной как поле в hello возвращаемого набора данных.</span><span class="sxs-lookup"><span data-stu-id="62966-220">If hello TEXTFILE table *&#60;database name>.&#60;external textfile table name>* has partitions, in STEP 3, hello `SELECT * FROM <database name>.<external textfile table name>` command selects hello partition variable as a field in hello returned data set.</span></span> <span data-ttu-id="62966-221">Вставка в hello *&#60; имя базы данных >. &#60; имя таблицы ORC >* завершается сбоем с момента *&#60; имя базы данных >. &#60; имя таблицы ORC >* имеет переменную hello секционирования как поле в схеме таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="62966-221">Inserting it into hello *&#60;database name>.&#60;ORC table name>* fails since *&#60;database name>.&#60;ORC table name>* does not have hello partition variable as a field in hello table schema.</span></span> <span data-ttu-id="62966-222">В этом случае необходимо toospecifically выберите hello поля toobe вставлены слишком*&#60; имя базы данных >. &#60; имя таблицы ORC >* следующим образом:</span><span class="sxs-lookup"><span data-stu-id="62966-222">In this case, you need toospecifically select hello fields toobe inserted too*&#60;database name>.&#60;ORC table name>* as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="62966-223">Это безопасно toodrop hello *&#60; имя таблицы внешних текстовый файл >* при приветствия при следующем запросе после всех данных с помощью была вставлена в *&#60; имя базы данных >. &#60; имя таблицы ORC >*:</span><span class="sxs-lookup"><span data-stu-id="62966-223">It is safe toodrop hello *&#60;external textfile table name>* when using hello following query after all data has been inserted into *&#60;database name>.&#60;ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="62966-224">После выполнения этой процедуры, должна быть представлена таблица с данными в toouse готовности формат ORC hello.</span><span class="sxs-lookup"><span data-stu-id="62966-224">After following this procedure, you should have a table with data in hello ORC format ready toouse.</span></span>  
