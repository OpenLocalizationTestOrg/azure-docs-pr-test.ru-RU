---
title: "hello toouse aaaHow SendGrid службы электронной почты (PHP) | Документы Microsoft"
description: "Узнайте, как отправлять сообщения электронной почты с hello SendGrid службы электронной почты в Azure. Примеры кода написаны на PHP."
documentationcenter: php
services: 
manager: sendgrid
editor: mollybos
author: thinkingserious
ms.assetid: 51a9928a-4c9e-4b0a-aca8-9a408aeb6f47
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork; matt.bernier@sendgrid.com
ms.openlocfilehash: 0076e56dc185cb8f52e629395e7d2c143cb5cfa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-sendgrid-email-service-from-php"></a><span data-ttu-id="9f5c9-104">Как tooUse hello службы электронной почты SendGrid из PHP</span><span class="sxs-lookup"><span data-stu-id="9f5c9-104">How tooUse hello SendGrid Email Service from PHP</span></span>
<span data-ttu-id="9f5c9-105">В этом руководстве показано, как tooperform часто встречающиеся задачи программирования с hello SendGrid электронной почты службы в Azure.</span><span class="sxs-lookup"><span data-stu-id="9f5c9-105">This guide demonstrates how tooperform common programming tasks with hello SendGrid email service on Azure.</span></span> <span data-ttu-id="9f5c9-106">Hello примеры на языке PHP.</span><span class="sxs-lookup"><span data-stu-id="9f5c9-106">hello samples are written in PHP.</span></span>
<span data-ttu-id="9f5c9-107">Hello сценарии включают **построении электронной почты**, **отправке сообщения электронной почты**, и **Добавление вложений**.</span><span class="sxs-lookup"><span data-stu-id="9f5c9-107">hello scenarios covered include **constructing email**, **sending email**, and **adding attachments**.</span></span> <span data-ttu-id="9f5c9-108">Дополнительные сведения о SendGrid и отправке сообщения электронной почты см. в разделе hello [дальнейшие действия](#next-steps) раздела.</span><span class="sxs-lookup"><span data-stu-id="9f5c9-108">For more information on SendGrid and sending email, see hello [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="9f5c9-109">Что такое hello SendGrid службы электронной почты?</span><span class="sxs-lookup"><span data-stu-id="9f5c9-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="9f5c9-110">SendGrid — это [облачная служба электронной почты], которая обеспечивает надежную [доставку транзакционных писем], предоставляет возможности масштабирования и аналитики в реальном времени, а также предоставляет гибкие интерфейсы API для пользовательской интеграции.</span><span class="sxs-lookup"><span data-stu-id="9f5c9-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="9f5c9-111">Ниже перечислены наиболее распространенные сценарии использования SendGrid.</span><span class="sxs-lookup"><span data-stu-id="9f5c9-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="9f5c9-112">Отправлять уведомления toocustomers автоматически</span><span class="sxs-lookup"><span data-stu-id="9f5c9-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="9f5c9-113">Администрирование списков рассылки для ежемесячной отправки клиентам электронных листовок и специальных предложений</span><span class="sxs-lookup"><span data-stu-id="9f5c9-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="9f5c9-114">Сбор показателей в режиме реального времени по таким параметрам, как заблокированная электронная почта и реагирование клиентов</span><span class="sxs-lookup"><span data-stu-id="9f5c9-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="9f5c9-115">Создание отчетов с тенденциями toohelp</span><span class="sxs-lookup"><span data-stu-id="9f5c9-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="9f5c9-116">Пересылка запросов клиентов</span><span class="sxs-lookup"><span data-stu-id="9f5c9-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="9f5c9-117">Уведомления от приложения по электронной почте</span><span class="sxs-lookup"><span data-stu-id="9f5c9-117">Email notifications from your application</span></span>

<span data-ttu-id="9f5c9-118">Дополнительные сведения см. на веб-сайте [https://sendgrid.com][https://sendgrid.com].</span><span class="sxs-lookup"><span data-stu-id="9f5c9-118">For more information, see [https://sendgrid.com][https://sendgrid.com].</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="9f5c9-119">Создание учетной записи SendGrid</span><span class="sxs-lookup"><span data-stu-id="9f5c9-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="using-sendgrid-from-your-php-application"></a><span data-ttu-id="9f5c9-120">Использование SendGrid в своем приложении PHP</span><span class="sxs-lookup"><span data-stu-id="9f5c9-120">Using SendGrid from your PHP Application</span></span>
<span data-ttu-id="9f5c9-121">Использование SendGrid в приложении Azure PHP не требует специальной настройки или кода.</span><span class="sxs-lookup"><span data-stu-id="9f5c9-121">Using SendGrid in an Azure PHP application requires no special configuration or coding.</span></span> <span data-ttu-id="9f5c9-122">Поскольку SendGrid является службой, он может осуществляться в hello точно так же, как из облачного приложения, как его можно из локального приложения.</span><span class="sxs-lookup"><span data-stu-id="9f5c9-122">Because SendGrid is a service, it can be accessed in exactly hello same way from a cloud application as it can from an on-premises application.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="9f5c9-123">Практическое руководство. Отправка сообщения эл. почты</span><span class="sxs-lookup"><span data-stu-id="9f5c9-123">How to: Send an Email</span></span>
<span data-ttu-id="9f5c9-124">Вы можете отправлять электронную почту с помощью SMTP или веб-API, предоставляемые SendGrid hello.</span><span class="sxs-lookup"><span data-stu-id="9f5c9-124">You can send email using either SMTP or hello Web API provided by SendGrid.</span></span>

### <a name="smtp-api"></a><span data-ttu-id="9f5c9-125">Интерфейс SMTP API</span><span class="sxs-lookup"><span data-stu-id="9f5c9-125">SMTP API</span></span>
<span data-ttu-id="9f5c9-126">toosend электронной почты с помощью hello SMTP SendGrid API, используйте *рассылку Swift*, библиотеку на основе компонентов для отправки сообщений электронной почты из приложений PHP.</span><span class="sxs-lookup"><span data-stu-id="9f5c9-126">toosend email using hello SendGrid SMTP API, use *Swift Mailer*, a component-based library for sending emails from PHP applications.</span></span> <span data-ttu-id="9f5c9-127">Вы можете загрузить hello *рассылку Swift* библиотеки из [http://swiftmailer.org/download] [ http://swiftmailer.org/download] v5.3.0 (используйте [Composer] tooinstall SWIFT Mailer).</span><span class="sxs-lookup"><span data-stu-id="9f5c9-127">You can download hello *Swift Mailer* library from [http://swiftmailer.org/download][http://swiftmailer.org/download] v5.3.0 (use [Composer] tooinstall Swift Mailer).</span></span> <span data-ttu-id="9f5c9-128">Отправка электронной почты с библиотекой hello включает в себя создание экземпляров <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_рассылку</span>, и <span class="auto-style2">Swift\_сообщения </span> классы задания соответствующих свойств и вызова <span class="auto-style2">Swift\_Mailer::send</span> метод.</span><span class="sxs-lookup"><span data-stu-id="9f5c9-128">Sending email with hello library involves creating instances of the <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span>, and <span class="auto-style2">Swift\_Message</span> classes, setting the appropriate properties, and calling the <span class="auto-style2">Swift\_Mailer::send</span> method.</span></span>

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello receiver is able tooview html emails then only hello html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
     $html = "<html>
           <head></head>
           <body>
               <p>Hi!<br>
                   How are you?<br>
               </p>
           </body>
           </html>";
     // This is your From email address
     $from = array('someone@example.com' => 'Name tooAppear');
     // Email recipients
     $too= array(
           'john@contoso.com'=>'Destination 1 Name',
           'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
         // This will let us know how many users received this message
         echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
         echo "Something went wrong - ";
         print_r($failures);
     }

### <a name="web-api"></a><span data-ttu-id="9f5c9-129">Веб-интерфейс API</span><span class="sxs-lookup"><span data-stu-id="9f5c9-129">Web API</span></span>
<span data-ttu-id="9f5c9-130">Использование PHP в [curl функция] [ curl function] toosend электронной почте с помощью SendGrid веб-API "hello".</span><span class="sxs-lookup"><span data-stu-id="9f5c9-130">Use PHP's [curl function][curl function] toosend email using hello SendGrid Web API.</span></span>

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $params = array(
          'api_user' => $user,
          'api_key' => $pass,
          'to' => 'john@contoso.com',
          'subject' => 'testing from curl',
          'html' => 'testing body',
          'text' => 'testing body',
          'from' => 'anna@contoso.com',
       );

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

<span data-ttu-id="9f5c9-131">SendGrid в веб-API — очень похожа tooa REST API на то, что это не просто RESTful API, поскольку в большинстве вызовов оба GET и POST команды взаимозаменяемы.</span><span class="sxs-lookup"><span data-stu-id="9f5c9-131">SendGrid's Web API is very similar tooa REST API, though it is not truly a RESTful API since, in most calls, both GET and POST verbs can be used interchangeably.</span></span>

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="9f5c9-132">Практическое руководство. Добавление вложения</span><span class="sxs-lookup"><span data-stu-id="9f5c9-132">How to: Add an Attachment</span></span>
### <a name="smtp-api"></a><span data-ttu-id="9f5c9-133">Интерфейс SMTP API</span><span class="sxs-lookup"><span data-stu-id="9f5c9-133">SMTP API</span></span>
<span data-ttu-id="9f5c9-134">Отправка вложение с помощью SMTP API hello включает в себя дополнительную строку кода toohello пример скрипта для отправки электронной почты с Swift рассылку.</span><span class="sxs-lookup"><span data-stu-id="9f5c9-134">Sending an attachment using hello SMTP API involves one additional line of code toohello example script for sending an email with Swift Mailer.</span></span>

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello reciever is able tooview html emails then only hello html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
      $html = "<html>
          <head></head>
          <body>
             <p>Hi!<br>
                How are you?<br>
             </p>
          </body>
          </html>";

     // This is your From email address
     $from = array('someone@example.com' => 'Name tooAppear');

     // Email recipients
     $too= array(
          'john@contoso.com'=>'Destination 1 Name',
          'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');
     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName("file_name"));

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
          // This will let us know how many users received this message
          echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
          echo "Something went wrong - ";
          print_r($failures);
     }

<span data-ttu-id="9f5c9-135">Hello дополнительную строку кода выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9f5c9-135">hello additional line of code is as follows:</span></span>

     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName('file_name'));

<span data-ttu-id="9f5c9-136">Эта строка кода вызывает hello attach-метод на <span class="auto-style2">Swift\_сообщение</span> объекта и использует статический метод <span class="auto-style2">параметре fromPath</span> на <span class="auto-style2">Swift\_вложения</span>класса tooget и присоедините файл tooa сообщение.</span><span class="sxs-lookup"><span data-stu-id="9f5c9-136">This line of code calls hello attach method on the <span class="auto-style2">Swift\_Message</span> object and uses static method <span class="auto-style2">fromPath</span> on the <span class="auto-style2">Swift\_Attachment</span> class tooget and attach a file tooa message.</span></span>

### <a name="web-api"></a><span data-ttu-id="9f5c9-137">Веб-интерфейс API</span><span class="sxs-lookup"><span data-stu-id="9f5c9-137">Web API</span></span>
<span data-ttu-id="9f5c9-138">Передачу очень похожа toosending находится вложение hello веб-API с помощью электронной почты с помощью hello веб-API.</span><span class="sxs-lookup"><span data-stu-id="9f5c9-138">Sending an attachment using hello Web API is very similar toosending an email using hello Web API.</span></span> <span data-ttu-id="9f5c9-139">Однако обратите внимание, что в следующем примере hello, массив параметров hello должны содержать этот элемент:</span><span class="sxs-lookup"><span data-stu-id="9f5c9-139">However, note that in hello example that follows, hello parameter array must contain this element:</span></span>

    'files['.$fileName.']' => '@'.$filePath.'/'.$fileName

<span data-ttu-id="9f5c9-140">Пример:</span><span class="sxs-lookup"><span data-stu-id="9f5c9-140">Example:</span></span>

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $fileName = 'myfile';
     $filePath = dirname(__FILE__);

     $params = array(
         'api_user' => $user,
         'api_key' => $pass,
         'to' =>'john@contoso.com',
         'subject' => 'test of file sends',
         'html' => '<p> hello HTML </p>',
         'text' => 'hello plain text',
         'from' => 'anna@contoso.com',
         'files['.$fileName.']' => '@'.$filePath.'/'.$fileName
     );

     print_r($params);

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="9f5c9-141">Как: использовать фильтры tooEnable нижние колонтитулы, отслеживания и аналитика</span><span class="sxs-lookup"><span data-stu-id="9f5c9-141">How to: Use Filters tooEnable Footers, Tracking, and Analytics</span></span>
<span data-ttu-id="9f5c9-142">SendGrid предоставляет функциональные возможности дополнительный адрес электронной почты с использованием hello «фильтры».</span><span class="sxs-lookup"><span data-stu-id="9f5c9-142">SendGrid provides additional email functionality through hello use of 'filters'.</span></span> <span data-ttu-id="9f5c9-143">Это параметры, которые могут быть добавлены tooan сообщение электронной почты для включения определенных функций, таких как включение отслеживание щелчков, Google analytics, отслеживание, подписки и т. д.</span><span class="sxs-lookup"><span data-stu-id="9f5c9-143">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span>

<span data-ttu-id="9f5c9-144">Фильтры могут быть применен tooa сообщения с помощью свойства фильтры hello.</span><span class="sxs-lookup"><span data-stu-id="9f5c9-144">Filters can be applied tooa message by using hello filters property.</span></span> <span data-ttu-id="9f5c9-145">Каждый фильтр определяется хэшем, содержащим параметры, которые связаны с данным конкретным фильтром.</span><span class="sxs-lookup"><span data-stu-id="9f5c9-145">Each filter is specified by a hash containing filter-specific settings.</span></span> <span data-ttu-id="9f5c9-146">В следующем примере включает фильтр нижний колонтитул hello и указывает, что текстовое сообщение, которое будет добавлено toohello внизу приветственное сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="9f5c9-146">The following example enables hello footer filter and specifies a text message that will be appended toohello bottom of hello email message.</span></span>
<span data-ttu-id="9f5c9-147">В этом примере мы будем использовать библиотеку [sendgrid-php library].</span><span class="sxs-lookup"><span data-stu-id="9f5c9-147">For this example we will use [sendgrid-php library].</span></span>
<span data-ttu-id="9f5c9-148">Используйте [Composer] tooinstall библиотеки:</span><span class="sxs-lookup"><span data-stu-id="9f5c9-148">Use [Composer] tooinstall library:</span></span>

    php composer.phar require sendgrid/sendgrid 2.1.1

<span data-ttu-id="9f5c9-149">Пример:</span><span class="sxs-lookup"><span data-stu-id="9f5c9-149">Example:</span></span>    

    <?php
     /*
      * This example is used for sendgrid-php V2.1.1 (https://github.com/sendgrid/sendgrid-php/tree/v2.1.1)
      */
     include "vendor/autoload.php";

     $email = new SendGrid\Email();
     // hello list of addresses this message will be sent to
     // [This list is used for sending multiple emails using just ONE request tooSendGrid]
     $toList = array('john@contoso.com', 'anna@contoso.com');

     // Specify hello names of hello recipients
     $nameList = array('Name 1', 'Name 2');

     // Used as an example of variable substitution
     $timeList = array('4 PM', '5 PM');

     // Set all of hello above variables
     $email->setTos($toList);
     $email->addSubstitution('-name-', $nameList);
     $email->addSubstitution('-time-', $timeList);

     // Specify that this is an initial contact message
     $email->addCategory("initial");

     // You can optionally setup individual filters here, in this example, we have
     // enabled hello footer filter
     $email->addFilter('footer', 'enable', 1);
     $email->addFilter('footer', "text/plain", "Thank you for your business");
     $email->addFilter('footer', "text/html", "Thank you for your business");

     // hello subject of your email
     $subject = 'Example SendGrid Email';

     // Where is this message coming from. For example, this message can be from
     // support@yourcompany.com, info@yourcompany.com
     $from = 'someone@example.com';

     // If you do not specify a sender list above, you can specifiy hello user here. If
     // a sender list IS specified above, this email address becomes irrelevant.
     $too= 'john@contoso.com';

     # Create hello body of hello message (a plain-text and an HTML version).
     # text is your plain-text email
     # html is your html version of hello email
     # if hello receiver is able tooview html emails then only hello html
     # email will be displayed

     /*
      * Note hello variable substitution here =)
      */
     $text = "
     Hello -name-,
     Thank you for your interest in our products. We have set up an appointment toocall you at -time- EST toodiscuss your needs in more detail.
     Regards,
     Fred";

     $html = "
     <html>
     <head></head>
     <body>
     <p>Hello -name-,<br>
     Thank you for your interest in our products. We have set up an appointment
     toocall you at -time- EST toodiscuss your needs in more detail.

     Regards,

     Fred<br>
     </p>
     </body>
     </html>";

     // set subject
     $email->setSubject($subject);

     // attach hello body of hello email
     $email->setFrom($from);
     $email->setHtml($html);
     $email->addTo($to);
     $email->setText($text);

     // Your SendGrid account credentials
     $username = 'sendgridusername@yourdomain.com';
     $password = 'example';

     // Create SendGrid object
     $sendgrid = new SendGrid($username, $password);

     // send message
     $response = $sendgrid->send($email);

     print_r($response);

## <a name="next-steps"></a><span data-ttu-id="9f5c9-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9f5c9-150">Next Steps</span></span>
<span data-ttu-id="9f5c9-151">Теперь, когда вы узнали основы hello hello служба SendGrid электронной почты, выполните следующие дополнительные toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="9f5c9-151">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="9f5c9-152">Документация по SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="9f5c9-152">SendGrid documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="9f5c9-153">Библиотека SendGrid для PHP: <https://github.com/sendgrid/sendgrid-php></span><span class="sxs-lookup"><span data-stu-id="9f5c9-153">SendGrid PHP library: <https://github.com/sendgrid/sendgrid-php></span></span>
* <span data-ttu-id="9f5c9-154">Специальное предложение SendGrid для клиентов Azure: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="9f5c9-154">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

<span data-ttu-id="9f5c9-155">Дополнительные сведения см. также: hello [Центр разработчика PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="9f5c9-155">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[https://sendgrid.com]: https://sendgrid.com
[https://sendgrid.com/transactional-email/pricing]: https://sendgrid.com/transactional-email/pricing
[special offer]: https://www.sendgrid.com/windowsazure.html
[Packaging and Deploying PHP Applications for Azure]: http://msdn.microsoft.com/library/windowsazure/hh674499(v=VS.103).aspx
[http://swiftmailer.org/download]: http://swiftmailer.org/download
[curl function]: http://php.net/curl
[облачная служба электронной почты]: https://sendgrid.com/email-solutions
[доставку транзакционных писем]: https://sendgrid.com/transactional-email
[sendgrid-php library]: https://github.com/sendgrid/sendgrid-php/tree/v2.1.1
[Composer]: https://getcomposer.org/download/
