---
title: "aaaBuild решения IoT с помощью Stream Analytics | Документы Microsoft"
description: "Приступая к работе учебника для решения Stream Analytics IoT сценарий пропускного пункта hello"
keywords: "Решение IOT, функции окна"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: e37fc5b56c4ffc4a2d7b820afe0c17631e577ea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-iot-solution-by-using-stream-analytics"></a>Создание решения IoT с помощью Stream Analytics
## <a name="introduction"></a>Введение
В этом учебнике вы узнаете, как toouse Azure Stream Analytics tooget в режиме реального времени аналитики из данных. Разработчикам легко объединять потоки данных, таких как щелчок потоки, журналы и события, вызываемые устройства, с помощью записей журнала или ссылку данных tooderive бизнес-аналитики. Как служба вычисления потока полностью управляемыми, в режиме реального времени, размещенном в Microsoft Azure Azure Stream Analytics предоставляет гибкость встроенными функциями, небольших задержек и масштабируемость tooget подготовки к работе в минутах.

После работы с этим учебником вы сможете выполнить следующие задачи:

* Ознакомьтесь с портала Azure Stream Analytics hello.
* Настроить и развернуть задание потоковой передачи.
* Сформулировать реальных проблем и их решения с помощью языка запросов Stream Analytics hello.
* Уверенно разрабатывать решения потоковой передачи для клиентов с помощью Stream Analytics.
* Используйте hello мониторинга и ведения журнала tootroubleshoot проблемы качества.

## <a name="prerequisites"></a>Предварительные требования
Вам будет необходимо hello следующие необходимые условия toocomplete этого учебника:

* Hello последнюю версию [Azure PowerShell](/powershell/azure/overview)
* Visual Studio 2017 г., 2015 г., или hello свободного [Visual Studio Community](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)
* [Подписка Azure](https://azure.microsoft.com/pricing/free-trial/)
* Права администратора на компьютере hello
* Время ожидания загрузки [TollApp.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) из центра загрузки Майкрософт hello
* Необязательно: Исходный код для генератора событий TollApp hello в [GitHub](https://aka.ms/azure-stream-analytics-toll-source)

## <a name="scenario-introduction-hello-toll"></a>Введение в сценарий "Hello, Toll!"
Станции сбора дорожной платы представляют собой распространенное явление. Можно встретить на многих скоростных, мосты и туннели между Здравствуй, мир!. Каждая станция имеет несколько пунктов сбора платы. В ручной стенды остановить toopay hello платный tooan помощника. В автоматических стенды датчика на основе каждого оплаты считывает RFID-карту, прикрепленную toohello ветровое стекло автомобиля, при проезде через кабинку hello. Это легко toovisualize hello проезд автомобилей через эти станции платный как поток событий, по которому интересные операции.

![Изображение автомобилей в пунктах сбора платы](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image1.jpg)

## <a name="incoming-data"></a>Входящие данные
В этом руководстве используется два потока данных. Датчики устанавливаются в hello вход и выход станций платный hello создания первого потока hello. Второй поток Hello — набора статических Уточняющий запрос, который имеет регистрационные данные машина.

### <a name="entry-data-stream"></a>Входной поток данных
поток данных Hello запись содержит сведения о автомобили вводе платный станции.

| ИД пункта сбора | Время въезда | LicensePlate | Состояние | Убедитесь, | Модель | Тип транспортного средства | Вес транспортного средства | Плата | Тег |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 |10.09.2014 12:01:00.000 |JNB 7001 |Нью-Йорк |Honda |CRV |1 |0 |7 | |
| 1 |10.09.2014 12:02:00.000 |YXZ 1001 |Нью-Йорк |Toyota |Camry |1 |0 |4. |123456789 |
| 3 |10.09.2014 12:02:00.000 |ABC 1004 |CT |Ford |Taurus |1 |0 |5 |456789123 |
| 2 |10.09.2014 12:03:00.000 |XYZ 1003 |CT |Toyota |Corolla |1 |0 |4. | |
| 1 |10.09.2014 12:03:00.000 |BNJ 1007 |Нью-Йорк |Honda |CRV |1 |0 |5 |789123456 |
| 2 |10.09.2014 12:05:00.000 |CDE 1007 |Нью-Джерси |Toyota |4x4 |1 |0 |6 |321987654 |

Вот краткое описание столбцов hello.

| столбец | Описание |
| --- | --- |
| ИД пункта сбора |Идентификатор Hello платный оплаты, который однозначно определяет оплаты дорожного сбора |
| Время въезда |Hello Дата и время записи hello vehicle toohello через кабинку в формате UTC |
| LicensePlate |Hello номерной автомобиля hello |
| Состояние |Штат в США |
| Убедитесь, |Hello производителя автомобиль hello |
| Модель |Номер модели Hello автомобиль hello |
| Тип транспортного средства |1 — для пассажирского транспорта, 2 — для коммерческого транспорта |
| Тип веса |Вес транспортного средства в тоннах. 0 — для пассажирского транспорта. |
| Плата |значение платный Hello в долларах США |
| Тег |Здравствуйте, e-Tag на автомобиль hello, который автоматизирует платежа; пустое, где было выполнено hello оплаты вручную |

### <a name="exit-data-stream"></a>Выходной поток данных
поток данных выхода Hello содержит сведения о автомобилей, оставляя станции платный hello.

| **ИД пункта сбора** | **Время выезда** | **LicensePlate** |
| --- | --- | --- |
| 1 |10.09.2014T12:03:00.0000000Z |JNB 7001 |
| 1 |10.09.2014T12:03:00.0000000Z |YXZ 1001 |
| 3 |10.09.2014T12:04:00.0000000Z |ABC 1004 |
| 2 |10.09.2014T12:07:00.0000000Z |XYZ 1003 |
| 1 |10.09.2014T12:08:00.0000000Z |BNJ 1007 |
| 2 |10.09.2014T12:07:00.0000000Z |CDE 1007 |

Вот краткое описание столбцов hello.

| столбец | Описание |
| --- | --- |
| ИД пункта сбора |Идентификатор Hello платный оплаты, который однозначно определяет оплаты дорожного сбора |
| Время выезда |Hello даты и времени выхода, hello автомобиля в кабинку сбора оплаты в формате UTC |
| LicensePlate |Hello номерной автомобиля hello |

### <a name="commercial-vehicle-registration-data"></a>Данные регистрации коммерческого транспортного средства
Hello учебнике используется статический моментальный снимок базы данных регистрации коммерческого транспорта.

| LicensePlate | ИД регистрации | Срок действия истек |
| --- | --- | --- |
| SVT 6023 |285429838 |1 |
| XLZ 3463 |362715656 |0 |
| BAC 1005 |876133137 |1 |
| RIV 8632 |992711956 |0 |
| SNY 7188 |592133890 |0 |
| ELH 9896 |678427724 |1 |

Вот краткое описание столбцов hello.

| столбец | Описание |
| --- | --- |
| LicensePlate |Hello номерной автомобиля hello |
| ИД регистрации |Идентификатор регистрации Hello vehicle |
| Срок действия истек |Здравствуйте состояния регистрации hello vehicle: 0, если средство регистрации активна, 1, если истек срок действия регистрации |

## <a name="set-up-hello-environment-for-azure-stream-analytics"></a>Настройка среды hello для Azure Stream Analytics
toocomplete этого учебника вам потребуется подписка Microsoft Azure. Мы предлагаем бесплатную пробную версию служб Microsoft Azure.

Если у вас нет учетной записи Azure, вы можете [получить бесплатную пробную версию](http://azure.microsoft.com/pricing/free-trial/).

> [!NOTE]
> toosign для использования бесплатной пробной версии, необходимо мобильное устройство, которое может принимать текстовые сообщения и действительной кредитной карты.
> 
> 

Убедитесь, что toofollow hello действия раздела hello «Очистки учетной записи Azure» в конце hello в этой статье, чтобы можно наиболее эффективно использовать hello Azure кредита.

## <a name="provision-azure-resources-required-for-hello-tutorial"></a>Подготовить Azure ресурсы, необходимые для работы с руководством hello
Этот учебник требует двух tooreceive концентраторов событий *запись* и *выхода* потоки данных. База данных SQL Azure выводит результаты hello заданий Stream Analytics hello. Для хранения справочных данных о регистрации транспортных средств используется служба хранилища Azure.

Можно использовать сценарий Setup.ps1 hello в папке TollApp hello на GitHub toocreate все необходимые ресурсы. Hello процент времени мы рекомендуем, запустите его. Если вы хотите toolearn Дополнительные сведения о как tooconfigure эти ресурсы в hello портал Azure, см. в приложении «Настройка учебника ресурсы на портале Azure» toohello.

Загрузить и сохранить их hello [TollApp](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) файлов и папок.

Откройте окно **Microsoft Azure PowerShell***от имени администратора*. Если вы еще не Azure PowerShell, следуйте инструкциям hello [Установка и настройка Azure PowerShell](/powershell/azure/overview) tooinstall его.

Поскольку Windows автоматически блокирует файлы .exe, .dll и .ps1, вам потребуется политика выполнения hello tooset перед запуском сценария hello. Убедитесь, что окно Azure PowerShell hello работает *с правами администратора*. Выполните команду **Set-ExecutionPolicy unrestricted**. При появлении запроса введите **Y**.

![Снимок экрана с командой Set-ExecutionPolicy unrestricted в окне Azure PowerShell](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image2.png)

Запустите **Get-ExecutionPolicy** toomake правильности команда hello.

![Снимок экрана с командой Get-ExecutionPolicy в окне Azure PowerShell](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image3.png)

Перейдите в каталог toohello, который имеет hello скрипты и приложения генератора.

![Снимок экрана «cd .\TollApp\TollApp» в окне Azure PowerShell hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image4.png)

Тип **.\\ Setup.ps1** tooset копирование учетной записи Azure, создать и настроить все необходимые ресурсы и запустить toogenerate события. сценарий Hello случайным образом забирает toocreate области ресурсов. tooexplicitly Укажите регион, можно передать hello **-расположение** параметра как hello в следующем примере:

**.\\Setup.ps1 -location "Central US"**

![Снимок экрана со страницей hello Azure вход](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image5.png)

скрипт Hello открывается hello **входа** страницы в Microsoft Azure. Введите свои учетные данные.

> [!NOTE]
> Если у вас есть доступ toomultiple подписки, можно hello задаваемые tooenter: требуется toouse в учебнике hello имя подписки.
> 
> 

Hello скрипт может занять несколько минут toorun. После его завершения hello вывод должен выглядеть так следующий снимок экрана приветствия.

![Снимок экрана скрипта hello в окне Azure PowerShell hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image6.PNG)

Также появится другое окно, которое аналогично toohello следующий снимок экрана. Это приложение отправляет события tooAzure концентраторов событий, являющийся учебника требуется toorun hello. Таким образом не остановить приложение hello и не закрывайте это окно до завершения работы с учебником hello.

![Снимок экрана "Отправка данных в концентратор событий"](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image7.png)

Вам необходимо будет toosee ресурсов на портале Azure теперь. Go слишком<https://portal.azure.com>и выполните вход с учетными данными. Обратите внимание, что в настоящее время некоторые функциональные возможности использует классический портал hello. Эти действия будут четко указаны.

### <a name="azure-event-hubs"></a>Концентраторы событий Azure
В hello портал Azure, щелкните **больше услуг** hello нижней области левой управления hello. Тип **концентраторов событий** в hello в поле и нажмите кнопку **концентраторов событий**. Будет запущен новый hello toodisplay окна браузера **SERVICE BUS** область hello **классический портал**. Вы видите hello концентратора событий, созданных hello Setup.ps1 сценария.

![Служебная шина](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image8.png)

Нажмите кнопку hello, который начинается с *tolldata*. Нажмите кнопку hello **КОНЦЕНТРАТОРОВ СОБЫТИЙ** вкладки. В этом пространстве имен вы увидите два созданных концентратора событий с именами *entry* и *exit*.

![Вкладки концентраторов событий в классическом портале hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image9.png)

### <a name="azure-storage-container"></a>Контейнер хранилища Azure
1. Вы можете вернуться toohello вкладка на портале tooAzure открыть браузер. Нажмите кнопку **ХРАНЕНИЯ** на hello слева от оператора hello Azure портала toosee hello хранилища Azure контейнер, который используется в учебнике hello.
   
    ![Пункт меню хранилища](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image11.png)
2. Нажмите кнопку hello, начинаться с *tolldata*. Нажмите кнопку hello **КОНТЕЙНЕРЫ** вкладку toosee hello создания контейнера.
   
    ![На вкладке контейнеры hello портал Azure](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image10.png)
3. Нажмите кнопку hello **tolldata** toosee hello контейнер загружен JSON-файл, содержащий данные машина регистрации.
   
    ![Снимок экрана файла registration.json hello в контейнере hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image12.png)

### <a name="azure-sql-database"></a>База данных SQL Azure
1. Вы можете вернуться toohello портал Azure на первой вкладке hello, который был открыт в браузере hello. Нажмите кнопку **баз данных SQL** на hello левая сторона hello Azure портала toosee hello SQL базы данных, которая будет использоваться в учебнике hello и нажмите кнопку **tolldatadb**.
   
    ![Снимок экрана: hello создана база данных SQL](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15.png)
2. Имя сервера hello копирования без номера порта hello (*servername*. database.windows.net, например).
    ![Снимок экрана: hello создания баз данных базы данных SQL Server](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15a.png)

## <a name="connect-toohello-database-from-visual-studio"></a>Подключение базы данных toohello из Visual Studio
Использование результатов запроса tooaccess Visual Studio в hello Выходная база данных.

Подключение базы данных SQL toohello (hello назначение) из Visual Studio:

1. Откройте Visual Studio и нажмите кнопку **средства** > **подключения tooDatabase**.
2. При запросе выберите **Microsoft SQL Server** в качестве источника данных.
   
    ![Диалоговое окно "Сменить источник данных"](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image16.png)
3. В hello **имя сервера** вставьте имя hello, скопированный в предыдущем разделе hello с hello портал Azure (то есть *servername*. database.windows.net).
4. Выберите **Использовать проверку подлинности SQL Server**.
5. Введите **tolladmin** в hello **имя пользователя** поля и **123toll!** в hello **пароль** поля.
6. Нажмите кнопку **выберите или введите имя базы данных**и выберите **TollDataDB** как hello базы данных.
   
    ![Диалоговое окно "Добавить подключение"](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image17.jpg)
7. Нажмите кнопку **ОК**.
8. Откройте обозреватель сервера.
   
    ![Обозреватель серверов](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image18.png)
9. См. в четырех таблиц в базе данных TollDataDB hello.
   
    ![Таблицы в базе данных TollDataDB hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image19.jpg)

## <a name="event-generator-tollapp-sample-project"></a>Генератор событий — пример проекта TollApp
Hello сценарий PowerShell автоматически запускает toosend события, используя пример приложения hello TollApp программы. Не нужно tooperform какие дополнительные шаги.

Тем не менее, если вы заинтересованы в детали реализации, можно найти hello TollApp приложения hello исходный код в GitHub [образцы/TollApp](https://aka.ms/azure-stream-analytics-toll-source).

![Снимок экрана примера кода в Visual Studio](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image20.png)

## <a name="create-a-stream-analytics-job"></a>Создание задания Stream Analytics
1. В hello портал Azure щелкните hello "плюс" в левом верхнем углу hello объекта toocreate страницы приветствия новое задание Stream Analytics. Выберите **Аналитика** и щелкните **Задание Stream Analytics**.
   
    ![Кнопка «Создать»](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image21.png)
2. Укажите имя задания, проверка подписки hello правильно, и затем создать новую группу ресурсов в hello же регионе, что hello хранилища концентратора событий (по умолчанию — центральных штатах юга США для hello скрипта).
3. Нажмите кнопку **toodashboard ПИН-код** и затем **создать** hello нижней части страницы приветствия.
   
    ![Параметр "Создать задание Stream Analytics"](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image22.png)

## <a name="define-input-sources"></a>Определение источников входных данных
1. Создает и открывает страницу приветствия задания Hello задания. Или можно щелкнуть hello analytics задание создано на панели мониторинга портала hello.

2. Нажмите кнопку hello **ВХОДОВ** вкладке toodefine hello исходных данных.
   
    ![Вкладка Hello входных данных](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image24.png)
3. Нажмите кнопку **Добавление входных данных**.
   
    ![Добавить вариант ввода Hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image25.png)
4. В качестве **Псевдонима входных данных** введите **EntryStream**.
5. В качестве типа источника данных выберите **Поток данных**.
6. Источник данных — **концентратор событий**.
7. **Пространство имен служебной шины** должно быть hello TollData один в hello раскрывающийся список.
8. **Имя концентратора событий** должно быть задано слишком**входа**.
9. **Имя политики концентратора событий*— **RootManageSharedAccessKey** (значение по умолчанию hello).
10. В поле **Формат сериализации событий** выберите **JSON**, а в поле **Кодировка** — **UTF8**.
   
    Настройки будут выглядеть следующим образом:
   
    ![Параметры концентратора событий](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image28.png)

10. Нажмите кнопку **создать** внизу hello toofinish hello hello страницы мастера.
    
    После создания потока записи hello будет следовать hello одного действия toocreate hello выхода потока. Быть убедиться, что значения tooenter на следующий снимок экрана приветствия.
    
    ![Параметры для потока выхода hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image31.png)
    
    Определены два потока входных данных:
    
    ![Определенные входные потоки в hello портал Azure](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image32.png)
    
    Далее вы добавите входных справочных данных для файла hello BLOB-объект, содержащий данные регистрации автомобиля.
11. Нажмите кнопку **добавить**, а затем следуйте hello же обработки потока входов hello, но выбрать **ССЫЛОЧНЫХ данных** вместо **потока данных** и hello **входных псевдонимов**  — **регистрации**.

12. Учетная запись хранения, имя которой начинается с **tolldata**. Имя контейнера Hello должно быть **tolldata**и hello **ШАБЛОН пути** должно быть **registration.json**. Имя файла должно быть введено **строчными буквами** (в нем учитывается регистр).
    
    ![Параметры хранилища BLOB-объектов](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image34.png)
13. Нажмите кнопку **создать** toofinish приветствия мастера.

Все входные данные определены.

## <a name="define-output"></a>Определение выходных данных
1. На панели обзора задания Stream Analytics hello выберите **ВЫХОДОВ**.
   
    ![Здравствуйте, вкладка «Вывод» и «Добавление выходных данных» параметр](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image37.png)
2. Щелкните **Добавить**.
3. Набор hello **Псевдоним выхода** too'output "и затем **приемника** слишком**базы данных SQL**.
3. Выберите имя сервера hello, который использовался в hello статьи «TooDatabase подключение из Visual Studio» hello. Имя базы данных Hello **TollDataDB**.
4. Введите **tolladmin** в hello **USERNAME** поля, **123toll!** в hello **пароль** поля, и **TollDataRefJoin** в hello **таблицы** поля.
   
    ![Параметры базы данных SQL](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image38.png)
5. Щелкните **Создать**.

## <a name="azure-stream-analytics-query"></a>Запрос в службе Azure Stream Analytics
Hello **ЗАПРОСА** вкладка содержит SQL-запроса, что преобразования hello входящих данных.

![Запрос добавлены toohello вкладка «запрос»](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image39.png)

Этот учебник попыток tooanswer несколько вопросов для бизнеса, связанных данных tootoll и конструкции Stream Analytics запросов, которые можно использовать в Azure Stream Analytics tooprovide соответствующий ответ.

Перед началом первого задание Stream Analytics, давайте рассмотрим несколько сценариев и синтаксис запросов hello.

## <a name="introduction-tooazure-stream-analytics-query-language"></a>Введение tooAzure языка запросов Stream Analytics
- - -
Предположим, что необходимые toocount hello число автомобилей, введите через кабинку. Поскольку это непрерывный поток событий, у вас есть toodefine» периода времени.» Изменим вопрос toobe hello, «сколько автомобилей введите через кабинку каждые три минуты?». Это часто ссылка tooas hello переворачивающееся count.

Давайте рассмотрим hello Azure Stream Analytics запрос, который отвечает на этот вопрос:

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count
    FROM EntryStream TIMESTAMP BY EntryTime
    GROUP BY TUMBLINGWINDOW(minute, 3), TollId

Как видите, Azure Stream Analytics использует язык запросов, подобного SQL и добавляет несколько расширений toospecify связанных со временем аспекты hello запроса.

Дополнительные сведения, узнайте, как [управление временем](https://msdn.microsoft.com/library/azure/mt582045.aspx) и [оконных](https://msdn.microsoft.com/library/azure/dn835019.aspx) конструкции, используемые в запросе hello с MSDN.

## <a name="testing-azure-stream-analytics-queries"></a>Тестирование запросов в службе Azure Stream Analytics
Теперь, когда вы написали первого запроса Azure Stream Analytics, это с помощью файла образцов данных, расположенные в папке TollApp в пути hello tootest времени:

**..\\TollApp\\TollApp\\Data**

Эта папка содержит hello следующие файлы:

* Entry.json
* Exit.json
* Registration.json

## <a name="question-1-number-of-vehicles-entering-a-toll-booth"></a>Вопрос 1. Количество автомобилей, въезжающих в пункт сбора платы
1. Откройте портал Azure hello и перейдите tooyour создать задание Azure Stream Analytics. Нажмите кнопку hello **ЗАПРОСА** и вставить запрос из предыдущего раздела hello.

2. toovalidate этот запрос на основе образцов данных, передаваемых данных hello в hello EntryStream ввода, нажав кнопку... hello символ и выбрав **отправьте демонстрационные данные из файла**.

    ![Снимок экрана файла Entry.json hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image41.png)
3. В области hello, которая отображается файла выберите hello (Entry.json) на локальном компьютере и нажмите кнопку **ОК**. Hello **тест** значок будет освещения и быть активным.
   
    ![Снимок экрана файла Entry.json hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image42.png)
3. Убедитесь, что hello выходных данных запроса hello — должным образом:
   
    ![Результаты теста hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image43.png)

## <a name="question-2-report-total-time-for-each-car-toopass-through-hello-toll-booth"></a>Вопрос 2: Общее время для каждой машины toopass через пункт оплаты дорожного сбора hello отчета
Hello среднее время, требуемое для toopass автомобиль через платный hello помогает tooassess hello эффективность процесса hello и качества hello.

Общее время toofind hello необходим toojoin hello EntryTime поток с потоком ExitTime hello. Потоки hello в столбцах TollId и LicencePlate будет присоединена. Hello **JOIN** оператор требует toospecify temporal свобода, описывающий приемлемое временное hello различие между hello входящих событий. Вы воспользуетесь **DATEDIFF** функции toospecify, что события должна быть не более 15 минут друг от друга. Также будут применяться hello **DATEDIFF** tooexit функции и операции раз фактическое время hello toocompute, которое он затрачивает автомобиля в hello номер телефона станции. Обратите внимание hello отличие использования hello **DATEDIFF** при использовании в **ВЫБЕРИТЕ** инструкции, а не **JOIN** условие.

    SELECT EntryStream.TollId, EntryStream.EntryTime, ExitStream.ExitTime, EntryStream.LicensePlate, DATEDIFF (minute , EntryStream.EntryTime, ExitStream.ExitTime) AS DurationInMinutes
    FROM EntryStream TIMESTAMP BY EntryTime
    JOIN ExitStream TIMESTAMP BY ExitTime
    ON (EntryStream.TollId= ExitStream.TollId AND EntryStream.LicensePlate = ExitStream.LicensePlate)
    AND DATEDIFF (minute, EntryStream, ExitStream ) BETWEEN 0 AND 15

1. tootest этот запрос hello запроса update на hello **ЗАПРОСА** для задания hello. Добавить файл теста hello для **ExitStream** так же, как **EntryStream** указано выше.
   
2. Нажмите **Проверить**.

3. Выберите hello флажок tootest hello запросов и представлений hello выходные данные:
   
    ![Выходные данные теста hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image45.png)

## <a name="question-3-report-all-commercial-vehicles-with-expired-registration"></a>Вопрос 3. Сообщать обо всех коммерческих транспортных средствах с истекшим сроком действия регистрации
Azure Stream Analytics можно использовать статические снимки данных toojoin с потоками временных данных. toodemonstrate эту возможность hello используйте следующий пример вопроса.

При регистрации коммерческого транспорта с компании hello его могут проходить через пункт оплаты дорожного сбора hello без остановки для проверки. Используется tooidentify таблицу подстановки регистрации коммерческого транспорта всех автомобилей, истек срок действия регистрации.

```
SELECT EntryStream.EntryTime, EntryStream.LicensePlate, EntryStream.TollId, Registration.RegistrationId
FROM EntryStream TIMESTAMP BY EntryTime
JOIN Registration
ON EntryStream.LicensePlate = Registration.LicensePlate
WHERE Registration.Expired = '1'
```

tootest запроса с помощью эталонных данных требуется toodefine источник входных данных для hello справочных данных, которые уже были выполнены.

tootest этот запрос, вставить hello в hello **ЗАПРОСА** щелкните **тест**и укажите hello двух источников входных данных регистрации hello образец данных и нажмите кнопку **теста**.  
   
![Выходные данные теста hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image46.png)

## <a name="start-hello-stream-analytics-job"></a>Запустить задание Stream Analytics hello
Пришло время toofinish hello настройки и запуска hello задания. Сохранить запрос hello из 3 вопроса, которые будут получены выходные данные, что совпадений hello схему hello **TollDataRefJoin** выходной таблицы.

Задание перейдите toohello **МОНИТОРИНГА**и нажмите кнопку **запустить**.

![Снимок экрана кнопку "Пуск" hello в панель мониторинга задания hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image48.png)

В hello открывшемся диалоговом окне, измените hello **ЗАПУСК ВЫВОДА** время слишком**время пользовательского**. Изменение hello час tooone часа, после чего hello текущее время. Это изменение гарантирует, что все события из концентратора событий hello обрабатываются с момента запуска toogenerate hello события в начале hello hello учебника. Теперь щелкните hello **запустить** кнопку toostart hello задания.

![Выбор настраиваемого времени](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image49.png)

Запуск задания hello может занять несколько минут. Можно просматривать состояние hello на страницу приветствия верхнего уровня для Stream Analytics.

![Снимок экрана: hello состояние задания hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image50.png)

## <a name="check-results-in-visual-studio"></a>Проверка результатов в Visual Studio
1. Откройте обозреватель серверов Visual Studio и щелкните правой кнопкой мыши hello **TollDataRefJoin** таблицы.
2. Нажмите кнопку **Показать таблицу данных** toosee hello выходные данные задания.
   
    ![Выбор "Показать таблицу данных" в обозревателе серверов](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image51.jpg)

## <a name="scale-out-azure-stream-analytics-jobs"></a>Задания по масштабированию в Azure Stream Analytics
Azure Stream Analytics предназначен tooelastically масштабирования, чтобы можно было обработать большой объем данных. можно использовать запрос Hello Azure Stream Analytics **PARTITION BY** предложение tootell hello системы, этот шаг будет горизонтального масштабирования. **PartitionId** — специальный столбец hello системы добавляет идентификатор секции hello toomatch входа hello (концентратор событий).

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*)AS Count
    FROM EntryStream TIMESTAMP BY EntryTime PARTITION BY PartitionId
    GROUP BY TUMBLINGWINDOW(minute,3), TollId, PartitionId

1. Остановка hello текущего задания, hello запроса update в hello **ЗАПРОСА** вкладка и откройте hello **параметры** шестеренки в панель мониторинга задания hello. Щелкните пункт **Масштаб**.
   
    **ЕДИНИЦЫ потоковой ПЕРЕДАЧИ** определить hello объем вычислительной мощности, hello задания может получать.
2. Изменение hello раскрывающегося списка от 1 из 6.
   
    ![Снимок экрана: выбор 6 единиц потоковой передачи](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image52.png)
3. Go toohello **ВЫХОДОВ** вкладку и измените имя hello таблицы SQL hello слишком**TollDataTumblingCountPartitioned**.

При запуске задания hello теперь Azure Stream Analytics можно распределить работу между дополнительные вычислительные ресурсы и улучшить производительность. Обратите внимание, что hello TollApp приложение также отправляет события, секционирована по TollId.

## <a name="monitor"></a>Монитор
Hello **монитор** область содержит статистические данные о выполнении задания hello. Первый раз Настройка требуется учетная запись хранения toouse hello в hello совпадают (имя платный как остальные hello в этом документе).   

![Снимок экрана области "Монитор"](media/stream-analytics-build-an-iot-solution-using-stream-analytics/monitoring.png)

Вы можете получить доступ к **журналы действий** из панели мониторинга задания hello **параметры** также области.


## <a name="conclusion"></a>Заключение
Этот учебник появился toohello службой Azure Stream Analytics. Он показано, как tooconfigure входов и выходов для hello задания Stream Analytics. С помощью сценария данных платный hello hello учебнике описано распространенных типов проблем, возникающих в пространстве данных в движения и как они могут быть устранены с помощью простых запросов в стиле SQL в Azure Stream Analytics hello. Учебник Hello описано конструкции SQL расширения для работы с темпоральных данных. Показано, как потоки данных toojoin, как поток данных hello tooenrich с статические справочные данные и как tooscale ожидания запроса tooachieve более высокую пропускную способность.

Несмотря на то что в этом руководстве хорошо представлена вступительная информация, оно является далеко не полным. Имеются дополнительные шаблоны запросов, с помощью языка SAQL hello в [примеры для распространенных шаблонов использования Stream Analytics запроса](stream-analytics-stream-analytics-query-patterns.md).
См. toohello [документации](https://azure.microsoft.com/documentation/services/stream-analytics/) toolearn больше о Azure Stream Analytics.

## <a name="clean-up-your-azure-account"></a>Очистка учетной записи Azure
1. Остановка задания Stream Analytics hello в hello портал Azure.
   
    Hello Setup.ps1 скрипт создает два концентраторов событий и базы данных SQL. следующие инструкции помогут очистки ресурсов в конце hello учебника hello Hello.
2. В окне PowerShell, введите **.\\ Cleanup.ps1** toostart hello скрипт, который удаляет ресурсы, используемые в учебнике hello.
   
   > [!NOTE]
   > Ресурсы идентифицируются по имени hello. Убедитесь, что перед подтверждением удаления вы внимательно просмотрели каждый элемент.
   > 
   > 


