---
title: "hello toouse aaaHow Maven подключаемого модуля для веб-приложения Azure toodeploy приложении Spring загрузки в реестре контейнеров Azure tooAzure службы приложений"
description: "Этот учебник поможет вам хотя toodeploy действия hello приложение Spring загрузки в реестре контейнеров Azure tooAzure tooAzure службы приложений с помощью подключаемого модуля Maven."
services: 
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
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 55b95e310c9ee186a6d77d941c5a620c2e259d8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a><span data-ttu-id="34711-103">Как toouse hello Maven подключаемого модуля для веб-приложения Azure toodeploy приложении Spring загрузки в реестре контейнеров Azure tooAzure службы приложений</span><span class="sxs-lookup"><span data-stu-id="34711-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app in Azure Container Registry tooAzure App Service</span></span>

<span data-ttu-id="34711-104">Hello  **[Spring Framework]**  — это популярный открытая платформа Java разработчики могут создать web, мобильных устройств и приложения API.</span><span class="sxs-lookup"><span data-stu-id="34711-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="34711-105">В этом учебнике используется образец приложения, созданного с использованием [загрузки Spring], управляемых соглашение случай использования Spring tooget быстро начать работу.</span><span class="sxs-lookup"><span data-stu-id="34711-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="34711-106">В этой статье показано, как toodeploy tooAzure приложения загрузки Spring образец реестра контейнера, а затем использовать hello Maven подключаемого модуля для веб-приложения Azure toodeploy tooAzure вашего приложения служб приложений.</span><span class="sxs-lookup"><span data-stu-id="34711-106">This article demonstrates how toodeploy a sample Spring Boot application tooAzure Container Registry, and then use hello Maven Plugin for Azure Web Apps toodeploy your application tooAzure App Service.</span></span>

> [!NOTE]
>
> <span data-ttu-id="34711-107">Hello Maven подключаемого модуля для веб-приложения Azure в настоящее время доступна в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="34711-107">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="34711-108">Сейчас поддерживается только FTP-публикации, несмотря на то, что дополнительные функции планируются для будущих hello.</span><span class="sxs-lookup"><span data-stu-id="34711-108">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="34711-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="34711-109">Prerequisites</span></span>

<span data-ttu-id="34711-110">В порядке toocomplete hello шагов в этом учебнике требуется hello toohave следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="34711-110">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="34711-111">Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="34711-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="34711-112">Hello [Azure интерфейс командной строки (CLI)].</span><span class="sxs-lookup"><span data-stu-id="34711-112">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="34711-113">Актуальный [пакет разработчиков Java (JDK)] версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="34711-113">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="34711-114">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="34711-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="34711-115">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="34711-115">A [Git] client.</span></span>
* <span data-ttu-id="34711-116">Клиент [Docker].</span><span class="sxs-lookup"><span data-stu-id="34711-116">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="34711-117">Из-за требований к виртуализации toohello этого учебника не может следовать за hello действия, описанные в этой статье на виртуальной машине; необходимо использовать физический компьютер с включенными возможностями виртуализации.</span><span class="sxs-lookup"><span data-stu-id="34711-117">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="34711-118">Образец hello клон Spring загрузки на Docker веб-приложения</span><span class="sxs-lookup"><span data-stu-id="34711-118">Clone hello sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="34711-119">В этом разделе представлены сведения о клонировании контейнерного приложения Spring Boot и его тестировании на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="34711-119">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="34711-120">Откройте командную строку или окно терминала и создайте toohold локальный каталог Spring загрузки приложения и перейдите в каталог toothat; Например:</span><span class="sxs-lookup"><span data-stu-id="34711-120">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="34711-121">-- или --</span><span class="sxs-lookup"><span data-stu-id="34711-121">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="34711-122">Клон hello [загрузки Spring по началу работы Docker] образец проекта в каталог hello, вы создали; например:</span><span class="sxs-lookup"><span data-stu-id="34711-122">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="34711-123">Изменение каталога toohello завершения проекта; Например:</span><span class="sxs-lookup"><span data-stu-id="34711-123">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="34711-124">Построение hello JAR-файл с помощью Maven; Например:</span><span class="sxs-lookup"><span data-stu-id="34711-124">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="34711-125">При создании веб-приложения hello запустите веб-приложение hello, с помощью Maven; Например:</span><span class="sxs-lookup"><span data-stu-id="34711-125">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="34711-126">Тестирование веб-приложения hello путем просмотра tooit локально с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="34711-126">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="34711-127">Например можно использовать следующую команду, если у вас есть доступные перелистывание hello:</span><span class="sxs-lookup"><span data-stu-id="34711-127">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="34711-128">Должно появиться сообщение, отображаемое после hello: **Docker Здравствуй, мир!**</span><span class="sxs-lookup"><span data-stu-id="34711-128">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![Локальный просмотр образца приложения][SB01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="34711-130">Создание субъекта-службы Azure</span><span class="sxs-lookup"><span data-stu-id="34711-130">Create an Azure service principal</span></span>

<span data-ttu-id="34711-131">В этом разделе создается Azure участника-службы, hello Maven подключаемый модуль использует при развертывании вашей tooAzure контейнера.</span><span class="sxs-lookup"><span data-stu-id="34711-131">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="34711-132">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="34711-132">Open a command prompt.</span></span>

1. <span data-ttu-id="34711-133">Вход в учетную запись Azure с помощью hello Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="34711-133">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="34711-134">Выполните hello инструкции toocomplete hello процесса входа.</span><span class="sxs-lookup"><span data-stu-id="34711-134">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="34711-135">Создайте субъект-службу Azure.</span><span class="sxs-lookup"><span data-stu-id="34711-135">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="34711-136">Где `uuuuuuuu` — имя пользователя hello и `pppppppp` hello пароль для hello участника-службы.</span><span class="sxs-lookup"><span data-stu-id="34711-136">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="34711-137">Azure в ответ отправляет похожа на следующий пример hello JSON:</span><span class="sxs-lookup"><span data-stu-id="34711-137">Azure responds with JSON that resembles hello following example:</span></span>
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
   > <span data-ttu-id="34711-138">Вы будете использовать значения hello из этот ответ JSON, при настройке подключаемого модуля toodeploy hello Maven вашей tooAzure контейнера.</span><span class="sxs-lookup"><span data-stu-id="34711-138">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your container tooAzure.</span></span> <span data-ttu-id="34711-139">Hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, и `tttttttt` являются значения заполнителя, которые используются в этом примере toomake его проще toomap эти значения tootheir соответствующие элементы во время настройки вашей Maven `settings.xml` файл hello рядом раздел.</span><span class="sxs-lookup"><span data-stu-id="34711-139">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="34711-140">Создайте в реестре контейнера Azure с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="34711-140">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="34711-141">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="34711-141">Open a command prompt.</span></span>

1. <span data-ttu-id="34711-142">Вход tooyour учетная запись Azure:</span><span class="sxs-lookup"><span data-stu-id="34711-142">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="34711-143">Создание группы ресурсов для hello ресурсы Azure, которая будет использоваться в этой статье:</span><span class="sxs-lookup"><span data-stu-id="34711-143">Create a resource group for hello Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="34711-144">Замените `wingtiptoysresources` в этом примере уникальным именем для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="34711-144">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="34711-145">Создайте реестра закрытый контейнер Azure в группе ресурсов hello Spring загрузки приложения:</span><span class="sxs-lookup"><span data-stu-id="34711-145">Create a private Azure container registry in hello resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="34711-146">Замените `wingtiptoysregistry` в этом примере уникальным именем для реестра контейнеров.</span><span class="sxs-lookup"><span data-stu-id="34711-146">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="34711-147">Получить пароль hello для контейнера реестра:</span><span class="sxs-lookup"><span data-stu-id="34711-147">Retrieve hello password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="34711-148">В ответ Azure предоставит пароль, например:</span><span class="sxs-lookup"><span data-stu-id="34711-148">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a><span data-ttu-id="34711-149">Добавьте контейнер Azure реестра и параметры Maven tooyour основной службы Azure</span><span class="sxs-lookup"><span data-stu-id="34711-149">Add your Azure container registry and Azure service principal tooyour Maven settings</span></span>

1. <span data-ttu-id="34711-150">Откройте ваш Maven `settings.xml` файл в текстовом редакторе; возможно, этот файл в пути, например hello следующие примеры:</span><span class="sxs-lookup"><span data-stu-id="34711-150">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="34711-151">Добавить параметры доступа реестра контейнера Azure hello в предыдущем разделе этой статьи toohello `<servers>` коллекции в hello *settings.xml* файла; например:</span><span class="sxs-lookup"><span data-stu-id="34711-151">Add your Azure Container Registry access settings from hello previous section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="34711-152">Описание</span><span class="sxs-lookup"><span data-stu-id="34711-152">Where:</span></span>
   <span data-ttu-id="34711-153">Элемент</span><span class="sxs-lookup"><span data-stu-id="34711-153">Element</span></span> | <span data-ttu-id="34711-154">Описание</span><span class="sxs-lookup"><span data-stu-id="34711-154">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="34711-155">Содержит имя hello реестра закрытый контейнер Azure.</span><span class="sxs-lookup"><span data-stu-id="34711-155">Contains hello name of your private Azure container registry.</span></span>
   `<username>` | <span data-ttu-id="34711-156">Содержит имя hello реестра закрытый контейнер Azure.</span><span class="sxs-lookup"><span data-stu-id="34711-156">Contains hello name of your private Azure container registry.</span></span>
   `<password>` | <span data-ttu-id="34711-157">Содержит пароль hello, полученный в предыдущем разделе hello данной статьи.</span><span class="sxs-lookup"><span data-stu-id="34711-157">Contains hello password you retrieved in hello previous section of this article.</span></span>

1. <span data-ttu-id="34711-158">Добавить параметры основной службы Azure в предыдущем разделе этой статьи toohello `<servers>` коллекции в hello *settings.xml* файла; например:</span><span class="sxs-lookup"><span data-stu-id="34711-158">Add your Azure service principal settings from an earlier section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="34711-159">Описание</span><span class="sxs-lookup"><span data-stu-id="34711-159">Where:</span></span>
   <span data-ttu-id="34711-160">Элемент</span><span class="sxs-lookup"><span data-stu-id="34711-160">Element</span></span> | <span data-ttu-id="34711-161">Описание</span><span class="sxs-lookup"><span data-stu-id="34711-161">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="34711-162">Задает уникальное имя, которое Maven использует toolook копию параметров безопасности при развертывании вашей tooAzure web app.</span><span class="sxs-lookup"><span data-stu-id="34711-162">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="34711-163">Содержит hello `appId` значение из участника-службы.</span><span class="sxs-lookup"><span data-stu-id="34711-163">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="34711-164">Содержит hello `tenant` значение из участника-службы.</span><span class="sxs-lookup"><span data-stu-id="34711-164">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="34711-165">Содержит hello `password` значение из участника-службы.</span><span class="sxs-lookup"><span data-stu-id="34711-165">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="34711-166">Определяет hello целевой Azure облачной среды, которая представляет `AZURE` в этом примере.</span><span class="sxs-lookup"><span data-stu-id="34711-166">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="34711-167">(Полный список сред доступен в hello [Maven подключаемого модуля для веб-приложения Azure] документации)</span><span class="sxs-lookup"><span data-stu-id="34711-167">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="34711-168">Сохраните и закройте hello *settings.xml* файла.</span><span class="sxs-lookup"><span data-stu-id="34711-168">Save and close hello *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a><span data-ttu-id="34711-169">Сборка Docker на образ контейнера и передать ее реестра tooyour контейнер Azure</span><span class="sxs-lookup"><span data-stu-id="34711-169">Build your Docker container image and push it tooyour Azure container registry</span></span>

1. <span data-ttu-id="34711-170">Перейдите в каталог проекта toohello завершения загрузки Spring приложения, (например) «*C:\SpringBoot\gs-spring-boot-docker\complete*«или»*/users/robert/SpringBoot/gs-spring-boot-docker/complete*») и откройте hello *pom.xml* -файл текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="34711-170">Navigate toohello completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="34711-171">Обновление hello `<properties>` коллекции в hello *pom.xml* файл со значение сервера hello входа для реестра контейнера Azure hello в предыдущем разделе этого учебника; например:</span><span class="sxs-lookup"><span data-stu-id="34711-171">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry from hello previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="34711-172">Описание</span><span class="sxs-lookup"><span data-stu-id="34711-172">Where:</span></span>
   <span data-ttu-id="34711-173">Элемент</span><span class="sxs-lookup"><span data-stu-id="34711-173">Element</span></span> | <span data-ttu-id="34711-174">Описание</span><span class="sxs-lookup"><span data-stu-id="34711-174">Description</span></span>
   ---|---|---
   `<azure.containerRegistry>` | <span data-ttu-id="34711-175">Указывает имя hello реестра закрытый контейнер Azure.</span><span class="sxs-lookup"><span data-stu-id="34711-175">Specifies hello name of your private Azure container registry.</span></span>
   `<docker.image.prefix>` | <span data-ttu-id="34711-176">Указывает URL-адрес hello реестра закрытый контейнер Azure, который является производным путем добавления «. azurecr.io» toohello имя контейнера закрытого реестра.</span><span class="sxs-lookup"><span data-stu-id="34711-176">Specifies hello URL of your private Azure container registry, which is derived by appending ".azurecr.io" toohello name of your private container registry.</span></span>

1. <span data-ttu-id="34711-177">Убедитесь, что `<plugin>` для подключаемого модуля Docker hello в вашей *pom.xml* файл содержит необходимые свойства hello для hello server адрес и реестра имя входа из предыдущего шага hello в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="34711-177">Verify that `<plugin>` for hello Docker plugin in your *pom.xml* file contains hello correct properties for hello login server address and registry name from hello previous step in this tutorial.</span></span> <span data-ttu-id="34711-178">Например:</span><span class="sxs-lookup"><span data-stu-id="34711-178">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   <span data-ttu-id="34711-179">Описание</span><span class="sxs-lookup"><span data-stu-id="34711-179">Where:</span></span>
   <span data-ttu-id="34711-180">Элемент</span><span class="sxs-lookup"><span data-stu-id="34711-180">Element</span></span> | <span data-ttu-id="34711-181">Описание</span><span class="sxs-lookup"><span data-stu-id="34711-181">Description</span></span>
   ---|---|---
   `<serverId>` | <span data-ttu-id="34711-182">Указывает свойство hello, которое содержит имя реестра закрытый контейнер Azure.</span><span class="sxs-lookup"><span data-stu-id="34711-182">Specifies hello property which contains name of your private Azure container registry.</span></span>
   `<registryUrl>` | <span data-ttu-id="34711-183">Указывает свойство hello, которое содержит URL-адрес hello реестра закрытый контейнер Azure.</span><span class="sxs-lookup"><span data-stu-id="34711-183">Specifies hello property which contains hello URL of your private Azure container registry.</span></span>

1. <span data-ttu-id="34711-184">Перейдите в каталог проекта toohello завершения загрузки Spring приложения и запустите следующие команды toorebuild hello приложения hello push tooyour контейнера hello контейнер Azure реестра:</span><span class="sxs-lookup"><span data-stu-id="34711-184">Navigate toohello completed project directory for your Spring Boot application and run hello following command toorebuild hello application and push hello container tooyour Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

1. <span data-ttu-id="34711-185">Необязательно: Обзор toohello [портал Azure] и убедитесь, что образ контейнера Docker с именем **gs spring загрузки docker** в реестре контейнера.</span><span class="sxs-lookup"><span data-stu-id="34711-185">OPTIONAL: Browse toohello [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Проверка контейнера на портале Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a><span data-ttu-id="34711-187">Настройка вашего pom.xml затем построения и развертывания вашего tooAzure контейнера</span><span class="sxs-lookup"><span data-stu-id="34711-187">Customize your pom.xml, then build and deploy your container tooAzure</span></span>

<span data-ttu-id="34711-188">Откройте hello `pom.xml` файл для загрузки Spring приложения в текстовом редакторе, а затем найдите hello `<plugin>` элемент для `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="34711-188">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="34711-189">Этот элемент должен быть похож на следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="34711-189">This element should resemble hello following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
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

<span data-ttu-id="34711-190">Имеется несколько значений, которые можно изменять для подключаемого модуля Maven hello и подробное описание каждого из этих элементов доступен в hello [Maven подключаемого модуля для веб-приложения Azure] документации.</span><span class="sxs-lookup"><span data-stu-id="34711-190">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="34711-191">Существует ряд значений, на которые следует обратить внимание в этой статье.</span><span class="sxs-lookup"><span data-stu-id="34711-191">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="34711-192">Элемент</span><span class="sxs-lookup"><span data-stu-id="34711-192">Element</span></span> | <span data-ttu-id="34711-193">Описание</span><span class="sxs-lookup"><span data-stu-id="34711-193">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="34711-194">Указывает версию hello hello [Maven подключаемого модуля для веб-приложения Azure].</span><span class="sxs-lookup"><span data-stu-id="34711-194">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="34711-195">Необходимо проверить версию hello, перечисленные в hello [Maven центрального репозитория](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure, в которых используется hello последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="34711-195">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="34711-196">Указывает hello сведения для проверки подлинности для Azure, который в данном примере содержит `<serverId>` элемент, содержащий `azure-auth`; Maven использует toolook, значение основного значениями hello службы Azure в вашей Maven *settings.xml* файл, который вы определили в предыдущем разделе этой статьи.</span><span class="sxs-lookup"><span data-stu-id="34711-196">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="34711-197">Указывает hello целевой группы ресурсов, который является `wingtiptoysresources` в этом примере.</span><span class="sxs-lookup"><span data-stu-id="34711-197">Specifies hello target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="34711-198">будет создана группа ресурсов Hello во время развертывания, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="34711-198">hello resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="34711-199">Указывает имя целевой hello для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="34711-199">Specifies hello target name for your web app.</span></span> <span data-ttu-id="34711-200">В этом примере — имя целевого hello `maven-linux-app-${maven.build.timestamp}`, где hello `${maven.build.timestamp}` в конфликт tooavoid примере добавляется суффикс.</span><span class="sxs-lookup"><span data-stu-id="34711-200">In this example, hello target name is `maven-linux-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="34711-201">(метка времени hello необязателен; можно указать любую уникальную строку для имени приложения hello).</span><span class="sxs-lookup"><span data-stu-id="34711-201">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="34711-202">Указывает hello целевой области, которая в данном примере `westus`.</span><span class="sxs-lookup"><span data-stu-id="34711-202">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="34711-203">(Полный список находится в hello [Maven подключаемого модуля для веб-приложения Azure] документации.)</span><span class="sxs-lookup"><span data-stu-id="34711-203">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<containerSettings>` | <span data-ttu-id="34711-204">Указывает свойства hello, содержащих имя hello и URL-адрес контейнера.</span><span class="sxs-lookup"><span data-stu-id="34711-204">Specifies hello properties which contain hello name and URL of your container.</span></span>
`<appSettings>` | <span data-ttu-id="34711-205">Определяет все уникальные настройки для Maven toouse при развертывании вашей tooAzure web app.</span><span class="sxs-lookup"><span data-stu-id="34711-205">Specifies any unique settings for Maven toouse when deploying your web app tooAzure.</span></span> <span data-ttu-id="34711-206">В этом примере `<property>` элемент содержит дочерние элементы, укажите порт приложения hello пары имя/значение.</span><span class="sxs-lookup"><span data-stu-id="34711-206">In this example, a `<property>` element contains a name/value pair of child elements that specify hello port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="34711-207">номер порта hello toochange параметры Hello в этом примере необходимы только при изменении порта hello относительно значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="34711-207">hello settings toochange hello port number in this example are only necessary when you are changing hello port from hello default.</span></span>
>

1. <span data-ttu-id="34711-208">Из командной строки hello или окно терминала, который использовался ранее, перестройте hello JAR-файл с помощью Maven при внесении любого изменения toohello *pom.xml* файла; например:</span><span class="sxs-lookup"><span data-stu-id="34711-208">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="34711-209">Развертывание вашей tooAzure web app с помощью Maven; Например:</span><span class="sxs-lookup"><span data-stu-id="34711-209">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="34711-210">Maven развернет ваш веб tooAzure приложения; Если веб-приложение hello еще не существует, он будет создан.</span><span class="sxs-lookup"><span data-stu-id="34711-210">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="34711-211">Если область hello, которое задается в hello `<region>` элемент вашей *pom.xml* файла не имеет достаточного количества доступных серверов при запуске развертывания, может появиться ошибка примерно toohello, в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="34711-211">If hello region which you specify in hello `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar toohello following example:</span></span>
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
> <span data-ttu-id="34711-212">В этом случае можно указать, что другой регион и повторно запустите hello toodeploy команда Maven приложения.</span><span class="sxs-lookup"><span data-stu-id="34711-212">If this happens, you can specify another region and re-run hello Maven command toodeploy your application.</span></span>
>
>

<span data-ttu-id="34711-213">При развертывании веб-узла можно будет toomanage его с помощью hello [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="34711-213">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="34711-214">Веб-приложение будет указано в разделе **Службы приложений**:</span><span class="sxs-lookup"><span data-stu-id="34711-214">Your web app will be listed in **App Services**:</span></span>

   ![Веб-приложение в разделе "Службы приложений" на портале Azure][AP01]

* <span data-ttu-id="34711-216">И hello URL-адрес для веб-приложения будут указаны в hello **Обзор** веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="34711-216">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

   ![Определение hello URL-адрес для веб-приложения][AP02]

## <a name="next-steps"></a><span data-ttu-id="34711-218">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="34711-218">Next steps</span></span>

<span data-ttu-id="34711-219">Дополнительные сведения о hello различные технологии, описанные в этой статье, см. следующие статьи hello:</span><span class="sxs-lookup"><span data-stu-id="34711-219">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="34711-220">[Maven подключаемого модуля для веб-приложения Azure]</span><span class="sxs-lookup"><span data-stu-id="34711-220">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="34711-221">Войдите в tooAzure из hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="34711-221">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="34711-222">Создание субъекта-службы Azure с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="34711-222">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="34711-223">Справочник по параметрам Maven</span><span class="sxs-lookup"><span data-stu-id="34711-223">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="34711-224">[Подключаемый модуль Docker для Maven]</span><span class="sxs-lookup"><span data-stu-id="34711-224">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Azure интерфейс командной строки (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[портал Azure]: https://portal.azure.com/
[Maven подключаемого модуля для веб-приложения Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Подключаемый модуль Docker для Maven]: https://github.com/spotify/docker-maven-plugin
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[загрузки Spring]: http://projects.spring.io/spring-boot/
[загрузки Spring по началу работы Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
