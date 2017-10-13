---
title: "Как использовать службу электронной почты SendGrid (Java) | Документация Майкрософт"
description: "Узнайте, как отправить электронное сообщение с помощью службы электронной почты SendGrid в Azure. Примеры кода написаны на Java."
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: cc75c43e-ede9-492b-98c2-9147fcb92c21
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork
ms.openlocfilehash: 85a0e302626ca14ac039ee6f662f372ddbeb62c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-email-using-sendgrid-from-java"></a>Как отправлять электронную почту с помощью SendGrid из Java
В этом руководстве показано, как выполнять типовые задачи программирования для службы электронной почты SendGrid в Azure. Примеры кода написаны на Java. Описываемые здесь сценарии включают в себя **создание электронного сообщения**, **отправку электронного сообщения**, **добавление вложений**, **использование фильтров** и **обновление свойств**. Дополнительные сведения о SendGrid и отправке электронной почты см. в разделе [Дальнейшие действия](#next-steps).

## <a name="what-is-the-sendgrid-email-service"></a>Что такое служба электронной почты SendGrid?
SendGrid — это [облачная служба электронной почты], которая обеспечивает надежную [доставку электронной почты], предоставляет возможности масштабирования и аналитики в реальном времени, а также предоставляет гибкие интерфейсы API для пользовательской интеграции. Ниже перечислены наиболее распространенные сценарии использования SendGrid.

* Автоматическая отправка уведомлений о получении клиентам
* Администрирование списков рассылки для ежемесячной отправки клиентам электронных листовок и специальных предложений
* Сбор показателей в режиме реального времени по таким параметрам, как заблокированная электронная почта и реагирование клиентов
* Создание отчетов для определения тенденций
* Пересылка запросов клиентов
* Уведомления от приложения по электронной почте

Дополнительные сведения см. на веб-сайте <http://sendgrid.com>.

## <a name="create-a-sendgrid-account"></a>Создание учетной записи SendGrid
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-the-javaxmail-libraries"></a>Практическое руководство. Использование библиотек javax.mail
Получите библиотеки javax.mail, например, по адресу <http://www.oracle.com/technetwork/java/javamai>, и импортируйте их в свой код. В общих чертах отправка сообщений электронной почты с помощью SMTP с использованием библиотеки javax.mail выглядит следующим образом.

1. Укажите значения SMTP, включая SMTP-сервер, для которого SendGrid имеет значение smtp.sendgrid.net.

```
        import java.util.Properties;
        import javax.activation.*;
        import javax.mail.*;
        import javax.mail.internet.*;

        public class MyEmailer {
           private static final String SMTP_HOST_NAME = "smtp.sendgrid.net";
           private static final String SMTP_AUTH_USER = "your_sendgrid_username";
           private static final String SMTP_AUTH_PWD = "your_sendgrid_password";

           public static void main(String[] args) throws Exception{
               new MyEmailer().SendMail();
           }

           public void SendMail() throws Exception
           {
              Properties properties = new Properties();
                 properties.put("mail.transport.protocol", "smtp");
                 properties.put("mail.smtp.host", SMTP_HOST_NAME);
                 properties.put("mail.smtp.port", 587);
                 properties.put("mail.smtp.auth", "true");
                 // …
```

1. Расширьте класс *javax.mail.Authenticator*, а затем в реализации метода *getPasswordAuthentication* возвратите имя пользователя и пароль SendGrid.  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. Создайте сеанс электронной почты, прошедший проверку подлинности, с помощью объекта *javax.mail.Session* .  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. Создайте сообщение и назначьте значения полей **Кому**, **От**, **Тема** и содержимое. Это описано в разделе [Практическое руководство. Создание сообщения электронной почты](#how-to-create-an-email).
4. Отправьте сообщение через объект *javax.mail.Transport*. Это показано в разделе [Практическое руководство. Отправка сообщения электронной почты].

## <a name="how-to-create-an-email"></a>Практическое руководство. Создание сообщения электронной почты
Ниже показано, как задать значения для сообщения электронной почты.

    MimeMessage message = new MimeMessage(mailSession);
    Multipart multipart = new MimeMultipart("alternative");
    BodyPart part1 = new MimeBodyPart();
    part1.setText("Hello, Your Contoso order has shipped. Thank you, John");
    BodyPart part2 = new MimeBodyPart();
    part2.setContent(
        "<p>Hello,</p>
        <p>Your Contoso order has <b>shipped</b>.</p>
        <p>Thank you,<br>John</br></p>",
        "text/html");
    multipart.addBodyPart(part1);
    multipart.addBodyPart(part2);
    message.setFrom(new InternetAddress("john@contoso.com"));
    message.addRecipient(Message.RecipientType.TO,
       new InternetAddress("someone@example.com"));
    message.setSubject("Your recent order");
    message.setContent(multipart);

## <a name="how-to-send-an-email"></a>Практическое руководство. Отправка сообщения эл. почты
Ниже показано, как отправить сообщение электронной почты.

    Transport transport = mailSession.getTransport();
    // Connect the transport object.
    transport.connect();
    // Send the message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close the connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a>Практическое руководство. Добавление вложения
В следующем коде показано, как добавить вложение.

    // Local file name and path.
    String attachmentName = "myfile.zip";
    String attachmentPath = "c:\\myfiles\\";
    MimeBodyPart attachmentPart = new MimeBodyPart();
    // Specify the local file to attach.
    DataSource source = new FileDataSource(attachmentPath + attachmentName);
    attachmentPart.setDataHandler(new DataHandler(source));
    // This example uses the local file name as the attachment name.
    // They could be different if you prefer.
    attachmentPart.setFileName(attachmentName);
    multipart.addBodyPart(attachmentPart);

## <a name="how-to-use-filters-to-enable-footers-tracking-and-analytics"></a>Практическое руководство. Использование фильтров для включения нижних колонтитулов, отслеживания и аналитики
SendGrid поддерживает дополнительные функциональные возможности электронной почты благодаря использованию *фильтров*. Это параметры, которые могут быть добавлены в сообщение электронной почты для включения определенных функций, например включения отслеживания щелчков, аналитики Google, отслеживания подписок и т. д. Полный список фильтров см. в разделе [Filter Settings][Filter Settings] (Параметры фильтрации).

* Ниже показано, как вставить фильтр нижнего колонтитула, который выводит HTML-текст, отображаемый в нижней части отправляемого сообщения электронной почты.

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* Еще одним примером фильтра является отслеживание щелчков. Предположим, что текст вашего сообщения электронной почты содержит гиперссылку, похожую на приведенную ниже, и вы хотите отследить частоту переходов по ней.

      messagePart.setContent(
          "Hello,
          <p>This is the body of the message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* Чтобы включить отслеживание щелчков, используйте следующий код:

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a>Практическое руководство. Обновление свойств электронной почты
Некоторые свойства электронной почты может быть перезаписана с помощью  **задать*свойство*** или добавляться с помощью  **добавить*свойство***.

Например, для указания адреса **ReplyTo** используйте следующий код:

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

Чтобы добавить получателя **СК** , используйте следующий код:

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a>Практическое руководство. Использование дополнительных служб SendGrid
SendGrid поддерживает различные веб-интерфейсы API, с помощью которых вы можете использовать дополнительные функции SendGrid, доступные в приложении Azure. Дополнительные сведения см. в [документации по интерфейсу API SendGrid][SendGrid API documentation].

## <a name="next-steps"></a>Дальнейшие действия
Вы получили основные сведения о службе доставки электронной почты SendGrid. Дополнительные сведения можно получить по следующим ссылкам.

* Пример, демонстрирующий использование SendGrid в развертывании Azure: [Практическое руководство. Отправка сообщения электронной почты из Java с помощью SendGrid в развертывании Azure](store-sendgrid-java-how-to-send-email-example.md)
* Пакет SDK SendGrid для Java: <https://sendgrid.com/docs/Code_Examples/java.html>
* Документация по API SendGrid: <https://sendgrid.com/docs/API_Reference/index.html>
* Специальное предложение SendGrid для клиентов Azure: <https://sendgrid.com/windowsazure.html>

[http://sendgrid.com]: https://sendgrid.com
[http://sendgrid.com/pricing.html]: http://sendgrid.com/pricing.html
[http://www.sendgrid.com/azure.html]: https://www.sendgrid.com/windowsazure.html
[http://sendgrid.com/features]: https://sendgrid.com/features
[http://www.oracle.com/technetwork/java/javamail]: http://www.oracle.com/technetwork/java/javamail/index.html
[Filter Settings]: https://sendgrid.com/docs/API_Reference/Web_API/filter_settings.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/index.html
[http://sendgrid.com/azure.html]: https://sendgrid.com/windowsazure.html
[облачная служба электронной почты]: https://sendgrid.com/email-solutions
[доставку электронной почты]: https://sendgrid.com/transactional-email
