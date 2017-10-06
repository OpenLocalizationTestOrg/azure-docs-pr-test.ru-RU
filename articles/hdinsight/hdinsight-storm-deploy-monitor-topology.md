---
title: "aaaDeploy и управления ими Apache Storm топологии на HDInsight | Документы Microsoft"
description: "Узнайте, как toodeploy, мониторинг и управление ими с помощью панели мониторинга Storm hello в HDInsight топологии Apache Storm. Использование инструментов Hadoop для Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a>Развертывание топологий Apache Storm в HDInsight под управлением Windows и управление ими

Hello Storm панель мониторинга позволяет tooeasily развернуть и запустить кластер HDInsight tooyour Apache Storm топологии с помощью веб-браузере. Можно также использовать панель мониторинга toomonitor hello и управлять выполняющегося топологии. Если вы используете Visual Studio, hello средства HDInsight для Visual Studio предоставляет аналогичные функциональные возможности в Visual Studio.

Hello Storm панели мониторинга и функции hello ураган в hello средства HDInsight используют hello Storm REST API, который можно использовать toocreate своих собственных решениях, мониторинга и управления.

> [!IMPORTANT]
> Hello в данном пошаговом руководстве требуется ураган в кластере HDInsight, который использует Windows hello операционной системой. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Сведения о развертывании топологий Storm и управлении ими с помощью кластера HDInsight под управлением Linux см. в статье [Развертывание топологий Apache Storm в HDInsight под управлением Linux и управление ими](hdinsight-storm-deploy-monitor-topology-linux.md).

## <a name="prerequisites"></a>Предварительные требования

* **Apache Storm в HDInsight** — инструкции по созданию кластера представлены в статье [Начало работы с Apache Storm в HDInsight](hdinsight-apache-storm-tutorial-get-started.md).

* Для hello **Storm мониторинга**: современных веб-браузер, поддерживающий HTML5.

* Для **Visual Studio** -пакета Azure SDK 2.5.1 или более поздней версии и hello средства HDInsight для Visual Studio. В разделе [приступить к работе со средствами HDInsight для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall и настройте hello средства HDInsight для Visual Studio.

    Одно из следующих версий Visual Studio hello:

  * Visual Studio 2012 с обновлением 4;

  * Visual Studio 2013 с обновлением 4 или Visual Studio 2013 Community;

  * Visual Studio 2015 (любой выпуск);

  * Visual Studio 2017 (любой выпуск).

## <a name="storm-dashboard"></a>Панель мониторинга Storm

Hello Storm панели мониторинга — веб-страница, доступных в вашем кластере Storm. URL-адрес Hello **https://&lt;имя_кластера >.azurehdinsight.net/**, где **clustername** — имя вашего ураган в кластере HDInsight hello.

С помощью hello hello Storm панели мониторинга, выберите **отправить топологии**. Следуйте hello инструкции на странице приветствия toorun пример топологии или tooupload и запустите топологии, созданный вами.

![Топология страница отправки Hello][storm-dashboard-submit]

### <a name="storm-ui"></a>Пользовательский интерфейс Storm

Hello Storm панели мониторинга, выберите hello **Storm пользовательского интерфейса** ссылку. Отобразятся сведения о кластере hello в tooany сложения под управлением топологии.

![пользовательский интерфейс storm Hello][storm-dashboard-ui]

> [!NOTE]
> В некоторых версиях Internet Explorer может оказаться, что hello Storm пользовательского интерфейса не обновляется после его сначала посещения. Например не может отображаться новый топологии hello отправленные вами или топологии активным может отображаться при его предшествующей деактивации. Корпорация Майкрософт знает о наличии этой проблемы и работает над ее решением.

#### <a name="main-page"></a>Главная страница

Главная страница Hello hello Storm пользовательского интерфейса предоставляет hello следующую информацию:

* **Сводка кластера**: основные сведения о кластере Storm hello.

* **Topology summary**(Сводка по топологиям) — список запущенных топологий. Используйте ссылки hello в этот раздел tooview Дополнительные сведения о конкретных топологии.

* **Допуск сводки**: сведения о начальника Storm hello.

* **Конфигурация nimbus**: Nimbus конфигурации для кластера hello.

#### <a name="topology-summary"></a>Topology summary

При выборе ссылки из hello **топологии Сводка** разделе отображаются следующие сведения о топологии hello hello:

* **Сводка топологии**: основные сведения о топологии hello.

* **Топология действия**: операции управления, которые можно выполнять для топологии hello.

  * **Activate**(Включить) — возобновление обработки отключенной топологии.

  * **Deactivate**(Отключить) — приостановка выполняемой топологии.

  * **Перебалансировка**: корректирует параллелизм hello hello топологии. После изменения hello количество узлов в кластере hello следует производят повторную балансировку выполняющегося топологии. Это позволяет toocompensate hello топологии tooadjust параллелизма для hello увеличивается или уменьшается число узлов в кластере hello.

      Дополнительные сведения см. в разделе [основные сведения о параллелизма hello топологии Storm (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).

  * **KILL**: завершает топологии Storm после hello указано время ожидания.

* **Топология stats**: статистические данные о топологии hello. Используйте ссылки hello в hello **окна** столбца tooset hello временные рамки hello оставшихся записей на странице приветствия.

* **Spouts**: hello spouts используемой топологии hello. Используйте ссылки hello в этот раздел tooview Дополнительные сведения о конкретных spouts.

* **Болтов**: hello винты используемой топологии hello. Используйте ссылки hello в этот раздел tooview Дополнительные сведения о конкретных винты.

* **Конфигурация топологии**: hello конфигурации hello выбранной топологии.

#### <a name="spout-and-bolt-summary"></a>Сводка по воронкам и ситам

Выбрав spout hello **Spouts** или **болтов** разделы отображает hello следующую информацию о hello выбранного элемента:

* **Сводка компонентов**: основные сведения о hello spout или молнии.

* **Spout/молнии stats**: статистику hello spout или винта. Используйте ссылки hello в hello **окна** столбца tooset hello временные рамки hello оставшихся записей на странице приветствия.

* **Статистика ввода** (только винта): сведения о hello входные потоки, используемые hello молнии.

* **Выходные данные статистики**: сведения о потоках hello, генерируемой это spout или винта.

* **Исполнители**: сведения об экземплярах hello hello spout или молнии. Выберите hello **порт** запись для tooview определенного исполнителя, создается журнал диагностических сведений для данного экземпляра.

* **Errors**(Ошибки) — информация об ошибках для данной воронки или сита.

## <a name="hdinsight-tools-for-visual-studio"></a>Средства HDInsight для Visual Studio

Средства HDInsight Hello может быть используется toosubmit C# или гибридной топологии tooyour Storm кластера. следующие шаги Hello используйте образец приложения. Сведения о создании собственных топологий с помощью средства HDInsight hello см. в разделе [топологии разработки C# с помощью hello средства HDInsight для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Используйте следующие шаги toodeploy пример tooyour Storm в кластере HDInsight hello просматривать и управлять топологией hello.

1. Если вы уже установили hello последнюю версию hello средства HDInsight для Visual Studio, в разделе [приступить к работе со средствами HDInsight для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

2. Откройте Visual Studio b выберите **Файл** > **Создать** > **Проект**.

3. В hello **новый проект** диалогового окна разверните **установленные** > **шаблоны**, а затем выберите **HDInsight**. Выберите из списка шаблонов hello **Storm пример**. Внизу hello диалогового окна «hello» введите имя для приложения hello.

    ![изображение](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и выберите **отправить tooStorm на HDInsight**.

   > [!NOTE]
   > Если необходимо, введите учетные данные входа hello для подписки Azure. При наличии более чем одной подписке, войдите в toohello версией, которая содержит ваш ураган в кластере HDInsight.

5. Выберите ваш ураган в кластере HDInsight из hello **кластер Storm** раскрывающегося списка, а затем выберите **отправить**. Можно отслеживать факт отправки hello выполнена с помощью hello **вывода** окна.

6. При успешной отправки топологии hello hello **Storm топологии** для hello кластера должны отображаться. Выберите топологию hello hello список tooview сведения о hello под управлением топологии.

    ![мониторинг Visual Studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > Можно также просмотреть **топологии Storm** в **обозревателе серверов**. Для этого разверните **Azure** > **HDInsight**, затем щелкните правой кнопкой мыши топологию Storm в кластере HDInsight и выберите **Просмотреть топологии Storm**.

    Выберите фигуру hello для hello spouts или болтов tooview сведения об этих компонентах. Для каждого выбранного элемента открывается новое окно.

   > [!NOTE]
   > Имя Hello hello топологии — имя класса hello hello топологии (в этом случае `HelloWord`,) с меткой времени добавляется.

7. Из hello **топологии Сводка** представление, выберите **Kill** toostop hello топологии.

   > [!NOTE]
   > Топологии storm продолжения, пока они не будут остановлены или hello кластер удаляется.


## <a name="rest-api"></a>Интерфейс REST API

Hello пользовательского интерфейса Storm построено на основе hello REST API, чтобы выполнить аналогичные отслеживание и управление ими функциональные возможности с помощью API-интерфейса REST hello. Hello API-интерфейса REST toocreate пользовательские средства можно использовать для управления и мониторинга Storm топологии.

Дополнительные сведения см. в разделе [API-интерфейс REST пользовательского интерфейса Storm](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md). Hello следующие сведения являются hello конкретных toousing API REST с Apache Storm на HDInsight.

### <a name="base-uri"></a>Базовый универсальный код ресурса

базовый URI для hello REST API в кластерах HDInsight Hello **https://&lt;имя_кластера >.azurehdinsight.net/stormui/api/v1/**, где **clustername** — имя вашего Storm hello на Кластер HDInsight.

### <a name="authentication"></a>Аутентификация

Toohello запросы, необходимо использовать API-Интерфейс REST **обычной проверки подлинности**, поэтому использовать hello HDInsight кластер имя и пароль администратора.

> [!NOTE]
> Поскольку обычная проверка подлинности передается с помощью открытого текста, следует **всегда** использовать кластере hello toosecure подключений по протоколу HTTPS.

### <a name="return-values"></a>Возвращаемые значения

Сведения, возвращаемые из hello API-интерфейса REST только может быть одновременно доступен из кода внутри кластера hello или виртуальных машин на hello одной виртуальной сети Azure как кластер hello. Например hello полное доменное имя (FQDN), возвращаемое для Zookeeper серверы являются недоступна из Интернета hello.

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы узнали, как монитор и toodeploy топологии с помощью hello Storm панели мониторинга, узнайте, как:

* [Разработка топологии C# с помощью hello средства HDInsight для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [Разработка топологий на платформе Java с помощью Maven](hdinsight-storm-develop-java-topology.md)

Другие примеры топологий Storm см. в разделе [Примеры топологий для Storm в HDInsight](hdinsight-storm-example-topology.md).

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
