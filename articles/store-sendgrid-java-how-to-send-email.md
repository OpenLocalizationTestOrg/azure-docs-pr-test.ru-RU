---
title: "hello toouse aaaHow SendGrid службы электронной почты (Java) | Документы Microsoft"
description: "Узнайте, как отправлять сообщения электронной почты с hello SendGrid службы электронной почты в Azure. Примеры кода написаны на Java."
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
ms.openlocfilehash: 542ce0003e94fc8f5551487d5a3cd6f75d27e8cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java"></a>Как tooSend электронной почты с помощью SendGrid из Java
В этом руководстве показано, как tooperform часто встречающиеся задачи программирования с помощью SendGrid электронной почты службы в Azure. Hello примеры написаны на Java. Hello сценарии включают **построении электронной почты**, **отправке сообщения электронной почты**, **Добавление вложений**, **с помощью фильтров**и **обновление свойств**. Дополнительные сведения о SendGrid и отправке сообщения электронной почты см. в разделе hello [дальнейшие действия](#next-steps) раздела.

## <a name="what-is-hello-sendgrid-email-service"></a>Что такое hello SendGrid службы электронной почты?
SendGrid — это [облачная служба электронной почты], которая обеспечивает надежную [доставку транзакционных писем], предоставляет возможности масштабирования и аналитики в реальном времени, а также предоставляет гибкие интерфейсы API для пользовательской интеграции. Ниже перечислены наиболее распространенные сценарии использования SendGrid.

* Отправлять уведомления toocustomers автоматически
* Администрирование списков рассылки для ежемесячной отправки клиентам электронных листовок и специальных предложений
* Сбор показателей в режиме реального времени по таким параметрам, как заблокированная электронная почта и реагирование клиентов
* Создание отчетов с тенденциями toohelp
* Пересылка запросов клиентов
* Уведомления от приложения по электронной почте

Дополнительные сведения см. на веб-сайте <http://sendgrid.com>.

## <a name="create-a-sendgrid-account"></a>Создание учетной записи SendGrid
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a>Как: использование библиотек javax.mail hello
Получить hello javax.mail библиотеки, например <http://www.oracle.com/technetwork/java/javamail> и импортировать их в коде. На высоком уровне hello hello javax.mail библиотеки toosend по электронной почте с помощью SMTP с помощью выполняется toodo hello следующее:

1. Укажите значения SMTP hello, включая hello SMTP-серверу, что для SendGrid является smtp.sendgrid.net.

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

1. Расширить hello *javax.mail.Authenticator* класса и в реализации *getPasswordAuthentication* метод, возвращающий SendGrid имя пользователя и пароль.  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. Создайте сеанс электронной почты, прошедший проверку подлинности, с помощью объекта *javax.mail.Session* .  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. Создайте сообщение и назначьте значения полей **Кому**, **От**, **Тема** и содержимое. Это показано в hello [How To: сообщения электронной почты](#how-to-create-an-email) раздела.
4. Отправить сообщение hello с *javax.mail.Transport* объекта. Это показано в hello [How To: отправить сообщение электронной почты] [как: отправить сообщение электронной почты] раздел.

## <a name="how-to-create-an-email"></a>Практическое руководство. Создание сообщения электронной почты
Hello Далее показано, как значения toospecify для сообщения электронной почты.

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
Здравствуйте, следуя показано как toosend сообщение электронной почты.

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a>Практическое руководство. Добавление вложения
Hello следующем примере кода показано, как tooadd вложения.

    // Local file name and path.
    String attachmentName = "myfile.zip";
    String attachmentPath = "c:\\myfiles\\";
    MimeBodyPart attachmentPart = new MimeBodyPart();
    // Specify hello local file tooattach.
    DataSource source = new FileDataSource(attachmentPath + attachmentName);
    attachmentPart.setDataHandler(new DataHandler(source));
    // This example uses hello local file name as hello attachment name.
    // They could be different if you prefer.
    attachmentPart.setFileName(attachmentName);
    multipart.addBodyPart(attachmentPart);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a>Как: используйте фильтры tooenable нижние колонтитулы, отслеживания и аналитика
SendGrid предоставляет функциональные возможности дополнительный адрес электронной почты с использованием hello *фильтры*. Это параметры, которые могут быть добавлены tooan сообщение электронной почты для включения определенных функций, таких как включение отслеживание щелчков, Google analytics, отслеживание, подписки и т. д. Полный список фильтров см. в разделе [Filter Settings][Filter Settings] (Параметры фильтрации).

* Hello Далее показано, как tooinsert нижний колонтитул фильтрации, результатов отображаются внизу hello hello электронной почты, отправляемых в HTML-текст.

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* Еще одним примером фильтра является отслеживание щелчков. Предположим, что ваш текст сообщения электронной почты содержащего гиперссылку, такие как hello ниже, чтобы tootrack hello скорость:

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* tooenable hello щелкните отслеживания hello используйте следующий код:

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a>Практическое руководство. Обновление свойств электронной почты
Некоторые свойства электронной почты может быть перезаписана с помощью  **задать*свойство*** или добавляться с помощью  **добавить*свойство***.

Например, toospecify **ReplyTo** адреса, используйте hello ниже:

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

tooadd **Cc** получателей, используйте hello следующее:

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a>Практическое руководство. Использование дополнительных служб SendGrid
SendGrid предлагает веб-API можно использовать дополнительные возможности SendGrid tooleverage из приложения Azure. Дополнительные сведения см. в разделе hello [документации по SendGrid API][SendGrid API documentation].

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello hello служба SendGrid электронной почты, выполните следующие дополнительные toolearn ссылки.

* Пример, демонстрирующий использование SendGrid в развертывания Azure: [как toosend электронной почты с помощью SendGrid из Java в среде Azure](store-sendgrid-java-how-to-send-email-example.md)
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
[доставку транзакционных писем]: https://sendgrid.com/transactional-email
