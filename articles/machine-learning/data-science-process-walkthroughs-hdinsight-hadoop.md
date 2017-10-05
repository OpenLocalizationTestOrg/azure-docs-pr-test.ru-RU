---
title: "Пошаговое руководство по обработке и анализу данных HDInsight Hadoop с использованием Hive в Azure | Документация Майкрософт"
description: "Примеры процесса обработки и анализа данных группы, которые объясняют, как использовать Hive в Azure HDInsight Hadoop для прогнозной аналитики."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: fb06c3c1b1ae30d970a2e4d45a49e22e9d78b876
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="hdinsight-hadoop-data-science-walkthroughs-using-hive-on-azure"></a>Пошаговое руководство по обработке и анализу данных HDInsight Hadoop с использованием Hive в Azure 

В этих пошаговых руководствах для прогнозной аналитики с кластером HDInsight Hadoop используется Hive. Они предусматривают выполнение инструкций, описанных в процессе обработки и анализа данных группы. Процесс обработки и анализа данных группы представлен в статье [Жизненный цикл процесса обработки и анализа данных группы](data-science-process-overview.md). Обзор Azure HDInsight см. в статье [Общие сведения об Azure HDInsight, технологической платформе Hadoop и кластерах Hadoop](../hdinsight/hdinsight-hadoop-introduction.md).

Дополнительные пошаговые инструкции по обработке и анализу данных группы объединены по используемой **платформе**: 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-hive-with-hdinsight-hadoop"></a>Прогнозирование чаевых за поездку в такси при помощи Hive с HDInsight Hadoop

В пошаговом руководстве [Процесс обработки и анализа данных группы на практике: использование кластеров Azure HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md) для прогнозирования используются данные такси Нью-Йорка: 

- Оставлены ли чаевые 
- Распределение сумм чаевых

Сценарий реализуется с помощью Hive и [кластера Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/). Вы узнаете, как хранить, изучать и проектировать признаки данных из общедоступного набора данных о поездках и тарифах в такси Нью-Йорка. Для сборки и развертывания моделей вы будет использовать машинное обучение Azure.

## <a name="predict-advertisement-clicks-using-hive-with-hdinsight-hadoop"></a>Прогнозирование переходов по рекламным объявлениям с помощью Hive с HDInsight Hadoop

В пошаговом руководстве [Процесс обработки и анализа данных группы на практике: использование кластера Azure HDInsight Hadoop с набором данных объемом 1 ТБ](machine-learning-data-science-process-hive-criteo-walkthrough.md) используется общедоступный набор данных переходов [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/), чтобы спрогнозировать, будут ли оставлены чаевые, и определить диапазон ожидаемых сумм. Сценарий реализуется с помощью Hive с [кластером Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) и используется для хранения, изучения, проектирования признаков и сокращения выборки данных. В сценарии применяется машинное обучение Azure для создания, обучения и оценки модели двоичной классификации, прогнозирующей, щелкнет ли пользователь рекламное объявление. В конце пошагового руководства показано, как опубликовать одну из этих моделей в качестве веб-службы.


## <a name="next-steps"></a>Дальнейшие действия

Описание ключевых компонентов, составляющих процесс обработки и анализа данных группы, см. в статье [Жизненный цикл процесса обработки и анализа данных группы](data-science-process-overview.md).

Описание жизненного цикла процесса обработки и анализа данных группы, который можно использовать для структурирования проектов по обработке и анализу данных, см. в статье [Жизненный цикл процесса обработки и анализа данных группы](data-science-process-lifecycle.md). Этот жизненный цикл представляет стандартные этапы выполнения проектов, от самого начала и до завершения. 

