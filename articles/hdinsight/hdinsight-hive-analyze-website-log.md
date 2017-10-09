---
title: "aaaUse Hive в Hadoop для анализа журналов веб-сайт - Azure HDInsight | Документы Microsoft"
description: "Узнайте, каким образом ведет журнал toouse Hive с HDInsight tooanalyze веб-сайта. Будет использовать в качестве входных данных в таблицу HDInsight файл журнала, а также использовать данные hello tooquery HiveQL."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6fb7b5c2-8df4-40b1-a9e2-6815080004f9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 9cbce3cc8cf8bc3ad104dc4ca6a5628802c8fe89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-windows-based-hdinsight-tooanalyze-logs-from-websites"></a><span data-ttu-id="82025-104">Используйте Hive с журналами tooanalyze HDInsight под управлением Windows с веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="82025-104">Use Hive with Windows-based HDInsight tooanalyze logs from websites</span></span>
<span data-ttu-id="82025-105">Узнайте, как toouse HiveQL с HDInsight tooanalyze журналы с веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="82025-105">Learn how toouse HiveQL with HDInsight tooanalyze logs from a website.</span></span> <span data-ttu-id="82025-106">Анализ журнала веб-сайта можно использовать toosegment аудиторию, в зависимости от подобные действия, классификации посетителей, демографические данные и toofind содержимое hello просматриваемого, hello веб-сайтов, которые они появились и т. д.</span><span class="sxs-lookup"><span data-stu-id="82025-106">Website log analysis can be used toosegment your audience based on similar activities, categorize site visitors by demographics, and toofind out hello content they view, hello websites they come from, and so on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82025-107">Hello шагов в этот документ корректно работать только с кластерами HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="82025-107">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="82025-108">Для версий ниже HDInsight 3.4 кластер HDInsight доступен только в Windows.</span><span class="sxs-lookup"><span data-stu-id="82025-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="82025-109">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="82025-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="82025-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="82025-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="82025-111">В этом образце используется HDInsight кластера tooanalyze веб-сайта журнала файлы tooget понимание частоты hello с внешних веб-сайтов с веб-сайта toohello посещений в день.</span><span class="sxs-lookup"><span data-stu-id="82025-111">In this sample, you will use an HDInsight cluster tooanalyze website log files tooget insight into hello frequency of visits toohello website from external websites in a day.</span></span> <span data-ttu-id="82025-112">Можно также создать сводку ошибок веб-сайт hello пользователей.</span><span class="sxs-lookup"><span data-stu-id="82025-112">You'll also generate a summary of website errors that hello users experience.</span></span> <span data-ttu-id="82025-113">Вы научитесь:</span><span class="sxs-lookup"><span data-stu-id="82025-113">You will learn how to:</span></span>

* <span data-ttu-id="82025-114">Подключите tooa хранилища больших двоичных объектов Azure, который содержит файлы журналов веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="82025-114">Connect tooa Azure Blob storage, which contains website log files.</span></span>
* <span data-ttu-id="82025-115">Создание таблицы HIVE, tooquery эти журналы.</span><span class="sxs-lookup"><span data-stu-id="82025-115">Create HIVE tables tooquery those logs.</span></span>
* <span data-ttu-id="82025-116">Создание запросов HIVE tooanalyze hello данных.</span><span class="sxs-lookup"><span data-stu-id="82025-116">Create HIVE queries tooanalyze hello data.</span></span>
* <span data-ttu-id="82025-117">Используйте tooHDInsight tooconnect Microsoft Excel (с помощью открыть базу данных (ODBC) tooretrieve hello проанализировать данные подключения.</span><span class="sxs-lookup"><span data-stu-id="82025-117">Use Microsoft Excel tooconnect tooHDInsight (by using open database connectivity (ODBC) tooretrieve hello analyzed data.</span></span>

![HDI.Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a><span data-ttu-id="82025-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="82025-119">Prerequisites</span></span>
* <span data-ttu-id="82025-120">Вы должны были подготовить кластер Hadoop в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="82025-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span></span> <span data-ttu-id="82025-121">Инструкции см. в статье [Создание кластеров Hadoop под управлением Windows в HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="82025-121">For instructions, see [Provision HDInsight Clusters][hdinsight-provision].</span></span>
* <span data-ttu-id="82025-122">У вас должен быть установлен Microsoft Excel 2013 или Microsoft Excel 2010.</span><span class="sxs-lookup"><span data-stu-id="82025-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span></span>
* <span data-ttu-id="82025-123">Необходимо иметь [драйвер Microsoft ODBC Hive](http://www.microsoft.com/download/details.aspx?id=40886) tooimport данных из куста в Excel.</span><span class="sxs-lookup"><span data-stu-id="82025-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) tooimport data from Hive into Excel.</span></span>

## <a name="toorun-hello-sample"></a><span data-ttu-id="82025-124">Образец hello toorun</span><span class="sxs-lookup"><span data-stu-id="82025-124">toorun hello sample</span></span>
1. <span data-ttu-id="82025-125">Из hello [портала Azure](https://portal.azure.com/), из hello начальной панели (если существует кластера hello закрепленной), щелкните плитку hello кластера, на котором будет toorun образец hello.</span><span class="sxs-lookup"><span data-stu-id="82025-125">From hello [Azure Portal](https://portal.azure.com/), from hello Startboard (if you pinned hello cluster there), click hello cluster tile on which you want toorun hello sample.</span></span>
2. <span data-ttu-id="82025-126">Из hello кластера колонки, в разделе **быстрые ссылки**, нажмите кнопку **мониторинга кластера**, а затем из hello **мониторинга кластера** колонке нажмите кнопку **кластера HDInsight Панель мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="82025-126">From hello cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from hello **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="82025-127">Кроме того вы можете напрямую открыть hello панели мониторинга с помощью hello URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="82025-127">Alternatively, you can directly open hello dashboard by using hello following URL:</span></span>

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="82025-128">В ответ на запрос проверки подлинности, используя имя пользователя администратора hello и пароль, используемый при подготовке кластера hello.</span><span class="sxs-lookup"><span data-stu-id="82025-128">When prompted, authenticate by using hello administrator user name and password you used when provisioning hello cluster.</span></span>
3. <span data-ttu-id="82025-129">Hello открывшейся веб-странице, щелкните hello **Приступая к работе коллекции** вкладку и затем в разделе hello **решений с образцами данных** категории, щелкните hello **анализ журнала веб-сайт** Пример.</span><span class="sxs-lookup"><span data-stu-id="82025-129">From hello web page that opens, click hello **Getting Started Gallery** tab, and then under hello **Solutions with Sample Data** category, click hello **Website Log Analysis** sample.</span></span>
4. <span data-ttu-id="82025-130">Следуйте инструкциям hello hello образец hello toofinish веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="82025-130">Follow hello instructions provided on hello web page toofinish hello sample.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82025-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="82025-131">Next steps</span></span>
<span data-ttu-id="82025-132">Повторите следующие образец hello: [анализ данных датчика, с помощью Hive в HDInsight](hdinsight-hive-analyze-sensor-data.md).</span><span class="sxs-lookup"><span data-stu-id="82025-132">Try hello following sample: [Analyzing sensor data using Hive with HDInsight](hdinsight-hive-analyze-sensor-data.md).</span></span>

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
