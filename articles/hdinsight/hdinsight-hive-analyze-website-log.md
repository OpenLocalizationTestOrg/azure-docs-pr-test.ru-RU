---
title: "Использование Hive и Hadoop для анализа журнала веб-сайта. Azure HDInsight | Документация Майкрософт"
description: "Узнайте, как использовать Hive с HDInsight для анализа журналов веб-сайтов. Вы будете использовать файл журнала в качестве входных данных для таблицы HDInsight, а также HiveQL для формирования запроса к данным."
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
ms.openlocfilehash: e1cdb786bb6049980aafc0213abf53013e342618
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-hive-with-windows-based-hdinsight-to-analyze-logs-from-websites"></a><span data-ttu-id="7fc59-104">Использование Hive c HDInsight под управлением Windows для анализа журналов веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="7fc59-104">Use Hive with Windows-based HDInsight to analyze logs from websites</span></span>
<span data-ttu-id="7fc59-105">Узнайте, как использовать HiveQL с HDInsight для анализа журналов веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="7fc59-105">Learn how to use HiveQL with HDInsight to analyze logs from a website.</span></span> <span data-ttu-id="7fc59-106">Анализ журнала веб-сайта можно использовать для разделения аудитории на основе аналогичной деятельности, классификации посетителей сайта по демографическим данным, а также выявления просмотренного ими содержимого, посещенных сайтов и так далее.</span><span class="sxs-lookup"><span data-stu-id="7fc59-106">Website log analysis can be used to segment your audience based on similar activities, categorize site visitors by demographics, and to find out the content they view, the websites they come from, and so on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7fc59-107">Шаги, описанные в этом документе, можно применять только к кластерам HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="7fc59-107">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="7fc59-108">Для версий ниже HDInsight 3.4 кластер HDInsight доступен только в Windows.</span><span class="sxs-lookup"><span data-stu-id="7fc59-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="7fc59-109">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="7fc59-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7fc59-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7fc59-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="7fc59-111">В данном примере для анализа файлов журнала веб-сайта вы будете использовать кластер HDInsight, чтобы получить представление о дневной частоте посещений веб-сайта из внешних сайтов.</span><span class="sxs-lookup"><span data-stu-id="7fc59-111">In this sample, you will use an HDInsight cluster to analyze website log files to get insight into the frequency of visits to the website from external websites in a day.</span></span> <span data-ttu-id="7fc59-112">Также вы сформируете сводку по ошибкам веб-сайта, с которыми столкнулись пользователи.</span><span class="sxs-lookup"><span data-stu-id="7fc59-112">You'll also generate a summary of website errors that the users experience.</span></span> <span data-ttu-id="7fc59-113">Вы научитесь:</span><span class="sxs-lookup"><span data-stu-id="7fc59-113">You will learn how to:</span></span>

* <span data-ttu-id="7fc59-114">подключаться к хранилищу больших двоичных объектов Azure, которое содержит файлы журнала веб-сайта;</span><span class="sxs-lookup"><span data-stu-id="7fc59-114">Connect to a Azure Blob storage, which contains website log files.</span></span>
* <span data-ttu-id="7fc59-115">создавать таблицы HIVE для формирования запросов к этим журналам;</span><span class="sxs-lookup"><span data-stu-id="7fc59-115">Create HIVE tables to query those logs.</span></span>
* <span data-ttu-id="7fc59-116">создавать запросы HIVE для анализа данных;</span><span class="sxs-lookup"><span data-stu-id="7fc59-116">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="7fc59-117">использовать Microsoft Excel для подключения к HDInsight (с помощью подключения ODBC), чтобы извлекать проанализированные данные.</span><span class="sxs-lookup"><span data-stu-id="7fc59-117">Use Microsoft Excel to connect to HDInsight (by using open database connectivity (ODBC) to retrieve the analyzed data.</span></span>

![HDI.Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a><span data-ttu-id="7fc59-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7fc59-119">Prerequisites</span></span>
* <span data-ttu-id="7fc59-120">Вы должны были подготовить кластер Hadoop в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7fc59-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span></span> <span data-ttu-id="7fc59-121">Инструкции см. в статье [Создание кластеров Hadoop под управлением Windows в HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="7fc59-121">For instructions, see [Provision HDInsight Clusters][hdinsight-provision].</span></span>
* <span data-ttu-id="7fc59-122">У вас должен быть установлен Microsoft Excel 2013 или Microsoft Excel 2010.</span><span class="sxs-lookup"><span data-stu-id="7fc59-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span></span>
* <span data-ttu-id="7fc59-123">У вас должен быть [Microsoft Hive ODBC драйвер](http://www.microsoft.com/download/details.aspx?id=40886) для импорта данных из Hive в Excel.</span><span class="sxs-lookup"><span data-stu-id="7fc59-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) to import data from Hive into Excel.</span></span>

## <a name="to-run-the-sample"></a><span data-ttu-id="7fc59-124">Запуск образца</span><span class="sxs-lookup"><span data-stu-id="7fc59-124">To run the sample</span></span>
1. <span data-ttu-id="7fc59-125">На начальной панели (если кластер закреплен на ней) [портала Azure](https://portal.azure.com/)щелкните элемент кластера, в котором требуется запустить данный пример.</span><span class="sxs-lookup"><span data-stu-id="7fc59-125">From the [Azure Portal](https://portal.azure.com/), from the Startboard (if you pinned the cluster there), click the cluster tile on which you want to run the sample.</span></span>
2. <span data-ttu-id="7fc59-126">В колонке кластера в разделе **Быстрые ссылки** щелкните **Панель мониторинга кластера**, а затем в колонке **Панель мониторинга кластера** щелкните **Панель мониторинга кластера HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7fc59-126">From the cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from the **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="7fc59-127">Панель мониторинга также можно открыть напрямую с помощью следующего URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="7fc59-127">Alternatively, you can directly open the dashboard by using the following URL:</span></span>

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="7fc59-128">В ответ на запрос выполните аутентификацию с помощью имени пользователя и пароля администратора, использованных при подготовке данного кластера.</span><span class="sxs-lookup"><span data-stu-id="7fc59-128">When prompted, authenticate by using the administrator user name and password you used when provisioning the cluster.</span></span>
3. <span data-ttu-id="7fc59-129">На открывшейся веб-странице выберите вкладку **Getting Started Gallery** (Коллекция для начала работы), а затем в категории **Solutions with Sample Data** (Решения с примером данных) щелкните пример **Анализ журналов веб-сайта**.</span><span class="sxs-lookup"><span data-stu-id="7fc59-129">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Website Log Analysis** sample.</span></span>
4. <span data-ttu-id="7fc59-130">Следуйте инструкциям, представленным на веб-странице, чтобы закончить образец.</span><span class="sxs-lookup"><span data-stu-id="7fc59-130">Follow the instructions provided on the web page to finish the sample.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fc59-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7fc59-131">Next steps</span></span>
<span data-ttu-id="7fc59-132">Попробуйте следующий пример: [Анализ данных датчика с помощью Hive с HDInsight](hdinsight-hive-analyze-sensor-data.md).</span><span class="sxs-lookup"><span data-stu-id="7fc59-132">Try the following sample: [Analyzing sensor data using Hive with HDInsight](hdinsight-hive-analyze-sensor-data.md).</span></span>

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
