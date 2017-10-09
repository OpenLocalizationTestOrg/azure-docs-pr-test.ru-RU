---
title: "Действие сценария aaaUse tooinstall Solr в кластере Hadoop - Azure | Документы Microsoft"
description: "Узнайте, как toocustomize HDInsight кластер с Solr, с помощью действия сценария."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="26e80-103">Установка и использование Solr в кластерах HDInsight под управлением Windows</span><span class="sxs-lookup"><span data-stu-id="26e80-103">Install and use Solr on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="26e80-104">Узнайте, как кластер toocustomize HDInsight под управлением Windows с Solr, с помощью действия скрипта и как toouse Solr toosearch данных.</span><span class="sxs-lookup"><span data-stu-id="26e80-104">Learn how toocustomize Windows-based HDInsight cluster with Solr using Script Action, and how toouse Solr toosearch data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26e80-105">Hello шагов в этот документ корректно работать только с кластерами HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="26e80-105">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="26e80-106">Для версий ниже HDInsight 3.4 кластер HDInsight доступен только в Windows.</span><span class="sxs-lookup"><span data-stu-id="26e80-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="26e80-107">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="26e80-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="26e80-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="26e80-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="26e80-109">Сведения об использовании Solr с кластером под управлением Linux см. в статье [Установка и использование Solr на кластерах HDInsight Hadoop](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="26e80-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span></span>


<span data-ttu-id="26e80-110">Solr можно установить в кластере любого типа (Hadoop, Storm, HBase, Spark) в HDInsight в Azure, воспользовавшись *Действием сценария*.</span><span class="sxs-lookup"><span data-stu-id="26e80-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="26e80-111">Образец сценария tooinstall Solr в кластере HDInsight доступна из большого двоичного объекта хранилища Azure только для чтения, в [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="26e80-111">A sample script tooinstall Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

<span data-ttu-id="26e80-112">Пример сценария Hello работает только с кластера HDInsight версии 3.1.</span><span class="sxs-lookup"><span data-stu-id="26e80-112">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="26e80-113">Дополнительную информацию о версиях кластера HDInsight см. в статье [Что представляют собой различные компоненты Hadoop, доступные в HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="26e80-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="26e80-114">Пример сценария Hello, используемые в данном разделе создается кластер Solr под управлением Windows с указанной конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="26e80-114">hello sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span></span> <span data-ttu-id="26e80-115">Если требуется кластер Solr hello tooconfigure с различными коллекциями, сегментами, схемы, реплики, т. д., следует изменить скрипт hello и Solr двоичные файлы соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="26e80-115">If you want tooconfigure hello Solr cluster with different collections, shards, schemas, replicas, etc., you must modify hello script and Solr binaries accordingly.</span></span>

<span data-ttu-id="26e80-116">**Связанные статьи**</span><span class="sxs-lookup"><span data-stu-id="26e80-116">**Related articles**</span></span>

* [<span data-ttu-id="26e80-117">Установка и использование Solr в кластерах HDInsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="26e80-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="26e80-118">[Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-provision-clusters.md) — общие сведения о создании кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26e80-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="26e80-119">[Настройка кластера HDInsight с помощью действия сценария][hdinsight-cluster-customize]. Общая информация о настройке кластеров HDInsight с помощью действия сценария.</span><span class="sxs-lookup"><span data-stu-id="26e80-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="26e80-120">[Разработка скриптов действия сценария для HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="26e80-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-solr"></a><span data-ttu-id="26e80-121">Что такое Solr?</span><span class="sxs-lookup"><span data-stu-id="26e80-121">What is Solr?</span></span>
<span data-ttu-id="26e80-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> — это корпоративная платформа поиска, предоставляющая многофункциональные инструменты полнотекстового поиска данных.</span><span class="sxs-lookup"><span data-stu-id="26e80-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="26e80-123">Хотя Hadoop позволяет хранения и управления огромный объем данных, Apache Solr предоставляет возможности поиска hello tooquickly извлекать данные hello.</span><span class="sxs-lookup"><span data-stu-id="26e80-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides hello search capabilities tooquickly retrieve hello data.</span></span>

## <a name="install-solr-using-portal"></a><span data-ttu-id="26e80-124">Установка Solr с помощью портала</span><span class="sxs-lookup"><span data-stu-id="26e80-124">Install Solr using portal</span></span>
1. <span data-ttu-id="26e80-125">Начать создание кластера с помощью hello **НАСТРАИВАЕМОЕ создание** параметра, как описано в разделе [кластеров создать Hadoop в HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="26e80-125">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="26e80-126">На hello **действия скрипта** страница приветствия мастера нажмите кнопку **добавьте действия скрипта** tooprovide сведений о hello действие скрипта, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="26e80-126">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="26e80-127">![Используйте действие скрипта toocustomize кластера](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "toocustomize действия скрипта для использования кластера")</span><span class="sxs-lookup"><span data-stu-id="26e80-127">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="26e80-128">Свойство</span><span class="sxs-lookup"><span data-stu-id="26e80-128">Property</span></span></th><th><span data-ttu-id="26e80-129">Значение</span><span class="sxs-lookup"><span data-stu-id="26e80-129">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="26e80-130">Имя</span><span class="sxs-lookup"><span data-stu-id="26e80-130">Name</span></span></td>
            <td><span data-ttu-id="26e80-131">Укажите имя для действия сценария hello.</span><span class="sxs-lookup"><span data-stu-id="26e80-131">Specify a name for hello script action.</span></span> <span data-ttu-id="26e80-132">Например, <b>Установить Solr</b>.</span><span class="sxs-lookup"><span data-stu-id="26e80-132">For example, <b>Install Solr</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="26e80-133">URI-адрес сценария</span><span class="sxs-lookup"><span data-stu-id="26e80-133">Script URI</span></span></td>
            <td><span data-ttu-id="26e80-134">Укажите сценарий toohello универсальный код ресурса (URI) hello, вызванный toocustomize hello кластера.</span><span class="sxs-lookup"><span data-stu-id="26e80-134">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="26e80-135">Например, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i>.</span><span class="sxs-lookup"><span data-stu-id="26e80-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="26e80-136">Тип узла</span><span class="sxs-lookup"><span data-stu-id="26e80-136">Node Type</span></span></td>
            <td><span data-ttu-id="26e80-137">Укажите hello узлов, на которых выполняется скрипт настройки hello.</span><span class="sxs-lookup"><span data-stu-id="26e80-137">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="26e80-138">Вы можете выбрать одно из трех значений: <b>Все узлы</b>, <b>Только головные узлы</b> или <b>Worker nodes only</b> (Только рабочие узлы).</span><span class="sxs-lookup"><span data-stu-id="26e80-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="26e80-139">Параметры</span><span class="sxs-lookup"><span data-stu-id="26e80-139">Parameters</span></span></td>
            <td><span data-ttu-id="26e80-140">Укажите параметры hello, если это требуется для сценария hello.</span><span class="sxs-lookup"><span data-stu-id="26e80-140">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="26e80-141">сценарий Hello tooinstall Solr параметры не требуются, поэтому это поле можно оставить пустым.</span><span class="sxs-lookup"><span data-stu-id="26e80-141">hello script tooinstall Solr does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="26e80-142">Можно добавить несколько компонентов несколько tooinstall действие сценария в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="26e80-142">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="26e80-143">После добавления скриптов hello, щелкните флажок toostart hello, для создания кластера hello.</span><span class="sxs-lookup"><span data-stu-id="26e80-143">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-solr"></a><span data-ttu-id="26e80-144">Использование Solr</span><span class="sxs-lookup"><span data-stu-id="26e80-144">Use Solr</span></span>
<span data-ttu-id="26e80-145">Необходимо начать с индексирования системой Solr нескольких файлов данных.</span><span class="sxs-lookup"><span data-stu-id="26e80-145">You must start with indexing Solr with some data files.</span></span> <span data-ttu-id="26e80-146">Затем можно использовать запросы поиска toorun Solr hello индексированных данных.</span><span class="sxs-lookup"><span data-stu-id="26e80-146">You can then use Solr toorun search queries on hello indexed data.</span></span> <span data-ttu-id="26e80-147">Выполните следующие шаги toouse Solr в кластер HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="26e80-147">Perform hello following steps toouse Solr in an HDInsight cluster:</span></span>

1. <span data-ttu-id="26e80-148">**Использовать протокол удаленного рабочего стола (RDP) tooremote в кластер HDInsight hello с Solr установлен**.</span><span class="sxs-lookup"><span data-stu-id="26e80-148">**Use Remote Desktop Protocol (RDP) tooremote into hello HDInsight cluster with Solr installed**.</span></span> <span data-ttu-id="26e80-149">Из hello портал Azure необходимо включите удаленный рабочий стол для кластера hello, созданного с помощью Solr hello установлены и затем удаленный в кластер.</span><span class="sxs-lookup"><span data-stu-id="26e80-149">From hello Azure portal, enable Remote Desktop for hello cluster you created with Solr installed, and then remote into hello cluster.</span></span> <span data-ttu-id="26e80-150">Инструкции см. в разделе [tooHDInsight кластерами, с помощью протокола удаленного рабочего СТОЛА подключиться](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="26e80-150">For instructions, see [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="26e80-151">**Выполните индексирование Solr, передав файлы данных**.</span><span class="sxs-lookup"><span data-stu-id="26e80-151">**Index Solr by uploading data files**.</span></span> <span data-ttu-id="26e80-152">Если индексируются Solr, в него, может понадобиться toosearch поместить документы.</span><span class="sxs-lookup"><span data-stu-id="26e80-152">When you index Solr, you put documents in it that you may need toosearch on.</span></span> <span data-ttu-id="26e80-153">tooindex Solr tooremote использования RDP в кластер hello перейдите toohello рабочего стола, откройте hello Hadoop командной строки и перейдите в слишком**C:\apps\dist\solr-4.7.2\example\exampledocs**.</span><span class="sxs-lookup"><span data-stu-id="26e80-153">tooindex Solr, use RDP tooremote into hello cluster, navigate toohello desktop, open hello Hadoop command line, and navigate too**C:\apps\dist\solr-4.7.2\example\exampledocs**.</span></span> <span data-ttu-id="26e80-154">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="26e80-154">Run hello following command:</span></span>

        java -jar post.jar solr.xml monitor.xml

    <span data-ttu-id="26e80-155">Вы увидите hello после вывода на консоль hello:</span><span class="sxs-lookup"><span data-stu-id="26e80-155">You'll see hello following output on hello console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="26e80-156">Программа Hello post.jar индексирует Solr с два образца документов **solr.xml** и **monitor.xml**.</span><span class="sxs-lookup"><span data-stu-id="26e80-156">hello post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span></span> <span data-ttu-id="26e80-157">Программа post.jar Hello и документы образец hello доступные при установке Solr.</span><span class="sxs-lookup"><span data-stu-id="26e80-157">hello post.jar utility and hello sample documents are available with Solr installation.</span></span>
3. <span data-ttu-id="26e80-158">**Используйте hello Solr мониторинга toosearch внутри hello индексированных документов**.</span><span class="sxs-lookup"><span data-stu-id="26e80-158">**Use hello Solr dashboard toosearch within hello indexed documents**.</span></span> <span data-ttu-id="26e80-159">В toohello сеанс RDP hello HDInsight кластера, откройте Internet Explorer и запуска мониторинга Solr hello в **http://headnodehost:8983/solr / #/**.</span><span class="sxs-lookup"><span data-stu-id="26e80-159">In hello RDP session toohello HDInsight cluster, open Internet Explorer, and launch hello Solr dashboard at **http://headnodehost:8983/solr/#/**.</span></span> <span data-ttu-id="26e80-160">Из левой области hello из hello **селектор Core** раскрывающийся список, выберите **collection1**и в этот пункт **запроса**.</span><span class="sxs-lookup"><span data-stu-id="26e80-160">From hello left pane, from hello **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span></span> <span data-ttu-id="26e80-161">Пример, tooselect и возвращают все документы hello в Solr, предоставляют hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="26e80-161">As an example, tooselect and return all hello docs in Solr, provide hello following values:</span></span>

   * <span data-ttu-id="26e80-162">В hello **q** текста введите  **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="26e80-162">In hello **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="26e80-163">Это будет возвращать все документы hello, которые индексируются в Solr.</span><span class="sxs-lookup"><span data-stu-id="26e80-163">This will return all hello documents that are indexed in Solr.</span></span> <span data-ttu-id="26e80-164">Если требуется toosearch конкретную строку в документах hello, можно ввести здесь строку.</span><span class="sxs-lookup"><span data-stu-id="26e80-164">If you want toosearch for a specific string within hello documents, you can enter that string here.</span></span>
   * <span data-ttu-id="26e80-165">В hello **wt** текстовое поле, выберите hello выходной формат.</span><span class="sxs-lookup"><span data-stu-id="26e80-165">In hello **wt** text box, select hello output format.</span></span> <span data-ttu-id="26e80-166">По умолчанию используется **JSON**.</span><span class="sxs-lookup"><span data-stu-id="26e80-166">Default is **json**.</span></span> <span data-ttu-id="26e80-167">Щелкните **Выполнить запрос**.</span><span class="sxs-lookup"><span data-stu-id="26e80-167">Click **Execute Query**.</span></span>

     <span data-ttu-id="26e80-168">![Используйте действие скрипта toocustomize кластера](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "запуска запроса на панели мониторинга Solr")</span><span class="sxs-lookup"><span data-stu-id="26e80-168">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span></span>

     <span data-ttu-id="26e80-169">выходные данные Hello возвращает hello два документа, мы использовали для индексирования Solr.</span><span class="sxs-lookup"><span data-stu-id="26e80-169">hello output returns hello two docs that we used for indexing Solr.</span></span> <span data-ttu-id="26e80-170">выходные данные Hello аналогичные hello ниже:</span><span class="sxs-lookup"><span data-stu-id="26e80-170">hello output resembles hello following:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }
4. <span data-ttu-id="26e80-171">**Рекомендуется: Резервное копирование hello индексированных данных из Solr tooAzure хранилища больших двоичных объектов, связанных с кластером HDInsight hello**.</span><span class="sxs-lookup"><span data-stu-id="26e80-171">**Recommended: Back up hello indexed data from Solr tooAzure Blob storage associated with hello HDInsight cluster**.</span></span> <span data-ttu-id="26e80-172">В хорошей практикой должны резервные копии hello индексированных данных из узлов кластера Solr hello в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="26e80-172">As a good practice, you should back up hello indexed data from hello Solr cluster nodes onto Azure Blob storage.</span></span> <span data-ttu-id="26e80-173">Выполните hello, поэтому следующие шаги toodo.</span><span class="sxs-lookup"><span data-stu-id="26e80-173">Perform hello following steps toodo so:</span></span>

   1. <span data-ttu-id="26e80-174">Hello сеансу удаленного рабочего СТОЛА откройте Internet Explorer и toohello точки URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="26e80-174">From hello RDP session, open Internet Explorer, and point toohello following URL:</span></span>

           http://localhost:8983/solr/replication?command=backup

       <span data-ttu-id="26e80-175">Вы должны получить примерно следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="26e80-175">You should see a response like this:</span></span>

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. <span data-ttu-id="26e80-176">В удаленном сеансе hello, перейдите слишком {SOLR_HOME}\{коллекции} \data.</span><span class="sxs-lookup"><span data-stu-id="26e80-176">In hello remote session, navigate too{SOLR_HOME}\{Collection}\data.</span></span> <span data-ttu-id="26e80-177">Для кластера hello, созданные с помощью сценария образец hello, это должен быть **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span><span class="sxs-lookup"><span data-stu-id="26e80-177">For hello cluster created via hello sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span></span> <span data-ttu-id="26e80-178">В этом месте должна появиться папка моментальных снимков, созданные с именем аналогичные слишком**моментальных снимков.* Отметка времени***.</span><span class="sxs-lookup"><span data-stu-id="26e80-178">At this location, you should see a snapshot folder created with a name similar too**snapshot.*timestamp***.</span></span>
   3. <span data-ttu-id="26e80-179">ZIP-папка моментальных снимков hello и отправьте его tooAzure хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="26e80-179">Zip hello snapshot folder and upload it tooAzure Blob storage.</span></span> <span data-ttu-id="26e80-180">Из командной строки Hadoop hello перейти toohello расположение папки моментальных снимков hello, используя hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="26e80-180">From hello Hadoop command line, navigate toohello location of hello snapshot folder by using hello following command:</span></span>

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       <span data-ttu-id="26e80-181">Эта команда копии данных моментального снимка слишком/пример/hello/контейнере hello в по умолчанию hello хранилища учетной записи связанного с кластером hello.</span><span class="sxs-lookup"><span data-stu-id="26e80-181">This command copies hello snapshot too/example/data/ under hello container within hello default Storage account associated with hello cluster.</span></span>

## <a name="install-solr-using-aure-powershell"></a><span data-ttu-id="26e80-182">Установка Solr с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="26e80-182">Install Solr using Aure PowerShell</span></span>
<span data-ttu-id="26e80-183">См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="26e80-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="26e80-184">Hello образце показано, как tooinstall Spark с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="26e80-184">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="26e80-185">Требуется toocustomize hello сценарий toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="26e80-185">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="install-solr-using-net-sdk"></a><span data-ttu-id="26e80-186">Установка Solr с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="26e80-186">Install Solr using .NET SDK</span></span>
<span data-ttu-id="26e80-187">См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="26e80-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="26e80-188">Hello образце показано, как tooinstall Spark с помощью пакета SDK для .NET "hello".</span><span class="sxs-lookup"><span data-stu-id="26e80-188">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="26e80-189">Требуется toocustomize hello сценарий toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="26e80-189">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="26e80-190">См. также</span><span class="sxs-lookup"><span data-stu-id="26e80-190">See also</span></span>
* [<span data-ttu-id="26e80-191">Установка и использование Solr в кластерах HDInsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="26e80-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="26e80-192">[Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-provision-clusters.md) — общие сведения о создании кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26e80-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="26e80-193">[Настройка кластера HDInsight с помощью действия сценария][hdinsight-cluster-customize]. Общая информация о настройке кластеров HDInsight с помощью действия сценария.</span><span class="sxs-lookup"><span data-stu-id="26e80-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="26e80-194">[Разработка скриптов действия сценария для HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="26e80-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="26e80-195">[Установка и использование Spark в кластерах HDInsight Hadoop с помощью действия сценария][hdinsight-install-spark]. Пример действия сценария для установки Spark.</span><span class="sxs-lookup"><span data-stu-id="26e80-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="26e80-196">[Установка и использование R на кластерах HDInsight Hadoop][hdinsight-install-r]. Пример действия сценария для установки R.</span><span class="sxs-lookup"><span data-stu-id="26e80-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="26e80-197">[Установка и использование Giraph в HDInsight](hdinsight-hadoop-giraph-install.md) — пример действия скрипта для установки Giraph.</span><span class="sxs-lookup"><span data-stu-id="26e80-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
