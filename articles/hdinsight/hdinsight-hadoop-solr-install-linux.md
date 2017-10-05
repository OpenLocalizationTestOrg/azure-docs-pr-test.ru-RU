---
title: "Использование действия скрипта для установки Solr в кластере HDInsight на основе Linux — Azure | Документы Майкрософт"
description: "Узнайте, как устанавливать Solr в кластерах HDInsight Hadoop на основе Linux с помощью действий сценария."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cc93ed5c-a358-456a-91a4-f179185c0e98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: ad930ca023a36fa5874483873c82fdba11d117c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="6b79b-103">Установка и использование Solr на кластерах HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="6b79b-103">Install and use Solr on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="6b79b-104">Узнайте, как установить Solr в Azure HDInsight с помощью действия сценария.</span><span class="sxs-lookup"><span data-stu-id="6b79b-104">Learn how to install Solr on Azure HDInsight by using Script Action.</span></span> <span data-ttu-id="6b79b-105">Solr представляет собой многофункциональную платформу поиска и предоставляет возможности поиска корпоративного уровня на основе данных, управляемых Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6b79b-105">Solr is a powerful search platform and provides enterprise-level search capabilities on data managed by Hadoop.</span></span>

> [!IMPORTANT]
    > <span data-ttu-id="6b79b-106">Для выполнения действий, описанных в этом документе, необходим кластер HDInsight, который использует Linux.</span><span class="sxs-lookup"><span data-stu-id="6b79b-106">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="6b79b-107">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="6b79b-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6b79b-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6b79b-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b79b-109">Пример скрипта, используемый в этом документе, устанавливает кластер Solr 4.9 с определенной конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="6b79b-109">The sample script used in this document installs Solr 4.9 with a specific configuration.</span></span> <span data-ttu-id="6b79b-110">Если вы хотите настроить кластер Solr для использования других коллекций, сегментов, схем, реплик и т. п., необходимо соответствующим образом изменить сценарий и двоичные файлы Solr.</span><span class="sxs-lookup"><span data-stu-id="6b79b-110">If you want to configure the Solr cluster with different collections, shards, schemas, replicas, etc., you must modify the script and Solr binaries.</span></span>

## <span data-ttu-id="6b79b-111"><a name="whatis"></a>Что такое Solr</span><span class="sxs-lookup"><span data-stu-id="6b79b-111"><a name="whatis"></a>What is Solr</span></span>

<span data-ttu-id="6b79b-112">[Apache Solr](http://lucene.apache.org/solr/features.html) — это корпоративная платформа поиска, предоставляющая эффективные инструменты полнотекстового поиска данных.</span><span class="sxs-lookup"><span data-stu-id="6b79b-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="6b79b-113">Если Hadoop обеспечивает хранение огромных объемов данных и управление ими, то Apache Solr предоставляет возможности поиска для быстрого извлечения этих данных.</span><span class="sxs-lookup"><span data-stu-id="6b79b-113">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides the search capabilities to quickly retrieve the data.</span></span>

> [!WARNING]
> <span data-ttu-id="6b79b-114">Компоненты, поставляемые с кластером HDInsight, полностью поддерживаются корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6b79b-114">Components provided with the HDInsight cluster are fully supported by Microsoft.</span></span>
>
> <span data-ttu-id="6b79b-115">Настраиваемые компоненты, такие как Solr, получают ограниченную коммерчески оправданную поддержку, способствующую дальнейшей диагностике проблемы.</span><span class="sxs-lookup"><span data-stu-id="6b79b-115">Custom components, such as Solr, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="6b79b-116">Служба поддержки Майкрософт не всегда имеет возможность устранить проблемы с пользовательскими компонентами.</span><span class="sxs-lookup"><span data-stu-id="6b79b-116">Microsoft support may not be able to resolve problems with custom components.</span></span> <span data-ttu-id="6b79b-117">Может потребоваться обратиться за помощью к сообществу разработчиков открытого кода.</span><span class="sxs-lookup"><span data-stu-id="6b79b-117">You may need to engage the open source communities for assistance.</span></span> <span data-ttu-id="6b79b-118">Можно использовать ряд сайтов сообществ, например [форум MSDN по HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) или [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="6b79b-118">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="6b79b-119">Кроме того, для проектов Apache есть соответствующие сайты, например [Hadoop](http://hadoop.apache.org/) на сайте [http://apache.org](http://apache.org).</span><span class="sxs-lookup"><span data-stu-id="6b79b-119">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

## <a name="what-the-script-does"></a><span data-ttu-id="6b79b-120">Что делает сценарий</span><span class="sxs-lookup"><span data-stu-id="6b79b-120">What the script does</span></span>

<span data-ttu-id="6b79b-121">Этот сценарий вносит следующие изменения в кластер HDInsight:</span><span class="sxs-lookup"><span data-stu-id="6b79b-121">This script makes the following changes to the HDInsight cluster:</span></span>

* <span data-ttu-id="6b79b-122">Устанавливает Solr 4.9 в `/usr/hdp/current/solr`.</span><span class="sxs-lookup"><span data-stu-id="6b79b-122">Installs Solr 4.9 into `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="6b79b-123">Создает пользователя **solrusr**, используемого для запуска службы Solr.</span><span class="sxs-lookup"><span data-stu-id="6b79b-123">Creates a user, **solrusr**, which is used to run the Solr service</span></span>
* <span data-ttu-id="6b79b-124">Делает пользователя **solrusr** владельцем `/usr/hdp/current/solr`.</span><span class="sxs-lookup"><span data-stu-id="6b79b-124">Sets **solruser** as the owner of `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="6b79b-125">Добавляет конфигурацию [Upstart](http://upstart.ubuntu.com/), которая автоматически запускает Solr.</span><span class="sxs-lookup"><span data-stu-id="6b79b-125">Adds an [Upstart](http://upstart.ubuntu.com/) configuration that starts Solr automatically.</span></span>

## <span data-ttu-id="6b79b-126"><a name="install"></a>Установка Solr с помощью действий сценария</span><span class="sxs-lookup"><span data-stu-id="6b79b-126"><a name="install"></a>Install Solr using Script Actions</span></span>

<span data-ttu-id="6b79b-127">Пример сценария для установки Solr в кластер HDInsight доступен по следующему адресу.</span><span class="sxs-lookup"><span data-stu-id="6b79b-127">A sample script to install Solr on an HDInsight cluster is available at the following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

<span data-ttu-id="6b79b-128">Чтобы создать кластер с установленной платформой Solr, следуйте указаниям в документе [Создание кластеров под управлением Linux в HDInsight с помощью портала Azure](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6b79b-128">To create a cluster that has Solr installed, use the steps in the [Create HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span></span> <span data-ttu-id="6b79b-129">Во время создания выполните приведенные ниже действия для установки Solr.</span><span class="sxs-lookup"><span data-stu-id="6b79b-129">During the creation process, use the following steps to install Solr:</span></span>

1. <span data-ttu-id="6b79b-130">В колонке __Сводка кластера__ для кластера выберите __Дополнительные параметры__, а затем — __Действия скрипта__.</span><span class="sxs-lookup"><span data-stu-id="6b79b-130">From the __Cluster summary__ blade, select__Advanced settings__, then __Script actions__.</span></span> <span data-ttu-id="6b79b-131">Используйте следующие сведения, чтобы заполнить форму.</span><span class="sxs-lookup"><span data-stu-id="6b79b-131">Use the following information to populate the form:</span></span>

   * <span data-ttu-id="6b79b-132">**ИМЯ**: введите понятное имя для действия сценария.</span><span class="sxs-lookup"><span data-stu-id="6b79b-132">**NAME**: Enter a friendly name for the script action.</span></span>
   * <span data-ttu-id="6b79b-133">**Универсальный код ресурса скрипта**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/r-installer-v01.sh.</span><span class="sxs-lookup"><span data-stu-id="6b79b-133">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span></span>
   * <span data-ttu-id="6b79b-134">**ГОЛОВНОЙ**: установите флажок.</span><span class="sxs-lookup"><span data-stu-id="6b79b-134">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="6b79b-135">**Рабочая роль**: установите флажок.</span><span class="sxs-lookup"><span data-stu-id="6b79b-135">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="6b79b-136">**ZooKeeper**: установите этот флажок для установки на узле Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="6b79b-136">**ZOOKEEPER**: Check this option to install on the Zookeeper node</span></span>
   * <span data-ttu-id="6b79b-137">**ПАРАМЕТРЫ**: оставьте это поле пустым.</span><span class="sxs-lookup"><span data-stu-id="6b79b-137">**PARAMETERS**: Leave this field blank</span></span>

2. <span data-ttu-id="6b79b-138">В нижней части колонки **Действия скрипта** нажмите кнопку **Выбрать**, чтобы сохранить конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="6b79b-138">At the bottom of the **Script actions** blade, use the **Select** button to save the configuration.</span></span> <span data-ttu-id="6b79b-139">Наконец, нажмите кнопку **Далее**, чтобы вернуться в колонку __Сводка кластера__.</span><span class="sxs-lookup"><span data-stu-id="6b79b-139">Finally, use the **Next** button to return to the __Cluster summary__</span></span>

3. <span data-ttu-id="6b79b-140">На странице __Сводка кластера__ щелкните __Создать__, чтобы создать кластер.</span><span class="sxs-lookup"><span data-stu-id="6b79b-140">From the __Cluster summary__ page, select __Create__ to create the cluster.</span></span>

## <span data-ttu-id="6b79b-141"><a name="usesolr"></a>Как использовать Solr в HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b79b-141"><a name="usesolr"></a>How do I use Solr in HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b79b-142">Действия, описанные в этом разделе, демонстрируют базовые функциональные возможности Solr.</span><span class="sxs-lookup"><span data-stu-id="6b79b-142">The steps in this section demonstrate basic Solr functionality.</span></span> <span data-ttu-id="6b79b-143">Дополнительные сведения об использовании Solr см. на [сайте Apache Solr](http://lucene.apache.org/solr/).</span><span class="sxs-lookup"><span data-stu-id="6b79b-143">For more information on using Solr, see the [Apache Solr site](http://lucene.apache.org/solr/).</span></span>

### <a name="index-data"></a><span data-ttu-id="6b79b-144">Данные индекса</span><span class="sxs-lookup"><span data-stu-id="6b79b-144">Index data</span></span>

<span data-ttu-id="6b79b-145">Выполните следующие действия, чтобы добавить демонстрационные данные в Solr и создать запрос к ним.</span><span class="sxs-lookup"><span data-stu-id="6b79b-145">Use the following steps to add example data to Solr, and then query it:</span></span>

1. <span data-ttu-id="6b79b-146">Подключитесь к кластеру HDInsight с помощью протокола SSH:</span><span class="sxs-lookup"><span data-stu-id="6b79b-146">Connect to the HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="6b79b-147">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6b79b-147">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="6b79b-148">В действиях, описанных ниже, для подключения к пользовательскому веб-интерфейсу Solr используется туннель SSL.</span><span class="sxs-lookup"><span data-stu-id="6b79b-148">Steps later in this document use an SSL tunnel to connect to the Solr web UI.</span></span> <span data-ttu-id="6b79b-149">Чтобы выполнить эти действия, необходимо установить туннель SSL и настроить браузер для его использования.</span><span class="sxs-lookup"><span data-stu-id="6b79b-149">To use these steps, you must establish an SSL tunnel and then configure your browser to use it.</span></span>
     >
     > <span data-ttu-id="6b79b-150">Дополнительные сведения см. в документе [Использование туннелирования SSH для доступа к веб-интерфейсу Ambari, JobHistory, NameNode, Oozie и другим веб-интерфейсам](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="6b79b-150">For more information, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="6b79b-151">Используйте следующие команды, чтобы получить образец данных индекса Solr:</span><span class="sxs-lookup"><span data-stu-id="6b79b-151">Use the following commands to have Solr index sample data:</span></span>

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    <span data-ttu-id="6b79b-152">В консоли отобразится результат следующего вида.</span><span class="sxs-lookup"><span data-stu-id="6b79b-152">The following output is returned to the console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes to http://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="6b79b-153">Служебная программа `post.jar` добавляет документы **solr.xml** и **monitor.xml** в индекс.</span><span class="sxs-lookup"><span data-stu-id="6b79b-153">The `post.jar` utility adds the **solr.xml** and **monitor.xml** documents to the index.</span></span>
  
3. <span data-ttu-id="6b79b-154">Для отправки запроса к REST API Solr используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="6b79b-154">Use the following command to query the Solr REST API:</span></span>

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    <span data-ttu-id="6b79b-155">Данная команда выполняет в **collection1** поиск документов, соответствующих **\*:\*** (кодируется как \*%3A\* в строке запроса).</span><span class="sxs-lookup"><span data-stu-id="6b79b-155">This command searches **collection1** for any documents matching **\*:\*** (encoded as \*%3A\* in the query string).</span></span> <span data-ttu-id="6b79b-156">Ниже приведен документ JSON, представляющий собой пример возвращенного ответа.</span><span class="sxs-lookup"><span data-stu-id="6b79b-156">The following JSON document is an example of the response:</span></span>

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

### <a name="using-the-solr-dashboard"></a><span data-ttu-id="6b79b-157">Использование панели мониторинга Solr</span><span class="sxs-lookup"><span data-stu-id="6b79b-157">Using the Solr dashboard</span></span>

<span data-ttu-id="6b79b-158">Панель мониторинга Solr — это веб-интерфейс для работы с Solr через веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="6b79b-158">The Solr dashboard is a web UI that allows you to work with Solr through your web browser.</span></span> <span data-ttu-id="6b79b-159">Прямой доступ к панели мониторинга Solr через Интернет из кластера HDInsight невозможен.</span><span class="sxs-lookup"><span data-stu-id="6b79b-159">The Solr dashboard is not exposed directly on the Internet from your HDInsight cluster.</span></span> <span data-ttu-id="6b79b-160">Для этого следует использовать туннель SSH.</span><span class="sxs-lookup"><span data-stu-id="6b79b-160">You can use an SSH tunnel to access it.</span></span> <span data-ttu-id="6b79b-161">Дополнительные сведения об использовании туннеля SSH см. в документе [Использование туннелирования SSH для доступа к веб-интерфейсу Ambari, JobHistory, NameNode, Oozie и другим веб-интерфейсам](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="6b79b-161">For more information on using an SSH tunnel, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="6b79b-162">Установив туннель SSH, выполните следующие действия, чтобы начать использовать панель мониторинга Solr.</span><span class="sxs-lookup"><span data-stu-id="6b79b-162">Once you have established an SSH tunnel, use the following steps to use the Solr dashboard:</span></span>

1. <span data-ttu-id="6b79b-163">Определите имя основного головного узла:</span><span class="sxs-lookup"><span data-stu-id="6b79b-163">Determine the host name for the primary headnode:</span></span>

   1. <span data-ttu-id="6b79b-164">Используйте протокол SSH, чтобы подключиться к головному узлу кластера.</span><span class="sxs-lookup"><span data-stu-id="6b79b-164">Use SSH to connect to the cluster head node.</span></span> <span data-ttu-id="6b79b-165">Например, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="6b79b-165">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

       <span data-ttu-id="6b79b-166">Дополнительные сведения об использовании протокола SSH см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6b79b-166">For more information on using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

   2. <span data-ttu-id="6b79b-167">Чтобы получить полное имя узла, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6b79b-167">Use the following command to get the fully qualified hostname:</span></span>

        ```bash
        hostname -f
        ```

        <span data-ttu-id="6b79b-168">Эта команда возвращает значение имени узла следующего вида.</span><span class="sxs-lookup"><span data-stu-id="6b79b-168">This command returns a value similar to the following host name:</span></span>

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        <span data-ttu-id="6b79b-169">Сохраните полученное значение, так как оно понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="6b79b-169">Save the value returned, as it is used later.</span></span>

2. <span data-ttu-id="6b79b-170">В окне браузера введите адрес **http://HOSTNAME:8983/solr/#/**, где **HOSTNAME** — это имя, определенное на предыдущих этапах.</span><span class="sxs-lookup"><span data-stu-id="6b79b-170">In your browser, connect to **http://HOSTNAME:8983/solr/#/**, where **HOSTNAME** is the name you determined in the previous steps.</span></span>

    <span data-ttu-id="6b79b-171">Запрос направляется через туннель SSH к пользовательскому веб-интерфейсу Solr в кластере.</span><span class="sxs-lookup"><span data-stu-id="6b79b-171">The request is routed through the SSH tunnel to the Solr web UI on your cluster.</span></span> <span data-ttu-id="6b79b-172">Отображается страница, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="6b79b-172">The page appears similar to the following image:</span></span>

    ![Изображение панели мониторинга Solr](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. <span data-ttu-id="6b79b-174">В левой части окна в раскрывающемся списке **Core Selector** (Базовый селектор) выберите **collection1**.</span><span class="sxs-lookup"><span data-stu-id="6b79b-174">From the left pane, use the **Core Selector** drop-down to select **collection1**.</span></span> <span data-ttu-id="6b79b-175">В разделе **collection1** будет отображено несколько записей.</span><span class="sxs-lookup"><span data-stu-id="6b79b-175">Several entries should them appear below **collection1**.</span></span>

4. <span data-ttu-id="6b79b-176">В разделе **collection1** выберите элемент **Запрос**.</span><span class="sxs-lookup"><span data-stu-id="6b79b-176">From the entries below **collection1**, select **Query**.</span></span> <span data-ttu-id="6b79b-177">На странице поиска введите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="6b79b-177">Use the following values to populate the search page:</span></span>

   * <span data-ttu-id="6b79b-178">В текстовом поле **q** введите **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="6b79b-178">In the **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="6b79b-179">Этот запрос возвращает все документы, индексированные в Solr.</span><span class="sxs-lookup"><span data-stu-id="6b79b-179">This query returns all the documents that are indexed in Solr.</span></span> <span data-ttu-id="6b79b-180">Если требуется найти в документах конкретную строку, ее также можно ввести в этом поле.</span><span class="sxs-lookup"><span data-stu-id="6b79b-180">If you want to search for a specific string within the documents, you can enter that string here.</span></span>
   * <span data-ttu-id="6b79b-181">В текстовом поле **wt** выберите формат выходных данных.</span><span class="sxs-lookup"><span data-stu-id="6b79b-181">In the **wt** text box, select the output format.</span></span> <span data-ttu-id="6b79b-182">По умолчанию используется **JSON**.</span><span class="sxs-lookup"><span data-stu-id="6b79b-182">Default is **json**.</span></span>

     <span data-ttu-id="6b79b-183">Наконец, нажмите кнопку **Execute Query** (Выполнить запрос) в нижней части панели поиска.</span><span class="sxs-lookup"><span data-stu-id="6b79b-183">Finally, select the **Execute Query** button at the bottom of the search pate.</span></span>

     ![Использование действия сценария для настройки кластера](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     <span data-ttu-id="6b79b-185">В выходных данных возвращается два документа, которые вы ранее добавили в индекс.</span><span class="sxs-lookup"><span data-stu-id="6b79b-185">The output returns the two documents that you added to the index earlier.</span></span> <span data-ttu-id="6b79b-186">Выходные данные аналогичны приведенному ниже документу JSON.</span><span class="sxs-lookup"><span data-stu-id="6b79b-186">The output is similar to the following JSON document:</span></span>

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

### <a name="starting-and-stopping-solr"></a><span data-ttu-id="6b79b-187">Запуск и остановка Solr</span><span class="sxs-lookup"><span data-stu-id="6b79b-187">Starting and stopping Solr</span></span>

<span data-ttu-id="6b79b-188">Чтобы вручную остановить или запустить Solr, используйте следующие команды.</span><span class="sxs-lookup"><span data-stu-id="6b79b-188">Use the following commands to manually stop and start Solr:</span></span>

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a><span data-ttu-id="6b79b-189">Резервное копирование индексированных данных</span><span class="sxs-lookup"><span data-stu-id="6b79b-189">Backup indexed data</span></span>

<span data-ttu-id="6b79b-190">Чтобы выполнить архивацию данных Solr в хранилище по умолчанию для кластера, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="6b79b-190">Use the following steps to back up Solr data to the default storage for your cluster:</span></span>

1. <span data-ttu-id="6b79b-191">Подключитесь к кластеру с помощью SSH, а затем используйте следующую команду, чтобы получить имя головного узла:</span><span class="sxs-lookup"><span data-stu-id="6b79b-191">Connect to the cluster using SSH, then use the following command to get the host name for the head node:</span></span>

    ```bash
    hostname -f
    ```

2. <span data-ttu-id="6b79b-192">Чтобы создать моментальный снимок индексированных данных, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="6b79b-192">Use the following command to create a snapshot of the indexed data.</span></span> <span data-ttu-id="6b79b-193">Замените **HOSTNAME** именем, полученным от предыдущей команды:</span><span class="sxs-lookup"><span data-stu-id="6b79b-193">Replace **HOSTNAME** with the name returned from the previous command:</span></span>

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    <span data-ttu-id="6b79b-194">В результате вы получите код XML следующего вида.</span><span class="sxs-lookup"><span data-stu-id="6b79b-194">The response is similar to the following XML:</span></span>

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. <span data-ttu-id="6b79b-195">Перейдите в каталог `/usr/hdp/current/solr/example/solr`.</span><span class="sxs-lookup"><span data-stu-id="6b79b-195">Change directories to `/usr/hdp/current/solr/example/solr`.</span></span> <span data-ttu-id="6b79b-196">В нем находятся подкаталоги для каждой коллекции.</span><span class="sxs-lookup"><span data-stu-id="6b79b-196">There is a subdirectory here for each collection.</span></span> <span data-ttu-id="6b79b-197">Каждый каталог коллекции содержит каталог `data`, в котором хранится моментальный снимок этой коллекции.</span><span class="sxs-lookup"><span data-stu-id="6b79b-197">Each collection directory contains a `data` directory that contains the snapshot for the collection.</span></span>

4. <span data-ttu-id="6b79b-198">Создайте сжатый архив папки с моментальным снимком, используя следующую команду.</span><span class="sxs-lookup"><span data-stu-id="6b79b-198">To create a compressed archive of the snapshot folder, use the following command:</span></span>

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    <span data-ttu-id="6b79b-199">Замените значения `snapshot.20150806185338855` именем моментального снимка коллекции.</span><span class="sxs-lookup"><span data-stu-id="6b79b-199">Replace the `snapshot.20150806185338855` values with the name of the snapshot for your collection.</span></span>

    <span data-ttu-id="6b79b-200">Эта команда создаст архив **snapshot.20150806185338855.tgz**, в который будет помещено содержимое каталога **snapshot.20150806185338855**.</span><span class="sxs-lookup"><span data-stu-id="6b79b-200">This command creates an archive named **snapshot.20150806185338855.tgz**, which contains the contents of the **snapshot.20150806185338855** directory.</span></span>

5. <span data-ttu-id="6b79b-201">Впоследствии вы сможете сохранить архив в основном хранилище кластера, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6b79b-201">You can then store the archive to the cluster's primary storage using the following command:</span></span>

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

<span data-ttu-id="6b79b-202">Дополнительные сведения о резервном копировании и восстановлении Solr см. на странице [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span><span class="sxs-lookup"><span data-stu-id="6b79b-202">For more information on working with Solr backup and restores, see [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b79b-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6b79b-203">Next steps</span></span>

* <span data-ttu-id="6b79b-204">[Установка Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6b79b-204">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="6b79b-205">Используйте настройки кластера для установки Giraph в кластерах HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6b79b-205">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="6b79b-206">Giraph позволяет выполнять обработку графов с использованием Hadoop и может использоваться с Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6b79b-206">Giraph allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="6b79b-207">[Установка Hue в кластерах HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6b79b-207">[Install Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="6b79b-208">Установить Hue в кластерах HDInsight Hadoop можно при помощи настройки кластера.</span><span class="sxs-lookup"><span data-stu-id="6b79b-208">Use cluster customization to install Hue on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="6b79b-209">Hue — это набор веб-приложений, используемых для взаимодействия с кластером Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6b79b-209">Hue is a set of Web applications used to interact with a Hadoop cluster.</span></span>

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
