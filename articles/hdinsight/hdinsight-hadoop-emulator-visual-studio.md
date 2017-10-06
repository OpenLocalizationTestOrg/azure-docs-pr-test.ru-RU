---
title: "Озеро aaaData средства для Visual Studio с песочницей Hortonworks - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse hello Озера данных Azure tools для Visual Studio с песочницей Hortonworks hello, работе на локальной виртуальной Машине. С помощью этих средств можно создавать и запускать задания Hive и Pig для \"песочницы\" hello и просмотр выходных данных задания и журнал."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a>Использовать средства hello Озера данных Azure для Visual Studio с hello Hortonworks "песочницы"

Azure Data Lake включает в себя средства для работы с универсальными кластерами Hadoop. В этом документе шаги hello необходимые средства Озера данных hello toouse с hello Hortonworks "песочницы", работающих в локальной виртуальной машины.

Использование hello Hortonworks "песочницы" позволяет toowork с Hadoop локально в среде разработки. После разработки решения и хотите toodeploy его в масштабе, можно переместить tooan кластера HDInsight.

## <a name="prerequisites"></a>Предварительные требования

* Здравствуйте, "песочницы" Hortonworks, работающих в виртуальной машине в среде разработки. Этот документ был написан и протестирован с "песочницы" hello, работающих в Oracle VirtualBox. Сведения о настройке hello "песочницы" в разделе hello [Приступая к работе с hello Hortonworks "песочницы".](hdinsight-hadoop-emulator-get-started.md) .

* Visual Studio 2013, Visual Studio 2015 или Visual Studio 2017 (любой выпуск).

* Hello [Azure SDK для .NET](https://azure.microsoft.com/downloads/) 2.7.1 или более поздней версии.

* Hello [Озера данных Azure tools для Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).

## <a name="configure-passwords-for-hello-sandbox"></a>Настройка паролей для "песочницы" hello

Убедитесь в том, что hello запущенного Hortonworks "песочницы". Следуйте указаниям hello hello [Приступая к работе с hello "песочницы" Hortonworks](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) документа. Эти шаги помогут вам настроить hello пароль для hello SSH `root` учетную запись, а hello Ambari `admin` учетной записи. Эти пароли используются при подключении "песочницы" toohello из Visual Studio.

## <a name="connect-hello-tools-toohello-sandbox"></a>Подключения "песочницы" toohello средства hello

1. Откройте Visual Studio и выберите **Вид**, а затем — **Обозреватель серверов**.

2. Из **обозревателя серверов**, щелкните правой кнопкой мыши hello **HDInsight** запись, а затем выберите **подключения tooHDInsight эмулятор**.

    ![Снимок экрана из обозревателя серверов, с tooHDInsight подключить эмулятор выделен](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. Из hello **подключения эмулятора tooHDInsight** диалогового окна введите пароль hello, настроенный для Ambari.

    ![Снимок экрана: диалоговое окно с выделенным текстовым полем для ввода пароля](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    Выберите **Далее** toocontinue.

4. Используйте hello **пароль** поле tooenter hello пароль, настроенные для hello `root` учетной записи. Оставьте остальные поля на значение по умолчанию hello hello.

    ![Снимок экрана: диалоговое окно с выделенным текстовым полем для ввода пароля](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    Выберите **Далее** toocontinue.

5. Ожидания для проверки служб toofinish hello. В некоторых случаях проверка может завершиться ошибкой и запрашивает tooupdate hello конфигурации. Если проверка завершается неудачно, установите **обновление**и дождитесь hello конфигурации и проверки для службы toofinish hello.

    ![Снимок экрана: диалоговое окно с выделенной кнопкой "Обновить"](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > процесс обновления Hello использует Ambari toomodify приветствия ожидаемых toowhat конфигурации Hortonworks "песочницы" hello Озера данных средства для Visual Studio.

6. После завершения проверки, выберите **Готово** toocomplete конфигурации.
    ![Снимок экрана: диалоговое окно с выделенной кнопкой "Готово"](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)

     >[!NOTE]
     > В зависимости от скорости hello среды разработки и hello объем памяти, выделенной toohello виртуальной машины его можно воспользоваться tooconfigure несколько минут и проверять hello службы.

После выполнения этих шагов, теперь у вас есть **локального кластера HDInsight** записи в обозревателе серверов hello **HDInsight** раздела.

## <a name="write-a-hive-query"></a>Написание запроса Hive

Hive предоставляет язык запросов по типу SQL (HiveQL) для работы со структурированными данными. Используйте следующие шаги toolearn как toorun по требованию запросов к локальному кластеру hello hello.

1. В **обозревателя серверов**, щелкните правой кнопкой мыши запись hello для hello локального кластера, который был добавлен ранее и выберите **написать запрос Hive**.

    ![Снимок экрана: обозреватель сервера с выделенным пунктом "Написать запрос Hive"](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    Откроется окно нового запроса. Здесь можно быстро писать и отправить запрос toohello локального кластера.

2. В новом окне запроса hello введите следующую команду hello:

        select count(*) from sample_08;

    toorun hello запроса select **отправить** hello верхней части окна hello. Оставьте hello другие значения (**пакета** и имя сервера) в значения по умолчанию hello.

    ![Снимок экрана окна запроса, с выделенной кнопкой отправки hello](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    Можно также использовать hello раскрывающееся меню рядом слишком**отправить** tooselect **Дополнительно**. Дополнительные параметры позволяют tooprovide Дополнительные параметры для отправки задания hello.

    ![Снимок экрана: диалоговое окно "Отправить скрипт"](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. После отправки запроса hello отображается состояние задания hello. состояние задания Hello отображаются сведения о задания hello, обрабатывается Hadoop. **Состояние задания** предоставляет hello состояние задания hello. периодически обновляется состояние Hello, или можно использовать hello обновление значок toorefresh hello состояния вручную.

    ![Снимок экрана: диалоговое окно "Представление заданий" с выделенной записью "Состояние задания"](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    После hello **состояние задания** изменяет слишком**завершен**, отображается направленный ациклического графа (DAG). На этой схеме описан hello путь выполнения, который был определяется Tez при обработке запроса Hive hello. Tez — подсистема выполнения по умолчанию hello для куста hello локальном кластере.

    > [!NOTE]
    > Tez будет по умолчанию hello при использовании кластеры HDInsight под управлением Linux. Это не по умолчанию hello в HDInsight под управлением Windows. toouse его нет, необходимо добавить строку hello `set hive.execution.engine = tez;` toohello Начало запроса Hive.

    Используйте hello **выходные данные задания** связать tooview hello вывода. В этом случае это 823 hello количество строк в таблице sample_08 hello. Диагностические данные об hello задания можно просмотреть с помощью hello **журнала задания** и **Загрузка журнала YARN** ссылки.

4. Можно также запустить задания Hive интерактивно, изменив hello **пакета** поле слишком**Interactive**. а затем нажать кнопку **Выполнить**.

    ![Снимок экрана с выделенным элементом "Интерактивный" и кнопкой "Выполнить"](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    Интерактивный запрос, потоки hello выходные данные журнала, созданного во время обработки toohello **HiveServer2 вывода** окна.

    > [!NOTE]
    > Hello сведения hello те же данные, можно получить из hello **журнала задания** связь после завершения задания.

    ![Снимок экрана: журнал выходных данных](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a>Создание проекта Hive

Вы также можете создать проект, который содержит несколько скриптов Hive. Используйте проект, если требуется иметь связанные сценарии или сценарии toostore в системе управления версиями.

1. Откройте Visual Studio, выберите **Файл**, **Создать**, а затем **Проект**.

2. Из списка проектов hello, разверните **шаблоны**, разверните **Озера данных Azure**и выберите **HIVE (HDInsight)**. Выберите из списка шаблонов hello **Hive образец**. Введите имя и расположение, а затем нажмите кнопку **ОК**.

    ![Снимок экрана; окно нового проекта с выделенными элементами "Azure Data Lake", "HIVE", "Пример Hive" и "ОК"](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

Hello **Hive образец** проект содержит два сценария **WebLogAnalysis.hql** и **SensorDataAnalysis.hql**. Вы можете отправить эти скрипты с помощью hello же **отправить** кнопку hello верхней части окна hello.

## <a name="create-a-pig-project"></a>Создание проекта Pig

Тогда как Hive предоставляет язык по типу SQL для работы со структурированными данными, Pig работает, преобразуя данные. Pig предоставляет язык (латиница Pig), который позволяет вам toodevelop конвейера преобразований. toouse Pig с hello локального кластера, выполните следующие действия.

1. Откройте Visual Studio, выберите **Файл**, **Создать**, а затем — **Проект**. Из списка проектов hello, разверните узел **шаблоны**, разверните **Озера данных Azure**, а затем выберите **Pig (HDInsight)**. Выберите из списка шаблонов hello **Pig приложения**. Введите имя и расположение, а затем нажмите кнопку **ОК**.

    ![Снимок экрана; окно нового проекта с выделенными элементами "Azure Data Lake", "Pig", "Приложение Pig" и "ОК"](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. Введите после текста как содержимое hello hello hello **script.pig** файла, созданного с помощью этого проекта.

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    А чем Hive, Pig использует другой язык, выполнение задания hello одинаково для обоих языков через hello **отправить** кнопки. Выбор hello раскрывающегося списка рядом с **отправить** выводит диалоговое окно расширенного отправки для Pig.

    ![Снимок экрана: диалоговое окно "Отправить скрипт"](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. также отображается состояние заданий Hello и выходные данные, Здравствуйте таким же, как запрос Hive.

    ![Снимок экрана: завершенное задание Pig](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a>Просмотр заданий

Средства Озера данных также позволяют tooeasily Просмотр сведений о заданиях, которые были запущены в Hadoop. Используйте следующие шаги toosee hello заданий, которые были запущены на локальном кластере hello hello.

1. Из **обозревателя серверов**, щелкните правой кнопкой мыши локальный кластер hello и выберите **Просмотр заданий**. Отображается список заданий, которые были отправленной toohello кластера.

    ![Снимок экрана: обозреватель сервера с выделенным пунктом "Просмотреть задания"](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. Hello список заданий выберите одну tooview сведений о задании hello.

    ![Снимок экрана из задания браузера, с помощью одного из заданий hello выделен](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    Отображаемые сведения Hello — примерно toowhat, отображаемые после выполнения запроса Hive или Pig, включая ссылки tooview hello выходные данные и сведения журналов.

3. Можно также изменять и повторно отправить задания hello отсюда.

## <a name="view-hive-databases"></a>Просмотр баз данных Hive

1. В **обозревателя серверов**, разверните hello **локального кластера HDInsight** входа и разверните **баз данных Hive**. Hello **по умолчанию** и **xademo** базы данных в локальном кластере hello отображаются. Развертывание базы данных показывает hello таблиц в базе данных hello.

    ![Снимок экрана: обозреватель сервера с развернутыми базами данных](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. Раскройте таблицу отображает hello столбцы этой таблицы. Просмотр hello tooquickly данных, щелкните правой кнопкой мыши таблицу и выберите **представление первые 100 строк**.

    ![Снимок экрана: обозреватель сервера с развернутой таблицей и выбранным пунктом "Просмотреть первые 100 строк"](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a>Свойства базы данных и таблицы

Можно просмотреть свойства hello базы данных или таблицы. При выборе **свойства** отображаются сведения об элементе выбран hello в окне свойств hello. Например в разделе hello сведения, отображаемые на следующий снимок экрана приветствия:

![Снимок экрана: окно свойств](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a>Создание таблицы

toocreate таблицу, щелкните правой кнопкой мыши базу данных, а затем выберите **Create Table**.

![Снимок экрана: обозреватель сервера с выделенным пунктом "Создать таблицу"](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

Затем можно создать таблицу hello, с помощью формы. Внизу hello следующий снимок экрана приветствия, можно увидеть hello необработанные HiveQL, используемые toocreate hello таблицы.

![Снимок экрана: hello форму используется toocreate таблицы](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a>Дальнейшие действия

* [Изучение ropes hello объекта hello Hortonworks "песочницы"](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Hadoop tutorial - Getting started with HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/) (Руководство по началу работы с Hadoop)
