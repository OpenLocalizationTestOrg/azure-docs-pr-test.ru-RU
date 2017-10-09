---
title: "Здравствуйте, aaaPublish контейнер Docker с помощью средств Azure для Eclipse | Документы Microsoft"
description: "Узнайте, как toopublish tooMicrosoft приложения web Azure в качестве контейнера Docker с помощью hello средств Azure для Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 53ec3a7f7a171691024e03622fd48d6f1e257b50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="dc0fd-103">Публикация веб-приложения как контейнер Docker с помощью hello набора средств Azure для Eclipse</span><span class="sxs-lookup"><span data-stu-id="dc0fd-103">Publish a web app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="dc0fd-104">Контейнеры Docker широко используются при развертывании веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="dc0fd-105">При использовании контейнеров Docker разработчиков можно объединить все файлы проекта и зависимости в один пакет для развертывания сервера tooa.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="dc0fd-106">Hello средств Azure для Eclipse, добавив упрощает этот процесс для разработчиков Java *опубликовать как контейнер Docker* компоненты для развертывания tooMicrosoft Azure.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-106">hello Azure Toolkit for Eclipse simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="dc0fd-107">В этой статье описывается toopublish необходимые шаги hello tooAzure вашего приложения как контейнеры Docker.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
> <span data-ttu-id="dc0fd-108">Дополнительные сведения о Docker доступен на hello [веб-узел Docker].</span><span class="sxs-lookup"><span data-stu-id="dc0fd-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="dc0fd-109">Публикация вашего tooAzure web app с помощью контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="dc0fd-109">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="dc0fd-110">Откройте проект веб-приложения в Eclipse.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-110">Open your web app project in Eclipse.</span></span>

2. <span data-ttu-id="dc0fd-111">toostart hello **опубликовать как контейнер Docker** мастер, выполните одно из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="dc0fd-111">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="dc0fd-112">В hello **Навигатор** , щелкните правой кнопкой мыши проект, щелкните **Azure**, а затем нажмите кнопку **опубликовать как контейнер Docker**.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-112">In hello **Navigator** view, right-click your project, click **Azure**, and then click **Publish as Docker Container**.</span></span>

      ![Представление навигатора, команда публикации в виде контейнера Docker][PUB01]

   * <span data-ttu-id="dc0fd-114">На панели инструментов Eclipse hello, нажмите кнопку hello **публикации** , а затем нажмите **опубликовать как контейнер Docker**.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-114">On hello Eclipse toolbar, click hello **Publish** button, and then click **Publish as Docker Container**.</span></span>

      ![Панель инструментов Eclipse, команда публикации в виде контейнера Docker][PUB02]
      
    <span data-ttu-id="dc0fd-116">Hello **развертывания контейнера Docker в Azure** откроется мастер.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-116">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

    ![Развертывание контейнера Docker в Azure мастер Hello][PUB03]

3. <span data-ttu-id="dc0fd-118">В hello **введите имя образа, выберите путь артефакта hello и проверьте toobe узла Docker используется** окне hello следующие:</span><span class="sxs-lookup"><span data-stu-id="dc0fd-118">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span>

    <span data-ttu-id="dc0fd-119">а.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-119">a.</span></span> <span data-ttu-id="dc0fd-120">В hello **имя образа Docker** введите уникальное имя для узла Docker.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-120">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="dc0fd-121">(hello мастер автоматически создает имя, но ее можно изменить).</span><span class="sxs-lookup"><span data-stu-id="dc0fd-121">(hello wizard automatically creates a name, but you can modify it.)</span></span>

    <span data-ttu-id="dc0fd-122">b.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-122">b.</span></span> <span data-ttu-id="dc0fd-123">Hello **узлов** области отображаются узлы Docker, уже создан.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-123">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="dc0fd-124">Выполните одно из следующих hello.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-124">Do either of hello following:</span></span>

    * <span data-ttu-id="dc0fd-125">Если у вас есть существующий узел Docker, можно развернуть вашей tooit web app.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-125">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
    * <span data-ttu-id="dc0fd-126">Щелкните новый узел Docker, toocreate **добавить**.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-126">toocreate a new Docker host, click **Add**.</span></span>  
      
    <span data-ttu-id="dc0fd-127">Hello **создать узел Docker** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-127">hello **Create Docker Host** dialog box opens.</span></span>

    ![Мастер развертывания контейнера Docker в Azure][PUB04a]

4. <span data-ttu-id="dc0fd-129">В hello **настроить новую виртуальную машину hello** окне укажите следующие параметры для узла Docker hello.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-129">In hello **Configure hello new virtual machine** window, specify hello following options for your Docker host.</span></span> <span data-ttu-id="dc0fd-130">(hello мастер автоматически создает большую часть параметров hello, но вы можете изменить любые из них).</span><span class="sxs-lookup"><span data-stu-id="dc0fd-130">(hello wizard automatically generates most of hello options for you, but you can modify any of them.)</span></span>

   <span data-ttu-id="dc0fd-131">а.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-131">a.</span></span> <span data-ttu-id="dc0fd-132">**Имя**: Введите уникальное имя для узла Docker hello.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-132">**Name**: Enter a unique name for hello Docker host.</span></span> <span data-ttu-id="dc0fd-133">(Это не так же, как имя образа Docker, указанный ранее hello hello.)</span><span class="sxs-lookup"><span data-stu-id="dc0fd-133">(It is not hello same as hello Docker image name that you specified earlier.)</span></span>

   <span data-ttu-id="dc0fd-134">b.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-134">b.</span></span> <span data-ttu-id="dc0fd-135">**Подписки**: Введите hello подписки Azure, которая используется для узла.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-135">**Subscription**: Enter hello Azure subscription that you use for your host.</span></span>

   <span data-ttu-id="dc0fd-136">c.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-136">c.</span></span> <span data-ttu-id="dc0fd-137">**Область**: hello географический регион, где находится на узле, введите.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-137">**Region**: Enter hello geographical region where your host is located.</span></span>

   <span data-ttu-id="dc0fd-138">d.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-138">d.</span></span> <span data-ttu-id="dc0fd-139">На hello **узла и размер** вкладки:</span><span class="sxs-lookup"><span data-stu-id="dc0fd-139">On hello **Host OS and Size** tab:</span></span>
     * <span data-ttu-id="dc0fd-140">**Системы узла**: Введите hello операционной системы для виртуальной машины hello, содержащий вашего узла.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-140">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span>
     * <span data-ttu-id="dc0fd-141">**Размер**: Введите размер hello виртуальной машины для узла.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-141">**Size**: Enter hello virtual-machine size for your host.</span></span>

   <span data-ttu-id="dc0fd-142">д.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-142">e.</span></span> <span data-ttu-id="dc0fd-143">На hello **группы ресурсов** вкладки:</span><span class="sxs-lookup"><span data-stu-id="dc0fd-143">On hello **Resource Group** tab:</span></span>
     * <span data-ttu-id="dc0fd-144">**Новая группа ресурсов**. Создайте группу ресурсов для узла.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-144">**New resource group**: Create a new resource group for your host.</span></span>
     * <span data-ttu-id="dc0fd-145">**Существующая группа ресурсов**. Укажите имеющуюся группу ресурсов из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-145">**Existing resource group**: Enter an existing resource group from your Azure account.</span></span>

   <span data-ttu-id="dc0fd-146">f.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-146">f.</span></span> <span data-ttu-id="dc0fd-147">На hello **сети** вкладки:</span><span class="sxs-lookup"><span data-stu-id="dc0fd-147">On hello **Network** tab:</span></span>
     * <span data-ttu-id="dc0fd-148">**New virtual network** (Новая виртуальная сеть). Создайте виртуальную сеть для узла.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-148">**New virtual network**: Create a new virtual network for your host.</span></span>
     * <span data-ttu-id="dc0fd-149">**Existing virtual network** (Имеющаяся виртуальная сеть). Укажите имеющуюся виртуальную сеть из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-149">**Existing virtual network**: Enter an existing virtual network from your Azure account.</span></span>

   <span data-ttu-id="dc0fd-150">ж.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-150">g.</span></span> <span data-ttu-id="dc0fd-151">На hello **хранения** вкладки:</span><span class="sxs-lookup"><span data-stu-id="dc0fd-151">On hello **Storage** tab:</span></span>
     * <span data-ttu-id="dc0fd-152">**Создать учетную запись хранения**. Создайте учетную запись хранения для узла.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-152">**New storage account**: Create a new storage account for your host.</span></span>
     * <span data-ttu-id="dc0fd-153">**Existing storage account** (Имеющаяся учетная запись хранения). Укажите имеющуюся учетную запись хранения из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-153">**Existing storage account**: Enter an existing storage account from your Azure account.</span></span>

5. <span data-ttu-id="dc0fd-154">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-154">Click **Next**.</span></span>

6. <span data-ttu-id="dc0fd-155">В hello **настроить журнал учетные данные и параметры порта** окно, выберите один из следующих вариантов hello:</span><span class="sxs-lookup"><span data-stu-id="dc0fd-155">In hello **Configure log in credentials and port settings** window, select one of hello following options:</span></span>

    * <span data-ttu-id="dc0fd-156">**Import credentials from Azure Key Vault** (Импортировать учетные данные из Azure Key Vault). Укажите сохраненный ранее набор учетных данных, хранящихся в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-156">**Import credentials from Azure Key Vault**: Specifies a previously saved set of credentials that are stored in your Azure subscription.</span></span>

      >[!NOTE]
      ><span data-ttu-id="dc0fd-157">Хранилище ключей Azure, созданная с определенной учетной записи или субъекта-службы автоматически недоступна по другой учетной записи или субъекта-службы, использующего hello подписки.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-157">An Azure Key Vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="dc0fd-158">tooallow другой учетной записи или служба основной toouse Здравствуйте хранилище ключей, необходимо использовать учетную запись Azure портала tooadd hello hello или участника-службы.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-158">tooallow another account or service principal toouse hello Key Vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

    * <span data-ttu-id="dc0fd-159">**New log in credentials** (Новые учетные данные для входа). Создайте набор учетных данных для входа в систему.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-159">**New log in credentials**: Creates a new set of login credentials.</span></span> <span data-ttu-id="dc0fd-160">Если этот флажок установлен, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="dc0fd-160">If you select this option, do hello following:</span></span>
    
      * <span data-ttu-id="dc0fd-161">На hello **учетные данные для виртуальной Машины** выберите один из следующих hello параметров для учетных данных входа в систему виртуальной машины hello узла Docker:</span><span class="sxs-lookup"><span data-stu-id="dc0fd-161">On hello **VM Credentials** tab, choose one of hello following options for hello virtual-machine login credentials of your Docker host:</span></span>

          * <span data-ttu-id="dc0fd-162">**Имя пользователя**: Введите hello пользователя для учетных данных входа в систему виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-162">**Username**: Enter hello username for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="dc0fd-163">**Пароль** и **Подтверждение**: hello пароль для учетных данных входа в систему виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-163">**Password** and **Confirm**: Enter hello password for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="dc0fd-164">**SSH**: Введите параметры hello Secure Shell (SSH) для узла Docker.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-164">**SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="dc0fd-165">Можно выбрать один из следующих вариантов hello:</span><span class="sxs-lookup"><span data-stu-id="dc0fd-165">You can choose from hello following options:</span></span>
            * <span data-ttu-id="dc0fd-166">**None** (Нет): указывает, что виртуальная машина не разрешает SSH-подключения.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-166">**None**: Specifies that your virtual machine will not allow SSH connections.</span></span>
            * <span data-ttu-id="dc0fd-167">**Автоматическое создание**: автоматически создает hello необходимые параметры для подключения по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-167">**Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
            * <span data-ttu-id="dc0fd-168">**Import from directory** (Импорт из каталога). Позволяет указать каталог, содержащий набор ранее сохраненных параметров SSH.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-168">**Import from directory**: Specifies a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="dc0fd-169">Hello каталог должен содержать hello, следующие два файла:</span><span class="sxs-lookup"><span data-stu-id="dc0fd-169">hello directory must contain hello following two files:</span></span>
                * <span data-ttu-id="dc0fd-170">*id_rsa*: содержит hello идентификации RSA для пользователя.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-170">*id_rsa*: Contains hello RSA identification for a user.</span></span>
                * <span data-ttu-id="dc0fd-171">*id_rsa.pub*: содержит открытый ключ RSA hello, который используется для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-171">*id_rsa.pub*: Contains hello RSA public key that is used for authentication.</span></span>
        
        ![Окно Create Docker Host (Создание узла Docker)][PUB05]

      * <span data-ttu-id="dc0fd-173">На hello **учетные данные управляющей программы Docker** укажите hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="dc0fd-173">On hello **Docker Daemon Credentials** tab, specify hello following options:</span></span>

          * <span data-ttu-id="dc0fd-174">**Порт управляющей программы docker**: Введите уникальный порт TCP hello для узла Docker.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-174">**Docker Daemon port**: Enter hello unique TCP port for your Docker host.</span></span>
          * <span data-ttu-id="dc0fd-175">**Безопасность TLS**: Введите hello параметры безопасности транспортного уровня для узла Docker.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-175">**TLS Security**: Enter hello Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="dc0fd-176">Можно выбрать один из следующих вариантов hello:</span><span class="sxs-lookup"><span data-stu-id="dc0fd-176">You can choose from hello following options:</span></span>
            * <span data-ttu-id="dc0fd-177">**None** (Нет): указывает, что виртуальная машина не разрешает TLS-подключения.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-177">**None**: Specifies that your virtual machine will not allow TLS connections.</span></span>
            * <span data-ttu-id="dc0fd-178">**Автоматическое создание**: автоматически создает hello необходимые параметры для подключения через TLS.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-178">**Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.</span></span>
            * <span data-ttu-id="dc0fd-179">**Import from directory** (Импорт из каталога). Позволяет указать каталог, содержащий набор ранее сохраненных параметров TLS.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-179">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="dc0fd-180">В частности hello каталог должен содержать следующие шесть файлы hello:</span><span class="sxs-lookup"><span data-stu-id="dc0fd-180">More specifically, hello directory must contain hello following six files:</span></span>
                * <span data-ttu-id="dc0fd-181">*CA.pem* и *key.pem ЦС*: содержат hello сертификат и открытый ключ для hello TLS центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-181">*ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.</span></span>
                * <span data-ttu-id="dc0fd-182">*CERT.pem* и *key.pem*: содержать hello клиентский сертификат и открытый ключ, используемый для проверки подлинности TLS.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-182">*cert.pem* and *key.pem*: Contain hello client certificate and public key that is used for TLS authentication.</span></span>
                * <span data-ttu-id="dc0fd-183">*Server.pem* и *key.pem сервера*: содержать hello сертификат и открытый ключ для узла hello.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-183">*server.pem* and *server-key.pem*: Contain hello server certificate and public key for hello host.</span></span>

        ![Окно Create Docker Host (Создание узла Docker)][PUB06]

7. <span data-ttu-id="dc0fd-185">После того как введены все предшествующие сведения hello, нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-185">After you have entered all of hello preceding information, click **Finish**.</span></span>

8. <span data-ttu-id="dc0fd-186">В hello **развертывания контейнера Docker в Azure** мастера, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-186">In hello **Deploy Docker Container on Azure** wizard, click **Next**.</span></span>

   ![Развертывание контейнера Docker в Azure мастер Hello][PUB07]

9. <span data-ttu-id="dc0fd-188">В hello **Настройка hello Docker контейнера toobe создан** окне hello следующие:</span><span class="sxs-lookup"><span data-stu-id="dc0fd-188">In hello **Configure hello Docker container toobe created** window, do hello following:</span></span>

   <span data-ttu-id="dc0fd-189">а.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-189">a.</span></span> <span data-ttu-id="dc0fd-190">В hello **имя контейнера Docker** введите уникальное имя для контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-190">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="dc0fd-191">b.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-191">b.</span></span> <span data-ttu-id="dc0fd-192">Выберите один из следующих образов Docker hello.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-192">Choose one of hello following Docker images:</span></span>
     * <span data-ttu-id="dc0fd-193">**Predefined Docker image** (Предопределенный образ Docker). Укажите имеющийся образ Docker из Azure.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-193">**Predefined Docker image**: Specifies a pre-existing Docker image from Azure.</span></span>

       >[!NOTE]
       ><span data-ttu-id="dc0fd-194">Hello список образов Docker в этом поле состоит из нескольких изображений, hello, набор средств Azure был настроен toopatch так, что автоматически развертывается на артефакт.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-194">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span>

     * <span data-ttu-id="dc0fd-195">**Custom Dockerfile** (Пользовательский Dockerfile). Укажите сохраненный ранее Dockerfile на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-195">**Custom Dockerfile**: Specifies a previously saved Dockerfile from your local computer.</span></span>

       >[!NOTE]
       ><span data-ttu-id="dc0fd-196">Это еще одна возможность разработчикам, создающим собственные Dockerfile toodeploy.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-196">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="dc0fd-197">Тем не менее он работает toodevelopers, использующих этот tooensure параметр, правильно ли построено их Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-197">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="dc0fd-198">Hello набора средств Azure не проверяет содержимое hello в пользовательский файл Dockerfile, поэтому hello развертывание может завершиться ошибкой, если hello Dockerfile вызывает проблемы.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-198">hello Azure Toolkit does not validate hello content in a custom Dockerfile, so hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="dc0fd-199">Кроме того hello набора средств Azure ожидает hello пользовательских Dockerfile toocontain артефакт web app и он попытается tooopen HTTP-соединение.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-199">In addition, hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, and it will attempt tooopen an HTTP connection.</span></span> <span data-ttu-id="dc0fd-200">Если разработчики публикуют артефакт другого типа, то после развертывания могут возникнуть некритичные ошибки.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-200">If developers publish a different type of artifact, they may receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="dc0fd-201">c.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-201">c.</span></span> <span data-ttu-id="dc0fd-202">**Параметры порта**: Введите уникальную привязку порта TCP hello для контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-202">**Port settings**: Enter hello unique TCP port binding for your Docker container.</span></span>

     ![Настройка Hello hello контейнера Docker toobe создания окна][PUB08]

10. <span data-ttu-id="dc0fd-204">После завершения предыдущих шагах hello щелкните **Готово**.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-204">After you have completed all of hello preceding steps, click **Finish**.</span></span>

<span data-ttu-id="dc0fd-205">Hello набора средств Azure начинается развертывание вашей tooAzure приложения web в контейнер Docker.</span><span class="sxs-lookup"><span data-stu-id="dc0fd-205">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="dc0fd-206">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dc0fd-206">Next steps</span></span>
<span data-ttu-id="dc0fd-207">Дополнительные сведения о hello наборы инструментов Azure для Java интегрированные среды разработки см. следующие ресурсы hello:</span><span class="sxs-lookup"><span data-stu-id="dc0fd-207">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="dc0fd-208">[Набор средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="dc0fd-208">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="dc0fd-209">[Новые возможности средств Azure для Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="dc0fd-209">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="dc0fd-210">[Установка средств Azure для Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="dc0fd-210">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="dc0fd-211">[Инструкции вход для hello средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="dc0fd-211">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="dc0fd-212">[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]</span><span class="sxs-lookup"><span data-stu-id="dc0fd-212">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="dc0fd-213">[Набор средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="dc0fd-213">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="dc0fd-214">[Новые возможности средств Azure для IntelliJ hello]</span><span class="sxs-lookup"><span data-stu-id="dc0fd-214">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="dc0fd-215">[Установка hello Azure Toolkit для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="dc0fd-215">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="dc0fd-216">[Вход инструкции для hello Azure Toolkit для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="dc0fd-216">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="dc0fd-217">[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="dc0fd-217">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="dc0fd-218">Дополнительные сведения об использовании Azure см. в [центре разработчиков Java для Azure] и на странице [средств Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="dc0fd-218">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="dc0fd-219">Дополнительные ресурсы для Docker см. в разделе официальные hello [веб-узел Docker].</span><span class="sxs-lookup"><span data-stu-id="dc0fd-219">For additional resources for Docker, see hello official [Docker website].</span></span>

<!-- URL List -->

[Набор средств Azure для Eclipse]: ./azure-toolkit-for-eclipse.md
[Набор средств Azure для IntelliJ]: ./azure-toolkit-for-intellij.md
[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Установка средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-installation.md
[Установка hello Azure Toolkit для IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Инструкции вход для hello средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Вход инструкции для hello Azure Toolkit для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Новые возможности средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-whats-new.md
[Новые возможности средств Azure для IntelliJ hello]: ./azure-toolkit-for-intellij-whats-new.md

[центре разработчиков Java для Azure]: https://azure.microsoft.com/develop/java/
[средств Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)

[веб-узел Docker]: https://www.docker.com/

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png