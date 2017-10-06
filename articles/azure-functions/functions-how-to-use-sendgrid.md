---
title: "aaaHow toouse SendGrid в функциях Azure | Документы Microsoft"
description: "Показано, как toouse SendGrid в функциях Azure"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/31/2017
ms.author: rachelap
ms.openlocfilehash: a0ffdae04e5924c773d2d26427626fc1f570f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-sendgrid-in-azure-functions"></a>Как toouse SendGrid в функциях Azure

## <a name="sendgrid-overview"></a>Общие сведения о SendGrid

Azure поддерживает функции SendGrid вывода tooenable привязки функции toosend сообщений электронной почты с помощью нескольких строк кода и учетной записи SendGrid.

hello toouse SendGrid API-Интерфейс в функции Azure, должен иметь [учетной записи SendGrid](http://SendGrid.com). А также необходимо иметь ключ API SendGrid. Войдите в учетной записи SendGrid tooyour и нажмите **параметры** затем **ключ API** toogenerate API-ключ. Сохраните этот ключ, так как он потребуется на последующем шаге.

Теперь вы находитесь готов toocreate Azure функции приложения.

## <a name="create-an-azure-function-app"></a>Создание приложения-функции Azure 

Приложения-функции Azure являются контейнерами для одной или нескольких функций Azure. Функции Azure являются именно функциями. Каждая функция Azure — связанные tooone срабатывание триггера, который представляет событие, вызывающее toorun функции hello.
Каждая функция может содержать любое количество входных или выходных привязок. Привязки — это службы, которые можно использовать в функции. Выходные данные, то можно использовать toosend электронной почты — SendGrid. 

1. Войдите в портал Azure toohello и [создать приложение Azure функция](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) или открывать существующие приложения для функции. 
2. Создайте функцию Azure. tookeep простым, выберите ручной триггера и C#. 

 ![Создание функции Azure](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a>Настройка SendGrid для использования в приложении-функции Azure

Необходимо хранить свой ключ API SendGrid как параметр приложения toouse его в функции. поле ApiKey Hello не фактические SendGrid API-ключ, но параметр приложения определить, представляет фактический ключ API. Такое хранение ключа способствует обеспечению безопасности, так как ключ отделен от кода и файлов, которые могут быть возвращены в систему управления версиями.

- Создайте ключ **AppSettings** в **параметрах** приложения-функции.

 ![Создание функции Azure](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a>Настройка выходных привязок SendGrid

Привязка SendGrid доступна как выходная привязка функции Azure. Привязка для вывода toocreate SendGrid:

1. Go toohello **Интеграция** вкладку функции hello в hello портал Azure.
2. Нажмите кнопку **новый Выход** toocreate SendGrid привязка для вывода.
3. Заполните hello **ключ API** и **имя параметра сообщение** свойства. Если требуется, можно ввести теперь hello других свойств или их вместо этого кода. Приведенные здесь параметры можно использовать как значения по умолчанию.

 ![Настройка выходных привязок SendGrid](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

Добавление функции tooa привязки создает файл с именем **function.json** в папке ваша функция. Этот файл содержит все же информация, отображаемая в hello Azure функции hello **Интеграция** вкладки, но в формате Json форматирования. Параметр hello **ApiKey**, **сообщение**, и **из** поля создать следующие записи в hello hello **function.json** файла: 

```json
{
  "bindings": [    
    {
      "type": "sendGrid",
      "name": "message",
      "apiKey": "SendGridKey",
      "direction": "out",
      "from": "azure@contoso.com"
    }
  ],
  "disabled": false
}
```

При желании вы можете изменить этот файл самостоятельно.

Теперь, создания и настройки функции приложения hello и функции можно написать toosend кода hello сообщение электронной почты.

## <a name="write-code-that-creates-and-sends-email"></a>Написание кода, который создает и отправляет электронную почту

Hello SendGrid API содержит все команды hello требуется toocreate и отправить сообщение электронной почты.  

- Замените код hello в функции hello hello, следующий код:

```cs
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
    message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    // change tooemail of recipient
    personalization.AddTo(new Email("MoreEmailPlease@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

Первая строка hello уведомления содержит hello ```#r``` директиву, которая ссылается на сборку SendGrid hello. После этого можно использовать ```using``` toomore инструкции легко получить доступ к объектам hello в этом пространстве имен. Создайте в коде hello экземпляров ```Mail```, ```Personalization```, и ```Content``` объектов из hello SendGrid API, Создание электронного сообщения hello. При возврате приветственное сообщение SendGrid доставляет его. 

Hello сигнатуру функции также содержит дополнительный параметр типа out ```Mail``` с именем ```message```. Как входные, так и выходные привязки выражаются в коде как параметры функции. 

2. Тестирование кода, щелкнув **теста** и ввода сообщения в hello **текст запроса** поля, а затем щелкнуть hello **запуска** кнопки.

 ![Тестирование кода](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. Проверьте, SendGrid отправлены по электронной почте hello tooverify электронной почты. Он должен перейти toohello адрес в коде hello из шага 1 и содержать приветственное сообщение из hello **текст запроса**.

## <a name="next-steps"></a>Дальнейшие действия
В этой статье показана как toouse hello toocreate SendGrid службы и отправить по электронной почте. toolearn Подробнее об использовании функций Azure в приложениях см. в разделе hello следующие вопросы: 

- [Советы и рекомендации для функций Azure](functions-best-practices.md) приведены некоторые советы и рекомендации toouse при создании функций Azure.

- [Руководство для разработчиков по Функциям Azure](functions-reference.md). Справочник программиста по созданию функций, а также определению триггеров и привязок.

- [Тестирование функций Azure](functions-test-a-function.md). Описание различных средств и методов тестирования функций.