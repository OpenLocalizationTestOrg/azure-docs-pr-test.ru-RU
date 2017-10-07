---
title: "hello toouse aaaHow SendGrid службы электронной почты (.NET) | Документы Microsoft"
description: "Узнайте, как отправлять сообщения электронной почты с hello SendGrid службы электронной почты в Azure. Примеры кода, написанного на C# и используйте hello .NET API."
services: app-service-web
documentationcenter: .net
author: thinkingserious
manager: erikre
editor: 
ms.assetid: 21bf4028-9046-476b-9799-3d3082a0f84c
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/15/2017
ms.author: dx@sendgrid.com
ms.openlocfilehash: b3d77bb67898b991c7293e6b9086b263f6bcb755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-with-azure"></a>Как tooSend SendGrid с помощью электронной почты с помощью Azure
## <a name="overview"></a>Обзор
В этом руководстве показано, как tooperform часто встречающиеся задачи программирования с помощью SendGrid электронной почты службы в Azure. Hello примеры на языке C\# и поддерживает .NET Standard 1.3. Hello сценарии включают создание электронной почты, отправка электронной почты, добавление вложений и включение различных почты и параметры отслеживания. Дополнительные сведения о SendGrid и отправке сообщения электронной почты см. в разделе hello [дальнейшие действия] [ Next steps] раздела.

## <a name="what-is-hello-sendgrid-email-service"></a>Что такое hello SendGrid службы электронной почты?
SendGrid — это [облачная служба электронной почты], которая обеспечивает надежную [доставку транзакционных писем], предоставляет возможности масштабирования и аналитики в реальном времени, а также предоставляет гибкие интерфейсы API для пользовательской интеграции. Наиболее распространенные варианты использования SendGrid:

* Автоматически отправляет уведомления или toocustomers подтверждений покупки.
* Администрирование списков рассылки для ежемесячной отправки клиентам рекламных листовок и рекламы.
* Сбор метрик в реальном времени по таким параметрам, как заблокированная электронная почта и взаимодействие с клиентами.
* Пересылка запросов клиентов.
* Обработка входящих сообщений электронной почты.

Для получения дополнительной информации посетите [https://sendgrid.com](https://sendgrid.com) или репозиторий GitHub [библиотек C#][sendgrid-csharp] для SendGrid.

## <a name="create-a-sendgrid-account"></a>Создание учетной записи SendGrid
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-net-class-library"></a>Справочник по hello SendGrid библиотеки классов .NET
Hello [пакет NuGet для SendGrid](https://www.nuget.org/packages/Sendgrid) является hello простым способом tooget hello SendGrid API и tooconfigure приложения со всеми зависимостями. NuGet является Visual Studio расширения, включенные с помощью Microsoft Visual Studio 2015 и более поздних версий, который позволяет легко tooinstall и обновление библиотек и средств.

> [!NOTE]
> При запуске в версии Visual Studio до Visual Studio 2015, посетите tooinstall NuGet [http://www.nuget.org](http://www.nuget.org)и нажмите кнопку hello **установить NuGet** кнопки.
>
>

hello tooinstall пакет NuGet для SendGrid в вашем приложении hello следующие:

1. Щелкните **Новый проект** и выберите **Шаблон**.

   ![Создание нового проекта][create-new-project]
2. В **обозревателе решений** щелкните правой кнопкой мыши **Ссылки**, а затем выберите **Управление пакетами NuGet**.

   ![Пакет SendGrid NuGet][SendGrid-NuGet-package]
3. Поиск **SendGrid** и выберите hello **SendGrid** элемент в списке результатов.
4. Выберите hello последняя стабильная версия пакета Nuget hello hello версии раскрывающийся список toobe может toowork hello объектную модель и API-интерфейсы, описанные в этой статье.

   ![Пакет SendGrid][sendgrid-package]
5. Нажмите кнопку **установить** toocomplete hello установки, а затем закройте это диалоговое окно.

Библиотека классов SendGrid .NET называется **SendGrid**. Он содержит следующие пространства имен hello:

* **SendGrid** для взаимодействия с API SendGrid.
* **SendGrid.Helpers.Mail** для вспомогательного метода tooeasily методы создания SendGridMessage объекты, которые указывают, каким образом toosend отправляется сообщение электронной почты.

Добавьте следующий код пространство имен объявления toohello начало любого файла C# в которой требуется служба электронной почты SendGrid hello доступа tooprogrammatically hello.

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a>Практическое руководство. Создание сообщения эл. почты
Используйте hello **SendGridMessage** объекта toocreate сообщение электронной почты. После создания объекта сообщения hello, можно задать свойства и методы, включая hello отправителю сообщения электронной почты, получателю сообщения hello и hello темы и текст hello электронной почты.

Hello следующем примере показано, как toocreate объект полностью заполненный электронной почты:

    var msg = new SendGridMessage();

    msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

    var recipients = new List<EmailAddress>
    {
        new EmailAddress("jeff@example.com", "Jeff Smith"),
        new EmailAddress("anna@example.com", "Anna Lidman"),
        new EmailAddress("peter@example.com", "Peter Saddow")
    };
    msg.AddTos(recipients);

    msg.SetSubject("Testing hello SendGrid C# Library");

    msg.AddContent(MimeType.Text, "Hello World plain text!");
    msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

Дополнительные сведения о всех свойствах и методах, поддерживаемых типом **SendGrid**, см. в разделе [sendgrid-csharp][sendgrid-csharp] на портале GitHub.

## <a name="how-to-send-an-email"></a>Практическое руководство. Отправка сообщения эл. почты
После создания сообщения электронной почты его можно отправить с помощью API SendGrid. Можно также воспользоваться [встроенной библиотекой .NET][NET-library].

Чтобы отправить электронное сообщение, необходимо указать ключ API SendGrid. При необходимости сведения о том, как tooconfigure ключи API посетите ключи API SendGrid [документации][documentation].

Эти учетные данные могут быть сохранены на портале Azure, выбрав параметры приложения и добавление пары ключ значение hello в разделе параметров приложения.

 ![Параметры приложения Azure][azure_app_settings]

 После этого обращаться к ним можно следующим образом.

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

Привет, следующие примеры показывают, как сообщения с помощью toosend hello веб-API.

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
                    Subject = "Hello World from hello SendGrid CSharp SDK!",
                    PlainTextContent = "Hello, Email!",
                    HtmlContent = "<strong>Hello, Email!</strong>"
                };
                msg.AddTo(new EmailAddress("test@example.com", "Test User"));
                var response = await client.SendEmailAsync(msg);
            }
        }
    }

## <a name="how-to-add-an-attachment"></a>Практическое руководство. Добавление вложения
Вложения могут быть добавлены tooa сообщения вызывающему Привет **AddAttachment** метод и как минимум, указав имя файла hello и кодировке Base64 содержимого вы хотите tooattach. Можно включить несколько вложений, путем вызова данного метода, когда для каждого файла нужно tooattach или с помощью hello **AddAttachments** метод. Привет, в следующем примере показано, как добавить сообщение tooa вложения:

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-tooenable-footers-tracking-and-analytics"></a>Как: используйте нижние колонтитулы tooenable параметры почты, отслеживания и аналитика
SendGrid предоставляет функциональные возможности дополнительный адрес электронной почты с использованием hello параметры почты и отслеживания. Эти параметры могут быть добавлены tooan по электронной почте сообщение tooenable определенных функций, например отслеживание щелчков, Google analytics, отслеживания подписки и т. д. Полный список приложений см. в разделе hello [документацию параметров][settings-documentation].

Приложения могут применяться слишком**SendGrid** по электронной почте, с помощью методов, реализованных в рамках hello **SendGridMessage** класса. Hello следующие примеры демонстрируют hello нижний колонтитул и выберите отслеживания фильтры:

Hello следующие примеры демонстрируют hello нижний колонтитул и выберите отслеживания фильтры:

### <a name="footer-settings"></a>Параметры нижнего колонтитула
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a>Отслеживание щелчков
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a>Практическое руководство. Использование дополнительных служб SendGrid
SendGrid предлагает несколько интерфейсов API и веб-привязок, можно использовать дополнительные функциональные возможности tooleverage внутри приложения Azure. Дополнительные сведения см. в разделе hello [Справочник по API SendGrid][SendGrid API documentation].

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello hello служба SendGrid электронной почты, выполните следующие дополнительные toolearn ссылки.

* Репозиторий библиотек C\# для SendGrid: [sendgrid-csharp][sendgrid-csharp]
* Документация по интерфейсу API SendGrid: <https://sendgrid.com/docs>

[Next steps]: #next-steps
[What is hello SendGrid Email Service?]: #whatis
[Create a SendGrid Account]: #createaccount
[Reference hello SendGrid .NET Class Library]: #reference
[How to: Create an Email]: #createemail
[How to: Send an Email]: #sendemail
[How to: Add an Attachment]: #addattachment
[How to: Use Filters tooEnable Footers, Tracking, and Analytics]: #usefilters
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

