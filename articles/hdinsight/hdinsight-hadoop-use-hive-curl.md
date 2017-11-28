---
title: "aaaUse Hadoop Hive с перелистывание в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как отправить tooremotely Pig заданий с помощью перелистывание tooHDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6ce18163-63b5-4df6-9bb6-8fcbd4db05d8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: e725829ad2adcf3540f44375e3e87b7cdaebd15e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a><span data-ttu-id="254d4-103">Выполнение запросов Hive с Hadoop в HDInsight с помощью REST</span><span class="sxs-lookup"><span data-stu-id="254d4-103">Run Hive queries with Hadoop in HDInsight using REST</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="254d4-104">Узнайте, как toouse hello WebHCat REST API toorun Hive запросы с Hadoop в кластере Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="254d4-104">Learn how toouse hello WebHCat REST API toorun Hive queries with Hadoop on Azure HDInsight cluster.</span></span>

<span data-ttu-id="254d4-105">[Curl](http://curl.haxx.se/) — используется toodemonstrate о взаимодействии с HDInsight с помощью необработанных запросов HTTP.</span><span class="sxs-lookup"><span data-stu-id="254d4-105">[Curl](http://curl.haxx.se/) is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests.</span></span> <span data-ttu-id="254d4-106">Hello [jq](http://stedolan.github.io/jq/) программа — используется tooprocess hello JSON данные, возвращенные из запросов REST.</span><span class="sxs-lookup"><span data-stu-id="254d4-106">hello [jq](http://stedolan.github.io/jq/) utility is used tooprocess hello JSON data returned from REST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="254d4-107">Если вы уже знакомы с использованием серверов под управлением Linux Hadoop, но являются новый tooHDInsight, см. раздел hello [необходимые tooknow о Hadoop в HDInsight под управлением Linux](hdinsight-hadoop-linux-information.md) документа.</span><span class="sxs-lookup"><span data-stu-id="254d4-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see hello [What you need tooknow about Hadoop on Linux-based HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>

## <span data-ttu-id="254d4-108"><a id="curl"></a>Выполнение запросов Hive</span><span class="sxs-lookup"><span data-stu-id="254d4-108"><a id="curl"></a>Run Hive queries</span></span>

> [!NOTE]
> <span data-ttu-id="254d4-109">При использовании перелистывания или любые другие связи REST с WebHCat, должен пройти проверку подлинности запросы hello, предоставляя hello имя пользователя и пароль администратора кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="254d4-109">When using cURL or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span>
>
> <span data-ttu-id="254d4-110">Hello команды в этом разделе, замените **USERNAME** tooauthenticate toohello hello пользователя кластера и заменить **пароль** hello пароль для учетной записи пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="254d4-110">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="254d4-111">Замените **CLUSTERNAME** с hello имя кластера.</span><span class="sxs-lookup"><span data-stu-id="254d4-111">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
>
> <span data-ttu-id="254d4-112">Hello API-интерфейса REST является защищен с помощью [обычной проверки подлинности](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="254d4-112">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="254d4-113">toohelp убедитесь, что учетные данные безопасно всегда отправляются серверу toohello, выполнение запросов с использованием безопасного HTTP (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="254d4-113">toohelp ensure that your credentials are securely sent toohello server, always make requests by using Secure HTTP (HTTPS).</span></span>

1. <span data-ttu-id="254d4-114">Из командной строки используйте следующие команды tooverify, возможность подключения кластера HDInsight tooyour hello:</span><span class="sxs-lookup"><span data-stu-id="254d4-114">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="254d4-115">Появится примерно toohello ответа, следующий текст:</span><span class="sxs-lookup"><span data-stu-id="254d4-115">You receive a response similar toohello following text:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="254d4-116">Ниже приведены параметры Hello, использованный в этой команде.</span><span class="sxs-lookup"><span data-stu-id="254d4-116">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="254d4-117">**-u** -hello имя пользователя и пароль используются tooauthenticate hello запроса.</span><span class="sxs-lookup"><span data-stu-id="254d4-117">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="254d4-118">**-G** — указывает, что это запрос, являющийся операцией GET.</span><span class="sxs-lookup"><span data-stu-id="254d4-118">**-G** - Indicates that this request is a GET operation.</span></span>

     <span data-ttu-id="254d4-119">Здравствуйте, начало hello URL-адрес, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, hello одинаково для всех запросов.</span><span class="sxs-lookup"><span data-stu-id="254d4-119">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span> <span data-ttu-id="254d4-120">путь Hello **параметр/Status**, указывает, что hello запрос tooreturn состояние WebHCat (также известный как Templeton) для сервера hello.</span><span class="sxs-lookup"><span data-stu-id="254d4-120">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> <span data-ttu-id="254d4-121">Можно также запросить hello версии Hive с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="254d4-121">You can also request hello version of Hive by using hello following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     <span data-ttu-id="254d4-122">Этот запрос возвращает аналогичные toohello ответа, следующий текст:</span><span class="sxs-lookup"><span data-stu-id="254d4-122">This request returns a response similar toohello following text:</span></span>

       <span data-ttu-id="254d4-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}.</span><span class="sxs-lookup"><span data-stu-id="254d4-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span></span>

2. <span data-ttu-id="254d4-124">Используйте hello, следуя toocreate таблицу с именем **log4jLogs**:</span><span class="sxs-lookup"><span data-stu-id="254d4-124">Use hello following toocreate a table named **log4jLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="254d4-125">Привет, следующие параметры, используемые с этим запросом:</span><span class="sxs-lookup"><span data-stu-id="254d4-125">hello following parameters used with this request:</span></span>

   * <span data-ttu-id="254d4-126">**-d** — с момента `-G` не используется, hello запроса по умолчанию используется метод POST toohello.</span><span class="sxs-lookup"><span data-stu-id="254d4-126">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="254d4-127">`-d`Указывает hello значения данных, отправляемых с запросом hello.</span><span class="sxs-lookup"><span data-stu-id="254d4-127">`-d` specifies hello data values that are sent with hello request.</span></span>

     * <span data-ttu-id="254d4-128">**User.Name** -hello пользователя, на котором выполняется команда hello.</span><span class="sxs-lookup"><span data-stu-id="254d4-128">**user.name** - hello user that is running hello command.</span></span>
     * <span data-ttu-id="254d4-129">**выполнение** -hello tooexecute операторы HiveQL.</span><span class="sxs-lookup"><span data-stu-id="254d4-129">**execute** - hello HiveQL statements tooexecute.</span></span>
     * <span data-ttu-id="254d4-130">**statusdir** -записывается hello каталог, в котором hello состояния для данного задания.</span><span class="sxs-lookup"><span data-stu-id="254d4-130">**statusdir** - hello directory that hello status for this job is written to.</span></span>

     <span data-ttu-id="254d4-131">Эти операторы выполняют hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="254d4-131">These statements perform hello following actions:</span></span>
   * <span data-ttu-id="254d4-132">**DROP TABLE** -Если hello таблица уже существует, она будет удалена.</span><span class="sxs-lookup"><span data-stu-id="254d4-132">**DROP TABLE** - If hello table already exists, it is deleted.</span></span>
   * <span data-ttu-id="254d4-133">**CREATE EXTERNAL TABLE** : создание новой "внешней" таблицы в Hive.</span><span class="sxs-lookup"><span data-stu-id="254d4-133">**CREATE EXTERNAL TABLE** - Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="254d4-134">Внешние таблицы хранить только определение таблицы hello в кусте.</span><span class="sxs-lookup"><span data-stu-id="254d4-134">External tables store only hello table definition in Hive.</span></span> <span data-ttu-id="254d4-135">Hello данные остаются в исходном расположении hello.</span><span class="sxs-lookup"><span data-stu-id="254d4-135">hello data is left in hello original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="254d4-136">Внешние таблицы следует использовать, если ожидается hello toobe базовых данных обновлены из внешнего источника.</span><span class="sxs-lookup"><span data-stu-id="254d4-136">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="254d4-137">Например, процессом автоматизированной передачи данных или другой операцией MapReduce.</span><span class="sxs-lookup"><span data-stu-id="254d4-137">For example, an automated data upload process or another MapReduce operation.</span></span>
     >
     > <span data-ttu-id="254d4-138">Удаление внешней таблицы **не** удаление данных hello, только определение таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="254d4-138">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

   * <span data-ttu-id="254d4-139">**ФОРМАТ СТРОК** — как формат данных hello.</span><span class="sxs-lookup"><span data-stu-id="254d4-139">**ROW FORMAT** - How hello data is formatted.</span></span> <span data-ttu-id="254d4-140">поля Hello в каждом журнале разделенные пробелом.</span><span class="sxs-lookup"><span data-stu-id="254d4-140">hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="254d4-141">**ХРАНИМЫЕ РАСПОЛОЖЕНИЕ текстового файла AS** — там, где хранятся данные hello (hello данные примера и каталог) и что он хранится в виде текста.</span><span class="sxs-lookup"><span data-stu-id="254d4-141">**STORED AS TEXTFILE LOCATION** - Where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="254d4-142">**ВЫБЕРИТЕ** -выбирает число всех строк где столбца **t4** содержит значение hello **[ошибка]**.</span><span class="sxs-lookup"><span data-stu-id="254d4-142">**SELECT** - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="254d4-143">Эта инструкция возвращает значение **3**, так как данное значение содержат три строки.</span><span class="sxs-lookup"><span data-stu-id="254d4-143">This statement returns a value of **3** as there are three rows that contain this value.</span></span>

     > [!NOTE]
     > <span data-ttu-id="254d4-144">Обратите внимание, что hello пробелы между инструкциями HiveQL заменяются hello `+` символов при использовании с Curl.</span><span class="sxs-lookup"><span data-stu-id="254d4-144">Notice that hello spaces between HiveQL statements are replaced by hello `+` character when used with Curl.</span></span> <span data-ttu-id="254d4-145">Заключенные в кавычки значения, содержащие символ пробела, такие как разделитель hello не заменяется `+`.</span><span class="sxs-lookup"><span data-stu-id="254d4-145">Quoted values that contain a space, such as hello delimiter, should not be replaced by `+`.</span></span>

   * <span data-ttu-id="254d4-146">**INPUT__FILE__NAME как «% 25.log»** — это инструкция ограничения hello поиска tooonly использовать файлы которых заканчиваются. журнала.</span><span class="sxs-lookup"><span data-stu-id="254d4-146">**INPUT__FILE__NAME LIKE '%25.log'** - This statement limits hello search tooonly use files ending in .log.</span></span>

     > [!NOTE]
     > <span data-ttu-id="254d4-147">Hello `%25` является форма URL-кодированием hello %, поэтому фактические условия hello `like '%.log'`.</span><span class="sxs-lookup"><span data-stu-id="254d4-147">hello `%25` is hello URL encoded form of %, so hello actual condition is `like '%.log'`.</span></span> <span data-ttu-id="254d4-148">Hello % имеет URL-адрес toobe кодировке, как он интерпретируется как специальный символ в URL-адресах.</span><span class="sxs-lookup"><span data-stu-id="254d4-148">hello % has toobe URL encoded, as it is treated as a special character in URLs.</span></span>

     <span data-ttu-id="254d4-149">Эта команда должна возвращать идентификатора задания, который может быть используется toocheck hello состояние задания hello.</span><span class="sxs-lookup"><span data-stu-id="254d4-149">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

       <span data-ttu-id="254d4-150">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="254d4-150">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="254d4-151">состояние hello toocheck задания hello, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="254d4-151">toocheck hello status of hello job, use hello following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="254d4-152">Замените **JOBID** с hello значение, возвращенное в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="254d4-152">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="254d4-153">Например, если hello, возвращают значение было `{"id":"job_1415651640909_0026"}`, затем **JOBID** бы `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="254d4-153">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="254d4-154">Если задание hello завершена, он имеет состояние hello **успешно**.</span><span class="sxs-lookup"><span data-stu-id="254d4-154">If hello job has finished, hello state is **SUCCEEDED**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="254d4-155">Этот запрос перелистывание возвращает документ нотации объектов JavaScript (JSON) с сведения о задании hello.</span><span class="sxs-lookup"><span data-stu-id="254d4-155">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job.</span></span> <span data-ttu-id="254d4-156">Используется Jq tooretrieve только hello значение состояния.</span><span class="sxs-lookup"><span data-stu-id="254d4-156">Jq is used tooretrieve only hello state value.</span></span>

4. <span data-ttu-id="254d4-157">После hello состояние задания hello изменилось слишком**успешно**, результаты hello hello задания можно получить из хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="254d4-157">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="254d4-158">Hello `statusdir` параметр, передаваемый с запросом hello содержит расположение hello hello выходного файла; в данном случае **/пример/перелистывание**.</span><span class="sxs-lookup"><span data-stu-id="254d4-158">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **/example/curl**.</span></span> <span data-ttu-id="254d4-159">Этот адрес hello результаты сохраняются hello **примере/перелистывание** каталог в hello кластеров хранения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="254d4-159">This address stores hello output in hello **example/curl** directory in hello clusters default storage.</span></span>

    <span data-ttu-id="254d4-160">Можно перечислить и загрузить эти файлы с помощью hello [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="254d4-160">You can list and download these files by using hello [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="254d4-161">Дополнительные сведения об использовании hello Azure CLI со службой хранилища Azure см. в разделе hello [использование Azure CLI 2.0 со службой хранилища Azure](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) документа.</span><span class="sxs-lookup"><span data-stu-id="254d4-161">For more information on using hello Azure CLI with Azure Storage, see hello [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span></span>

5. <span data-ttu-id="254d4-162">Hello используйте следующие инструкции toocreate новую таблицу «internal» с именем **журналы ошибок**:</span><span class="sxs-lookup"><span data-stu-id="254d4-162">Use hello following statements toocreate a new 'internal' table named **errorLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="254d4-163">Эти операторы выполняют hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="254d4-163">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="254d4-164">**CREATE TABLE IF NOT EXISTS** : создание таблицы, если она до этого не существовала.</span><span class="sxs-lookup"><span data-stu-id="254d4-164">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="254d4-165">Эта инструкция создает внутренней таблицы, которые хранятся в хранилище данных Hive hello и полностью управляются Hive.</span><span class="sxs-lookup"><span data-stu-id="254d4-165">This statement creates an internal table, which is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="254d4-166">В отличие от внешних таблиц при удалении внутренней таблицы удаляются hello базовые данные.</span><span class="sxs-lookup"><span data-stu-id="254d4-166">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

   * <span data-ttu-id="254d4-167">**ORC ХРАНИМОЙ AS** -хранит данные hello в оптимизированные строк по столбцам (формат ORC.).</span><span class="sxs-lookup"><span data-stu-id="254d4-167">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="254d4-168">Это высокооптимизированный и эффективный формат для хранения данных Hive.</span><span class="sxs-lookup"><span data-stu-id="254d4-168">ORC is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="254d4-169">**INSERT OVERWRITE ... ВЫБЕРИТЕ** -выбирает строки из hello **log4jLogs** таблицы, которые содержат **[ошибка]**, а затем вставки данных hello в hello **журналы ошибок** таблицы.</span><span class="sxs-lookup"><span data-stu-id="254d4-169">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>
   * <span data-ttu-id="254d4-170">**ВЫБЕРИТЕ** -выбирает все строки из нового hello **журналы ошибок** таблицы.</span><span class="sxs-lookup"><span data-stu-id="254d4-170">**SELECT** - Selects all rows from hello new **errorLogs** table.</span></span>

6. <span data-ttu-id="254d4-171">Используйте идентификатор задания hello, возвращенное состояние hello toocheck hello задания.</span><span class="sxs-lookup"><span data-stu-id="254d4-171">Use hello job ID returned toocheck hello status of hello job.</span></span> <span data-ttu-id="254d4-172">После его успешного использования hello Azure CLI, как описано ранее toodownload и просмотр результатов hello.</span><span class="sxs-lookup"><span data-stu-id="254d4-172">Once it has succeeded, use hello Azure CLI as described previously toodownload and view hello results.</span></span> <span data-ttu-id="254d4-173">Hello выход должен содержать три строки, которые содержат **[ошибка]**.</span><span class="sxs-lookup"><span data-stu-id="254d4-173">hello output should contain three lines, all of which contain **[ERROR]**.</span></span>

## <span data-ttu-id="254d4-174"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="254d4-174"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="254d4-175">Общая информация об использовании Hive в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="254d4-175">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="254d4-176">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="254d4-176">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="254d4-177">Дополнительная информация о других способах работы с Hadoop в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="254d4-177">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="254d4-178">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="254d4-178">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="254d4-179">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="254d4-179">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="254d4-180">При использовании Tez с куста см. следующие документы отладочной информации hello:</span><span class="sxs-lookup"><span data-stu-id="254d4-180">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="254d4-181">Использовать hello Ambari Tez представление на основе Linux HDInsight</span><span class="sxs-lookup"><span data-stu-id="254d4-181">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

<span data-ttu-id="254d4-182">Дополнительные сведения о hello API REST, используемые в этом документе в разделе hello [WebHCat ссылки](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) документа.</span><span class="sxs-lookup"><span data-stu-id="254d4-182">For more information on hello REST API used in this document, see hello [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span></span>

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


