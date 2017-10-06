---
title: "Регистрирует aaaAccess Hadoop YARN приложения на основе Linux HDInsight — Azure | Документы Microsoft"
description: "Узнайте, каким образом приложения YARN tooaccess ведет журнал на кластере под управлением Linux HDInsight (Hadoop), с помощью командной строки hello и веб-браузер."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 3ec08d20-4f19-4a8e-ac86-639c04d2f12e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0bab356e3b97114abbb05712c8e7b21a194f2508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-linux-based-hdinsight"></a>Доступ к журналам приложений YARN в HDInsight под управлением Linux

Узнайте, как tooaccess hello в журналах приложений YARN (еще другого ресурса Согласователь) в кластере Hadoop в Azure HDInsight.

> [!IMPORTANT]
> Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Что представляют собой различные компоненты и версии Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md#hdinsight-windows-retirement)

## <a name="YARNTimelineServer"></a>YARN Timeline Server

Hello [YARN временная шкала Server](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html) предоставляет сведения общего характера о завершенных приложений и сведений специфические для платформы разработки приложений с помощью двух различных интерфейсов. В частности:

* Возможность хранения и извлечения общей информации о приложениях в кластерах HDInsight появилась, начиная с версии 3.1.1.374.
* компонент сведения специфические для платформы разработки приложения Hello hello Server временной шкалы недоступен в кластерах HDInsight.

Общие сведения о приложениях включает hello следующий тип данных:

* Идентификатор приложения Hello, уникальный идентификатор приложения
* Hello пользователя, запустившего приложение hello
* Сведения о попытках внесенные toocomplete приложения hello
* Hello контейнеры, используемые любые попытки конкретного приложения

## <a name="YARNAppsAndLogs"></a>Приложения и журналы YARN

YARN поддерживает несколько моделей программирования (в том числе MapReduce), отделяя управление ресурсами от планирования и мониторинга приложений. YARN использует глобальный диспетчер *ResourceManager*, *диспетчеры узлов* на каждый рабочий узел и *диспетчеры приложений* на каждое приложение. Hello AM-приложения согласовывает ресурсы (ЦП, памяти, диска, сети) для запуска приложения с hello крепления. Hello RM работает с NMs toogrant эти ресурсы, которые предоставляются как *контейнеры*. Hello AM отвечает за отслеживание хода выполнения hello tooit контейнеров, назначенных hello по hello крепления. Приложение может требовать много контейнеров, в зависимости от характера приложения hello hello.

Для выполнения приложения может потребоваться несколько *попыток*. Если выполнение приложения завершается ошибкой, его можно повторить как новую попытку. Каждая попытка выполняется в контейнере. С точки зрения контейнер предоставляет контекст hello для основной единицей работы, выполняемой в приложении YARN. Все действия, которые выполняются в контексте hello контейнера выполняется на узле один рабочий hello, на какие hello контейнер был выделен. Дополнительные сведения см. в статье об [основных понятиях YARN][YARN-concepts].

При отладке приложений проблемный Hadoop важны журналы (журналы приложений и связанных hello контейнера). YARN предоставляет удобная платформа для сбора, статистической обработки и хранения журналов приложений с hello [статистической обработки журнала] [ log-aggregation] компонентов. более определенными доступ к журналы приложений благодаря Hello журнала статистической функции. так как она объединяет журналы со всех контейнеров на рабочем узле и хранит их как один сводный файл журнала на рабочем узле Hello журнала хранится в файловой системе по умолчанию hello, после завершения работы приложения. Приложение может использовать сотен или тысяч контейнеров, но журналы для всех контейнеров на узле один рабочий всегда являются агрегированных tooa одного файла. Поэтому на каждый рабочий узел, используемый приложением, приходится один файл журнала. Объединение журналов включено по умолчанию на кластерах HDInsight версии 3.0 и более поздних версий. Статистические журналы расположены в хранилище по умолчанию для кластера hello. Hello пути — hello HDFS путь toohello журналы:

    /app-logs/<user>/logs/<applicationId>

В пути hello `user` — имя hello hello пользователя, запустившего приложение hello. Hello `applicationId` hello уникальный идентификатор, назначенный tooan по представляет приложение крепления hello YARN.

Hello агрегированных журналы не читаются непосредственно, как они написаны [TFile][T-file], [двоичный формат] [ binary-format] проиндексирован контейнера. Используйте журналы YARN ResourceManager hello или tooview средства CLI эти журналы как обычный текст для приложений или контейнеры, представляющие интерес.

## <a name="yarn-cli-tools"></a>Средства CLI для YARN

средства интерфейса командной строки YARN hello toouse, необходимо сначала подключиться toohello кластера HDInsight, с помощью SSH. См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Можно просмотреть эти журналы как обычный текст, выполнив один из hello, следующие команды:

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>

Укажите hello &lt;applicationId >, &lt;пользователя, работы приложения >, &lt;containerId >, и &lt;рабочий адрес узла > сведения при выполнении этих команд.

## <a name="yarn-resourcemanager-ui"></a>Пользовательский интерфейс YARN ResourceManager

пользовательский Интерфейс диспетчера ресурсов YARN Hello выполняется на головному узлу кластера hello. Она осуществляется с помощью Ambari web hello пользовательского интерфейса. Регистрирует hello используйте следующие шаги tooview hello YARN:

1. В веб-браузере перейдите toohttps://CLUSTERNAME.azurehdinsight.net. Замените ИМЯ_КЛАСТЕРА hello имя кластера HDInsight.
2. Выберите из списка служб слева hello hello **YARN**.

    ![Выбранные службы Yarn](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnservice.png)
3. Из hello **быстрые ссылки** раскрывающийся список, выберите один из головного узла кластера hello, а затем выберите **ResourceManager журнала**.

    ![Быстрые ссылки для Yarn](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnquicklinks.png)

    Появится список журналов tooYARN ссылки.

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
