---
title: "с помощью Hive и Hadoop - Azure HDInsight aaaAnalyze датчиков | Документы Microsoft"
description: "Узнайте, как tooanalyze данных датчика с помощью hello Hive консоль запросов с HDInsight (Hadoop), а затем отобразить данные hello в Microsoft Excel с помощью PowerView."
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
ms.openlocfilehash: 70e595705c33d9835dc9809161f79c3ac5ece870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-using-hello-hive-query-console-on-hadoop-in-hdinsight"></a><span data-ttu-id="225b7-103">Анализ данных датчика с помощью hello Hive консоль запросов в Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="225b7-103">Analyze sensor data using hello Hive Query Console on Hadoop in HDInsight</span></span>

<span data-ttu-id="225b7-104">Узнайте, как tooanalyze данных датчика с помощью hello Hive консоль запросов с HDInsight (Hadoop), а затем отобразить данные hello в Microsoft Excel при помощи Power View.</span><span class="sxs-lookup"><span data-stu-id="225b7-104">Learn how tooanalyze sensor data by using hello Hive Query Console with HDInsight (Hadoop), then visualize hello data in Microsoft Excel by using Power View.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="225b7-105">Hello шагов в этот документ корректно работать только с кластерами HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="225b7-105">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="225b7-106">Для версий ниже HDInsight 3.4 кластер HDInsight доступен только в Windows.</span><span class="sxs-lookup"><span data-stu-id="225b7-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="225b7-107">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="225b7-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="225b7-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="225b7-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


<span data-ttu-id="225b7-109">В этом образце используется куст tooprocess исторических данных и выявления проблем с системами отопления и кондиционирования.</span><span class="sxs-lookup"><span data-stu-id="225b7-109">In this sample, you use Hive tooprocess historical data and identify problems with heating and air conditioning systems.</span></span> <span data-ttu-id="225b7-110">В частности, позволяющий определять системы не удается tooreliably Ведение температуры набора, выполняя следующие задачи hello:</span><span class="sxs-lookup"><span data-stu-id="225b7-110">Specifically, you identify systems are not able tooreliably maintain a set temperature by performing hello following tasks:</span></span>

* <span data-ttu-id="225b7-111">Создание HIVE таблиц tooquery данные, хранящиеся в файлах с разделителями-запятыми (CSV).</span><span class="sxs-lookup"><span data-stu-id="225b7-111">Create HIVE tables tooquery data stored in comma-separated value (CSV) files.</span></span>
* <span data-ttu-id="225b7-112">Создание запросов HIVE tooanalyze hello данных.</span><span class="sxs-lookup"><span data-stu-id="225b7-112">Create HIVE queries tooanalyze hello data.</span></span>
* <span data-ttu-id="225b7-113">tooretrieve hello анализа данных, используйте tooHDInsight tooconnect Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="225b7-113">tooretrieve hello analyzed data, use Microsoft Excel tooconnect tooHDInsight.</span></span>
* <span data-ttu-id="225b7-114">toovisualize hello данных, используйте Power View.</span><span class="sxs-lookup"><span data-stu-id="225b7-114">toovisualize hello data, use Power View.</span></span>

![Схема архитектуры решения hello](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a><span data-ttu-id="225b7-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="225b7-116">Prerequisites</span></span>

* <span data-ttu-id="225b7-117">Кластер HDInsight (Hadoop). Сведения о создании кластера см. в статье о [создании кластеров Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="225b7-117">An HDInsight (Hadoop) cluster: See [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster.</span></span>
* <span data-ttu-id="225b7-118">Microsoft Excel 2013</span><span class="sxs-lookup"><span data-stu-id="225b7-118">Microsoft Excel 2013</span></span>

  > [!NOTE]
  > <span data-ttu-id="225b7-119">Microsoft Excel используется для визуализации данных с помощью [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="225b7-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span></span>

* [<span data-ttu-id="225b7-120">Драйвер Microsoft Hive ODBC.</span><span class="sxs-lookup"><span data-stu-id="225b7-120">Microsoft Hive ODBC Driver</span></span>](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="toorun-hello-sample"></a><span data-ttu-id="225b7-121">Образец hello toorun</span><span class="sxs-lookup"><span data-stu-id="225b7-121">toorun hello sample</span></span>

1. <span data-ttu-id="225b7-122">В веб-браузере перейдите toohello URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="225b7-122">From your web browser, navigate toohello following URL:</span></span> 

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="225b7-123">Замените `<clustername>` с hello имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="225b7-123">Replace `<clustername>` with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="225b7-124">В ответ на запрос проверки подлинности, используя имя пользователя администратора hello и пароль, используемый при подготовке этого кластера.</span><span class="sxs-lookup"><span data-stu-id="225b7-124">When prompted, authenticate by using hello administrator user name and password you used when provisioning this cluster.</span></span>

2. <span data-ttu-id="225b7-125">Hello открывшейся веб-странице, щелкните hello **Приступая к работе коллекции** вкладку и затем в разделе hello **решений с образцами данных** категории, щелкните hello **анализ данных датчика** Пример.</span><span class="sxs-lookup"><span data-stu-id="225b7-125">From hello web page that opens, click hello **Getting Started Gallery** tab, and then under hello **Solutions with Sample Data** category, click hello **Sensor Data Analysis** sample.</span></span>

    ![Рисунок коллекции для начала работы](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. <span data-ttu-id="225b7-127">Следуйте инструкциям hello hello образец hello toofinish веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="225b7-127">Follow hello instructions provided on hello web page toofinish hello sample.</span></span>
