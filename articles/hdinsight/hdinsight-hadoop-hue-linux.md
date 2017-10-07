---
title: "aaaHue с Hadoop на основе HDInsight Linux кластерах - Azure | Документы Microsoft"
description: "Узнать, как кластеры оттенка tooinstall на HDInsight и использовании туннелирования tooHue запросы hello tooroute. Использовать хранилище toobrowse оттенка и запустите Hive или Pig."
keywords: hue hadoop
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 9e57fcca-e26c-479d-a745-7b80a9290447
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: f086cbad2a90cc6903fbfccbf4a6be44f8999d07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-hue-on-hdinsight-hadoop-clusters"></a>Установка и использование Hue на кластерах HDInsight Hadoop

Узнать, как кластеры оттенка tooinstall на HDInsight и использовании туннелирования tooHue запросы hello tooroute.

> [!IMPORTANT]
> Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="what-is-hue"></a>Что такое Hue
Цветовой тон представляет собой набор веб-приложений, используемых toointeract в кластере Hadoop. Можно использовать хранилище hello toobrowse цветового тона, связанные с кластера Hadoop (в случае hello кластеров HDInsight WASB), выполнять задания Hive и Pig сценарии и так далее. Hello следующие компоненты доступны для установки оттенка в кластере HDInsight Hadoop.

* редактор Beeswax Hive,
* Pig,
* диспетчер метахранилища,
* Oozie,
* FileBrowser (говорящий tooWASB контейнер по умолчанию)
* обозреватель заданий.

> [!WARNING]
> Компоненты, предоставляемые с кластером HDInsight hello полностью поддерживаются и поддержки Майкрософт способствуют tooisolate и разрешить проблемы toothese связанные компоненты.
>
> Пользовательские компоненты получают toohelp ограниченную техническую поддержку вы toofurther устранить проблему hello. Это может привести к устранению проблемы hello и без tooengage доступных каналов для hello открытии источника технологий, которых находится глубокие знания для данной технологии. Можно использовать ряд сайтов сообществ, например [форум MSDN по HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) или [http://stackoverflow.com](http://stackoverflow.com). Кроме того, для проектов Apache есть соответствующие сайты, например [Hadoop](http://hadoop.apache.org/) на сайте [http://apache.org](http://apache.org).
>
>

## <a name="install-hue-using-script-actions"></a>Установка Hue с помощью действий сценария

сценарий tooinstall Hello оттенка в кластере HDInsight под управлением Linux можно получить на https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. В кластерах с BLOB-объектов хранилища Azure (WASB) или хранилища Озера данных Azure можно использовать этот сценарий tooinstall оттенка хранения по умолчанию.

Этот раздел содержит инструкции о как toouse hello скрипта при подготовке кластера hello, с помощью портала Azure hello.

> [!NOTE]
> Действия сценариев используется tooapply также может быть Azure PowerShell, hello Azure CLI, hello HDInsight .NET SDK или шаблоны Azure Resource Manager. Можно также применить tooalready действия сценария работающие кластеры. Дополнительные сведения см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).
>
>

1. Запуск подготовки кластера с помощью действия hello в [HDInsight подготовки кластеров в Linux](hdinsight-hadoop-provision-linux-clusters.md), но не завершайте подготовки.

   > [!NOTE]
   > цветовой тон tooinstall на HDInsight кластеры, hello головному узлу рекомендуемый размер — по крайней мере A4 (8 ядер, 14 ГБ памяти).
   >
   >
2. На hello **необязательная конфигурация** колонке выберите **действия скрипта**и указать сведения для hello, как показано ниже:

    ![Предоставление параметров действий сценария для Hue](./media/hdinsight-hadoop-hue-linux/hue-script-action.png "Предоставление параметров действий сценария для Hue")

   * **ИМЯ**: Введите понятное имя для действия сценария hello.
   * **Универсальный код ресурса скрипта** — https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh;
   * **ГОЛОВНОЙ**: установите флажок.
   * **Рабочая роль** — оставьте это поле пустым;
   * **Zookeeper** — оставьте это поле пустым;
   * **Параметры** — оставьте это поле пустым.
3. Внизу hello hello **действия скрипта**, использовать hello **выберите** конфигурация hello toosave кнопок. Наконец, используйте hello **выберите** кнопку внизу hello hello **необязательная конфигурация** колонке toosave hello необязательная конфигурация сведения.
4. Продолжить подготовки кластера hello, как описано в [HDInsight подготовки кластеров в Linux](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="use-hue-with-hdinsight-clusters"></a>Использование Hue с кластерами HDInsight

Туннелирование SSH — hello единственным способом tooaccess оттенка hello кластере после его выполнения. Туннелирование через SSH позволяет toogo трафика hello напрямую головному узлу toohello hello кластера, где запущен цветовой тон. После завершения подготовки кластера hello используйте следующие шаги toouse оттенка в кластере HDInsight Linux hello.

> [!NOTE]
> Мы рекомендуем использовать Firefox веб браузера toofollow hello приведенным ниже инструкциям.
>
>

1. Используйте сведения hello в [пользовательского интерфейса, диспетчер ресурсов, JobHistory, NameNode, Oozie и других веб-интерфейса, веб-использование SSH туннелирование tooaccess Ambari](hdinsight-linux-ambari-ssh-tunnel.md) toocreate SSH туннелирования из кластера HDInsight toohello системы клиента, а затем настройте ваш веб браузера toouse hello туннеля SSH прокси-сервером.

2. После создания туннель SSH и настройки браузера tooproxy трафика через него следует найти имя узла hello hello основного головного узла. Это можно сделать, подключив toohello кластера с помощью SSH на порт 22. Например `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net` где **USERNAME** — имя пользователя SSH и **ИМЯ_КЛАСТЕРА** hello имя кластера.

    Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

3. После подключения используйте следующие команды hello tooobtain полное доменное имя первичного головному узлу hello hello:

        hostname -f

    Возвращает имя аналогичные toohello после:

        hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

    Это hello имя узла первичного hello головному узлу, где находится веб-сайт оттенка hello.
4. Используйте hello браузера tooopen hello оттенка портала в http://HOSTNAME:8888. Замените имя узла с именем hello, полученный на предыдущем шаге hello.

   > [!NOTE]
   > При входе для hello первый раз, появится запрос toocreate toolog учетную запись на портале оттенка toohello. учетные данные Hello, здесь будут ограниченные toohello портала и не связанные toohello администратором или учетные данные SSH, указанные во время подготовки кластера hello.
   >
   >

    ![Портал оттенка toohello входа в систему](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-login.png "укажите учетные данные для портала цветовой тон")

### <a name="run-a-hive-query"></a>Выполнение запроса Hive
1. Из портала оттенка hello, нажмите кнопку **редакторы запросов**и нажмите кнопку **Hive** редактор куста tooopen hello.

    ![Использование Hive](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-use-hive.png "Использование Hive")
2. На hello **Assist** в разделе **базы данных**, вы увидите **hivesampletable**. Это пример таблицы, входящей в состав всех кластеров Hadoop в HDInsight. Введите образец запроса в правой области hello и вывод hello hello **результатов** вкладки панели hello ниже, как показано в снимок экрана приветствия.

    ![Выполнение запросов Hive](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-hive-query.png "Выполнение запросов Hive")

    Можно также использовать hello **диаграммы** вкладке toosee визуальное представление результатов hello.

### <a name="browse-hello-cluster-storage"></a>Обзор хранилища кластера hello
1. Из портала оттенка hello, нажмите кнопку **браузер файла** в правом верхнем углу hello hello меню.
2. По умолчанию hello файл откроется в браузере на hello **/пользователя/myuser** каталога. Щелкните hello косой черты до каталога пользователей hello в корневом toohello toogo hello путь контейнера хранилища Azure hello, связанного с кластером hello.

    ![Использование браузера файлов](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-file-browser.png "Использование браузера файлов")
3. Щелкните правой кнопкой мыши файл или папку toosee hello доступных операций. Используйте hello **отправить** кнопку в hello правом углу tooupload файлы toohello текущий каталог. Используйте hello **New** кнопку toocreate новых файлов или каталогов.

> [!NOTE]
> Hello оттенка файл браузера может быть отображено только содержимое hello hello контейнера по умолчанию, связанного с кластером HDInsight hello. Любое дополнительное хранилище учетных записей и контейнеров, которые могут была связана с кластером hello станут недоступны с помощью браузера файл hello. Тем не менее связанные с кластером hello дополнительные контейнеры hello всегда будет доступен для задания Hive hello. Например, если ввести команду hello `dfs -ls wasb://newcontainer@mystore.blob.core.windows.net` в редактор куста hello, можно просмотреть дополнительные контейнеры, а также содержимое hello. В этой команде **newcontainer** не hello контейнер по умолчанию, связанное с кластером.
>
>

## <a name="important-considerations"></a>Важные сведения
1. Hello скрипту tooinstall оттенка устанавливает только на hello основной головному узлу кластера hello.

2. Во время установки для обновления конфигурации hello перезапускаются несколько служб Hadoop (HDFS, YARN, MR2, Oozie). По завершении установки оттенка hello сценария она может занять некоторое время для других toostart Hadoop службы. Это может повлиять на первоначальную производительность Hue. После запуска всех служб набор Hue полностью готов к работе.
3. Цветовой тон не понимает Tez заданий, являющееся hello текущего значения по умолчанию для куста. Toouse MapReduce как hello подсистема выполнения Hive, обновите hello сценария toouse hello следующую команду в сценарии:

        set hive.execution.engine=mr;

4. Кластеры Linux предоставляет сценарий, где вашей службы запущены на основной головному узлу hello пока hello диспетчер ресурсов может быть запущен hello получателей. Такой сценарий может привести к ошибкам, (см. ниже) при использовании цветовой тон tooview сведения о ВЫПОЛНЯЕМЫЕ задания в кластере hello. Тем не менее можно просмотреть сведения о задании hello при завершении задания hello.

   ![Ошибка портала Hue](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-error.png "Ошибка портала Hue")

   Причиной этого является tooa известная проблема. Чтобы избежать этого измените Ambari, hello active Resource Manager также выполняется на первичной головному узлу hello.
5. Hue понимает WebHDFS, а кластеры HDInsight используют службу хранилища Azure с приставкой `wasb://`в начале пути. Таким образом пользовательский сценарий hello, используемое в скрипт операции устанавливает WebWasb, — службой речь tooWASB WebHDFS совместимой. Да, несмотря на то, что портал оттенка hello говорит HDFS в местах (как при перемещении мыши над hello **браузер файлов**), он должен интерпретироваться как WASB.

## <a name="next-steps"></a>Дальнейшие действия
* [Установка Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install-linux.md). Используйте tooinstall настройки кластера кластеров Giraph на HDInsight Hadoop. Giraph позволяет graph tooperform обработка с использованием Hadoop и может использоваться с Azure HDInsight.
* [Установка Solr в кластерах HDInsight](hdinsight-hadoop-solr-install-linux.md). Используйте tooinstall настройки кластера кластеров Solr на HDInsight Hadoop. Solr позволяет выполнять операции поиска мощные tooperform хранимых данных.
* [Установка R в кластерах HDInsight](hdinsight-hadoop-r-scripts-linux.md). Используйте настройки кластера tooinstall R в кластерах HDInsight Hadoop. R — это открытый язык программирования и свободная программная среда для статистических вычислений. Он предоставляет сотни встраиваемых статистических функций и собственный язык программирования, который сочетает аспекты функционального и объектно-ориентированного программирования. Этот проект также обеспечивает обширные графические возможности.

[powershell-install-configure]: install-configure-powershell-linux.md
[hdinsight-provision]: hdinsight-provision-clusters-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
