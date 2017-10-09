---
title: "aaaGet к работе с примером HBase на HDInsight - Azure | Документы Microsoft"
description: "Выполните этот пример toostart Apache HBase, с помощью hadoop в HDInsight. Создание таблиц из оболочки HBase hello, а также запросить с помощью Hive."
keywords: "hbasecommand, пример hbase"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 4d6a2658-6b19-4268-95ee-822890f5a33a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 43419780142b320b16180a2b1f25020dee2f7a11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a><span data-ttu-id="5950f-105">Начало работы с примером Apache HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="5950f-105">Get started with an Apache HBase example in HDInsight</span></span>

<span data-ttu-id="5950f-106">Узнайте, как создать таблицы в HBase toocreate кластер HBase в HDInsight и запросы к таблицам с помощью Hive.</span><span class="sxs-lookup"><span data-stu-id="5950f-106">Learn how toocreate an HBase cluster in HDInsight, create HBase tables, and query tables by using Hive.</span></span> <span data-ttu-id="5950f-107">Для получения общих сведений по HBase обратитесь к разделу [Что такое HBase в HDInsight][hdinsight-hbase-overview].</span><span class="sxs-lookup"><span data-stu-id="5950f-107">For general HBase information, see [HDInsight HBase overview][hdinsight-hbase-overview].</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a><span data-ttu-id="5950f-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5950f-108">Prerequisites</span></span>
<span data-ttu-id="5950f-109">Прежде чем начать, в этом примере HBase попытки, необходимо иметь hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="5950f-109">Before you begin trying this HBase example, you must have hello following items:</span></span>

* <span data-ttu-id="5950f-110">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="5950f-110">**An Azure subscription**.</span></span> <span data-ttu-id="5950f-111">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5950f-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="5950f-112">[Secure Shell(SSH).](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="5950f-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> 
* <span data-ttu-id="5950f-113">[curl](http://curl.haxx.se/download.html).</span><span class="sxs-lookup"><span data-stu-id="5950f-113">[curl](http://curl.haxx.se/download.html).</span></span>

## <a name="create-hbase-cluster"></a><span data-ttu-id="5950f-114">Создание кластера HBase</span><span class="sxs-lookup"><span data-stu-id="5950f-114">Create HBase cluster</span></span>
<span data-ttu-id="5950f-115">Hello следующая процедура использует toocreate шаблона диспетчера ресурсов Azure версии 3.4 HBase под управлением Linux кластера и hello зависимых по умолчанию учетная запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="5950f-115">hello following procedure uses an Azure Resource Manager template toocreate a version 3.4 Linux-based HBase cluster and hello dependent default Azure Storage account.</span></span> <span data-ttu-id="5950f-116">toounderstand hello параметров, используемых в процедуре hello и другие методы создания кластера, в разделе [кластеров под управлением Linux, создать Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="5950f-116">toounderstand hello parameters used in hello procedure and other cluster creation methods, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="5950f-117">Щелкните hello следующий шаблон hello tooopen изображения в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5950f-117">Click hello following image tooopen hello template in hello Azure portal.</span></span> <span data-ttu-id="5950f-118">Hello шаблон находится в большой двоичный объект открытого контейнера.</span><span class="sxs-lookup"><span data-stu-id="5950f-118">hello template is located in a public blob container.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="5950f-119">Из hello **развертывания пользовательского** колонке введите hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="5950f-119">From hello **Custom deployment** blade, enter hello following values:</span></span>
   
   * <span data-ttu-id="5950f-120">**Подписки**: выберите подписку Azure, используемых toocreate hello кластера.</span><span class="sxs-lookup"><span data-stu-id="5950f-120">**Subscription**: Select your Azure subscription that is used toocreate hello cluster.</span></span>
   * <span data-ttu-id="5950f-121">**Группа ресурсов**: создайте группу ресурсов Azure или выберите существующую.</span><span class="sxs-lookup"><span data-stu-id="5950f-121">**Resource group**: Create an Azure Resource Management group or use an existing one.</span></span>
   * <span data-ttu-id="5950f-122">**Расположение**: укажите расположение hello hello группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5950f-122">**Location**: Specify hello location of hello resource group.</span></span> 
   * <span data-ttu-id="5950f-123">**Имя_кластера**: Введите имя кластера HBase hello.</span><span class="sxs-lookup"><span data-stu-id="5950f-123">**ClusterName**: Enter a name for hello HBase cluster.</span></span>
   * <span data-ttu-id="5950f-124">**Имя входа и пароль кластера**: имя для входа по умолчанию hello **администратора**.</span><span class="sxs-lookup"><span data-stu-id="5950f-124">**Cluster login name and password**: hello default login name is **admin**.</span></span>
   * <span data-ttu-id="5950f-125">**SSH имя пользователя и пароль**: имя пользователя по умолчанию hello **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="5950f-125">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="5950f-126">Это имя можно изменить.</span><span class="sxs-lookup"><span data-stu-id="5950f-126">You can rename it.</span></span>
     
     <span data-ttu-id="5950f-127">Все остальные параметры являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="5950f-127">Other parameters are optional.</span></span>  
     
     <span data-ttu-id="5950f-128">У каждого кластера есть зависимость учетной записи хранения для службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="5950f-128">Each cluster has an Azure Storage account dependency.</span></span> <span data-ttu-id="5950f-129">После удаления кластера hello данные сохраняются в учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="5950f-129">After you delete a cluster, hello data retains in hello storage account.</span></span> <span data-ttu-id="5950f-130">Имя учетной записи хранения по умолчанию Hello кластера — имя кластера hello без «store» добавлено.</span><span class="sxs-lookup"><span data-stu-id="5950f-130">hello cluster default storage account name is hello cluster name with "store" appended.</span></span> <span data-ttu-id="5950f-131">Это жестко задано в разделе переменных шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="5950f-131">It is hardcoded in hello template variables section.</span></span>
3. <span data-ttu-id="5950f-132">Выберите **я принимаю условия, указанных выше, toohello**, а затем нажмите кнопку **покупки**.</span><span class="sxs-lookup"><span data-stu-id="5950f-132">Select **I agree toohello terms and conditions stated above**, and then click **Purchase**.</span></span> <span data-ttu-id="5950f-133">Занимает около 20 минут toocreate кластера.</span><span class="sxs-lookup"><span data-stu-id="5950f-133">It takes about 20 minutes toocreate a cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="5950f-134">После удаления кластер HBase, можно создать другой кластер HBase с помощью hello же контейнер больших двоичных объектов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5950f-134">After an HBase cluster is deleted, you can create another HBase cluster by using hello same default blob container.</span></span> <span data-ttu-id="5950f-135">новый кластер Hello забирает hello HBase таблицы, которые вы создали в исходном кластере hello.</span><span class="sxs-lookup"><span data-stu-id="5950f-135">hello new cluster picks up hello HBase tables you created in hello original cluster.</span></span> <span data-ttu-id="5950f-136">tooavoid несогласованности, рекомендуется отключить hello HBase таблиц перед удалением hello кластера.</span><span class="sxs-lookup"><span data-stu-id="5950f-136">tooavoid inconsistencies, we recommend that you disable hello HBase tables before you delete hello cluster.</span></span>
> 
> 

## <a name="create-tables-and-insert-data"></a><span data-ttu-id="5950f-137">Создание таблиц и вставка данных</span><span class="sxs-lookup"><span data-stu-id="5950f-137">Create tables and insert data</span></span>
<span data-ttu-id="5950f-138">Можно использовать SSH tooconnect tooHBase кластеров и затем с помощью оболочки HBase toocreate HBase таблицы, вставка данных и запроса данных.</span><span class="sxs-lookup"><span data-stu-id="5950f-138">You can use SSH tooconnect tooHBase clusters and then use HBase Shell toocreate HBase tables, insert data, and query data.</span></span> <span data-ttu-id="5950f-139">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5950f-139">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="5950f-140">Для большинства пользователей данные отображаются в табличном формате hello:</span><span class="sxs-lookup"><span data-stu-id="5950f-140">For most people, data appears in hello tabular format:</span></span>

![Табличные данные HDInsight HBase][img-hbase-sample-data-tabular]

<span data-ttu-id="5950f-142">В HBase (реализацию BigTable) hello же данных имеет следующий вид:</span><span class="sxs-lookup"><span data-stu-id="5950f-142">In HBase (an implementation of BigTable), hello same data looks like:</span></span>

![Данные BigTable HDInsight HBase][img-hbase-sample-data-bigtable]


<span data-ttu-id="5950f-144">**hello toouse оболочки HBase**</span><span class="sxs-lookup"><span data-stu-id="5950f-144">**toouse hello HBase shell**</span></span>

1. <span data-ttu-id="5950f-145">В SSH выполните следующую команду HBase hello.</span><span class="sxs-lookup"><span data-stu-id="5950f-145">From SSH, run hello following HBase command:</span></span>
   
    ```bash
    hbase shell
    ```

2. <span data-ttu-id="5950f-146">Создайте HBase с двумя столбцами:</span><span class="sxs-lookup"><span data-stu-id="5950f-146">Create an HBase with two-column families:</span></span>

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. <span data-ttu-id="5950f-147">Вставьте какие-либо данные:</span><span class="sxs-lookup"><span data-stu-id="5950f-147">Insert some data:</span></span>
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![Оболочка HDInsight Hadoop HBase][img-hbase-shell]
4. <span data-ttu-id="5950f-149">Получите одну строку</span><span class="sxs-lookup"><span data-stu-id="5950f-149">Get a single row</span></span>
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    <span data-ttu-id="5950f-150">Вы увидите hello же результаты, как с помощью команды проверки hello, поскольку имеется только одна строка.</span><span class="sxs-lookup"><span data-stu-id="5950f-150">You shall see hello same results as using hello scan command because there is only one row.</span></span>
   
    <span data-ttu-id="5950f-151">Дополнительные сведения о схеме таблицы в HBase hello см. в разделе [tooHBase введение структуре схемы][hbase-schema].</span><span class="sxs-lookup"><span data-stu-id="5950f-151">For more information about hello HBase table schema, see [Introduction tooHBase Schema Design][hbase-schema].</span></span> <span data-ttu-id="5950f-152">Дополнительные команды HBase см. в [справочнике по Apache HBase][hbase-quick-start].</span><span class="sxs-lookup"><span data-stu-id="5950f-152">For more HBase commands, see [Apache HBase reference guide][hbase-quick-start].</span></span>
5. <span data-ttu-id="5950f-153">Выйти из оболочки hello</span><span class="sxs-lookup"><span data-stu-id="5950f-153">Exit hello shell</span></span>
   
    ```hbaseshell
    exit
    ```

<span data-ttu-id="5950f-154">**toobulk загрузки данных в таблицу HBase hello контактов**</span><span class="sxs-lookup"><span data-stu-id="5950f-154">**toobulk load data into hello contacts HBase table**</span></span>

<span data-ttu-id="5950f-155">HBase включает несколько методов загрузки данных в таблицы.</span><span class="sxs-lookup"><span data-stu-id="5950f-155">HBase includes several methods of loading data into tables.</span></span>  <span data-ttu-id="5950f-156">Для получения дополнительных сведений обратитесь к разделу [Массовая загрузка](http://hbase.apache.org/book.html#arch.bulk.load).</span><span class="sxs-lookup"><span data-stu-id="5950f-156">For more information, see [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load).</span></span>

<span data-ttu-id="5950f-157">Пример файла данных находится в общедоступном контейнере больших двоичных объектов *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span><span class="sxs-lookup"><span data-stu-id="5950f-157">A sample data file can be found in a public blob container, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span></span>  <span data-ttu-id="5950f-158">Hello содержимое файла данных hello является:</span><span class="sxs-lookup"><span data-stu-id="5950f-158">hello content of hello data file is:</span></span>

    8396    Calvin Raji      230-555-0191    230-555-0191    5415 San Gabriel Dr.
    16600   Karen Wu         646-555-0113    230-555-0192    9265 La Paz
    4324    Karl Xie         508-555-0163    230-555-0193    4912 La Vuelta
    16891   Jonn Jackson     674-555-0110    230-555-0194    40 Ellis St.
    3273    Miguel Miller    397-555-0155    230-555-0195    6696 Anchor Drive
    3588    Osa Agbonile     592-555-0152    230-555-0196    1873 Lion Circle
    10272   Julia Lee        870-555-0110    230-555-0197    3148 Rose Street
    4868    Jose Hayes       599-555-0171    230-555-0198    793 Crawford Street
    4761    Caleb Alexander  670-555-0141    230-555-0199    4775 Kentucky Dr.
    16443   Terry Chander    998-555-0171    230-555-0200    771 Northridge Drive

<span data-ttu-id="5950f-159">При необходимости можно создать текстовый файл и отправить файл hello tooyour собственную учетную.</span><span class="sxs-lookup"><span data-stu-id="5950f-159">You can optionally create a text file and upload hello file tooyour own storage account.</span></span> <span data-ttu-id="5950f-160">Hello инструкции см. в разделе [передать данные для заданий Hadoop в HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="5950f-160">For hello instructions, see [Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data].</span></span>

> [!NOTE]
> <span data-ttu-id="5950f-161">Эта процедура использует таблицу HBase контакты hello, созданный в последней процедуры hello.</span><span class="sxs-lookup"><span data-stu-id="5950f-161">This procedure uses hello Contacts HBase table you have created in hello last procedure.</span></span>
> 

1. <span data-ttu-id="5950f-162">Запустите из SSH, следующая команда tootransform hello в файле tooStoreFiles данных и хранить в относительный путь, указанный Dimporttsv.bulk.output hello.</span><span class="sxs-lookup"><span data-stu-id="5950f-162">From SSH, run hello following command tootransform hello data file tooStoreFiles and store at a relative path specified by Dimporttsv.bulk.output.</span></span>  <span data-ttu-id="5950f-163">Если вы находитесь в оболочку HBase, используйте tooexit команду выхода hello.</span><span class="sxs-lookup"><span data-stu-id="5950f-163">If you are in HBase Shell, use hello exit command tooexit.</span></span>

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. <span data-ttu-id="5950f-164">Выполните следующие команды tooupload hello данные из таблицы HBase toohello /example/data/storeDataFileOutput hello.</span><span class="sxs-lookup"><span data-stu-id="5950f-164">Run hello following command tooupload hello data from  /example/data/storeDataFileOutput toohello HBase table:</span></span>
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. <span data-ttu-id="5950f-165">Откройте оболочку HBase hello и использовать hello hello сканирования команда toolist содержимое таблицы.</span><span class="sxs-lookup"><span data-stu-id="5950f-165">You can open hello HBase shell, and use hello scan command toolist hello table content.</span></span>

## <a name="use-hive-tooquery-hbase"></a><span data-ttu-id="5950f-166">Используйте куст tooquery HBase</span><span class="sxs-lookup"><span data-stu-id="5950f-166">Use Hive tooquery HBase</span></span>

<span data-ttu-id="5950f-167">Можно запросить данные в таблицах HBase с помощью Hive.</span><span class="sxs-lookup"><span data-stu-id="5950f-167">You can query data in HBase tables by using Hive.</span></span> <span data-ttu-id="5950f-168">В этом разделе, можно создать таблицу Hive, сопоставляется таблице HBase toohello и использует tooquery hello данных в таблице HBase.</span><span class="sxs-lookup"><span data-stu-id="5950f-168">In this section, you create a Hive table that maps toohello HBase table and uses it tooquery hello data in your HBase table.</span></span>

1. <span data-ttu-id="5950f-169">Откройте **PuTTY**и подключите toohello кластер.</span><span class="sxs-lookup"><span data-stu-id="5950f-169">Open **PuTTY**, and connect toohello cluster.</span></span>  <span data-ttu-id="5950f-170">См. инструкции hello в предыдущей процедуре hello.</span><span class="sxs-lookup"><span data-stu-id="5950f-170">See hello instructions in hello previous procedure.</span></span>
2. <span data-ttu-id="5950f-171">Из сеанса SSH hello используйте следующие команды toostart Beeline hello:</span><span class="sxs-lookup"><span data-stu-id="5950f-171">From hello SSH session, use hello following command toostart Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="5950f-172">Дополнительные сведения о Beeline см. в статье [Использование Hive с Hadoop в HDInsight с применением Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="5950f-172">For more information about Beeline, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
       
3. <span data-ttu-id="5950f-173">Запустите следующие toocreate сценарий HiveQL hello таблицу Hive, который сопоставляется таблице HBase toohello.</span><span class="sxs-lookup"><span data-stu-id="5950f-173">Run hello following HiveQL script  toocreate a Hive table that maps toohello HBase table.</span></span> <span data-ttu-id="5950f-174">Убедитесь, что вы создали образец таблицы hello ссылается ранее в этом учебнике с помощью оболочки HBase hello, перед выполнением этой инструкции.</span><span class="sxs-lookup"><span data-stu-id="5950f-174">Make sure that you have created hello sample table referenced earlier in this tutorial by using hello HBase shell before you run this statement.</span></span>

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. <span data-ttu-id="5950f-175">Выполните следующие данные hello tooquery сценарий HiveQL в таблице HBase hello hello.</span><span class="sxs-lookup"><span data-stu-id="5950f-175">Run hello following HiveQL script tooquery hello data in hello HBase table:</span></span>

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a><span data-ttu-id="5950f-176">Использование API REST для HBase</span><span class="sxs-lookup"><span data-stu-id="5950f-176">Use HBase REST APIs using Curl</span></span>

<span data-ttu-id="5950f-177">Hello API-интерфейса REST является защищен с помощью [обычной проверки подлинности](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="5950f-177">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="5950f-178">Всегда должны выполнять запросы с помощью безопасного HTTP (HTTPS) toohelp убедитесь, что учетные данные безопасно отправляются toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="5950f-178">You shall always make requests by using Secure HTTP (HTTPS) toohelp ensure that your credentials are securely sent toohello server.</span></span>

2. <span data-ttu-id="5950f-179">Используйте следующие команды toolist hello существующей таблицы, HBase hello.</span><span class="sxs-lookup"><span data-stu-id="5950f-179">Use hello following command toolist hello existing HBase tables:</span></span>

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. <span data-ttu-id="5950f-180">Используйте hello, следующая команда toocreate новая таблица с двумя столбцами семейства HBase:</span><span class="sxs-lookup"><span data-stu-id="5950f-180">Use hello following command toocreate a new HBase table with two-column families:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    <span data-ttu-id="5950f-181">Схема Hello предоставляется в формате JSon hello.</span><span class="sxs-lookup"><span data-stu-id="5950f-181">hello schema is provided in hello JSon format.</span></span>
4. <span data-ttu-id="5950f-182">Используйте следующие команды tooinsert hello некоторые данные:</span><span class="sxs-lookup"><span data-stu-id="5950f-182">Use hello following command tooinsert some data:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    <span data-ttu-id="5950f-183">Необходимо base64 кодирования hello значениями, указанными в параметр -d hello.</span><span class="sxs-lookup"><span data-stu-id="5950f-183">You must base64 encode hello values specified in hello -d switch.</span></span> <span data-ttu-id="5950f-184">В примере hello:</span><span class="sxs-lookup"><span data-stu-id="5950f-184">In hello example:</span></span>
   
   * <span data-ttu-id="5950f-185">MTAwMA==: 1000;</span><span class="sxs-lookup"><span data-stu-id="5950f-185">MTAwMA==: 1000</span></span>
   * <span data-ttu-id="5950f-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span><span class="sxs-lookup"><span data-stu-id="5950f-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span></span>
   * <span data-ttu-id="5950f-187">Sm9obiBEb2xl: John Dole.</span><span class="sxs-lookup"><span data-stu-id="5950f-187">Sm9obiBEb2xl: John Dole</span></span>
     
     <span data-ttu-id="5950f-188">[false ключ строки](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) позволяет tooinsert несколько значений (в пакетном режиме).</span><span class="sxs-lookup"><span data-stu-id="5950f-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) allows you tooinsert multiple (batched) values.</span></span>
5. <span data-ttu-id="5950f-189">Используйте следующие команды tooget строку hello.</span><span class="sxs-lookup"><span data-stu-id="5950f-189">Use hello following command tooget a row:</span></span>
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

<span data-ttu-id="5950f-190">Дополнительные сведения см. в [справочнике по Apache HBase](https://hbase.apache.org/book.html#_rest).</span><span class="sxs-lookup"><span data-stu-id="5950f-190">For more information about HBase Rest, see [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest).</span></span>

> [!NOTE]
> <span data-ttu-id="5950f-191">Thrift не поддерживается HBase в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5950f-191">Thrift is not supported by HBase in HDInsight.</span></span>
>
> <span data-ttu-id="5950f-192">При использовании перелистывания или любые другие связи REST с WebHCat, должен пройти проверку подлинности запросы hello, предоставляя hello имя пользователя и пароль администратора кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5950f-192">When using Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span> <span data-ttu-id="5950f-193">Как использовать запросы toohello toosend hello server часть hello универсальный код ресурса (URI), необходимо также использовать hello имя кластера:</span><span class="sxs-lookup"><span data-stu-id="5950f-193">You must also use hello cluster name as part of hello Uniform Resource Identifier (URI) used toosend hello requests toohello server:</span></span>
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    <span data-ttu-id="5950f-194">Должно появиться примерно toohello ответа, следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="5950f-194">You should receive a response similar toohello following response:</span></span>
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a><span data-ttu-id="5950f-195">Проверка состояния кластера</span><span class="sxs-lookup"><span data-stu-id="5950f-195">Check cluster status</span></span>
<span data-ttu-id="5950f-196">HBase на HDInsight поставляется с веб-интерфейсом для наблюдения за кластерами.</span><span class="sxs-lookup"><span data-stu-id="5950f-196">HBase in HDInsight ships with a Web UI for monitoring clusters.</span></span> <span data-ttu-id="5950f-197">С помощью hello веб-интерфейса пользователя, можно запросить статистические данные или сведения об областях.</span><span class="sxs-lookup"><span data-stu-id="5950f-197">Using hello Web UI, you can request statistics or information about regions.</span></span>

<span data-ttu-id="5950f-198">**hello tooaccess HBase образец пользовательского интерфейса**</span><span class="sxs-lookup"><span data-stu-id="5950f-198">**tooaccess hello HBase Master UI**</span></span>

1. <span data-ttu-id="5950f-199">Вход в hello hello Ambari веб-интерфейса адресу https://&lt;Имя_кластера >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="5950f-199">Sign into hello hello Ambari Web UI at https://&lt;Clustername>.azurehdinsight.net.</span></span>
2. <span data-ttu-id="5950f-200">Нажмите кнопку **HBase** из меню слева hello.</span><span class="sxs-lookup"><span data-stu-id="5950f-200">Click **HBase** from hello left menu.</span></span>
3. <span data-ttu-id="5950f-201">Нажмите кнопку **быстрые ссылки** на hello вверху страницы приветствия, toohello точки активной Zookeeper узел ссылки, а затем нажмите кнопку **пользовательского интерфейса главного HBase**.</span><span class="sxs-lookup"><span data-stu-id="5950f-201">Click **Quick links** on hello top of hello page, point toohello active Zookeeper node link, and then click **HBase Master UI**.</span></span>  <span data-ttu-id="5950f-202">на другой вкладке браузера открывается Hello пользовательского интерфейса:</span><span class="sxs-lookup"><span data-stu-id="5950f-202">hello UI is opened in another browser tab:</span></span>

  ![Основной интерфейс HDInsight HBase](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  <span data-ttu-id="5950f-204">Hello пользовательского интерфейса главного HBase содержит hello в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="5950f-204">hello HBase Master UI contains hello following sections:</span></span>

  - <span data-ttu-id="5950f-205">региональные серверы;</span><span class="sxs-lookup"><span data-stu-id="5950f-205">region servers</span></span>
  - <span data-ttu-id="5950f-206">главные узлы резервного копирования;</span><span class="sxs-lookup"><span data-stu-id="5950f-206">backup masters</span></span>
  - <span data-ttu-id="5950f-207">таблицы;</span><span class="sxs-lookup"><span data-stu-id="5950f-207">tables</span></span>
  - <span data-ttu-id="5950f-208">задачи;</span><span class="sxs-lookup"><span data-stu-id="5950f-208">tasks</span></span>
  - <span data-ttu-id="5950f-209">атрибуты ПО.</span><span class="sxs-lookup"><span data-stu-id="5950f-209">software attributes</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="5950f-210">Удалить кластер hello</span><span class="sxs-lookup"><span data-stu-id="5950f-210">Delete hello cluster</span></span>
<span data-ttu-id="5950f-211">tooavoid несогласованности, рекомендуется отключить hello HBase таблиц перед удалением hello кластера.</span><span class="sxs-lookup"><span data-stu-id="5950f-211">tooavoid inconsistencies, we recommend that you disable hello HBase tables before you delete hello cluster.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="5950f-212">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="5950f-212">Troubleshoot</span></span>

<span data-ttu-id="5950f-213">Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="5950f-213">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5950f-214">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5950f-214">Next steps</span></span>
<span data-ttu-id="5950f-215">В этой статье вы узнали, как toocreate кластер HBase и как данные этих таблиц из hello toocreate таблиц и представлений hello оболочки HBase.</span><span class="sxs-lookup"><span data-stu-id="5950f-215">In this article, you learned how toocreate an HBase cluster and how toocreate tables and view hello data in those tables from hello HBase shell.</span></span> <span data-ttu-id="5950f-216">Вы также узнали, как запрос на данные в таблицах HBase и как toouse hello toocreate HBase C# API-интерфейс REST таблицу HBase и получения данных из таблицы hello toouse куста.</span><span class="sxs-lookup"><span data-stu-id="5950f-216">You also learned how toouse a Hive query on data in HBase tables and how toouse hello HBase C# REST APIs toocreate an HBase table and retrieve data from hello table.</span></span>

<span data-ttu-id="5950f-217">toolearn более, см.:</span><span class="sxs-lookup"><span data-stu-id="5950f-217">toolearn more, see:</span></span>

* <span data-ttu-id="5950f-218">[Что такое HBase в HDInsight][hdinsight-hbase-overview]. HBase — это база данных NoSQL с открытым исходным кодом Apache, разработанная в рамках проекта Hadoop, которая обеспечивает произвольный доступ и строгую согласованность больших объемов неструктурированных и частично структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="5950f-218">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hdinsight-hbase-cluster-quick-create]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-quick-create.png
[img-hdinsight-hbase-hive-editor]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hive-editor.png
[img-hdinsight-hbase-file-browser]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-file-browser.png
[img-hbase-shell]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png
