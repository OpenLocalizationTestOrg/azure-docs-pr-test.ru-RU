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
# <a name="use-hive-with-windows-based-hdinsight-tooanalyze-logs-from-websites"></a>Используйте Hive с журналами tooanalyze HDInsight под управлением Windows с веб-сайтов
Узнайте, как toouse HiveQL с HDInsight tooanalyze журналы с веб-сайта. Анализ журнала веб-сайта можно использовать toosegment аудиторию, в зависимости от подобные действия, классификации посетителей, демографические данные и toofind содержимое hello просматриваемого, hello веб-сайтов, которые они появились и т. д.

> [!IMPORTANT]
> Hello шагов в этот документ корректно работать только с кластерами HDInsight под управлением Windows. Для версий ниже HDInsight 3.4 кластер HDInsight доступен только в Windows. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

В этом образце используется HDInsight кластера tooanalyze веб-сайта журнала файлы tooget понимание частоты hello с внешних веб-сайтов с веб-сайта toohello посещений в день. Можно также создать сводку ошибок веб-сайт hello пользователей. Вы научитесь:

* Подключите tooa хранилища больших двоичных объектов Azure, который содержит файлы журналов веб-сайта.
* Создание таблицы HIVE, tooquery эти журналы.
* Создание запросов HIVE tooanalyze hello данных.
* Используйте tooHDInsight tooconnect Microsoft Excel (с помощью открыть базу данных (ODBC) tooretrieve hello проанализировать данные подключения.

![HDI.Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a>Предварительные требования
* Вы должны были подготовить кластер Hadoop в Azure HDInsight. Инструкции см. в статье [Создание кластеров Hadoop под управлением Windows в HDInsight][hdinsight-provision].
* У вас должен быть установлен Microsoft Excel 2013 или Microsoft Excel 2010.
* Необходимо иметь [драйвер Microsoft ODBC Hive](http://www.microsoft.com/download/details.aspx?id=40886) tooimport данных из куста в Excel.

## <a name="toorun-hello-sample"></a>Образец hello toorun
1. Из hello [портала Azure](https://portal.azure.com/), из hello начальной панели (если существует кластера hello закрепленной), щелкните плитку hello кластера, на котором будет toorun образец hello.
2. Из hello кластера колонки, в разделе **быстрые ссылки**, нажмите кнопку **мониторинга кластера**, а затем из hello **мониторинга кластера** колонке нажмите кнопку **кластера HDInsight Панель мониторинга**. Кроме того вы можете напрямую открыть hello панели мониторинга с помощью hello URL-адреса:

         https://<clustername>.azurehdinsight.net

    В ответ на запрос проверки подлинности, используя имя пользователя администратора hello и пароль, используемый при подготовке кластера hello.
3. Hello открывшейся веб-странице, щелкните hello **Приступая к работе коллекции** вкладку и затем в разделе hello **решений с образцами данных** категории, щелкните hello **анализ журнала веб-сайт** Пример.
4. Следуйте инструкциям hello hello образец hello toofinish веб-страницы.

## <a name="next-steps"></a>Дальнейшие действия
Повторите следующие образец hello: [анализ данных датчика, с помощью Hive в HDInsight](hdinsight-hive-analyze-sensor-data.md).

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
