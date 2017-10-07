---
title: "события aaaCorrelate со временем с Storm и HBase на HDInsight"
description: "Узнайте, как toocorrelate события, поступающие в разное время с помощью Storm и HBase на HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 17d11479-2d02-4790-8d29-05fb38351479
ms.service: hdinsight
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: f915eef77bbda5b02bfd02ad0b5a4923ff2f4f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a>Сопоставление событий, поступающих в разное время, с помощью Storm и HBase

Благодаря сохранению постоянных данных в Apache Storm можно сопоставлять данные, поступающие в разное время. Например связывание события входа и выхода для toocalculate сеанса пользователя как долго сеанс hello выполнялись.

В этом документе вы узнаете, как toocreate базовая топология Storm C#, отслеживает события входа и выхода для сеансов пользователей, а затем вычисляет hello продолжительность сеанса hello. Топология Hello HBase использует в качестве хранилища постоянных данных. HBase также позволяет tooperform пакетные запросы на hello исторические данные tooproduce дополнительные функции анализа. Например, количество пользовательских сеансов, начатых или завершенных за определенный период времени.

## <a name="prerequisites"></a>Предварительные требования

* Visual Studio и hello HDInsight tools для Visual Studio. Дополнительные сведения см. в разделе [приступить к работе со средствами hello HDInsight для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

* Apache Storm в кластере HDInsight (под управлением Windows).

  > [!WARNING]
  > Выполняемая SCP.NET топологии в кластерах Storm под управлением Linux, созданных после 10/28/2016 hello HBase пакета SDK для .NET пакет, доступный на 10/28/2016 г. не работает на основе Linux HDInsight

* Apache HBase в кластере HDInsight (под управлением Linux или Windows).

  > [!IMPORTANT]
  > Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [Java](https://java.com) 1.7 или более поздняя версия в среде разработки. Java — используется toopackage hello топологии при отправленной toohello кластера HDInsight.

  * Hello **JAVA_HOME** среды переменной должен точки toohello каталог, содержащий Java.
  * Hello **%JAVA_HOME%/bin** каталог должен находиться в пути hello

## <a name="architecture"></a>Архитектура

![Схема потока данных hello через hello топологии](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

Сопоставление событий требуется идентификатор для источника события hello. Например идентификатор пользователя, идентификатор сеанса или другой частью данных это) уникальный и б) в включаются все данные, отправляемые tooStorm. В этом примере используется значение GUID toorepresent идентификатор сеанса.

В примере есть два кластера HDInsight:

* HBase: хранилище постоянных данных для исторических данных;
* Storm: использовать tooingest входящих данных

Hello данных формируется случайным образом топологии Storm hello и состоит из следующих элементов hello:

* идентификатор сеанса: GUID, который однозначно определяет каждый сеанс;
* событие: событие НАЧАЛО или КОНЕЦ, в этом примере НАЧАЛО всегда раньше КОНЦА;
* Время: hello время события hello.

Эти данные обрабатываются и хранятся в HBase.

### <a name="storm-topology"></a>Топология Storm

При запуске сеанса, **ЗАПУСК** событие полученных топологии hello и tooHBase в журнал. При **окончания** полученных событий, топологии hello извлекает hello **ЗАПУСК** событие и вычисляет hello времени между событиями hello двух. Это **длительность** значение сохраняется в HBase вместе с hello **окончания** сведения о событии.

> [!IMPORTANT]
> Во время этой топологии демонстрирует базовый шаблон hello, решение производственного понадобится tootake конструктора для hello следующие сценарии:
>
> * события, поступающие не по порядку;
> * повторяющиеся события;
> * удаленные события.

Пример топологии Hello состоит из hello следующие компоненты:

* Session.cs: имитирует сеанса пользователя путем создания идентификатора сеанса произвольного, время сеанса hello время и сколько времени начала.

* Spout.cs: создает 100 сеансов, создает событие НАЧАЛА, ожидает hello случайное время ожидания для каждого сеанса и затем создает событие END. Затем перезапускает завершения сеансов toogenerate новые.

* HBaseLookupBolt.cs: использует toolook идентификатор сеанса hello информации сеанса в HBase. При обработке события окончания обнаруживает соответствующее событие НАЧАЛА hello и вычисляет hello продолжительность сеанса hello.

* HBaseBolt.cs: сохранение информации в HBase.

* TypeHelper.cs: Помогает преобразования типа при чтении или записи tooHBase.

### <a name="hbase-schema"></a>Схема HBase

В HBase hello данные хранятся в таблице с hello следующие схемы и параметры:

* Ключ строки: hello сеанса идентификатор используется как hello ключ для строк в этой таблице.

* Семейство столбца: hello имя семейства — «cf». В этом семействе хранятся столбцы:

  * событие: НАЧАЛО или КОНЕЦ;

  * время: hello время в миллисекундах, которое hello событие произошло.

  * длительность: hello расстояние от НАЧАЛА и окончания событий.

* ВЕРСИИ: семейства «cf» hello, задается tooretain 5 версии каждой строки.

  > [!NOTE]
  > Версии представляют собой запись предыдущих значений, сохраненных для конкретного ключа строки. По умолчанию HBase возвращает только значение hello hello самой последней версии строки. В этом случае hello одной строки используется для всех событий (начало, конец.) в каждой версии строки определяется hello значение отметки времени. Версии предоставляют обзор прошлых событий, зарегистрированных для определенного идентификатора.

## <a name="download-hello-project"></a>Загрузите проект hello

Образец Hello проекта можно загрузить из [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).

Этот загружаемый файл содержит следующие проекты C# hello:

* CorrelationTopology: топология C# Storm, которая случайным образом генерирует события начала и конца для пользовательских сеансов. Каждый сеанс продолжается от 1 до 5 минут.

* SessionInfo: Консольное приложение C#, создающий таблицу HBase hello и предоставляются примеры запросов tooreturn сведения о данных, сохраненный сеанс.

## <a name="create-hello-table"></a>Создать таблицу hello

1. Откройте hello **SessionInfo** проекта в Visual Studio.

2. В **обозревателе решений**, щелкните правой кнопкой мыши hello **SessionInfo** проект и выберите **свойства**.

    ![Снимок экрана меню с выбранными свойствами](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. Выберите **параметры**, а затем набор hello следующие значения:

   * HBaseClusterURL: hello URL-адрес tooyour HBase кластера. Например, https://myhbasecluster.azurehdinsight.net.

   * HBaseClusterUserName: учетная запись администратора/HTTP hello для кластера

   * HBaseClusterPassword: hello пароль для учетной записи пользователя admin/HTTP hello

   * HBaseTableName: имя hello hello toouse таблицы с этим примером

   * HBaseTableColumnFamily: имя семейства столбца hello

     ![Изображение окна "Параметры"](./media/hdinsight-storm-correlation-topology/settings.png)

4. Запустите решение hello. При появлении запроса выберите таблицу, hello ключа toocreate hello «c» в кластере HBase.

## <a name="build-and-deploy-hello-storm-topology"></a>Построение и развертывание топологии Storm hello

1. Откройте hello **CorrelationTopology** решения в Visual Studio.

2. В **обозревателе решений**, щелкните правой кнопкой мыши hello **CorrelationTopology** проекта и выберите пункт Свойства.

3. Выберите в окне свойств hello **параметры** и введите hello значения конфигурации для этого проекта. Hello первые 5 являются hello используются одинаковые значения, hello **SessionInfo** проекта:

   * HBaseClusterURL: hello URL-адрес tooyour HBase кластера. Например, https://myhbasecluster.azurehdinsight.net.

   * HBaseClusterUserName: hello admin/HTTP учетная запись пользователя для кластера.

   * HBaseClusterPassword: hello пароль для учетной записи пользователя admin/HTTP hello.

   * HBaseTableName: имя hello hello toouse таблицы с этим примером. Это значение является одинаковым hello имя таблицы, используемой в проекте SessionInfo hello.

   * HBaseTableColumnFamily: имя семейства столбца hello. Это значение является одинаковым hello имя семейства столбца как используемый в проекте SessionInfo hello.

   > [!IMPORTANT]
   > Не изменяйте hello HBaseTableColumnNames, так как значения по умолчанию hello: hello имена, используемые **SessionInfo** tooretrieve данных.

4. Сохранить свойства hello, а затем постройте проект hello.

5. В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и выберите **отправить tooStorm на HDInsight**. При появлении запроса введите учетные данные hello подписки Azure.

   ![Пункт меню toostorm отправить изображение hello](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. В hello **отправить топологии** диалоговое окно, выберите hello Storm кластер toodeploy к этой топологии.

   > [!NOTE]
   > Hello первый раз отправить топологии, может потребоваться несколько секунд имя hello tooretrieve своими кластерами HDInsight.

7. Здравствуйте, после топологии hello отправлять и отправленных toohello кластера, **представление топологии Storm** открывает и отображает hello под управлением топологии. toorefresh hello данных, выберите hello **CorrelationTopology** и используется кнопка обновления hello в hello верхнем правом углу страницы приветствия.

   ![Изображение представления топологии hello](./media/hdinsight-storm-correlation-topology/topologyview.png)

   С началом создания данных топологии hello hello значение в hello **Emitted** приращения столбца.

   > [!NOTE]
   > Если hello **представление топологии Storm** не открывается автоматически, используйте hello следующие tooopen действия:
   >
   > 1. В **обозревателе решений** разверните **Azure**, а затем — **HDInsight**.
   > 2. Щелкните правой кнопкой мыши hello Storm кластера, hello топологии ОС, а затем выберите **представление топологии Storm**

## <a name="query-hello-data"></a>Запрос данных hello

После получится данных используйте следующие шаги tooquery hello данные hello.

1. Вернуть toohello **SessionInfo** проекта. Если он не открыт, запустите новый экземпляр.

2. При появлении запроса выберите **s** toosearch для НАЧАЛА события. Являются запрашиваемые tooenter начала и окончания времени toodefine диапазон времени - возвращаются только события, между этими двумя значениями времени.

    Используйте следующие hello форматирования при вводе hello начала времени и завершения: ЧЧ: мм ''M' или 'pm». Например, 11:20 pm.

    события в журнал tooreturn использовать время начала перед hello Storm топологии была развернута и время окончания сейчас. возвращаемые данные Hello содержит аналогичные toohello записи после текста:

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

Поиск hello works события окончания таким же как НАЧАЛА события. От 1 до 5 минут после НАЧАЛА события hello события окончания создаются случайным образом. Может иметь несколько раз события окончания hello диапазоны toofind tootry. События окончания также содержать hello продолжительность сеанса hello - hello различие между hello время события НАЧАЛА и время окончания события. Ниже приведен пример данных для событий КОНЕЦ:

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> Хотя hello введенные значения времени в формате местного времени, в формате UTC — время hello, возвращаемых запросом hello.

## <a name="stop-hello-topology"></a>Остановить hello топологии

Когда вы будете готовы toostop hello топологии, возвращают toohello **CorrelationTopology** проекта в Visual Studio. В hello **представление топологии Storm**выберите топологию hello и затем использовать hello **Kill** кнопку вверху hello представление топологии hello.

## <a name="delete-your-cluster"></a>Удаление кластера

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Дальнейшие действия

Другие примеры топологий для Storm см. в разделе [Примеры топологий для Storm в HDInsight](hdinsight-storm-example-topology.md).
