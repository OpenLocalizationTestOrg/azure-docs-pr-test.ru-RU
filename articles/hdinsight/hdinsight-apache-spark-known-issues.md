---
title: "кластер aaaTroubleshoot проблемы с Apache Spark в Azure HDInsight | Документы Microsoft"
description: "Узнайте о проблемах, связанных tooApache кластеров Spark в Azure HDInsight и как toowork вокруг их."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a>Известные проблемы в работе кластера Apache Spark в HDInsight

В этом документе хранит информацию о всех hello известные проблемы для общедоступной предварительной версии HDInsight Spark hello.  

## <a name="livy-leaks-interactive-session"></a>Утечка интерактивного сеанса Livy
При Livy перезапуске (из Ambari или из-за перезагрузки виртуальной машины tooheadnode 0) с помощью интерактивного сеанса жизнеспособность попасть задания интерактивного сеанса. По этой причине новые задания может находится в состоянии принято hello и не может быть запущена.

**Устранение.**

Используйте следующие процедуры tooworkaround hello проблема hello.

1. Подключитесь к головному узлу по протоколу SSH. См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Выполнения hello, следующая команда toofind hello приложения идентификаторы hello интерактивный заданий запущен через Livy. 
   
        yarn application –list
   
    Hello имена заданий по умолчанию будет Livy Если hello задания были запущены с Livy интерактивный сеанс с явные имена не указан, для hello Livy сеанса, запущенную книжке Jupyter, hello имя задания будет начинаться с remotesparkmagics_ *. 
3. Запустите следующие команды tookill hello этих заданий. 
   
        yarn application –kill <Application ID>

После этого новые задания начнут выполняться. 

## <a name="spark-history-server-not-started"></a>Сервер журналов Spark не запускается
Сервер журналов Spark не запускается автоматически после создания кластера.  

**Устранение.** 

Запустите hello журнала сервера Ambari вручную.

## <a name="permission-issue-in-spark-log-directory"></a>Проблема разрешений в каталоге журналов Spark
При hdiuser отправляет задание с spark-submit, возникает ошибка java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Отказано в доступе) и hello драйвер журнал не записывается. 

**Устранение.**

1. Добавьте группу Hadoop toohello hdiuser. 
2. После создания кластера предоставьте разрешения 777 для каталога /var/log/spark. 
3. Обновите расположение журнала spark hello, с помощью Ambari toobe каталог с 777 разрешениями.  
4. Выполните команду spark-submit как sudo.  

## <a name="spark-phoenix-connector-is-not-supported"></a>Соединитель Spark-Phoenix не поддерживается

В настоящее время hello Spark Финиксе соединитель не поддерживается с кластером HDInsight Spark.

**Устранение.**

Вместо этого необходимо использовать соединитель Spark HBase hello. Инструкции см. в разделе [как соединитель toouse Spark HBase](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).

## <a name="issues-related-toojupyter-notebooks"></a>Проблемы, связанные с tooJupyter ноутбуков
Ниже перечислены некоторые известные проблемы связанные tooJupyter ноутбуков.

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a>Записные книжки со знаками не из набора ASCII в именах файлов
Записные книжки Jupyter, которые могут использоваться в кластерах Spark HDInsight, не должны содержать в именах файлов знаки не из набора ASCII. При попытке tooupload в файл с помощью hello Jupyter пользовательского интерфейса, имеющая имя файла не ASCII, то возникнет ошибка без вмешательства пользователя (т. е Jupyter не позволит передать файл hello, но он не будет выдавать ошибку видимым либо). 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a>Ошибка при загрузке записных книжек большого размера
При загрузке записных книжек большого размера может возникнуть ошибка **`Error loading notebook`** .  

**Устранение.**

Появление этой ошибки не означает, что данные повреждены или утрачены.  Записных книжек, по-прежнему на диске в `/var/lib/jupyter`, и вы можете SSH в tooaccess кластера hello их. См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

После подключения toohello кластера с помощью SSH записных книжек можно скопировать из кластера tooyour локального компьютера (с помощью SCP или WinSCP) как потеря hello tooprevent резервной копии всех важных данных в записной книжке hello. Можно затем туннель SSH в к головному узлу на порт 8001 tooaccess Jupyter без прохода через шлюз hello.  Оттуда снимите вывода hello записной и повторно сохраните размер toominimize hello портативного компьютера.

tooprevent ошибки ситуации в hello в будущем, необходимо выполнить некоторые рекомендации:

* Это важные tookeep hello записной книжки размер небольшой. Любые выходные данные Spark заданиям, отправляется обратно tooJupyter, хранящихся в записной книжке hello.  Рекомендации по Jupyter он находится в общие tooavoid под управлением `.collect()` на больших RDD или блоки данных; вместо этого, если вы хотите toopeek RDD содержимого, рекомендуется запускать `.take()` или `.sample()` , где выходные данные не слишком велик.
* Кроме того при сохранении записной книжке, снимите все выходные размер hello tooreduce ячеек.

### <a name="notebook-initial-startup-takes-longer-than-expected"></a>Начальная загрузка записной книжки загружается дольше ожидаемого
Выполнение первой инструкции кода в записной книжке Jupyter с использованием волшебного слова Spark может занимать больше минуты.  

**Пояснение**

Это происходит потому, что при запуске первую ячейку кода hello. В фоновом режиме hello это инициирует конфигурации сеанса и Spark, SQL и контекстах Hive устанавливаются. После задания этих контекстов выполнения первой инструкции hello, и это дает hello впечатление, что инструкция hello заняло toocomplete много времени.

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a>Время ожидания записной книжки Jupyter в создании сеанса hello
Если недостаточно ресурсов для кластера Spark, hello Spark и Pyspark ядер в записной книжке Jupyter hello будет истекло время ожидания при toocreate hello сеанса. 

**Устранение** 

1. Освободите часть ресурсов в кластере Spark.
   
   * Остановка других записных книжек Spark переходом toohello закрыть и остановке меню или нажав кнопку завершения работы в обозревателе записной книжки hello.
   * Остановите другие приложения Spark из YARN.
2. Перезапустите hello ноутбук, который выполняется копирование toostart. Недостаточно ресурсов должны быть доступны для вас toocreate теперь сеанса.

## <a name="see-also"></a>См. также
* [Обзор: Apache Spark в Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Сценарии
* [Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики](hdinsight-apache-spark-use-bi-tools.md)
* [Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени](hdinsight-apache-spark-eventhub-streaming.md)
* [Анализ журнала веб-сайта с использованием Spark в HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Создание и запуск приложений
* [Создание автономного приложения с использованием Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Удаленный запуск заданий с помощью Livy в кластере Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Средства и расширения
* [Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala основных приложений](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Использование записных книжек Zeppelin с кластером Spark в HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Использование внешних пакетов с записными книжками Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Управление ресурсами
* [Управление ресурсами кластера hello Apache Spark в Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux](hdinsight-apache-spark-job-debugging.md)

