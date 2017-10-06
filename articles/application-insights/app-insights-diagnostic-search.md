---
title: "aaaUsing поиска в Azure Application Insights | Документы Microsoft"
description: "Поиск и фильтрация необработанных данных телеметрии, отправляемых веб-приложением."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2a437555-8043-45ec-937a-225c9bf0066b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: df2b0eb017ad48bcdc6ef57d8dff207d120143b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-search-in-application-insights"></a>Поиск в Application Insights
Функция поиска [Application Insights](app-insights-overview.md) использовать toofind и исследовать телеметрии отдельные элементы, такие как представления страниц, исключения или веб-запросов. Также можно просматривать журнал трассировки и события, которые были закодированы.

(Для более сложных запросов к данным используйте [Analytics](app-insights-analytics-tour.md).)

## <a name="where-do-you-see-search"></a>Как найти функцию поиска?
### <a name="in-hello-azure-portal"></a>В hello портал Azure
Поиск диагностики можно открыть явно из колонки Обзор аналитики приложения hello приложения:

![Откройте поиск по журналу диагностики](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

Она также открывается при щелчке некоторых диаграмм и элементов сетки. В этом случае его фильтров предварительно задан toofocus на hello тип выбранного элемента. 

Например в колонке Обзор hello, представляет собой линейчатую диаграмму, запросов, относящихся к времени ответа. Переходите toosee диапазон производительности список отдельных запросов, время отклика диапазоном.

![Выбор производительности запроса](./media/app-insights-diagnostic-search/07-open-from-filters.png)

основной текст Hello диагностики поиска является список элементов телеметрии - запросов сервера страница представления, пользовательские события, которые были закодированы и т. д. Hello вверху списка hello является Сводка диаграмма, отображающая счетчики событий со временем.

Нажмите кнопку обновления tooget новые события.

### <a name="in-visual-studio"></a>В Visual Studio

В Visual Studio также есть окно поиска по Application Insights. Это может пригодиться для отображения телеметрии события, создаваемые приложением hello, который выполняется отладка. Однако также можно показать hello события, полученные от опубликованного приложения в hello портал Azure.

Откройте окно поиска hello в Visual Studio:

![Как открыть окно "Поиск по Application Insights" в Visual Studio](./media/app-insights-diagnostic-search/32.png)

окно поиска Hello имеет аналогичные функции toohello веб-портала.

![Окно "Поиск по Application Insights" в Visual Studio](./media/app-insights-diagnostic-search/34.png)

Вкладка операции отслеживания Hello отображается при открытии запроса или вид страницы. "Операция" — это последовательность событий, связанный с tooa одного запроса или страницы представления. В одну операцию могут входить, например, вызовы зависимостей, исключения, журналы трассировки и пользовательские события. на вкладке выводятся операции отслеживания Hello графически hello времени и продолжительности эти события в представлении запроса или страница toohello отношения. 

## <a name="inspect-individual-items"></a>Проверка отдельных элементов
Выберите все поля ключа toosee элемента телеметрии и связанных элементов. Toosee hello полный набор полей, нажмите кнопку «...». 

![Щелкните новый рабочий элемент, изменить поля hello и нажмите кнопку ОК.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a>Фильтрация по типам событий
Откройте колонку hello фильтр и выберите типы событий hello, вы хотите toosee. (Если более поздней версии, нужно фильтры hello toorestore, с которыми вы открыли колонке hello, щелкните Reset).

![Щелкните "Фильтр" и укажите типы элементов телеметрии](./media/app-insights-diagnostic-search/02-filter-req.png)

Ниже приведены типы событий Hello.

* **Трассировка**  -  [журналы диагностики](app-insights-asp-net-trace-logs.md), в том числе TrackTrace, log4Net, NLog и вызовы System.Diagnostic.Trace.
* **Запрос** — HTTP-запросы, полученные серверным приложением, включая страницы, скрипты, изображения, файлы стилей и данные. Эти события — это используемые toocreate hello запроса и ответа Обзор диаграммы.
* **Представление страницы** - [телеметрии, отправленные клиентом веб-hello](app-insights-javascript.md), используемые toocreate страницы Просмотр отчетов. 
* **Пользовательское событие** — Если было введено tooTrackEvent() вызывает в порядке слишком[наблюдение за использованием](app-insights-api-custom-events-metrics.md), их можно найти здесь.
* **Исключение** - неперехваченных [исключения в hello server](app-insights-asp-net-exceptions.md)и те, которые войдите, используя TrackException().
* **Зависимости** - [вызовы из приложения сервера](app-insights-asp-net-dependencies.md) tooother служб, например API-интерфейс REST или баз данных, а также вызовы AJAX с вашей [клиентский код](app-insights-javascript.md).
* **Доступность** — результаты [тестов доступности](app-insights-monitor-web-app-availability.md).

## <a name="filter-on-property-values"></a>Фильтрация на основе значений свойств
Можно отфильтровать такие события на hello значения их свойств. Hello доступные свойства зависят от выбранных типов событий hello. 

Например, можно выбрать запросы с определенным кодом ответа. 

![Разверните свойство и выберите значение](./media/app-insights-diagnostic-search/03-response500.png)

Выбор значения конкретного свойства не имеет тот же эффект, как выбор всех значений hello. Фильтрация по этому свойству будет отключена.

### <a name="narrow-your-search"></a>Сужение области поиска
Обратите внимание, что этот hello подсчитывает toohello справа от значения фильтра hello показывать число вхождений существует в текущем наборе отфильтрованные hello. 

В этом примере ясно, что этот запрос «Rpt/сотрудники» hello приводит большинство ошибок hello "500":

![Разверните свойство и выберите значение](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-hello-same-property"></a>Найти события с hello одного свойства
Найти Здравствуйте, все элементы, которые hello же значение свойства:

![Щелкните правой кнопкой мыши свойство](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-hello-data"></a>Поиск данных hello

> [!NOTE]
> toowrite более сложные запросы, откройте [ **Analytics** ](app-insights-analytics-tour.md) из hello верхней части колонки поиска hello.
> 

Можно выполнить поиск условия в любом hello значений свойств. Это особенно полезно, если вы написали [пользовательские события](app-insights-api-custom-events-metrics.md) со значениями свойств. 

Может потребоваться tooset диапазон времени, как поиск на короткий период, выполняются быстрее. 

![Откройте поиск по журналу диагностики](./media/app-insights-diagnostic-search/appinsights-311search.png)

Выполните поиск по полным словам, а не по подстрокам. Используйте кавычки tooenclose специальные символы.

| string | *не* найдена по словам | но найдена по словам |
| --- | --- | --- |
| HomeController.About |home<br/>controller<br/>out | homecontroller<br/>about<br/>"homecontroller.about"|
|США|Сое<br/>диненные|соединенные<br/>штаты<br/>соединенные AND штаты<br/>"соединенные штаты"

Ниже приведены hello выражения поиска, которые можно использовать.

| Пример запроса | Результат |
| --- | --- |
| `apple` |Найти все события за период времени hello, поля которых есть слово hello «apple» |
| `apple AND banana` |Поиск событий, содержащих оба слова. Используйте "AND" заглавными буквами, а не "and". |
| `apple OR banana`<br/>`apple banana` |Поиск событий, содержащих любое из этих слов. Используйте «OR» заглавными буквами, а не «or».<br/>Короткая форма. |
| `apple NOT banana` |Найти события, содержащие одно слово, но не hello других. |



## <a name="sampling"></a>Выборка
Если приложение создает большой объем данных телеметрии (при использовании hello 2.0.0-beta3 версии пакета SDK для ASP.NET или более поздней версии), модуль адаптивной выборки hello автоматически уменьшает hello тома, отправляемое toohello портала, отправляя репрезентативной часть событий. Тем не менее события, которые связанные toohello того же запроса или отмену выбора как группой, чтобы могли перемещаться между связанными событиями. 

[Дополнительная информация о выборке](app-insights-sampling.md).



## <a name="create-work-item"></a>Создание рабочего элемента
Можно создать ошибку в GitHub или Visual Studio Team Services с подробными сведениями hello из любого элемента телеметрии. 

![Щелкните новый рабочий элемент, изменить поля hello и нажмите кнопку ОК.](./media/app-insights-diagnostic-search/42.png)

Hello при первом запуске этого будет предложено tooconfigure tooyour ссылку Team Services учетной записи и проекта.

![Введите URL-адрес hello сервера Team Services и имя проекта hello и нажмите авторизовать](./media/app-insights-diagnostic-search/41.png)

(Можно также настроить ссылку hello в колонке hello рабочих элементов.)

## <a name="save-your-search"></a>Сохранение результатов поиска
При установке все фильтры hello hello поиска можно сохранить в список избранного. Если вы работаете в учетную запись организации, можно ли tooshare его с другими членами команды.

![Щелкните Избранное hello имя набора и нажмите кнопку Сохранить](./media/app-insights-diagnostic-search/08-favorite-save.png)

Поиск hello toosee еще раз, **колонке Обзор перейдите toohello** и открыть Избранное:

![Плитка "Избранное"](./media/app-insights-diagnostic-search/09-favorite-get.png)

Если вы сохранили относительный временной диапазон, повторно открыть колонку hello имеет hello последние данные. Если вы сохранили с диапазоном абсолютное время, вы увидите hello и те же данные каждый раз. (Если «Relative» не поддерживается при необходимости toosave Избранное, выберите диапазон времени в заголовке hello и задать диапазон времени, не настраиваемого диапазона).

## <a name="send-more-telemetry-tooapplication-insights"></a>Отправлять дополнительные данные телеметрии tooApplication аналитики
В телеметрии toohello out of box сложения отправленных пакет SDK Application Insights вы можете:

* Выполнять трасcировку журналов, используя избранную платформу ведения журнала в [.NET](app-insights-asp-net-trace-logs.md) или [Java](app-insights-java-trace-logs.md). Благодаря этому можно будет выполнить поиск в журнале трассировки и сопоставить результаты с просмотрами страниц, исключениями и другими событиями. 
* [Написание кода](app-insights-api-custom-events-metrics.md) toosend пользовательских событий, представления страниц и исключения. 

[Узнайте, каким образом ведет журнал toosend и пользовательского телеметрии tooApplication аналитики](app-insights-asp-net-trace-logs.md).

## <a name="questions"></a>Вопросы и ответы
### <a name="limits"></a>Какой объем данных сохраняется?

В разделе hello [Сводная таблица ограничений](app-insights-pricing.md#limits-summary).

### <a name="how-can-i-see-post-data-in-my-server-requests"></a>Как просмотреть данные POST в запросах к серверу?
Мы не заносить в журнал данные POST hello автоматически, но можно использовать [TrackTrace или журнала вызовов](app-insights-asp-net-trace-logs.md). Поместите hello ОТПРАВЛЕННЫХ данных в параметре сообщение hello. Невозможно применить фильтр сообщений hello в hello таким же, каким образом можно применить фильтр свойств, но ограничение размера hello длиннее.

## <a name="video"></a>Видео

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="add"></a>Дальнейшие действия
* [Создание сложных запросов в Analytics](app-insights-analytics-tour.md)
* [Отправить журналы настроенной телеметрии и tooApplication аналитики](app-insights-asp-net-trace-logs.md)
* [Наблюдение за доступностью и скоростью реагирования веб-сайта](app-insights-monitor-web-app-availability.md)
* [Устранение неполадок](app-insights-troubleshoot-faq.md)
