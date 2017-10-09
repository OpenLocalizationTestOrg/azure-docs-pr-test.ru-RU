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
# <a name="how-toosend-email-using-sendgrid-from-java"></a><span data-ttu-id="0005d-104">Как tooSend электронной почты с помощью SendGrid из Java</span><span class="sxs-lookup"><span data-stu-id="0005d-104">How tooSend Email Using SendGrid from Java</span></span>
<span data-ttu-id="0005d-105">В этом руководстве показано, как tooperform часто встречающиеся задачи программирования с помощью SendGrid электронной почты службы в Azure.</span><span class="sxs-lookup"><span data-stu-id="0005d-105">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="0005d-106">Hello примеры написаны на Java.</span><span class="sxs-lookup"><span data-stu-id="0005d-106">hello samples are written in Java.</span></span> <span data-ttu-id="0005d-107">Hello сценарии включают **построении электронной почты**, **отправке сообщения электронной почты**, **Добавление вложений**, **с помощью фильтров**и **обновление свойств**.</span><span class="sxs-lookup"><span data-stu-id="0005d-107">hello scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="0005d-108">Дополнительные сведения о SendGrid и отправке сообщения электронной почты см. в разделе hello [дальнейшие действия](#next-steps) раздела.</span><span class="sxs-lookup"><span data-stu-id="0005d-108">For more information on SendGrid and sending email, see hello [Next steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="0005d-109">Что такое hello SendGrid службы электронной почты?</span><span class="sxs-lookup"><span data-stu-id="0005d-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="0005d-110">SendGrid — это [облачная служба электронной почты], которая обеспечивает надежную [доставку транзакционных писем], предоставляет возможности масштабирования и аналитики в реальном времени, а также предоставляет гибкие интерфейсы API для пользовательской интеграции.</span><span class="sxs-lookup"><span data-stu-id="0005d-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="0005d-111">Ниже перечислены наиболее распространенные сценарии использования SendGrid.</span><span class="sxs-lookup"><span data-stu-id="0005d-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="0005d-112">Отправлять уведомления toocustomers автоматически</span><span class="sxs-lookup"><span data-stu-id="0005d-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="0005d-113">Администрирование списков рассылки для ежемесячной отправки клиентам электронных листовок и специальных предложений</span><span class="sxs-lookup"><span data-stu-id="0005d-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="0005d-114">Сбор показателей в режиме реального времени по таким параметрам, как заблокированная электронная почта и реагирование клиентов</span><span class="sxs-lookup"><span data-stu-id="0005d-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="0005d-115">Создание отчетов с тенденциями toohelp</span><span class="sxs-lookup"><span data-stu-id="0005d-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="0005d-116">Пересылка запросов клиентов</span><span class="sxs-lookup"><span data-stu-id="0005d-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="0005d-117">Уведомления от приложения по электронной почте</span><span class="sxs-lookup"><span data-stu-id="0005d-117">Email notifications from your application</span></span>

<span data-ttu-id="0005d-118">Дополнительные сведения см. на веб-сайте <http://sendgrid.com>.</span><span class="sxs-lookup"><span data-stu-id="0005d-118">For more information, see <http://sendgrid.com>.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="0005d-119">Создание учетной записи SendGrid</span><span class="sxs-lookup"><span data-stu-id="0005d-119">Create a SendGrid account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a><span data-ttu-id="0005d-120">Как: использование библиотек javax.mail hello</span><span class="sxs-lookup"><span data-stu-id="0005d-120">How to: Use hello javax.mail libraries</span></span>
<span data-ttu-id="0005d-121">Получить hello javax.mail библиотеки, например <http://www.oracle.com/technetwork/java/javamail> и импортировать их в коде.</span><span class="sxs-lookup"><span data-stu-id="0005d-121">Obtain hello javax.mail libraries, for example from <http://www.oracle.com/technetwork/java/javamail> and import them into your code.</span></span> <span data-ttu-id="0005d-122">На высоком уровне hello hello javax.mail библиотеки toosend по электронной почте с помощью SMTP с помощью выполняется toodo hello следующее:</span><span class="sxs-lookup"><span data-stu-id="0005d-122">At a high-level, hello process for using hello javax.mail library toosend email using SMTP is toodo hello following:</span></span>

1. <span data-ttu-id="0005d-123">Укажите значения SMTP hello, включая hello SMTP-серверу, что для SendGrid является smtp.sendgrid.net.</span><span class="sxs-lookup"><span data-stu-id="0005d-123">Specify hello SMTP values, including hello SMTP server, which for SendGrid is smtp.sendgrid.net.</span></span>

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

1. <span data-ttu-id="0005d-124">Расширить hello *javax.mail.Authenticator* класса и в реализации *getPasswordAuthentication* метод, возвращающий SendGrid имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="0005d-124">Extend hello *javax.mail.Authenticator* class, and in your implementation of the *getPasswordAuthentication* method, return your SendGrid user name and password.</span></span>  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. <span data-ttu-id="0005d-125">Создайте сеанс электронной почты, прошедший проверку подлинности, с помощью объекта *javax.mail.Session* .</span><span class="sxs-lookup"><span data-stu-id="0005d-125">Create an authenticated email session through a *javax.mail.Session* object.</span></span>  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. <span data-ttu-id="0005d-126">Создайте сообщение и назначьте значения полей **Кому**, **От**, **Тема** и содержимое.</span><span class="sxs-lookup"><span data-stu-id="0005d-126">Create your message and assign **To**, **From**, **Subject** and content values.</span></span> <span data-ttu-id="0005d-127">Это показано в hello [How To: сообщения электронной почты](#how-to-create-an-email) раздела.</span><span class="sxs-lookup"><span data-stu-id="0005d-127">This is shown in hello [How To: Create an Email](#how-to-create-an-email) section.</span></span>
4. <span data-ttu-id="0005d-128">Отправить сообщение hello с *javax.mail.Transport* объекта.</span><span class="sxs-lookup"><span data-stu-id="0005d-128">Send hello message through a *javax.mail.Transport* object.</span></span> <span data-ttu-id="0005d-129">Это показано в hello [How To: отправить сообщение электронной почты] [как: отправить сообщение электронной почты] раздел.</span><span class="sxs-lookup"><span data-stu-id="0005d-129">This is shown in hello [How To: Send an Email][How to: Send an Email] section.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="0005d-130">Практическое руководство. Создание сообщения электронной почты</span><span class="sxs-lookup"><span data-stu-id="0005d-130">How to: Create an email</span></span>
<span data-ttu-id="0005d-131">Hello Далее показано, как значения toospecify для сообщения электронной почты.</span><span class="sxs-lookup"><span data-stu-id="0005d-131">hello following shows how toospecify values for an email.</span></span>

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

## <a name="how-to-send-an-email"></a><span data-ttu-id="0005d-132">Практическое руководство. Отправка сообщения эл. почты</span><span class="sxs-lookup"><span data-stu-id="0005d-132">How to: Send an email</span></span>
<span data-ttu-id="0005d-133">Здравствуйте, следуя показано как toosend сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="0005d-133">hello following shows how toosend an email.</span></span>

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="0005d-134">Практическое руководство. Добавление вложения</span><span class="sxs-lookup"><span data-stu-id="0005d-134">How to: Add an attachment</span></span>
<span data-ttu-id="0005d-135">Hello следующем примере кода показано, как tooadd вложения.</span><span class="sxs-lookup"><span data-stu-id="0005d-135">hello following code shows you how tooadd an attachment.</span></span>

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

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="0005d-136">Как: используйте фильтры tooenable нижние колонтитулы, отслеживания и аналитика</span><span class="sxs-lookup"><span data-stu-id="0005d-136">How to: Use filters tooenable footers, tracking, and analytics</span></span>
<span data-ttu-id="0005d-137">SendGrid предоставляет функциональные возможности дополнительный адрес электронной почты с использованием hello *фильтры*.</span><span class="sxs-lookup"><span data-stu-id="0005d-137">SendGrid provides additional email functionality through hello use of *filters*.</span></span> <span data-ttu-id="0005d-138">Это параметры, которые могут быть добавлены tooan сообщение электронной почты для включения определенных функций, таких как включение отслеживание щелчков, Google analytics, отслеживание, подписки и т. д.</span><span class="sxs-lookup"><span data-stu-id="0005d-138">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="0005d-139">Полный список фильтров см. в разделе [Filter Settings][Filter Settings] (Параметры фильтрации).</span><span class="sxs-lookup"><span data-stu-id="0005d-139">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

* <span data-ttu-id="0005d-140">Hello Далее показано, как tooinsert нижний колонтитул фильтрации, результатов отображаются внизу hello hello электронной почты, отправляемых в HTML-текст.</span><span class="sxs-lookup"><span data-stu-id="0005d-140">hello following shows how tooinsert a footer filter that results in HTML text appearing at hello bottom of hello email being sent.</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* <span data-ttu-id="0005d-141">Еще одним примером фильтра является отслеживание щелчков.</span><span class="sxs-lookup"><span data-stu-id="0005d-141">Another example of a filter is click tracking.</span></span> <span data-ttu-id="0005d-142">Предположим, что ваш текст сообщения электронной почты содержащего гиперссылку, такие как hello ниже, чтобы tootrack hello скорость:</span><span class="sxs-lookup"><span data-stu-id="0005d-142">Let’s say that your email text contains a hyperlink, such as hello following, and you want tootrack hello click rate:</span></span>

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* <span data-ttu-id="0005d-143">tooenable hello щелкните отслеживания hello используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="0005d-143">tooenable hello click tracking, use hello following code:</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a><span data-ttu-id="0005d-144">Практическое руководство. Обновление свойств электронной почты</span><span class="sxs-lookup"><span data-stu-id="0005d-144">How to: Update email properties</span></span>
<span data-ttu-id="0005d-145">Некоторые свойства электронной почты может быть перезаписана с помощью  **задать*свойство*** или добавляться с помощью  **добавить*свойство***.</span><span class="sxs-lookup"><span data-stu-id="0005d-145">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span>

<span data-ttu-id="0005d-146">Например, toospecify **ReplyTo** адреса, используйте hello ниже:</span><span class="sxs-lookup"><span data-stu-id="0005d-146">For example, toospecify **ReplyTo** addresses, use hello following:</span></span>

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

<span data-ttu-id="0005d-147">tooadd **Cc** получателей, используйте hello следующее:</span><span class="sxs-lookup"><span data-stu-id="0005d-147">tooadd a **Cc** recipient, use hello following:</span></span>

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="0005d-148">Практическое руководство. Использование дополнительных служб SendGrid</span><span class="sxs-lookup"><span data-stu-id="0005d-148">How to: Use additional SendGrid services</span></span>
<span data-ttu-id="0005d-149">SendGrid предлагает веб-API можно использовать дополнительные возможности SendGrid tooleverage из приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="0005d-149">SendGrid offers web-based APIs that you can use tooleverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="0005d-150">Дополнительные сведения см. в разделе hello [документации по SendGrid API][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="0005d-150">For full details, see hello [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="0005d-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0005d-151">Next steps</span></span>
<span data-ttu-id="0005d-152">Теперь, когда вы узнали основы hello hello служба SendGrid электронной почты, выполните следующие дополнительные toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="0005d-152">Now that you’ve learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="0005d-153">Пример, демонстрирующий использование SendGrid в развертывания Azure: [как toosend электронной почты с помощью SendGrid из Java в среде Azure](store-sendgrid-java-how-to-send-email-example.md)</span><span class="sxs-lookup"><span data-stu-id="0005d-153">Sample that demonstrates using SendGrid in an Azure deployment: [How toosend email using SendGrid from Java in an Azure deployment](store-sendgrid-java-how-to-send-email-example.md)</span></span>
* <span data-ttu-id="0005d-154">Пакет SDK SendGrid для Java: <https://sendgrid.com/docs/Code_Examples/java.html></span><span class="sxs-lookup"><span data-stu-id="0005d-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span></span>
* <span data-ttu-id="0005d-155">Документация по API SendGrid: <https://sendgrid.com/docs/API_Reference/index.html></span><span class="sxs-lookup"><span data-stu-id="0005d-155">SendGrid API documentation: <https://sendgrid.com/docs/API_Reference/index.html></span></span>
* <span data-ttu-id="0005d-156">Специальное предложение SendGrid для клиентов Azure: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="0005d-156">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

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
