---
title: "Анализ данных датчиков с помощью Hive и Hadoop. Azure HDInsight | Документация Майкрософт"
description: "Узнайте, как анализировать данные датчика с помощью консоли запросов Hive с HDInsight (Hadoop), а затем наглядно представлять данные в Microsoft Excel с помощью Power View."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: a8ac160c-1cef-45d9-bf36-7beb5a439105
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 3abb71c12b4769bebd808276f8bdd832aad22d7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-sensor-data-using-the-hive-query-console-on-hadoop-in-hdinsight"></a><span data-ttu-id="c0cd7-103">Анализ данных датчика с помощью консоли запросов Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="c0cd7-103">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span></span>

<span data-ttu-id="c0cd7-104">Узнайте, как анализировать данные датчика с помощью консоли запросов Hive с HDInsight (Hadoop), а затем наглядно представлять данные в Microsoft Excel с помощью Power View.</span><span class="sxs-lookup"><span data-stu-id="c0cd7-104">Learn how to analyze sensor data by using the Hive Query Console with HDInsight (Hadoop), then visualize the data in Microsoft Excel by using Power View.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0cd7-105">Шаги, описанные в этом документе, можно применять только к кластерам HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="c0cd7-105">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="c0cd7-106">Для версий ниже HDInsight 3.4 кластер HDInsight доступен только в Windows.</span><span class="sxs-lookup"><span data-stu-id="c0cd7-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="c0cd7-107">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="c0cd7-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c0cd7-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c0cd7-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


<span data-ttu-id="c0cd7-109">В этом примере используется Hive для обработки исторических данных и выявления проблем с системами отопления и кондиционирования воздуха.</span><span class="sxs-lookup"><span data-stu-id="c0cd7-109">In this sample, you use Hive to process historical data and identify problems with heating and air conditioning systems.</span></span> <span data-ttu-id="c0cd7-110">В частности, выявляются системы, неспособные надежно поддерживать заданную температуру. Для этого вы будете:</span><span class="sxs-lookup"><span data-stu-id="c0cd7-110">Specifically, you identify systems are not able to reliably maintain a set temperature by performing the following tasks:</span></span>

* <span data-ttu-id="c0cd7-111">создавать таблицы HIVE для формирования запросов к данным, хранящимся в файлах значений, разделенных запятыми (CSV-файлах);</span><span class="sxs-lookup"><span data-stu-id="c0cd7-111">Create HIVE tables to query data stored in comma-separated value (CSV) files.</span></span>
* <span data-ttu-id="c0cd7-112">создавать запросы HIVE для анализа данных;</span><span class="sxs-lookup"><span data-stu-id="c0cd7-112">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="c0cd7-113">использовать Microsoft Excel для подключения к HDInsight, чтобы извлекать проанализированные данные;</span><span class="sxs-lookup"><span data-stu-id="c0cd7-113">To retrieve the analyzed data, use Microsoft Excel to connect to HDInsight.</span></span>
* <span data-ttu-id="c0cd7-114">использовать Power View для визуализации данных.</span><span class="sxs-lookup"><span data-stu-id="c0cd7-114">To visualize the data, use Power View.</span></span>

![Схема архитектуры решения](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a><span data-ttu-id="c0cd7-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c0cd7-116">Prerequisites</span></span>

* <span data-ttu-id="c0cd7-117">Кластер HDInsight (Hadoop). Сведения о создании кластера см. в статье о [создании кластеров Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="c0cd7-117">An HDInsight (Hadoop) cluster: See [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster.</span></span>
* <span data-ttu-id="c0cd7-118">Microsoft Excel 2013</span><span class="sxs-lookup"><span data-stu-id="c0cd7-118">Microsoft Excel 2013</span></span>

  > [!NOTE]
  > <span data-ttu-id="c0cd7-119">Microsoft Excel используется для визуализации данных с помощью [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="c0cd7-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span></span>

* [<span data-ttu-id="c0cd7-120">Драйвер Microsoft Hive ODBC.</span><span class="sxs-lookup"><span data-stu-id="c0cd7-120">Microsoft Hive ODBC Driver</span></span>](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="to-run-the-sample"></a><span data-ttu-id="c0cd7-121">Запуск образца</span><span class="sxs-lookup"><span data-stu-id="c0cd7-121">To run the sample</span></span>

1. <span data-ttu-id="c0cd7-122">Откройте веб-браузер и перейдите по следующему URL-адресу:</span><span class="sxs-lookup"><span data-stu-id="c0cd7-122">From your web browser, navigate to the following URL:</span></span> 

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="c0cd7-123">Замените `<clustername>` на имя вашего кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c0cd7-123">Replace `<clustername>` with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="c0cd7-124">В ответ на запрос выполните аутентификацию с помощью имени пользователя и пароля администратора, использованных при подготовке данного кластера.</span><span class="sxs-lookup"><span data-stu-id="c0cd7-124">When prompted, authenticate by using the administrator user name and password you used when provisioning this cluster.</span></span>

2. <span data-ttu-id="c0cd7-125">На открывшейся веб-странице выберите вкладку **Getting Started Gallery** (Коллекция для начала работы), а затем в категории **Solutions with Sample Data** (Решения с примером данных) щелкните пример **Анализ данных датчиков**.</span><span class="sxs-lookup"><span data-stu-id="c0cd7-125">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Sensor Data Analysis** sample.</span></span>

    ![Рисунок коллекции для начала работы](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. <span data-ttu-id="c0cd7-127">Следуйте инструкциям, представленным на веб-странице, чтобы закончить образец.</span><span class="sxs-lookup"><span data-stu-id="c0cd7-127">Follow the instructions provided on the web page to finish the sample.</span></span>
