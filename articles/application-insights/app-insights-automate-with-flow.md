---
title: "aaaAutomate аналитики приложения Azure обрабатывает с потоком Microsoft"
description: "Дополнительные сведения об использовании Microsoft Flow tooquickly автоматизации повторяющихся процессов с помощью соединителя hello Application Insights."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: bwren
ms.openlocfilehash: b34488a6b8b8b0a6add960a67f1426cbbbc13552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automate-azure-application-insights-processes-with-hello-connector-for-microsoft-flow"></a>Автоматизации процессов Azure Application Insights с соединителем hello для Microsoft Flow

Как найти самостоятельно повторяющемся выполнении hello же запросы на вашей toocheck данные телеметрии, что служба работает правильно? Вид tooautomate эти запросы используются для поиска тренды и аномалии, а затем построить собственные рабочие процессы вокруг них? Соединитель Hello аналитики приложений Azure (Предварительная версия) для Microsoft Flow — hello правильное средство для следующих целей.

Благодаря этой интеграции можно автоматизировать множество процессов, не написав ни строчки кода. После создания потока с помощью Application Insights действие, hello потока автоматически запускает запрос аналитики аналитики приложений. 

Вы также можете добавить дополнительные действия. Служба Flow предоставляет сотни действий. Например можно использовать Microsoft Flow tooautomatically отправки уведомления по электронной почте или создание ошибки в Visual Studio Team Services. Можно также использовать один из hello многие [шаблоны](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) , доступных для hello соединитель для потока корпорации Майкрософт. Эти шаблоны ускорить процесс создания потока hello. 

<!--hello Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a>Создание последовательности для Application Insights

В этом учебнике вы узнаете, как toocreate поток, который использует hello Analytics кластера автоматически алгоритм toogroup атрибуты в hello данных для веб-приложения. поток Hello автоматически отправляет результаты hello по электронной почте, лишь один пример того, как можно использовать Microsoft Flow и аналитика аналитики приложений друг с другом. 

### <a name="step-1-create-a-flow"></a>Шаг 1. Создание последовательности
1. Вход слишком[Microsoft Flow](http://flow.microsoft.com)и выберите **Мои потоки**.
2. Щелкните **Create a flow from blank** (Создать последовательность с нуля).

### <a name="step-2-create-a-trigger-for-your-flow"></a>Шаг 2. Создание триггера для последовательности
1. Выберите **Расписание**, а затем **Расписание — повторение**.
2. В hello **частоты** выберите **день**и в hello **интервал** введите **1**.

    ![Диалоговое окно триггера Microsoft Flow](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a>Шаг 3. Добавление действия Application Insights
1. Выберите поле **+Новый шаг**, а затем щелкните **Добавить действие**.
2. Выполните поиск по запросу **Azure Application Insights**.
3. Выберите **Azure Application Insights – Visualize Analytics query Preview** (Azure Application Insights — визуализация запроса Analytics [предварительная версия]).

    ![Окно запуска запроса Analytics](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>Шаг 4: Подключение tooan ресурс Application Insights

toocomplete этот шаг требуется для вашего ресурса идентификатора приложения и ключ API. Их можно восстановить из hello портал Azure, как показано в hello, следующая схема:

![Идентификатор приложения в hello портал Azure](./media/app-insights-automate-with-flow/appid.png) 

- Введите имя для соединения, вместе с hello приложения идентификатор и ключ API.

    ![Окно подключения Microsoft Flow](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>Шаг 5: Укажите hello аналитический запрос и тип диаграммы
Следующий пример запроса выбирает hello сбой запросов в последний день hello и сопоставляет их с исключения, которые возникают в ходе операции hello. Аналитика сопоставляет их на основе идентификатора operation_Id hello. Затем запрос Hello сегменты hello результаты с помощью алгоритма autocluster hello. 

При создании собственных запросов, убедитесь, что они работают надлежащим образом в Analytics перед его добавлением tooyour потока.

- Добавьте hello в следующем запросе аналитика и выберите тип диаграммы таблицы HTML hello. 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```
    
    ![Окно настройки запроса Analytics](./media/app-insights-automate-with-flow/flow4.png)

### <a name="step-6-configure-hello-flow-toosend-email"></a>Шаг 6: Настройка электронной почты toosend потока hello

1. Выберите поле **+Новый шаг**, а затем щелкните **Добавить действие**.
2. Выполните поиск по запросу **Office 365 Outlook**.
3. Щелкните **Office 365 Outlook – Send an email** (Office 365 Outlook — отправка сообщения электронной почты).

    ![Окно выбора Office 365 Outlook](./media/app-insights-automate-with-flow/flow2b.png)

4. В hello **отправить сообщение электронной почты** окне hello следующие:

   а. Введите адрес электронной почты получателя hello hello.

   b. Введите тему сообщения hello.

   c. Щелкните в любом месте hello **текст** и меню hello динамического содержимого, открывающееся hello справа выберите **текст**.

   d. Щелкните **Показать дополнительные параметры**.

    ![Конфигурация Office 365 Outlook](./media/app-insights-automate-with-flow/flow5.png)

5. В меню hello динамического содержимого hello следующие:

    а. Выберите **Имя вложения**.

    b. Выберите **Содержимое вложения**.
    
    c. В hello **HTML-** выберите **Да**.

    ![Экран настройки сообщения электронной почты Office 365](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a>Шаг 7. Сохранение и тестирование последовательности
- В hello **имя потока** , добавьте имя для вашего потока и нажмите кнопку **создания потока**.

    ![Окно создания последовательности](./media/app-insights-automate-with-flow/flow8.png)

Можно подождать hello триггер toorun это действие или hello потока можно запустить немедленно по [выполнения триггера hello по требованию](https://flow.microsoft.com/blog/run-now-and-six-more-services/).

При запуске потока hello hello получатели, заданные в списка по электронной почте hello получать сообщения электронной почты, который выглядит как следующий hello:

![Пример электронного сообщения](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a>Дальнейшие действия

- Узнайте больше о создании [запросов Analytics](app-insights-analytics-using.md).
- Дополнительные сведения о [Microsoft Flow](https://ms.flow.microsoft.com).



<!--Link references-->





