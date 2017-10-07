---
title: "aaaDebug Apache Spark задания, выполняющиеся на Azure HDInsight | Документы Microsoft"
description: "Используйте YARN пользовательского интерфейса, Spark пользовательского интерфейса и Spark журнал сервера tootrack и отладка задания на кластере Spark в Azure HDInsight"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 33d352a5773920735aa4e5e8532b78122f381377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a>Отладка заданий Apache Spark в Azure HDInsight

В этой статье вы узнаете, как tootrack и отладки Поместите здесь заданий, работающих в кластерах HDInsight с помощью hello YARN пользовательского интерфейса, Spark пользовательского интерфейса и hello Spark журнала сервера. В этой статье мы запустит задание Spark использование записной книжке доступен с кластера Spark hello, **машинное обучение: прогнозирующей аналитики на данные проверки пищевых продуктов с помощью MLLib**. Можно использовать следующие tootrack приложение, которое можно отправлять с помощью любого другого подхода, например, действия hello **spark-submit**.

## <a name="prerequisites"></a>Предварительные требования
Необходимо иметь следующие hello.

* Подписка Azure. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Кластер Apache Spark в HDInsight. Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).
* Вы должны начали работает hello,  **[машинное обучение: прогнозирующей аналитики на данные проверки пищевых продуктов с помощью MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**. Дополнительные сведения о toorun блокнота, выполните hello ссылку.  

## <a name="track-an-application-in-hello-yarn-ui"></a>Отслеживать приложение hello YARN пользовательского интерфейса
1. Запустите hello YARN пользовательского интерфейса. Из колонки hello кластера, нажмите кнопку **мониторинга кластера**, а затем нажмите кнопку **YARN**.
   
    ![Запуск пользовательского интерфейса YARN](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > Кроме того вы можете запустить hello YARN пользовательского интерфейса из hello Ambari пользовательского интерфейса. hello toolaunch Ambari пользовательского интерфейса, из колонки hello кластера, нажмите кнопку **мониторинга кластера**, а затем нажмите кнопку **мониторинга кластера HDInsight**. Hello Ambari пользовательского интерфейса, выберите **YARN**, нажмите кнопку **быстрые ссылки**, щелкните Диспетчер ресурсов active hello и нажмите кнопку **пользовательского интерфейса диспетчера ресурсов**.    
   > 
   > 
2. Так как вы начали hello Spark задания с помощью записные книжки Jupyter, приложение hello имеет имя hello **remotesparkmagics** (это имя hello для всех приложений, запускаемых из записных книжек hello). Дополнительные сведения о задании приветствия нажмите кнопку идентификатора приложения hello с tooget имя приложения hello. Откроется представление приложения hello.
   
    ![Поиск идентификатора приложения Spark](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    Для таких приложений, запускаемых из записные книжки Jupyter hello, всегда имеет состояние hello **под УПРАВЛЕНИЕМ** до выхода из записной книжки hello.
3. Из представления приложения hello можно выполнить детализацию дальнейшей toofind out hello контейнеров, связанных с приложение hello и журналы hello (stdout и stderr). Можно также запустить hello Spark пользовательского интерфейса, нажав кнопку hello связывания соответствующий toohello **URL-адрес отслеживания**, как показано ниже. 
   
    ![Скачивание журналов контейнера](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-hello-spark-ui"></a>Отслеживать приложение hello Spark пользовательского интерфейса
В hello Spark пользовательского интерфейса можно детализировать hello Spark заданий, порождаемых hello приложения, который был запущен ранее.

1. hello toolaunch Spark пользовательского интерфейса, из представления приложения hello, щелкните ссылку hello от hello **URL-адрес отслеживания**, как показано выше снимок экрана приветствия. Можно просмотреть все задания Spark hello, которые загружаются hello приложение, работающее в записной книжке Jupyter hello.
   
    ![Просмотр заданий Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. Нажмите кнопку hello **исполнителей** вкладке toosee обработки и хранения информации для каждого исполнителя. Стек вызовов hello также можно получить, щелкнув hello **потоков дампа** ссылку.
   
    ![Просмотр исполнителей Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. Нажмите кнопку hello **этапы** вкладке toosee этапы hello, связанных с приложением hello.
   
    ![Просмотр этапов Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    Каждый этап может включать несколько задач. Вы можете просмотреть для них статистику выполнения, как показано ниже.
   
    ![Просмотр этапов Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. На странице сведений о рабочей области hello вы можете запустить DAG визуализации. Разверните hello **визуализации DAG** ссылку вверху hello страницы приветствия, как показано ниже.
   
    ![Просмотр этапов Spark в формате визуализации DAG](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    DAG или прямой Aclyic граф представляет различные этапы hello в приложение hello. Каждый прямоугольник blue hello диаграмме представляет Spark операции, вызываемые из приложения hello.
5. На странице сведений о рабочей области hello также можно запустить просмотр временная шкала приложения hello. Разверните hello **временной шкалы событий** ссылку вверху hello страницы приветствия, как показано ниже.
   
    ![Представление временной шкалы для этапов Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    Этот монитор отображает события Spark hello в виде hello временной шкалы. представление временной шкалы Hello доступно три уровня для заданий в задании и в рабочей области. выше рисунке Hello захватывает hello представлении временной шкалы для данного этапа.
   
   > [!TIP]
   > При выборе hello **изменять масштаб** флажок, таблицу можно прокрутить влево и вправо в представлении временной шкалы hello.
   > 
   > 
6. Другие вкладки в hello Spark пользовательского интерфейса предоставляют полезные сведения об экземпляре Spark hello также.
   
   * Вкладка «хранилище» — Если приложение создает RDDs можно найти сведения о заданиях в вкладка hello хранилища.
   * Вкладка «среда» — на этой вкладке содержится много полезных сведений о данном экземпляре Spark, например hello 
     * версия Scala;
     * Каталог журнала событий, связанный с hello кластера
     * Число ядер исполнителя для приложения hello
     * и т. д.

## <a name="find-information-about-completed-jobs-using-hello-spark-history-server"></a>Найти сведения о выполненных заданиях с помощью hello Spark журнала сервера
После завершения задания hello сведения о задании hello сохраняются в hello Spark журнала сервера.

1. toolaunch hello Server журнал Spark, из колонки hello кластера, нажмите кнопку **мониторинга кластера**, а затем нажмите кнопку **Spark журнала сервера**.
   
    ![Запуск сервера журнала Spark](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > Кроме того вы можете запустить hello пользовательский Интерфейс сервера Spark журнала из hello Ambari пользовательского интерфейса. hello toolaunch Ambari пользовательского интерфейса, из колонки hello кластера, нажмите кнопку **мониторинга кластера**, а затем нажмите кнопку **мониторинга кластера HDInsight**. Hello Ambari пользовательского интерфейса, выберите **Spark**, нажмите кнопку **быстрые ссылки**и нажмите кнопку **пользовательский Интерфейс сервера журнал Spark**.
   > 
   > 
2. Вы увидите все перечисленные приложения hello завершена. Щелкните идентификатор приложения toodrill вниз в приложение Дополнительные сведения.
   
    ![Запуск сервера журнала Spark](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a>См. также
*  [Управление ресурсами кластера hello Apache Spark в Azure HDInsight](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a>Для специалистов по анализу данных

* [Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Анализ журнала веб-сайта с использованием Spark в HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Analyze Application Insights telemetry logs with Spark on HDInsight (Анализ журналов телеметрии Application Insights с помощью Spark в HDInsight)](hdinsight-spark-analyze-application-insight-logs.md)
* [Использование Caffe в кластере Azure HDInsight Spark для распределенного глубокого обучения](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a>Для разработчиков Spark

* [Создание автономного приложения с использованием Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Удаленный запуск заданий с помощью Livy в кластере Spark](hdinsight-apache-spark-livy-rest-interface.md)
* [Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala приложений](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени](hdinsight-apache-spark-eventhub-streaming.md)
* [Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Использование записных книжек Zeppelin с кластером Spark в HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Использование внешних пакетов с записными книжками Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


