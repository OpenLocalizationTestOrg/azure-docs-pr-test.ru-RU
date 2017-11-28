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
# <a name="deploy-a-spring-boot-application-on-linux-in-hello-azure-container-service"></a><span data-ttu-id="d344f-103">Развертывание приложения загрузки Spring в Linux в hello контейнера службы Azure</span><span class="sxs-lookup"><span data-stu-id="d344f-103">Deploy a Spring Boot application on Linux in hello Azure Container Service</span></span>

<span data-ttu-id="d344f-104">Hello  **[Spring Framework]**  — это решение открытым исходным кодом, разработчики Java могут создавать корпоративные приложения.</span><span class="sxs-lookup"><span data-stu-id="d344f-104">hello **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="d344f-105">Один из проектов более популярных hello, построенных на основе этой платформы является [загрузки Spring], который предоставляет упрощенный подход для создания изолированного приложения Java.</span><span class="sxs-lookup"><span data-stu-id="d344f-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="d344f-106">**[Docker]**  является открытым исходным кодом решения, которые помогают разработчикам автоматизировать развертывание hello, масштабирование и управление их приложений, выполняющихся в контейнерах.</span><span class="sxs-lookup"><span data-stu-id="d344f-106">**[Docker]** is open-source solutions that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="d344f-107">Этот учебник поможет выполнить с помощью Docker toodevelop и развернуть узел Linux tooa Spring загрузки приложения в hello [контейнера службы Azure (ACS)].</span><span class="sxs-lookup"><span data-stu-id="d344f-107">This tutorial walks you through using Docker toodevelop and deploy a Spring Boot application tooa Linux host in hello [Azure Container Service (ACS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d344f-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d344f-108">Prerequisites</span></span>

<span data-ttu-id="d344f-109">В порядке toocomplete hello шагов в этом учебнике требуется hello toohave следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="d344f-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="d344f-110">Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="d344f-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="d344f-111">Hello [Azure интерфейс командной строки (CLI)].</span><span class="sxs-lookup"><span data-stu-id="d344f-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="d344f-112">Актуальная версия [Java Developer Kit (JDK)].</span><span class="sxs-lookup"><span data-stu-id="d344f-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="d344f-113">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="d344f-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="d344f-114">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="d344f-114">A [Git] client.</span></span>
* <span data-ttu-id="d344f-115">Клиент [Docker].</span><span class="sxs-lookup"><span data-stu-id="d344f-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="d344f-116">Из-за требований к виртуализации toohello этого учебника не может следовать за hello действия, описанные в этой статье на виртуальной машине; необходимо использовать физический компьютер с включенными возможностями виртуализации.</span><span class="sxs-lookup"><span data-stu-id="d344f-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="d344f-117">Создать hello Spring загрузки на веб-приложение Docker начало работы</span><span class="sxs-lookup"><span data-stu-id="d344f-117">Create hello Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="d344f-118">Hello следующие шаги описывают hello шаги, необходимые toocreate простого Spring загрузки веб-приложения и протестировать на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="d344f-118">hello following steps walk you through hello steps that are required toocreate a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="d344f-119">Откройте командную строку и создать toohold локальный каталог, приложение и перейдите в каталог toothat; Например:</span><span class="sxs-lookup"><span data-stu-id="d344f-119">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="d344f-120">-- или --</span><span class="sxs-lookup"><span data-stu-id="d344f-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="d344f-121">Клон hello [загрузки Spring по началу работы Docker] образец проекта в каталог hello, вы создали; например:</span><span class="sxs-lookup"><span data-stu-id="d344f-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="d344f-122">Изменение каталога toohello завершения проекта; Например:</span><span class="sxs-lookup"><span data-stu-id="d344f-122">Change directory toohello completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="d344f-123">Построение hello JAR-файл с помощью Maven; Например:</span><span class="sxs-lookup"><span data-stu-id="d344f-123">Build hello JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="d344f-124">После создания веб-приложения hello изменить каталог toohello `target` каталог, где расположен hello JAR-файл и запустить веб-приложение hello; например:</span><span class="sxs-lookup"><span data-stu-id="d344f-124">Once hello web app has been created, change directory toohello `target` directory where hello JAR file is located and start hello web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="d344f-125">Тестирование веб-приложения hello путем просмотра tooit локально с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="d344f-125">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="d344f-126">Например при наличии перелистывание доступен и настроен toorun сервера Tomcat hello на порт 80:</span><span class="sxs-lookup"><span data-stu-id="d344f-126">For example, if you have curl available and you configured hello Tomcat server toorun on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="d344f-127">Должно появиться сообщение, отображаемое после hello: **Docker Здравствуй, мир!**</span><span class="sxs-lookup"><span data-stu-id="d344f-127">You should see hello following message displayed: **Hello Docker World!**</span></span>

   ![Локальный просмотр образца приложения][SB01]

## <a name="create-an-azure-container-registry-toouse-as-a-private-docker-registry"></a><span data-ttu-id="d344f-129">Создайте toouse реестра контейнера Azure в качестве частного реестра Docker</span><span class="sxs-lookup"><span data-stu-id="d344f-129">Create an Azure Container Registry toouse as a Private Docker Registry</span></span>

<span data-ttu-id="d344f-130">Hello следующие шаги описывают с помощью hello Azure портала toocreate реестра контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="d344f-130">hello following steps walk you through using hello Azure portal toocreate an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="d344f-131">Toouse hello Azure CLI вместо hello портал Azure, выполните шаги hello в [создать закрытый реестре контейнеров Docker с помощью Azure CLI 2.0 hello](../../container-registry/container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d344f-131">If you want toouse hello Azure CLI instead of hello Azure portal, follow hello steps in [Create a private Docker container registry using hello Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span></span>
>

1. <span data-ttu-id="d344f-132">Обзор toohello [портал Azure] и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="d344f-132">Browse toohello [Azure portal] and sign in.</span></span>

   <span data-ttu-id="d344f-133">После входа в учетную запись tooyour на портал Azure hello, выполните действия hello в hello [создать закрытый реестре контейнеров Docker с помощью портала Azure hello] статьи, которая paraphrased в следующие шаги для hello hello исследования целесообразности.</span><span class="sxs-lookup"><span data-stu-id="d344f-133">Once you have signed in tooyour account on hello Azure portal, you can follow hello steps in hello [Create a private Docker container registry using hello Azure portal] article, which are paraphrased in hello following steps for hello sake of expediency.</span></span>

1. <span data-ttu-id="d344f-134">Щелкните значок меню hello для **+ создать**, нажмите кнопку **контейнеры**, а затем нажмите кнопку **реестра контейнера Azure**.</span><span class="sxs-lookup"><span data-stu-id="d344f-134">Click hello menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Создание нового реестра контейнеров Azure][AR01]

1. <span data-ttu-id="d344f-136">Если отображается страница hello сведения для hello Azure реестра контейнера шаблона, щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="d344f-136">When hello information page for hello Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Создание нового реестра контейнеров Azure][AR02]

1. <span data-ttu-id="d344f-138">Здравствуйте, когда **создать контейнер реестра** отобразить страницу, введите ваш **имя реестра** и **группы ресурсов**, выберите **включить** для Hello **пользователю с правами администратора**, а затем нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="d344f-138">When hello **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for hello **Admin user**, and then click **Create**.</span></span>

   ![Настройка параметров реестра контейнеров Azure][AR03]

1. <span data-ttu-id="d344f-140">После создания контейнера реестра перейдите реестр контейнера tooyour hello портал Azure и нажмите кнопку **клавиши доступа**.</span><span class="sxs-lookup"><span data-stu-id="d344f-140">Once your container registry has been created, navigate tooyour container registry in hello Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="d344f-141">Запишите hello имя пользователя и пароль для hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="d344f-141">Take note of hello username and password for hello next steps.</span></span>

   ![Ключи доступа к реестру контейнеров Azure][AR04]

## <a name="configure-maven-toouse-your-azure-container-registry-access-keys"></a><span data-ttu-id="d344f-143">Настройка доступа к разделам реестра контейнера Azure Maven toouse</span><span class="sxs-lookup"><span data-stu-id="d344f-143">Configure Maven toouse your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="d344f-144">Откройте hello и toohello каталог конфигурации для установки Maven *settings.xml* файл в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="d344f-144">Navigate toohello configuration directory for your Maven installation and open hello *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="d344f-145">Добавить параметры доступа реестра контейнера Azure hello в предыдущем разделе этого учебника toohello `<servers>` коллекции в hello *settings.xml* файла; например:</span><span class="sxs-lookup"><span data-stu-id="d344f-145">Add your Azure Container Registry access settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="d344f-146">Перейдите в каталог проекта toohello завершена для приложения Spring загрузки (например: «*C:\SpringBoot\gs-spring-boot-docker\complete*«или»*/users/robert/SpringBoot/gs-spring-boot-docker / Полный*») и откройте hello *pom.xml* файл в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="d344f-146">Navigate toohello completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="d344f-147">Обновление hello `<properties>` коллекции в hello *pom.xml* файл со значение сервера hello входа для реестра контейнера Azure hello в предыдущем разделе этого учебника; например:</span><span class="sxs-lookup"><span data-stu-id="d344f-147">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry from hello previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="d344f-148">Обновление hello `<plugins>` коллекции в hello *pom.xml* файл, который hello `<plugin>` содержит hello server адрес и реестра имя входа для реестра контейнера Azure hello в предыдущем разделе этого учебника.</span><span class="sxs-lookup"><span data-stu-id="d344f-148">Update hello `<plugins>` collection in hello *pom.xml* file so that hello `<plugin>` contains hello login server address and registry name for your Azure Container Registry from hello previous section of this tutorial.</span></span> <span data-ttu-id="d344f-149">Например:</span><span class="sxs-lookup"><span data-stu-id="d344f-149">For example:</span></span>

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

1. <span data-ttu-id="d344f-150">Перейдите в каталог проекта toohello завершения загрузки Spring приложения и запустите следующие команды toorebuild hello приложения hello push tooyour контейнера hello Azure контейнер реестра:</span><span class="sxs-lookup"><span data-stu-id="d344f-150">Navigate toohello completed project directory for your Spring Boot application and run hello following command toorebuild hello application and push hello container tooyour Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="d344f-151">При отправке вашего tooAzure контейнера Docker, может появиться сообщение об ошибке, аналогичные tooone Привет приведенному ниже, несмотря на то, что успешно создан контейнер Docker:</span><span class="sxs-lookup"><span data-stu-id="d344f-151">When you are pushing your Docker container tooAzure, you may receive an error message that is similar tooone of hello following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="d344f-152">В этом случае может потребоваться toosign в tooyour учетная запись Azure из командной строки Docker hello; Например:</span><span class="sxs-lookup"><span data-stu-id="d344f-152">If this happens, you may need toosign in tooyour Azure account from hello Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="d344f-153">После этого можно передать контейнер с hello командной строки; Например:</span><span class="sxs-lookup"><span data-stu-id="d344f-153">You can then push your container from hello command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="d344f-154">Создание веб-приложения в Linux в службе приложений Azure с помощью образа контейнера</span><span class="sxs-lookup"><span data-stu-id="d344f-154">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="d344f-155">Обзор toohello [портал Azure] и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="d344f-155">Browse toohello [Azure portal] and sign in.</span></span>

1. <span data-ttu-id="d344f-156">Щелкните значок меню hello **+ создать**, нажмите кнопку **Интернет + мобильные устройства**, а затем нажмите кнопку **веб-приложения на платформе Linux**.</span><span class="sxs-lookup"><span data-stu-id="d344f-156">Click hello menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![Создайте новое веб-приложение в hello портал Azure][LX01]

1. <span data-ttu-id="d344f-158">Здравствуйте, когда **веб-приложения на платформе Linux** отобразить страницу, введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="d344f-158">When hello **Web App on Linux** page is displayed, enter hello following information:</span></span>

   <span data-ttu-id="d344f-159">а.</span><span class="sxs-lookup"><span data-stu-id="d344f-159">a.</span></span> <span data-ttu-id="d344f-160">Введите уникальное имя для hello **имя приложения**, например: «*wingtiptoyslinux*.»</span><span class="sxs-lookup"><span data-stu-id="d344f-160">Enter a unique name for hello **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="d344f-161">b.</span><span class="sxs-lookup"><span data-stu-id="d344f-161">b.</span></span> <span data-ttu-id="d344f-162">Выберите ваш **подписки** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="d344f-162">Choose your **Subscription** from hello drop-down list.</span></span>

   <span data-ttu-id="d344f-163">c.</span><span class="sxs-lookup"><span data-stu-id="d344f-163">c.</span></span> <span data-ttu-id="d344f-164">Выберите существующую **группы ресурсов**, или укажите имя toocreate новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d344f-164">Choose an existing **Resource Group**, or specify a name toocreate a new resource group.</span></span>

   <span data-ttu-id="d344f-165">d.</span><span class="sxs-lookup"><span data-stu-id="d344f-165">d.</span></span> <span data-ttu-id="d344f-166">Нажмите кнопку **Настройка контейнера** и введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="d344f-166">Click **Configure container** and enter hello following information:</span></span>

      * <span data-ttu-id="d344f-167">Выберите **Частный реестр**.</span><span class="sxs-lookup"><span data-stu-id="d344f-167">Choose **Private registry**.</span></span>

      * <span data-ttu-id="d344f-168">**Образ и дополнительный тег**: задайте имя контейнера из более ранней версии, например "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span><span class="sxs-lookup"><span data-stu-id="d344f-168">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

      * <span data-ttu-id="d344f-169">**URL-адрес сервера**: укажите URL-адрес реестра из более ранней версии, например "*https://wingtiptoysregistry.azurecr.io*"</span><span class="sxs-lookup"><span data-stu-id="d344f-169">**Server URL**: Specify your registry URL from earlier; for example: "*https://wingtiptoysregistry.azurecr.io*"</span></span>

      * <span data-ttu-id="d344f-170">**Имя входа пользователя** и **Пароль**: укажите учетные данные для входа из своих **ключей доступа**, которые использовались на предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="d344f-170">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="d344f-171">д.</span><span class="sxs-lookup"><span data-stu-id="d344f-171">e.</span></span> <span data-ttu-id="d344f-172">После ввода hello выше сведений щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d344f-172">Once you have entered all of hello above information, click **OK**.</span></span>

   ![Настройка параметров веб-приложения][LX02]

1. <span data-ttu-id="d344f-174">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d344f-174">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="d344f-175">Azure автоматически сопоставит сервера Tomcat tooembedded запросы Интернета, на котором выполняется на hello стандартные порты 80 или 8080.</span><span class="sxs-lookup"><span data-stu-id="d344f-175">Azure will automatically map Internet requests tooembedded Tomcat server that is running on hello standard ports of 80 or 8080.</span></span> <span data-ttu-id="d344f-176">Однако если вы настроили ваш внедренные toorun сервера Tomcat на другой номер порта, необходимо tooadd веб-приложение tooyour переменной среды, определяющего hello порт для внедренного сервера Tomcat.</span><span class="sxs-lookup"><span data-stu-id="d344f-176">However, if you configured your embedded Tomcat server toorun on a custom port, you need tooadd an environment variable tooyour web app that defines hello port for your embedded Tomcat server.</span></span> <span data-ttu-id="d344f-177">Таким образом, toodo используйте hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="d344f-177">toodo so, use hello following steps:</span></span>
>
> 1. <span data-ttu-id="d344f-178">Обзор toohello [портал Azure] и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="d344f-178">Browse toohello [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="d344f-179">Щелкните значок hello **службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="d344f-179">Click hello icon for **App Services**.</span></span> <span data-ttu-id="d344f-180">(См. элемент #1 в приведенном ниже рисунке hello).</span><span class="sxs-lookup"><span data-stu-id="d344f-180">(See item #1 in hello image below.)</span></span>
>
> 3. <span data-ttu-id="d344f-181">Выберите веб-приложение из списка hello.</span><span class="sxs-lookup"><span data-stu-id="d344f-181">Select your web app from hello list.</span></span> <span data-ttu-id="d344f-182">(Элемент #2 в приведенном ниже рисунке hello).</span><span class="sxs-lookup"><span data-stu-id="d344f-182">(Item #2 in hello image below.)</span></span>
>
> 4. <span data-ttu-id="d344f-183">Щелкните **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="d344f-183">Click **Application Settings**.</span></span> <span data-ttu-id="d344f-184">(Элемент #3 в приведенном ниже рисунке hello).</span><span class="sxs-lookup"><span data-stu-id="d344f-184">(Item #3 in hello image below.)</span></span>
>
> 5. <span data-ttu-id="d344f-185">В hello **параметры приложения** добавьте новую переменную среды с именем **ПОРТ** и введите номер другой номер порта для hello значения.</span><span class="sxs-lookup"><span data-stu-id="d344f-185">In hello **App settings** section, add a new environment variable named **PORT** and enter your custom port number for hello value.</span></span> <span data-ttu-id="d344f-186">(Элемент #4 в приведенном ниже рисунке hello).</span><span class="sxs-lookup"><span data-stu-id="d344f-186">(Item #4 in hello image below.)</span></span>
>
> 6. <span data-ttu-id="d344f-187">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d344f-187">Click **Save**.</span></span> <span data-ttu-id="d344f-188">(Элемент #5 в приведенном ниже рисунке hello).</span><span class="sxs-lookup"><span data-stu-id="d344f-188">(Item #5 in hello image below.)</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="d344f-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d344f-190">Next steps</span></span>

<span data-ttu-id="d344f-191">Дополнительные сведения об использовании приложений Spring загрузки в Azure см. следующие статьи hello:</span><span class="sxs-lookup"><span data-stu-id="d344f-191">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="d344f-192">Развертывание приложения загрузки Spring toohello службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="d344f-192">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="d344f-193">Развертывание приложения загрузки Spring в кластере Kubernetes в hello контейнера службы Azure</span><span class="sxs-lookup"><span data-stu-id="d344f-193">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="d344f-194">Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure] и hello [Java средств для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="d344f-194">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="d344f-195">Дополнительные сведения о hello Spring загрузки на Docker образец проекта в разделе [загрузки Spring по началу работы Docker].</span><span class="sxs-lookup"><span data-stu-id="d344f-195">For further details about hello Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="d344f-196">Справку по Приступая к работе с приложениями Spring загрузки см. в разделе hello **Spring Initializr** на https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="d344f-196">For help with getting started with your own Spring Boot applications, see hello **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="d344f-197">Дополнительные сведения о начале работы с создания простого приложения загрузки Spring hello Spring Initializr на https://start.spring.io/ см.</span><span class="sxs-lookup"><span data-stu-id="d344f-197">For more information about getting started with creating a simple Spring Boot application, see hello Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="d344f-198">Дополнительные примеры по как toouse Docker пользовательских образов с помощью Azure в разделе [с помощью пользовательского образа Docker для веб-приложения Azure в Linux].</span><span class="sxs-lookup"><span data-stu-id="d344f-198">For additional examples for how toouse custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

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
