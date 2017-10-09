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
# <a name="analyze-sensor-data-using-hello-hive-query-console-on-hadoop-in-hdinsight"></a>Анализ данных датчика с помощью hello Hive консоль запросов в Hadoop в HDInsight

Узнайте, как tooanalyze данных датчика с помощью hello Hive консоль запросов с HDInsight (Hadoop), а затем отобразить данные hello в Microsoft Excel при помощи Power View.

> [!IMPORTANT]
> Hello шагов в этот документ корректно работать только с кластерами HDInsight под управлением Windows. Для версий ниже HDInsight 3.4 кластер HDInsight доступен только в Windows. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).


В этом образце используется куст tooprocess исторических данных и выявления проблем с системами отопления и кондиционирования. В частности, позволяющий определять системы не удается tooreliably Ведение температуры набора, выполняя следующие задачи hello:

* Создание HIVE таблиц tooquery данные, хранящиеся в файлах с разделителями-запятыми (CSV).
* Создание запросов HIVE tooanalyze hello данных.
* tooretrieve hello анализа данных, используйте tooHDInsight tooconnect Microsoft Excel.
* toovisualize hello данных, используйте Power View.

![Схема архитектуры решения hello](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a>Предварительные требования

* Кластер HDInsight (Hadoop). Сведения о создании кластера см. в статье о [создании кластеров Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
* Microsoft Excel 2013

  > [!NOTE]
  > Microsoft Excel используется для визуализации данных с помощью [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).

* [Драйвер Microsoft Hive ODBC.](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="toorun-hello-sample"></a>Образец hello toorun

1. В веб-браузере перейдите toohello URL-адреса: 

         https://<clustername>.azurehdinsight.net

    Замените `<clustername>` с hello имя кластера HDInsight.

    В ответ на запрос проверки подлинности, используя имя пользователя администратора hello и пароль, используемый при подготовке этого кластера.

2. Hello открывшейся веб-странице, щелкните hello **Приступая к работе коллекции** вкладку и затем в разделе hello **решений с образцами данных** категории, щелкните hello **анализ данных датчика** Пример.

    ![Рисунок коллекции для начала работы](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. Следуйте инструкциям hello hello образец hello toofinish веб-страницы.
