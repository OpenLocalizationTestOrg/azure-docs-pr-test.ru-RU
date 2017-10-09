---
title: "aaaHDInsight Spark пошаговые руководства с использованием PySpark и Scala в Azure | Документы Microsoft"
description: "Примеры hello командного процесса обработки и анализа данных для изучения hello использование PySpark и Scala на toodo прогнозной аналитики Azure HDInsight Spark."
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
ms.openlocfilehash: f8b41a8cae414586570761ba4b4eb4c239cbb981
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hdinsight-spark-data-science-walkthroughs-using-pyspark-and-scala-on-azure"></a>Пошаговое руководство обработки и анализа данных HDInsight Spark с использованием PySpark и Scala в Azure

В этих пошаговых руководствах использовать PySpark и Scala в кластере Azure Spark toodo прогнозной аналитики. Они следуют hello действия, описанные в hello командного процесса обработки и анализа данных. Обзор hello командного процесса обработки и анализа данных см. в разделе [процесса обработки и анализа данных](data-science-process-overview.md). Обзор Spark в HDInsight см. в разделе [tooSpark введение в HDInsight](../hdinsight/hdinsight-apache-spark-overview.md).

Примеры обработки и анализа дополнительных данных, выполняемых hello командного процесса обработки и анализа данных будут сгруппированы по hello **платформы** используемой ими: 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]

## <a name="predict-taxi-tips-using-pyspark-on-azure-spark"></a>Прогнозирование чаевых за такси с помощью PySpark в Azure Spark

Hello [используйте Spark на Azure HDInsight](machine-learning-data-science-spark-overview.md) Пошаговое руководство использует данные из Нью-Йорк такси toopredict ли оплачивается совет и диапазон hello суммы требуется платная toobe. Она использует hello процесс обработки и анализа данных для команды в сценарий, используя [кластера Azure HDInsight Spark](https://azure.microsoft.com/services/hdinsight/) toostore, исследовать и компонент инженер данные из hello общедоступным NYC такси маршрута и успешного набора данных. В этом обзорном разделе устанавливает вы с кластером HDInsight Spark и hello Jupyter PySpark портативные компьютеры, используемые в остальной hello hello пошагового руководства. Эти записные показывается, как tooexplore данных и как затем toocreate и использования моделей. Расширенный просмотр данных и моделирование записной книжки показано как Hello tooinclude свертки перекрестной проверки, hyper параметр и вычисления моделей.

### <a name="data-exploration-and-modeling-with-spark"></a>Исследование и моделирование данных с помощью Spark 
Изучение набора данных hello и создать, оценки и оценивать hello моделей машинного обучения, прохождение hello [создать двоичных классификационных и регрессионных моделей данных с помощью набора средств для обеспечения Spark MLlib hello](machine-learning-data-science-spark-data-exploration-modeling.md) раздела.

### <a name="model-consumption"></a>Использование модели
toolearn создания классификационных и регрессионных моделей tooscore hello в этом разделе в статье [оценка и оценки моделей построен Spark машинного обучения](machine-learning-data-science-spark-model-consumption.md).

### <a name="cross-validation-and-hyperparameter-sweeping"></a>Перекрестная проверка и перебор гиперпараметров
Сведения об обучении моделей с помощью перекрестной проверки и перебора гиперпараметров см. в статье [Расширенное исследование и моделирование данных с помощью Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md).


## <a name="predict-taxi-tips-using-scala-on-azure-spark"></a>Прогнозирование чаевых за такси с помощью Scala в Azure Spark

Hello [Scala использования с Spark на Azure](machine-learning-data-science-process-scala-walkthrough.md) Пошаговое руководство использует данные из Нью-Йорк такси toopredict ли оплачивается совет и диапазон hello суммы требуется платная toobe. В нем показано, как toouse Scala для задач защищенных машинного обучения с hello Spark компьютера обучения (MLlib) и SparkML пакетов на кластере Azure HDInsight Spark. Он поможет выполнить задачи hello, составляющих hello [процесса обработки и анализа данных](http://aka.ms/datascienceprocess): приема данных и просмотра, визуализации, конструируются, моделирования и модели использования. Hello моделей, построенных включают логистической и линейной регрессии, случайные леса и градиента повышенных деревьев.


## <a name="next-steps"></a>Дальнейшие действия

Обсуждение hello ключевые компоненты, которые составляют hello командного процесса обработки и анализа данных см. в разделе [Обзор процесса обработки и анализа данных командного](data-science-process-overview.md).

Обсуждение hello жизненного цикла командного процесса обработки и анализа данных, которые можно использовать toostructure проектами обработки и анализа данных, в разделе [жизненного цикла командного процесса обработки и анализа данных](data-science-process-lifecycle.md). жизненный цикл Hello описаны шаги, hello, из начала toofinish, обычно выполняют проекты при их выполнении. 

