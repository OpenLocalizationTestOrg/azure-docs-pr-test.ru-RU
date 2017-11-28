---
title: "aaaDeploy приложении Spring загрузки на Kubernetes в службе контейнера Azure | Документы Microsoft"
description: "Этот учебник поможет вам хотя toodeploy действия hello приложение загрузки Spring Kubernetes кластера в Microsoft Azure."
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
ms.openlocfilehash: 2bf9df459f874a1f478f43cdd29992d86c370837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-hello-azure-container-service"></a><span data-ttu-id="c275b-103">Развертывание приложения загрузки Spring в кластере Kubernetes в hello контейнера службы Azure</span><span class="sxs-lookup"><span data-stu-id="c275b-103">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>

<span data-ttu-id="c275b-104">Hello  **[Spring Framework]**  — это популярный открытая платформа Java разработчики могут создать web, мобильных устройств и приложения API.</span><span class="sxs-lookup"><span data-stu-id="c275b-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="c275b-105">В этом учебнике используется образец приложения, созданного с использованием [загрузки Spring], управляемых соглашение случай использования Spring tooget быстро начать работу.</span><span class="sxs-lookup"><span data-stu-id="c275b-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="c275b-106">**[Kubernetes]**  и  **[Docker]**  открытая решений, помогающих разработчикам автоматизировать развертывания hello, масштабирования и управления приложениями под управлением в контейнерах.</span><span class="sxs-lookup"><span data-stu-id="c275b-106">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate hello deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="c275b-107">Этот учебник поможет на то, что объединение toodevelop эти две технологии популярных, открытым исходным кодом и развертывание tooMicrosoft приложения загрузки Spring Azure.</span><span class="sxs-lookup"><span data-stu-id="c275b-107">This tutorial walks you though combining these two popular, open-source technologies toodevelop and deploy a Spring Boot application tooMicrosoft Azure.</span></span> <span data-ttu-id="c275b-108">В частности, использовать  *[загрузки Spring]*  для разработки приложений,  *[Kubernetes]*  для развертывания контейнера и hello [Контейнера службы azure (ACS)] toohost приложения.</span><span class="sxs-lookup"><span data-stu-id="c275b-108">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and hello [Azure Container Service (ACS)] toohost your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c275b-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c275b-109">Prerequisites</span></span>

* <span data-ttu-id="c275b-110">Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="c275b-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="c275b-111">Hello [Azure интерфейс командной строки (CLI)].</span><span class="sxs-lookup"><span data-stu-id="c275b-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="c275b-112">Актуальная версия [Java Developer Kit (JDK)].</span><span class="sxs-lookup"><span data-stu-id="c275b-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="c275b-113">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="c275b-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="c275b-114">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="c275b-114">A [Git] client.</span></span>
* <span data-ttu-id="c275b-115">Клиент [Docker].</span><span class="sxs-lookup"><span data-stu-id="c275b-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c275b-116">Из-за требований к виртуализации toohello этого учебника не может следовать за hello действия, описанные в этой статье на виртуальной машине; необходимо использовать физический компьютер с включенными возможностями виртуализации.</span><span class="sxs-lookup"><span data-stu-id="c275b-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="c275b-117">Создать hello Spring загрузки на веб-приложение Docker начало работы</span><span class="sxs-lookup"><span data-stu-id="c275b-117">Create hello Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="c275b-118">Hello следующие шаги содержат пошаговые инструкции для построения Spring загрузки веб-приложения и локального тестирования.</span><span class="sxs-lookup"><span data-stu-id="c275b-118">hello following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="c275b-119">Откройте командную строку и создать toohold локальный каталог, приложение и перейдите в каталог toothat; Например:</span><span class="sxs-lookup"><span data-stu-id="c275b-119">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="c275b-120">-- или --</span><span class="sxs-lookup"><span data-stu-id="c275b-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="c275b-121">Клон hello [загрузки Spring по началу работы Docker] образец проекта в каталог hello.</span><span class="sxs-lookup"><span data-stu-id="c275b-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="c275b-122">Изменение каталога toohello завершения проекта.</span><span class="sxs-lookup"><span data-stu-id="c275b-122">Change directory toohello completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="c275b-123">Используйте Maven toobuild и пример приложения hello выполнения.</span><span class="sxs-lookup"><span data-stu-id="c275b-123">Use Maven toobuild and run hello sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="c275b-124">Веб-приложения hello теста путем просмотра toohttp://localhost:8080 или hello следующий `curl` команды:</span><span class="sxs-lookup"><span data-stu-id="c275b-124">Test hello web app by browsing toohttp://localhost:8080, or with hello following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="c275b-125">Должно появиться сообщение, отображаемое после hello: **Docker Здравствуй, мир!**</span><span class="sxs-lookup"><span data-stu-id="c275b-125">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![Локальный просмотр образца приложения][SB01]

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="c275b-127">Создайте в реестре контейнера Azure с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c275b-127">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="c275b-128">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="c275b-128">Open a command prompt.</span></span>

1. <span data-ttu-id="c275b-129">Вход tooyour учетная запись Azure:</span><span class="sxs-lookup"><span data-stu-id="c275b-129">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="c275b-130">Создание группы ресурсов для hello Azure ресурсы, используемые в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="c275b-130">Create a resource group for hello Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="c275b-131">Создание реестра закрытый контейнер Azure в группе ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="c275b-131">Create a private Azure container registry in hello resource group.</span></span> <span data-ttu-id="c275b-132">Пример приложения hello помещает учебника Hello как реестра toothis образа Docker на последующих этапах.</span><span class="sxs-lookup"><span data-stu-id="c275b-132">hello tutorial pushes hello sample app as a Docker image toothis registry in later steps.</span></span> <span data-ttu-id="c275b-133">Замените `wingtiptoysregistry` уникальным именем для реестра.</span><span class="sxs-lookup"><span data-stu-id="c275b-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-toohello-container-registry"></a><span data-ttu-id="c275b-134">Принудительная реестр контейнера toohello приложения</span><span class="sxs-lookup"><span data-stu-id="c275b-134">Push your app toohello container registry</span></span>

1. <span data-ttu-id="c275b-135">Перейдите в каталог toohello конфигурации для установки Maven (по умолчанию ~/.m2/ или C:\Users\username\.m2) и откройте hello *settings.xml* файл в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="c275b-135">Navigate toohello configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open hello *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="c275b-136">Получить пароль hello для контейнера реестра из hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c275b-136">Retrieve hello password for your container registry from hello Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="c275b-137">Добавить ваш реестра контейнера Azure идентификатора и пароля tooa новый `<server>` коллекции в hello *settings.xml* файла.</span><span class="sxs-lookup"><span data-stu-id="c275b-137">Add your Azure Container Registry id and password tooa new `<server>` collection in hello *settings.xml* file.</span></span>
<span data-ttu-id="c275b-138">Hello `id` и `username` являются hello имя реестра hello.</span><span class="sxs-lookup"><span data-stu-id="c275b-138">hello `id` and `username` are hello name of hello registry.</span></span> <span data-ttu-id="c275b-139">Используйте hello `password` значение из предыдущей команды hello (без кавычек).</span><span class="sxs-lookup"><span data-stu-id="c275b-139">Use hello `password` value from hello previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="c275b-140">Перейдите в каталог проекта toohello завершения загрузки Spring приложения (например, «*C:\SpringBoot\gs-spring-boot-docker\complete*«или»*/users/robert/SpringBoot/gs-spring-boot-docker / Полный*») и откройте hello *pom.xml* файл в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="c275b-140">Navigate toohello completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="c275b-141">Обновление hello `<properties>` коллекции в hello *pom.xml* файл со значение сервера hello входа для реестра контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="c275b-141">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="c275b-142">Обновление hello `<plugins>` коллекции в hello *pom.xml* файл, который hello `<plugin>` содержит hello server адрес и реестра имя входа для реестра контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="c275b-142">Update hello `<plugins>` collection in hello *pom.xml* file so that hello `<plugin>` contains hello login server address and registry name for your Azure Container Registry.</span></span>

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

1. <span data-ttu-id="c275b-143">Перейдите в каталог проекта toohello завершения загрузки Spring приложения и выполните hello, следующая команда toobuild hello Docker контейнера и принудительной hello изображения toohello реестра:</span><span class="sxs-lookup"><span data-stu-id="c275b-143">Navigate toohello completed project directory for your Spring Boot application and run hello following command toobuild hello Docker container and push hello image toohello registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="c275b-144">Может появиться сообщение об ошибке, аналогичные tooone следующие hello при Maven помещает hello tooAzure изображения:</span><span class="sxs-lookup"><span data-stu-id="c275b-144">You may receive an error message that is similar tooone of hello following when Maven pushes hello image tooAzure:</span></span>
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="c275b-145">Если возникли ошибки, вход tooAzure из командной строки Docker hello.</span><span class="sxs-lookup"><span data-stu-id="c275b-145">If you get this error, log in tooAzure from hello Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="c275b-146">Затем принудительно отправьте контейнер:</span><span class="sxs-lookup"><span data-stu-id="c275b-146">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-hello-azure-cli"></a><span data-ttu-id="c275b-147">Создание кластера Kubernetes на службы ACS с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c275b-147">Create a Kubernetes Cluster on ACS using hello Azure CLI</span></span>

1. <span data-ttu-id="c275b-148">Создайте кластер Kubernetes в службе контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="c275b-148">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="c275b-149">Hello следующая команда создает *kubernetes* кластера в hello *wingtiptoys kubernetes* ресурсов группы с *wingtiptoys containerservice* как кластер hello имя, и *wingtiptoys kubernetes* как префикс DNS hello:</span><span class="sxs-lookup"><span data-stu-id="c275b-149">hello following command creates a *kubernetes* cluster in hello *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as hello cluster name, and *wingtiptoys-kubernetes* as hello DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="c275b-150">Эта команда может занять некоторое время toocomplete.</span><span class="sxs-lookup"><span data-stu-id="c275b-150">This command may take a while toocomplete.</span></span>

1. <span data-ttu-id="c275b-151">Установить `kubectl` с помощью Azure CLI "hello".</span><span class="sxs-lookup"><span data-stu-id="c275b-151">Install `kubectl` using hello Azure CLI.</span></span> <span data-ttu-id="c275b-152">Пользователи Linux, возможно, tooprefix к этой команде `sudo` с момента развертывает hello Kubernetes CLI слишком`/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="c275b-152">Linux users may have tooprefix this command with `sudo` since it deploys hello Kubernetes CLI too`/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="c275b-153">Загрузка сведений о конфигурации кластера hello кластера можно управлять из веб-интерфейса Kubernetes hello и `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="c275b-153">Download hello cluster configuration information so you can manage your cluster from hello Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-hello-image-tooyour-kubernetes-cluster"></a><span data-ttu-id="c275b-154">Развертывание кластера Kubernetes tooyour изображение hello</span><span class="sxs-lookup"><span data-stu-id="c275b-154">Deploy hello image tooyour Kubernetes cluster</span></span>

<span data-ttu-id="c275b-155">Этот учебник развертывает приложения hello с использованием `kubectl`, подождите, пока вы tooexplore hello развертывания hello Kubernetes веб-интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="c275b-155">This tutorial deploys hello app using `kubectl`, then allow you tooexplore hello deployment through hello Kubernetes web interface.</span></span>

### <a name="deploy-with-hello-kubernetes-web-interface"></a><span data-ttu-id="c275b-156">Развертывание веб-интерфейсе Kubernetes hello</span><span class="sxs-lookup"><span data-stu-id="c275b-156">Deploy with hello Kubernetes web interface</span></span>

1. <span data-ttu-id="c275b-157">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="c275b-157">Open a command prompt.</span></span>

1. <span data-ttu-id="c275b-158">Откройте веб-сайт конфигурации hello для кластера Kubernetes в браузере по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="c275b-158">Open hello configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="c275b-159">Когда веб-сайт конфигурации Kubernetes hello откроется в браузере, щелкните ссылку hello слишком**развертывание контейнерного приложения**:</span><span class="sxs-lookup"><span data-stu-id="c275b-159">When hello Kubernetes configuration website opens in your browser, click hello link too**deploy a containerized app**:</span></span>

   ![Веб-сайт конфигурации Kubernetes][KB01]

1. <span data-ttu-id="c275b-161">Здравствуйте, когда **развертывание контейнерного приложения** отображается страница, укажите hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="c275b-161">When hello **Deploy a containerized app** page is displayed, specify hello following options:</span></span>

   <span data-ttu-id="c275b-162">а.</span><span class="sxs-lookup"><span data-stu-id="c275b-162">a.</span></span> <span data-ttu-id="c275b-163">Выберите **Specify app details below** (Указать сведения о приложении ниже).</span><span class="sxs-lookup"><span data-stu-id="c275b-163">Select **Specify app details below**.</span></span>

   <span data-ttu-id="c275b-164">b.</span><span class="sxs-lookup"><span data-stu-id="c275b-164">b.</span></span> <span data-ttu-id="c275b-165">Введите имя приложения Spring загрузки для hello **имя приложения**, например: «*gs spring загрузки docker*».</span><span class="sxs-lookup"><span data-stu-id="c275b-165">Enter your Spring Boot application name for hello **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="c275b-166">c.</span><span class="sxs-lookup"><span data-stu-id="c275b-166">c.</span></span> <span data-ttu-id="c275b-167">Введите имя входа образа сервера и контейнера из более ранних версий для hello **образ контейнера**, например: «*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*».</span><span class="sxs-lookup"><span data-stu-id="c275b-167">Enter your login server and container image from earlier for hello **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="c275b-168">d.</span><span class="sxs-lookup"><span data-stu-id="c275b-168">d.</span></span> <span data-ttu-id="c275b-169">Выберите **внешних** для hello **службы**.</span><span class="sxs-lookup"><span data-stu-id="c275b-169">Choose **External** for hello **Service**.</span></span>

   <span data-ttu-id="c275b-170">д.</span><span class="sxs-lookup"><span data-stu-id="c275b-170">e.</span></span> <span data-ttu-id="c275b-171">Указать на внешние и внутренние порты hello **порт** и **целевой порт** текстовые поля.</span><span class="sxs-lookup"><span data-stu-id="c275b-171">Specify your external and internal ports in hello **Port** and **Target port** text boxes.</span></span>

   ![Веб-сайт конфигурации Kubernetes][KB02]


1. <span data-ttu-id="c275b-173">Нажмите кнопку **развернуть** toodeploy hello контейнера.</span><span class="sxs-lookup"><span data-stu-id="c275b-173">Click **Deploy** toodeploy hello container.</span></span>

   ![Развертывание контейнера][KB05]

1. <span data-ttu-id="c275b-175">После развертывания приложение Spring Boot отобразится в списке **Службы**.</span><span class="sxs-lookup"><span data-stu-id="c275b-175">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Службы Kubernetes][KB06]

1. <span data-ttu-id="c275b-177">Если щелкнуть ссылку hello для **внешние конечные точки**, вы увидите Spring загрузки приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="c275b-177">If you click hello link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Службы Kubernetes][KB07]

   ![Просмотр примера приложения в Azure][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="c275b-180">Развертывание с помощью kubectl</span><span class="sxs-lookup"><span data-stu-id="c275b-180">Deploy with kubectl</span></span>

1. <span data-ttu-id="c275b-181">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="c275b-181">Open a command prompt.</span></span>

1. <span data-ttu-id="c275b-182">Запустите контейнер в кластере Kubernetes hello с помощью hello `kubectl run` команды.</span><span class="sxs-lookup"><span data-stu-id="c275b-182">Run your container in hello Kubernetes cluster by using hello `kubectl run` command.</span></span> <span data-ttu-id="c275b-183">Присвойте имя службы для приложения в Kubernetes и hello имя полного образа.</span><span class="sxs-lookup"><span data-stu-id="c275b-183">Give a service name for your app in Kubernetes and hello full image name.</span></span> <span data-ttu-id="c275b-184">Например:</span><span class="sxs-lookup"><span data-stu-id="c275b-184">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="c275b-185">В этой команде:</span><span class="sxs-lookup"><span data-stu-id="c275b-185">In this command:</span></span>

   * <span data-ttu-id="c275b-186">Имя контейнера Hello `gs-spring-boot-docker` указывается сразу после hello `run` команды</span><span class="sxs-lookup"><span data-stu-id="c275b-186">hello container name `gs-spring-boot-docker` is specified immediately after hello `run` command</span></span>

   * <span data-ttu-id="c275b-187">Hello `--image` указывает hello вместе серверу входа в систему и имя образа, как`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="c275b-187">hello `--image` parameter specifies hello combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="c275b-188">Предоставлять кластера Kubernetes извне с помощью hello `kubectl expose` команды.</span><span class="sxs-lookup"><span data-stu-id="c275b-188">Expose your Kubernetes cluster externally by using hello `kubectl expose` command.</span></span> <span data-ttu-id="c275b-189">Укажите имя службы, hello приложение общедоступный TCP порт, используемый tooaccess hello и hello внутренней целевой порт, который прослушивается приложения.</span><span class="sxs-lookup"><span data-stu-id="c275b-189">Specify your service name, hello public-facing TCP port used tooaccess hello app, and hello internal target port your app listens on.</span></span> <span data-ttu-id="c275b-190">Например:</span><span class="sxs-lookup"><span data-stu-id="c275b-190">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="c275b-191">В этой команде:</span><span class="sxs-lookup"><span data-stu-id="c275b-191">In this command:</span></span>

   * <span data-ttu-id="c275b-192">Имя контейнера Hello `gs-spring-boot-docker` указывается сразу после hello `expose deployment` команды</span><span class="sxs-lookup"><span data-stu-id="c275b-192">hello container name `gs-spring-boot-docker` is specified immediately after hello `expose deployment` command</span></span>

   * <span data-ttu-id="c275b-193">Hello `--type` параметр указывает, hello кластер использует подсистему балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="c275b-193">hello `--type` parameter specifies that hello cluster uses load balancer</span></span>

   * <span data-ttu-id="c275b-194">Hello `--port` указывает hello общедоступный TCP-порт 80.</span><span class="sxs-lookup"><span data-stu-id="c275b-194">hello `--port` parameter specifies hello public-facing TCP port of 80.</span></span> <span data-ttu-id="c275b-195">Доступ к приложение hello через этот порт.</span><span class="sxs-lookup"><span data-stu-id="c275b-195">You access hello app on this port.</span></span>

   * <span data-ttu-id="c275b-196">Hello `--target-port` указывает hello внутренней TCP-порт 8080.</span><span class="sxs-lookup"><span data-stu-id="c275b-196">hello `--target-port` parameter specifies hello internal TCP port of 8080.</span></span> <span data-ttu-id="c275b-197">Подсистема балансировки нагрузки Hello пересылает приложения tooyour запросы через этот порт.</span><span class="sxs-lookup"><span data-stu-id="c275b-197">hello load balancer forwards requests tooyour app on this port.</span></span>

1. <span data-ttu-id="c275b-198">После развертывания приложение hello кластера toohello hello внешний IP-адрес запроса и открыть его в веб-браузере:</span><span class="sxs-lookup"><span data-stu-id="c275b-198">Once hello app is deployed toohello cluster, query hello external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Просмотр примера приложения в Azure][SB02]


## <a name="next-steps"></a><span data-ttu-id="c275b-200">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c275b-200">Next steps</span></span>

<span data-ttu-id="c275b-201">Дополнительные сведения об использовании Spring загрузки в Azure см. следующие статьи hello:</span><span class="sxs-lookup"><span data-stu-id="c275b-201">For more information about using Spring Boot on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="c275b-202">Развертывание приложения загрузки Spring toohello службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="c275b-202">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="c275b-203">Развертывание приложения загрузки Spring в Linux в hello контейнера службы Azure</span><span class="sxs-lookup"><span data-stu-id="c275b-203">Deploy a Spring Boot application on Linux in hello Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-linux.md)

<span data-ttu-id="c275b-204">Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure] и hello [Java средств для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="c275b-204">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="c275b-205">Дополнительные сведения о hello Spring загрузки Docker образец проекта в разделе [загрузки Spring по началу работы Docker].</span><span class="sxs-lookup"><span data-stu-id="c275b-205">For more information about hello Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="c275b-206">Hello следующие ссылки предоставляют дополнительные сведения о создании приложений Spring загрузки.</span><span class="sxs-lookup"><span data-stu-id="c275b-206">hello following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="c275b-207">Дополнительные сведения о создании простого приложения загрузки Spring hello Spring Initializr на https://start.spring.io/ см.</span><span class="sxs-lookup"><span data-stu-id="c275b-207">For more information about creating a simple Spring Boot application, see hello Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="c275b-208">Hello следующие ссылки предоставляют дополнительные сведения об использовании Kubernetes с Azure:</span><span class="sxs-lookup"><span data-stu-id="c275b-208">hello following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="c275b-209">Развертывание кластера Kubernetes для контейнеров Linux</span><span class="sxs-lookup"><span data-stu-id="c275b-209">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="c275b-210">С помощью hello Kubernetes веб-интерфейсом пользователя с помощью контейнера службы Azure</span><span class="sxs-lookup"><span data-stu-id="c275b-210">Using hello Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="c275b-211">Дополнительные сведения об использовании интерфейса командной строки Kubernetes доступен в hello **kubectl** руководство пользователя по <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="c275b-211">More information about using Kubernetes command-line interface is available in hello **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="c275b-212">веб-сайт Kubernetes Hello имеет несколько статей, в которых рассматривается использование изображений в частных реестрах:</span><span class="sxs-lookup"><span data-stu-id="c275b-212">hello Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="c275b-213">[Configure Service Accounts for Pods] (Настройка учетных записей службы для модулей Pod)</span><span class="sxs-lookup"><span data-stu-id="c275b-213">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="c275b-214">[Namespaces] (Пространства имен)</span><span class="sxs-lookup"><span data-stu-id="c275b-214">[Namespaces]</span></span>
* <span data-ttu-id="c275b-215">[Pull an Image from a Private Registry] (Извлечение образа из частного реестра)</span><span class="sxs-lookup"><span data-stu-id="c275b-215">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="c275b-216">Дополнительные примеры по как toouse Docker пользовательских образов с помощью Azure в разделе [с помощью пользовательского образа Docker для веб-приложения Azure в Linux].</span><span class="sxs-lookup"><span data-stu-id="c275b-216">For additional examples for how toouse custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure интерфейс командной строки (CLI)]: /cli/azure/overview
[Контейнера службы azure (ACS)]: https://azure.microsoft.com/services/container-service/
[центра разработчиков Java Azure]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[с помощью пользовательского образа Docker для веб-приложения Azure в Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java средств для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[загрузки Spring]: http://projects.spring.io/spring-boot/
[загрузки Spring по началу работы Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Configure Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/ (Настройка учетных записей службы для модулей Pod)
[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/ (Пространства имен)
[Pull an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ (Извлечение образа из частного реестра)

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR04.png

[KB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB01.png
[KB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB02.png
[KB03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB03.png
[KB04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB04.png
[KB05]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB05.png
[KB06]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB06.png
[KB07]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB07.png
