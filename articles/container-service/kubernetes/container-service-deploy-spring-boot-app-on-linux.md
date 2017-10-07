---
title: "aaaDeploy Spring загрузки веб-приложения на платформе Linux в службе контейнера Azure | Документы Microsoft"
description: "В этом учебнике рассматриваются хотя toodeploy действия hello Spring загрузки приложения как веб-приложения Linux в Microsoft Azure."
services: container-service
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 2c44be1c7f66a38f48239001f0be9e90c7e6edef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-hello-azure-container-service"></a>Развертывание приложения загрузки Spring в Linux в hello контейнера службы Azure

Hello  **[Spring Framework]**  — это решение открытым исходным кодом, разработчики Java могут создавать корпоративные приложения. Один из проектов более популярных hello, построенных на основе этой платформы является [загрузки Spring], который предоставляет упрощенный подход для создания изолированного приложения Java.

**[Docker]**  является открытым исходным кодом решения, которые помогают разработчикам автоматизировать развертывание hello, масштабирование и управление их приложений, выполняющихся в контейнерах.

Этот учебник поможет выполнить с помощью Docker toodevelop и развернуть узел Linux tooa Spring загрузки приложения в hello [контейнера службы Azure (ACS)].

## <a name="prerequisites"></a>Предварительные требования

В порядке toocomplete hello шагов в этом учебнике требуется hello toohave следующие предварительные требования:

* Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].
* Hello [Azure интерфейс командной строки (CLI)].
* Актуальная версия [Java Developer Kit (JDK)].
* Средство сборки [Maven] (версия 3) от Apache.
* Клиент [Git].
* Клиент [Docker].

> [!NOTE]
>
> Из-за требований к виртуализации toohello этого учебника не может следовать за hello действия, описанные в этой статье на виртуальной машине; необходимо использовать физический компьютер с включенными возможностями виртуализации.
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a>Создать hello Spring загрузки на веб-приложение Docker начало работы

Hello следующие шаги описывают hello шаги, необходимые toocreate простого Spring загрузки веб-приложения и протестировать на локальном компьютере.

1. Откройте командную строку и создать toohold локальный каталог, приложение и перейдите в каталог toothat; Например:
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- или --
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Клон hello [загрузки Spring по началу работы Docker] образец проекта в каталог hello, вы создали; например:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Изменение каталога toohello завершения проекта; Например:
   ```
   cd gs-spring-boot-docker/complete
   ```

1. Построение hello JAR-файл с помощью Maven; Например:
   ```
   mvn package
   ```

1. После создания веб-приложения hello изменить каталог toohello `target` каталог, где расположен hello JAR-файл и запустить веб-приложение hello; например:
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. Тестирование веб-приложения hello путем просмотра tooit локально с помощью веб-браузера. Например при наличии перелистывание доступен и настроен toorun сервера Tomcat hello на порт 80:
   ```
   curl http://localhost
   ```

1. Должно появиться сообщение, отображаемое после hello: **Docker Здравствуй, мир!**

   ![Локальный просмотр образца приложения][SB01]

## <a name="create-an-azure-container-registry-toouse-as-a-private-docker-registry"></a>Создайте toouse реестра контейнера Azure в качестве частного реестра Docker

Hello следующие шаги описывают с помощью hello Azure портала toocreate реестра контейнера Azure.

> [!NOTE]
>
> Toouse hello Azure CLI вместо hello портал Azure, выполните шаги hello в [создать закрытый реестре контейнеров Docker с помощью Azure CLI 2.0 hello](../../container-registry/container-registry-get-started-azure-cli.md).
>

1. Обзор toohello [портал Azure] и выполните вход.

   После входа в учетную запись tooyour на портал Azure hello, выполните действия hello в hello [создать закрытый реестре контейнеров Docker с помощью портала Azure hello] статьи, которая paraphrased в следующие шаги для hello hello исследования целесообразности.

1. Щелкните значок меню hello для **+ создать**, нажмите кнопку **контейнеры**, а затем нажмите кнопку **реестра контейнера Azure**.
   
   ![Создание нового реестра контейнеров Azure][AR01]

1. Если отображается страница hello сведения для hello Azure реестра контейнера шаблона, щелкните **создать**. 

   ![Создание нового реестра контейнеров Azure][AR02]

1. Здравствуйте, когда **создать контейнер реестра** отобразить страницу, введите ваш **имя реестра** и **группы ресурсов**, выберите **включить** для Hello **пользователю с правами администратора**, а затем нажмите кнопку **создать**.

   ![Настройка параметров реестра контейнеров Azure][AR03]

1. После создания контейнера реестра перейдите реестр контейнера tooyour hello портал Azure и нажмите кнопку **клавиши доступа**. Запишите hello имя пользователя и пароль для hello дальнейшие действия.

   ![Ключи доступа к реестру контейнеров Azure][AR04]

## <a name="configure-maven-toouse-your-azure-container-registry-access-keys"></a>Настройка доступа к разделам реестра контейнера Azure Maven toouse

1. Откройте hello и toohello каталог конфигурации для установки Maven *settings.xml* файл в текстовом редакторе.

1. Добавить параметры доступа реестра контейнера Azure hello в предыдущем разделе этого учебника toohello `<servers>` коллекции в hello *settings.xml* файла; например:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Перейдите в каталог проекта toohello завершена для приложения Spring загрузки (например: «*C:\SpringBoot\gs-spring-boot-docker\complete*«или»*/users/robert/SpringBoot/gs-spring-boot-docker / Полный*») и откройте hello *pom.xml* файл в текстовом редакторе.

1. Обновление hello `<properties>` коллекции в hello *pom.xml* файл со значение сервера hello входа для реестра контейнера Azure hello в предыдущем разделе этого учебника; например:

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Обновление hello `<plugins>` коллекции в hello *pom.xml* файл, который hello `<plugin>` содержит hello server адрес и реестра имя входа для реестра контейнера Azure hello в предыдущем разделе этого учебника. Например:

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. Перейдите в каталог проекта toohello завершения загрузки Spring приложения и запустите следующие команды toorebuild hello приложения hello push tooyour контейнера hello Azure контейнер реестра:

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> При отправке вашего tooAzure контейнера Docker, может появиться сообщение об ошибке, аналогичные tooone Привет приведенному ниже, несмотря на то, что успешно создан контейнер Docker:
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> В этом случае может потребоваться toosign в tooyour учетная запись Azure из командной строки Docker hello; Например:
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> После этого можно передать контейнер с hello командной строки; Например:
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a>Создание веб-приложения в Linux в службе приложений Azure с помощью образа контейнера

1. Обзор toohello [портал Azure] и выполните вход.

1. Щелкните значок меню hello **+ создать**, нажмите кнопку **Интернет + мобильные устройства**, а затем нажмите кнопку **веб-приложения на платформе Linux**.
   
   ![Создайте новое веб-приложение в hello портал Azure][LX01]

1. Здравствуйте, когда **веб-приложения на платформе Linux** отобразить страницу, введите hello следующую информацию:

   а. Введите уникальное имя для hello **имя приложения**, например: «*wingtiptoyslinux*.»

   b. Выберите ваш **подписки** из раскрывающегося списка hello.

   c. Выберите существующую **группы ресурсов**, или укажите имя toocreate новую группу ресурсов.

   d. Нажмите кнопку **Настройка контейнера** и введите hello следующую информацию:

      * Выберите **Частный реестр**.

      * **Образ и дополнительный тег**: задайте имя контейнера из более ранней версии, например "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"

      * **URL-адрес сервера**: укажите URL-адрес реестра из более ранней версии, например "*https://wingtiptoysregistry.azurecr.io*"

      * **Имя входа пользователя** и **Пароль**: укажите учетные данные для входа из своих **ключей доступа**, которые использовались на предыдущих шагах.
   
   д. После ввода hello выше сведений щелкните **ОК**.

   ![Настройка параметров веб-приложения][LX02]

1. Щелкните **Создать**.

> [!NOTE]
>
> Azure автоматически сопоставит сервера Tomcat tooembedded запросы Интернета, на котором выполняется на hello стандартные порты 80 или 8080. Однако если вы настроили ваш внедренные toorun сервера Tomcat на другой номер порта, необходимо tooadd веб-приложение tooyour переменной среды, определяющего hello порт для внедренного сервера Tomcat. Таким образом, toodo используйте hello следующие шаги:
>
> 1. Обзор toohello [портал Azure] и выполните вход.
> 
> 2. Щелкните значок hello **службы приложений**. (См. элемент #1 в приведенном ниже рисунке hello).
>
> 3. Выберите веб-приложение из списка hello. (Элемент #2 в приведенном ниже рисунке hello).
>
> 4. Щелкните **Параметры приложения**. (Элемент #3 в приведенном ниже рисунке hello).
>
> 5. В hello **параметры приложения** добавьте новую переменную среды с именем **ПОРТ** и введите номер другой номер порта для hello значения. (Элемент #4 в приведенном ниже рисунке hello).
>
> 6. Щелкните **Сохранить**. (Элемент #5 в приведенном ниже рисунке hello).
>
> ![Сохранение пользовательский номер порта в hello портал Azure][LX03]
>

<!--
##  OPTIONAL: Configure hello embedded Tomcat server toorun on a different port

hello embedded Tomcat server in hello sample Spring Boot application is configured toorun on port 8080 by default. However, if you want toorun hello embedded Tomcat server toorun on a different port, such as port 80 for local testing, you can configure hello port by using hello following steps.

1. Go toohello *resources* directory (or create hello directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open hello *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify hello **server** setting so that hello server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close hello *application.yml* file.
-->

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения об использовании приложений Spring загрузки в Azure см. следующие статьи hello:

* [Развертывание приложения загрузки Spring toohello службе приложений Azure](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [Развертывание приложения загрузки Spring в кластере Kubernetes в hello контейнера службы Azure](container-service-deploy-spring-boot-app-on-kubernetes.md)

Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure] и hello [Java средств для Visual Studio Team Services].

Дополнительные сведения о hello Spring загрузки на Docker образец проекта в разделе [загрузки Spring по началу работы Docker].

Справку по Приступая к работе с приложениями Spring загрузки см. в разделе hello **Spring Initializr** на https://start.spring.io/.

Дополнительные сведения о начале работы с создания простого приложения загрузки Spring hello Spring Initializr на https://start.spring.io/ см.

Дополнительные примеры по как toouse Docker пользовательских образов с помощью Azure в разделе [с помощью пользовательского образа Docker для веб-приложения Azure в Linux].

<!-- URL List -->

[Azure интерфейс командной строки (CLI)]: /cli/azure/overview
[контейнера службы Azure (ACS)]: https://azure.microsoft.com/services/container-service/
[центра разработчиков Java Azure]: https://azure.microsoft.com/develop/java/
[портал Azure]: https://portal.azure.com/
[создать закрытый реестре контейнеров Docker с помощью портала Azure hello]: /azure/container-registry/container-registry-get-started-portal
[с помощью пользовательского образа Docker для веб-приложения Azure в Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java средств для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[Maven]: http://maven.apache.org/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[загрузки Spring]: http://projects.spring.io/spring-boot/
[загрузки Spring по началу работы Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-linux/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-linux/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-linux/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-linux/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-linux/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-linux/AR04.png

[LX01]: ./media/container-service-deploy-spring-boot-app-on-linux/LX01.png
[LX02]: ./media/container-service-deploy-spring-boot-app-on-linux/LX02.png
[LX03]: ./media/container-service-deploy-spring-boot-app-on-linux/LX03.png
