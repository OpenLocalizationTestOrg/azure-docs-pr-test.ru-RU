---
title: "aaaSwitch инструкции для различных действий в приложениях для логики Azure | Документы Microsoft"
description: "Выберите tooperform различные действия на логику приложения, на основе выражения значений с помощью оператора выбора."
services: logic-apps
keywords: "оператор switch"
author: derek1ee
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: LADocs; deli
ms.openlocfilehash: 09ed7e4a752003aba157e9156bf4dc89ef86f5ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a>Выполнение различных действий в приложениях логики с помощью оператора switch

При создании рабочего процесса, часто имеют разные действия tootake на основе значения hello объекта или выражение. Например может потребоваться вашей toobehave логику приложения, по-разному на основе hello кода состояния HTTP-запроса или параметра, выбранного в сообщение электронной почты.

Эти сценарии можно использовать tooimplement оператора switch. Логика приложения можно оценить маркера или выражение и выберите случай hello с hello же hello tooexecute значение указанного действия. Только один вариант должен соответствовать инструкцию switch hello.

> [!TIP]
> Как и в других языках программирования, операторы switch поддерживают только операторы равенства. Если вам нужны другие операторы сравнения (к примеру, оператор greater than), используйте выражение условия.
> поведение детерминированным выполнения tooensure, вариантов должен содержать значение уникальный и статические вместо динамических токены или выражение.

## <a name="prerequisites"></a>Предварительные требования

- Активная подписка Azure. Если у вас еще нет активной подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/) или [попробуйте бесплатную версию Logic Apps](https://tryappservice.azure.com/).
- [Базовые сведения о приложениях логики](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-tooyour-workflow"></a>Добавление рабочего процесса tooyour оператора switch

как работает оператор switch tooshow, в этом примере создается логики приложения, что мониторы файлы загружены tooDropbox. При отправке новых файлов hello приложения hello логики отправляет утверждающего tooan электронной почты, выбирает ли tootransfer tooSharePoint этих файлов. приложение Hello использует инструкцию switch, который будет выполнять различные действия на основе значения hello hello выбирает утверждающий.

1. Создайте приложение логики и выберите триггер **Dropbox – When a file is created** (Dropbox — при создании файла).

   ![Использование триггера Dropbox — When a file is created (Dropbox — при создании файла)](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. Добавьте это действие триггера hello: **Outlook.com - утверждения отправлять по электронной почте**

   > [!TIP]
   > Приложения логики поддерживают также утверждение по электронной почте из учетной записи Outlook в Office 365.

   - Если у вас нет существующего подключения, вам предложат toocreate один.
   - Заполните необходимые hello. Например, в разделе **для**, укажите hello адрес электронной почты для отправки электронной почты утверждающий hello.
   - В разделе **User Options** (Параметры пользователя) введите `Approve, Reject`.

   ![Настройка подключения](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. Добавьте оператор switch.

   - Выберите **+ New step** (+Новый шаг) > **... Дополнительно** > **Add a switch case** (Добавить вариант для оператора switch). 
   - Теперь мы хотим tooselect hello действие tooperform основании hello `SelectedOptions` выходные данные hello *письмо утверждения* действие. 
   Это поле можно найти в hello **добавить динамическое содержимое** селектора.
   - Используйте *случая 1* toohandle при выборе утверждающий hello `Approve`.
     - Утвержденный, скопируйте hello исходный файл tooSharePoint через Интернет с hello [ **SharePoint Online — создать файл** действия](../connectors/connectors-create-api-sharepointonline.md).
     - Добавьте еще одно действие hello пользователи toonotify вариантов, что файл доступен на сайте SharePoint.
   - Добавление другого варианта toohandle при выборе пользователем `Reject`.
     - В случае отклонения отправляете уведомления по электронной почте о том других утверждающих, что файл hello отклоняется и никаких дальнейших действий не требуется.
   - `SelectedOptions`предоставляет только два варианта, поэтому можно оставить hello **по умолчанию** варианта пустая.

   ![Оператор switch](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > Оператор switch требуется по крайней мере один вариант в случае по умолчанию toohello сложения.

4. После инструкции switch hello, удалить исходный файл, отправленный tooDropbox hello путем добавления этого действия: **общего банка данных - удалить файл**

5. Сохраните приложение логики. Протестируйте приложение, передав tooDropbox файла. Вскоре должно прийти сообщение электронной почты утверждения. Выберите параметр и наблюдать за поведением hello.

   > [!TIP]
   > Узнать о возможностях слишком[Отслеживайте свои приложения логики](logic-apps-monitor-your-logic-apps.md).

## <a name="understand-hello-code-behind-switch-statements"></a>Понимание кода hello за операторами switch

Теперь, когда создан логику приложения, используя инструкцию switch, давайте взглянем на определение кода hello за инструкцию switch hello.

```json
"Switch": {
    "type": "Switch",
    "expression": "@body('Send_approval_email')?['SelectedOption']",
    "cases": {
        "Case 1" : {
            "case" : "Approved",
            "actions" : {}
        },
        "Case 2" : {
            "case" : "Rejected",
            "actions" : {}
        }
    },
    "default": {
        "actions": {}
    },
    "runAfter": {
        "Send_approval_email": [
            "Succeeded"
        ]
    }
}
```

* `"Switch"`— Имя hello инструкцию switch hello, его можно переименовать для удобства чтения. 
* `"type": "Switch"`Указывает действие hello в операторе switch. 
* `"expression"`hello утверждающий выбранный параметр в этом примере и вычисляется для каждого варианта case, объявленном позже в определении hello. 
* `"cases"` может содержать любое число вариантов. Для каждого варианта `"Case *"` является именем по умолчанию hello hello случай, который можно переименовать для удобства чтения. 
`"case"`Указывает метку case hello, hello коммутатора использует выражение для сравнения, которое должно быть константой и уникальные значения. Если ни один из вариантов hello соответствует hello switch-выражения, в рамках `"default"` выполняются.

## <a name="get-help"></a>Получение справки

tooask вопросы, ответы на вопросы и см. какие другие пользователи приложения логики Azure делают, посетите hello [форуме по Azure логику приложений](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp улучшить логику приложения Azure и соединителей, проголосовать или отправить идеями hello [веб-сайт отзывов пользователей приложения логики Azure](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Дальнейшие действия

- Узнайте, каким образом слишком[Добавление условий](logic-apps-use-logic-app-features.md)
- Узнайте, как [обрабатываются ошибки и исключения в Logic Apps](logic-apps-exception-handling.md).
- Ознакомьтесь с [возможностями языка для описания рабочих процессов](logic-apps-author-definitions.md).