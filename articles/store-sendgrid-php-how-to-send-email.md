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
# <a name="how-toouse-hello-sendgrid-email-service-from-php"></a>Как tooUse hello службы электронной почты SendGrid из PHP
В этом руководстве показано, как tooperform часто встречающиеся задачи программирования с hello SendGrid электронной почты службы в Azure. Hello примеры на языке PHP.
Hello сценарии включают **построении электронной почты**, **отправке сообщения электронной почты**, и **Добавление вложений**. Дополнительные сведения о SendGrid и отправке сообщения электронной почты см. в разделе hello [дальнейшие действия](#next-steps) раздела.

## <a name="what-is-hello-sendgrid-email-service"></a>Что такое hello SendGrid службы электронной почты?
SendGrid — это [облачная служба электронной почты], которая обеспечивает надежную [доставку транзакционных писем], предоставляет возможности масштабирования и аналитики в реальном времени, а также предоставляет гибкие интерфейсы API для пользовательской интеграции. Ниже перечислены наиболее распространенные сценарии использования SendGrid.

* Отправлять уведомления toocustomers автоматически
* Администрирование списков рассылки для ежемесячной отправки клиентам электронных листовок и специальных предложений
* Сбор показателей в режиме реального времени по таким параметрам, как заблокированная электронная почта и реагирование клиентов
* Создание отчетов с тенденциями toohelp
* Пересылка запросов клиентов
* Уведомления от приложения по электронной почте

Дополнительные сведения см. на веб-сайте [https://sendgrid.com][https://sendgrid.com].

## <a name="create-a-sendgrid-account"></a>Создание учетной записи SendGrid
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="using-sendgrid-from-your-php-application"></a>Использование SendGrid в своем приложении PHP
Использование SendGrid в приложении Azure PHP не требует специальной настройки или кода. Поскольку SendGrid является службой, он может осуществляться в hello точно так же, как из облачного приложения, как его можно из локального приложения.

## <a name="how-to-send-an-email"></a>Практическое руководство. Отправка сообщения эл. почты
Вы можете отправлять электронную почту с помощью SMTP или веб-API, предоставляемые SendGrid hello.

### <a name="smtp-api"></a>Интерфейс SMTP API
toosend электронной почты с помощью hello SMTP SendGrid API, используйте *рассылку Swift*, библиотеку на основе компонентов для отправки сообщений электронной почты из приложений PHP. Вы можете загрузить hello *рассылку Swift* библиотеки из [http://swiftmailer.org/download] [ http://swiftmailer.org/download] v5.3.0 (используйте [Composer] tooinstall SWIFT Mailer). Отправка электронной почты с библиотекой hello включает в себя создание экземпляров <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_рассылку</span>, и <span class="auto-style2">Swift\_сообщения </span> классы задания соответствующих свойств и вызова <span class="auto-style2">Swift\_Mailer::send</span> метод.

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

### <a name="web-api"></a>Веб-интерфейс API
Использование PHP в [curl функция] [ curl function] toosend электронной почте с помощью SendGrid веб-API "hello".

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

SendGrid в веб-API — очень похожа tooa REST API на то, что это не просто RESTful API, поскольку в большинстве вызовов оба GET и POST команды взаимозаменяемы.

## <a name="how-to-add-an-attachment"></a>Практическое руководство. Добавление вложения
### <a name="smtp-api"></a>Интерфейс SMTP API
Отправка вложение с помощью SMTP API hello включает в себя дополнительную строку кода toohello пример скрипта для отправки электронной почты с Swift рассылку.

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

Hello дополнительную строку кода выглядит следующим образом:

     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName('file_name'));

Эта строка кода вызывает hello attach-метод на <span class="auto-style2">Swift\_сообщение</span> объекта и использует статический метод <span class="auto-style2">параметре fromPath</span> на <span class="auto-style2">Swift\_вложения</span>класса tooget и присоедините файл tooa сообщение.

### <a name="web-api"></a>Веб-интерфейс API
Передачу очень похожа toosending находится вложение hello веб-API с помощью электронной почты с помощью hello веб-API. Однако обратите внимание, что в следующем примере hello, массив параметров hello должны содержать этот элемент:

    'files['.$fileName.']' => '@'.$filePath.'/'.$fileName

Пример:

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

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a>Как: использовать фильтры tooEnable нижние колонтитулы, отслеживания и аналитика
SendGrid предоставляет функциональные возможности дополнительный адрес электронной почты с использованием hello «фильтры». Это параметры, которые могут быть добавлены tooan сообщение электронной почты для включения определенных функций, таких как включение отслеживание щелчков, Google analytics, отслеживание, подписки и т. д.

Фильтры могут быть применен tooa сообщения с помощью свойства фильтры hello. Каждый фильтр определяется хэшем, содержащим параметры, которые связаны с данным конкретным фильтром. В следующем примере включает фильтр нижний колонтитул hello и указывает, что текстовое сообщение, которое будет добавлено toohello внизу приветственное сообщение электронной почты.
В этом примере мы будем использовать библиотеку [sendgrid-php library].
Используйте [Composer] tooinstall библиотеки:

    php composer.phar require sendgrid/sendgrid 2.1.1

Пример:    

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

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello hello служба SendGrid электронной почты, выполните следующие дополнительные toolearn ссылки.

* Документация по SendGrid: <https://sendgrid.com/docs>
* Библиотека SendGrid для PHP: <https://github.com/sendgrid/sendgrid-php>
* Специальное предложение SendGrid для клиентов Azure: <https://sendgrid.com/windowsazure.html>

Дополнительные сведения см. также: hello [Центр разработчика PHP](/develop/php/).

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
