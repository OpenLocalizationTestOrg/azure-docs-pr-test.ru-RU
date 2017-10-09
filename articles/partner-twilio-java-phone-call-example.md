---
title: "aaaHow tooMake телефонный звонок с Twilio (Java) | Документы Microsoft"
description: "Узнайте, как вызвать toomake телефон с веб-страницы с использованием Twilio в Java-приложении в Azure."
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 0381789e-e775-41a0-a784-294275192b1d
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 04fe5a78d431a79790dee3ca75c2b004aea4345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-java-application-on-azure"></a>Как tooMake Twilio с помощью телефонного звонка в приложении Java в Azure
Hello пример вы использование Twilio toomake вызов веб-страницы, размещенной в Azure. полученное приложение Hello пользователю будет предложено hello ввести значения телефонного вызова, как показано на следующий снимок экрана приветствия.

![Форма вызова Azure с помощью Twilio и Java][twilio_java]

Вам потребуется следующее hello toodo toouse hello кода в этом разделе:

1. Получение учетной записи Twilio и токена подтверждения подлинности. Оценка tooget к работе с Twilio, цены на [http://www.twilio.com/pricing][twilio_pricing]. Вы можете зарегистрироваться на [https://www.twilio.com/try-twilio][try_twilio]. Сведения об API, предоставляемые Twilio hello см. в разделе [http://www.twilio.com/api][twilio_api].
2. Получите Twilio JAR hello. В [https://github.com/twilio/twilio-java][twilio_java_github], можно загрузить исходных GitHub hello и создать собственные JAR или загрузить предварительно построенного JAR-ФАЙЛ (с или без зависимостей).
   в этом разделе код Hello было написано с помощью hello готовые JAR TwilioJava 3.3.8 with dependencies.
3. Добавьте JAR tooyour hello, путь построения Java.
4. При использовании Eclipse toocreate этого приложения Java, включают hello Twilio JAR в файл развертывания приложения (WAR) с помощью функции сборки развертывания Eclipse. Если вы не используете Eclipse toocreate этого приложения Java, обеспечить включение hello Twilio JAR в hello же роли Azure как путь приложения и добавлены toohello класс Java приложения.
5. Убедитесь в хранилище ключей cacerts содержит hello Equifax Secure центром сертификации сертификат с MD5 отпечатков пальцев 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (последовательный номер 35:DE:F4:CF и отпечаток hello SHA1 D2:32:09:AD:23:D hello 3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A). Это hello сертификат центра сертификации (ЦС) для hello [https://api.twilio.com] [ twilio_api_service] службы, которая вызывается при использовании API Twilio. Сведения о добавлении хранилища cacert этот ЦС сертификата tooyour JDK см. в разделе [Добавление toohello сертификат, в хранилище сертификатов ЦС Java][add_ca_cert].

Кроме того, вы знакомы с hello данных во время [создание с помощью приложения Hello World hello средств Azure для Eclipse][azure_java_eclipse_hello_world], или с помощью других методов для размещения приложений Java в Azure Если вы Вы не используете Eclipse, настоятельно рекомендуется.

## <a name="create-a-web-form-for-making-a-call"></a>Создание веб-формы для выполнения звонка
Hello, следующий код показывает, как данные пользователя tooretrieve подключения формы toocreate веб-узла. В этом примере создается динамический веб-проект **TwilioCloud**, в который в качестве JSP-файла добавляется файл **callform.jsp**.

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Automated call form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Make this call</b>.</p>
     <br/>
      <form action="makecall.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="callTo" value="" />
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="callFrom" value="" />
           </td>
         </tr>
         <tr>
           <td>Call message:</td>
           <td><input type="text" size=400 name="callText" value="Hello. This is hello call text. Good bye." />
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Make this call" />
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toomake-hello-call"></a>Создание вызова hello toomake кода hello
Hello следующий код, который вызывается, когда пользователь hello завершает hello формы, отображаемого элементом callform.jsp, создает сообщение о вызове hello и приводит к возникновению ошибки вызова hello. Для целей этого примера hello JSP-файл с именем **makecall.jsp** и может быть добавлена toohello **TwilioCloud** проекта. (Использование учетной записи Twilio и проверки подлинности маркера вместо значения заполнителей hello, назначенный слишком**accountSID** и **authToken** в следующем примере кода hello.)

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    import="java.util.*"
    import="com.twilio.*"
    import="com.twilio.sdk.*"
    import="com.twilio.sdk.resource.factory.*"
    import="com.twilio.sdk.resource.instance.*"
    pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Call processing happens here</title>
    </head>
    <body>
        <b>This is my make call page.</b><p/>
     <%
    try 
    {
         // Use your account SID and authentication token instead
         // of hello placeholders shown here.
         String accountSID = "your_twilio_account";
         String authToken = "your_twilio_authentication_token";

         // Instantiate an instance of hello Twilio client.     
         TwilioRestClient client;
         client = new TwilioRestClient(accountSID, authToken);

         // Retrieve hello account, used later tooretrieve hello CallFactory.
         Account account = client.getAccount();

         // Display hello client endpoint. 
         out.println("<p>Using Twilio endpoint " + client.getEndpoint() + ".</p>");

         // Display hello API version.
         String APIVERSION = TwilioRestClient.DEFAULT_VERSION;
         out.println("<p>Twilio client API version is " + APIVERSION + ".</p>");

         // Retrieve hello values entered by hello user.
         String callTo = request.getParameter("callTo");  
         // hello Outgoing Caller ID, used for hello From parameter,
         // must have previously been verified with Twilio.
         String callFrom = request.getParameter("callFrom");
         String userText = request.getParameter("callText");

         // Replace spaces in hello user's text with '%20', 
         // toomake hello text suitable for a URL.
         userText = userText.replace(" ", "%20");

         // Create a URL using hello Twilio message and hello user-entered text.
         String Url="http://twimlets.com/message";
         Url = Url + "?Message%5B0%5D=" + userText;

         // Display hello message URL.
         out.println("<p>");
         out.println("hello URL is " + Url);
         out.println("</p>");

         // Place hello call From, tooand URL values into a hash map. 
         HashMap<String, String> params = new HashMap<String, String>();
         params.put("From", callFrom);
         params.put("To", callTo);
         params.put("Url", Url);

         CallFactory callFactory = account.getCallFactory();
         Call call = callFactory.create(params);
         out.println("<p>Call status: " + call.getStatus()  + "</p>"); 
    } 
    catch (TwilioRestException e) 
    {
        out.println("<p>TwilioRestException encountered: " + e.getMessage() + "</p>");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    catch (Exception e) 
    {
        out.println("<p>Exception encountered: " + e.getMessage() + "");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    %>
    </body>
    </html>

Кроме toomaking hello вызовов, makecall.jsp в конечную точку Twilio hello, версия API и состояние вызова hello. Примером является следующий снимок экрана приветствия:

![Ответ на звонок Azure с помощью Twilio и Java][twilio_java_response]

## <a name="run-hello-application"></a>Запустите приложение hello
Следующие являются hello toorun высокоуровневые действия приложения; сведения о эти действия можно найти в [создание с помощью приложения Hello World hello средств Azure для Eclipse][azure_java_eclipse_hello_world].

1. Экспорт вашей TwilioCloud WAR toohello Azure **approot** папки. 
2. Изменить **startup.cmd** toounzip вашей TwilioCloud WAR.
3. Скомпилируйте приложение для hello эмулятор вычислений.
4. Запустите развертывание в эмуляторе вычислений hello.
5. Откройте браузер и введите адрес **http://localhost:8080/TwilioCloud/callform.jsp**.
6. Введите значения в форме hello, нажмите кнопку **вызывать этот метод**, а затем просмотреть результаты hello в makecall.jsp.

Когда вы будете готовы toodeploy tooAzure, повторной компиляции для развертывания toohello облака, tooAzure развертывания и запуска http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp в браузере hello (заменить значения для *your_hosted_name*).

## <a name="next-steps"></a>Дальнейшие действия
Этот код был предоставлен tooshow вы основные функциональные возможности с использованием Twilio в Java в Azure. Перед развертыванием tooAzure в рабочей среде, вы можете tooadd дополнительные обработки ошибок или других компонентов. Например:

* Вместо использования веб-формы, может использовать хранилища Azure BLOB-объектов или базы данных SQL toostore телефонных номеров и вызовите текста. Сведения об использовании больших двоичных объектов хранилища Azure в Java см. в разделе [как tooUse hello службы хранилища больших двоичных объектов из Java][howto_blob_storage_java]. Сведения об использовании базы данных SQL в Java см. в разделе [с помощью базы данных SQL в Java][howto_sql_azure_java].
* Можно использовать **RoleEnvironment.getConfigurationSettings** идентификатор учетной записи Twilio tooretrieve hello и проверки подлинности токена из параметры конфигурации развертывания, а не жестко запрограммированных значений hello в makecall.jsp. Сведения о hello **RoleEnvironment** см. в описании [hello использование библиотеки среды выполнения службы Azure в JSP] [ azure_runtime_jsp] и hello документации пакета среды выполнения служб Azure в [http://dl.windowsazure.com/javadoc][azure_javadoc].
* Hello makecall.jsp код присваивает URL-АДРЕСЕ предоставляемых системой Twilio, [http://twimlets.com/message][twimlet_message_url], toohello **URL-адрес** переменной. Этот URL-адрес предоставляет ответ языка разметки Twilio (TwiML) о том, как вызвать tooproceed с hello Twilio. Например, может содержать hello TwiML, который возвращается  **&lt;Say&gt;**  команду, которая приводит к текст будет произноситься toohello получателя вызова. Вместо hello Twilio предоставленный URL-адрес, можно строить собственные службы tooTwilio toorespond запроса; Дополнительные сведения см. в разделе [как tooUse Twilio для голосовых возможностей и SMS в Java][howto_twilio_voice_sms_java]. Дополнительные сведения о TwiML можно найти в [http://www.twilio.com/docs/api/twiml][twiml]и Дополнительные сведения о  **&lt;Say&gt;**  и другие команды Twilio можно найти в [http://www.twilio.com/docs/api/twiml/say][twilio_say].
* Прочитать рекомендации по безопасности Twilio hello в [https://www.twilio.com/docs/security][twilio_docs_security].

Дополнительные сведения о Twilio см. на сайте [https://www.twilio.com/docs][twilio_docs].

## <a name="see-also"></a>См. также
* [Как tooUse Twilio для голосовых возможностей и SMS в Java][howto_twilio_voice_sms_java]
* [Добавление сертификата toohello Java хранилища сертификатов центра сертификации][add_ca_cert]

[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/api
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_java_github]: http://github.com/twilio/twilio-java
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[azure_java_eclipse_hello_world]: http://msdn.microsoft.com/library/windowsazure/hh690944.aspx
[howto_twilio_voice_sms_java]: partner-twilio-java-how-to-use-voice-sms.md
[howto_blob_storage_java]: http://www.windowsazure.com/develop/java/how-to-guides/blob-storage/
[howto_sql_azure_java]: http://msdn.microsoft.com/library/windowsazure/hh749029.aspx
[azure_runtime_jsp]: http://msdn.microsoft.com/library/windowsazure/hh690948.aspx
[azure_javadoc]: http://dl.windowsazure.com/javadoc
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[twilio_java]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaCallForm.jpg
[twilio_java_response]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaMakeCall.jpg
