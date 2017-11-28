---
title: "Создание таблиц Hive и загрузка данных из хранилища BLOB-объектов Azure | Документация Майкрософт"
description: "Создание таблиц Hive и загрузка в них данных больших двоичных объектов"
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
ms.openlocfilehash: eca4ecd8f639bb9816903f4b1d1f999755da819c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="a0d90-103">Создание таблиц Hive и загрузка данных из хранилища BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="a0d90-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="a0d90-104">В этой статье рассматриваются общие запросы Hive, которые создают таблицы Hive и загружают данные из хранилищ BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="a0d90-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="a0d90-105">Здесь также приведены некоторые указания по секционированию таблиц Hive и использованию формата Optimized Row Columnar (ORC) для улучшения производительности запросов.</span><span class="sxs-lookup"><span data-stu-id="a0d90-105">Some guidance is also provided on partitioning Hive tables and on using the Optimized Row Columnar (ORC) formatting to improve query performance.</span></span>

<span data-ttu-id="a0d90-106">Это **меню** содержит ссылки на разделы, описывающие прием данных в целевых средах, где они могут храниться и обрабатываться процессом обработки и анализа данных группы (TDSP).</span><span class="sxs-lookup"><span data-stu-id="a0d90-106">This **menu** links to topics that describe how to ingest data into target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="a0d90-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a0d90-107">Prerequisites</span></span>
<span data-ttu-id="a0d90-108">В этой статье предполагается, что вы:</span><span class="sxs-lookup"><span data-stu-id="a0d90-108">This article assumes that you have:</span></span>

* <span data-ttu-id="a0d90-109">Создали учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="a0d90-109">Created an Azure storage account.</span></span> <span data-ttu-id="a0d90-110">Инструкции см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="a0d90-110">If you need instructions, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="a0d90-111">Подготовили настраиваемый кластер Hadoop с помощью службы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a0d90-111">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span>  <span data-ttu-id="a0d90-112">Инструкции см. в статье [Настройка кластеров Azure HDInsight Hadoop для процесса обработки и анализа данных группы](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="a0d90-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="a0d90-113">Включили удаленный доступ к кластеру, вошли в систему и открыли консоль командной строки Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a0d90-113">Enabled remote access to the cluster, logged in, and opened the Hadoop Command-Line console.</span></span> <span data-ttu-id="a0d90-114">Инструкции можно найти в разделе [Доступ к головному узлу в кластере Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="a0d90-114">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="a0d90-115">Отправка данных в хранилище больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="a0d90-115">Upload data to Azure blob storage</span></span>
<span data-ttu-id="a0d90-116">Если вы создали виртуальную машину Azure в соответствии с инструкциями в разделе [Настройка виртуальной машины Azure для расширенной аналитики](machine-learning-data-science-setup-virtual-machine.md), этот файл сценария должен быть загружен в каталог *C:\\Users\\\<имя пользователя\>\\Documents\\Data Science Scripts* на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a0d90-116">If you created an Azure virtual machine by following the instructions provided in [Set up an Azure virtual machine for advanced analytics](machine-learning-data-science-setup-virtual-machine.md), this script file should have been downloaded to the *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on the virtual machine.</span></span> <span data-ttu-id="a0d90-117">Чтобы запросы Hive были готовы к отправке, достаточно подключить свою схему данных и применить конфигурацию хранилища больших двоичных объектов Azure в соответствующих полях.</span><span class="sxs-lookup"><span data-stu-id="a0d90-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in the appropriate fields to be ready for submission.</span></span>

<span data-ttu-id="a0d90-118">Предполагается, что формат данных для таблиц Hive — табличный формат **без сжатия** и что данные отправлены в контейнер по умолчанию (или дополнительный контейнер) учетной записи хранения, которую использует кластер Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a0d90-118">We assume that the data for Hive tables is in an **uncompressed** tabular format, and that the data has been uploaded to the default (or to an additional) container of the storage account used by the Hadoop cluster.</span></span>

<span data-ttu-id="a0d90-119">Если вы хотите попрактиковаться на **наборе данных "Поездки такси Нью-Йорка"**, то необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a0d90-119">If you want to practice on the **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="a0d90-120">**скачать** 24 файла [набора данных "Поездки такси Нью-Йорка"](http://www.andresmh.com/nyctaxitrips) (12 файлов поездок и 12 файлов тарифов);</span><span class="sxs-lookup"><span data-stu-id="a0d90-120">**download** the 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="a0d90-121">**распаковать** все CSV-файлы; а затем</span><span class="sxs-lookup"><span data-stu-id="a0d90-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="a0d90-122">**передать** их в контейнер по умолчанию (или соответствующий контейнер) в учетной записи хранения Azure, которая создана с помощью процедуры, описанной в разделе [Настройка кластеров Azure HDInsight Hadoop для процесса обработки и анализа данных группы](machine-learning-data-science-customize-hadoop-cluster.md) .</span><span class="sxs-lookup"><span data-stu-id="a0d90-122">**upload** them to the default (or appropriate container) of the Azure storage account that was created by the procedure outlined in the [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="a0d90-123">Процесс отправки CSV-файла в контейнер по умолчанию в учетной записи хранения описан на этой [странице](machine-learning-data-science-process-hive-walkthrough.md#upload).</span><span class="sxs-lookup"><span data-stu-id="a0d90-123">The process to upload the .csv files to the default container on the storage account can be found on this [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span></span>

## <span data-ttu-id="a0d90-124"><a name="submit"></a>Отправка запросов Hive</span><span class="sxs-lookup"><span data-stu-id="a0d90-124"><a name="submit"></a>How to submit Hive queries</span></span>
<span data-ttu-id="a0d90-125">Инструменты для отправки запросов Hive:</span><span class="sxs-lookup"><span data-stu-id="a0d90-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="a0d90-126">Отправка запросов Hive через командную строку Hadoop в головной узел кластера Hadoop</span><span class="sxs-lookup"><span data-stu-id="a0d90-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="a0d90-127">Отправка запросов Hive с помощью редактора Hive</span><span class="sxs-lookup"><span data-stu-id="a0d90-127">Submit Hive queries with the Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="a0d90-128">Отправка запросов Hive с помощью команд PowerShell Azure</span><span class="sxs-lookup"><span data-stu-id="a0d90-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="a0d90-129">Запросы Hive похожи на SQL.</span><span class="sxs-lookup"><span data-stu-id="a0d90-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="a0d90-130">Если вы знакомы с SQL, то вам может оказаться полезной [памятка по Hive для пользователей SQL](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) .</span><span class="sxs-lookup"><span data-stu-id="a0d90-130">If you are familiar with SQL, you may find the [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="a0d90-131">Отправляя запрос Hive, вы можете указать также место назначения, в которое будут отправлены результаты обработки запроса. Местом назначения может быть экран, локальный файл в головном узле или большой двоичный объект Azure.</span><span class="sxs-lookup"><span data-stu-id="a0d90-131">When submitting a Hive query, you can also control the destination of the output from Hive queries, whether it be on the screen or to a local file on the head node or to an Azure blob.</span></span>

### <span data-ttu-id="a0d90-132"><a name="headnode"></a> 1. Отправка запросов Hive через командную строку Hadoop в головной узел кластера Hadoop</span><span class="sxs-lookup"><span data-stu-id="a0d90-132"><a name="headnode"></a> 1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="a0d90-133">Отправка сложных запросов Hive непосредственно в головном узле кластера Hadoop обычно позволяет получить ответ быстрее, чем при использовании редактора Hive или сценариев Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0d90-133">If the Hive query is complex, submitting it directly in the head node of the Hadoop cluster typically leads to faster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="a0d90-134">Войдите в головной узел кластера Hadoop, откройте командную строку Hadoop на рабочем столе головного узла и введите команду `cd %hive_home%\bin`.</span><span class="sxs-lookup"><span data-stu-id="a0d90-134">Log in to the head node of the Hadoop cluster, open the Hadoop Command Line on the desktop of the head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="a0d90-135">Отправить запрос Hive из командной строки Hadoop можно тремя способами:</span><span class="sxs-lookup"><span data-stu-id="a0d90-135">You have three ways to submit Hive queries in the Hadoop Command Line:</span></span>

* <span data-ttu-id="a0d90-136">напрямую;</span><span class="sxs-lookup"><span data-stu-id="a0d90-136">directly</span></span>
* <span data-ttu-id="a0d90-137">с помощью HQL-файлов;</span><span class="sxs-lookup"><span data-stu-id="a0d90-137">using .hql files</span></span>
* <span data-ttu-id="a0d90-138">из командной консоли Hive.</span><span class="sxs-lookup"><span data-stu-id="a0d90-138">with the Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="a0d90-139">Отправка запросов Hive непосредственно из командной строки Hadoop</span><span class="sxs-lookup"><span data-stu-id="a0d90-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="a0d90-140">Отправить простой запрос Hive непосредственно из командной строки Hadoop можно с помощью такой команды, как `hive -e "<your hive query>;` .</span><span class="sxs-lookup"><span data-stu-id="a0d90-140">You can run command like `hive -e "<your hive query>;` to submit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="a0d90-141">Ниже приведен пример, в котором красной рамкой обведена команда, которая отправляет запрос Hive, а зеленой обведены выходные данные обработки этого запроса.</span><span class="sxs-lookup"><span data-stu-id="a0d90-141">Here is an example, where the red box outlines the command that submits the Hive query, and the green box outlines the output from the Hive query.</span></span>

![Создание рабочей области](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="a0d90-143">Отправка запросов Hive в HQL-файлах</span><span class="sxs-lookup"><span data-stu-id="a0d90-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="a0d90-144">Если запрос Hive сложный и содержит несколько строк, редактировать запросы в командной строке или командной консоли Hive нецелесообразно.</span><span class="sxs-lookup"><span data-stu-id="a0d90-144">When the Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="a0d90-145">Вместо этого можно использовать текстовый редактор в головном узле кластера Hadoop для сохранения запросов Hive в HQL-файле в локальном каталоге головного узла.</span><span class="sxs-lookup"><span data-stu-id="a0d90-145">An alternative is to use a text editor in the head node of the Hadoop cluster to save the Hive queries in a .hql file in a local directory of the head node.</span></span> <span data-ttu-id="a0d90-146">Затем можно отправить запрос Hive в HQL-файле, воспользовавшись аргументом `-f` :</span><span class="sxs-lookup"><span data-stu-id="a0d90-146">Then the Hive query in the .hql file can be submitted by using the `-f` argument as follows:</span></span>

    hive -f "<path to the .hql file>"

![Создание рабочей области](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="a0d90-148">**Отменить вывод состояния хода выполнения запросов Hive на экран**</span><span class="sxs-lookup"><span data-stu-id="a0d90-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="a0d90-149">По умолчанию после отправки запроса Hive в командной строке Hadoop на экране отображается состояние хода выполнения задания Map/Reduce.</span><span class="sxs-lookup"><span data-stu-id="a0d90-149">By default, after Hive query is submitted in Hadoop Command Line, the progress of the Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="a0d90-150">Чтобы ход выполнения задания Map/Reduce не выводился на экран, можно указать в командной строке аргумент `-S` (S в верхнем регистре) как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="a0d90-150">To suppress the screen print of the Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in the command line as follows:</span></span>

    hive -S -f "<path to the .hql file>"
<span data-ttu-id="a0d90-151">.</span><span class="sxs-lookup"><span data-stu-id="a0d90-151">.</span></span>    <span data-ttu-id="a0d90-152">hive -S -e "<Hive queries>"</span><span class="sxs-lookup"><span data-stu-id="a0d90-152">hive -S -e "<Hive queries>"</span></span>

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="a0d90-153">Отправка запросов Hive в командной консоли Hive</span><span class="sxs-lookup"><span data-stu-id="a0d90-153">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="a0d90-154">Также можно сначала войти в консоль команд Hive, выполнив команду `hive` в командной строке Hadoop, и затем отправить запросы Hive в командной консоли Hive.</span><span class="sxs-lookup"><span data-stu-id="a0d90-154">You can also first enter the Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="a0d90-155">Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="a0d90-155">Here is an example.</span></span> <span data-ttu-id="a0d90-156">В этом примере красными рамками обведены команды, с помощью которых вы вошли в командную консоль Hive, и запрос Hive, отправленный в командную консоль Hive.</span><span class="sxs-lookup"><span data-stu-id="a0d90-156">In this example, the two red boxes highlight the commands used to enter the Hive command console, and the Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="a0d90-157">Зеленой рамкой выделены выходные данные запроса Hive.</span><span class="sxs-lookup"><span data-stu-id="a0d90-157">The green box highlights the output from the Hive query.</span></span>

![Создание рабочей области](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="a0d90-159">В предыдущих примерах данные обработки запроса Hive выведены прямо на экране.</span><span class="sxs-lookup"><span data-stu-id="a0d90-159">The previous examples directly output the Hive query results on screen.</span></span> <span data-ttu-id="a0d90-160">Выходные данные также можно записать в локальный файл на головном узле или в большой двоичный объект Azure.</span><span class="sxs-lookup"><span data-stu-id="a0d90-160">You can also write the output to a local file on the head node, or to an Azure blob.</span></span> <span data-ttu-id="a0d90-161">Затем можно использовать другие инструменты для дальнейшего анализа выходных данных запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="a0d90-161">Then, you can use other tools to further analyze the output of Hive queries.</span></span>

<span data-ttu-id="a0d90-162">**Вывод результатов запроса Hive в локальный файл**</span><span class="sxs-lookup"><span data-stu-id="a0d90-162">**Output Hive query results to a local file.**</span></span>
<span data-ttu-id="a0d90-163">Чтобы вывести результаты запроса Hive в локальный каталог на головном узле, следует отправить запрос Hive из командной строки Hadoop, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="a0d90-163">To output Hive query results to a local directory on the head node, you have to submit the Hive query in the Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in the head node>

<span data-ttu-id="a0d90-164">В следующем примере выходные данные запроса Hive записываются в файл `hivequeryoutput.txt` в каталоге `C:\apps\temp`.</span><span class="sxs-lookup"><span data-stu-id="a0d90-164">In the following example, the output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![Создание рабочей области](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="a0d90-166">**Вывод результатов запроса Hive в большой двоичный объект Azure**</span><span class="sxs-lookup"><span data-stu-id="a0d90-166">**Output Hive query results to an Azure blob**</span></span>

<span data-ttu-id="a0d90-167">Результаты запроса Hive также можно выводить в большой двоичный объект Azure в используемом по умолчанию контейнере кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a0d90-167">You can also output the Hive query results to an Azure blob, within the default container of the Hadoop cluster.</span></span> <span data-ttu-id="a0d90-168">Для этого используется следующий запрос Hive:</span><span class="sxs-lookup"><span data-stu-id="a0d90-168">The Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within the default container> <select clause from ...>

<span data-ttu-id="a0d90-169">В следующем примере выходные данные запроса Hive записываются в каталог большого двоичного объекта `queryoutputdir` в используемом по умолчанию контейнере кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a0d90-169">In the following example, the output of Hive query is written to a blob directory `queryoutputdir` within the default container of the Hadoop cluster.</span></span> <span data-ttu-id="a0d90-170">Здесь нужно указать только имя каталога, не указывая имя большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="a0d90-170">Here, you only need to provide the directory name, without the blob name.</span></span> <span data-ttu-id="a0d90-171">Если указать имя каталога и имя большого двоичного объекта, появится следующее сообщение об ошибке: `wasb:///queryoutputdir/queryoutput.txt`.</span><span class="sxs-lookup"><span data-stu-id="a0d90-171">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![Создание рабочей области](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="a0d90-173">При открытии используемого по умолчанию контейнера кластера Hadoop с помощью Azure Storage Explorer выходные данные запроса Hive могут выглядеть так, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="a0d90-173">If you open the default container of the Hadoop cluster using Azure Storage Explorer, you can see the output of the Hive query as shown in the following figure.</span></span> <span data-ttu-id="a0d90-174">Чтобы извлечь большие двоичные объекты только с указанными буквами в именах, можно применить фильтр (выделенный красной рамкой).</span><span class="sxs-lookup"><span data-stu-id="a0d90-174">You can apply the filter (highlighted by red box) to only retrieve the blob with specified letters in names.</span></span>

![Создание рабочей области](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <span data-ttu-id="a0d90-176"><a name="hive-editor"></a> 2. Отправка запросов Hive с помощью редактора Hive</span><span class="sxs-lookup"><span data-stu-id="a0d90-176"><a name="hive-editor"></a> 2. Submit Hive queries with the Hive Editor</span></span>
<span data-ttu-id="a0d90-177">Вы также можете использовать консоль запросов (редактор Hive). Для этого введите в веб-браузер URL-адрес в таком формате: *https://&#60;имя кластера Hadoop>.azurehdinsight.net/Home/HiveEditor*.</span><span class="sxs-lookup"><span data-stu-id="a0d90-177">You can also use the Query Console (Hive Editor) by entering a URL of the form *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="a0d90-178">Чтобы увидеть эту консоль, необходимо выполнить вход, а для этого вам потребуются ваши учетные данные для кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a0d90-178">You must be logged in the see this console and so you need your Hadoop cluster credentials here.</span></span>

### <span data-ttu-id="a0d90-179"><a name="ps"></a> 3. Отправка запросов Hive с помощью команд PowerShell Azure</span><span class="sxs-lookup"><span data-stu-id="a0d90-179"><a name="ps"></a> 3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="a0d90-180">Для отправки запросов Hive также можно использовать PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0d90-180">You can also use PowerShell to submit Hive queries.</span></span> <span data-ttu-id="a0d90-181">Инструкции см. в статье [Отправка заданий Hadoop в HDInsight](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a0d90-181">For instructions, see [Submit Hive jobs using PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span></span>

## <span data-ttu-id="a0d90-182"><a name="create-tables"></a>Создание базы данных и таблиц Hive</span><span class="sxs-lookup"><span data-stu-id="a0d90-182"><a name="create-tables"></a>Create Hive database and tables</span></span>
<span data-ttu-id="a0d90-183">Запросы Hive доступны для общего использования в [репозитории GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql), откуда их можно скачать.</span><span class="sxs-lookup"><span data-stu-id="a0d90-183">The Hive queries are shared in the [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="a0d90-184">Ниже приведен запрос Hive, который создает таблицу Hive.</span><span class="sxs-lookup"><span data-stu-id="a0d90-184">Here is the Hive query that creates a Hive table.</span></span>

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

<span data-ttu-id="a0d90-185">Здесь приведены описания полей, необходимых для подключения, и прочие конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a0d90-185">Here are the descriptions of the fields that you need to plug in and other configurations:</span></span>

* <span data-ttu-id="a0d90-186">**&#60;database name>** — имя создаваемой базы данных.</span><span class="sxs-lookup"><span data-stu-id="a0d90-186">**&#60;database name>**: the name of the database that you want to create.</span></span> <span data-ttu-id="a0d90-187">Если вы предпочитаете использовать базу данных по умолчанию, то запрос *create database...* можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="a0d90-187">If you just want to use the default database, the query *create database...* can be omitted.</span></span>
* <span data-ttu-id="a0d90-188">**&#60;table name>** — имя таблицы, создаваемой в указанной базе данных.</span><span class="sxs-lookup"><span data-stu-id="a0d90-188">**&#60;table name>**: the name of the table that you want to create within the specified database.</span></span> <span data-ttu-id="a0d90-189">Если вы хотите использовать базу данных по умолчанию, то для обращения к таблице можно указать только имя таблицы *&#60;имя_таблицы>* без указания имени базы данных.</span><span class="sxs-lookup"><span data-stu-id="a0d90-189">If you want to use the default database, the table can be directly referred by *&#60;table name>* without &#60;database name>.</span></span>
* <span data-ttu-id="a0d90-190">**&#60;field separator>** — разделитель полей в файле данных, который следует загрузить в таблицу Hive.</span><span class="sxs-lookup"><span data-stu-id="a0d90-190">**&#60;field separator>**: the separator that delimits fields in the data file to be uploaded to the Hive table.</span></span>
* <span data-ttu-id="a0d90-191">**&#60;line separator>** — разделитель строк в файле данных.</span><span class="sxs-lookup"><span data-stu-id="a0d90-191">**&#60;line separator>**: the separator that delimits lines in the data file.</span></span>
* <span data-ttu-id="a0d90-192">**&#60;storage location>** — хранилище Azure для хранения данных таблиц Hive.</span><span class="sxs-lookup"><span data-stu-id="a0d90-192">**&#60;storage location>**: the Azure storage location to save the data of Hive tables.</span></span> <span data-ttu-id="a0d90-193">Если не указывать параметр *LOCATION &#60;storage location>*, база данных и таблицы сохраняются в каталоге *hive/warehouse/* в контейнере по умолчанию для кластера Hive.</span><span class="sxs-lookup"><span data-stu-id="a0d90-193">If you do not specify *LOCATION &#60;storage location>*, the database and the tables are stored in *hive/warehouse/* directory in the default container of the Hive cluster by default.</span></span> <span data-ttu-id="a0d90-194">Если вы хотите указать место хранения, то оно должно находиться в пределах контейнера по умолчанию для базы данных и таблиц.</span><span class="sxs-lookup"><span data-stu-id="a0d90-194">If you want to specify the storage location, the storage location has to be within the default container for the database and tables.</span></span> <span data-ttu-id="a0d90-195">Это расположение необходимо указать относительно контейнера кластера по умолчанию в формате *wasb:///&#60;каталог 1>/* или *wasb:///&#60;каталог 1>/&#60;каталог 2>/* и т. д. После выполнения запроса в контейнере по умолчанию создаются соответствующие каталоги.</span><span class="sxs-lookup"><span data-stu-id="a0d90-195">This location has to be referred as location relative to the default container of the cluster in the format of *'wasb:///&#60;directory 1>/'* or *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. After the query is executed, the relative directories are created within the default container.</span></span>
* <span data-ttu-id="a0d90-196">**TBLPROPERTIES("skip.header.line.count"="1")**. Если файл данных содержит строку заголовка, необходимо добавить это свойство **в конец** запроса *create table*.</span><span class="sxs-lookup"><span data-stu-id="a0d90-196">**TBLPROPERTIES("skip.header.line.count"="1")**: If the data file has a header line, you have to add this property **at the end** of the *create table* query.</span></span> <span data-ttu-id="a0d90-197">В противном случае строка заголовка загружается в таблицу в качестве записи.</span><span class="sxs-lookup"><span data-stu-id="a0d90-197">Otherwise, the header line is loaded as a record to the table.</span></span> <span data-ttu-id="a0d90-198">Если в файле данных нет строки заголовка, в запросе эту конфигурацию можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="a0d90-198">If the data file does not have a header line, this configuration can be omitted in the query.</span></span>

## <span data-ttu-id="a0d90-199"><a name="load-data"></a>Загрузка данных в таблицы Hive</span><span class="sxs-lookup"><span data-stu-id="a0d90-199"><a name="load-data"></a>Load data to Hive tables</span></span>
<span data-ttu-id="a0d90-200">Ниже приведен запрос Hive, который загружает данные в таблицу Hive.</span><span class="sxs-lookup"><span data-stu-id="a0d90-200">Here is the Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path to blob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="a0d90-201">**&#60;path to blob data>**. Если файл BLOB-объекта, который необходимо передать в таблицу Hive, расположен в контейнере по умолчанию для кластера HDInsight Hadoop, параметр *&#60;path to blob data>* следует указать в формате *wasb:///&#60;каталог в контейнере>/&#60;имя файла большого двоичного объекта>*.</span><span class="sxs-lookup"><span data-stu-id="a0d90-201">**&#60;path to blob data>**: If the blob file to be uploaded to the Hive table is in the default container of the HDInsight Hadoop cluster, the *&#60;path to blob data>* should be in the format *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span></span> <span data-ttu-id="a0d90-202">В дополнительном контейнере кластера Hadoop под управлением службы HDInsight также может быть файл большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="a0d90-202">The blob file can also be in an additional container of the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="a0d90-203">В этом случае *&#60;путь_к_данным_большого_двоичного_объекта>* необходимо указать в формате *'wasb://&#60;имя контейнера>@&#60;имя учетной записи хранения>.blob.core.windows.net/&#60;имя файла большого двоичного объекта>'*.</span><span class="sxs-lookup"><span data-stu-id="a0d90-203">In this case, *&#60;path to blob data>* should be in the format *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="a0d90-204">Данные большого двоичного объекта, которые необходимо отправить в таблицу Hive, должны находиться в контейнере по умолчанию или в дополнительном контейнере учетной записи хранения для кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a0d90-204">The blob data to be uploaded to Hive table has to be in the default or additional container of the storage account for the Hadoop cluster.</span></span> <span data-ttu-id="a0d90-205">В противном случае запрос *LOAD DATA* завершается ошибкой доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="a0d90-205">Otherwise, the *LOAD DATA* query fails complaining that it cannot access the data.</span></span>
  >
  >

## <span data-ttu-id="a0d90-206"><a name="partition-orc"></a>Дополнительные разделы: секционированные таблицы и хранение данных Hive в формате ORC</span><span class="sxs-lookup"><span data-stu-id="a0d90-206"><a name="partition-orc"></a>Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="a0d90-207">При большом объеме данных секционирование таблицы полезно для запросов, в рамках которых требуется сканировать только несколько секций таблицы.</span><span class="sxs-lookup"><span data-stu-id="a0d90-207">If the data is large, partitioning the table is beneficial for queries that only need to scan a few partitions of the table.</span></span> <span data-ttu-id="a0d90-208">Например, целесообразно секционировать данные журнала веб-сайта по датам.</span><span class="sxs-lookup"><span data-stu-id="a0d90-208">For instance, it is reasonable to partition the log data of a web site by dates.</span></span>

<span data-ttu-id="a0d90-209">Помимо секционирования таблиц Hive данные Hive также удобно хранить в формате ORC.</span><span class="sxs-lookup"><span data-stu-id="a0d90-209">In addition to partitioning Hive tables, it is also beneficial to store the Hive data in the Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="a0d90-210">Дополнительную информацию об использовании формата ORC см. в <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">разделе о том, как использование ORC-файлов повышает производительность при чтении, записи и обработке данных Hive</a>.</span><span class="sxs-lookup"><span data-stu-id="a0d90-210">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="a0d90-211">Секционированная таблица</span><span class="sxs-lookup"><span data-stu-id="a0d90-211">Partitioned table</span></span>
<span data-ttu-id="a0d90-212">Ниже приведен запрос Hive, который создает секционированную таблицу и загружает в нее данные.</span><span class="sxs-lookup"><span data-stu-id="a0d90-212">Here is the Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path to the source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="a0d90-213">При запросах к секционированным таблицам желательно указывать условие секционирования **в начале** предложения `where`. Этот прием позволяет значительно повысить эффективность поиска.</span><span class="sxs-lookup"><span data-stu-id="a0d90-213">When querying partitioned tables, it is recommended to add the partition condition in the **beginning** of the `where` clause as this improves the efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <span data-ttu-id="a0d90-214"><a name="orc"></a>Хранение данных Hive в формате ORC</span><span class="sxs-lookup"><span data-stu-id="a0d90-214"><a name="orc"></a>Store Hive data in ORC format</span></span>
<span data-ttu-id="a0d90-215">Вы не можете загружать данные непосредственно из хранилища BLOB-объектов в таблицы Hive в формате ORC.</span><span class="sxs-lookup"><span data-stu-id="a0d90-215">You cannot directly load data from blob storage into Hive tables that is stored in the ORC format.</span></span> <span data-ttu-id="a0d90-216">Ниже приведены действия, которые необходимо выполнить, чтобы загрузить данные из больших двоичных объектов Azure в таблицы Hive в формате ORC.</span><span class="sxs-lookup"><span data-stu-id="a0d90-216">Here are the steps that the you need to take to load data from Azure blobs to Hive tables stored in ORC format.</span></span>

<span data-ttu-id="a0d90-217">Создайте внешнюю таблицу **В ВИДЕ ТЕКСТОВОГО ФАЙЛА** и загрузите в нее данные из хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="a0d90-217">Create an external table **STORED AS TEXTFILE** and load data from blob storage to the table.</span></span>

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

        LOAD DATA INPATH '<path to the source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="a0d90-218">Создайте внутреннюю таблицу, используя ту же схему и тот же разделитель полей, что и во внешней таблице на шаге 1, и сохраните данные Hive в формате ORC.</span><span class="sxs-lookup"><span data-stu-id="a0d90-218">Create an internal table with the same schema as the external table in step 1, with the same field delimiter, and store the Hive data in the ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="a0d90-219">Выберите данные во внешней таблице на шаге 1 и вставьте их в таблицу в формате ORC.</span><span class="sxs-lookup"><span data-stu-id="a0d90-219">Select data from the external table in step 1 and insert into the ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="a0d90-220">Если в таблице TEXTFILE *&#60;database name>.&#60;external textfile table name>* есть секции, команда `SELECT * FROM <database name>.<external textfile table name>`, выполняемая на шаге 3, сохраняет обозначение секции в отдельное поле в возвращаемом наборе данных.</span><span class="sxs-lookup"><span data-stu-id="a0d90-220">If the TEXTFILE table *&#60;database name>.&#60;external textfile table name>* has partitions, in STEP 3, the `SELECT * FROM <database name>.<external textfile table name>` command selects the partition variable as a field in the returned data set.</span></span> <span data-ttu-id="a0d90-221">Если попытаться вставить эти данные в *&#60;database name>.&#60;ORC table name>*, возникает ошибка, так как в схеме таблицы *&#60;database name>.&#60;ORC table name>* нет отдельного поля для обозначения секции.</span><span class="sxs-lookup"><span data-stu-id="a0d90-221">Inserting it into the *&#60;database name>.&#60;ORC table name>* fails since *&#60;database name>.&#60;ORC table name>* does not have the partition variable as a field in the table schema.</span></span> <span data-ttu-id="a0d90-222">В этом случае необходимо указать поля, которые требуется вставить в таблицу *&#60;database name>.&#60;ORC table name>*, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a0d90-222">In this case, you need to specifically select the fields to be inserted to *&#60;database name>.&#60;ORC table name>* as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="a0d90-223">Когда все данные будут вставлены в таблицу *&#60;database name>.&#60;ORC table name>*, можно безопасно удалить таблицу *&#60;external textfile table name>*, используя следующий запрос.</span><span class="sxs-lookup"><span data-stu-id="a0d90-223">It is safe to drop the *&#60;external textfile table name>* when using the following query after all data has been inserted into *&#60;database name>.&#60;ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="a0d90-224">После выполнения этой процедуры у вас должна быть готовая к использованию таблица с данными в формате ORC.</span><span class="sxs-lookup"><span data-stu-id="a0d90-224">After following this procedure, you should have a table with data in the ORC format ready to use.</span></span>  
