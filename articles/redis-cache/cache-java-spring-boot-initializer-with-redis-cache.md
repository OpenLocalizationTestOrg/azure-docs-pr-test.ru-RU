---
title: "aaaHow tooconfigure toouse приложения инициализатора Spring загрузки кэша Redis"
description: "Узнайте, как tooconfigure приложение загрузки Spring созданными toouse Spring Initializr hello кэша Redis для Azure."
services: redis-cache
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
keywords: "spring, начальное приложение spring boot, кэш redis"
ms.assetid: 
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: java
ms.topic: article
ms.date: 7/21/2017
ms.author: robmcm;zhijzhao;yidon
ms.openlocfilehash: ad532c88d2d67b97079eeb0e0e392add29ac365b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-spring-boot-initializer-app-toouse-redis-cache"></a><span data-ttu-id="e1545-104">Как tooconfigure toouse приложения инициализатора Spring загрузки кэша Redis</span><span class="sxs-lookup"><span data-stu-id="e1545-104">How tooconfigure a Spring Boot Initializer app toouse Redis Cache</span></span>

## <a name="overview"></a><span data-ttu-id="e1545-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="e1545-105">Overview</span></span>

<span data-ttu-id="e1545-106">Hello  **[Spring Framework]**  — это решение с открытым исходным кодом, которое Java разработчики могут создавать приложения уровня предприятия.</span><span class="sxs-lookup"><span data-stu-id="e1545-106">hello **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="e1545-107">Один из проектов более популярных hello которых строится на основе этой платформы является [загрузки Spring], который предоставляет упрощенный подход для создания изолированного приложения Java.</span><span class="sxs-lookup"><span data-stu-id="e1545-107">One of hello more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="e1545-108">Разработчики toohelp начать работу с загрузкой Spring, несколько образцов Spring загрузки пакетов можно найти по адресу <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="e1545-108">toohelp developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="e1545-109">В дополнение к этому toochoosing списке hello базового загрузочного Spring проекты, hello  **[Spring Initializr]**  помогает разработчикам Приступая к работе с созданием пользовательских приложений Spring загрузки.</span><span class="sxs-lookup"><span data-stu-id="e1545-109">In addition toochoosing from hello list of basic Spring Boot projects, hello **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="e1545-110">В этой статье описывается создание кэша Redis с использованием портала Azure, затем с помощью hello hello **Spring Initializr** toocreate пользовательское приложение, а затем создав Java веб-приложения, который сохраняет и извлекает данные с помощью вашей Кэш redis.</span><span class="sxs-lookup"><span data-stu-id="e1545-110">This article walks you through creating a Redis cache using hello Azure portal, then using hello **Spring Initializr** toocreate a custom application, and then creating a Java web application which stores and retrieves data using your Redis cache.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1545-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e1545-111">Prerequisites</span></span>

<span data-ttu-id="e1545-112">в порядке toofollow hello действия, описанные в этой статье требуются следующие необходимые условия Hello:</span><span class="sxs-lookup"><span data-stu-id="e1545-112">hello following prerequisites are required in order toofollow hello steps in this article:</span></span>

* <span data-ttu-id="e1545-113">Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="e1545-113">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="e1545-114">[Пакет разработчиков Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="e1545-114">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="e1545-115">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="e1545-115">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="e1545-116">Создание кэша Redis в Azure</span><span class="sxs-lookup"><span data-stu-id="e1545-116">Create a Redis cache on Azure</span></span>

1. <span data-ttu-id="e1545-117">Обзор toohello Azure портала в <https://portal.azure.com/> и выберите пункт hello для **+ создать**.</span><span class="sxs-lookup"><span data-stu-id="e1545-117">Browse toohello Azure portal at <https://portal.azure.com/> and click hello item for **+New**.</span></span>

   ![Портал Azure][AZ01]

1. <span data-ttu-id="e1545-119">Выберите **База данных**, а затем — **Кэш Redis**.</span><span class="sxs-lookup"><span data-stu-id="e1545-119">Click **Database**, and then click **Redis Cache**.</span></span>

   ![Портал Azure][AZ02]

1. <span data-ttu-id="e1545-121">На hello **новый кэш Redis** введите hello **DNS-имя** кэша, затем укажите ваш **подписки**, **группы ресурсов**,  **Расположение**, и **Ценовая категория**.</span><span class="sxs-lookup"><span data-stu-id="e1545-121">On hello **New Redis Cache** page, enter hello **DNS name** for your cache, then specify your **Subscription**, **Resource group**, **Location**, and **Pricing tier**.</span></span> <span data-ttu-id="e1545-122">При указании этих параметров щелкните **создать** toocreate кэша.</span><span class="sxs-lookup"><span data-stu-id="e1545-122">When you have specified these options, click **Create** toocreate your cache.</span></span>

   ![Портал Azure][AZ03]

1. <span data-ttu-id="e1545-124">После завершения вашего кэша, вы увидите его в списке на Azure **мониторинга**, а также в разделе hello **все ресурсы**, и **Redis кэши** страниц.</span><span class="sxs-lookup"><span data-stu-id="e1545-124">Once your cache has been completed, you will see it listed on your Azure **Dashboard**, as well as under hello **All Resources**, and **Redis Caches** pages.</span></span> <span data-ttu-id="e1545-125">Можно щелкнуть кэша на любом из этих расположений tooopen hello страница «свойства» для кэша.</span><span class="sxs-lookup"><span data-stu-id="e1545-125">You can click on your cache on any of those locations tooopen hello properties page for your cache.</span></span>

   ![Портал Azure][AZ04]

1. <span data-ttu-id="e1545-127">Когда откроется страница приветствия, содержащая список свойств для кэша hello, нажмите кнопку **ключи доступа** и скопируйте ключи доступа для кэша.</span><span class="sxs-lookup"><span data-stu-id="e1545-127">When hello page which contains hello list of properties for your cache is displayed, click **Access keys** and copy your access keys for your cache.</span></span>

   ![Портал Azure][AZ05]

## <a name="create-a-custom-application-using-hello-spring-initializr"></a><span data-ttu-id="e1545-129">Создать пользовательское приложение с помощью hello Initializr пружины</span><span class="sxs-lookup"><span data-stu-id="e1545-129">Create a custom application using hello Spring Initializr</span></span>

1. <span data-ttu-id="e1545-130">Обзор слишком<https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="e1545-130">Browse too<https://start.spring.io/>.</span></span>

1. <span data-ttu-id="e1545-131">Укажите, требуется toogenerate **Maven** проекта с **Java**, введите hello **группы** и **Aritifact** имена для вашего приложения и щелкните ссылку hello слишком**коммутатор toohello полную версию** из Spring Initializr hello.</span><span class="sxs-lookup"><span data-stu-id="e1545-131">Specify that you want toogenerate a **Maven** project with **Java**, enter hello **Group** and **Aritifact** names for your application, and then click hello link too**Switch toohello full version** of hello Spring Initializr.</span></span>

   ![Основные параметры Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="e1545-133">Hello Spring Initializr будет использовать hello **группы** и **Aritifact** имя пакета hello toocreate имена, например: *com.contoso.myazuredemo*.</span><span class="sxs-lookup"><span data-stu-id="e1545-133">hello Spring Initializr will use hello **Group** and **Aritifact** names toocreate hello package name; for example: *com.contoso.myazuredemo*.</span></span>
   >

1. <span data-ttu-id="e1545-134">Прокрутите вниз toohello **Web** статьи и установите флажок "hello" для **Web**, и прокрутите вниз toohello **NoSQL** статьи и установите флажок "hello" для **Redis**, прокрутите toohello внизу страницы приветствия и нажмите кнопку "hello", слишком**создания проекта**.</span><span class="sxs-lookup"><span data-stu-id="e1545-134">Scroll down toohello **Web** section and check hello box for **Web**, then scroll down toohello **NoSQL** section and check hello box for **Redis**, then scroll toohello bottom of hello page and click hello button too**Generate Project**.</span></span>

   ![Все параметры Spring Initializr][SI02]

1. <span data-ttu-id="e1545-136">При появлении соответствующего запроса загрузите hello путь tooa проекта на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="e1545-136">When prompted, download hello project tooa path on your local computer.</span></span>

   ![Скачивание пользовательского проекта Spring Boot][SI03]

1. <span data-ttu-id="e1545-138">После извлечения файлов hello в локальной системе вашего приложения Spring загрузки будет готова для редактирования.</span><span class="sxs-lookup"><span data-stu-id="e1545-138">After you have extracted hello files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![Пользовательские файлы проекта Spring Boot][SI04]

## <a name="configure-your-custom-spring-boot-toouse-your-redis-cache"></a><span data-ttu-id="e1545-140">Настройка вашего пользовательского toouse Spring загрузки кэша Redis</span><span class="sxs-lookup"><span data-stu-id="e1545-140">Configure your custom Spring Boot toouse your Redis Cache</span></span>

1. <span data-ttu-id="e1545-141">Найдите hello *application.properties* файла в hello *ресурсов* каталог приложения, или создать файл hello в том случае, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="e1545-141">Locate hello *application.properties* file in hello *resources* directory of your app, or create hello file if it does not already exist.</span></span>

   ![Найдите файл application.properties hello][RE01]

1. <span data-ttu-id="e1545-143">Откройте hello *application.properties* в текстовом редакторе и добавьте следующие строки toohello файл hello и замените значения образец hello hello соответствующие свойства из кэша:</span><span class="sxs-lookup"><span data-stu-id="e1545-143">Open hello *application.properties* file in a text editor, and add hello following lines toohello file, and replace hello sample values with hello appropriate properties from your cache:</span></span>

   ```yaml
   # Specify hello DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify hello port for your Redis cache.
   spring.redis.port=6380

   # Specify hello access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Изменение файла application.properties hello][RE02]

1. <span data-ttu-id="e1545-145">Сохраните и закройте hello *application.properties* файла.</span><span class="sxs-lookup"><span data-stu-id="e1545-145">Save and close hello *application.properties* file.</span></span>

1. <span data-ttu-id="e1545-146">Создайте папку с именем *контроллера* под hello исходную папку для пакета; например:</span><span class="sxs-lookup"><span data-stu-id="e1545-146">Create a folder named *controller* under hello source folder for your package; for example:</span></span>

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   <span data-ttu-id="e1545-147">-или-</span><span class="sxs-lookup"><span data-stu-id="e1545-147">-or-</span></span>

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. <span data-ttu-id="e1545-148">Создайте новый файл с именем *HelloController.java* в hello *контроллера* папки.</span><span class="sxs-lookup"><span data-stu-id="e1545-148">Create a new file named *HelloController.java* in hello *controller* folder.</span></span> <span data-ttu-id="e1545-149">Откройте файл hello в текстовом редакторе и добавьте следующий код tooit hello:</span><span class="sxs-lookup"><span data-stu-id="e1545-149">Open hello file in a text editor and add hello following code tooit:</span></span>

   ```java
   package com.contoso.myazuredemo;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Value;
   import redis.clients.jedis.Jedis;
   import redis.clients.jedis.JedisShardInfo;

   @RestController
   public class HelloController {
   
      // Retrieve hello DNS name for your cache.
      @Value("${spring.redis.host}")
      private String redisHost;

      // Retrieve hello port for your cache.
      @Value("${spring.redis.port}")
      private int redisPort;

      // Retrieve hello access key for your cache.
      @Value("${spring.redis.password}")
      private String redisPassword;

      @RequestMapping("/")
      // Define hello Hello World controller.
      public String hello() {
      
         // Create a JedisShardInfo object tooconnect tooyour Redis cache.
         JedisShardInfo jedisShardInfo = new JedisShardInfo(redisHost, redisPort, true);
         // Specify your access key.
         jedisShardInfo.setPassword(redisPassword);
         // Create a Jedis object toostore/retrieve information from your cache.
         Jedis jedis = new Jedis(jedisShardInfo);

         // Add a Hello World string tooyour cache.
         jedis.set("greeting", "Hello World!");

         // Return hello string from your cache.
         return jedis.get("greeting");
      }
   }
   ```
   
   <span data-ttu-id="e1545-150">Когда будет необходимо tooreplace `com.contoso.myazuredemo` с именем hello пакета для проекта.</span><span class="sxs-lookup"><span data-stu-id="e1545-150">Where you will need tooreplace `com.contoso.myazuredemo` with hello package name for your project.</span></span>

1. <span data-ttu-id="e1545-151">Сохраните и закройте hello *HelloController.java* файла.</span><span class="sxs-lookup"><span data-stu-id="e1545-151">Save and close hello *HelloController.java* file.</span></span>

1. <span data-ttu-id="e1545-152">Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e1545-152">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="e1545-153">Тестирование веб-приложения hello, перейдя в веб-браузере toohttp://localhost:8080, или с помощью синтаксиса hello как следующий пример, при наличии доступных перелистывание hello:</span><span class="sxs-lookup"><span data-stu-id="e1545-153">Test hello web app by browsing toohttp://localhost:8080 using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="e1545-154">Вы увидите hello «Hello World!»</span><span class="sxs-lookup"><span data-stu-id="e1545-154">You should see hello "Hello World!"</span></span> <span data-ttu-id="e1545-155">которое динамически извлекается из кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="e1545-155">message from your sample controller displayed, which is being retrieved dynamically from your Redis cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1545-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e1545-156">Next steps</span></span>

<span data-ttu-id="e1545-157">Дополнительные сведения об использовании приложений Spring загрузки в Azure см. следующие статьи hello:</span><span class="sxs-lookup"><span data-stu-id="e1545-157">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="e1545-158">Развертывание приложения загрузки Spring toohello службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="e1545-158">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="e1545-159">Запуск приложения загрузки Spring в кластере Kubernetes в hello контейнера службы Azure</span><span class="sxs-lookup"><span data-stu-id="e1545-159">Running a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="e1545-160">Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure] и hello [Java средств для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="e1545-160">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="e1545-161">Дополнительные сведения о начале работы с использованием кэша Redis с Java в Azure, см. в разделе [способом toouse Redis для Azure для кэширования с помощью Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="e1545-161">For more information about getting started using Redis Cache with Java on Azure, see [How toouse Azure Redis Cache with Java][Redis Cache with Java].</span></span>

<!-- URL List -->

[центра разработчиков Java Azure]: https://azure.microsoft.com/develop/java/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Java средств для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[загрузки Spring]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Redis Cache with Java]: cache-java-get-started.md

<!-- IMG List -->

[AZ01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ01.png
[AZ02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ02.png
[AZ03]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ03.png
[AZ04]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ04.png
[AZ05]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ05.png

[SI01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI01.png
[SI02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI02.png
[SI03]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI03.png
[SI04]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI04.png

[RE01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/RE01.png
[RE02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/RE02.png
