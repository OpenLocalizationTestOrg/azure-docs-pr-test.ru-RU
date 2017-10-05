---
title: "Использование действия скрипта для установки Solr в кластере Hadoop — Azure | Документы Майкрософт"
description: "Узнайте, как настроить кластер HDInsight с Solr помощью действия сценария."
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
ms.openlocfilehash: 6efb7ea26c3cdf7748fff4b02b5810c85cc41e1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="6adbe-103">Установка и использование Solr в кластерах HDInsight под управлением Windows</span><span class="sxs-lookup"><span data-stu-id="6adbe-103">Install and use Solr on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="6adbe-104">Узнайте, как настроить кластер HDInsight под управлением Windows с Solr с помощью действия сценария и использовать Solr для поиска данных.</span><span class="sxs-lookup"><span data-stu-id="6adbe-104">Learn how to customize Windows-based HDInsight cluster with Solr using Script Action, and how to use Solr to search data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6adbe-105">Шаги, описанные в этом документе, можно применять только к кластерам HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="6adbe-105">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="6adbe-106">Для версий ниже HDInsight 3.4 кластер HDInsight доступен только в Windows.</span><span class="sxs-lookup"><span data-stu-id="6adbe-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="6adbe-107">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="6adbe-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6adbe-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6adbe-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="6adbe-109">Сведения об использовании Solr с кластером под управлением Linux см. в статье [Установка и использование Solr на кластерах HDInsight Hadoop](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6adbe-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span></span>


<span data-ttu-id="6adbe-110">Solr можно установить в кластере любого типа (Hadoop, Storm, HBase, Spark) в HDInsight в Azure, воспользовавшись *Действием сценария*.</span><span class="sxs-lookup"><span data-stu-id="6adbe-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="6adbe-111">Пример сценария для установки Solr в кластере HDInsight доступен в большом двоичном объекте службы хранилища Azure (доступ только для чтения): [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="6adbe-111">A sample script to install Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

<span data-ttu-id="6adbe-112">Пример скрипта работает только с кластером HDInsight версии 3.1.</span><span class="sxs-lookup"><span data-stu-id="6adbe-112">The sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="6adbe-113">Дополнительную информацию о версиях кластера HDInsight см. в статье [Что представляют собой различные компоненты Hadoop, доступные в HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="6adbe-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="6adbe-114">Пример сценария, используемый в данном разделе, создает кластер Solr на основе Windows с определенной конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="6adbe-114">The sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span></span> <span data-ttu-id="6adbe-115">Если вы хотите настроить кластер Solr на использование других коллекций, сегментов, схем, реплик и т. п., необходимо соответствующим образом изменить скрипт и двоичные файлы Solr.</span><span class="sxs-lookup"><span data-stu-id="6adbe-115">If you want to configure the Solr cluster with different collections, shards, schemas, replicas, etc., you must modify the script and Solr binaries accordingly.</span></span>

<span data-ttu-id="6adbe-116">**Связанные статьи**</span><span class="sxs-lookup"><span data-stu-id="6adbe-116">**Related articles**</span></span>

* [<span data-ttu-id="6adbe-117">Установка и использование Solr в кластерах HDInsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="6adbe-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="6adbe-118">[Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-provision-clusters.md) — общие сведения о создании кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6adbe-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="6adbe-119">[Настройка кластера HDInsight с помощью действия сценария][hdinsight-cluster-customize]. Общая информация о настройке кластеров HDInsight с помощью действия сценария.</span><span class="sxs-lookup"><span data-stu-id="6adbe-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="6adbe-120">[Разработка скриптов действия сценария для HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="6adbe-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-solr"></a><span data-ttu-id="6adbe-121">Что такое Solr?</span><span class="sxs-lookup"><span data-stu-id="6adbe-121">What is Solr?</span></span>
<span data-ttu-id="6adbe-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> — это корпоративная платформа поиска, предоставляющая многофункциональные инструменты полнотекстового поиска данных.</span><span class="sxs-lookup"><span data-stu-id="6adbe-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="6adbe-123">Если Hadoop обеспечивает хранение огромных объемов данных и управление ими, то Apache Solr предоставляет возможности поиска для быстрого извлечения этих данных.</span><span class="sxs-lookup"><span data-stu-id="6adbe-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides the search capabilities to quickly retrieve the data.</span></span>

## <a name="install-solr-using-portal"></a><span data-ttu-id="6adbe-124">Установка Solr с помощью портала</span><span class="sxs-lookup"><span data-stu-id="6adbe-124">Install Solr using portal</span></span>
1. <span data-ttu-id="6adbe-125">Начните создание кластера с помощью параметра **Настраиваемое создание**, как описано в статье [Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="6adbe-125">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="6adbe-126">На странице **Действия скрипта** мастера щелкните **Добавить действие скрипта** для предоставления сведений о данном действии скрипта, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="6adbe-126">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="6adbe-127">![Использование действия сценария для настройки кластера](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Использование действия сценария для настройки кластера")</span><span class="sxs-lookup"><span data-stu-id="6adbe-127">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="6adbe-128">Свойство</span><span class="sxs-lookup"><span data-stu-id="6adbe-128">Property</span></span></th><th><span data-ttu-id="6adbe-129">Значение</span><span class="sxs-lookup"><span data-stu-id="6adbe-129">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="6adbe-130">Имя</span><span class="sxs-lookup"><span data-stu-id="6adbe-130">Name</span></span></td>
            <td><span data-ttu-id="6adbe-131">Укажите имя для действия сценария.</span><span class="sxs-lookup"><span data-stu-id="6adbe-131">Specify a name for the script action.</span></span> <span data-ttu-id="6adbe-132">Например, <b>Установить Solr</b>.</span><span class="sxs-lookup"><span data-stu-id="6adbe-132">For example, <b>Install Solr</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="6adbe-133">URI-адрес сценария</span><span class="sxs-lookup"><span data-stu-id="6adbe-133">Script URI</span></span></td>
            <td><span data-ttu-id="6adbe-134">Укажите универсальный идентификатор ресурса (URI) для сценария, который вызывается для настройки кластера.</span><span class="sxs-lookup"><span data-stu-id="6adbe-134">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="6adbe-135">Например, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i>.</span><span class="sxs-lookup"><span data-stu-id="6adbe-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="6adbe-136">Тип узла</span><span class="sxs-lookup"><span data-stu-id="6adbe-136">Node Type</span></span></td>
            <td><span data-ttu-id="6adbe-137">Укажите узлы, на которых выполняется сценарий настройки.</span><span class="sxs-lookup"><span data-stu-id="6adbe-137">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="6adbe-138">Вы можете выбрать одно из трех значений: <b>Все узлы</b>, <b>Только головные узлы</b> или <b>Worker nodes only</b> (Только рабочие узлы).</span><span class="sxs-lookup"><span data-stu-id="6adbe-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="6adbe-139">Параметры</span><span class="sxs-lookup"><span data-stu-id="6adbe-139">Parameters</span></span></td>
            <td><span data-ttu-id="6adbe-140">Укажите параметры, если они требуются для сценария.</span><span class="sxs-lookup"><span data-stu-id="6adbe-140">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="6adbe-141">Сценарий для установки Solr не требует никаких параметров, поэтому можно оставить это поле пустым.</span><span class="sxs-lookup"><span data-stu-id="6adbe-141">The script to install Solr does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="6adbe-142">Можно добавить несколько действий сценария для установки нескольких компонентов в кластере.</span><span class="sxs-lookup"><span data-stu-id="6adbe-142">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="6adbe-143">После добавления скриптов щелкните флажок, чтобы начать создание кластера.</span><span class="sxs-lookup"><span data-stu-id="6adbe-143">After you have added the scripts, click the checkmark to start creating the cluster.</span></span>

## <a name="use-solr"></a><span data-ttu-id="6adbe-144">Использование Solr</span><span class="sxs-lookup"><span data-stu-id="6adbe-144">Use Solr</span></span>
<span data-ttu-id="6adbe-145">Необходимо начать с индексирования системой Solr нескольких файлов данных.</span><span class="sxs-lookup"><span data-stu-id="6adbe-145">You must start with indexing Solr with some data files.</span></span> <span data-ttu-id="6adbe-146">Затем можно использовать Solr для выполнения запросов поиска в индексированных данных.</span><span class="sxs-lookup"><span data-stu-id="6adbe-146">You can then use Solr to run search queries on the indexed data.</span></span> <span data-ttu-id="6adbe-147">Выполните следующие действия, чтобы использовать Solr в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6adbe-147">Perform the following steps to use Solr in an HDInsight cluster:</span></span>

1. <span data-ttu-id="6adbe-148">**Используйте протокол удаленного рабочего стола (RDP) для удаленного подключения к кластеру HDInsight с установленной Solr.**</span><span class="sxs-lookup"><span data-stu-id="6adbe-148">**Use Remote Desktop Protocol (RDP) to remote into the HDInsight cluster with Solr installed**.</span></span> <span data-ttu-id="6adbe-149">На портале Azure включите удаленный рабочий стол для созданного кластера с установленной Solr, а затем подключитесь к кластеру.</span><span class="sxs-lookup"><span data-stu-id="6adbe-149">From the Azure portal, enable Remote Desktop for the cluster you created with Solr installed, and then remote into the cluster.</span></span> <span data-ttu-id="6adbe-150">Указания см. в разделе [Подключение к кластерам HDInsight с помощью RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="6adbe-150">For instructions, see [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="6adbe-151">**Выполните индексирование Solr, передав файлы данных**.</span><span class="sxs-lookup"><span data-stu-id="6adbe-151">**Index Solr by uploading data files**.</span></span> <span data-ttu-id="6adbe-152">При индексировании системы Solr вы помещаете в нее документы, по которым может потребоваться выполнить поиск.</span><span class="sxs-lookup"><span data-stu-id="6adbe-152">When you index Solr, you put documents in it that you may need to search on.</span></span> <span data-ttu-id="6adbe-153">Чтобы выполнить индексирование Solr, подключитесь к кластеру по протоколу удаленного рабочего стола, перейдите на рабочий стол, откройте командную строку Hadoop и перейдите к **C:\apps\dist\solr-4.7.2\example\exampledocs**.</span><span class="sxs-lookup"><span data-stu-id="6adbe-153">To index Solr, use RDP to remote into the cluster, navigate to the desktop, open the Hadoop command line, and navigate to **C:\apps\dist\solr-4.7.2\example\exampledocs**.</span></span> <span data-ttu-id="6adbe-154">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6adbe-154">Run the following command:</span></span>

        java -jar post.jar solr.xml monitor.xml

    <span data-ttu-id="6adbe-155">В консоли будут выведены такие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="6adbe-155">You'll see the following output on the console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes to http://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="6adbe-156">Служебная программа post.jar индексирует Solr с использованием двух примеров документов — **solr.xml** и **monitor.xml**.</span><span class="sxs-lookup"><span data-stu-id="6adbe-156">The post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span></span> <span data-ttu-id="6adbe-157">Служебная программа post.jar и примеры документов входят в состав установки Solr.</span><span class="sxs-lookup"><span data-stu-id="6adbe-157">The post.jar utility and the sample documents are available with Solr installation.</span></span>
3. <span data-ttu-id="6adbe-158">**Воспользуйтесь панелью мониторинга Solr для поиска по индексированным документам.**</span><span class="sxs-lookup"><span data-stu-id="6adbe-158">**Use the Solr dashboard to search within the indexed documents**.</span></span> <span data-ttu-id="6adbe-159">В сеансе связи с кластером HDInsight по протоколу RDP откройте Internet Explorer и запустите панель мониторинга Solr по адресу **http://headnodehost:8983/solr/#/**.</span><span class="sxs-lookup"><span data-stu-id="6adbe-159">In the RDP session to the HDInsight cluster, open Internet Explorer, and launch the Solr dashboard at **http://headnodehost:8983/solr/#/**.</span></span> <span data-ttu-id="6adbe-160">В левой области в раскрывающемся списке **Core Selector** (Базовый селектор) выберите **collection1**, а затем щелкните **Запрос**.</span><span class="sxs-lookup"><span data-stu-id="6adbe-160">From the left pane, from the **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span></span> <span data-ttu-id="6adbe-161">Например, чтобы выбрать и возвратить все документы в Solr, укажите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="6adbe-161">As an example, to select and return all the docs in Solr, provide the following values:</span></span>

   * <span data-ttu-id="6adbe-162">В текстовом поле **q** введите **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="6adbe-162">In the **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="6adbe-163">Это позволяет возвратить все документы, индексированные в Solr.</span><span class="sxs-lookup"><span data-stu-id="6adbe-163">This will return all the documents that are indexed in Solr.</span></span> <span data-ttu-id="6adbe-164">Если требуется найти в документах конкретную строку, ее также можно ввести в этом поле.</span><span class="sxs-lookup"><span data-stu-id="6adbe-164">If you want to search for a specific string within the documents, you can enter that string here.</span></span>
   * <span data-ttu-id="6adbe-165">В текстовом поле **wt** выберите формат выходных данных.</span><span class="sxs-lookup"><span data-stu-id="6adbe-165">In the **wt** text box, select the output format.</span></span> <span data-ttu-id="6adbe-166">По умолчанию используется **JSON**.</span><span class="sxs-lookup"><span data-stu-id="6adbe-166">Default is **json**.</span></span> <span data-ttu-id="6adbe-167">Щелкните **Выполнить запрос**.</span><span class="sxs-lookup"><span data-stu-id="6adbe-167">Click **Execute Query**.</span></span>

     <span data-ttu-id="6adbe-168">![Использование действия сценария для настройки кластера](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Выполнение запроса на панели мониторинга Solr")</span><span class="sxs-lookup"><span data-stu-id="6adbe-168">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span></span>

     <span data-ttu-id="6adbe-169">В выходных данных возвращаются два документа, которые использовались при индексировании Solr.</span><span class="sxs-lookup"><span data-stu-id="6adbe-169">The output returns the two docs that we used for indexing Solr.</span></span> <span data-ttu-id="6adbe-170">Результат выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6adbe-170">The output resembles the following:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, the Enterprise Search Server",
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
                     "Scalability - Efficient Replication to other Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over the e)"
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
4. <span data-ttu-id="6adbe-171">**Рекомендуется создать резервную копию индексированных данных из Solr в хранилище больших двоичных объектов Azure, связанном с кластером HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="6adbe-171">**Recommended: Back up the indexed data from Solr to Azure Blob storage associated with the HDInsight cluster**.</span></span> <span data-ttu-id="6adbe-172">Опыт показывает, что стоит выполнять резервное копирование индексированных данных с узлов кластера Solr в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="6adbe-172">As a good practice, you should back up the indexed data from the Solr cluster nodes onto Azure Blob storage.</span></span> <span data-ttu-id="6adbe-173">Для этого выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="6adbe-173">Perform the following steps to do so:</span></span>

   1. <span data-ttu-id="6adbe-174">В сеансе связи по протоколу RDP откройте Internet Explorer и выберите следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="6adbe-174">From the RDP session, open Internet Explorer, and point to the following URL:</span></span>

           http://localhost:8983/solr/replication?command=backup

       <span data-ttu-id="6adbe-175">Вы должны получить примерно следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="6adbe-175">You should see a response like this:</span></span>

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. <span data-ttu-id="6adbe-176">В удаленном сеансе перейдите к {SOLR_HOME}\{Collection}\data.</span><span class="sxs-lookup"><span data-stu-id="6adbe-176">In the remote session, navigate to {SOLR_HOME}\{Collection}\data.</span></span> <span data-ttu-id="6adbe-177">Для кластера, созданного с помощью примера скрипта, это должна быть папка **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span><span class="sxs-lookup"><span data-stu-id="6adbe-177">For the cluster created via the sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span></span> <span data-ttu-id="6adbe-178">В этом расположении вы увидите папку моментальных снимков с именем, похожим на **snapshot.*timestamp***.</span><span class="sxs-lookup"><span data-stu-id="6adbe-178">At this location, you should see a snapshot folder created with a name similar to **snapshot.*timestamp***.</span></span>
   3. <span data-ttu-id="6adbe-179">Запакуйте эту папку моментальных снимков и отправьте ее в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="6adbe-179">Zip the snapshot folder and upload it to Azure Blob storage.</span></span> <span data-ttu-id="6adbe-180">В командной строке Hadoop перейдите к расположению папки моментальных снимков, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6adbe-180">From the Hadoop command line, navigate to the location of the snapshot folder by using the following command:</span></span>

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       <span data-ttu-id="6adbe-181">Эта команда копирует моментальный снимок в папку /example/data/ в контейнере учетной записи хранения по умолчанию, связанной с этим кластером.</span><span class="sxs-lookup"><span data-stu-id="6adbe-181">This command copies the snapshot to /example/data/ under the container within the default Storage account associated with the cluster.</span></span>

## <a name="install-solr-using-aure-powershell"></a><span data-ttu-id="6adbe-182">Установка Solr с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6adbe-182">Install Solr using Aure PowerShell</span></span>
<span data-ttu-id="6adbe-183">См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="6adbe-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="6adbe-184">В этом примере показано, как установить Spark с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6adbe-184">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="6adbe-185">Необходимо изменить сценарий для использования [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="6adbe-185">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="install-solr-using-net-sdk"></a><span data-ttu-id="6adbe-186">Установка Solr с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="6adbe-186">Install Solr using .NET SDK</span></span>
<span data-ttu-id="6adbe-187">См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="6adbe-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="6adbe-188">В этом примере показано, как установить Spark с помощью пакета SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="6adbe-188">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="6adbe-189">Необходимо изменить сценарий для использования [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="6adbe-189">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="6adbe-190">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="6adbe-190">See also</span></span>
* [<span data-ttu-id="6adbe-191">Установка и использование Solr в кластерах HDInsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="6adbe-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="6adbe-192">[Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-provision-clusters.md) — общие сведения о создании кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6adbe-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="6adbe-193">[Настройка кластера HDInsight с помощью действия сценария][hdinsight-cluster-customize]. Общая информация о настройке кластеров HDInsight с помощью действия сценария.</span><span class="sxs-lookup"><span data-stu-id="6adbe-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="6adbe-194">[Разработка скриптов действия сценария для HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="6adbe-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="6adbe-195">[Установка и использование Spark в кластерах HDInsight Hadoop с помощью действия сценария][hdinsight-install-spark]. Пример действия сценария для установки Spark.</span><span class="sxs-lookup"><span data-stu-id="6adbe-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="6adbe-196">[Установка и использование R на кластерах HDInsight Hadoop][hdinsight-install-r]. Пример действия сценария для установки R.</span><span class="sxs-lookup"><span data-stu-id="6adbe-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="6adbe-197">[Установка и использование Giraph в HDInsight](hdinsight-hadoop-giraph-install.md) — пример действия скрипта для установки Giraph.</span><span class="sxs-lookup"><span data-stu-id="6adbe-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
