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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-java-application-on-azure"></a><span data-ttu-id="3b630-103">Как tooMake Twilio с помощью телефонного звонка в приложении Java в Azure</span><span class="sxs-lookup"><span data-stu-id="3b630-103">How tooMake a Phone Call Using Twilio in a Java Application on Azure</span></span>
<span data-ttu-id="3b630-104">Hello пример вы использование Twilio toomake вызов веб-страницы, размещенной в Azure.</span><span class="sxs-lookup"><span data-stu-id="3b630-104">hello following example shows you how you can use Twilio toomake a call from a web page hosted in Azure.</span></span> <span data-ttu-id="3b630-105">полученное приложение Hello пользователю будет предложено hello ввести значения телефонного вызова, как показано на следующий снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="3b630-105">hello resulting application will prompt hello user for phone call values, as shown in hello following screen shot.</span></span>

![Форма вызова Azure с помощью Twilio и Java][twilio_java]

<span data-ttu-id="3b630-107">Вам потребуется следующее hello toodo toouse hello кода в этом разделе:</span><span class="sxs-lookup"><span data-stu-id="3b630-107">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="3b630-108">Получение учетной записи Twilio и токена подтверждения подлинности.</span><span class="sxs-lookup"><span data-stu-id="3b630-108">Acquire a Twilio account and authentication token.</span></span> <span data-ttu-id="3b630-109">Оценка tooget к работе с Twilio, цены на [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="3b630-109">tooget started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="3b630-110">Вы можете зарегистрироваться на [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="3b630-110">You can sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="3b630-111">Сведения об API, предоставляемые Twilio hello см. в разделе [http://www.twilio.com/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="3b630-111">For information about hello API provided by Twilio, see [http://www.twilio.com/api][twilio_api].</span></span>
2. <span data-ttu-id="3b630-112">Получите Twilio JAR hello.</span><span class="sxs-lookup"><span data-stu-id="3b630-112">Obtain hello Twilio JAR.</span></span> <span data-ttu-id="3b630-113">В [https://github.com/twilio/twilio-java][twilio_java_github], можно загрузить исходных GitHub hello и создать собственные JAR или загрузить предварительно построенного JAR-ФАЙЛ (с или без зависимостей).</span><span class="sxs-lookup"><span data-stu-id="3b630-113">At [https://github.com/twilio/twilio-java][twilio_java_github], you can download hello GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
   <span data-ttu-id="3b630-114">в этом разделе код Hello было написано с помощью hello готовые JAR TwilioJava 3.3.8 with dependencies.</span><span class="sxs-lookup"><span data-stu-id="3b630-114">hello code in this topic was written using hello pre-built TwilioJava-3.3.8-with-dependencies JAR.</span></span>
3. <span data-ttu-id="3b630-115">Добавьте JAR tooyour hello, путь построения Java.</span><span class="sxs-lookup"><span data-stu-id="3b630-115">Add hello JAR tooyour Java build path.</span></span>
4. <span data-ttu-id="3b630-116">При использовании Eclipse toocreate этого приложения Java, включают hello Twilio JAR в файл развертывания приложения (WAR) с помощью функции сборки развертывания Eclipse.</span><span class="sxs-lookup"><span data-stu-id="3b630-116">If you are using Eclipse toocreate this Java application, include hello Twilio JAR in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="3b630-117">Если вы не используете Eclipse toocreate этого приложения Java, обеспечить включение hello Twilio JAR в hello же роли Azure как путь приложения и добавлены toohello класс Java приложения.</span><span class="sxs-lookup"><span data-stu-id="3b630-117">If you are not using Eclipse toocreate this Java application, ensure hello Twilio JAR is included within hello same Azure role as your Java application, and added toohello class path of your application.</span></span>
5. <span data-ttu-id="3b630-118">Убедитесь в хранилище ключей cacerts содержит hello Equifax Secure центром сертификации сертификат с MD5 отпечатков пальцев 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (последовательный номер 35:DE:F4:CF и отпечаток hello SHA1 D2:32:09:AD:23:D hello 3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="3b630-118">Ensure your cacerts keystore contains hello Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello serial number is 35:DE:F4:CF and hello SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="3b630-119">Это hello сертификат центра сертификации (ЦС) для hello [https://api.twilio.com] [ twilio_api_service] службы, которая вызывается при использовании API Twilio.</span><span class="sxs-lookup"><span data-stu-id="3b630-119">This is hello certificate authority (CA) certificate for hello [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="3b630-120">Сведения о добавлении хранилища cacert этот ЦС сертификата tooyour JDK см. в разделе [Добавление toohello сертификат, в хранилище сертификатов ЦС Java][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="3b630-120">For information about adding this CA certificate tooyour JDK's cacert store, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="3b630-121">Кроме того, вы знакомы с hello данных во время [создание с помощью приложения Hello World hello средств Azure для Eclipse][azure_java_eclipse_hello_world], или с помощью других методов для размещения приложений Java в Azure Если вы Вы не используете Eclipse, настоятельно рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="3b630-121">Additionally, familiarity with hello information at [Creating a Hello World Application Using hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world], or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="3b630-122">Создание веб-формы для выполнения звонка</span><span class="sxs-lookup"><span data-stu-id="3b630-122">Create a web form for making a call</span></span>
<span data-ttu-id="3b630-123">Hello, следующий код показывает, как данные пользователя tooretrieve подключения формы toocreate веб-узла.</span><span class="sxs-lookup"><span data-stu-id="3b630-123">hello following code shows how toocreate a web form tooretrieve user data for making a call.</span></span> <span data-ttu-id="3b630-124">В этом примере создается динамический веб-проект **TwilioCloud**, в который в качестве JSP-файла добавляется файл **callform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="3b630-124">For purposes of this example, a new dynamic web project, named **TwilioCloud**, was created, and **callform.jsp** was added as a JSP file.</span></span>

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

## <a name="create-hello-code-toomake-hello-call"></a><span data-ttu-id="3b630-125">Создание вызова hello toomake кода hello</span><span class="sxs-lookup"><span data-stu-id="3b630-125">Create hello code toomake hello call</span></span>
<span data-ttu-id="3b630-126">Hello следующий код, который вызывается, когда пользователь hello завершает hello формы, отображаемого элементом callform.jsp, создает сообщение о вызове hello и приводит к возникновению ошибки вызова hello.</span><span class="sxs-lookup"><span data-stu-id="3b630-126">hello following code, which is called when hello user completes hello form displayed by callform.jsp, creates hello call message and generates hello call.</span></span> <span data-ttu-id="3b630-127">Для целей этого примера hello JSP-файл с именем **makecall.jsp** и может быть добавлена toohello **TwilioCloud** проекта.</span><span class="sxs-lookup"><span data-stu-id="3b630-127">For purposes of this example, hello JSP file is named **makecall.jsp** and was added toohello **TwilioCloud** project.</span></span> <span data-ttu-id="3b630-128">(Использование учетной записи Twilio и проверки подлинности маркера вместо значения заполнителей hello, назначенный слишком**accountSID** и **authToken** в следующем примере кода hello.)</span><span class="sxs-lookup"><span data-stu-id="3b630-128">(Use your Twilio account and authentication token instead of hello placeholder values assigned too**accountSID** and **authToken** in hello code below.)</span></span>

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

<span data-ttu-id="3b630-129">Кроме toomaking hello вызовов, makecall.jsp в конечную точку Twilio hello, версия API и состояние вызова hello.</span><span class="sxs-lookup"><span data-stu-id="3b630-129">In addition toomaking hello call, makecall.jsp displays hello Twilio endpoint, API version, and hello call status.</span></span> <span data-ttu-id="3b630-130">Примером является следующий снимок экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="3b630-130">An example is hello following screen shot:</span></span>

![Ответ на звонок Azure с помощью Twilio и Java][twilio_java_response]

## <a name="run-hello-application"></a><span data-ttu-id="3b630-132">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="3b630-132">Run hello application</span></span>
<span data-ttu-id="3b630-133">Следующие являются hello toorun высокоуровневые действия приложения; сведения о эти действия можно найти в [создание с помощью приложения Hello World hello средств Azure для Eclipse][azure_java_eclipse_hello_world].</span><span class="sxs-lookup"><span data-stu-id="3b630-133">Following are hello high-level steps toorun your application; details for these steps can be found at [Creating a Hello World Application Using hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world].</span></span>

1. <span data-ttu-id="3b630-134">Экспорт вашей TwilioCloud WAR toohello Azure **approot** папки.</span><span class="sxs-lookup"><span data-stu-id="3b630-134">Export your TwilioCloud WAR toohello Azure **approot** folder.</span></span> 
2. <span data-ttu-id="3b630-135">Изменить **startup.cmd** toounzip вашей TwilioCloud WAR.</span><span class="sxs-lookup"><span data-stu-id="3b630-135">Modify **startup.cmd** toounzip your TwilioCloud WAR.</span></span>
3. <span data-ttu-id="3b630-136">Скомпилируйте приложение для hello эмулятор вычислений.</span><span class="sxs-lookup"><span data-stu-id="3b630-136">Compile your application for hello compute emulator.</span></span>
4. <span data-ttu-id="3b630-137">Запустите развертывание в эмуляторе вычислений hello.</span><span class="sxs-lookup"><span data-stu-id="3b630-137">Start your deployment in hello compute emulator.</span></span>
5. <span data-ttu-id="3b630-138">Откройте браузер и введите адрес **http://localhost:8080/TwilioCloud/callform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="3b630-138">Open a browser, and run **http://localhost:8080/TwilioCloud/callform.jsp**.</span></span>
6. <span data-ttu-id="3b630-139">Введите значения в форме hello, нажмите кнопку **вызывать этот метод**, а затем просмотреть результаты hello в makecall.jsp.</span><span class="sxs-lookup"><span data-stu-id="3b630-139">Enter values in hello form, click **Make this call**, and then see hello results in makecall.jsp.</span></span>

<span data-ttu-id="3b630-140">Когда вы будете готовы toodeploy tooAzure, повторной компиляции для развертывания toohello облака, tooAzure развертывания и запуска http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp в браузере hello (заменить значения для *your_hosted_name*).</span><span class="sxs-lookup"><span data-stu-id="3b630-140">When you are ready toodeploy tooAzure, recompile for deployment toohello cloud, deploy tooAzure, and run http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp in hello browser (substitute your value for *your_hosted_name*).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b630-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3b630-141">Next steps</span></span>
<span data-ttu-id="3b630-142">Этот код был предоставлен tooshow вы основные функциональные возможности с использованием Twilio в Java в Azure.</span><span class="sxs-lookup"><span data-stu-id="3b630-142">This code was provided tooshow you basic functionality using Twilio in Java on Azure.</span></span> <span data-ttu-id="3b630-143">Перед развертыванием tooAzure в рабочей среде, вы можете tooadd дополнительные обработки ошибок или других компонентов.</span><span class="sxs-lookup"><span data-stu-id="3b630-143">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="3b630-144">Например:</span><span class="sxs-lookup"><span data-stu-id="3b630-144">For example:</span></span>

* <span data-ttu-id="3b630-145">Вместо использования веб-формы, может использовать хранилища Azure BLOB-объектов или базы данных SQL toostore телефонных номеров и вызовите текста.</span><span class="sxs-lookup"><span data-stu-id="3b630-145">Instead of using a web form, you could use Azure storage blobs or SQL Database toostore phone numbers and call text.</span></span> <span data-ttu-id="3b630-146">Сведения об использовании больших двоичных объектов хранилища Azure в Java см. в разделе [как tooUse hello службы хранилища больших двоичных объектов из Java][howto_blob_storage_java].</span><span class="sxs-lookup"><span data-stu-id="3b630-146">For information about using Azure storage blobs in Java, see [How tooUse hello Blob Storage Service from Java][howto_blob_storage_java].</span></span> <span data-ttu-id="3b630-147">Сведения об использовании базы данных SQL в Java см. в разделе [с помощью базы данных SQL в Java][howto_sql_azure_java].</span><span class="sxs-lookup"><span data-stu-id="3b630-147">For information about using SQL Database in Java, see [Using SQL Database in Java][howto_sql_azure_java].</span></span>
* <span data-ttu-id="3b630-148">Можно использовать **RoleEnvironment.getConfigurationSettings** идентификатор учетной записи Twilio tooretrieve hello и проверки подлинности токена из параметры конфигурации развертывания, а не жестко запрограммированных значений hello в makecall.jsp.</span><span class="sxs-lookup"><span data-stu-id="3b630-148">You could use **RoleEnvironment.getConfigurationSettings** tooretrieve hello Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding hello values in makecall.jsp.</span></span> <span data-ttu-id="3b630-149">Сведения о hello **RoleEnvironment** см. в описании [hello использование библиотеки среды выполнения службы Azure в JSP] [ azure_runtime_jsp] и hello документации пакета среды выполнения служб Azure в [http://dl.windowsazure.com/javadoc][azure_javadoc].</span><span class="sxs-lookup"><span data-stu-id="3b630-149">For information about hello **RoleEnvironment** class, see [Using hello Azure Service Runtime Library in JSP][azure_runtime_jsp] and hello Azure Service Runtime package documentation at [http://dl.windowsazure.com/javadoc][azure_javadoc].</span></span>
* <span data-ttu-id="3b630-150">Hello makecall.jsp код присваивает URL-АДРЕСЕ предоставляемых системой Twilio, [http://twimlets.com/message][twimlet_message_url], toohello **URL-адрес** переменной.</span><span class="sxs-lookup"><span data-stu-id="3b630-150">hello makecall.jsp code assigns a Twilio-provided URL, [http://twimlets.com/message][twimlet_message_url], toohello **Url** variable.</span></span> <span data-ttu-id="3b630-151">Этот URL-адрес предоставляет ответ языка разметки Twilio (TwiML) о том, как вызвать tooproceed с hello Twilio.</span><span class="sxs-lookup"><span data-stu-id="3b630-151">This URL provides a Twilio Markup Language (TwiML) response that informs Twilio how tooproceed with hello call.</span></span> <span data-ttu-id="3b630-152">Например, может содержать hello TwiML, который возвращается  **&lt;Say&gt;**  команду, которая приводит к текст будет произноситься toohello получателя вызова.</span><span class="sxs-lookup"><span data-stu-id="3b630-152">For example, hello TwiML that is returned can contain a **&lt;Say&gt;** verb that results in text being spoken toohello call recipient.</span></span> <span data-ttu-id="3b630-153">Вместо hello Twilio предоставленный URL-адрес, можно строить собственные службы tooTwilio toorespond запроса; Дополнительные сведения см. в разделе [как tooUse Twilio для голосовых возможностей и SMS в Java][howto_twilio_voice_sms_java].</span><span class="sxs-lookup"><span data-stu-id="3b630-153">Instead of using hello Twilio-provided URL, you could build your own service toorespond tooTwilio's request; for more information, see [How tooUse Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java].</span></span> <span data-ttu-id="3b630-154">Дополнительные сведения о TwiML можно найти в [http://www.twilio.com/docs/api/twiml][twiml]и Дополнительные сведения о  **&lt;Say&gt;**  и другие команды Twilio можно найти в [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="3b630-154">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about **&lt;Say&gt;** and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="3b630-155">Прочитать рекомендации по безопасности Twilio hello в [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="3b630-155">Read hello Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="3b630-156">Дополнительные сведения о Twilio см. на сайте [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="3b630-156">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="3b630-157">См. также</span><span class="sxs-lookup"><span data-stu-id="3b630-157">See Also</span></span>
* <span data-ttu-id="3b630-158">[Как tooUse Twilio для голосовых возможностей и SMS в Java][howto_twilio_voice_sms_java]</span><span class="sxs-lookup"><span data-stu-id="3b630-158">[How tooUse Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java]</span></span>
* <span data-ttu-id="3b630-159">[Добавление сертификата toohello Java хранилища сертификатов центра сертификации][add_ca_cert]</span><span class="sxs-lookup"><span data-stu-id="3b630-159">[Adding a Certificate toohello Java CA Certificate Store][add_ca_cert]</span></span>

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
