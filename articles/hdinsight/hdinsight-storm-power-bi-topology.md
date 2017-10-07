---
title: "aaaUse Apache Storm с Power BI — Azure HDInsight | Документы Microsoft"
description: "Создавайте отчеты Power BI на основе данных, собранных из топологии C#, запущенной в кластере Apache Storm в HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a>Использование Power BI toovisualize данных из топологии Apache Storm

Power BI позволяет toovisually отображать данные в виде отчетов. В этом документе приведен пример того, как toouse Apache Storm данных toogenerate HDInsight для Power BI.

> [!NOTE]
> Hello действия, описанные в этом документе используют среду разработки Windows с помощью Visual Studio. Hello скомпилированный проект может быть отправлено tooa кластера HDInsight под управлением Linux. Топологии SCP.NET поддерживаются только теми кластерами под управлением Linux, которые созданы после 28 октября 2016 г.
>
> toouse топологии на C# в кластере под управлением Linux, hello обновления пакета Microsoft.SCP.Net.SDK NuGet, используемый в ваш проект tooversion 0.10.0.6 или более поздней версии. Hello версию пакета hello должно также совпадать hello основной номер версии Storm установлен на HDInsight. Например, для Storm в HDInsight версии 3.3 и 3.4 используйте Storm версии 0.10.x, а HDInsight 3.5 использует Storm 1.0.x.
>
> C# топологиях для кластеров под управлением Linux необходимо использовать .NET 4.5 и использовать моно toorun hello кластера HDInsight. Большинство возможностей будут работать. Однако следует проверить hello [совместимости моно](http://www.mono-project.com/docs/about-mono/compatibility/) документа потенциальные проблемы совместимости.
>
> Java-версию этого проекта, работающую с кластером HDInsight под управлением Linux или Windows, можно найти в статье [Обработка событий из службы концентраторов событий Azure с помощью Storm в HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="prerequisites"></a>Предварительные требования

* Пользователь Azure Active Directory с доступом к [Power BI](https://powerbi.com).
* Кластер HDInsight. Дополнительные сведения см. в статье [Начало работы с Storm в HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

  > [!IMPORTANT]
  > Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Visual Studio (один из следующих версий hello)

  * Visual Studio 2012 с [обновлением 4](http://www.microsoft.com/download/details.aspx?id=39305)
  * Visual Studio 2013 с [обновлением 4](http://www.microsoft.com/download/details.aspx?id=44921) или [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409);
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * Visual Studio 2017 (любой выпуск)

* Hello средства HDInsight для Visual Studio: в разделе [приступить к работе со средствами hello HDInsight для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) сведения на сведения об установке.

## <a name="how-it-works"></a>Принцип работы

В нашем примере используется топология C# Storm, которая случайным образом формирует данные журнала Internet Information Services (IIS). Эти данные затем записываются tooa базы данных SQL, а оттуда это используется toogenerate отчеты в Power BI.

следующие файлы реализуйте hello основные функциональные возможности в этом примере Hello:

* **SqlAzureBolt.cs**: записывает сведения, созданные в tooSQL топологии hello Storm базы данных.
* **IISLogsTable.sql**: hello Transact-SQL инструкции, используемые toogenerate hello базы данных, которая hello данные хранятся в.

> [!WARNING]
> Создайте таблицу hello в базе данных SQL перед запуском топологии hello в кластере HDInsight.

## <a name="download-hello-example"></a>Загрузить пример hello

Загрузите hello [HDInsight C# Storm Power BI пример](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi). toodownload, либо вилки или клону его с помощью [git](http://git-scm.com/), или использовать hello **загрузки** toodownload ссылку .zip hello архива.

## <a name="create-a-database"></a>Создание базы данных

1. toocreate базы данных, выполните действия hello в hello [SQL Database tutorial](../sql-database/sql-database-get-started.md) документа.

2. Подключение базы данных toohello hello следующие шаги в hello [подключения tooa базы данных SQL с помощью Visual Studio](../sql-database/sql-database-connect-query.md) документа.

3. В обозревателе объектов щелкните правой кнопкой мыши базу данных hello и выберите **новый запрос**. Вставьте содержимое hello hello **IISLogsTable.sql** файл, включенный в hello загружен в окно запроса hello проекта, а затем используйте сочетание клавиш Ctrl + Shift + E tooexecute hello запроса. Должно появиться сообщение, которое hello команд успешно завершено.

## <a name="configure-hello-sample"></a>Настройка образца hello

1. Из hello [портал Azure](https://portal.azure.com), выберите вашу базу данных SQL. Из hello **Essentials** hello SQL колонке базы данных, выберите раздел **Показать строки подключения базы данных**. В появившемся списке hello скопируйте hello **ADO.NET (проверка подлинности SQL)** сведения.

2. Открытие образца hello в Visual Studio. Из **обозревателе решений**откройте hello **App.config** файл, а затем найдите hello следующая запись:

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    Замените hello **TOBEFILLED ##** значение с hello строку подключения базы данных копируются в предыдущем шаге hello. Замените **{вашей\_username}** и **{вашей\_пароль}** с hello имя пользователя и пароль для базы данных hello.

3. Сохраните и закройте файлы hello.

## <a name="deploy-hello-sample"></a>Развертывание образца hello

1. Из **обозревателе решений**, щелкните правой кнопкой мыши hello **StormToSQL** проект и выберите **отправить tooStorm на HDInsight**. Кластер HDInsight выберите hello из hello **кластер Storm** диалогового окна в раскрывающемся списке.

   > [!NOTE]
   > Может потребоваться несколько секунд для hello **кластер Storm** toopopulate раскрывающийся список с именами серверов.
   >
   > Если необходимо, введите учетные данные входа hello для подписки Azure. При наличии более чем одной подписке, войдите в toohello версией, которая содержит ваш ураган в кластере HDInsight.

2. При отправке топологии hello hello __средство просмотра топологии__ отображается. tooview этой топологии, выберите hello SqlAzureWriterTopology входа из списка hello.

    ![Hello топологий, с выбранной топологии hello](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    Можно использовать эту информацию toosee представление топологии hello или дважды щелкните компонент конкретных tooa входа (например, «hello SqlAzureBolt) toosee сведения в топологии hello.

3. После hello топологии имеет запуска для нескольких минут, используется база данных hello toocreate окна запроса SQL возвращаемого toohello. Замените существующие инструкции hello приветствия при следующем запросе:

        select * from iislogs;

    Используйте клавиши Ctrl + Shift + E tooexecute hello запросов и вы должны получить аналогичные toohello результаты следующие данные:

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    Эти данные будет записана из топологии Storm hello.

## <a name="create-a-report"></a>Создание отчета

1. Подключение toohello [соединителю базы данных SQL Azure](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) для Power BI. 

2. В элементе **Базы данных** выберите **Получить**.

3. Выберите **База данных SQL Azure** и щелкните **Подключиться**.

    > [!NOTE]
    > Может появиться запрос toocontinue Power BI Desktop toodownload hello. Если это так, используйте следующие шаги tooconnect hello:
    >
    > 1. Откройте Power BI Desktop и выберите __Получение данных__.
    > 2. Выберите __Azure__, а затем __База данных SQL Azure__.

4. Введите tooyour tooconnect hello сведения базы данных SQL Azure. Эти сведения можно найти, перейдя по адресу hello [портал Azure](https://portal.azure.com) и выбрав эту базу данных SQL.

   > [!NOTE]
   > Можно также задать интервал обновления hello и настраиваемые фильтры с помощью **включить дополнительные параметры** hello подключитесь диалогового окна.

5. После подключения, вы увидите новый набор данных с таким же именем как hello базы данных, вы подключены к hello. Выберите toobegin dataset hello проектирования отчета.

6. Из **поля**, разверните hello **IISLOGS** входа. toocreate реализован отчетов, что списки hello URI, установите флажок hello для **URISTEM**.

    ![Создание отчета](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. Затем перетащите **МЕТОД** toohello отчета. реализован hello toolist обновления отчета Hello и hello соответствующий метод HTTP, используемый для hello HTTP-запроса.

    ![Добавление данных метод hello](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. Из hello **визуализации** столбец, выберите hello **поля** значок, а затем выберите hello стрелку вниз рядом слишком**МЕТОД** в hello **значения**раздел. Выберите toodisplay обращался число сколько раз URI **число**.

    ![Изменение числа tooa методов](./media/hdinsight-storm-power-bi-topology/count.png)

9. Затем выберите hello **гистограмму с накоплением** toochange Отображение сведений hello.

    ![Изменение диаграммы с накоплением tooa](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. toosave hello отчета, выберите **Сохранить** и введите имя отчета hello.

## <a name="stop-hello-topology"></a>Остановить hello топологии

Топология Hello продолжается toorun, пока не будет остановлена пользователем или удалить hello ураган в кластере HDInsight. toostop hello топологии, выполните следующие шаги hello.

1. В Visual Studio возвращается toohello средство просмотра топологии и выберите топологию hello.

2. Выберите hello **Kill** кнопку toostop hello топологии.

    ![KILL кнопку на топологии hello сводки](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Удаление кластера

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Дальнейшие действия

В этом документе вы узнали, как данные toosend из tooSQL топологии Storm базы данных, затем визуализации данных hello, с помощью Power BI. Сведения о том, как toowork с использованием других технологий Azure, с помощью Storm на HDInsight, см. следующий документ hello:

* [Примеры топологий для Storm в HDInsight](hdinsight-storm-example-topology.md)
