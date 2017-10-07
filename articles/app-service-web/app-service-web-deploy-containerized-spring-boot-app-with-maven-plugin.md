---
title: "hello toouse aaaHow Maven подключаемого модуля для веб-приложения Azure toodeploy контейнерного tooAzure приложения загрузки пружины"
description: "Узнайте, как toouse hello Maven подключаемого модуля для веб-приложения Azure toodeploy tooAzure Spring загрузки приложения."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: e7e760d4ef5bd4c92a4126a50a2b12e5c8f2b4a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-containerized-spring-boot-app-tooazure"></a><span data-ttu-id="08967-103">Как toouse hello Maven подключаемого модуля для веб-приложения Azure toodeploy контейнерного tooAzure приложения загрузки пружины</span><span class="sxs-lookup"><span data-stu-id="08967-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a containerized Spring Boot app tooAzure</span></span>

<span data-ttu-id="08967-104">Hello [Maven подключаемого модуля для веб-приложения Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) для [Apache Maven](http://maven.apache.org/) обеспечивает прозрачную интеграцию службы приложений Azure в проекты Maven и упрощает процесс hello для разработчиков toodeploy веб-приложений tooAzure службы приложений.</span><span class="sxs-lookup"><span data-stu-id="08967-104">hello [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines hello process for developers toodeploy web apps tooAzure App Service .</span></span>

<span data-ttu-id="08967-105">В этой статье демонстрируется использование hello Maven подключаемого модуля для веб-приложения Azure toodeploy Spring загрузки примера приложения в tooAzure контейнера Docker приложения службы.</span><span class="sxs-lookup"><span data-stu-id="08967-105">This article demonstrates using hello Maven Plugin for Azure Web Apps toodeploy a sample Spring Boot application in a Docker container tooAzure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="08967-106">Hello Maven подключаемого модуля для веб-приложения Azure в настоящее время доступна в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="08967-106">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="08967-107">Сейчас поддерживается только FTP-публикации, несмотря на то, что дополнительные функции планируются для будущих hello.</span><span class="sxs-lookup"><span data-stu-id="08967-107">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="08967-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="08967-108">Prerequisites</span></span>

<span data-ttu-id="08967-109">В порядке toocomplete hello шагов в этом учебнике требуется hello toohave следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="08967-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="08967-110">Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="08967-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="08967-111">Hello [Azure интерфейс командной строки (CLI)].</span><span class="sxs-lookup"><span data-stu-id="08967-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="08967-112">Актуальный [пакет разработчиков Java (JDK)] версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="08967-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="08967-113">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="08967-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="08967-114">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="08967-114">A [Git] client.</span></span>
* <span data-ttu-id="08967-115">Клиент [Docker].</span><span class="sxs-lookup"><span data-stu-id="08967-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="08967-116">Из-за требований к виртуализации toohello этого учебника не может следовать за hello действия, описанные в этой статье на виртуальной машине; необходимо использовать физический компьютер с включенными возможностями виртуализации.</span><span class="sxs-lookup"><span data-stu-id="08967-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="08967-117">Образец hello клон Spring загрузки на Docker веб-приложения</span><span class="sxs-lookup"><span data-stu-id="08967-117">Clone hello sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="08967-118">В этом разделе представлены сведения о клонировании контейнерного приложения Spring Boot и его тестировании на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="08967-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="08967-119">Откройте командную строку или окно терминала и создайте toohold локальный каталог Spring загрузки приложения и перейдите в каталог toothat; Например:</span><span class="sxs-lookup"><span data-stu-id="08967-119">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="08967-120">-- или --</span><span class="sxs-lookup"><span data-stu-id="08967-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="08967-121">Клон hello [загрузки Spring по началу работы Docker] образец проекта в каталог hello, вы создали; например:</span><span class="sxs-lookup"><span data-stu-id="08967-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="08967-122">Изменение каталога toohello завершения проекта; Например:</span><span class="sxs-lookup"><span data-stu-id="08967-122">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="08967-123">Построение hello JAR-файл с помощью Maven; Например:</span><span class="sxs-lookup"><span data-stu-id="08967-123">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="08967-124">При создании веб-приложения hello запустите веб-приложение hello, с помощью Maven; Например:</span><span class="sxs-lookup"><span data-stu-id="08967-124">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="08967-125">Тестирование веб-приложения hello путем просмотра tooit локально с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="08967-125">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="08967-126">Например можно использовать следующую команду, если у вас есть доступные перелистывание hello:</span><span class="sxs-lookup"><span data-stu-id="08967-126">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="08967-127">Должно появиться сообщение, отображаемое после hello: **Docker Здравствуй, мир!**</span><span class="sxs-lookup"><span data-stu-id="08967-127">You should see hello following message displayed: **Hello Docker World**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="08967-128">Создание субъекта-службы Azure</span><span class="sxs-lookup"><span data-stu-id="08967-128">Create an Azure service principal</span></span>

<span data-ttu-id="08967-129">В этом разделе создается Azure участника-службы, hello Maven подключаемый модуль использует при развертывании вашей tooAzure контейнера.</span><span class="sxs-lookup"><span data-stu-id="08967-129">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="08967-130">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="08967-130">Open a command prompt.</span></span>

1. <span data-ttu-id="08967-131">Вход в учетную запись Azure с помощью hello Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="08967-131">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="08967-132">Выполните hello инструкции toocomplete hello процесса входа.</span><span class="sxs-lookup"><span data-stu-id="08967-132">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="08967-133">Создайте субъект-службу Azure.</span><span class="sxs-lookup"><span data-stu-id="08967-133">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="08967-134">Где `uuuuuuuu` — имя пользователя hello и `pppppppp` hello пароль для hello участника-службы.</span><span class="sxs-lookup"><span data-stu-id="08967-134">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="08967-135">Azure в ответ отправляет похожа на следующий пример hello JSON:</span><span class="sxs-lookup"><span data-stu-id="08967-135">Azure responds with JSON that resembles hello following example:</span></span>
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="08967-136">Вы будете использовать значения hello из этот ответ JSON, при настройке подключаемого модуля toodeploy hello Maven вашей tooAzure контейнера.</span><span class="sxs-lookup"><span data-stu-id="08967-136">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your container tooAzure.</span></span> <span data-ttu-id="08967-137">Hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, и `tttttttt` являются значения заполнителя, которые используются в этом примере toomake его проще toomap эти значения tootheir соответствующие элементы во время настройки вашей Maven `settings.xml` файл hello рядом раздел.</span><span class="sxs-lookup"><span data-stu-id="08967-137">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a><span data-ttu-id="08967-138">Настройка Maven toouse, участниками службы Azure</span><span class="sxs-lookup"><span data-stu-id="08967-138">Configure Maven toouse your Azure service principal</span></span>

<span data-ttu-id="08967-139">В этом разделе используется hello значения из hello проверки подлинности участника tooconfigure службы Azure, Maven будет использовать при развертывании вашей tooAzure контейнера.</span><span class="sxs-lookup"><span data-stu-id="08967-139">In this section, you use hello values from your Azure service principal tooconfigure hello authentication that Maven will use when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="08967-140">Откройте ваш Maven `settings.xml` файл в текстовом редакторе; возможно, этот файл в пути, например hello следующие примеры:</span><span class="sxs-lookup"><span data-stu-id="08967-140">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="08967-141">Добавить параметры основной службы Azure hello в предыдущем разделе этого учебника toohello `<servers>` коллекции в hello *settings.xml* файла; например:</span><span class="sxs-lookup"><span data-stu-id="08967-141">Add your Azure service principal settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   <span data-ttu-id="08967-142">Описание</span><span class="sxs-lookup"><span data-stu-id="08967-142">Where:</span></span>
   <span data-ttu-id="08967-143">Элемент</span><span class="sxs-lookup"><span data-stu-id="08967-143">Element</span></span> | <span data-ttu-id="08967-144">Описание</span><span class="sxs-lookup"><span data-stu-id="08967-144">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="08967-145">Задает уникальное имя, которое Maven использует toolook копию параметров безопасности при развертывании вашей tooAzure web app.</span><span class="sxs-lookup"><span data-stu-id="08967-145">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="08967-146">Содержит hello `appId` значение из участника-службы.</span><span class="sxs-lookup"><span data-stu-id="08967-146">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="08967-147">Содержит hello `tenant` значение из участника-службы.</span><span class="sxs-lookup"><span data-stu-id="08967-147">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="08967-148">Содержит hello `password` значение из участника-службы.</span><span class="sxs-lookup"><span data-stu-id="08967-148">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="08967-149">Определяет hello целевой Azure облачной среды, которая представляет `AZURE` в этом примере.</span><span class="sxs-lookup"><span data-stu-id="08967-149">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="08967-150">(Полный список сред доступен в hello [Maven подключаемого модуля для веб-приложения Azure] документации)</span><span class="sxs-lookup"><span data-stu-id="08967-150">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="08967-151">Сохраните и закройте hello *settings.xml* файла.</span><span class="sxs-lookup"><span data-stu-id="08967-151">Save and close hello *settings.xml* file.</span></span>

## <a name="optional-deploy-your-local-docker-file-toodocker-hub"></a><span data-ttu-id="08967-152">ДОПОЛНИТЕЛЬНО Развертывание вашей локальной tooDocker файл Docker Hub</span><span class="sxs-lookup"><span data-stu-id="08967-152">OPTIONAL: Deploy your local Docker file tooDocker Hub</span></span>

<span data-ttu-id="08967-153">При наличии учетной записи Docker, можно построить вашей Docker локально образ контейнера и принудительно отправить его tooDocker концентратора.</span><span class="sxs-lookup"><span data-stu-id="08967-153">If you have a Docker account, you can build your Docker container image locally and push it tooDocker Hub.</span></span> <span data-ttu-id="08967-154">toodo таким образом, используйте следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="08967-154">toodo so, use hello following steps.</span></span>

1. <span data-ttu-id="08967-155">Откройте hello `pom.xml` файл для загрузки Spring приложения в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="08967-155">Open hello `pom.xml` file for your Spring Boot application in a text editor.</span></span>

1. <span data-ttu-id="08967-156">Найдите hello `<imageName>` дочерний элемент элемента hello `<containerSettings>` элемента.</span><span class="sxs-lookup"><span data-stu-id="08967-156">Locate hello `<imageName>` child element of hello `<containerSettings>` element.</span></span>

1. <span data-ttu-id="08967-157">Обновление hello `${docker.image.prefix}` значение с Docker имя учетной записи:</span><span class="sxs-lookup"><span data-stu-id="08967-157">Update hello `${docker.image.prefix}` value with your Docker account name:</span></span>
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. <span data-ttu-id="08967-158">Выберите один из следующих методов развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="08967-158">Choose one of hello following deployment methods:</span></span>

   * <span data-ttu-id="08967-159">Построение образа контейнера локально с Maven, а затем использовать Docker toopush вашего контейнера tooDocker концентратора:</span><span class="sxs-lookup"><span data-stu-id="08967-159">Build your container image locally with Maven, and then use Docker toopush your container tooDocker Hub:</span></span>
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * <span data-ttu-id="08967-160">Если у вас есть hello [подключаемый модуль Docker для Maven] установлен, можно автоматически создавать и hello вашей tooDocker образ контейнера концентратора с помощью `-DpushImage` параметр:</span><span class="sxs-lookup"><span data-stu-id="08967-160">If you have hello [Docker plugin for Maven] installed, you can automatically build and your container image tooDocker Hub by using hello `-DpushImage` parameter:</span></span>
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-tooazure"></a><span data-ttu-id="08967-161">Необязательно: Настройка вашего pom.xml перед развертыванием вашей tooAzure контейнера</span><span class="sxs-lookup"><span data-stu-id="08967-161">OPTIONAL: Customize your pom.xml before deploying your container tooAzure</span></span>

<span data-ttu-id="08967-162">Откройте hello `pom.xml` файл для загрузки Spring приложения в текстовом редакторе, а затем найдите hello `<plugin>` элемент для `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="08967-162">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="08967-163">Этот элемент должен быть похож на следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="08967-163">This element should resemble hello following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="08967-164">Имеется несколько значений, которые можно изменять для подключаемого модуля Maven hello и подробное описание каждого из этих элементов доступен в hello [Maven подключаемого модуля для веб-приложения Azure] документации.</span><span class="sxs-lookup"><span data-stu-id="08967-164">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="08967-165">Существует ряд значений, на которые следует обратить внимание в этой статье.</span><span class="sxs-lookup"><span data-stu-id="08967-165">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="08967-166">Элемент</span><span class="sxs-lookup"><span data-stu-id="08967-166">Element</span></span> | <span data-ttu-id="08967-167">Описание</span><span class="sxs-lookup"><span data-stu-id="08967-167">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="08967-168">Указывает версию hello hello [Maven подключаемого модуля для веб-приложения Azure].</span><span class="sxs-lookup"><span data-stu-id="08967-168">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="08967-169">Необходимо проверить версию hello, перечисленные в hello [Maven центрального репозитория](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure, в которых используется hello последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="08967-169">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="08967-170">Указывает hello сведения для проверки подлинности для Azure, который в данном примере содержит `<serverId>` элемент, содержащий `azure-auth`; Maven использует toolook, значение основного значениями hello службы Azure в вашей Maven *settings.xml* файл, который вы определили в предыдущем разделе этой статьи.</span><span class="sxs-lookup"><span data-stu-id="08967-170">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="08967-171">Указывает hello целевой группы ресурсов, который является `maven-plugin` в этом примере.</span><span class="sxs-lookup"><span data-stu-id="08967-171">Specifies hello target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="08967-172">будет создана группа ресурсов Hello во время развертывания, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="08967-172">hello resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="08967-173">Указывает имя целевой hello для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="08967-173">Specifies hello target name for your web app.</span></span> <span data-ttu-id="08967-174">В этом примере — имя целевого hello `maven-linux-app-${maven.build.timestamp}`, где hello `${maven.build.timestamp}` в конфликт tooavoid примере добавляется суффикс.</span><span class="sxs-lookup"><span data-stu-id="08967-174">In this example, hello target name is `maven-linux-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="08967-175">(метка времени hello необязателен; можно указать любую уникальную строку для имени приложения hello).</span><span class="sxs-lookup"><span data-stu-id="08967-175">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="08967-176">Указывает hello целевой области, которая в данном примере `westus`.</span><span class="sxs-lookup"><span data-stu-id="08967-176">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="08967-177">(Полный список находится в hello [Maven подключаемого модуля для веб-приложения Azure] документации.)</span><span class="sxs-lookup"><span data-stu-id="08967-177">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<appSettings>` | <span data-ttu-id="08967-178">Определяет все уникальные настройки для Maven toouse при развертывании вашей tooAzure web app.</span><span class="sxs-lookup"><span data-stu-id="08967-178">Specifies any unique settings for Maven toouse when deploying your web app tooAzure.</span></span> <span data-ttu-id="08967-179">В этом примере `<property>` элемент содержит дочерние элементы, укажите порт приложения hello пары имя/значение.</span><span class="sxs-lookup"><span data-stu-id="08967-179">In this example, a `<property>` element contains a name/value pair of child elements that specify hello port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="08967-180">номер порта hello toochange параметры Hello в этом примере необходимы только при изменении порта hello относительно значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="08967-180">hello settings toochange hello port number in this example are only necessary when you are changing hello port from hello default.</span></span>
>

## <a name="build-and-deploy-your-container-tooazure"></a><span data-ttu-id="08967-181">Построение и развертывание вашей tooAzure контейнера</span><span class="sxs-lookup"><span data-stu-id="08967-181">Build and deploy your container tooAzure</span></span>

<span data-ttu-id="08967-182">После настройки всех параметров hello в предыдущих подразделах этой статьи hello, вы являетесь toodeploy готовности вашей tooAzure контейнера.</span><span class="sxs-lookup"><span data-stu-id="08967-182">Once you have configured all of hello settings in hello preceding sections of this article, you are ready toodeploy your container tooAzure.</span></span> <span data-ttu-id="08967-183">Таким образом, toodo используйте hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="08967-183">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="08967-184">Из командной строки hello или окно терминала, который использовался ранее, перестройте hello JAR-файл с помощью Maven при внесении любого изменения toohello *pom.xml* файла; например:</span><span class="sxs-lookup"><span data-stu-id="08967-184">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="08967-185">Развертывание вашей tooAzure web app с помощью Maven; Например:</span><span class="sxs-lookup"><span data-stu-id="08967-185">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="08967-186">Maven развернет ваш веб tooAzure приложения; Если веб-приложение hello еще не существует, он будет создан.</span><span class="sxs-lookup"><span data-stu-id="08967-186">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="08967-187">Если область hello, которое задается в hello `<region>` элемент вашей *pom.xml* файла не имеет достаточного количества доступных серверов при запуске развертывания, может появиться ошибка примерно toohello, в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="08967-187">If hello region which you specify in hello `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar toohello following example:</span></span>
>
> ```
> [INFO] Start deploying tooWeb App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed tooexecute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="08967-188">В этом случае можно указать, что другой регион и повторно запустите hello toodeploy команда Maven приложения.</span><span class="sxs-lookup"><span data-stu-id="08967-188">If this happens, you can specify another region and re-run hello Maven command toodeploy your application.</span></span>
>
>

<span data-ttu-id="08967-189">При развертывании веб-узла можно будет toomanage его с помощью hello [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="08967-189">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="08967-190">Веб-приложение будет указано в разделе **Службы приложений**:</span><span class="sxs-lookup"><span data-stu-id="08967-190">Your web app will be listed in **App Services**:</span></span>

   ![Веб-приложение в разделе "Службы приложений" на портале Azure][AP01]

* <span data-ttu-id="08967-192">И hello URL-адрес для веб-приложения будут указаны в hello **Обзор** веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="08967-192">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

   ![Определение hello URL-адрес для веб-приложения][AP02]

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

## <a name="next-steps"></a><span data-ttu-id="08967-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="08967-194">Next steps</span></span>

<span data-ttu-id="08967-195">Дополнительные сведения о hello различные технологии, описанные в этой статье, см. следующие статьи hello:</span><span class="sxs-lookup"><span data-stu-id="08967-195">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="08967-196">[Maven подключаемого модуля для веб-приложения Azure]</span><span class="sxs-lookup"><span data-stu-id="08967-196">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="08967-197">Войдите в tooAzure из hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="08967-197">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="08967-198">Как toouse hello Maven подключаемого модуля для веб-приложения Azure toodeploy tooAzure приложения загрузки Spring службы приложений</span><span class="sxs-lookup"><span data-stu-id="08967-198">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app tooAzure App Service </span></span>](app-service-web-deploy-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="08967-199">Создание субъекта-службы Azure с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="08967-199">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="08967-200">Справочник по параметрам Maven</span><span class="sxs-lookup"><span data-stu-id="08967-200">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="08967-201">[подключаемый модуль Docker для Maven]</span><span class="sxs-lookup"><span data-stu-id="08967-201">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Azure интерфейс командной строки (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[портал Azure]: https://portal.azure.com/
[Docker]: https://www.docker.com/
[подключаемый модуль Docker для Maven]: https://github.com/spotify/docker-maven-plugin
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[загрузки Spring по началу работы Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Maven подключаемого модуля для веб-приложения Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP02.png
