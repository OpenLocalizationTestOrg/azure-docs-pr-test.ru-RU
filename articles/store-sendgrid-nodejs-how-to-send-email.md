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
# <a name="how-toosend-email-using-sendgrid-from-nodejs"></a><span data-ttu-id="b0072-104">Как tooSend электронной почты с помощью SendGrid из Node.js</span><span class="sxs-lookup"><span data-stu-id="b0072-104">How tooSend Email Using SendGrid from Node.js</span></span>
<span data-ttu-id="b0072-105">В этом руководстве показано, как tooperform часто встречающиеся задачи программирования с помощью SendGrid электронной почты службы в Azure.</span><span class="sxs-lookup"><span data-stu-id="b0072-105">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="b0072-106">образцы Hello записываются с помощью Node.js API hello.</span><span class="sxs-lookup"><span data-stu-id="b0072-106">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="b0072-107">Hello сценарии включают **построении электронной почты**, **отправке сообщения электронной почты**, **Добавление вложений**, **с помощью фильтров**и **обновление свойств**.</span><span class="sxs-lookup"><span data-stu-id="b0072-107">hello scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="b0072-108">Дополнительные сведения о SendGrid и отправке сообщения электронной почты см. в разделе hello [дальнейшие действия](#next-steps) раздела.</span><span class="sxs-lookup"><span data-stu-id="b0072-108">For more information on SendGrid and sending email, see hello [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="b0072-109">Что такое hello SendGrid службы электронной почты?</span><span class="sxs-lookup"><span data-stu-id="b0072-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="b0072-110">SendGrid — это [облачная служба электронной почты], которая обеспечивает надежную [доставку транзакционных писем], предоставляет возможности масштабирования и аналитики в реальном времени, а также предоставляет гибкие интерфейсы API для пользовательской интеграции.</span><span class="sxs-lookup"><span data-stu-id="b0072-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="b0072-111">Ниже перечислены наиболее распространенные сценарии использования SendGrid.</span><span class="sxs-lookup"><span data-stu-id="b0072-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="b0072-112">Отправлять уведомления toocustomers автоматически</span><span class="sxs-lookup"><span data-stu-id="b0072-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="b0072-113">Администрирование списков рассылки для ежемесячной отправки клиентам электронных листовок и специальных предложений</span><span class="sxs-lookup"><span data-stu-id="b0072-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="b0072-114">Сбор показателей в режиме реального времени по таким параметрам, как заблокированная электронная почта и реагирование клиентов</span><span class="sxs-lookup"><span data-stu-id="b0072-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="b0072-115">Создание отчетов с тенденциями toohelp</span><span class="sxs-lookup"><span data-stu-id="b0072-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="b0072-116">Пересылка запросов клиентов</span><span class="sxs-lookup"><span data-stu-id="b0072-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="b0072-117">Уведомления от приложения по электронной почте</span><span class="sxs-lookup"><span data-stu-id="b0072-117">Email notifications from your application</span></span>

<span data-ttu-id="b0072-118">Дополнительные сведения см. на веб-сайте [https://sendgrid.com](https://sendgrid.com).</span><span class="sxs-lookup"><span data-stu-id="b0072-118">For more information, see [https://sendgrid.com](https://sendgrid.com).</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="b0072-119">Создание учетной записи SendGrid</span><span class="sxs-lookup"><span data-stu-id="b0072-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-nodejs-module"></a><span data-ttu-id="b0072-120">Справочник по hello модуль Node.js SendGrid</span><span class="sxs-lookup"><span data-stu-id="b0072-120">Reference hello SendGrid Node.js Module</span></span>
<span data-ttu-id="b0072-121">модуль SendGrid приветствия для Node.js можно устанавливать с помощью диспетчера пакетов node hello (npm-файл) с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b0072-121">hello SendGrid module for Node.js can be installed through hello node package manager (npm) by using hello following command:</span></span>

    npm install sendgrid

<span data-ttu-id="b0072-122">После установки может потребоваться hello модуля в приложении с помощью hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="b0072-122">After installation, you can require hello module in your application by using hello following code:</span></span>

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

<span data-ttu-id="b0072-123">экспортируемые модулем SendGrid Hello hello **SendGrid** и **электронной почты** функции.</span><span class="sxs-lookup"><span data-stu-id="b0072-123">hello SendGrid module exports hello **SendGrid** and **Email** functions.</span></span>
<span data-ttu-id="b0072-124">**SendGrid** отвечает за отправку почты через SMTP или веб-API, а **Email** инкапсулирует электронное сообщение.</span><span class="sxs-lookup"><span data-stu-id="b0072-124">**SendGrid** is responsible for sending email through Web API, while **Email** encapsulates an email message.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="b0072-125">Практическое руководство. Создание сообщения эл. почты</span><span class="sxs-lookup"><span data-stu-id="b0072-125">How to: Create an Email</span></span>
<span data-ttu-id="b0072-126">Создание сообщения электронной почты, с помощью модуля SendGrid hello включает в себя сначала создается сообщение электронной почты с помощью функции hello электронной почты и последующей отправки с помощью функции hello SendGrid.</span><span class="sxs-lookup"><span data-stu-id="b0072-126">Creating an email message using hello SendGrid module involves first creating an email message using hello Email function, and then sending it using hello SendGrid function.</span></span> <span data-ttu-id="b0072-127">Hello ниже приведен пример создания нового сообщения с помощью функции hello электронной почты:</span><span class="sxs-lookup"><span data-stu-id="b0072-127">hello following is an example of creating a new message using hello Email function:</span></span>

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

<span data-ttu-id="b0072-128">Можно также указать сообщение в формате HTML для клиентов, поддерживающих ее, задав свойству hello html.</span><span class="sxs-lookup"><span data-stu-id="b0072-128">You can also specify an HTML message for clients that support it by setting hello html property.</span></span> <span data-ttu-id="b0072-129">Например:</span><span class="sxs-lookup"><span data-stu-id="b0072-129">For example:</span></span>

    html: This is a sample <b>HTML<b> email message.

<span data-ttu-id="b0072-130">Задание оба свойства text и html hello обеспечивает корректное переход к текстовое содержимое для клиентов, не поддерживающие сообщения в формате HTML.</span><span class="sxs-lookup"><span data-stu-id="b0072-130">Setting both hello text and html properties provides graceful fallback to text content for clients that cannot support HTML messages.</span></span>

<span data-ttu-id="b0072-131">Дополнительные сведения о всех свойствах, поддерживаемых hello функции электронной почты см. в разделе [sendgrid nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="b0072-131">For more information on all properties supported by hello Email function, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="b0072-132">Практическое руководство. Отправка сообщения эл. почты</span><span class="sxs-lookup"><span data-stu-id="b0072-132">How to: Send an Email</span></span>
<span data-ttu-id="b0072-133">После создания сообщения электронной почты через hello функции электронной почты, можно отправить его с помощью веб-API, предоставляемые SendGrid hello.</span><span class="sxs-lookup"><span data-stu-id="b0072-133">After creating an email message using hello Email function, you can send it using hello Web API provided by SendGrid.</span></span> 

### <a name="web-api"></a><span data-ttu-id="b0072-134">Веб-интерфейс API</span><span class="sxs-lookup"><span data-stu-id="b0072-134">Web API</span></span>
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> <span data-ttu-id="b0072-135">А hello выше примерах показывает передачи в объект и обратным вызовом функции электронной почты, можно также непосредственно вызвать функции отправки hello путем указания свойства по электронной почте непосредственно.</span><span class="sxs-lookup"><span data-stu-id="b0072-135">While hello above examples show passing in an email object and callback function, you can also directly invoke hello send function by directly specifying email properties.</span></span> <span data-ttu-id="b0072-136">Например:</span><span class="sxs-lookup"><span data-stu-id="b0072-136">For example:</span></span>  
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

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="b0072-137">Практическое руководство. Добавление вложения</span><span class="sxs-lookup"><span data-stu-id="b0072-137">How to: Add an Attachment</span></span>
<span data-ttu-id="b0072-138">Можно добавлять вложения tooa сообщения, указав hello имена файлов или путь к диску в hello **файлы** свойство.</span><span class="sxs-lookup"><span data-stu-id="b0072-138">Attachments can be added tooa message by specifying hello file name(s) and path(s) in hello **files** property.</span></span> <span data-ttu-id="b0072-139">Привет, следующий пример демонстрирует отправку вложения:</span><span class="sxs-lookup"><span data-stu-id="b0072-139">hello following example demonstrates sending an attachment:</span></span>

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
> <span data-ttu-id="b0072-140">При использовании hello **файлы** свойства hello файл должен быть доступен через [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span><span class="sxs-lookup"><span data-stu-id="b0072-140">When using hello **files** property, hello file must be accessible through [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span></span> <span data-ttu-id="b0072-141">Если hello файла tooattach находится в хранилище Azure, например в контейнер больших двоичных объектов, необходимо сначала скопировать хранения toolocal файлов hello или tooan диск Azure перед отправкой во вложении, с помощью hello **файлы** свойство.</span><span class="sxs-lookup"><span data-stu-id="b0072-141">If hello file you wish tooattach is hosted in Azure Storage, such as in a Blob container, you must first copy hello file toolocal storage or tooan Azure drive before it can be sent as an attachment using hello **files** property.</span></span>
> 
> 

## <a name="how-to-use-filters-tooenable-footers-and-tracking"></a><span data-ttu-id="b0072-142">Как: использовать фильтры tooEnable нижние колонтитулы и отслеживания</span><span class="sxs-lookup"><span data-stu-id="b0072-142">How to: Use Filters tooEnable Footers and Tracking</span></span>
<span data-ttu-id="b0072-143">SendGrid предоставляет функциональные возможности дополнительный адрес электронной почты с использованием hello фильтров.</span><span class="sxs-lookup"><span data-stu-id="b0072-143">SendGrid provides additional email functionality through hello use of filters.</span></span> <span data-ttu-id="b0072-144">Это параметры, которые могут быть добавлены tooan сообщение электронной почты для включения определенных функций, таких как включение отслеживание щелчков, Google analytics, отслеживание, подписки и т. д.</span><span class="sxs-lookup"><span data-stu-id="b0072-144">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="b0072-145">Полный список фильтров см. в разделе [Filter Settings][Filter Settings] (Параметры фильтрации).</span><span class="sxs-lookup"><span data-stu-id="b0072-145">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

<span data-ttu-id="b0072-146">Фильтры могут быть применен tooa сообщения с помощью hello **фильтры** свойство.</span><span class="sxs-lookup"><span data-stu-id="b0072-146">Filters can be applied tooa message by using hello **filters** property.</span></span>
<span data-ttu-id="b0072-147">Каждый фильтр определяется хэшем, содержащим параметры, которые связаны с данным конкретным фильтром.</span><span class="sxs-lookup"><span data-stu-id="b0072-147">Each filter is specified by a hash containing filter-specific settings.</span></span>
<span data-ttu-id="b0072-148">Hello следующие примеры демонстрируют hello нижний колонтитул и выберите отслеживания фильтры:</span><span class="sxs-lookup"><span data-stu-id="b0072-148">hello following examples demonstrate hello footer and click tracking filters:</span></span>

### <a name="footer"></a><span data-ttu-id="b0072-149">Нижний колонтитул</span><span class="sxs-lookup"><span data-stu-id="b0072-149">Footer</span></span>
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

### <a name="click-tracking"></a><span data-ttu-id="b0072-150">Отслеживание щелчков</span><span class="sxs-lookup"><span data-stu-id="b0072-150">Click Tracking</span></span>
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

## <a name="how-to-update-email-properties"></a><span data-ttu-id="b0072-151">Практическое руководство. Обновление свойств электронной почты</span><span class="sxs-lookup"><span data-stu-id="b0072-151">How to: Update Email Properties</span></span>
<span data-ttu-id="b0072-152">Некоторые свойства электронной почты может быть перезаписана с помощью  **задать*свойство*** или добавляться с помощью  **добавить*свойство***.</span><span class="sxs-lookup"><span data-stu-id="b0072-152">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span> <span data-ttu-id="b0072-153">Например, вы можете добавить дополнительных получателей с помощью</span><span class="sxs-lookup"><span data-stu-id="b0072-153">For example, you can add additional recipients by using</span></span>

    email.addTo('jeff@contoso.com');

<span data-ttu-id="b0072-154">или задать фильтр с помощью</span><span class="sxs-lookup"><span data-stu-id="b0072-154">or set a filter by using</span></span>

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

<span data-ttu-id="b0072-155">Дополнительные сведения см. в разделе [sendgrid nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="b0072-155">For more information, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="b0072-156">Практическое руководство. Использование дополнительных служб SendGrid</span><span class="sxs-lookup"><span data-stu-id="b0072-156">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="b0072-157">SendGrid предлагает веб-API можно использовать дополнительные возможности SendGrid tooleverage из приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="b0072-157">SendGrid offers web-based APIs that you can use tooleverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="b0072-158">Дополнительные сведения см. в разделе hello [документации по SendGrid API][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="b0072-158">For full details, see hello [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0072-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b0072-159">Next Steps</span></span>
<span data-ttu-id="b0072-160">Теперь, когда вы узнали основы hello hello служба SendGrid электронной почты, выполните следующие дополнительные toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="b0072-160">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="b0072-161">Репозитории модулей SendGrid Node.js: [sendgrid nodejs][sendgrid-nodejs]</span><span class="sxs-lookup"><span data-stu-id="b0072-161">SendGrid Node.js module repository: [sendgrid-nodejs][sendgrid-nodejs]</span></span>
* <span data-ttu-id="b0072-162">Документация по интерфейсу API SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="b0072-162">SendGrid API documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="b0072-163">Специальное предложение SendGrid для клиентов Azure: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span><span class="sxs-lookup"><span data-stu-id="b0072-163">SendGrid special offer for Azure customers: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span></span>

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[облачная служба электронной почты]: https://sendgrid.com/email-solutions
[доставку транзакционных писем]: https://sendgrid.com/transactional-email
