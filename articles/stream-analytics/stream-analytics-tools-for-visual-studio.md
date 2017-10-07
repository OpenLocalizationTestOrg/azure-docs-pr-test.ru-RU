---
title: "aaaUse Azure Stream Analytics средства для Visual Studio | Документы Microsoft"
description: "Приступая к работе учебника для hello Azure Stream Analytics средства для Visual Studio"
keywords: Visual Studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a>Использование инструментов Azure Stream Analytics для Visual Studio
## <a name="introduction"></a>Введение
В этом учебнике вы узнаете, как средства анализа потока toouse Azure для Visual Studio toocreate, создавать, локального тестирования, управления и отладки заданий Stream Analytics. 

После работы с этим учебником вы сможете выполнить следующие задачи:
* Изучить инструменты Stream Analytics для Visual Studio.
* Настроить и развернуть задание Stream Analytics.
* Протестировать это задание локально с помощью локальных примеров данных.
* С помощью мониторинга tootroubleshoot проблемы.
* Экспорт tooprojects существующего задания.

## <a name="prerequisites"></a>Предварительные требования
toocomplete этого учебника требуется hello следующие предварительные требования:
* Готово hello действия, предшествующие «Создание задания Stream Analytics» в hello [построить решение IoT с помощью учебника Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics). 
* Используйте Visual Studio 2015, Visual Studio 2013 с обновлением 4 или Visual Studio 2012. Поддерживаются выпуски Enterprise (Ultimate/Premium), Professional и Community. Выпуск Express не поддерживается. Visual Studio 2017 не поддерживается. 
* Используйте hello Azure SDK для .NET версии 2.7.1 или более поздней версии. Установите его с помощью hello [установщика веб-платформы](http://www.microsoft.com/web/downloads/platform.aspx).
* Установка hello [средства анализа потока для Visual Studio](http://aka.ms/asatoolsvs).

## <a name="create-a-stream-analytics-project"></a>Создание проекта Stream Analytics
1. В Visual Studio щелкните hello **файл** и выбрать пункт **новый проект**. 

2. В списке шаблонов hello hello левой части окна выберите **Stream Analytics** и нажмите кнопку **Azure Stream Analytics приложения**.

3. Введите hello проекта **имя**, **расположение**, и **имя решения** как и для других проектов.

    ![Окно нового проекта](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    Будет создан проект **Toll** в **обозревателе решений**.

    ![Проект Toll, созданный в обозревателе решений](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a>Выбор нужной подписки hello
1. В Visual Studio щелкните hello **представление** меню и открыть **обозревателя серверов**.

2. Войдите в систему, используя учетную запись Azure. 

## <a name="define-hello-input-sources"></a>Определение источников входных данных hello
1.  В **обозревателе решений**, разверните hello **входов** узла и имени **Input.json** слишком**EntryStream.json**. Дважды щелкните **EntryStream.json**.
2.  Hello **входных псевдонимов** теперь **EntryStream**. в скрипте hello запроса используется псевдоним Hello входных данных. 
3.  В поле **Тип источника** выберите **Поток данных**.
4.  В поле **Источник** выберите **Концентратор событий**.
5.  В **пространство имен служебной шины**выберите hello **TollData** параметр.
6.  В поле **Имя концентратора событий** выберите **запись**.
7.  В **имя политики концентратора событий**выберите **RootManageSharedAccessKey** (значение по умолчанию hello).
8.  В поле **Формат сериализации событий** выберите**Json**. 
9.  В поле **Кодировка** выберите **UTF-8**. Параметры должно иметь вид hello следующий снимок экрана:

    ![Окно ввода](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. toofinish приветствия мастера, нажмите кнопку **Сохранить**. Теперь можно добавить другой поток выхода hello toocreate источника входных данных. Щелкните правой кнопкой мыши hello **входов** , а затем установите **новый элемент**.

    ![Новый элемент](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. В окне приветствия щелкните **Azure Stream Analytics ввода**и измените hello **имя** слишком**ExitStream.json**. Щелкните **Добавить**.

    ![Окно "Добавить новый элемент"](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. Дважды щелкните **ExitStream.json** в проекте hello и выполните hello же шаги, как это было сделано для hello записи потока. Быть убедиться, что tooenter **выхода** для hello **имя концентратора событий** как показано на следующий снимок экрана приветствия:

    ![Окно ExitStream](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    Теперь определены два входных потока.

    ![Входные потоки входа и выхода](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    Затем добавьте входных справочных данных для файла hello BLOB-объект, содержащий данные регистрации автомобиля.

13. Щелкните правой кнопкой мыши hello **входов** узла в проекте hello, а затем выполните hello же шаги, как это было сделано для входных данных поток hello. Для параметра **Псевдоним входных данных** введите **Регистрация**, а для параметра **Тип источника** выберите **Справочные данные**.

    ![Окно регистрации](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. В **учетной записи хранилища**выберите hello **tolldata** параметр. В поле **Контейнер** выберите **tolldata**, а в поле **Шаблон пути** введите **registration.json**. Имя файла должно быть введено строчными буквами (в нем учитывается регистр).
15. toofinish приветствия мастера, нажмите кнопку **Сохранить**.

Теперь определены все входные данные hello.

## <a name="define-hello-output"></a>Указать выходные hello
1.  В **обозревателе решений**, разверните hello **входов** узла и дважды щелкните **Output.json**.

2.  В поле **Псевдоним выходных данных** введите **output**. 
3.  В поле **Приемник** выберите **База данных SQL**.
4.  В поле **База данных** выберите **TollDataDB**.
5.  В поле **Имя пользователя** введите **tolladmin**. 
6.  В поле **Пароль** введите **123toll!**.
7.  В поле **Таблица** введите **TollDataRefJoin**.
8.  Щелкните **Сохранить**.

    ![Окно вывода](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a>Создание запроса Stream Analytics
Этот учебник попыток tooanswer несколько вопросов для бизнеса, tootoll связанные данные. Он также создает запросов Stream Analytics, которые можно использовать в соответствующие ответы tooprovide Stream Analytics.
Перед началом первого задание Stream Analytics, давайте рассмотрим простой сценарий и hello синтаксис запроса.

### <a name="introduction-toohello-stream-analytics-query-language"></a>Введение toohello языка запросов Stream Analytics
Предположим, что необходимые toocount hello число автомобилей, введите через кабинку. Поскольку в этом примере непрерывного потока событий, у вас есть toodefine период времени. Изменение вопроса toobe hello, «сколько автомобилей введите через кабинку каждые три минуты?» Этот способ toocount, обычно является данных называется число переворачивающееся tooas hello.

Рассмотрим запрос hello Stream Analytics, который отвечает на этот вопрос:

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

Stream Analytics использует язык запросов, подобного SQL и добавляет несколько расширений toospecify связанных со временем аспекты hello запроса.

Дополнительные сведения см. в разделе [управление временем](https://msdn.microsoft.com/library/azure/mt582045.aspx) и [оконных](https://msdn.microsoft.com/library/azure/dn835019.aspx) конструкции, используемые в запросе hello с MSDN.

Теперь, когда вы написали первого запроса Stream Analytics, это время tootest его. Используйте файлы образцов данных hello, расположенный в папке TollApp в hello пути:

..\TollApp\TollApp\Data

Эта папка содержит hello следующие файлы:
*   Entry.json
*   Exit.json
*   Registration.json

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a>Hello число автомобилей, введя оплаты дорожного сбора
В проекте hello, дважды щелкните **Script.asaql** tooopen сценарий hello в hello **редактора запросов**. Скопируйте и вставьте скрипт hello в предыдущем разделе hello в редакторе hello. Hello редактор запросов поддерживает технологию IntelliSense, Цветовая подсветка синтаксиса и ошибки маркера hello.

![Редактор запросов](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a>Локальное тестирование запросов Stream Analytics

1. запрос toosee toocompile hello, при наличии синтаксическая ошибка, щелкните правой кнопкой мыши проект hello и выберите **сборки**. 

2. toovalidate этот запрос на основе образцов данных, можно использовать локальный образцы данных. Щелкните правой кнопкой мыши hello входных данных и выберите **добавить локальный вход**.

    ![Добавление локальных входных данных](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. Во всплывающем окне приветствия выберите hello образцы данных из локального пути. Щелкните **Сохранить**.

    ![Окно добавления локальных входных данных](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    Файл с именем **local_EntryStream.json** автоматически добавляется в папку tooyour входных данных.

    ![Папка добавлена tooinputs файла](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. В hello **редактора запросов**, нажмите кнопку **запуска локально**. Или можно нажать клавишу F5 hello.

    ![Локальный запуск](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Выходные данные локального запуска](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    Нажмите клавишу никаких выходных данных ключа tooview hello в hello **ASA локального результат выполнения** окна в Visual Studio. 

    ![Окно "Результаты локального запуска ASA"](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. Нажмите кнопку **откройте папку результатов** toocheck hello выходных файлов, оба в формате CSV и JSON.

    ![Выходные данные "Открыть папку результата"](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a>Образец hello входных данных
Вы также можете образец входных данных из локального файла tooa источников входных данных. 
1. Щелкните правой кнопкой мыши файл hello входной конфигурации и выберите **образец данных**. 

   ![Образец данных](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    Сейчас можно выбрать только концентратор событий или центр Интернета вещей. Другие источники входных данных не поддерживаются.

2. Во всплывающем окне приветствия введите hello локальный путь, используемый toosave hello образца данных. Щелкните **Выборка**.

    ![Окно "Образцы данных"](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    Следить за ходом hello в hello можно **вывода** окна. 

    ![Окно вывода](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a>Отправка запросов Stream Analytics tooAzure
1. В hello **редактора запросов**, нажмите кнопку **отправить tooAzure** в редакторе сценариев hello.

    ![Отправить tooAzure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. Выберите **Create a New Azure Stream Analytics Job** (Создать задание Azure Stream Analytics). Введите hello **имя задания**и выберите hello правильный **подписки**. Нажмите кнопку **Submit**(Отправить).

    ![Окно отправки задания](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a>Запустите задание
После создания задания представлении задания hello открывается автоматически. 
1. toostart hello задания, нажмите кнопку hello **зеленая стрелка** кнопки.

    ![Запустите задание](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. Выберите параметр по умолчанию hello и нажмите кнопку **запустить**.
 
    ![Окно запуска задания](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    Задание Hello **состояние** изменяет слишком**под управлением**, и **событий ввода** и **выходных событий** отображаются.

    ![Состояние выполнения в сводных данных задания](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a>Результаты проверки hello в Visual Studio
1. В Visual Studio откройте **обозревателя серверов** и щелкните правой кнопкой мыши hello **TollDataRefJoin** таблицы.
2. Выберите **Показать таблицу данных** toosee hello выходные данные задания.
   
    ![Выбор "Показать таблицу данных" в обозревателе серверов](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a>Представление hello задания метрики
Определенную базовую статистику задания можно найти с помощью **метрик задания**. 

![Окно метрик задания](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a>Список заданий hello в обозревателе серверов
В **обозревателе серверов** щелкните **Задания Stream Analytics** и щелкните **Обновить**. Задание Hello отображается под **заданий Stream Analytics**.

![Задания Stream Analytics в списке обозревателя серверов](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a>Привет открыть просмотр задания
Просмотр задания tooopen hello, разверните узел задания и дважды щелкните hello **представлении задания** узла.

![Узел представления задания](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a>Экспортировать существующий проект tooa задания
Существует два способа, можно экспортировать существующий проект tooa задания.

В **обозревателя серверов**, щелкните правой кнопкой мыши узел задания hello в hello **заданий Stream Analytics** , а затем выберите **Экспорт tooNew Stream Analytics проекта**.

![Экспорт tooNew Stream Analytics проекта](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

создается проект Hello в **обозревателе решений**.

![Проект, созданный в обозревателе решений](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
Можно также использовать представление задания hello и нажмите кнопку **создания проекта**.

![Создание проекта](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a>Известные проблемы и ограничения
 
- Не поддерживаются выходные данные Power BI и Azure Date Lake Store.
- Редактор не поддерживает добавление или изменение определяемых пользователем функций JavaScript.

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics: выявление мошенничества в режиме реального времени](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
