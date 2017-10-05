---
title: store-sendgrid-java-how-to-send-email-example
description: "Как отправлять электронную почту с помощью SendGrid из Java в развертывании Azure"
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
ms.openlocfilehash: d80d7d9c54bad12a4d26d8623eeccdf9bc2a743a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-email-using-sendgrid-from-java-in-an-azure-deployment"></a><span data-ttu-id="dafee-103">Как отправлять электронную почту с помощью SendGrid из Java в развертывании Azure</span><span class="sxs-lookup"><span data-stu-id="dafee-103">How to Send Email Using SendGrid from Java in an Azure Deployment</span></span>
<span data-ttu-id="dafee-104">В следующем примере показано, как отправлять сообщения электронной почты с веб-страницы, размещенной в Azure, с помощью SendGrid.</span><span class="sxs-lookup"><span data-stu-id="dafee-104">The following example shows you how you can use SendGrid to send emails from a web page hosted in Azure.</span></span> <span data-ttu-id="dafee-105">В полученном приложении пользователю предлагается ввести данные электронной почты, как показано на следующем снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="dafee-105">The resulting application will prompt the user for email values, as shown in the following screen shot.</span></span>

![Формат адреса электронной почты][emailform]

<span data-ttu-id="dafee-107">Итоговое сообщение электронной почты будет выглядеть примерно так.</span><span class="sxs-lookup"><span data-stu-id="dafee-107">The resulting email will look similar to the following screen shot.</span></span>

![Сообщение электронной почты][emailsent]

<span data-ttu-id="dafee-109">Чтобы использовать код, представленный в этом разделе, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="dafee-109">You'll need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="dafee-110">JAR-файлы javax.mail можно получить, например, по адресу <http://www.oracle.com/technetwork/java/javamail/index.html>.</span><span class="sxs-lookup"><span data-stu-id="dafee-110">Obtain the javax.mail JARs, for example from <http://www.oracle.com/technetwork/java/javamail/index.html>.</span></span>
2. <span data-ttu-id="dafee-111">Добавьте JAR-файлы в путь сборки Java.</span><span class="sxs-lookup"><span data-stu-id="dafee-111">Add the JARs to your Java build path.</span></span>
3. <span data-ttu-id="dafee-112">Если вы используете Eclipse для создания приложения Java, включите библиотеки SendGrid в файл развертывания приложения (WAR-файл) с помощью компонента сборки развертывания Eclipse.</span><span class="sxs-lookup"><span data-stu-id="dafee-112">If you are using Eclipse to create this Java application, you can include the SendGrid libraries in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="dafee-113">Если среда Eclipse не используется, включите эти библиотеки в ту же роль Azure, которой принадлежит ваше Java-приложение, после чего добавьте в приложение путь к классу.</span><span class="sxs-lookup"><span data-stu-id="dafee-113">If you are not using Eclipse to create this Java application, ensure the libraries are included within the same Azure role as your Java application, and added to the class path of your application.</span></span>

<span data-ttu-id="dafee-114">Для отправки электронной почты вам также понадобится собственное имя пользователя и пароль SendGrid.</span><span class="sxs-lookup"><span data-stu-id="dafee-114">You must also have your own SendGrid username and password, to be able to send the email.</span></span> <span data-ttu-id="dafee-115">Чтобы приступить к работе с SendGrid, ознакомьтесь с разделом [Как отправлять электронную почту с помощью SendGrid из Java](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="dafee-115">To get started with SendGrid, see [How to send email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

<span data-ttu-id="dafee-116">Кроме того, если вы не используете среду Eclipse, мы настоятельно рекомендуем вам ознакомиться с разделом [Создание приложения "Hello World" для Azure в Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), а также другими способами размещения Java-приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="dafee-116">Additionally, familiarity with the information at [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-sending-email"></a><span data-ttu-id="dafee-117">Создание веб-формы для отправки электронных сообщений</span><span class="sxs-lookup"><span data-stu-id="dafee-117">Create a web form for sending email</span></span>
<span data-ttu-id="dafee-118">В следующем коде показано, как создать веб-форму, позволяющую извлечь данные пользователя для отправки электронной почты.</span><span class="sxs-lookup"><span data-stu-id="dafee-118">The following code shows how to create a web form to retrieve user data for sending email.</span></span> <span data-ttu-id="dafee-119">В данном контексте этот JSP-файл имеет имя **emailform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="dafee-119">For purposes of this content, the JSP file is named **emailform.jsp**.</span></span>

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

## <a name="create-the-code-to-send-the-email"></a><span data-ttu-id="dafee-120">Создание кода для отправки электронного сообщения</span><span class="sxs-lookup"><span data-stu-id="dafee-120">Create the code to send the email</span></span>
<span data-ttu-id="dafee-121">Следующий код, который вызывается после заполнения формы в emailform.jsp, создает сообщение электронной почты, а затем отправляет его.</span><span class="sxs-lookup"><span data-stu-id="dafee-121">The following code, which is called when you complete the form in emailform.jsp, creates the email message and sends it.</span></span> <span data-ttu-id="dafee-122">В данном контексте этот JSP-файл имеет имя **sendemail.jsp**.</span><span class="sxs-lookup"><span data-stu-id="dafee-122">For purposes of this content, the JSP file is named **sendemail.jsp**.</span></span>

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

         // The SendGrid SMTP server.
         String SMTP_HOST_NAME = "smtp.sendgrid.net";

         Properties properties;

         properties = new Properties();

         // Specify SMTP values.
         properties.put("mail.transport.protocol", "smtp");
         properties.put("mail.smtp.host", SMTP_HOST_NAME);
         properties.put("mail.smtp.port", 587);
         properties.put("mail.smtp.auth", "true");

         // Display the email fields entered by the user. 
         out.println("Value entered for email Subject: " + request.getParameter("emailSubject") + "<br/>");        
         out.println("Value entered for email      To: " + request.getParameter("emailTo") + "<br/>");
         out.println("Value entered for email    From: " + request.getParameter("emailFrom") + "<br/>");
         out.println("Value entered for email    Text: " + "<br/>" + request.getParameter("emailText") + "<br/>");

         // Create the authenticator object.
         Authenticator authenticator = new SMTPAuthenticator();

         // Create the mail session object.
         Session mailSession;
         mailSession = Session.getDefaultInstance(properties, authenticator);

         // Display debug information to stdout, useful when using the
         // compute emulator during development.
         mailSession.setDebug(true);

         // Create the message and message part objects.
         MimeMessage message;
         Multipart multipart;
         MimeBodyPart messagePart; 

         message = new MimeMessage(mailSession);

         multipart = new MimeMultipart("alternative");
         messagePart = new MimeBodyPart();
         messagePart.setContent(request.getParameter("emailText"), "text/html");
         multipart.addBodyPart(messagePart);            

         // Specify the email To, From, Subject and Content. 
         message.setFrom(new InternetAddress(request.getParameter("emailFrom")));
         message.addRecipient(Message.RecipientType.TO, new InternetAddress(request.getParameter("emailTo")));
         message.setSubject(request.getParameter("emailSubject")); 
         message.setContent(multipart);

         // Uncomment the following if you want to add a footer.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"footer\": {\"settings\": {\"enable\":1,\"text/html\": \"<html>This is my <b>email footer</b>.</html>\"}}}}");

         // Uncomment the following if you want to enable click tracking.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"clicktrack\": {\"settings\": {\"enable\":1}}}}");

         Transport transport;
         transport = mailSession.getTransport();
         // Connect the transport object.
         transport.connect();
         // Send the message.
         transport.sendMessage(message,  message.getRecipients(Message.RecipientType.TO));
         // Close the connection.
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

<span data-ttu-id="dafee-123">Кроме отправки электронной почты, emailform.jsp предоставляет результат пользователю. Пример приведен на следующем снимке экрана:</span><span class="sxs-lookup"><span data-stu-id="dafee-123">In addition to sending the email, emailform.jsp provides a result for the user; an example is the following screen shot:</span></span>

![Результат отправки почты][emailresult]

## <a name="next-steps"></a><span data-ttu-id="dafee-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dafee-125">Next steps</span></span>
<span data-ttu-id="dafee-126">Разверните приложение в эмуляторе вычислений, запустите emailform.jsp в браузере, введите значения в форме, нажмите кнопку **Отправить это сообщение электронной почты**, а затем просмотрите результаты в sendemail.jsp.</span><span class="sxs-lookup"><span data-stu-id="dafee-126">Deploy your application to the compute emulator and within a browser run emailform.jsp, enter values in the form, click **Send this email**, and then see results in sendemail.jsp.</span></span>

<span data-ttu-id="dafee-127">Этот код был представлен для того, чтобы показать вам, как использовать SendGrid для языка Java в Azure.</span><span class="sxs-lookup"><span data-stu-id="dafee-127">This code was provided to show you how to use SendGrid in Java on Azure.</span></span> <span data-ttu-id="dafee-128">Возможно, перед развертыванием в рабочей среде Azure потребуется добавить в него дополнительные обработчики ошибок и другие функции.</span><span class="sxs-lookup"><span data-stu-id="dafee-128">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="dafee-129">Например:</span><span class="sxs-lookup"><span data-stu-id="dafee-129">For example:</span></span> 

* <span data-ttu-id="dafee-130">Вместо веб-формы для сохранения адресов и электронных сообщений вы можете использовать хранилище больших двоичных объектов Azure или базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="dafee-130">You could use Azure storage blobs or SQL Database to store email addresses and email messages, instead of using a web form.</span></span> <span data-ttu-id="dafee-131">Дополнительные сведения об использовании больших двоичных объектов службы хранилища Azure в Java см. в разделе [Как использовать службу хранилища BLOB-объектов из Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span><span class="sxs-lookup"><span data-stu-id="dafee-131">For information about using Azure storage blobs in Java, see [How to Use the Blob Storage Service from Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span></span> <span data-ttu-id="dafee-132">Дополнительные сведения об использовании базы данных SQL в Java см. в разделе [Использование базы данных SQL в Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span><span class="sxs-lookup"><span data-stu-id="dafee-132">For information about using SQL Database in Java, see [Using SQL Database in Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span></span>
* <span data-ttu-id="dafee-133">Для получения имени пользователя и пароля SendGrid из параметров конфигурации развертывания вместо веб-формы можно использовать `RoleEnvironment.getConfigurationSettings`.</span><span class="sxs-lookup"><span data-stu-id="dafee-133">You could use `RoleEnvironment.getConfigurationSettings` to retrieve the SendGrid username and password from your deployment's configuration settings, instead of using the web form to retrieve those values.</span></span> <span data-ttu-id="dafee-134">Дополнительную информацию о классе `RoleEnvironment` см. в разделе [Использование библиотеки среды выполнения служб Azure в JSP](http://msdn.microsoft.com/library/windowsazure/hh690948), а также в документации по пакету среды выполнения служб Azure по адресу <http://dl.windowsazure.com/javadoc>.</span><span class="sxs-lookup"><span data-stu-id="dafee-134">For information about the `RoleEnvironment` class, see [Using the Azure Service Runtime Library in JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) and the Azure Service Runtime package documentation at <http://dl.windowsazure.com/javadoc>.</span></span>
* <span data-ttu-id="dafee-135">Дополнительную информацию об использовании SendGrid в Java см. в разделе [Как отправлять электронную почту с помощью SendGrid из Java](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="dafee-135">For more information about using SendGrid in Java, see [How to send email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
