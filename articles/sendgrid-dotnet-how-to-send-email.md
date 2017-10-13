---
title: "Использование службы электронной почты SendGrid (.NET) | Документация Майкрософт"
description: "Узнайте, как отправить электронное сообщение с помощью службы электронной почты SendGrid в Azure. Примеры написаны на языке C# и используют API .NET."
services: 
documentationcenter: .net
author: thinkingserious
manager: erikre
editor: 
ms.assetid: 21bf4028-9046-476b-9799-3d3082a0f84c
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/15/2017
ms.author: dx@sendgrid.com
ms.openlocfilehash: 14161a0747add43a99e301eacf700ab79c77c767
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-send-email-using-sendgrid-with-azure"></a>Как отправлять электронную почту с помощью SendGrid и Azure
## <a name="overview"></a>Обзор
В этом руководстве показано, как выполнять типовые задачи программирования для службы электронной почты SendGrid в Azure. Примеры написаны на языке C\# и поддерживают .NET Standard 1.3. Здесь описываются сценарии создания электронного сообщения, его отправки, добавления вложений и включения различных параметров электронной почты и отслеживания. Дополнительные сведения о SendGrid и отправке электронной почты см. в разделе [Дальнейшие действия][Next steps].

## <a name="what-is-the-sendgrid-email-service"></a>Что такое служба электронной почты SendGrid?
SendGrid — это [облачная служба электронной почты], которая обеспечивает надежную [доставку транзакционных писем], предоставляет возможности масштабирования и аналитики в реальном времени, а также предоставляет гибкие интерфейсы API для пользовательской интеграции. Наиболее распространенные варианты использования SendGrid:

* Автоматическая отправка клиентам квитанций или сообщений о подтверждении покупки.
* Администрирование списков рассылки для ежемесячной отправки клиентам рекламных листовок и рекламы.
* Сбор метрик в реальном времени по таким параметрам, как заблокированная электронная почта и взаимодействие с клиентами.
* Пересылка запросов клиентов.
* Обработка входящих сообщений электронной почты.

Для получения дополнительной информации посетите [https://sendgrid.com](https://sendgrid.com) или репозиторий GitHub [библиотек C#][sendgrid-csharp] для SendGrid.

## <a name="create-a-sendgrid-account"></a>Создание учетной записи SendGrid
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-the-sendgrid-net-class-library"></a>Справочник по библиотеке классов SendGrid .NET
[Пакет SendGrid NuGet](https://www.nuget.org/packages/Sendgrid) — это самый простой способ получить интерфейс API службы SendGrid и настроить свое приложение с учетом всех зависимостей. Пакет NuGet — это расширение Visual Studio, включенное в Microsoft Visual Studio 2015 в более поздние версии, которое упрощает установку и обновление библиотек и инструментов.

> [!NOTE]
> Чтобы установить пакет NuGet, если вы используете версию Visual Studio, предшествующую Visual Studio 2015, посетите сайт [http://www.nuget.org](http://www.nuget.org)и нажмите кнопку **Установить NuGet** .
>
>

Для установки пакета SendGrid NuGet в приложении выполните следующие действия:

1. Щелкните **Новый проект** и выберите **Шаблон**.

   ![Создание нового проекта][create-new-project]
2. В **обозревателе решений** щелкните правой кнопкой мыши **Ссылки**, а затем выберите **Управление пакетами NuGet**.

   ![Пакет SendGrid NuGet][SendGrid-NuGet-package]
3. Выполните поиск **SendGrid** и выберите элемент **SendGrid** в списке результатов.
4. Выберите последнюю стабильную версию пакета NuGet из раскрывающегося списка версий, чтобы иметь возможность работать с объектной моделью и интерфейсами API, описанными в этой статье.

   ![Пакет SendGrid][sendgrid-package]
5. Нажмите кнопку **Установить** , чтобы выполнить установку, а затем закройте диалоговое окно.

Библиотека классов SendGrid .NET называется **SendGrid**. Она содержит такие пространства имен:

* **SendGrid** для взаимодействия с API SendGrid.
* **SendGrid.Helpers.Mail** для вспомогательных методов, используемых для создания объектов SendGridMessage, определяющих способ отправки электронных сообщений.

Добавьте следующие объявления пространств имен кода в начало любого файла C#, в котором вы собираетесь получать доступ к хранилищу службы электронной почты SendGrid программным способом.

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a>Практическое руководство. Создание сообщения эл. почты
Для создания сообщения электронной почты используется объект **SendGridMessage** . После создания объекта сообщения можно задать свойства и методы, включая отправителя и получателя электронной почты, тему и текст сообщения.

В следующем примере показано, как создать полностью заполненный объект электронной почты.

    var msg = new SendGridMessage();

    msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

    var recipients = new List<EmailAddress>
    {
        new EmailAddress("jeff@example.com", "Jeff Smith"),
        new EmailAddress("anna@example.com", "Anna Lidman"),
        new EmailAddress("peter@example.com", "Peter Saddow")
    };
    msg.AddTos(recipients);

    msg.SetSubject("Testing the SendGrid C# Library");

    msg.AddContent(MimeType.Text, "Hello World plain text!");
    msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

Дополнительные сведения о всех свойствах и методах, поддерживаемых типом **SendGrid**, см. в разделе [sendgrid-csharp][sendgrid-csharp] на портале GitHub.

## <a name="how-to-send-an-email"></a>Практическое руководство. Отправка сообщения эл. почты
После создания сообщения электронной почты его можно отправить с помощью API SendGrid. Можно также воспользоваться [встроенной библиотекой .NET][NET-library].

Чтобы отправить электронное сообщение, необходимо указать ключ API SendGrid. Если требуются сведения о том, как настроить ключи API SendGrid, ознакомьтесь с нашей [документацией по ключам API SendGrid][documentation].

Вы можете сохранить эти учетные данные с помощью портала Azure, щелкнув "Параметры приложения" и добавив пары "ключ-значение" в разделе "Параметры приложения".

 ![Параметры приложения Azure][azure_app_settings]

 После этого обращаться к ним можно следующим образом.

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

В следующих примерах показано, как отправить сообщение с помощью веб-API.

    using System;
    using System.Threading.Tasks;
    using SendGrid;
    using SendGrid.Helpers.Mail;

    namespace Example
    {
        internal class Example
        {
            private static void Main()
            {
                Execute().Wait();
            }

            static async Task Execute()
            {
                var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
                var client = new SendGridClient(apiKey);
                var msg = new SendGridMessage()
                {
                    From = new EmailAddress("test@example.com", "DX Team"),
                    Subject = "Hello World from the SendGrid CSharp SDK!",
                    PlainTextContent = "Hello, Email!",
                    HtmlContent = "<strong>Hello, Email!</strong>"
                };
                msg.AddTo(new EmailAddress("test@example.com", "Test User"));
                var response = await client.SendEmailAsync(msg);
            }
        }
    }

## <a name="how-to-add-an-attachment"></a>Практическое руководство. Добавление вложения
Чтобы добавить вложение в сообщение, вызовите метод **AddAttachment** и по крайней мере укажите имя файла и содержимое в кодировке Base64 для вложения. Можно добавить несколько вложений, вызывая этот метод для каждого вкладываемого файла. Можно также использовать метод **AddAttachments**. На приведенном ниже примере продемонстрировано добавление вложения в сообщение.

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-to-enable-footers-tracking-and-analytics"></a>Практическое руководство. Использование параметров почты для добавления нижних колонтитулов, отслеживания и аналитики
SendGrid обеспечивает дополнительные функции электронной почты благодаря использованию параметров почты и отслеживания. Эти параметры можно добавлять в сообщения для включения определенных функций, например отслеживания щелчков, аналитики Google, отслеживания подписок и т. п. Полный список приложений приведен в [документации по параметрам][settings-documentation].

Приложения можно использовать в электронных сообщениях **SendGrid** с помощью методов, реализованных в рамках класса **SendGridMessage**. В следующих примерах показаны фильтры нижних колонтитулов и отслеживания щелчков:

В следующих примерах показаны фильтры нижних колонтитулов и отслеживания щелчков:

### <a name="footer-settings"></a>Параметры нижнего колонтитула
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a>Отслеживание щелчков
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a>Практическое руководство. Использование дополнительных служб SendGrid
SendGrid предоставляет несколько интерфейсов API и объектов webhook, с помощью которых в своем приложении Azure можно использовать дополнительные функции. Дополнительные сведения см. в [справочнике по API SendGrid][SendGrid API documentation].

## <a name="next-steps"></a>Дальнейшие действия
Вы получили основные сведения о службе доставки электронной почты SendGrid. Дополнительные сведения вы найдете по следующим ссылкам.

* Репозиторий библиотек C\# для SendGrid: [sendgrid-csharp][sendgrid-csharp]
* Документация по интерфейсу API SendGrid: <https://sendgrid.com/docs>

[Next steps]: #next-steps
[What is the SendGrid Email Service?]: #whatis
[Create a SendGrid Account]: #createaccount
[Reference the SendGrid .NET Class Library]: #reference
[How to: Create an Email]: #createemail
[How to: Send an Email]: #sendemail
[How to: Add an Attachment]: #addattachment
[How to: Use Filters to Enable Footers, Tracking, and Analytics]: #usefilters
[How to: Use Additional SendGrid Services]: #useservices

[create-new-project]: ./media/sendgrid-dotnet-how-to-send-email/new-project.png
[SendGrid-NuGet-package]: ./media/sendgrid-dotnet-how-to-send-email/reference.png
[sendgrid-package]: ./media/sendgrid-dotnet-how-to-send-email/sendgrid-package.png
[azure_app_settings]: ./media/sendgrid-dotnet-how-to-send-email/azure-app-settings.png
[sendgrid-csharp]: https://github.com/sendgrid/sendgrid-csharp
[SMTP vs. Web API]: https://sendgrid.com/docs/Integrate/index.html
[App Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/api_v3.html
[NET-library]: https://sendgrid.com/docs/Integrate/Code_Examples/v2_Mail/csharp.html#-Using-NETs-Builtin-SMTP-Library
[documentation]: https://sendgrid.com/docs/Classroom/Send/api_keys.html
[settings-documentation]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html

[облачная служба электронной почты]: https://sendgrid.com/solutions
[доставку транзакционных писем]: https://sendgrid.com/use-cases/transactional-email

