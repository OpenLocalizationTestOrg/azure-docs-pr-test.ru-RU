---
title: "aaaMonitor и управления ими конвейеры данных — Azure | Документы Microsoft"
description: "Узнайте, как toouse Здравствуйте, мониторинг и управление toomonitor приложения и управлять фабриками данных Azure и конвейеры."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: 5e4ef6ec5fb8ebc9bda0be7899a39a51d58403d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-monitoring-and-management-app"></a>Мониторинг и управление ими конвейеров фабрики данных Azure с помощью приложения hello мониторинг и управление
> [!div class="op_single_selector"]
> * [Использование портала Azure или Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [Использование приложения для мониторинга и управления](data-factory-monitor-manage-app.md)
>
>

В этой статье описывается toouse мониторинг и управление toomonitor приложения hello, управления и отладки конвейеров фабрики данных. Он также содержит сведения по как toocreate предупреждения tooget уведомления об ошибках. Вы можете начать с помощью приложения hello за просмотром hello следующие видео:

> [!NOTE]
> пользовательский интерфейс Hello показано hello видео может не соответствовать отображаемые на портале hello. Это немного старше, но основные понятия остаются hello же. 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-hello-monitoring-and-management-app"></a>Запустите приложение hello мониторинг и управление
hello toolaunch монитора и приложение для управления, нажмите кнопку hello **отслеживать состо & Управление** плитки приветствия **фабрики данных** колонку для фабрики данных.

![Мониторинг плитки на домашней странице hello фабрики данных](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

Вы увидите мониторинг и управление приложение hello открыть в отдельном окне.  

![Приложение для мониторинга и управления](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> При появлении этого веб-браузер hello застряла в «Авторизации...», снимите hello **блокировать сторонние файлы cookie и данным сайта** флажок--или он установлен, необходимо создать исключение для **login.microsoftonline.com** , а затем повторите попытку tooopen приложение hello.


В списке действий Windows hello в средней области hello появится окно действия для каждого запуска действия. Например при наличии toorun действие, запланированное hello каждый час на пять часов, см пять окон действий, связанных с пять срезы. Если вы не видите окон действий в списке hello нижней hello, hello следующие:
 
- Обновление hello **время начала** и **время окончания** фильтров в верхнем toomatch hello hello запуска и завершения работы конвейера и нажмите кнопку hello **применить** кнопки.  
- Список действий Windows Hello не обновляется автоматически. Щелкните hello **обновление** на инструментов hello в hello **действия Windows** списка.  

При отсутствии tootest фабрики данных приложения следующие действия с, hello учебника: [копирования данных из хранилища больших двоичных объектов tooSQL базы данных с помощью фабрики данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="understand-hello-monitoring-and-management-app"></a>Понять, управление и мониторинг приложение hello
Есть три вкладки слева hello: **обозреватель ресурсов**, **представления мониторинга**, и **предупреждения**. Первая вкладка Hello (**обозреватель ресурсов**) выбран по умолчанию.

### <a name="resource-explorer"></a>Обозреватель ресурсов
Вы видите hello следующее:

* Обозреватель ресурсов Hello **представление в виде дерева** hello левой панели.
* Hello **представление диаграммы** hello в в верхней части средней панели hello.
* Hello **действия Windows** списке нижней hello в средней области hello.
* Hello **свойства**, **действия окно обозревателя**, и **сценарий** вкладках в правой области hello.

В обозревателе ресурсов можно просмотреть все ресурсы (конвейеры, наборы данных, связанных служб) в фабрике данных hello в виде дерева. При выборе объекта в обозревателе ресурсов вы заметите следующее:

* Hello связанные сущности, выделяется в представление диаграммы hello фабрики данных.
* [Связанные действия windows](data-factory-scheduling-and-execution.md) , выделяются в списке действий Windows hello нижней hello.  
* в окне свойств hello hello правой панели отображаются свойства Hello hello выбранного объекта.
* Hello определения JSON hello выбранного объекта отображается, если это применимо. (например: связанная служба, набор данных или конвейер).

![Обозреватель ресурсов](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

В разделе hello [планирования и выполнения](data-factory-scheduling-and-execution.md) подробные Общие сведения о windows действия.

### <a name="diagram-view"></a>Представление схемы
Hello фабрики данных представление схемы предоставляет единое toomonitor стекла и управление ими фабрику данных и ресурсы. При выборе сущности фабрики данных (dataset и конвейер) hello представление схемы:

* в древовидном представлении hello выбрана сущность фабрики данных Hello.
* Hello связанные действия, который windows, выделяются в списке действий Windows hello.
* в окне свойств hello отображаются свойства Hello hello выбранного объекта.

При включении конвейера hello (не в приостановленном состоянии), он отображается с зеленая линия:

![Выполняющийся конвейер](./media/data-factory-monitor-manage-app/PipelineRunning.png)

Можно приостановить, возобновить или завершить конвейера, выбрав его в представлении диаграммы hello и использование hello кнопок на панели команд hello.

![Приостановить или возобновить на панели команд, hello](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
Существуют три кнопки панели команд для конвейера hello в hello представление диаграммы. Можно использовать hello вторая кнопка toopause hello конвейера. Приостановка не завершить hello, выполняемые действия и позволяет им продолжить toocompletion. Третья кнопка Hello hello конвейера приостанавливает и прекращает работу своих существующих выполняемых действий. Первая кнопка Hello возобновляет hello конвейера. При приостановке конвейер hello цвет конвейера hello меняется. Например приостановленного конвейера выглядит следующим образом в hello после изображения. 

![Приостановленный конвейер](./media/data-factory-monitor-manage-app/PipelinePaused.png)

Можно выбрать несколько конвейеров два или более с помощью hello клавишу Ctrl. Можно использовать панель кнопок hello команда toopause или возобновления нескольких конвейеров одновременно.

Вы можете также щелкнуть правой кнопкой конвейера и выбрать параметры toosuspend, возобновлять или завершать работу конвейера. 

![Контекстное меню конвейера](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

Нажмите кнопку hello **откройте конвейера** параметр toosee все hello действий в конвейере hello. 

![Откройте меню конвейера](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

Привет открыть конвейера, можно просмотреть все действия в конвейере hello. В этом примере в конвейере существует только одно действие — действие копирования. 

![Открытый конвейер](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

toogo резервное toohello предыдущего представления, щелкните имя фабрики данных hello в меню навигации hello верхней hello.

Hello конвейера при выборе выходной набор данных или при перемещении мыши над hello выходной набор данных, можно просмотреть действия Windows hello всплывающего окна для этого набора данных.

![Всплывающее окно "Activity Windows" (Окна действий)](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

Сведения об активности окна toosee можно щелкнуть для него hello **свойства** окно hello правой панели.

![Свойства окна действий](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

В правой области hello переключение toohello **действия окно обозревателя** вкладке toosee Дополнительные сведения см.

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

Отображается также **разрешить переменные** для каждой попытки выполнения для действия в hello **попыток** раздела.

![Разрешенные переменные](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

Переключение toohello **сценарий** вкладке toosee hello Определение сценария JSON для выбранного объекта hello.   

![Вкладка "Скрипт"](./media/data-factory-monitor-manage-app/ScriptTab.png)

Окна действий можно просматривать в трех местах:

* Hello окон действий во всплывающих окнах hello представление диаграммы (средняя панель).
* Hello окно обозревателя действие hello правой панели.
* Список действий Windows Hello hello нижней панели.

В всплывающих окон действий hello и действия окно обозревателя таблицу можно прокрутить toohello предыдущей недели и hello следующей неделе, используя hello стрелок влево и вправо.

![Кнопки со стрелками вправо и влево в "Activity Window Explorer" (Обозреватель окон действий)](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

Внизу hello hello представление диаграммы, можно увидеть эти кнопки: увеличить масштаб, уменьшить масштаб, tooFit масштаба масштаб 100%, макет блокировки. Hello **макета блокировки** кнопку предотвращает случайное перемещение таблиц и конвейеров в hello представление диаграммы. Она включена по умолчанию. Можно отключить его и перемещать сущностей в схеме hello. При выключении этого параметра можно использовать hello последней кнопки tooautomatically позиции таблиц и конвейеров. Также можно увеличить или уменьшить с помощью hello колесика мыши.

![Команды изменения масштаба в представлении схемы](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a>Список "Activity Windows" (Окна действий)
Список действий Windows Hello hello нижней части средней панели hello отображает все действия для hello набора данных, выбранного в hello обозреватель ресурсов или hello представление диаграммы. По умолчанию список hello — по убыванию, это означает, что вы видите окно последние действия hello вверху hello.

![Список "Activity Windows" (Окна действий)](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

Этот список не обновляет автоматически, поэтому ее обновление используйте кнопку обновления hello на панели инструментов toomanually hello.  

Действие windows может быть одним из следующих статусов hello:

<table>
<tr>
    <th align="left">Состояние</th><th align="left">Подсостояние</th><th align="left">Описание</th>
</tr>
<tr>
    <td rowspan="8">Waiting</td><td>ScheduleTime</td><td>время Hello не входят в toorun окно действие hello.</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>Hello восходящие зависимости не готовы.</td>
</tr>
<tr>
<td>ComputeResources</td><td>Hello вычислительные ресурсы недоступны.</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>Все экземпляры действий hello заняты обработкой других окон действий.</td>
</tr>
<tr>
<td>ActivityResume</td><td>Действие Hello приостановлено и не может работать windows действие hello, пока будет возобновлено.</td>
</tr>
<tr>
<td>Retry</td><td>Повторная попытка выполнения операции Hello.</td>
</tr>
<tr>
<td>Проверка</td><td>Проверка еще не начата.</td>
</tr>
<tr>
<td>ValidationRetry</td><td>Проверка выполняется повторная toobe ожидания.</td>
</tr>
<tr>
<tr>
<td rowspan="2">InProgress</td><td>Validating</td><td>Проверка выполняется.</td>
</tr>
<td>-</td>
<td>окно действия Hello обрабатывается.</td>
</tr>
<tr>
<td rowspan="4">Сбой</td><td>TimedOut</td><td>Выполнение действия Hello продолжалась дольше, чем допустимых с действия "hello".</td>
</tr>
<tr>
<td>Canceled</td><td>окно Hello действия была отменена пользователем.</td>
</tr>
<tr>
<td>Проверка</td><td>Сбой проверки.</td>
</tr>
<tr>
<td>-</td><td>окно действия Hello сбой toobe или подтверждения.</td>
</tr>
<td>Ready</td><td>-</td><td>окно действия Hello готов к использованию.</td>
</tr>
<tr>
<td>Skipped</td><td>-</td><td>окно Hello действия не было обработано.</td>
</tr>
<tr>
<td>None</td><td>-</td><td>В окне активности используется tooexist в другом состоянии, но был сброшен.</td>
</tr>
</table>


Появляется при нажатии кнопки окна действия в списке hello, сведения о ней в hello **действия Проводник** или hello **свойства** окна на правом hello.

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a>Обновление окон действий
Подробности Hello не обновляются автоматически, поэтому следует использовать hello обновления (hello второй) кнопки на панели списка toomanually обновления hello действия windows hello команд.  

### <a name="properties-window"></a>Окно "Свойства"
окно "Свойства" Hello находится в области справа hello приложение hello наблюдения и управления.

![Окно "Свойства"](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

Показать свойства для hello элемента, выбранного в hello обозреватель ресурсов (дерево), представление схемы или списка действий Windows.

### <a name="activity-window-explorer"></a>Activity Window Explorer
Hello **действия окно обозревателя** окно находится в области справа hello приложение hello наблюдения и управления. Он отображает сведения о окно hello действия, выбранного в всплывающее окно действия Windows hello или список действий Windows hello.

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

Окно tooanother действия можно перейти, щелкнув его в представлении календаря hello вверху hello. Можно также используйте кнопки со стрелками влево, Стрелка/вправо hello в windows действие hello top toosee из hello предыдущей недели или hello следующей неделе.

Можно использовать кнопки панели инструментов hello в окно приветствия нижней панели toorerun hello действия или обновить информацию о hello hello панели.

### <a name="script"></a>Скрипт
Можно использовать hello **сценарий** hello tooview вкладка Определение JSON hello выбранных сущностей фабрики данных (связанной службы, набор данных или конвейера).

![Вкладка "Скрипт"](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a>Использование системных представлений
Hello управление и мониторинг приложений включает в себя готовые системные представления (**последние действия windows**, **сбой действия windows**, **выполняющееся действие windows**), Разрешить windows tooview последних/сбой или выполняющееся действие для фабрики данных.

Переключение toohello **представления мониторинга** вкладке слева hello, щелкнув его.

![Вкладка "Представления мониторинга"](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

В настоящее время поддерживаются три системных представления. Выберите параметр toosee Недавние действия windows, сбой операции windows или windows выполняющееся действие в список действий Windows hello (внизу hello hello средней панели).

При выборе hello **последние действия windows** параметр, вы видите все недавние действия windows в порядке убывания hello **время последней попытки**.

Можно использовать hello **сбой действия windows** просмотра windows toosee не удалось выполнить действие в списке hello. Выберите окно отмененное действие в hello список toosee подробные сведения о нем в hello **свойства** окна или hello **действия окно обозревателя**. Можно также загрузить журналы для завершившегося ошибкой окна действия.

## <a name="sort-and-filter-activity-windows"></a>Сортировка и фильтрация окон действий
Изменение hello **время начала** и **время окончания** параметры в панели toofilter действия windows hello команд. После изменения hello время начала и время окончания выберите hello кнопку Далее toohello окончания времени toorefresh hello окон действий списка.

![Время начала и окончания](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> В настоящее время все значения времени приведены в формате UTC в приложение hello наблюдения и управления.
>
>

В hello **список действий Windows**, щелкните имя столбца hello (например: состояние).

![Меню столбца списка "Activity Windows" (Окна действий)](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

Можно сделать hello следующее:

* отсортировать по возрастанию;
* отсортировать по убыванию;
* отфильтровать по одному или нескольким значениям ("Готово", "Ожидание" и т. д.).

При указании фильтр на столбце отображается кнопка фильтра hello включен для этого столбца, который указывает, что hello значения в столбце hello отфильтрованные значения.

![Применить фильтр к столбцу списка действий Windows hello](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

Можно использовать hello и те же фильтры tooclear во всплывающем окне. tooclear все фильтры для списка действий Windows hello, нажмите кнопку Очистить фильтр hello hello панели команд.

![Очистить все фильтры для списка действий Windows hello](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a>Выполнение пакетных действий
### <a name="rerun-selected-activity-windows"></a>Повторное выполнение выбранных окон действий
Выберите окно действия hello вниз для hello первой кнопке панели команд и выберите **повторить** / **повторно с проверенными в конвейере**. При выборе hello **повторно с проверенными в конвейере** параметр, он перезапустит также все окна восходящего действия.
    ![Повторное выполнение окна действия](./media/data-factory-monitor-manage-app/ReRunSlice.png)

Также можно выбрать несколько окон действий в списке hello и снова запустите их на hello то же время. Может потребоваться toofilter действия windows на основе состояния hello (например: **сбой**)--и повторно запустите программу windows hello не удалось выполнить действия после исправления hello проблему, которая вызывает toofail windows hello действия. См. в следующем разделе Дополнительные сведения о фильтрации windows действия в списке hello hello.  

### <a name="pauseresume-multiple-pipelines"></a>Приостановка и возобновление нескольких конвейеров
Multiselect конвейеры два или более можно с помощью клавиши Ctrl hello. Можно использовать кнопки панели команд hello (который выделены hello красный прямоугольник в hello после изображения) toopause или возобновления их.

![Приостановить или возобновить на панели команд, hello](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a>Создание оповещений
Hello **оповещения** страница позволяет создать оповещение и Просмотр/изменение/Удаление оповещения. Можно также включить или отключить оповещение. toosee Здравствуйте страницы оповещения, щелкните hello **оповещения** вкладки.

![Вкладка "Оповещения"](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="toocreate-an-alert"></a>toocreate оповещение
1. Нажмите кнопку **добавить оповещение** tooadd оповещение. Вы видите hello **сведения** страницы.

    ![Создание оповещений — страница "Сведения"](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. Укажите hello **имя** и **описание** hello предупреждение, а затем щелкните **Далее**. Вы увидите hello **фильтры** страницы.

    ![Создание оповещений — страница "Фильтры"](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. Выберите hello **событий**, **состояние**, и **подсостояния** (необязательно), которые должны toocreate служба фабрики данных для предупреждения и нажмите кнопку **Далее**. Вы увидите hello **получателей** страницы.

    ![Создание оповещений — страница "Получатели"](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. Выберите hello **по электронной почте администраторам подписки** параметра или ввести **дополнительная электронная почта администратора**и нажмите кнопку **Готово**. Вы увидите предупреждение hello в списке hello.

    ![Список "Оповещения"](./media/data-factory-monitor-manage-app/AlertsList.png)

В списке оповещений hello кнопки hello, которые связаны с hello предупреждения tooedit/delete/включить или отключить предупреждение.

### <a name="eventstatussubstatus"></a>Событие, состояние и подсостояние
Hello следующей таблице приведен список hello доступные события и состояния (и Дополнительные сведения).

| Имя события | Состояние | Подсостояние |
| --- | --- | --- |
| Выполнение действия начато |Started |Запуск |
| Выполнение действия завершено |Успешно |Успешно |
| Выполнение действия завершено |Сбой |Неудачное выделение ресурсов<br/><br/>Сбой при выполнении<br/><br/>Timed Out<br/><br/>Failed Validation<br/><br/>Abandoned |
| Создание кластера HDI по запросу начато |Started |-|
| Кластер HDI по запросу успешно создан |Успешно |-|
| Кластер HDI по запросу удален |Успешно |-|

### <a name="tooedit-delete-or-disable-an-alert"></a>tooedit, удалить или отключить оповещения

Используйте следующие tooedit кнопок (выделено красным цветом), delete или отключить оповещения hello.

![Кнопки оповещений](./media/data-factory-monitor-manage-app/AlertButtons.png)
