---
title: "hello toouse aaaHow Maven подключаемого модуля для веб-приложения Azure toodeploy tooAzure Spring загрузки приложения"
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
ms.openlocfilehash: 376fe90fe20621e15d7c9856214937c78b66026a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-tooazure"></a><span data-ttu-id="04810-103">Как toouse hello Maven подключаемого модуля для веб-приложения Azure toodeploy tooAzure Spring загрузки приложения</span><span class="sxs-lookup"><span data-stu-id="04810-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app tooAzure</span></span>

<span data-ttu-id="04810-104">Hello [Maven подключаемого модуля для веб-приложения Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) для [Apache Maven](http://maven.apache.org/) обеспечивает прозрачную интеграцию службы приложений Azure в проекты Maven и упрощает процесс hello для разработчиков toodeploy веб-приложений tooAzure службы приложений.</span><span class="sxs-lookup"><span data-stu-id="04810-104">hello [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines hello process for developers toodeploy web apps tooAzure App Service.</span></span>

<span data-ttu-id="04810-105">В этой статье демонстрируется использование hello Maven подключаемого модуля для веб-приложения Azure toodeploy tooAzure приложения загрузки Spring образца службы приложений.</span><span class="sxs-lookup"><span data-stu-id="04810-105">This article demonstrates using hello Maven Plugin for Azure Web Apps toodeploy a sample Spring Boot application tooAzure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="04810-106">Hello Maven подключаемого модуля для веб-приложения Azure в настоящее время доступна в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="04810-106">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="04810-107">Сейчас поддерживается только FTP-публикации, несмотря на то, что дополнительные функции планируются для будущих hello.</span><span class="sxs-lookup"><span data-stu-id="04810-107">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="04810-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="04810-108">Prerequisites</span></span>

<span data-ttu-id="04810-109">В порядке toocomplete hello шагов в этом учебнике требуется hello toohave следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="04810-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="04810-110">Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="04810-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="04810-111">Hello [Azure интерфейс командной строки (CLI)].</span><span class="sxs-lookup"><span data-stu-id="04810-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="04810-112">Актуальный [пакет разработчиков Java (JDK)] версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="04810-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="04810-113">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="04810-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="04810-114">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="04810-114">A [Git] client.</span></span>

## <a name="clone-hello-sample-spring-boot-web-app"></a><span data-ttu-id="04810-115">Клонирование hello образец Spring загрузки веб-приложения</span><span class="sxs-lookup"><span data-stu-id="04810-115">Clone hello sample Spring Boot web app</span></span>

<span data-ttu-id="04810-116">В этом разделе представлены сведения о клонировании готового приложения Spring Boot и его тестировании на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="04810-116">In this section, you clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="04810-117">Откройте командную строку или окно терминала и создайте toohold локальный каталог Spring загрузки приложения и перейдите в каталог toothat; Например:</span><span class="sxs-lookup"><span data-stu-id="04810-117">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="04810-118">-- или --</span><span class="sxs-lookup"><span data-stu-id="04810-118">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="04810-119">Клон hello [Spring начальной загрузки] образец проекта в каталог hello, вы создали; например:</span><span class="sxs-lookup"><span data-stu-id="04810-119">Clone hello [Spring Boot Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. <span data-ttu-id="04810-120">Изменение каталога toohello завершения проекта; Например:</span><span class="sxs-lookup"><span data-stu-id="04810-120">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="04810-121">Построение hello JAR-файл с помощью Maven; Например:</span><span class="sxs-lookup"><span data-stu-id="04810-121">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="04810-122">При создании веб-приложения hello запустите веб-приложение hello, с помощью Maven; Например:</span><span class="sxs-lookup"><span data-stu-id="04810-122">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="04810-123">Тестирование веб-приложения hello путем просмотра tooit локально с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="04810-123">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="04810-124">Например можно использовать следующую команду, если у вас есть доступные перелистывание hello:</span><span class="sxs-lookup"><span data-stu-id="04810-124">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="04810-125">Должно появиться сообщение, отображаемое после hello: **Greetings с Spring загрузки!**</span><span class="sxs-lookup"><span data-stu-id="04810-125">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="04810-126">Создание субъекта-службы Azure</span><span class="sxs-lookup"><span data-stu-id="04810-126">Create an Azure service principal</span></span>

<span data-ttu-id="04810-127">В этом разделе создается Azure участника-службы, hello Maven подключаемый модуль использует при развертывании вашей tooAzure web app.</span><span class="sxs-lookup"><span data-stu-id="04810-127">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your web app tooAzure.</span></span>

1. <span data-ttu-id="04810-128">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="04810-128">Open a command prompt.</span></span>

1. <span data-ttu-id="04810-129">Вход в учетную запись Azure с помощью hello Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="04810-129">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="04810-130">Выполните hello инструкции toocomplete hello процесса входа.</span><span class="sxs-lookup"><span data-stu-id="04810-130">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="04810-131">Создайте субъект-службу Azure.</span><span class="sxs-lookup"><span data-stu-id="04810-131">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="04810-132">Где `uuuuuuuu` — имя пользователя hello и `pppppppp` hello пароль для hello участника-службы.</span><span class="sxs-lookup"><span data-stu-id="04810-132">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="04810-133">Azure в ответ отправляет похожа на следующий пример hello JSON:</span><span class="sxs-lookup"><span data-stu-id="04810-133">Azure responds with JSON that resembles hello following example:</span></span>
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
   > <span data-ttu-id="04810-134">Вы будете использовать значения hello из этот ответ JSON, при настройке подключаемого модуля toodeploy hello Maven вашей tooAzure web app.</span><span class="sxs-lookup"><span data-stu-id="04810-134">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your web app tooAzure.</span></span> <span data-ttu-id="04810-135">Hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, и `tttttttt` являются значения заполнителя, которые используются в этом примере toomake его проще toomap эти значения tootheir соответствующие элементы во время настройки вашей Maven `settings.xml` файл hello рядом раздел.</span><span class="sxs-lookup"><span data-stu-id="04810-135">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a><span data-ttu-id="04810-136">Настройка Maven toouse, участниками службы Azure</span><span class="sxs-lookup"><span data-stu-id="04810-136">Configure Maven toouse your Azure service principal</span></span>

<span data-ttu-id="04810-137">В этом разделе используется hello значения из hello проверки подлинности участника tooconfigure службы Azure, Maven использует при развертывании вашей tooAzure web app.</span><span class="sxs-lookup"><span data-stu-id="04810-137">In this section, you use hello values from your Azure service principal tooconfigure hello authentication that Maven uses when deploying your web app tooAzure.</span></span>

1. <span data-ttu-id="04810-138">Откройте ваш Maven `settings.xml` файл в текстовом редакторе; возможно, этот файл в пути, например hello следующие примеры:</span><span class="sxs-lookup"><span data-stu-id="04810-138">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="04810-139">Добавить параметры основной службы Azure hello в предыдущем разделе этого учебника toohello `<servers>` коллекции в hello *settings.xml* файла; например:</span><span class="sxs-lookup"><span data-stu-id="04810-139">Add your Azure service principal settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="04810-140">Описание</span><span class="sxs-lookup"><span data-stu-id="04810-140">Where:</span></span>
   <span data-ttu-id="04810-141">Элемент</span><span class="sxs-lookup"><span data-stu-id="04810-141">Element</span></span> | <span data-ttu-id="04810-142">Описание</span><span class="sxs-lookup"><span data-stu-id="04810-142">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="04810-143">Задает уникальное имя, которое Maven использует toolook копию параметров безопасности при развертывании вашей tooAzure web app.</span><span class="sxs-lookup"><span data-stu-id="04810-143">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="04810-144">Содержит hello `appId` значение из участника-службы.</span><span class="sxs-lookup"><span data-stu-id="04810-144">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="04810-145">Содержит hello `tenant` значение из участника-службы.</span><span class="sxs-lookup"><span data-stu-id="04810-145">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="04810-146">Содержит hello `password` значение из участника-службы.</span><span class="sxs-lookup"><span data-stu-id="04810-146">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="04810-147">Определяет hello целевой Azure облачной среды, которая представляет `AZURE` в этом примере.</span><span class="sxs-lookup"><span data-stu-id="04810-147">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="04810-148">(Полный список сред доступен в hello [Maven подключаемого модуля для веб-приложения Azure] документации)</span><span class="sxs-lookup"><span data-stu-id="04810-148">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="04810-149">Сохраните и закройте hello *settings.xml* файла.</span><span class="sxs-lookup"><span data-stu-id="04810-149">Save and close hello *settings.xml* file.</span></span>

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-tooazure"></a><span data-ttu-id="04810-150">Необязательно: Настройка вашего pom.xml перед развертыванием вашей tooAzure web app</span><span class="sxs-lookup"><span data-stu-id="04810-150">OPTIONAL: Customize your pom.xml before deploying your web app tooAzure</span></span>

<span data-ttu-id="04810-151">Откройте hello `pom.xml` файл для загрузки Spring приложения в текстовом редакторе, а затем найдите hello `<plugin>` элемент для `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="04810-151">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="04810-152">Этот элемент должен быть похож на следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="04810-152">This element should resemble hello following example:</span></span>

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
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="04810-153">Имеется несколько значений, которые можно изменять для подключаемого модуля Maven hello и подробное описание каждого из этих элементов доступен в hello [Maven подключаемого модуля для веб-приложения Azure] документации.</span><span class="sxs-lookup"><span data-stu-id="04810-153">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="04810-154">Существует ряд значений, на которые следует обратить внимание в этой статье.</span><span class="sxs-lookup"><span data-stu-id="04810-154">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="04810-155">Элемент</span><span class="sxs-lookup"><span data-stu-id="04810-155">Element</span></span> | <span data-ttu-id="04810-156">Описание</span><span class="sxs-lookup"><span data-stu-id="04810-156">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="04810-157">Указывает версию hello hello [Maven подключаемого модуля для веб-приложения Azure].</span><span class="sxs-lookup"><span data-stu-id="04810-157">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="04810-158">Необходимо проверить версию hello, перечисленные в hello [Maven центрального репозитория](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure, в которых используется hello последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="04810-158">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="04810-159">Указывает hello сведения для проверки подлинности для Azure, который в данном примере содержит `<serverId>` элемент, содержащий `azure-auth`; Maven использует toolook, значение основного значениями hello службы Azure в вашей Maven *settings.xml* файл, который вы определили в предыдущем разделе этой статьи.</span><span class="sxs-lookup"><span data-stu-id="04810-159">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="04810-160">Указывает hello целевой группы ресурсов, который является `maven-plugin` в этом примере.</span><span class="sxs-lookup"><span data-stu-id="04810-160">Specifies hello target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="04810-161">Группа ресурсов Hello создается во время развертывания, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="04810-161">hello resource group is created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="04810-162">Указывает имя целевой hello для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="04810-162">Specifies hello target name for your web app.</span></span> <span data-ttu-id="04810-163">В этом примере — имя целевого hello `maven-web-app-${maven.build.timestamp}`, где hello `${maven.build.timestamp}` в конфликт tooavoid примере добавляется суффикс.</span><span class="sxs-lookup"><span data-stu-id="04810-163">In this example, hello target name is `maven-web-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="04810-164">(метка времени hello необязателен; можно указать любую уникальную строку для имени приложения hello).</span><span class="sxs-lookup"><span data-stu-id="04810-164">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="04810-165">Указывает hello целевой области, которая в данном примере `westus`.</span><span class="sxs-lookup"><span data-stu-id="04810-165">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="04810-166">(Полный список находится в hello [Maven подключаемого модуля для веб-приложения Azure] документации.)</span><span class="sxs-lookup"><span data-stu-id="04810-166">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<javaVersion>` | <span data-ttu-id="04810-167">Указывает версию среды выполнения Java hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="04810-167">Specifies hello Java runtime version for your web app.</span></span> <span data-ttu-id="04810-168">(Полный список находится в hello [Maven подключаемого модуля для веб-приложения Azure] документации.)</span><span class="sxs-lookup"><span data-stu-id="04810-168">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<deploymentType>` | <span data-ttu-id="04810-169">Тип развертывания для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="04810-169">Specifies deployment type for your web app.</span></span> <span data-ttu-id="04810-170">Сейчас поддерживается только `ftp`, хотя поддержка других типов развертывания находится в разработке.</span><span class="sxs-lookup"><span data-stu-id="04810-170">For now, only `ftp` is supported, although support for other deployment types is in development.</span></span>
`<resources>` | <span data-ttu-id="04810-171">Указывает ресурсы и получателям, которые Maven использует при развертывании вашей tooAzure web app.</span><span class="sxs-lookup"><span data-stu-id="04810-171">Specifies resources and target destinations which Maven uses when deploying your web app tooAzure.</span></span> <span data-ttu-id="04810-172">В этом примере два `<resource>` элементы указывают, что Maven развернет hello JAR-файл для веб-приложения и hello *web.config* файл из проекта загрузки Spring hello.</span><span class="sxs-lookup"><span data-stu-id="04810-172">In this example, two `<resource>` elements specify that Maven will deploy hello JAR file for your web app and hello *web.config* file from hello Spring Boot project.</span></span>

## <a name="build-and-deploy-your-web-app-tooazure"></a><span data-ttu-id="04810-173">Построение и развертывание вашей tooAzure web app</span><span class="sxs-lookup"><span data-stu-id="04810-173">Build and deploy your web app tooAzure</span></span>

<span data-ttu-id="04810-174">После настройки всех параметров hello в предыдущих подразделах этой статьи hello, вы являетесь toodeploy готовности вашей tooAzure web app.</span><span class="sxs-lookup"><span data-stu-id="04810-174">Once you have configured all of hello settings in hello preceding sections of this article, you are ready toodeploy your web app tooAzure.</span></span> <span data-ttu-id="04810-175">Таким образом, toodo используйте hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="04810-175">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="04810-176">Из командной строки hello или окно терминала, который использовался ранее, перестройте hello JAR-файл с помощью Maven при внесении любого изменения toohello *pom.xml* файла; например:</span><span class="sxs-lookup"><span data-stu-id="04810-176">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="04810-177">Развертывание вашей tooAzure web app с помощью Maven; Например:</span><span class="sxs-lookup"><span data-stu-id="04810-177">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="04810-178">Maven развернет ваш веб tooAzure приложения; Если веб-приложение hello еще не существует, он будет создан.</span><span class="sxs-lookup"><span data-stu-id="04810-178">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

<span data-ttu-id="04810-179">При развертывании веб-узла можно будет toomanage его с помощью hello [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="04810-179">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="04810-180">Веб-приложение будет указано в разделе **Службы приложений**:</span><span class="sxs-lookup"><span data-stu-id="04810-180">Your web app will be listed in **App Services**:</span></span>

   ![Веб-приложение в разделе "Службы приложений" на портале Azure][AP01]

* <span data-ttu-id="04810-182">И hello URL-адрес для веб-приложения будут указаны в hello **Обзор** веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="04810-182">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="04810-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="04810-184">Next steps</span></span>

<span data-ttu-id="04810-185">Дополнительные сведения о hello различные технологии, описанные в этой статье, см. следующие статьи hello:</span><span class="sxs-lookup"><span data-stu-id="04810-185">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="04810-186">[Maven подключаемого модуля для веб-приложения Azure]</span><span class="sxs-lookup"><span data-stu-id="04810-186">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="04810-187">Войдите в tooAzure из hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="04810-187">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="04810-188">Как toouse hello Maven подключаемого модуля для веб-приложения Azure toodeploy контейнерного tooAzure приложения загрузки пружины</span><span class="sxs-lookup"><span data-stu-id="04810-188">How toouse hello Maven Plugin for Azure Web Apps toodeploy a containerized Spring Boot app tooAzure</span></span>](app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="04810-189">Создание субъекта-службы Azure с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="04810-189">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="04810-190">Справочник по параметрам Maven</span><span class="sxs-lookup"><span data-stu-id="04810-190">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure интерфейс командной строки (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[портал Azure]: https://portal.azure.com/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring начальной загрузки]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Maven подключаемого модуля для веб-приложения Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP02.png
