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
# <a name="how-tooconfigure-a-spring-boot-initializer-app-toouse-redis-cache"></a>Как tooconfigure toouse приложения инициализатора Spring загрузки кэша Redis

## <a name="overview"></a>Обзор

Hello  **[Spring Framework]**  — это решение с открытым исходным кодом, которое Java разработчики могут создавать приложения уровня предприятия. Один из проектов более популярных hello которых строится на основе этой платформы является [загрузки Spring], который предоставляет упрощенный подход для создания изолированного приложения Java. Разработчики toohelp начать работу с загрузкой Spring, несколько образцов Spring загрузки пакетов можно найти по адресу <https://github.com/spring-guides/>. В дополнение к этому toochoosing списке hello базового загрузочного Spring проекты, hello  **[Spring Initializr]**  помогает разработчикам Приступая к работе с созданием пользовательских приложений Spring загрузки.

В этой статье описывается создание кэша Redis с использованием портала Azure, затем с помощью hello hello **Spring Initializr** toocreate пользовательское приложение, а затем создав Java веб-приложения, который сохраняет и извлекает данные с помощью вашей Кэш redis.

## <a name="prerequisites"></a>Предварительные требования

в порядке toofollow hello действия, описанные в этой статье требуются следующие необходимые условия Hello:

* Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].

* [Пакет разработчиков Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) версии 1.7 или более поздней.

* [Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.

## <a name="create-a-redis-cache-on-azure"></a>Создание кэша Redis в Azure

1. Обзор toohello Azure портала в <https://portal.azure.com/> и выберите пункт hello для **+ создать**.

   ![Портал Azure][AZ01]

1. Выберите **База данных**, а затем — **Кэш Redis**.

   ![Портал Azure][AZ02]

1. На hello **новый кэш Redis** введите hello **DNS-имя** кэша, затем укажите ваш **подписки**, **группы ресурсов**,  **Расположение**, и **Ценовая категория**. При указании этих параметров щелкните **создать** toocreate кэша.

   ![Портал Azure][AZ03]

1. После завершения вашего кэша, вы увидите его в списке на Azure **мониторинга**, а также в разделе hello **все ресурсы**, и **Redis кэши** страниц. Можно щелкнуть кэша на любом из этих расположений tooopen hello страница «свойства» для кэша.

   ![Портал Azure][AZ04]

1. Когда откроется страница приветствия, содержащая список свойств для кэша hello, нажмите кнопку **ключи доступа** и скопируйте ключи доступа для кэша.

   ![Портал Azure][AZ05]

## <a name="create-a-custom-application-using-hello-spring-initializr"></a>Создать пользовательское приложение с помощью hello Initializr пружины

1. Обзор слишком<https://start.spring.io/>.

1. Укажите, требуется toogenerate **Maven** проекта с **Java**, введите hello **группы** и **Aritifact** имена для вашего приложения и щелкните ссылку hello слишком**коммутатор toohello полную версию** из Spring Initializr hello.

   ![Основные параметры Spring Initializr][SI01]

   > [!NOTE]
   >
   > Hello Spring Initializr будет использовать hello **группы** и **Aritifact** имя пакета hello toocreate имена, например: *com.contoso.myazuredemo*.
   >

1. Прокрутите вниз toohello **Web** статьи и установите флажок "hello" для **Web**, и прокрутите вниз toohello **NoSQL** статьи и установите флажок "hello" для **Redis**, прокрутите toohello внизу страницы приветствия и нажмите кнопку "hello", слишком**создания проекта**.

   ![Все параметры Spring Initializr][SI02]

1. При появлении соответствующего запроса загрузите hello путь tooa проекта на локальном компьютере.

   ![Скачивание пользовательского проекта Spring Boot][SI03]

1. После извлечения файлов hello в локальной системе вашего приложения Spring загрузки будет готова для редактирования.

   ![Пользовательские файлы проекта Spring Boot][SI04]

## <a name="configure-your-custom-spring-boot-toouse-your-redis-cache"></a>Настройка вашего пользовательского toouse Spring загрузки кэша Redis

1. Найдите hello *application.properties* файла в hello *ресурсов* каталог приложения, или создать файл hello в том случае, если он еще не существует.

   ![Найдите файл application.properties hello][RE01]

1. Откройте hello *application.properties* в текстовом редакторе и добавьте следующие строки toohello файл hello и замените значения образец hello hello соответствующие свойства из кэша:

   ```yaml
   # Specify hello DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify hello port for your Redis cache.
   spring.redis.port=6380

   # Specify hello access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Изменение файла application.properties hello][RE02]

1. Сохраните и закройте hello *application.properties* файла.

1. Создайте папку с именем *контроллера* под hello исходную папку для пакета; например:

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   -или-

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. Создайте новый файл с именем *HelloController.java* в hello *контроллера* папки. Откройте файл hello в текстовом редакторе и добавьте следующий код tooit hello:

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
   
   Когда будет необходимо tooreplace `com.contoso.myazuredemo` с именем hello пакета для проекта.

1. Сохраните и закройте hello *HelloController.java* файла.

1. Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Тестирование веб-приложения hello, перейдя в веб-браузере toohttp://localhost:8080, или с помощью синтаксиса hello как следующий пример, при наличии доступных перелистывание hello:

   ```shell
   curl http://localhost:8080
   ```

   Вы увидите hello «Hello World!» которое динамически извлекается из кэша Redis.

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения об использовании приложений Spring загрузки в Azure см. следующие статьи hello:

* [Развертывание приложения загрузки Spring toohello службе приложений Azure](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Запуск приложения загрузки Spring в кластере Kubernetes в hello контейнера службы Azure](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure] и hello [Java средств для Visual Studio Team Services].

Дополнительные сведения о начале работы с использованием кэша Redis с Java в Azure, см. в разделе [способом toouse Redis для Azure для кэширования с помощью Java][Redis Cache with Java].

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
