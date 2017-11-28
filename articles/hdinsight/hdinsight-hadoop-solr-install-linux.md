---
title: "Действие сценария aaaUse tooinstall Solr на HDInsight под управлением Linux — в Azure | Документы Microsoft"
description: "Узнайте, как tooinstall Solr на основе Linux HDInsight Hadoop кластеры, использующие действий скрипта."
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
ms.openlocfilehash: 4c179032b95ae187f1830d8927f8796372fa8ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="6f637-103">Установка и использование Solr на кластерах HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="6f637-103">Install and use Solr on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="6f637-104">Узнайте, как tooinstall Solr на Azure HDInsight с помощью действия сценария.</span><span class="sxs-lookup"><span data-stu-id="6f637-104">Learn how tooinstall Solr on Azure HDInsight by using Script Action.</span></span> <span data-ttu-id="6f637-105">Solr представляет собой многофункциональную платформу поиска и предоставляет возможности поиска корпоративного уровня на основе данных, управляемых Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6f637-105">Solr is a powerful search platform and provides enterprise-level search capabilities on data managed by Hadoop.</span></span>

> [!IMPORTANT]
    > <span data-ttu-id="6f637-106">Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux.</span><span class="sxs-lookup"><span data-stu-id="6f637-106">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="6f637-107">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="6f637-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6f637-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6f637-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6f637-109">Пример сценария Hello, используемые в этом документе устанавливает Solr 4.9 с указанной конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="6f637-109">hello sample script used in this document installs Solr 4.9 with a specific configuration.</span></span> <span data-ttu-id="6f637-110">Следует tooconfigure hello Solr кластера с помощью различных коллекций, сегментами, схемы, реплики, т. д. необходимо изменить скрипт hello и двоичные файлы Solr.</span><span class="sxs-lookup"><span data-stu-id="6f637-110">If you want tooconfigure hello Solr cluster with different collections, shards, schemas, replicas, etc., you must modify hello script and Solr binaries.</span></span>

## <span data-ttu-id="6f637-111"><a name="whatis"></a>Что такое Solr</span><span class="sxs-lookup"><span data-stu-id="6f637-111"><a name="whatis"></a>What is Solr</span></span>

<span data-ttu-id="6f637-112">[Apache Solr](http://lucene.apache.org/solr/features.html) — это корпоративная платформа поиска, предоставляющая многофункциональные инструменты полнотекстового поиска данных.</span><span class="sxs-lookup"><span data-stu-id="6f637-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="6f637-113">Хотя Hadoop позволяет хранения и управления огромный объем данных, Apache Solr предоставляет возможности поиска hello tooquickly извлекать данные hello.</span><span class="sxs-lookup"><span data-stu-id="6f637-113">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides hello search capabilities tooquickly retrieve hello data.</span></span>

> [!WARNING]
> <span data-ttu-id="6f637-114">Компоненты, предоставляемые с кластером HDInsight hello полностью поддерживаются корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6f637-114">Components provided with hello HDInsight cluster are fully supported by Microsoft.</span></span>
>
> <span data-ttu-id="6f637-115">Пользовательские компоненты, такие как Solr, получать toohelp ограниченную техническую поддержку вы toofurther устранить проблему hello.</span><span class="sxs-lookup"><span data-stu-id="6f637-115">Custom components, such as Solr, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="6f637-116">Службы поддержки Майкрософт не может быть может tooresolve проблемы при пользовательские компоненты.</span><span class="sxs-lookup"><span data-stu-id="6f637-116">Microsoft support may not be able tooresolve problems with custom components.</span></span> <span data-ttu-id="6f637-117">Может потребоваться tooengage hello сообществе открытого для получения помощи.</span><span class="sxs-lookup"><span data-stu-id="6f637-117">You may need tooengage hello open source communities for assistance.</span></span> <span data-ttu-id="6f637-118">Можно использовать ряд сайтов сообществ, например [форум MSDN по HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) или [http://stackoverflow.com](http://stackoverflow.com). Кроме того, для проектов Apache есть соответствующие сайты, например [Hadoop](http://hadoop.apache.org/) на сайте [http://apache.org](http://apache.org).</span><span class="sxs-lookup"><span data-stu-id="6f637-118">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

## <a name="what-hello-script-does"></a><span data-ttu-id="6f637-119">Какие hello скрипта</span><span class="sxs-lookup"><span data-stu-id="6f637-119">What hello script does</span></span>

<span data-ttu-id="6f637-120">Этот сценарий вносит следующие изменения кластера HDInsight toohello hello:</span><span class="sxs-lookup"><span data-stu-id="6f637-120">This script makes hello following changes toohello HDInsight cluster:</span></span>

* <span data-ttu-id="6f637-121">Устанавливает Solr 4.9 в `/usr/hdp/current/solr`.</span><span class="sxs-lookup"><span data-stu-id="6f637-121">Installs Solr 4.9 into `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="6f637-122">Создает пользователя, **solrusr**, являющееся hello используется toorun Solr службы</span><span class="sxs-lookup"><span data-stu-id="6f637-122">Creates a user, **solrusr**, which is used toorun hello Solr service</span></span>
* <span data-ttu-id="6f637-123">Наборы **solruser** как владелец hello`/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="6f637-123">Sets **solruser** as hello owner of `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="6f637-124">Добавляет конфигурацию [Upstart](http://upstart.ubuntu.com/), которая автоматически запускает Solr.</span><span class="sxs-lookup"><span data-stu-id="6f637-124">Adds an [Upstart](http://upstart.ubuntu.com/) configuration that starts Solr automatically.</span></span>

## <span data-ttu-id="6f637-125"><a name="install"></a>Установка Solr с помощью действий сценария</span><span class="sxs-lookup"><span data-stu-id="6f637-125"><a name="install"></a>Install Solr using Script Actions</span></span>

<span data-ttu-id="6f637-126">Пример сценария tooinstall Solr в кластере HDInsight доступна на hello следующие расположения:</span><span class="sxs-lookup"><span data-stu-id="6f637-126">A sample script tooinstall Solr on an HDInsight cluster is available at hello following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

<span data-ttu-id="6f637-127">toocreate кластер с Solr установлен hello используйте шаги в hello [HDInsight, создания кластеров](hdinsight-hadoop-create-linux-clusters-portal.md) документа.</span><span class="sxs-lookup"><span data-stu-id="6f637-127">toocreate a cluster that has Solr installed, use hello steps in hello [Create HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span></span> <span data-ttu-id="6f637-128">Во время процесса создания hello используйте следующие шаги tooinstall Solr hello.</span><span class="sxs-lookup"><span data-stu-id="6f637-128">During hello creation process, use hello following steps tooinstall Solr:</span></span>

1. <span data-ttu-id="6f637-129">Из hello __Сводка кластера__ колонки, select__Advanced settings__, затем __скрипт действия__.</span><span class="sxs-lookup"><span data-stu-id="6f637-129">From hello __Cluster summary__ blade, select__Advanced settings__, then __Script actions__.</span></span> <span data-ttu-id="6f637-130">Используйте следующие сведения toopopulate hello формы hello.</span><span class="sxs-lookup"><span data-stu-id="6f637-130">Use hello following information toopopulate hello form:</span></span>

   * <span data-ttu-id="6f637-131">**ИМЯ**: Введите понятное имя для действия сценария hello.</span><span class="sxs-lookup"><span data-stu-id="6f637-131">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="6f637-132">**Универсальный код ресурса скрипта**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/r-installer-v01.sh.</span><span class="sxs-lookup"><span data-stu-id="6f637-132">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span></span>
   * <span data-ttu-id="6f637-133">**ГОЛОВНОЙ**: установите флажок.</span><span class="sxs-lookup"><span data-stu-id="6f637-133">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="6f637-134">**Рабочая роль**: установите флажок.</span><span class="sxs-lookup"><span data-stu-id="6f637-134">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="6f637-135">**ZOOKEEPER**: Проверьте tooinstall этот параметр на узле Zookeeper hello</span><span class="sxs-lookup"><span data-stu-id="6f637-135">**ZOOKEEPER**: Check this option tooinstall on hello Zookeeper node</span></span>
   * <span data-ttu-id="6f637-136">**ПАРАМЕТРЫ**: оставьте это поле пустым.</span><span class="sxs-lookup"><span data-stu-id="6f637-136">**PARAMETERS**: Leave this field blank</span></span>

2. <span data-ttu-id="6f637-137">Внизу hello hello **скрипт действия** колонки, используйте hello **выберите** конфигурация hello toosave кнопок.</span><span class="sxs-lookup"><span data-stu-id="6f637-137">At hello bottom of hello **Script actions** blade, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="6f637-138">Наконец, используйте hello **Далее** toohello tooreturn кнопку __Сводка кластера__</span><span class="sxs-lookup"><span data-stu-id="6f637-138">Finally, use hello **Next** button tooreturn toohello __Cluster summary__</span></span>

3. <span data-ttu-id="6f637-139">Из hello __Сводка кластера__ выберите __создать__ toocreate hello кластера.</span><span class="sxs-lookup"><span data-stu-id="6f637-139">From hello __Cluster summary__ page, select __Create__ toocreate hello cluster.</span></span>

## <span data-ttu-id="6f637-140"><a name="usesolr"></a>Как использовать Solr в HDInsight</span><span class="sxs-lookup"><span data-stu-id="6f637-140"><a name="usesolr"></a>How do I use Solr in HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6f637-141">Hello шаги в этом разделе показывают основные функциональные возможности Solr.</span><span class="sxs-lookup"><span data-stu-id="6f637-141">hello steps in this section demonstrate basic Solr functionality.</span></span> <span data-ttu-id="6f637-142">Дополнительные сведения об использовании Solr см. в разделе hello [Apache Solr сайта](http://lucene.apache.org/solr/).</span><span class="sxs-lookup"><span data-stu-id="6f637-142">For more information on using Solr, see hello [Apache Solr site](http://lucene.apache.org/solr/).</span></span>

### <a name="index-data"></a><span data-ttu-id="6f637-143">Данные индекса</span><span class="sxs-lookup"><span data-stu-id="6f637-143">Index data</span></span>

<span data-ttu-id="6f637-144">Используйте следующие шаги tooadd пример данных tooSolr hello и затем запрос:</span><span class="sxs-lookup"><span data-stu-id="6f637-144">Use hello following steps tooadd example data tooSolr, and then query it:</span></span>

1. <span data-ttu-id="6f637-145">Подключите кластер HDInsight toohello с помощью SSH:</span><span class="sxs-lookup"><span data-stu-id="6f637-145">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="6f637-146">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6f637-146">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="6f637-147">Позже в данном пошаговом руководстве используется SSL туннеля tooconnect toohello Solr пользовательского веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="6f637-147">Steps later in this document use an SSL tunnel tooconnect toohello Solr web UI.</span></span> <span data-ttu-id="6f637-148">toouse следующие действия, необходимо установить SSL туннелирования, а затем настройте Ваш браузер toouse его.</span><span class="sxs-lookup"><span data-stu-id="6f637-148">toouse these steps, you must establish an SSL tunnel and then configure your browser toouse it.</span></span>
     >
     > <span data-ttu-id="6f637-149">Дополнительные сведения см. в разделе hello [использование SSH туннелирование с HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) документа.</span><span class="sxs-lookup"><span data-stu-id="6f637-149">For more information, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="6f637-150">Используйте hello, следующие команды toohave Solr индекс образец данных:</span><span class="sxs-lookup"><span data-stu-id="6f637-150">Use hello following commands toohave Solr index sample data:</span></span>

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    <span data-ttu-id="6f637-151">Hello следующие выходные данные возвращаются в консоли toohello:</span><span class="sxs-lookup"><span data-stu-id="6f637-151">hello following output is returned toohello console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="6f637-152">Hello `post.jar` программа добавляет hello **solr.xml** и **monitor.xml** документов toohello индекса.</span><span class="sxs-lookup"><span data-stu-id="6f637-152">hello `post.jar` utility adds hello **solr.xml** and **monitor.xml** documents toohello index.</span></span>
  
3. <span data-ttu-id="6f637-153">Используйте hello следующая команда hello tooquery Solr REST API:</span><span class="sxs-lookup"><span data-stu-id="6f637-153">Use hello following command tooquery hello Solr REST API:</span></span>

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    <span data-ttu-id="6f637-154">Эта команда ищет **collection1** для документов, соответствующих  **\*:\***  (кодируются как \*% 3A\* в строке запроса hello).</span><span class="sxs-lookup"><span data-stu-id="6f637-154">This command searches **collection1** for any documents matching **\*:\*** (encoded as \*%3A\* in hello query string).</span></span> <span data-ttu-id="6f637-155">Следующий документ JSON Hello приведен пример ответа hello.</span><span class="sxs-lookup"><span data-stu-id="6f637-155">hello following JSON document is an example of hello response:</span></span>

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

### <a name="using-hello-solr-dashboard"></a><span data-ttu-id="6f637-156">С помощью панели мониторинга Solr hello</span><span class="sxs-lookup"><span data-stu-id="6f637-156">Using hello Solr dashboard</span></span>

<span data-ttu-id="6f637-157">панель мониторинга Solr Hello является веб-интерфейса, который позволяет вам toowork с Solr через веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="6f637-157">hello Solr dashboard is a web UI that allows you toowork with Solr through your web browser.</span></span> <span data-ttu-id="6f637-158">панель мониторинга Solr Hello не представлено напрямую в hello Интернет из кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6f637-158">hello Solr dashboard is not exposed directly on hello Internet from your HDInsight cluster.</span></span> <span data-ttu-id="6f637-159">Можно использовать tooaccess туннель SSH его.</span><span class="sxs-lookup"><span data-stu-id="6f637-159">You can use an SSH tunnel tooaccess it.</span></span> <span data-ttu-id="6f637-160">Дополнительные сведения об использовании туннель SSH см. в разделе hello [использование SSH туннелирование с HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) документа.</span><span class="sxs-lookup"><span data-stu-id="6f637-160">For more information on using an SSH tunnel, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="6f637-161">После установления туннель SSH, используйте следующие шаги toouse hello Solr мониторинга hello:</span><span class="sxs-lookup"><span data-stu-id="6f637-161">Once you have established an SSH tunnel, use hello following steps toouse hello Solr dashboard:</span></span>

1. <span data-ttu-id="6f637-162">Укажите имя узла hello для основной hello головному узлу:</span><span class="sxs-lookup"><span data-stu-id="6f637-162">Determine hello host name for hello primary headnode:</span></span>

   1. <span data-ttu-id="6f637-163">Использование SSH tooconnect toohello головного узла кластера.</span><span class="sxs-lookup"><span data-stu-id="6f637-163">Use SSH tooconnect toohello cluster head node.</span></span> <span data-ttu-id="6f637-164">Например, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="6f637-164">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

       <span data-ttu-id="6f637-165">Дополнительные сведения об использовании SSH см. в разделе hello [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6f637-165">For more information on using SSH, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

   2. <span data-ttu-id="6f637-166">Используйте следующую команду, tooget hello полное имя узла hello.</span><span class="sxs-lookup"><span data-stu-id="6f637-166">Use hello following command tooget hello fully qualified hostname:</span></span>

        ```bash
        hostname -f
        ```

        <span data-ttu-id="6f637-167">Эта команда возвращает значение аналогичные toohello, за которым следует имя узла:</span><span class="sxs-lookup"><span data-stu-id="6f637-167">This command returns a value similar toohello following host name:</span></span>

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        <span data-ttu-id="6f637-168">Сохраните возвращенное hello, как будет использоваться позднее.</span><span class="sxs-lookup"><span data-stu-id="6f637-168">Save hello value returned, as it is used later.</span></span>

2. <span data-ttu-id="6f637-169">В окне браузера подключитесь слишком**http://HOSTNAME:8983/solr / #/**, где **HOSTNAME** является именем hello, определенным в предыдущих шагах hello.</span><span class="sxs-lookup"><span data-stu-id="6f637-169">In your browser, connect too**http://HOSTNAME:8983/solr/#/**, where **HOSTNAME** is hello name you determined in hello previous steps.</span></span>

    <span data-ttu-id="6f637-170">Hello запросы направляются через hello SSH туннеля toohello Solr веб-интерфейса в кластере.</span><span class="sxs-lookup"><span data-stu-id="6f637-170">hello request is routed through hello SSH tunnel toohello Solr web UI on your cluster.</span></span> <span data-ttu-id="6f637-171">Откроется страница приветствия аналогичные toohello после изображения:</span><span class="sxs-lookup"><span data-stu-id="6f637-171">hello page appears similar toohello following image:</span></span>

    ![Изображение панели мониторинга Solr](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. <span data-ttu-id="6f637-173">В левой области hello, используйте hello **селектор Core** tooselect раскрывающегося списка **collection1**.</span><span class="sxs-lookup"><span data-stu-id="6f637-173">From hello left pane, use hello **Core Selector** drop-down tooselect **collection1**.</span></span> <span data-ttu-id="6f637-174">В разделе **collection1** будет отображено несколько записей.</span><span class="sxs-lookup"><span data-stu-id="6f637-174">Several entries should them appear below **collection1**.</span></span>

4. <span data-ttu-id="6f637-175">В следующих операциях hello **collection1**выберите **запроса**.</span><span class="sxs-lookup"><span data-stu-id="6f637-175">From hello entries below **collection1**, select **Query**.</span></span> <span data-ttu-id="6f637-176">Используйте следующие страницы поиска значений toopopulate hello hello.</span><span class="sxs-lookup"><span data-stu-id="6f637-176">Use hello following values toopopulate hello search page:</span></span>

   * <span data-ttu-id="6f637-177">В hello **q** текста введите  **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="6f637-177">In hello **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="6f637-178">Этот запрос возвращает все документы hello, которые индексируются в Solr.</span><span class="sxs-lookup"><span data-stu-id="6f637-178">This query returns all hello documents that are indexed in Solr.</span></span> <span data-ttu-id="6f637-179">Если требуется toosearch конкретную строку в документах hello, можно ввести здесь строку.</span><span class="sxs-lookup"><span data-stu-id="6f637-179">If you want toosearch for a specific string within hello documents, you can enter that string here.</span></span>
   * <span data-ttu-id="6f637-180">В hello **wt** текстовое поле, выберите hello выходной формат.</span><span class="sxs-lookup"><span data-stu-id="6f637-180">In hello **wt** text box, select hello output format.</span></span> <span data-ttu-id="6f637-181">По умолчанию используется **JSON**.</span><span class="sxs-lookup"><span data-stu-id="6f637-181">Default is **json**.</span></span>

     <span data-ttu-id="6f637-182">Наконец, выберите hello **выполнить запрос** кнопку внизу hello pate поиска hello.</span><span class="sxs-lookup"><span data-stu-id="6f637-182">Finally, select hello **Execute Query** button at hello bottom of hello search pate.</span></span>

     ![Используйте действие скрипта toocustomize кластера](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     <span data-ttu-id="6f637-184">Hello выходных данных возвращается hello, в которых два документа, что вы добавили toohello индекса более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="6f637-184">hello output returns hello two documents that you added toohello index earlier.</span></span> <span data-ttu-id="6f637-185">Hello выходные данные, аналогичные toohello следовать документ JSON:</span><span class="sxs-lookup"><span data-stu-id="6f637-185">hello output is similar toohello following JSON document:</span></span>

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

### <a name="starting-and-stopping-solr"></a><span data-ttu-id="6f637-186">Запуск и остановка Solr</span><span class="sxs-lookup"><span data-stu-id="6f637-186">Starting and stopping Solr</span></span>

<span data-ttu-id="6f637-187">Используйте следующие команды toomanually остановить и запустить Solr hello.</span><span class="sxs-lookup"><span data-stu-id="6f637-187">Use hello following commands toomanually stop and start Solr:</span></span>

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a><span data-ttu-id="6f637-188">Резервное копирование индексированных данных</span><span class="sxs-lookup"><span data-stu-id="6f637-188">Backup indexed data</span></span>

<span data-ttu-id="6f637-189">Используйте следующие шаги tooback хранилищ Solr данных toohello по умолчанию для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="6f637-189">Use hello following steps tooback up Solr data toohello default storage for your cluster:</span></span>

1. <span data-ttu-id="6f637-190">Подключите кластер toohello с помощью SSH, а затем использовать после имени узла hello tooget команды для головного узла hello hello:</span><span class="sxs-lookup"><span data-stu-id="6f637-190">Connect toohello cluster using SSH, then use hello following command tooget hello host name for hello head node:</span></span>

    ```bash
    hostname -f
    ```

2. <span data-ttu-id="6f637-191">Следующая команда toocreate моментальный снимок hello hello использование индексированных данных.</span><span class="sxs-lookup"><span data-stu-id="6f637-191">Use hello following command toocreate a snapshot of hello indexed data.</span></span> <span data-ttu-id="6f637-192">Замените **HOSTNAME** с именем hello, возвращенные hello предыдущей команде:</span><span class="sxs-lookup"><span data-stu-id="6f637-192">Replace **HOSTNAME** with hello name returned from hello previous command:</span></span>

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    <span data-ttu-id="6f637-193">Hello ответ — примерно toohello следующий XML-код:</span><span class="sxs-lookup"><span data-stu-id="6f637-193">hello response is similar toohello following XML:</span></span>

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. <span data-ttu-id="6f637-194">Измените каталоги слишком`/usr/hdp/current/solr/example/solr`.</span><span class="sxs-lookup"><span data-stu-id="6f637-194">Change directories too`/usr/hdp/current/solr/example/solr`.</span></span> <span data-ttu-id="6f637-195">В нем находятся подкаталоги для каждой коллекции.</span><span class="sxs-lookup"><span data-stu-id="6f637-195">There is a subdirectory here for each collection.</span></span> <span data-ttu-id="6f637-196">Каждый каталог коллекции содержит `data` каталог, содержащий hello моментальных снимков для hello коллекции.</span><span class="sxs-lookup"><span data-stu-id="6f637-196">Each collection directory contains a `data` directory that contains hello snapshot for hello collection.</span></span>

4. <span data-ttu-id="6f637-197">toocreate собой сжатый архив папки моментальных снимков hello, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6f637-197">toocreate a compressed archive of hello snapshot folder, use hello following command:</span></span>

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    <span data-ttu-id="6f637-198">Замените hello `snapshot.20150806185338855` значения с именем hello hello моментального снимка для коллекции.</span><span class="sxs-lookup"><span data-stu-id="6f637-198">Replace hello `snapshot.20150806185338855` values with hello name of hello snapshot for your collection.</span></span>

    <span data-ttu-id="6f637-199">Эта команда создает архив с именем **snapshot.20150806185338855.tgz**, который содержит содержимое hello hello **snapshot.20150806185338855** каталога.</span><span class="sxs-lookup"><span data-stu-id="6f637-199">This command creates an archive named **snapshot.20150806185338855.tgz**, which contains hello contents of hello **snapshot.20150806185338855** directory.</span></span>

5. <span data-ttu-id="6f637-200">Затем можно сохранить основное хранилище hello архив toohello кластера с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6f637-200">You can then store hello archive toohello cluster's primary storage using hello following command:</span></span>

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

<span data-ttu-id="6f637-201">Дополнительные сведения о резервном копировании и восстановлении Solr см. на странице [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span><span class="sxs-lookup"><span data-stu-id="6f637-201">For more information on working with Solr backup and restores, see [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f637-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6f637-202">Next steps</span></span>

* <span data-ttu-id="6f637-203">[Установка Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6f637-203">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="6f637-204">Используйте tooinstall настройки кластера кластеров Giraph на HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6f637-204">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="6f637-205">Giraph дает graph tooperform обработки с помощью Hadoop и может использоваться с Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6f637-205">Giraph allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="6f637-206">[Установка Hue в кластерах HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6f637-206">[Install Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="6f637-207">Используйте оттенка tooinstall настройки кластера в кластерах HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6f637-207">Use cluster customization tooinstall Hue on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="6f637-208">Цветовой тон представляет собой набор веб-приложений, используемых toointeract в кластере Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6f637-208">Hue is a set of Web applications used toointeract with a Hadoop cluster.</span></span>

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
