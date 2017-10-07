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
# <a name="how-toosend-email-using-sendgrid-with-azure"></a><span data-ttu-id="f88f4-104">Как tooSend SendGrid с помощью электронной почты с помощью Azure</span><span class="sxs-lookup"><span data-stu-id="f88f4-104">How tooSend Email Using SendGrid with Azure</span></span>
## <a name="overview"></a><span data-ttu-id="f88f4-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="f88f4-105">Overview</span></span>
<span data-ttu-id="f88f4-106">В этом руководстве показано, как tooperform часто встречающиеся задачи программирования с помощью SendGrid электронной почты службы в Azure.</span><span class="sxs-lookup"><span data-stu-id="f88f4-106">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="f88f4-107">Hello примеры на языке C\# и поддерживает .NET Standard 1.3.</span><span class="sxs-lookup"><span data-stu-id="f88f4-107">hello samples are written in C\# and supports .NET Standard 1.3.</span></span> <span data-ttu-id="f88f4-108">Hello сценарии включают создание электронной почты, отправка электронной почты, добавление вложений и включение различных почты и параметры отслеживания.</span><span class="sxs-lookup"><span data-stu-id="f88f4-108">hello scenarios covered include constructing email, sending email, adding attachments, and enabling various mail and tracking settings.</span></span> <span data-ttu-id="f88f4-109">Дополнительные сведения о SendGrid и отправке сообщения электронной почты см. в разделе hello [дальнейшие действия] [ Next steps] раздела.</span><span class="sxs-lookup"><span data-stu-id="f88f4-109">For more information on SendGrid and sending email, see hello [Next steps][Next steps] section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="f88f4-110">Что такое hello SendGrid службы электронной почты?</span><span class="sxs-lookup"><span data-stu-id="f88f4-110">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="f88f4-111">SendGrid — это [облачная служба электронной почты], которая обеспечивает надежную [доставку транзакционных писем], предоставляет возможности масштабирования и аналитики в реальном времени, а также предоставляет гибкие интерфейсы API для пользовательской интеграции.</span><span class="sxs-lookup"><span data-stu-id="f88f4-111">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="f88f4-112">Наиболее распространенные варианты использования SendGrid:</span><span class="sxs-lookup"><span data-stu-id="f88f4-112">Common SendGrid use cases include:</span></span>

* <span data-ttu-id="f88f4-113">Автоматически отправляет уведомления или toocustomers подтверждений покупки.</span><span class="sxs-lookup"><span data-stu-id="f88f4-113">Automatically sending receipts or purchase confirmations toocustomers.</span></span>
* <span data-ttu-id="f88f4-114">Администрирование списков рассылки для ежемесячной отправки клиентам рекламных листовок и рекламы.</span><span class="sxs-lookup"><span data-stu-id="f88f4-114">Administering distribution lists for sending customers monthly fliers and promotions.</span></span>
* <span data-ttu-id="f88f4-115">Сбор метрик в реальном времени по таким параметрам, как заблокированная электронная почта и взаимодействие с клиентами.</span><span class="sxs-lookup"><span data-stu-id="f88f4-115">Collecting real-time metrics for things like blocked email and customer engagement.</span></span>
* <span data-ttu-id="f88f4-116">Пересылка запросов клиентов.</span><span class="sxs-lookup"><span data-stu-id="f88f4-116">Forwarding customer inquiries.</span></span>
* <span data-ttu-id="f88f4-117">Обработка входящих сообщений электронной почты.</span><span class="sxs-lookup"><span data-stu-id="f88f4-117">Processing incoming emails.</span></span>

<span data-ttu-id="f88f4-118">Для получения дополнительной информации посетите [https://sendgrid.com](https://sendgrid.com) или репозиторий GitHub [библиотек C#][sendgrid-csharp] для SendGrid.</span><span class="sxs-lookup"><span data-stu-id="f88f4-118">For more information, visit [https://sendgrid.com](https://sendgrid.com) or SendGrid's [C# library][sendgrid-csharp] GitHub repo.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="f88f4-119">Создание учетной записи SendGrid</span><span class="sxs-lookup"><span data-stu-id="f88f4-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-net-class-library"></a><span data-ttu-id="f88f4-120">Справочник по hello SendGrid библиотеки классов .NET</span><span class="sxs-lookup"><span data-stu-id="f88f4-120">Reference hello SendGrid .NET Class Library</span></span>
<span data-ttu-id="f88f4-121">Hello [пакет NuGet для SendGrid](https://www.nuget.org/packages/Sendgrid) является hello простым способом tooget hello SendGrid API и tooconfigure приложения со всеми зависимостями.</span><span class="sxs-lookup"><span data-stu-id="f88f4-121">hello [SendGrid NuGet package](https://www.nuget.org/packages/Sendgrid) is hello easiest way tooget hello SendGrid API and tooconfigure your application with all dependencies.</span></span> <span data-ttu-id="f88f4-122">NuGet является Visual Studio расширения, включенные с помощью Microsoft Visual Studio 2015 и более поздних версий, который позволяет легко tooinstall и обновление библиотек и средств.</span><span class="sxs-lookup"><span data-stu-id="f88f4-122">NuGet is a Visual Studio extension included with Microsoft Visual Studio 2015 and above that makes it easy tooinstall and update libraries and tools.</span></span>

> [!NOTE]
> <span data-ttu-id="f88f4-123">При запуске в версии Visual Studio до Visual Studio 2015, посетите tooinstall NuGet [http://www.nuget.org](http://www.nuget.org)и нажмите кнопку hello **установить NuGet** кнопки.</span><span class="sxs-lookup"><span data-stu-id="f88f4-123">tooinstall NuGet if you are running a version of Visual Studio earlier than Visual Studio 2015, visit [http://www.nuget.org](http://www.nuget.org), and click hello **Install NuGet** button.</span></span>
>
>

<span data-ttu-id="f88f4-124">hello tooinstall пакет NuGet для SendGrid в вашем приложении hello следующие:</span><span class="sxs-lookup"><span data-stu-id="f88f4-124">tooinstall hello SendGrid NuGet package in your application, do hello following:</span></span>

1. <span data-ttu-id="f88f4-125">Щелкните **Новый проект** и выберите **Шаблон**.</span><span class="sxs-lookup"><span data-stu-id="f88f4-125">Click on **New Project** and select a **Template**.</span></span>

   ![Создание нового проекта][create-new-project]
2. <span data-ttu-id="f88f4-127">В **обозревателе решений** щелкните правой кнопкой мыши **Ссылки**, а затем выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f88f4-127">In **Solution Explorer**, right-click **References**, then click **Manage NuGet Packages**.</span></span>

   ![Пакет SendGrid NuGet][SendGrid-NuGet-package]
3. <span data-ttu-id="f88f4-129">Поиск **SendGrid** и выберите hello **SendGrid** элемент в списке результатов.</span><span class="sxs-lookup"><span data-stu-id="f88f4-129">Search for **SendGrid** and select hello **SendGrid** item in the results list.</span></span>
4. <span data-ttu-id="f88f4-130">Выберите hello последняя стабильная версия пакета Nuget hello hello версии раскрывающийся список toobe может toowork hello объектную модель и API-интерфейсы, описанные в этой статье.</span><span class="sxs-lookup"><span data-stu-id="f88f4-130">Select hello latest stable version of hello Nuget package from hello version dropdown toobe able toowork with hello object model and APIs demonstrated in this article.</span></span>

   ![Пакет SendGrid][sendgrid-package]
5. <span data-ttu-id="f88f4-132">Нажмите кнопку **установить** toocomplete hello установки, а затем закройте это диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="f88f4-132">Click **Install** toocomplete hello installation, and then close this dialog.</span></span>

<span data-ttu-id="f88f4-133">Библиотека классов SendGrid .NET называется **SendGrid**.</span><span class="sxs-lookup"><span data-stu-id="f88f4-133">SendGrid's .NET class library is called **SendGrid**.</span></span> <span data-ttu-id="f88f4-134">Он содержит следующие пространства имен hello:</span><span class="sxs-lookup"><span data-stu-id="f88f4-134">It contains hello following namespaces:</span></span>

* <span data-ttu-id="f88f4-135">**SendGrid** для взаимодействия с API SendGrid.</span><span class="sxs-lookup"><span data-stu-id="f88f4-135">**SendGrid** for communicating with SendGrid’s API.</span></span>
* <span data-ttu-id="f88f4-136">**SendGrid.Helpers.Mail** для вспомогательного метода tooeasily методы создания SendGridMessage объекты, которые указывают, каким образом toosend отправляется сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="f88f4-136">**SendGrid.Helpers.Mail** for helper methods tooeasily create SendGridMessage objects that specify how toosend emails.</span></span>

<span data-ttu-id="f88f4-137">Добавьте следующий код пространство имен объявления toohello начало любого файла C# в которой требуется служба электронной почты SendGrid hello доступа tooprogrammatically hello.</span><span class="sxs-lookup"><span data-stu-id="f88f4-137">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access hello SendGrid email service.</span></span>

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a><span data-ttu-id="f88f4-138">Практическое руководство. Создание сообщения эл. почты</span><span class="sxs-lookup"><span data-stu-id="f88f4-138">How to: Create an Email</span></span>
<span data-ttu-id="f88f4-139">Используйте hello **SendGridMessage** объекта toocreate сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="f88f4-139">Use hello **SendGridMessage** object toocreate an email message.</span></span> <span data-ttu-id="f88f4-140">После создания объекта сообщения hello, можно задать свойства и методы, включая hello отправителю сообщения электронной почты, получателю сообщения hello и hello темы и текст hello электронной почты.</span><span class="sxs-lookup"><span data-stu-id="f88f4-140">Once hello message object is created, you can set properties and methods, including hello email sender, hello email recipient, and hello subject and body of hello email.</span></span>

<span data-ttu-id="f88f4-141">Hello следующем примере показано, как toocreate объект полностью заполненный электронной почты:</span><span class="sxs-lookup"><span data-stu-id="f88f4-141">hello following example demonstrates how toocreate a fully populated email object:</span></span>

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

<span data-ttu-id="f88f4-142">Дополнительные сведения о всех свойствах и методах, поддерживаемых типом **SendGrid**, см. в разделе [sendgrid-csharp][sendgrid-csharp] на портале GitHub.</span><span class="sxs-lookup"><span data-stu-id="f88f4-142">For more information on all properties and methods supported by the **SendGrid** type, see [sendgrid-csharp][sendgrid-csharp] on GitHub.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="f88f4-143">Практическое руководство. Отправка сообщения эл. почты</span><span class="sxs-lookup"><span data-stu-id="f88f4-143">How to: Send an Email</span></span>
<span data-ttu-id="f88f4-144">После создания сообщения электронной почты его можно отправить с помощью API SendGrid.</span><span class="sxs-lookup"><span data-stu-id="f88f4-144">After creating an email message, you can send it using SendGrid's API.</span></span> <span data-ttu-id="f88f4-145">Можно также воспользоваться [встроенной библиотекой .NET][NET-library].</span><span class="sxs-lookup"><span data-stu-id="f88f4-145">Alternatively, you may use [.NET's built in library][NET-library].</span></span>

<span data-ttu-id="f88f4-146">Чтобы отправить электронное сообщение, необходимо указать ключ API SendGrid.</span><span class="sxs-lookup"><span data-stu-id="f88f4-146">Sending email requires that you supply your SendGrid API Key.</span></span> <span data-ttu-id="f88f4-147">При необходимости сведения о том, как tooconfigure ключи API посетите ключи API SendGrid [документации][documentation].</span><span class="sxs-lookup"><span data-stu-id="f88f4-147">If you need details about how tooconfigure API Keys, please visit SendGrid's API Keys [documentation][documentation].</span></span>

<span data-ttu-id="f88f4-148">Эти учетные данные могут быть сохранены на портале Azure, выбрав параметры приложения и добавление пары ключ значение hello в разделе параметров приложения.</span><span class="sxs-lookup"><span data-stu-id="f88f4-148">You may store these credentials via your Azure Portal by clicking Application settings and adding hello key/value pairs under App settings.</span></span>

 ![Параметры приложения Azure][azure_app_settings]

 <span data-ttu-id="f88f4-150">После этого обращаться к ним можно следующим образом.</span><span class="sxs-lookup"><span data-stu-id="f88f4-150">Then, you may access them as follows:</span></span>

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

<span data-ttu-id="f88f4-151">Привет, следующие примеры показывают, как сообщения с помощью toosend hello веб-API.</span><span class="sxs-lookup"><span data-stu-id="f88f4-151">hello following examples show how toosend a message using hello Web API.</span></span>

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

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="f88f4-152">Практическое руководство. Добавление вложения</span><span class="sxs-lookup"><span data-stu-id="f88f4-152">How to: Add an attachment</span></span>
<span data-ttu-id="f88f4-153">Вложения могут быть добавлены tooa сообщения вызывающему Привет **AddAttachment** метод и как минимум, указав имя файла hello и кодировке Base64 содержимого вы хотите tooattach.</span><span class="sxs-lookup"><span data-stu-id="f88f4-153">Attachments can be added tooa message by calling hello **AddAttachment** method and minimally specifying hello file name and Base64 encoded content you want tooattach.</span></span> <span data-ttu-id="f88f4-154">Можно включить несколько вложений, путем вызова данного метода, когда для каждого файла нужно tooattach или с помощью hello **AddAttachments** метод.</span><span class="sxs-lookup"><span data-stu-id="f88f4-154">You can include multiple attachments by calling this method once for each file you wish tooattach or by using hello **AddAttachments** method.</span></span> <span data-ttu-id="f88f4-155">Привет, в следующем примере показано, как добавить сообщение tooa вложения:</span><span class="sxs-lookup"><span data-stu-id="f88f4-155">hello following example demonstrates adding an attachment tooa message:</span></span>

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="f88f4-156">Как: используйте нижние колонтитулы tooenable параметры почты, отслеживания и аналитика</span><span class="sxs-lookup"><span data-stu-id="f88f4-156">How to: Use mail settings tooenable footers, tracking, and analytics</span></span>
<span data-ttu-id="f88f4-157">SendGrid предоставляет функциональные возможности дополнительный адрес электронной почты с использованием hello параметры почты и отслеживания.</span><span class="sxs-lookup"><span data-stu-id="f88f4-157">SendGrid provides additional email functionality through hello use of mail settings and tracking settings.</span></span> <span data-ttu-id="f88f4-158">Эти параметры могут быть добавлены tooan по электронной почте сообщение tooenable определенных функций, например отслеживание щелчков, Google analytics, отслеживания подписки и т. д.</span><span class="sxs-lookup"><span data-stu-id="f88f4-158">These settings can be added tooan email message tooenable specific functionality such as click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="f88f4-159">Полный список приложений см. в разделе hello [документацию параметров][settings-documentation].</span><span class="sxs-lookup"><span data-stu-id="f88f4-159">For a full list of apps, see hello [Settings Documentation][settings-documentation].</span></span>

<span data-ttu-id="f88f4-160">Приложения могут применяться слишком**SendGrid** по электронной почте, с помощью методов, реализованных в рамках hello **SendGridMessage** класса.</span><span class="sxs-lookup"><span data-stu-id="f88f4-160">Apps can be applied too**SendGrid** email messages using methods implemented as part of hello **SendGridMessage** class.</span></span> <span data-ttu-id="f88f4-161">Hello следующие примеры демонстрируют hello нижний колонтитул и выберите отслеживания фильтры:</span><span class="sxs-lookup"><span data-stu-id="f88f4-161">hello following examples demonstrate hello footer and click tracking filters:</span></span>

<span data-ttu-id="f88f4-162">Hello следующие примеры демонстрируют hello нижний колонтитул и выберите отслеживания фильтры:</span><span class="sxs-lookup"><span data-stu-id="f88f4-162">hello following examples demonstrate hello footer and click tracking filters:</span></span>

### <a name="footer-settings"></a><span data-ttu-id="f88f4-163">Параметры нижнего колонтитула</span><span class="sxs-lookup"><span data-stu-id="f88f4-163">Footer settings</span></span>
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a><span data-ttu-id="f88f4-164">Отслеживание щелчков</span><span class="sxs-lookup"><span data-stu-id="f88f4-164">Click tracking</span></span>
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="f88f4-165">Практическое руководство. Использование дополнительных служб SendGrid</span><span class="sxs-lookup"><span data-stu-id="f88f4-165">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="f88f4-166">SendGrid предлагает несколько интерфейсов API и веб-привязок, можно использовать дополнительные функциональные возможности tooleverage внутри приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="f88f4-166">SendGrid offers several APIs and webhooks that you can use tooleverage additional functionality within your Azure application.</span></span> <span data-ttu-id="f88f4-167">Дополнительные сведения см. в разделе hello [Справочник по API SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="f88f4-167">For more details, see hello [SendGrid API Reference][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="f88f4-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f88f4-168">Next steps</span></span>
<span data-ttu-id="f88f4-169">Теперь, когда вы узнали основы hello hello служба SendGrid электронной почты, выполните следующие дополнительные toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="f88f4-169">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="f88f4-170">Репозиторий библиотек C\# для SendGrid: [sendgrid-csharp][sendgrid-csharp]</span><span class="sxs-lookup"><span data-stu-id="f88f4-170">SendGrid C\# library repo: [sendgrid-csharp][sendgrid-csharp]</span></span>
* <span data-ttu-id="f88f4-171">Документация по интерфейсу API SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="f88f4-171">SendGrid API documentation: <https://sendgrid.com/docs></span></span>

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

