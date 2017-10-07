---
title: aaastore-sendgrid-Java-How-to-send-email-example
description: "Как toosend электронной почты с помощью SendGrid из Java в среде Azure"
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: af096a73-6985-4350-92e4-ce1722c8d72f
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: vibhork;dominic.may@sendgrid.com;elmer.thomas@sendgrid.com
ms.openlocfilehash: 51fde1fc71467f8252532b30d2f87856ec25067b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java-in-an-azure-deployment"></a>Как tooSend электронной почты с помощью SendGrid из Java в среде Azure
Hello пример при использовании сообщения электронной почты toosend SendGrid с веб-страницы, размещенной в Azure. полученное приложение Hello пользователю будет предложено hello ввести значения электронной почты, как показано на следующий снимок экрана приветствия.

![Формат адреса электронной почты][emailform]

Привет, полученный по электронной почте будет выглядеть аналогично toohello следующий снимок экрана.

![Сообщение электронной почты][emailsent]

Вам потребуется следующее hello toodo toouse hello кода в этом разделе:

1. Получить hello javax.mail JAR-файлов, например из <http://www.oracle.com/technetwork/java/javamail/index.html>.
2. Добавьте tooyour hello JAR-файлов, путь построения Java.
3. При использовании Eclipse toocreate этого приложения Java, hello SendGrid библиотеки можно включить в файл развертывания приложения (WAR) с помощью функции сборки развертывания Eclipse. Если вы не используете Eclipse toocreate этого приложения Java, обеспечить hello библиотеки включены в hello же роли Azure как путь приложения и добавлены toohello класс Java приложения.

Также необходимо иметь собственные SendGrid имя пользователя и пароль, может toosend toobe hello-электронной почты. tooget к работе с SendGrid, в разделе [как toosend электронной почты с помощью SendGrid из Java](store-sendgrid-java-how-to-send-email.md).

Кроме того, вы знакомы с hello данных во время [Создание приложения Hello World для Azure в Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), или с помощью других методов для размещения приложений Java в Azure, если вы не используете Eclipse, настоятельно рекомендуется.

## <a name="create-a-web-form-for-sending-email"></a>Создание веб-формы для отправки электронных сообщений
Hello, следующий код показывает, как данные пользователя tooretrieve для отправки электронной почты формы toocreate веб-узла. Для целей этого содержимого hello JSP-файл с именем **emailform.jsp**.

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Send this email</b>.</p>
     <br/>
      <form action="sendemail.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="emailTo">
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="emailFrom">
           </td>
         </tr>
         <tr>
           <td>Subject:</td>
           <td><input type="text" size=100 name="emailSubject" value="My email subject">
           </td>
         </tr>
         <tr>
           <td>Text:</td>
           <td><input type="text" size=400 name="emailText" value="Hello,<p>This is my message.</p>Thank you." />
           </td>
         </tr>
         <tr>
           <td>SendGrid user name:</td>
           <td><input type="text" name="sendGridUser">
           </td>
         </tr>
         <tr>
           <td>SendGrid password:</td>
           <td><input type="password" name="sendGridPassword">
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Send this email">
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toosend-hello-email"></a>Создание электронной почты для hello toosend кода hello
Hello следующий код, который вызывается при заполнении формы hello в emailform.jsp, создает приветственное сообщение электронной почты и отправляет его. Для целей этого содержимого hello JSP-файл с именем **sendemail.jsp**.

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" import="javax.activation.*, javax.mail.*, javax.mail.internet.*, java.util.Date, java.util.Properties" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email processing happens here</title>
    </head>
    <body>
        <b>This is my send mail page.</b><p/>
     <%

     final String sendGridUser = request.getParameter("sendGridUser");
     final String sendGridPassword = request.getParameter("sendGridPassword");

     class SMTPAuthenticator extends Authenticator
     {
       public PasswordAuthentication getPasswordAuthentication()
       {
            String username = sendGridUser;
            String password = sendGridPassword;

            return new PasswordAuthentication(username, password);   
       }
     }
     try
     {

         // hello SendGrid SMTP server.
         String SMTP_HOST_NAME = "smtp.sendgrid.net";

         Properties properties;

         properties = new Properties();

         // Specify SMTP values.
         properties.put("mail.transport.protocol", "smtp");
         properties.put("mail.smtp.host", SMTP_HOST_NAME);
         properties.put("mail.smtp.port", 587);
         properties.put("mail.smtp.auth", "true");

         // Display hello email fields entered by hello user. 
         out.println("Value entered for email Subject: " + request.getParameter("emailSubject") + "<br/>");        
         out.println("Value entered for email      To: " + request.getParameter("emailTo") + "<br/>");
         out.println("Value entered for email    From: " + request.getParameter("emailFrom") + "<br/>");
         out.println("Value entered for email    Text: " + "<br/>" + request.getParameter("emailText") + "<br/>");

         // Create hello authenticator object.
         Authenticator authenticator = new SMTPAuthenticator();

         // Create hello mail session object.
         Session mailSession;
         mailSession = Session.getDefaultInstance(properties, authenticator);

         // Display debug information toostdout, useful when using the
         // compute emulator during development.
         mailSession.setDebug(true);

         // Create hello message and message part objects.
         MimeMessage message;
         Multipart multipart;
         MimeBodyPart messagePart; 

         message = new MimeMessage(mailSession);

         multipart = new MimeMultipart("alternative");
         messagePart = new MimeBodyPart();
         messagePart.setContent(request.getParameter("emailText"), "text/html");
         multipart.addBodyPart(messagePart);            

         // Specify hello email To, From, Subject and Content. 
         message.setFrom(new InternetAddress(request.getParameter("emailFrom")));
         message.addRecipient(Message.RecipientType.TO, new InternetAddress(request.getParameter("emailTo")));
         message.setSubject(request.getParameter("emailSubject")); 
         message.setContent(multipart);

         // Uncomment hello following if you want tooadd a footer.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"footer\": {\"settings\": {\"enable\":1,\"text/html\": \"<html>This is my <b>email footer</b>.</html>\"}}}}");

         // Uncomment hello following if you want tooenable click tracking.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"clicktrack\": {\"settings\": {\"enable\":1}}}}");

         Transport transport;
         transport = mailSession.getTransport();
         // Connect hello transport object.
         transport.connect();
         // Send hello message.
         transport.sendMessage(message,  message.getRecipients(Message.RecipientType.TO));
         // Close hello connection.
         transport.close();

        out.println("<p>Email processing completed.</p>");

     }
     catch (Exception e)
     {
         out.println("<p>Exception encountered: " + 
                            e.getMessage()     +
                            "</p>");   
     }
    %>

    </body>
    </html>

В дополнение к этому по электронной почте hello toosending emailform.jsp предоставляет результат для пользователя hello. Примером является следующий снимок экрана приветствия:

![Результат отправки почты][emailresult]

## <a name="next-steps"></a>Дальнейшие действия
Развертывание эмулятор вычислений toohello вашего приложения и в браузере запустите emailform.jsp, введите значения в форме hello, нажмите кнопку **отправить это сообщение электронной почты**, а затем просмотреть результаты в sendemail.jsp.

Этот код был предоставлен tooshow вы как toouse SendGrid в Java в Azure. Перед развертыванием tooAzure в рабочей среде, вы можете tooadd дополнительные обработки ошибок или других компонентов. Например: 

* Большие двоичные объекты хранилища Azure или адреса электронной почты toostore базы данных SQL и сообщений электронной почты, можно использовать вместо использования веб-формы. Сведения об использовании больших двоичных объектов хранилища Azure в Java см. в разделе [как tooUse hello службы хранилища больших двоичных объектов из Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/). Дополнительные сведения об использовании базы данных SQL в Java см. в разделе [Использование базы данных SQL в Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).
* Можно использовать `RoleEnvironment.getConfigurationSettings` tooretrieve hello SendGrid, имя пользователя и пароль от параметров конфигурации развертывания, а не с помощью hello tooretrieve форма web эти значения. Сведения о hello `RoleEnvironment` см. в описании [hello использование библиотеки среды выполнения службы Azure в JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) и hello документации пакета среды выполнения служб Azure в <http://dl.windowsazure.com/javadoc>.
* Дополнительные сведения об использовании SendGrid в Java см. в разделе [как toosend электронной почты с помощью SendGrid из Java](store-sendgrid-java-how-to-send-email.md).

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
