---
title: "hello toouse aaaHow SendGrid службы электронной почты (Node.js) | Документы Microsoft"
description: "Узнайте, как отправлять сообщения электронной почты с hello SendGrid службы электронной почты в Azure. Примеры, написанные с использованием hello Node.js API кода."
services: 
documentationcenter: nodejs
author: erikre
manager: wpickett
editor: 
ms.assetid: cac444b4-26b0-45ea-9c3d-eca28d57dacb
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 01/05/2016
ms.author: erikre
ms.openlocfilehash: fd617b6aaa656e7b5dd51c51ebb0db1e848450f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-nodejs"></a>Как tooSend электронной почты с помощью SendGrid из Node.js
В этом руководстве показано, как tooperform часто встречающиеся задачи программирования с помощью SendGrid электронной почты службы в Azure. образцы Hello записываются с помощью Node.js API hello. Hello сценарии включают **построении электронной почты**, **отправке сообщения электронной почты**, **Добавление вложений**, **с помощью фильтров**и **обновление свойств**. Дополнительные сведения о SendGrid и отправке сообщения электронной почты см. в разделе hello [дальнейшие действия](#next-steps) раздела.

## <a name="what-is-hello-sendgrid-email-service"></a>Что такое hello SendGrid службы электронной почты?
SendGrid — это [облачная служба электронной почты], которая обеспечивает надежную [доставку транзакционных писем], предоставляет возможности масштабирования и аналитики в реальном времени, а также предоставляет гибкие интерфейсы API для пользовательской интеграции. Ниже перечислены наиболее распространенные сценарии использования SendGrid.

* Отправлять уведомления toocustomers автоматически
* Администрирование списков рассылки для ежемесячной отправки клиентам электронных листовок и специальных предложений
* Сбор показателей в режиме реального времени по таким параметрам, как заблокированная электронная почта и реагирование клиентов
* Создание отчетов с тенденциями toohelp
* Пересылка запросов клиентов
* Уведомления от приложения по электронной почте

Дополнительные сведения см. на веб-сайте [https://sendgrid.com](https://sendgrid.com).

## <a name="create-a-sendgrid-account"></a>Создание учетной записи SendGrid
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-nodejs-module"></a>Справочник по hello модуль Node.js SendGrid
модуль SendGrid приветствия для Node.js можно устанавливать с помощью диспетчера пакетов node hello (npm-файл) с помощью hello следующую команду:

    npm install sendgrid

После установки может потребоваться hello модуля в приложении с помощью hello, следующий код:

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

экспортируемые модулем SendGrid Hello hello **SendGrid** и **электронной почты** функции.
**SendGrid** отвечает за отправку почты через SMTP или веб-API, а **Email** инкапсулирует электронное сообщение.

## <a name="how-to-create-an-email"></a>Практическое руководство. Создание сообщения эл. почты
Создание сообщения электронной почты, с помощью модуля SendGrid hello включает в себя сначала создается сообщение электронной почты с помощью функции hello электронной почты и последующей отправки с помощью функции hello SendGrid. Hello ниже приведен пример создания нового сообщения с помощью функции hello электронной почты:

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

Можно также указать сообщение в формате HTML для клиентов, поддерживающих ее, задав свойству hello html. Например:

    html: This is a sample <b>HTML<b> email message.

Задание оба свойства text и html hello обеспечивает корректное переход к текстовое содержимое для клиентов, не поддерживающие сообщения в формате HTML.

Дополнительные сведения о всех свойствах, поддерживаемых hello функции электронной почты см. в разделе [sendgrid nodejs][sendgrid-nodejs].

## <a name="how-to-send-an-email"></a>Практическое руководство. Отправка сообщения эл. почты
После создания сообщения электронной почты через hello функции электронной почты, можно отправить его с помощью веб-API, предоставляемые SendGrid hello. 

### <a name="web-api"></a>Веб-интерфейс API
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> А hello выше примерах показывает передачи в объект и обратным вызовом функции электронной почты, можно также непосредственно вызвать функции отправки hello путем указания свойства по электронной почте непосредственно. Например:  
> 
> `````
> sendgrid.send({
> to: 'john@contoso.com',
> from: 'anna@contoso.com',
> subject: 'test mail',
> text: 'This is a sample email message.'
> });
> `````
> 
> 

## <a name="how-to-add-an-attachment"></a>Практическое руководство. Добавление вложения
Можно добавлять вложения tooa сообщения, указав hello имена файлов или путь к диску в hello **файлы** свойство. Привет, следующий пример демонстрирует отправку вложения:

    sendgrid.send({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.',
        files: [
            {
                filename:     '',           // required only if file.content is used.
                contentType:  '',           // optional
                cid:          '',           // optional, used toospecify cid for inline content
                path:         '',           //
                url:          '',           // == One of these three options is required
                content:      ('' | Buffer) //
            }
        ],
    });

> [!NOTE]
> При использовании hello **файлы** свойства hello файл должен быть доступен через [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile). Если hello файла tooattach находится в хранилище Azure, например в контейнер больших двоичных объектов, необходимо сначала скопировать хранения toolocal файлов hello или tooan диск Azure перед отправкой во вложении, с помощью hello **файлы** свойство.
> 
> 

## <a name="how-to-use-filters-tooenable-footers-and-tracking"></a>Как: использовать фильтры tooEnable нижние колонтитулы и отслеживания
SendGrid предоставляет функциональные возможности дополнительный адрес электронной почты с использованием hello фильтров. Это параметры, которые могут быть добавлены tooan сообщение электронной почты для включения определенных функций, таких как включение отслеживание щелчков, Google analytics, отслеживание, подписки и т. д. Полный список фильтров см. в разделе [Filter Settings][Filter Settings] (Параметры фильтрации).

Фильтры могут быть применен tooa сообщения с помощью hello **фильтры** свойство.
Каждый фильтр определяется хэшем, содержащим параметры, которые связаны с данным конкретным фильтром.
Hello следующие примеры демонстрируют hello нижний колонтитул и выберите отслеживания фильтры:

### <a name="footer"></a>Нижний колонтитул
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'footer': {
            'settings': {
                'enable': 1,
                'text/plain': 'This is a text footer.'
            }
        }
    });

    sendgrid.send(email);

### <a name="click-tracking"></a>Отслеживание щелчков
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'clicktrack': {
            'settings': {
                'enable': 1
            }
        }
    });

    sendgrid.send(email);

## <a name="how-to-update-email-properties"></a>Практическое руководство. Обновление свойств электронной почты
Некоторые свойства электронной почты может быть перезаписана с помощью  **задать*свойство*** или добавляться с помощью  **добавить*свойство***. Например, вы можете добавить дополнительных получателей с помощью

    email.addTo('jeff@contoso.com');

или задать фильтр с помощью

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

Дополнительные сведения см. в разделе [sendgrid nodejs][sendgrid-nodejs].

## <a name="how-to-use-additional-sendgrid-services"></a>Практическое руководство. Использование дополнительных служб SendGrid
SendGrid предлагает веб-API можно использовать дополнительные возможности SendGrid tooleverage из приложения Azure. Дополнительные сведения см. в разделе hello [документации по SendGrid API][SendGrid API documentation].

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello hello служба SendGrid электронной почты, выполните следующие дополнительные toolearn ссылки.

* Репозитории модулей SendGrid Node.js: [sendgrid nodejs][sendgrid-nodejs]
* Документация по интерфейсу API SendGrid: <https://sendgrid.com/docs>
* Специальное предложение SendGrid для клиентов Azure: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[облачная служба электронной почты]: https://sendgrid.com/email-solutions
[доставку транзакционных писем]: https://sendgrid.com/transactional-email
