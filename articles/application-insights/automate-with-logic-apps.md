---
title: "aaaAutomate аналитики приложения Azure обрабатывает с помощью приложения логики."
description: "Узнайте, как быстро можно автоматизировать повторяющихся процессов, путем добавления hello Application Insights соединитель tooyour логику приложения."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a>Автоматизация процессов Application Insights с помощью Logic Apps

Как найти самостоятельно многократно выполнение hello же запросов в вашей toocheck данные телеметрии ли служба работает правильно? Вид tooautomate эти запросы используются для поиска тренды и аномалии, а затем построить собственные рабочие процессы вокруг них? Соединитель Hello аналитики приложений Azure (Предварительная версия) для логики приложений — hello правильное средство для этой цели.

Благодаря этой интеграции можно автоматизировать множество процессов, не написав ни строчки кода. Приложения логики можно создать соединитель tooquickly hello Application Insights полностью автоматизировать любой процесс Application Insights. 

Вы также можете добавить дополнительные действия. Hello Logic Apps службы приложения Azure позволяют сотни действия доступны. Например, вы можете использовать приложение логики, чтобы автоматически отправить уведомление по электронной почте или создать ошибку в Visual Studio Team Services. Можно также использовать один hello многие доступные [шаблоны](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp ускорить процесс создания логики приложения hello. 

## <a name="create-a-logic-app-for-application-insights"></a>Создание приложения логики для Application Insights

В этом учебнике вы узнаете, как toocreate логику приложения, в котором используется hello Analytics autocluster алгоритм toogroup атрибуты в hello данных для веб-приложения. Hello потока автоматически отправляет результаты hello по электронной почте, лишь один пример того, как можно использовать приложения аналитика Analytics и Logic Apps друг с другом. 

### <a name="step-1-create-a-logic-app"></a>Шаг 1. Создание приложения логики
1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. В hello **New** выберите **Интернет + мобильные устройства**, а затем выберите **приложения логики**.

    ![Окно создания приложения логики](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a>Шаг 2. Создание триггера для приложения логики
1. В hello **конструктор логику приложения** окна в разделе **начинаться с общий триггер**выберите **повторения**.

    ![Окно конструктора приложений логики](./media/automate-with-logic-apps/logicapp2.png)

2. В hello **частоты** выберите **день** и затем в hello **интервал** введите **1**.

    ![Окно "Повторение" в конструкторе приложений логики](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a>Шаг 3. Добавление действия Application Insights
1. Выберите поле **+Новый шаг**, а затем щелкните **Добавить действие**.

2. В hello **выбрать действия** поле поиска, введите **Azure Application Insights**.

3. В разделе **Действия** выберите **Azure Application Insights – Visualize Analytics query Preview** (Azure Application Insights — визуализация запроса Analytics [предварительная версия]).

    ![Окно "Выберите действие" в конструкторе приложений логики](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>Шаг 4: Подключение tooan ресурс Application Insights

toocomplete этот шаг требуется для вашего ресурса идентификатора приложения и ключ API. Их можно восстановить из hello портал Azure, как показано в hello, следующая схема:

![Идентификатор приложения в hello портал Azure](./media/automate-with-logic-apps/appid.png) 

Введите имя для соединения, идентификатор приложения hello и ключ API hello.

![Окно подключения последовательности в конструкторе приложений логики](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>Шаг 5: Укажите hello аналитический запрос и тип диаграммы
В следующем примере hello hello запрос выбирает hello сбой запросов в последний день hello и сопоставляет их с исключения, которые возникают в ходе операции hello. Аналитика сопоставляет hello не удалось выполнить запросы, исходя из идентификатора operation_Id hello. Затем запрос Hello сегменты hello результаты с помощью алгоритма autocluster hello. 

При создании собственных запросов, убедитесь, что они работают надлежащим образом в Analytics перед его добавлением tooyour потока.

1. В hello **запроса** добавьте hello в следующем запросе аналитика: 

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

2. В hello **тип диаграммы** выберите **HTML-таблицы**.

    ![Окно настройки запроса Analytics](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a>Шаг 6: Настройка hello логику приложения toosend по электронной почте

1. Щелкните **Новый шаг**, а затем — **Добавить действие**.

2. Введите в поле поиска hello **Office 365 Outlook**.

3. Щелкните **Office 365 Outlook – Send an email** (Office 365 Outlook — отправка сообщения электронной почты).

    ![Выбор Office 365 Outlook](./media/automate-with-logic-apps/flow2b.png)

4. В hello **отправить сообщение электронной почты** окне hello следующие:

   а. Введите адрес электронной почты получателя hello hello.

   b. Введите тему сообщения hello.

   c. Щелкните в любом месте hello **текст** и меню hello динамического содержимого, открывающееся hello справа выберите **текст**.

   d. Щелкните **Показать дополнительные параметры**.

      ![Конфигурация Office 365 Outlook](./media/automate-with-logic-apps/flow5.png)

5. В меню hello динамического содержимого hello следующие:

    а. Выберите **Имя вложения**.

    b. Выберите **Содержимое вложения**.
    
    c. В hello **HTML-** выберите **Да**.

      ![Экран настройки электронного сообщения Office 365](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a>Шаг 7. Сохранение и тестирование приложения логики
* Нажмите кнопку **Сохранить** toosave изменения.

Вы можете ожидать hello триггер toorun hello логику приложения или немедленно запустить приложение hello логику, выбрав **запуска**.

![Экран создания приложения логики](./media/automate-with-logic-apps/step7.png)

При запуске приложения логики hello получателей, указанных в список сообщений электронной почты hello получит сообщение электронной почты, который выглядит как следующий hello:

![Сообщение электронной почты приложения логики](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a>Дальнейшие действия

- Узнайте больше о создании [запросов Analytics](app-insights-analytics-using.md).
- Дополнительные сведения о [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).



<!--Link references-->





