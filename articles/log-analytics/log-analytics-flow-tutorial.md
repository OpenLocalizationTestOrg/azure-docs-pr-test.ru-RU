---
title: "aaaAutomate анализа журналов Azure обрабатывает с потоком Microsoft"
description: "Дополнительные сведения об использовании Microsoft Flow tooquickly автоматизации повторяющихся процессов с помощью соединителя Azure Log Analytics hello."
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a>Автоматизировать процессы службы анализа журналов с соединителем hello для Microsoft Flow
[Microsoft Flow](https://ms.flow.microsoft.com) позволяет автоматизировать toocreate рабочих процессов, использующих сотни действия для различных служб. Выходные данные из одного действия может использоваться как входные tooanother, позволяя toocreate интеграции между различными службами.  Соединитель Hello анализа журналов Azure для Microsoft Flow разрешить toobuild рабочих процессов, которые включают данные, полученные путем поиска журналов в службе анализа журналов.

Например можно использовать данные анализа журналов Microsoft Flow toouse уведомление по электронной почте из Office 365, создание ошибки в Visual Studio Team Services или резерв сообщение.  Вы можете запускать рабочие процессы с помощью простого расписания или какого-либо действия в подключенной службе, например при получении почты или твита.  


> [!NOTE]
> Hello анализа журналов Azure для Microsoft Flow соединителю вашей рабочей области обновления toobe toohello новый анализа журналов язык запросов. Можно узнать больше о новом языке hello и получить tooupgrade процедуры hello в рабочей области [обновление поиск журнала toonew рабочей области Azure Log Analytics](log-analytics-log-search-upgrade.md).  

Учебник Hello в этой статье показано, как toocreate поток, который автоматически отправляет hello результатов поиска журналов Служба аналитики журналов по электронной почте, лишь один пример того, как можно использовать в Microsoft Flow анализа журналов. 


## <a name="step-1-create-a-flow"></a>Шаг 1. Создание последовательности
1. Войдите в слишком[Microsoft Flow](http://flow.microsoft.com)и выберите **Мои потоки**.
2. Щелкните **Создать с нуля**.

## <a name="step-2-create-a-trigger-for-your-flow"></a>Шаг 2. Создание триггера для последовательности
1. Щелкните **Search hundreds of connectors and triggers** (Поиск по сотням соединителей и триггеров).
2. Тип **расписание** в поле поиска hello.
3. Выберите **Расписание**, а затем **Расписание — повторение**.
4. В hello **частоты** выберите **день** и в hello **интервал** введите **1**.<br><br>![Диалоговое окно триггера Microsoft Flow](media/log-analytics-flow-tutorial/flow01.png)


## <a name="step-3-add-a-log-analytics-action"></a>Шаг 3. Добавление действия Log Analytics
1. Выберите поле **+ Новый шаг**, а затем щелкните **Добавить действие**.
2. Найдите **Log Analytics**.
3. Щелкните **Azure Log Analytics – Run query and visualize results** (Azure Log Analytics – выполнить запрос и отобразить результаты).<br><br>![Окно выполнения запроса Log Analytics](media/log-analytics-flow-tutorial/flow02.png)

## <a name="step-4-configure-hello-log-analytics-action"></a>Шаг 4: Настройка анализа журналов действие hello

1. Укажите подробности hello для вашей рабочей области, включая hello подписки ID, группа ресурсов и имя рабочей области.
2. Добавьте следующие toohello запросов анализа журналов hello **запроса** окна.  Это лишь пример запроса, поэтому вы можете заменить его любым другим запросом, возвращающим данные.
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. Выберите **HTML-таблицы** для hello **тип диаграммы**.<br><br>![Действие Log Analytics](media/log-analytics-flow-tutorial/flow03.png)

## <a name="step-5-configure-hello-flow-toosend-email"></a>Шаг 5: Настройка электронной почты toosend потока hello

1. Выберите поле **Новый шаг**, а затем щелкните **Добавить действие**.
2. Выполните поиск по запросу **Office 365 Outlook**.
3. Щелкните **Office 365 Outlook – Send an email** (Office 365 Outlook — отправка сообщения электронной почты).<br><br>![Окно выбора Office 365 Outlook](media/log-analytics-flow-tutorial/flow04.png)

4. Укажите адрес электронной почты получателя hello в hello **для** окна и темой сообщения hello в **субъекта**.
5. Щелкните в любом месте hello **текст** поле.  В открывшемся окне **Динамическое содержимое** отобразятся значения из предыдущих действий.  
6. Выберите **Текст**.  Это hello результаты запроса hello hello анализа журналов действий.
6. Щелкните **Показать дополнительные параметры**.
7. В hello **HTML-** выберите **Да**.<br><br>![Окно настройки сообщения электронной почты Office 365](media/log-analytics-flow-tutorial/flow05.png)

## <a name="step-6-save-and-test-your-flow"></a>Шаг 6. Сохранение и тестирование последовательности
1. В hello **имя потока** , добавьте имя для вашего потока и нажмите кнопку **создания потока**.<br><br>![Сохранение последовательности](media/log-analytics-flow-tutorial/flow06.png)
2. поток Hello теперь создается и выполняется следующий день, который является заданному расписанию hello. 
3. поток hello tooimmediately тестирования, нажмите кнопку **выполнить** и затем **выполнять поток**.<br><br>![Запуск последовательности](media/log-analytics-flow-tutorial/flow07.png)
3. По завершении потока hello проверки почты hello hello получателя, указанном вами.  Вы должны были получить сообщения, содержащего текст аналогичные toohello следующее:<br><br>![Пример электронного сообщения](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения о [поиске по журналам Log Analytics](log-analytics-log-search-new.md).
- Дополнительные сведения о [Microsoft Flow](https://ms.flow.microsoft.com).



