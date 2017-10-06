---
title: "aaaScenario - создать панель мониторинга аналитики клиента без сервера Azure с | Документы Microsoft"
description: "Пример того, как можно построить toomanage клиента панели мониторинга, отзыв, социальных данных и многие другие приложения логики Azure и Azure функции."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: jehollan
ms.openlocfilehash: db175e895e37aa795a9c34bf4d65566bf68f8c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a>Создание панели мониторинга сведений о клиентах в режиме реального времени с помощью Функций Azure и Azure Logic Apps.

Azure без сервера средства предоставляют мощные возможности tooquickly сборки и узлов приложений в облаке hello без необходимости toothink об инфраструктуре.  В этом случае она будет создана tootrigger мониторинга отзывов пользователей, анализ сопровождение машинного обучения и публикации аналитики источника как Power BI или Озера данных Azure.

## <a name="overview-of-hello-scenario-and-tools-used"></a>Общие сведения о сценарии hello и средства, используемые

В заказ tooimplement это решение, мы будет использовать hello два ключевых компонента без сервера приложений в Azure: [функции Azure](https://azure.microsoft.com/services/functions/) и [приложения логики Azure](https://azure.microsoft.com/services/logic-apps/).

Логика приложения — это механизм без сервера рабочих процессов в облаке hello.  Он обеспечивает согласование по компонентам без сервера, а также подключается к tooover 100 служб и интерфейсов API.  В этом случае мы создадим tootrigger логики приложения на отзывы от клиентов.  Ниже перечислены некоторые hello соединителей, которые могут помочь в отклик отзыв toocustomer Outlook.com, Office 365, Monkey опроса, Twitter и HTTP-запроса [из веб-формы](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).  Для рабочего процесса hello ниже мы отслеживает хэштегом в Twitter.

Функции предоставляют без сервера вычислений в облаке hello.  В этом сценарии мы будем использовать функции Azure tooflag твиты от клиентов на основе ряда предварительно определенных ключевых слов.

Hello всего решения может быть [сборки в Visual Studio](logic-apps-deploy-from-vs.md) и [развернут как часть шаблона ресурсов](logic-apps-create-deploy-template.md).  Имеется также видеоруководство hello сценария [на канале 9](http://aka.ms/logicappsdemo).

## <a name="build-hello-logic-app-tootrigger-on-customer-data"></a>Построение tootrigger приложения hello логику на данных о клиентах

После [Создание приложения логики](logic-apps-create-a-logic-app.md) в Visual Studio или hello портала Azure:

1. Добавьте триггер, который будет активироваться при размещении **новых твитов** в Twitter.
2. Настройте tootweets toolisten hello триггер на ключевое слово или хэштегом.

   > [!NOTE]
   > Определяет свойство повторения Hello в триггере hello частоты приложения hello логики проверки для новых элементов на основе опроса триггеры

   ![Пример триггера Twitter][1]

Это приложение будет реагировать на все новые твиты.  Мы может принимать эти данные твит и глубже выраженное мнений hello.  Для этого мы используем hello [Когнитивных службы Azure](https://azure.microsoft.com/services/cognitive-services/) мнений toodetect текста.

1. Нажмите кнопку **Новый шаг**.
1. Выберите или найдите hello **анализа текста** соединителя
1. Выберите hello **мнений обнаружить** операции
1. При запросе введите допустимый ключ Когнитивных службы для службы анализа текста hello
1. Добавить hello **твит текст** как hello tooanalyze текста.

Теперь, когда есть hello твит данные и сведения, полученные на твиты hello ряд других соединители могут относиться:
* Power BI — добавить tooStreaming строк набора данных: представление твиты режиме реального времени на Информационной панели.
* Озеро данных Azure — добавить файл: добавить tooinclude tooan Озера данных Azure набора данных для клиента данных в заданиях analytics.
* SQL. Добавляются строки. Данные можно сохранить в базе данных для последующего извлечения.
* Slack. Отправляется сообщение. Канал Slack получает оповещение об отрицательном отзыве, для которого нужно предпринять действия.

Это функция Azure также может быть используется toodo несколько пользовательских вычислений на основе данных hello.

## <a name="enriching-hello-data-with-an-azure-function"></a>Обогащения данных hello с функцией Azure

Прежде чем создавать функции, мы должны toohave приложения функции в нашей подписке Azure.  Сведения о создании функцию Azure на портале hello можно [по следующему адресу](../azure-functions/functions-create-first-azure-function-azure-portal.md)

Для вызова непосредственно из приложения логики toobe функция она должна toohave HTTP активировать привязки.  Мы рекомендуем использовать hello **HttpTrigger** шаблона.

В этом случае тело запроса hello hello Azure функция будет твит текста hello.  В коде функции hello просто определите логику на, если текст hello твит содержит ключевое слово или фразу.  сама функция Hello может храниться как простые или сложные, необходимые для сценария hello.

В конце функции hello hello просто возвращают ответа приложения логики toohello с данными.  Это может быть простое логическое значение (например, `containsKeyword`) или сложный объект.

![Настройка шага Функции Azure][2]

> [!TIP]
> При доступе к сложным ответа от функции в приложение логики, используйте действие hello синтаксического анализа JSON.

После сохранения функции hello, его можно добавить в приложение логику hello, созданной ранее.  В приложение логику hello:

1. Нажмите кнопку tooadd **новый шаг**
1. Выберите hello **функции Azure** соединителя
1. Выберите существующую функцию toochoose и обзор toohello функция, созданная
1. Отправить в hello **текст твит** для hello **текст запроса**

## <a name="running-and-monitoring-hello-solution"></a>Выполнение и отслеживание hello решения

Одно из преимуществ hello разработки без сервера взаимодействий в приложениях для логики — hello широкие возможности отладки и возможности мониторинга.  Любое выполнение (текущие или исторические) можно просмотреть в среде Visual Studio, hello портал Azure или с помощью API-интерфейса REST hello и пакеты SDK.

Один из tootest простых способов hello приложения логики использует hello **запуска** кнопку в конструкторе hello.  Щелкнув **запуска** продолжится триггер hello toopoll каждые 5 секунд, пока не будет обнаружено событие и предоставить обеспечивает динамическое представление в процессе запуска hello.

Можно просмотреть предыдущие журналы выполнения в колонке Обзор hello hello портал Azure, или с помощью Visual Studio Cloud Explorer hello.

## <a name="creating-a-deployment-template-for-automated-deployments"></a>Создание шаблона развертывания для автоматического развертывания

После разработки решения, его можно записать и развернут с помощью tooany шаблона развертывания Azure регион Azure в Здравствуй, мир!.  Это полезно для изменения параметров разных версий этого рабочего процесса, а также для интеграции этого решения в конвейер сборки и выпуска.  Дополнительные сведения о создании шаблона развертывания см. [в этой статье](logic-apps-create-deploy-template.md).

Функции Azure также могут быть включены в шаблон развертывания hello - так hello всего решения с все зависимости можно управлять как один шаблон.  Пример развертывания шаблона функции можно найти в hello [быстрый запуск Azure шаблон репозитория](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).

## <a name="next-steps"></a>Дальнейшие действия

* [Примеры и распространенные сценарии для Azure Logic Apps](logic-apps-examples-and-scenarios.md)
* [Пошаговое видеоруководство по созданию этого решения](http://aka.ms/logicappsdemo)
* [Узнайте, как toohandle и перехвата исключений в пределах приложения логики](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: ./media/logic-apps-scenario-social-serverless/twitter.png
[2]: ./media/logic-apps-scenario-social-serverless/function.png