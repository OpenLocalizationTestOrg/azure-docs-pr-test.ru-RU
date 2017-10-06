---
title: "aaaDeploy toohello Spring загрузки приложения службы приложений Azure | Документы Microsoft"
description: "Этот учебник поможет разработчиками с помощью hello действия toodeploy hello Spring начальной загрузки web app tooAzure службы приложений."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.openlocfilehash: 69f9c4903fd740125194402cdb4b4db46a1f2773
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-toohello-azure-app-service"></a><span data-ttu-id="fc995-103">Развертывание приложения загрузки Spring toohello службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="fc995-103">Deploy a Spring Boot Application toohello Azure App Service</span></span>

<span data-ttu-id="fc995-104">Hello  **[Spring Framework]**  — это решение с открытым исходным кодом, которое Java разработчики могут создавать приложения корпоративного уровня, и один из проектов более популярных hello которых построено на основе этой платформы [Загрузки spring], который предоставляет упрощенный подход для создания изолированного приложения Java.</span><span class="sxs-lookup"><span data-stu-id="fc995-104">hello **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications, and one of hello more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="fc995-105">Этот учебник поможет вам хотя Создание hello образец Spring начальной загрузки веб-приложения и развертывание слишком[службе приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="fc995-105">This tutorial will walk you though creating hello sample Spring Boot Getting Started web app and deploying it too[Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="fc995-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fc995-106">Prerequisites</span></span>

<span data-ttu-id="fc995-107">В порядке toocomplete hello шагов в этом учебнике требуется toohave hello следующее:</span><span class="sxs-lookup"><span data-stu-id="fc995-107">In order toocomplete hello steps in this tutorial, you need toohave hello following:</span></span>

* <span data-ttu-id="fc995-108">Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="fc995-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="fc995-109">Актуальная версия [Java Developer Kit (JDK)].</span><span class="sxs-lookup"><span data-stu-id="fc995-109">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="fc995-110">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="fc995-110">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="fc995-111">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="fc995-111">A [Git] client.</span></span>

## <a name="create-hello-spring-boot-getting-started-web-app"></a><span data-ttu-id="fc995-112">Создать hello Spring начальной загрузки веб-приложение</span><span class="sxs-lookup"><span data-stu-id="fc995-112">Create hello Spring Boot Getting Started web app</span></span>

<span data-ttu-id="fc995-113">Hello ниже поможет hello шаги, необходимые toocreate простого Spring загрузки веб-приложения и протестировать на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="fc995-113">hello following steps will walk you through hello steps that are required toocreate a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="fc995-114">Откройте командную строку и создать toohold локальный каталог, приложение и перейдите в каталог toothat; Например:</span><span class="sxs-lookup"><span data-stu-id="fc995-114">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="fc995-115">-- или --</span><span class="sxs-lookup"><span data-stu-id="fc995-115">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="fc995-116">Клон hello [Spring начальной загрузки] образец проекта в каталог hello, только что созданный; например:</span><span class="sxs-lookup"><span data-stu-id="fc995-116">Clone hello [Spring Boot Getting Started] sample project into hello directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="fc995-117">Изменение каталога toohello завершения проекта; Например:</span><span class="sxs-lookup"><span data-stu-id="fc995-117">Change directory toohello completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="fc995-118">Построение hello JAR-файл с помощью Maven; Например:</span><span class="sxs-lookup"><span data-stu-id="fc995-118">Build hello JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="fc995-119">После создания веб-приложения hello изменить каталог toohello JAR-файл и запустить веб-приложение hello; Например:</span><span class="sxs-lookup"><span data-stu-id="fc995-119">Once hello web app has been created, change directory toohello JAR file and start hello web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="fc995-120">Тестирование веб-приложения hello, перейдя в веб-браузере toohttp://localhost:8080, или с помощью синтаксиса hello как следующий пример, при наличии доступных перелистывание hello:</span><span class="sxs-lookup"><span data-stu-id="fc995-120">Test hello web app by browsing toohttp://localhost:8080 using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="fc995-121">Должно появиться сообщение, отображаемое после hello: **Greetings с Spring загрузки!**</span><span class="sxs-lookup"><span data-stu-id="fc995-121">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Обзор образца приложения][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="fc995-123">Создание веб-приложения Azure для использования с Java</span><span class="sxs-lookup"><span data-stu-id="fc995-123">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="fc995-124">Hello следующие шаги пошаговыми руководствами hello действия toocreate веб-приложение Azure, настройте hello необходимые параметры для Java и настроить учетные данные FTP.</span><span class="sxs-lookup"><span data-stu-id="fc995-124">hello following steps will walk you through hello steps toocreate an Azure Web App, configure hello required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="fc995-125">Обзор toohello [портал Azure] и войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="fc995-125">Browse toohello [Azure portal] and log in.</span></span>

1. <span data-ttu-id="fc995-126">После входа в вашу учетную запись на hello портал Azure, щелкните значок меню hello **службы приложений**:</span><span class="sxs-lookup"><span data-stu-id="fc995-126">Once you have logged into your account on hello Azure portal, click hello menu icon for **App Services**:</span></span>
   
   ![Портал Azure][AZ01]

1. <span data-ttu-id="fc995-128">Здравствуйте, когда **службы приложений** страница отображается, щелкните **+ добавить** toocreate нового приложения службы.</span><span class="sxs-lookup"><span data-stu-id="fc995-128">When hello **App Services** page is displayed, click **+ Add** toocreate a new App Service.</span></span>

   ![Создание службы приложений][AZ02]

1. <span data-ttu-id="fc995-130">При отображении hello список шаблонов веб-приложение, щелкните ссылку hello для hello основные веб-приложение Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fc995-130">When hello list of web app templates is displayed, click hello link for hello basic Microsoft Web App.</span></span>

   ![Шаблоны веб-приложений][AZ03]

1. <span data-ttu-id="fc995-132">Когда откроется страница приветствия сведения для шаблона веб-приложения hello, нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="fc995-132">When hello information page for hello Web App template is displayed, click **Create**.</span></span>

   ![Создание веб-приложения][AZ04]

1. <span data-ttu-id="fc995-134">Укажите уникальное имя веб-приложения и задайте дополнительные параметры, после чего нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="fc995-134">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![Параметры создания веб-приложения][AZ05]

1. <span data-ttu-id="fc995-136">После создания веб-приложения, щелкните значок меню hello **службы приложений**и выберите только что созданный веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="fc995-136">Once your web app has been created, click hello menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![Список веб-приложений][AZ06]

1. <span data-ttu-id="fc995-138">При отображении веб-приложения, укажите hello версии Java с помощью hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="fc995-138">When your web app is displayed, specify hello Java version by using hello following steps:</span></span>

   <span data-ttu-id="fc995-139">а.</span><span class="sxs-lookup"><span data-stu-id="fc995-139">a.</span></span> <span data-ttu-id="fc995-140">Нажмите кнопку hello **параметры приложения** элемента меню.</span><span class="sxs-lookup"><span data-stu-id="fc995-140">Click hello **Application Settings** menu item.</span></span>

   <span data-ttu-id="fc995-141">b.</span><span class="sxs-lookup"><span data-stu-id="fc995-141">b.</span></span> <span data-ttu-id="fc995-142">Выберите **Java 8** hello версии Java.</span><span class="sxs-lookup"><span data-stu-id="fc995-142">Choose **Java 8** for hello Java version.</span></span>

   <span data-ttu-id="fc995-143">c.</span><span class="sxs-lookup"><span data-stu-id="fc995-143">c.</span></span> <span data-ttu-id="fc995-144">Выберите **Newest** для hello дополнительный номер версии Java.</span><span class="sxs-lookup"><span data-stu-id="fc995-144">Choose **Newest** for hello minor Java version.</span></span>

   <span data-ttu-id="fc995-145">d.</span><span class="sxs-lookup"><span data-stu-id="fc995-145">d.</span></span> <span data-ttu-id="fc995-146">Выберите **новейшие 8.5 Tomcat** для hello web контейнера.</span><span class="sxs-lookup"><span data-stu-id="fc995-146">Choose **Newest Tomcat 8.5** for hello web container.</span></span> <span data-ttu-id="fc995-147">(Этот контейнер не фактически будет использоваться; Azure будет использовать контейнер hello Spring загрузки приложения.)</span><span class="sxs-lookup"><span data-stu-id="fc995-147">(This container will not actually be used; Azure will use hello container from your Spring Boot application.)</span></span>

   <span data-ttu-id="fc995-148">д.</span><span class="sxs-lookup"><span data-stu-id="fc995-148">e.</span></span> <span data-ttu-id="fc995-149">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fc995-149">Click **Save**.</span></span>

   ![Параметры приложения][AZ07]

1. <span data-ttu-id="fc995-151">Укажите учетные данные развертывания FTP, используя hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="fc995-151">Specify your FTP deployment credentials by using hello following steps:</span></span>

   <span data-ttu-id="fc995-152">а.</span><span class="sxs-lookup"><span data-stu-id="fc995-152">a.</span></span> <span data-ttu-id="fc995-153">Нажмите кнопку hello **учетные данные развертывания** элемента меню.</span><span class="sxs-lookup"><span data-stu-id="fc995-153">Click hello **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="fc995-154">b.</span><span class="sxs-lookup"><span data-stu-id="fc995-154">b.</span></span> <span data-ttu-id="fc995-155">Укажите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="fc995-155">Specify your username and password.</span></span>

   <span data-ttu-id="fc995-156">c.</span><span class="sxs-lookup"><span data-stu-id="fc995-156">c.</span></span> <span data-ttu-id="fc995-157">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fc995-157">Click **Save**.</span></span>

   ![Указание учетных данных развертывания][AZ08]

1. <span data-ttu-id="fc995-159">Получить сведения о подключении к FTP, с помощью hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="fc995-159">Retrieve your FTP connection information by using hello following steps:</span></span>

   <span data-ttu-id="fc995-160">а.</span><span class="sxs-lookup"><span data-stu-id="fc995-160">a.</span></span> <span data-ttu-id="fc995-161">Нажмите кнопку hello **учетные данные развертывания** элемента меню.</span><span class="sxs-lookup"><span data-stu-id="fc995-161">Click hello **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="fc995-162">b.</span><span class="sxs-lookup"><span data-stu-id="fc995-162">b.</span></span> <span data-ttu-id="fc995-163">Скопируйте полное имя пользователя FTP и URL-адрес и сохранить их для hello следующей части этого учебника.</span><span class="sxs-lookup"><span data-stu-id="fc995-163">Copy your full FTP username and URL and save them for hello next section of this tutorial.</span></span>

   ![URL-адрес и учетные данные FTP][AZ09]

## <a name="deploy-your-spring-boot-web-app-tooazure"></a><span data-ttu-id="fc995-165">Развертывание вашей tooAzure приложения web Spring загрузки</span><span class="sxs-lookup"><span data-stu-id="fc995-165">Deploy your Spring Boot web app tooAzure</span></span>

<span data-ttu-id="fc995-166">Hello, выполнив действия поможет toodeploy действия hello вашей tooAzure приложения web Spring загрузки.</span><span class="sxs-lookup"><span data-stu-id="fc995-166">hello following steps will walk you through hello steps toodeploy your Spring Boot web app tooAzure.</span></span>

1. <span data-ttu-id="fc995-167">Откройте текстовый редактор, например Блокнот и вставьте следующий текст в новый документ hello, а затем сохраните файл как файл hello *web.config*:</span><span class="sxs-lookup"><span data-stu-id="fc995-167">Open a text editor such as Windows Notepad and paste hello following text into a new document, then save hello file as *web.config*:</span></span>
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. <span data-ttu-id="fc995-168">После сохранения hello *web.config* файловая система tooyour, подключите tooyour веб-приложения по протоколу FTP, с помощью hello URL-адрес, имя пользователя и пароль из hello предшествующий разделе этого учебника.</span><span class="sxs-lookup"><span data-stu-id="fc995-168">After you have saved hello *web.config* file tooyour system, connect tooyour web app via FTP using hello URL, username, and password from hello preceding section of this tutorial.</span></span> <span data-ttu-id="fc995-169">Например:</span><span class="sxs-lookup"><span data-stu-id="fc995-169">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="fc995-170">Изменение hello удаленный каталог toohello корневую папку веб-приложения (который находится на */сайт/wwwroot*), затем скопируйте Spring загрузки приложения hello JAR-файл и hello *web.config* из более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="fc995-170">Change hello remote directory toohello root folder of your web app, (which is at */site/wwwroot*), then copy hello JAR file from your Spring Boot application and hello *web.config* from earlier.</span></span> <span data-ttu-id="fc995-171">Например:</span><span class="sxs-lookup"><span data-stu-id="fc995-171">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="fc995-172">После развертывания вашего JAR и *web.config* файлы tooyour веб-приложения, необходимо toorestart веб-приложения с помощью портала Azure hello:</span><span class="sxs-lookup"><span data-stu-id="fc995-172">After you have deployed your JAR and *web.config* files tooyour web app, you need toorestart your web app using hello Azure portal:</span></span>

   ![][AZ10]

1. <span data-ttu-id="fc995-173">Тестирование веб-приложения hello путем просмотра URL-адрес tooyour веб-приложения в веб-браузере, или с помощью синтаксиса hello как следующий пример, при наличии доступных перелистывание hello:</span><span class="sxs-lookup"><span data-stu-id="fc995-173">Test hello web app by browsing tooyour web app's URL using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="fc995-174">Должно появиться сообщение, отображаемое после hello: **Greetings с Spring загрузки!**</span><span class="sxs-lookup"><span data-stu-id="fc995-174">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Обзор образца приложения][SB02]

## <a name="next-steps"></a><span data-ttu-id="fc995-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fc995-176">Next steps</span></span>

<span data-ttu-id="fc995-177">Дополнительные сведения об использовании приложений Spring загрузки в Azure см. следующие статьи hello:</span><span class="sxs-lookup"><span data-stu-id="fc995-177">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="fc995-178">Развертывание приложения загрузки Spring в Linux в hello контейнера службы Azure</span><span class="sxs-lookup"><span data-stu-id="fc995-178">Deploy a Spring Boot Application on Linux in hello Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [<span data-ttu-id="fc995-179">Развертывание приложения загрузки Spring в кластере Kubernetes в hello контейнера службы Azure</span><span class="sxs-lookup"><span data-stu-id="fc995-179">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="fc995-180">Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure] и hello [Java средств для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="fc995-180">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="fc995-181">Дополнительные сведения о tooAzure приложения web depoying, с помощью протокола FTP см. в разделе [развертывание вашего приложения tooAzure службы приложений с помощью FTP/S].</span><span class="sxs-lookup"><span data-stu-id="fc995-181">For additional information about depoying web apps tooAzure using FTP, see [Deploy your app tooAzure App Service using FTP/S].</span></span>

<span data-ttu-id="fc995-182">Дополнительные сведения о проекте образец hello Spring загрузки см. [Spring начальной загрузки].</span><span class="sxs-lookup"><span data-stu-id="fc995-182">For further details about hello Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="fc995-183">Справку по Приступая к работе с приложениями Spring загрузки см. в разделе hello **Spring Initializr** на https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="fc995-183">For help with getting started with your own Spring Boot applications, see hello **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="fc995-184">Дополнительные сведения о настройке дополнительных параметров для веб-приложения см. в статье [Настройка веб-приложений в службе приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="fc995-184">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

<!-- URL List -->

[службе приложений Azure]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[центра разработчиков Java Azure]: https://azure.microsoft.com/develop/java/
[портал Azure]: https://portal.azure.com/
[Настройка веб-приложений в службе приложений Azure]: /azure/app-service-web/web-sites-configure
[развертывание вашего приложения tooAzure службы приложений с помощью FTP/S]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java средств для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[Maven]: http://maven.apache.org/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Загрузки spring]: http://projects.spring.io/spring-boot/
[Spring начальной загрузки]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB01.png
[SB02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB02.png

[AZ01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ01.png
[AZ02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ02.png
[AZ03]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ03.png
[AZ04]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ04.png
[AZ05]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ05.png
[AZ06]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ06.png
[AZ07]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ07.png
[AZ08]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ08.png
[AZ09]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ09.png
[AZ10]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ10.png
