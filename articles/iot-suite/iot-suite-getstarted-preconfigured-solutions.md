---
title: "aaaGet к работе с предварительно настроенных решений | Документы Microsoft"
description: "Выполните этот учебник toolearn как toodeploy набор IoT Azure предварительно настроенных решений."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 6ab38d1a-b564-469e-8a87-e597aa51d0f7
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: a7f46023d26b08de2e8ed48c34c5066a43e3fa38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-preconfigured-solutions"></a>Приступая к работе с hello предварительно настроенных решений

Azure IoT Suite [предварительно настроенных решений] [ lnk-preconfigured-solutions] объединить несколько конца в конец решений toodeliver Azure IoT служб, реализующие общих деловых сценариях IoT. Hello *удаленный мониторинг* предварительно настроенных решений подключается мониторы tooand устройств. Можно использовать hello tooanalyze решения hello поток данных с устройств и результатов бизнеса tooimprove, делая процессы отвечать автоматически toothat поток данных.

Этот учебник показывает, как удаленный мониторинг tooprovision hello предварительно настроенных решений. Он также поможет выполнить основные функции hello hello предварительно настроенных решений. Многие из этих средств можно получить из решения hello *мониторинга* , которая выполняет развертывание в рамках hello предварительно настроенных решений:

![Панель мониторинга предварительно настроенного решения для удаленного мониторинга][img-dashboard]

toocomplete этого учебника требуется Активная подписка Azure.

> [!NOTE]
> Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk_free_trial].

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a>Обзор сценария

При развертывании удаленного мониторинга предварительно настроенных решений hello заполнена ресурсов, позволяющих toostep через обычный сценарий удаленного мониторинга. В этом сценарии несколько решений toohello подключенных устройств сообщаете температуры непредвиденные значения. Hello следующих разделах показано, как для:

* Определение устройств hello температуры непредвиденные значения.
* Настройка этих устройств toosend более подробные данные телеметрии.
* Hello проблему можно устраните путем обновления встроенного по hello на этих устройствах.
* Проверка действия разрешения проблемы hello.

Ключевой особенностью этого сценария заключается в, можно выполнить все эти действия удаленно с панели мониторинга hello решения. Не обязательно toohello физического доступа к устройствам.

## <a name="view-hello-solution-dashboard"></a>Представление hello решений мониторинга

панель мониторинга Hello решение позволяет toomanage hello развертывания решения. Например, можно просматривать данные телеметрии, добавлять устройства и настраивать правила.

1. После подготовки hello завершения и указывает hello плитки для предварительно настроенного решения **готовности**, выберите **запуска** tooopen на новой вкладке портал удаленного мониторинга решения.

    ![Запустите hello предварительно настроенных решений][img-launch-solution]

1. По умолчанию hello решение портала отображает hello *мониторинга*. Можно перемещаться tooother области портала hello решения, с помощью меню hello hello левой стороны страницы приветствия.

    ![Панель мониторинга предварительно настроенного решения для удаленного мониторинга][img-menu]

панель мониторинга Hello отображает hello следующую информацию:

* Карта, отображающая hello расположение каждого устройства подключены toohello решения. При первом запуске hello решение, есть 25 имитации устройства. Hello устройств, имитация реализованы в виде веб-заданий Azure и hello решение использует hello Bing Maps API tooplot сведения на карте hello. В разделе hello [часто задаваемые вопросы о] [ lnk-faq] toolearn как toomake hello динамической карты.
* На панели **Журнал телеметрии** отображаются графики влажности и температуры с выбранного устройства в близком к реальному времени, а также сводные данные, например максимальное, минимальное и среднее значения влажности.
* На панели **Журнал оповещений** отображаются последние события, когда значение телеметрии превышает пороговое значение. Можно определить собственные сигналы в примерах toohello сложения, созданные hello предварительно настроенных решений.
* В области **Задания** отображаются сведения о запланированных заданиях. Вы можете запланировать собственные задания на странице **заданий управления**.

## <a name="view-alarms"></a>Просмотр оповещений

«Журнал» звуковых сигналов Hello показано выше, чем ожидаемое телеметрии значения Подотчетные пять устройства.

![Журнал TODO сигнала на панели мониторинга решения hello][img-alarms]

> [!NOTE]
> Эти предупреждения создаются правилом, включенный в hello предварительно настроенных решений. Это правило создает оповещение, когда значение температуры hello, отправляемый устройством превышает 60. Можно определить собственные правила и действия, выбрав [правила](#add-a-rule) и [действия](#add-an-action) в левом меню hello.

## <a name="view-devices"></a>Просмотр устройств

Hello *устройств* список содержит все устройства, зарегистрированные hello в решении hello. Из списка устройств hello можно просматривать и изменять метаданные устройства добавьте или удалите устройства и вызова методов на устройствах. Можно фильтровать и сортировать список устройств в списке устройств hello hello. Можно также настроить hello столбцов, показанных в списке устройств hello.

1. Выберите **устройств** список устройств hello tooshow для этого решения.

   ![Просмотр списка устройств hello hello решение портала][img-devicelist]

1. Список устройств Hello первоначально показывает 25 имитации устройства, созданные по подготовке hello. Можно добавить решение toohello дополнительных имитацию и физических устройств.

1. сведения о hello tooview устройства, выберите устройство в список устройств hello.

   ![Просмотр сведений об устройстве hello hello решение портала][img-devicedetails]

Hello **сведений об устройстве** панель содержит шесть разделы:

* Коллекция ссылок, включения вы toocustomize hello значок устройства, отключите устройство hello, добавить правило, вызвать метод или отправить команду. Сведения о сравнении команд (сообщения из устройства в облако) и методов (прямые методы) см. в [руководстве о связи между облаком и устройством][lnk-c2d-guidance].
* Hello **устройства двойных - теги** раздел позволяет tooedit значения тега для hello устройства. Можно отобразить значения тега в список устройств hello и использовать список устройств hello toofilter значения тега.
* Hello **устройства двойных - требуемого свойства** раздел позволяет tooset свойство значения toobe отправлено toohello устройства.
* Hello **устройства двойных - сообщил свойства** разделе показаны значения свойств, отправляемых с устройства hello.
* Hello **свойства устройства** разделе отображаются сведения из реестра удостоверение hello, например hello устройства идентификатор и проверки подлинности ключи.
* Hello **последних заданий** разделе приводятся сведения о все задания, которые недавно предназначены этого устройства.

## <a name="filter-hello-device-list"></a>Фильтровать список устройств hello

Можно использовать только те устройства, которые отправляют значения температуры Непредвиденная toodisplay фильтра. удаленный мониторинг предварительно настроенных решений Hello включает hello **неработоспособности устройства** фильтрации tooshow устройствами с помощью температуры среднее значение, большее, чем 60. Также можно [создать собственные фильтры](#add-a-filter).

1. Выберите **открыть сохраненный фильтр** toodisplay список доступных фильтров. Выберите **неработоспособности устройства** tooapply hello фильтра:

    ![Отображение списка фильтров hello][img-unhealthy-filter]

1. Hello устройство теперь перечислены только устройства с температуры среднее значение больше 60.

    ![Просмотр списка отфильтрованных устройств hello отображает неработоспособен][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a>Обновление требуемых свойств

Вы определили набор устройств, которые необходимо исправить. Однако принято hello периодичность данных составляет 15 секунд недостаточно для очистки диагностики проблемы hello. Изменение hello телеметрии частоты toofive секунд tooprovide вам toobetter точек дополнительные данные диагностики проблемы hello. Это изменение конфигурации tooyour удаленных устройств можно передать через портал hello решения. Необходимо будет внести изменение hello один раз, оценивать влияние hello и выполнить действия с hello результаты.

Выполните эти шаги toorun задание, которое изменяет hello **TelemetryInterval** требуемого свойства для затронутых hello устройств. Когда hello устройства будут получать новый hello **TelemetryInterval** значения свойства, они изменяют свои данные телеметрии toosend конфигурации каждые пять секунд, а не через каждые 15 секунд:

1. Хотя список hello неработоспособное устройств отображаются в списке устройств hello, **планировщик заданий**, затем **изменить двойных устройства**.

1. Вызов задания hello **интервала изменений телеметрии**.

1. Измените значение hello hello **нужное свойство** имя **требуемой. Config.TelemetryInterval** toofive секунд.

1. Выберите **Расписание**.

    ![Изменить свойства toofive hello TelemetryInterval секунд][img-change-interval]

1. Отследить ход выполнения hello hello задания на hello **управления заданиями** портале hello.

> [!NOTE]
> Toochange значению свойства для отдельных устройств, используйте hello **нужными свойствами** раздела hello **сведений об устройстве** панель вместо запуска задания.

Это задание задает значение hello hello **TelemetryInterval** требуемого свойства в двойных hello устройства для всех hello выбранных фильтром hello устройств. Hello устройств это значение получалось из устройства двойных hello и обновите их поведения. Когда устройство получает и обрабатывает нужные свойства из двойных устройства, его свойству hello соответствующего значение по отчету.

## <a name="invoke-methods"></a>Вызов методов

Во время выполнения задания hello замечаете в списке hello неработоспособное устройств, все эти устройства микропрограмма старого (меньше, чем версии 1.6) версии.

![Представление hello сообщила о версии встроенного по для устройств неработоспособное hello][img-old-firmware]

Эта версия встроенного по может быть hello первопричину hello Непредвиденная значения температуры, поскольку известно, что другие работоспособных устройств были недавно обновленного tooversion 2.0. Можно использовать встроенные hello **старые встроенного по устройства** фильтрации tooidentify все устройства со старыми версиями встроенного по. Из портала hello можно удаленно обновить все устройства hello, по-прежнему под управлением старых версий встроенного по:

1. Выберите **открыть сохраненный фильтр** toodisplay список доступных фильтров. Выберите **старые встроенного по устройства** tooapply hello фильтра:

    ![Отображение списка фильтров hello][img-old-filter]

1. Список устройств Hello теперь отображаются только устройства с помощью старых версий встроенного по. Этот список включает пять устройств hello, определенных hello **неработоспособности устройства** фильтр и трех дополнительных устройств:

    ![Просмотр списка отфильтрованных устройств hello отображаются старые устройства][img-filtered-old-list]

1. Выберите **Планировщик заданий**, а затем — **Вызвать метод**.

1. Задать **имя задания** слишком**tooversion обновление встроенного по 2.0**.

1. Выберите **InitiateFirmwareUpdate** как hello **метод**.

1. Набор hello **FwPackageUri** параметр слишком**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.

1. Выберите **Расписание**. по умолчанию Hello сейчас для задания toorun hello.

    ![Создание задания tooupdate hello встроенное по устройств выбран hello][img-method-update]

> [!NOTE]
> Tooinvoke метод отдельные устройства, выберите **методы** в hello **сведений об устройстве** панель вместо запуска задания.

Это задание вызывает hello **InitiateFirmwareUpdate** прямой метод на всех устройствах hello выбранных фильтром hello. Устройства ответить немедленно tooIoT концентратора и асинхронной инициации процесса обновления встроенного по hello. устройства Hello предоставляют сведения о состоянии процесса обновления встроенного по hello через значения свойств отчета, как показано на следующих снимках экрана приветствия. Выберите hello **обновление** значок tooupdate hello сведения в списки устройств и задание hello:

![Список заданий, показывающий выполнение списка обновления встроенного по hello][img-update-1]
![список устройств, показывающий состояние обновления встроенного по][img-update-2]
![задания списка Отображение hello встроенного по обновления списка завершения][img-update-3]

> [!NOTE]
> В рабочей среде можно запланировать toorun задания во время заданного периода.

## <a name="scenario-review"></a>Разбор сценария

В этом сценарии определить потенциальные проблемы с некоторыми из удаленного устройства с помощью журнала hello звуковых сигналов на панель мониторинга hello и фильтр. Вы затем фильтра используется hello и tooremotely задания настройки устройств tooprovide hello дополнительные toohelp сведения диагностики проблемы hello. Наконец вы использовали фильтр и задания обслуживания tooschedule на устройствах затронуты hello. Если возвращается toohello панели мониторинга можно проверить, что больше не существует любой сигналы поступают от устройств в решении. Можно использовать фильтр актуален tooverify, hello встроенного по на всех устройствах hello в решении и больше нет неработоспособности устройства:

![Фильтр, показывающий, что все устройства имеют актуальную версию встроенного ПО][img-updated]

![Фильтр, показывающий, что все устройства работоспособны][img-healthy]

## <a name="other-features"></a>Другие возможности

Hello следующих разделах описаны некоторые дополнительные функции hello удаленное наблюдение предварительно настроенного решения, описанные в предыдущем сценарии hello.

### <a name="customize-columns"></a>Настройка столбцов

Можно настроить hello сведения отображаются в списке устройств hello, выбрав **редактор столбец**. Кроме того, можно добавлять и удалять столбцы, отображающие полученные значения тегов и свойств, а также изменять порядок столбцов и переименовывать их.

   ![Список столбцов редактор ion hello устройства][img-columneditor]

### <a name="customize-hello-device-icon"></a>Настройка значок устройства hello

Вы можете настроить hello устройства значка, отображаемого в списке устройств hello из hello **сведений об устройстве** панели следующим образом:

1. Выберите значок tooopen hello карандаша hello **редактирование изображения** панель для устройства:

   ![Открытие редактора изображений устройств][img-startimageedit]

1. Отправить новый образ или использовать один из существующих образов hello и выберите **Сохранить**:

   ![Редактор изменения изображений устройства][img-imageedit]

1. Hello образа, выбранного теперь отображаются в hello **значок** столбца для hello устройства.

> [!NOTE]
> Hello изображение хранится в хранилище больших двоичных объектов. Тег в двойных устройства hello содержит изображение toohello ссылку в хранилище больших двоичных объектов.

### <a name="add-a-device"></a>Добавление устройства

При развертывании решения hello предварительно настроен, Автоматическая подготовка 25 образец устройств, которые отображаются в списке устройств hello. Это *виртуальные устройства*, работающие в веб-задании Azure. Устройств, имитация упростить для вас tooexperiment hello предварительно настроенное решение без hello необходимость toodeploy реальных физических устройств. Если вы хотите tooconnect решения toohello реального устройства, см. раздел hello [подключения вашего устройства toohello удаленное наблюдение предварительно настроенных решений] [ lnk-connect-rm] учебника.

Hello следующие шаги показывают, как tooadd имитацию toohello устройствами:

1. Перейдите назад toohello список устройств.

1. Выберите tooadd устройством, **+ добавить устройство** в левом нижнем углу hello.

   ![Добавление решения toohello предварительно настроенных устройств][img-adddevice]

1. Выберите **добавить новое** на hello **имитируемые устройства** плитки.

   ![Настройка сведений о новом устройстве на панели мониторинга][img-addnew]

   В добавление toocreating имитацию новое устройство, можно также добавить физическое устройство при выборе toocreate **пользовательских устройств**. toolearn Дополнительные сведения о подключении решения toohello физических устройств, в разделе [подключиться к toohello устройств IoT Suite удаленное наблюдение предварительно настроенных решений][lnk-connect-rm].

1. Выберите пункт **Let me define my own Device ID** (Задать идентификатор устройства самостоятельно) и укажите имя уникального идентификатора устройства: **mydevice_01**.

1. Выберите **Создать**.

   ![Сохранение нового устройства][img-definedevice]

1. На шаге 3 **добавить имитированное устройство**, выберите **сделать** список устройств toohello tooreturn.

1. Можно просматривать устройства **под управлением** в список устройств hello.

    ![Просмотр нового устройства в списке устройств][img-runningnew]

1. Можно также просмотреть hello смоделированные данные телеметрии с нового устройства на панели мониторинга hello:

    ![Просмотр данных телеметрии с нового устройства][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a>Отключение и удаление устройства

Можно отключить устройство, а после отключения его можно удалить.

![Отключение и удаление устройства][img-disable]

### <a name="add-a-rule"></a>Добавление правила

Нет правил для hello новое устройство только что добавлен. В этом разделе добавьте правило, которое запускает оповещение, когда температуры hello сообщили hello нового устройства превышает 47 градусов. Прежде чем начать, обратите внимание, журнал телеметрии hello hello новое устройство, на панели мониторинга hello показывают температура устройства hello никогда не превышает 45 градусов.

1. Перейдите назад toohello список устройств.

1. tooadd правило для hello устройства, выберите новое устройство в hello **список устройств**, а затем выберите **добавить правило**.

1. Создать правило, которое использует **температуры** как поле данных hello и использует **AlarmTemp** как hello выходных данных, если температуры hello превышает 47 градусов:

    ![Добавление правила устройства][img-adddevicerule]

1. Выберите изменения, toosave **сохранение и Просмотр правил**.

1. Выберите **команды** в области сведений hello устройства для hello новое устройство.

    ![Добавление правила устройства][img-adddevicerule2]

1. Выберите **ChangeSetPointTemp** из списка команд hello и набор **SetPointTemp** too45. Выберите **Отправить команду**.

    ![Добавление правила устройства][img-adddevicerule3]

1. Перейдите назад toohello панели мониторинга. Через некоторое время, вы увидите новую запись в hello **журнал сигнала** панели при температуры hello сообщили новое устройство превышает пороговое значение степени 47 hello:

    ![Добавление правила устройства][img-adddevicerule4]

1. Можно просмотреть и изменить все правила на hello **правила** hello панели мониторинга:

    ![Список правил устройства][img-rules]

1. Можно просмотреть и изменить все hello действия, которые могут быть предприняты в правиле tooa ответа на hello **действия** hello панели мониторинга:

    ![Список действий с устройством][img-actions]

> [!NOTE]
> Это toodefine возможные действия, которые можно отправить сообщение электронной почты или SMS в ответ tooa правило или интегрировать бизнес-системе с помощью [приложения логики][lnk-logic-apps]. Дополнительные сведения см. в разделе hello [tooyour подключения приложения логики Azure IoT Suite удаленный мониторинг предварительно настроенное решение][lnk-logicapptutorial].

### <a name="manage-filters"></a>Управление фильтрами

В списке устройств hello создания, сохранения и перезагрузить toodisplay фильтры список концентратора tooyour подключенных устройств. toocreate фильтра:

1. Выберите значок фильтра hello редактирования над списком hello устройств:

    ![Привет открыть редактор фильтров][img-editfiltericon]

1. В hello **редактор фильтров**, добавьте hello поля, операторы и список значений toofilter hello устройств. Можно добавить несколько toorefine предложения фильтра. Выберите **фильтра** tooapply hello фильтра:

    ![Создание фильтра][img-filtereditor]

1. В этом примере hello список фильтруется по производителю и номер модели:

    ![Фильтрованный список][img-filterelist]

1. toosave фильтра с пользовательским именем выберите hello **сохранение** значок:

    ![Сохранение фильтра][img-savefilter]

1. tooreapply фильтр, сохраненный ранее, выберите hello **открыть сохраненный фильтр** значок:

    ![Открытие фильтра][img-openfilter]

Вы можете создавать фильтры на основе идентификатора устройства, его состояния, требуемых или переданных свойств и тегов. Добавление устройства tooa настраиваемые теги в hello **теги** раздел hello **сведений об устройстве** панели или запустить теги tooupdate заданий на нескольких устройствах.

> [!NOTE]
> В hello **редактор фильтров**, можно использовать hello **расширенное представление** текст запроса hello tooedit напрямую.

### <a name="commands"></a>Команды

Из hello **сведений об устройстве** панель, можно отправлять команды toohello устройства. При первом запуске устройство отправляет сведения о hello команд, что он поддерживает toohello решения. Обсуждение hello различия между командами и методов см. в разделе [параметры облака на устройство Azure IoT Hub][lnk-c2d-guidance].

1. Выберите **команды** в hello **сведений об устройстве** панель для выбранного устройства hello:

   ![Команды устройств на панели мониторинга][img-devicecommands]

1. Выберите **PingDevice** из списка команд hello.

1. Щелкните **Отправить команду**.

1. Вы увидите состояние hello hello команды в журнале команды hello.

   ![Состояние команды на панели мониторинга][img-pingcommand]

решение Hello отслеживает состояние hello каждой команды, которую он отправляет. Изначально hello результатом является **ожидающие**. Если устройство hello сообщает, что она выполнена команда hello, hello результирующий набор слишком**успешно**.

## <a name="behind-hello-scenes"></a>Фоновом hello

При развертывании предварительно настроенных решений hello процесс развертывания создает несколько ресурсов в hello Azure подписку, которую вы выбрали. Эти ресурсы можно просмотреть в hello Azure [портала][lnk-portal]. процесс развертывания Hello создает **группы ресурсов** с именем, основываясь на имени hello, выберите для предварительно настроенного решения:

![Предварительно настроенных решений в hello портал Azure][img-portal]

Параметры hello каждый ресурс можно просмотреть, выбрав его в список ресурсов в группе ресурсов hello hello.

Также можно просмотреть исходный код hello hello предварительно настроенных решений. Hello удаленное наблюдение предварительно настроенных решений исходный код находится в hello [azure iot удаленного мониторинга] [ lnk-rmgithub] репозитории GitHub:

* Hello **DeviceAdministration** папка содержит hello исходный код для мониторинга "hello".
* Hello **симулятор** папка содержит hello исходного кода для имитации устройства hello.
* Hello **EventProcessor** папка содержит hello исходного кода для серверной части процесса hello, который обрабатывает входящие данные телеметрии hello.

После завершения, можно удалить hello предварительно настроенное решение из подписки Azure на hello [azureiotsuite.com] [ lnk-azureiotsuite] сайта. Этот сайт обеспечивает delete tooeasily Здравствуйте, все ресурсы, которые были подготовлены при создании hello предварительно настроенных решений.

> [!NOTE]
> toohello предварительно настроенных решений, связанных с tooensure, удалите весь код, удалите его на hello [azureiotsuite.com] [ lnk-azureiotsuite] сайта, а также не удаляйте группу ресурсов hello hello портала.

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы развернули предварительно настроенное рабочее решение, можно перейти, Приступая к работе с IoT Suite, считывая hello в следующих статьях:

* [Пошаговое руководство по работе с настроенным решением для удаленного мониторинга][lnk-rm-walkthrough]
* [Подключиться с вашего устройства toohello удаленное наблюдение предварительно настроенных решений][lnk-connect-rm]
* [Разрешения на сайт azureiotsuite.com hello][lnk-permissions]

[img-launch-solution]: media/iot-suite-getstarted-preconfigured-solutions/launch.png
[img-dashboard]: media/iot-suite-getstarted-preconfigured-solutions/dashboard.png
[img-menu]: media/iot-suite-getstarted-preconfigured-solutions/menu.png
[img-devicelist]: media/iot-suite-getstarted-preconfigured-solutions/devicelist.png
[img-alarms]: media/iot-suite-getstarted-preconfigured-solutions/alarms.png
[img-devicedetails]: media/iot-suite-getstarted-preconfigured-solutions/devicedetails.png
[img-devicecommands]: media/iot-suite-getstarted-preconfigured-solutions/devicecommands.png
[img-pingcommand]: media/iot-suite-getstarted-preconfigured-solutions/pingcommand.png
[img-adddevice]: media/iot-suite-getstarted-preconfigured-solutions/adddevice.png
[img-addnew]: media/iot-suite-getstarted-preconfigured-solutions/addnew.png
[img-definedevice]: media/iot-suite-getstarted-preconfigured-solutions/definedevice.png
[img-runningnew]: media/iot-suite-getstarted-preconfigured-solutions/runningnew.png
[img-runningnew-2]: media/iot-suite-getstarted-preconfigured-solutions/runningnew2.png
[img-rules]: media/iot-suite-getstarted-preconfigured-solutions/rules.png
[img-adddevicerule]: media/iot-suite-getstarted-preconfigured-solutions/addrule.png
[img-adddevicerule2]: media/iot-suite-getstarted-preconfigured-solutions/addrule2.png
[img-adddevicerule3]: media/iot-suite-getstarted-preconfigured-solutions/addrule3.png
[img-adddevicerule4]: media/iot-suite-getstarted-preconfigured-solutions/addrule4.png
[img-actions]: media/iot-suite-getstarted-preconfigured-solutions/actions.png
[img-portal]: media/iot-suite-getstarted-preconfigured-solutions/portal.png
[img-disable]: media/iot-suite-getstarted-preconfigured-solutions/solutionportal_08.png
[img-columneditor]: media/iot-suite-getstarted-preconfigured-solutions/columneditor.png
[img-startimageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit1.png
[img-imageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit2.png
[img-editfiltericon]: media/iot-suite-getstarted-preconfigured-solutions/editfiltericon.png
[img-filtereditor]: media/iot-suite-getstarted-preconfigured-solutions/filtereditor.png
[img-filterelist]: media/iot-suite-getstarted-preconfigured-solutions/filteredlist.png
[img-savefilter]: media/iot-suite-getstarted-preconfigured-solutions/savefilter.png
[img-openfilter]:  media/iot-suite-getstarted-preconfigured-solutions/openfilter.png
[img-unhealthy-filter]: media/iot-suite-getstarted-preconfigured-solutions/unhealthyfilter.png
[img-filtered-unhealthy-list]: media/iot-suite-getstarted-preconfigured-solutions/unhealthylist.png
[img-change-interval]: media/iot-suite-getstarted-preconfigured-solutions/changeinterval.png
[img-old-firmware]: media/iot-suite-getstarted-preconfigured-solutions/noticeold.png
[img-old-filter]: media/iot-suite-getstarted-preconfigured-solutions/oldfilter.png
[img-filtered-old-list]: media/iot-suite-getstarted-preconfigured-solutions/oldlist.png
[img-method-update]: media/iot-suite-getstarted-preconfigured-solutions/methodupdate.png
[img-update-1]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate1.png
[img-update-2]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate2.png
[img-update-3]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate3.png
[img-updated]: media/iot-suite-getstarted-preconfigured-solutions/updated.png
[img-healthy]: media/iot-suite-getstarted-preconfigured-solutions/healthy.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-logic-apps]: https://azure.microsoft.com/documentation/services/app-service/logic/
[lnk-portal]: http://portal.azure.com/
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-logicapptutorial]: iot-suite-logic-apps-tutorial.md
[lnk-rm-walkthrough]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-faq]: iot-suite-faq.md