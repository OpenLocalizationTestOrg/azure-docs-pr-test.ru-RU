---
title: "aaaAccess Hadoop YARN приложения программно - журналы Azure | Документы Microsoft"
description: "Программный доступ к журналам приложений в кластере Hadoop в HDInsight."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0198d6c9-7767-4682-bd34-42838cf48fc5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 064efee1ea6a864c29ab897692ead0152c926c0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-windows-based-hdinsight"></a>Доступ к журналам приложений YARN в HDInsight под управлением Windows
В этом разделе объясняется, как tooaccess hello журналов для приложений YARN (еще другого ресурса Согласователь), которые завершили в кластере под управлением Windows Hadoop в Azure HDInsight

> [!IMPORTANT]
> Hello сведения в этом документе применяются только на основе tooWindows кластеров HDInsight. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement). Сведения о доступе к журналам YARN в кластерах HDInsight под управлением Linux см. в статье [Доступ к журналам приложений YARN в HDInsight под управлением Linux](hdinsight-hadoop-access-yarn-app-logs-linux.md).
>


### <a name="prerequisites"></a>Предварительные требования
* Кластер HDInsight на платформе Windows См.  статью [Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="yarn-timeline-server"></a>Сервер временной шкалы YARN
Hello <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN временная шкала Server</a> содержит универсальные сведения о завершенных приложений также как приложение сведения о среде через две различные интерфейсы. В частности:

* Возможность хранения и извлечения общей информации о приложениях в кластерах HDInsight появилась, начиная с версии 3.1.1.374.
* компонент сведения специфические для платформы разработки приложения Hello hello Server временной шкалы недоступен в кластерах HDInsight.

Общие сведения о приложениях включает следующие виды данных hello.

* Идентификатор приложения Hello, уникальный идентификатор приложения
* Hello пользователя, запустившего приложение hello
* Сведения о попытках внесенные toocomplete приложения hello
* Hello контейнеры, используемые любые попытки конкретного приложения

На своими кластерами HDInsight эти сведения будут храниться в хранилище журнала tooa диспетчера ресурсов Azure в контейнер по умолчанию hello вашей учетной записи хранилища Azure по умолчанию. Эти общие данные о завершенных приложениях можно извлечь с помощью REST API:

    GET on https://<cluster-dns-name>.azurehdinsight.net/ws/v1/applicationhistory/apps


## <a name="yarn-applications-and-logs"></a>Приложения и журналы YARN
YARN поддерживает несколько моделей программирования (в том числе MapReduce), отделяя управление ресурсами от планирования и мониторинга приложений. Это осуществляется с помощью глобального диспетчера *ResourceManager*, *диспетчеров узлов*, на каждый рабочий узел и *диспетчеров приложений* на каждое приложение. Hello AM-приложения согласовывает ресурсы (ЦП, памяти, диска, сети) для запуска приложения с hello крепления. Hello RM работает с NMs toogrant эти ресурсы, которые предоставляются как *контейнеры*. Hello AM отвечает за отслеживание хода выполнения hello tooit контейнеров, назначенных hello по hello крепления. Приложение может требовать много контейнеров, в зависимости от характера приложения hello hello.

Кроме того, каждое приложение может состоять из нескольких *попыток, предпринимаемых приложением* в порядке toofinish в присутствии hello сбои или из-за потери связи между AM toohello и крепления. Таким образом контейнеры, предоставляются tooa конкретных попытки приложения. С точки зрения hello контекст для основной единицей работы, выполняемой в приложении YARN предоставляет контейнер, а все действия, которые выполняются в контексте hello контейнера выполняется на узле один рабочий hello, на какие hello контейнер был выделен. Дополнительные сведения см. в статье об [основных понятиях YARN][YARN-concepts].

При отладке приложений проблемный Hadoop важны журналы (журналы приложений и связанных hello контейнера). YARN предоставляет удобная платформа для сбора, статистической обработки и хранения журналов приложений с hello [статистической обработки журнала] [ log-aggregation] компонентов. Hello статистической обработки журнала позволяют доступ к журналы приложений более определенными собирает журналы для всех контейнеров на рабочий узел и сохраняет их как один агрегированных файл журнала на рабочий узел в файловой системе по умолчанию hello после завершения работы приложения. Ваше приложение может использовать сотен или тысяч контейнеров, но журналы для всех контейнеров на узле один рабочий всегда будет агрегированных tooa отдельных файлов, возникающие в один файл журнала на рабочий узел, используемую приложением. Статистической обработки журнала включено по умолчанию в кластерах HDInsight (версии 3.0 и более поздних версий), и статистические журналы можно найти в контейнер по умолчанию hello кластера на hello следующие расположения:

    wasb:///app-logs/<user>/logs/<applicationId>

В этом расположении *пользователя* — имя hello hello пользователя, запустившего приложение hello и *applicationId* — уникальный идентификатор приложения hello, назначенный крепления hello YARN.

Hello агрегированных журналы не читаются непосредственно, как они написаны [TFile][T-file], [двоичный формат] [ binary-format] проиндексирован контейнера. YARN предоставляет средства toodump CLI эти журналы как обычный текст для приложений или контейнеры, представляющие интерес. Можно просмотреть эти журналы как обычный текст, выполнив один из hello, следующие команды YARN непосредственно на узлах кластера hello (после tooit соединение с использованием протокола удаленного рабочего СТОЛА):

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>


## <a name="yarn-resourcemanager-ui"></a>Пользовательский интерфейс YARN ResourceManager
Здравствуйте пользовательского интерфейса диспетчера ресурсов YARN работает на головному узлу кластера hello и можно получить с помощью hello Azure панели мониторинга портала:

1. Войдите в слишком[портал Azure](https://portal.azure.com/).
2. Hello левого меню **Обзор**, нажмите кнопку **кластеров HDInsight**, щелкните кластер под управлением Windows, требуется tooaccess hello YARN журналы приложений.
3. Hello верхнего меню **мониторинга**. В новой вкладке браузера откроется страница **Консоль запросов HDInsight**.
4. В **консоли запросов HDInsight** щелкните **Yarn UI** (Пользовательский интерфейс Yarn).

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
