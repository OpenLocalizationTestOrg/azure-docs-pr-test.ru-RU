---
title: "контейнер Docker с помощью aaaPublish hello Azure Toolkit для IntelliJ | Документы Microsoft"
description: "Узнайте, как toopublish tooMicrosoft приложения web Azure в качестве контейнера Docker с помощью hello Azure Toolkit для IntelliJ."
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
ms.openlocfilehash: bee94cb269ea707ae7ad55232e23e915aec48c34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="46f6d-103">Публикация веб-приложения как контейнер Docker с помощью hello Azure Toolkit для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="46f6d-103">Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="46f6d-104">Контейнеры Docker широко используются при развертывании веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="46f6d-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="46f6d-105">При использовании контейнеров Docker разработчиков можно объединить все файлы проекта и зависимости в один пакет для развертывания сервера tooa.</span><span class="sxs-lookup"><span data-stu-id="46f6d-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="46f6d-106">набор средств Azure для IntelliJ Hello упрощает этот процесс для разработчиков Java, добавив *опубликовать как контейнер Docker* компоненты для развертывания tooMicrosoft Azure.</span><span class="sxs-lookup"><span data-stu-id="46f6d-106">hello Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="46f6d-107">В этой статье описывается toopublish необходимые шаги hello tooAzure вашего приложения как контейнеры Docker.</span><span class="sxs-lookup"><span data-stu-id="46f6d-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="46f6d-108">Дополнительные сведения о Docker доступен на hello [веб-узел Docker].</span><span class="sxs-lookup"><span data-stu-id="46f6d-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="46f6d-109">Публикация вашего tooAzure web app с помощью контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="46f6d-109">Publish your web app tooAzure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="46f6d-110">toopublish веб-приложения необходимо создать артефакт готовым к развертыванию.</span><span class="sxs-lookup"><span data-stu-id="46f6d-110">toopublish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="46f6d-111">toolearn. более того, в разделе hello [Дополнительные сведения о создании артефактов](#artifacts) раздела.</span><span class="sxs-lookup"><span data-stu-id="46f6d-111">toolearn more, see hello [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="46f6d-112">Мастер развертывания hello выполнено хотя бы один раз, большая часть параметров, используемые по умолчанию, при запуске мастера hello.</span><span class="sxs-lookup"><span data-stu-id="46f6d-112">After you have completed hello deployment wizard at least once, most of your settings are used as defaults when you run hello wizard again.</span></span>
>

1. <span data-ttu-id="46f6d-113">Откройте проект веб-приложения в IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="46f6d-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="46f6d-114">toostart hello **опубликовать как контейнер Docker** мастер, выполните одно из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="46f6d-114">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="46f6d-115">В hello **проекта** окно инструментов, щелкните правой кнопкой мыши проект, нажмите кнопку **Azure**, а затем нажмите кнопку **опубликовать как контейнер Docker**:</span><span class="sxs-lookup"><span data-stu-id="46f6d-115">In hello **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![Hello опубликовать как команда контейнера Docker][PUB01]

   * <span data-ttu-id="46f6d-117">На панели инструментов IntelliJ hello, нажмите кнопку hello **публикации группы** , а затем нажмите **опубликовать как контейнер Docker**:</span><span class="sxs-lookup"><span data-stu-id="46f6d-117">On hello IntelliJ toolbar, click hello **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="46f6d-118">![Hello опубликовать как команда контейнера Docker][PUB02]</span><span class="sxs-lookup"><span data-stu-id="46f6d-118">![hello Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="46f6d-119">Hello **развертывания контейнера Docker в Azure** откроется мастер.</span><span class="sxs-lookup"><span data-stu-id="46f6d-119">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Развертывание контейнера Docker в Azure мастер Hello][PUB03]

3. <span data-ttu-id="46f6d-121">В hello **введите имя образа, выберите путь артефакта hello и проверьте toobe узла Docker используется** окне hello следующие:</span><span class="sxs-lookup"><span data-stu-id="46f6d-121">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span> 

   <span data-ttu-id="46f6d-122">а.</span><span class="sxs-lookup"><span data-stu-id="46f6d-122">a.</span></span> <span data-ttu-id="46f6d-123">В hello **имя образа Docker** введите уникальное имя для узла Docker.</span><span class="sxs-lookup"><span data-stu-id="46f6d-123">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="46f6d-124">(hello мастер автоматически создает имя, но ее можно изменить).</span><span class="sxs-lookup"><span data-stu-id="46f6d-124">(hello wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="46f6d-125">b.</span><span class="sxs-lookup"><span data-stu-id="46f6d-125">b.</span></span> <span data-ttu-id="46f6d-126">Hello **узлов** области отображаются узлы Docker, уже создан.</span><span class="sxs-lookup"><span data-stu-id="46f6d-126">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="46f6d-127">Выполните одно из следующих hello.</span><span class="sxs-lookup"><span data-stu-id="46f6d-127">Do either of hello following:</span></span> 
      * <span data-ttu-id="46f6d-128">Если у вас есть существующий узел Docker, можно развернуть вашей tooit web app.</span><span class="sxs-lookup"><span data-stu-id="46f6d-128">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
      * <span data-ttu-id="46f6d-129">toocreate узел Docker, щелкните зеленый hello "плюс" (**+**).</span><span class="sxs-lookup"><span data-stu-id="46f6d-129">toocreate a Docker host, click hello green plus sign (**+**).</span></span>  
       <span data-ttu-id="46f6d-130">Hello **создать узел Docker** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="46f6d-130">hello **Create Docker Host** dialog box opens.</span></span> 

      ![Мастер развертывания контейнера Docker в Azure][PUB04a]

4. <span data-ttu-id="46f6d-132">В hello **настроить новую виртуальную машину hello** окна, укажите следующую информацию о вашем узле Docker hello.</span><span class="sxs-lookup"><span data-stu-id="46f6d-132">In hello **Configure hello new virtual machine** window, provide hello following information about your Docker host.</span></span> <span data-ttu-id="46f6d-133">(hello мастер автоматически создает большую часть информации hello для вас, но вы можете изменить любые из них).</span><span class="sxs-lookup"><span data-stu-id="46f6d-133">(hello wizard automatically generates most of hello information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="46f6d-134">а.</span><span class="sxs-lookup"><span data-stu-id="46f6d-134">a.</span></span> <span data-ttu-id="46f6d-135">В hello **имя** введите уникальное имя для узла Docker hello.</span><span class="sxs-lookup"><span data-stu-id="46f6d-135">In hello **Name** box, enter a unique name for hello Docker host.</span></span> <span data-ttu-id="46f6d-136">(Это не так же, как имя образа Docker, указанный ранее hello hello.)</span><span class="sxs-lookup"><span data-stu-id="46f6d-136">(It is not hello same as hello Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="46f6d-137">b.</span><span class="sxs-lookup"><span data-stu-id="46f6d-137">b.</span></span> <span data-ttu-id="46f6d-138">В hello **подписки** введите hello подписки Azure, которая используется для узла.</span><span class="sxs-lookup"><span data-stu-id="46f6d-138">In hello **Subscription** box, enter hello Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="46f6d-139">c.</span><span class="sxs-lookup"><span data-stu-id="46f6d-139">c.</span></span> <span data-ttu-id="46f6d-140">В hello **область** введите hello географический регион, где находится вашего узла.</span><span class="sxs-lookup"><span data-stu-id="46f6d-140">In hello **Region** box, enter hello geographical region where your host is located.</span></span>
      
   <span data-ttu-id="46f6d-141">d.</span><span class="sxs-lookup"><span data-stu-id="46f6d-141">d.</span></span> <span data-ttu-id="46f6d-142">На hello **ОС и размер** вкладки, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="46f6d-142">On hello **OS and Size** tab, do hello following:</span></span>      
      * <span data-ttu-id="46f6d-143">**Системы узла**: Введите hello операционной системы для виртуальной машины hello, содержащий вашего узла.</span><span class="sxs-lookup"><span data-stu-id="46f6d-143">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="46f6d-144">**Размер**: Введите размер hello виртуальной машины для узла.</span><span class="sxs-lookup"><span data-stu-id="46f6d-144">**Size**: Enter hello virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="46f6d-145">д.</span><span class="sxs-lookup"><span data-stu-id="46f6d-145">e.</span></span> <span data-ttu-id="46f6d-146">На hello **группы ресурсов** выберите одно из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="46f6d-146">On hello **Resource Group** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="46f6d-147">**Новая группа ресурсов.** Создайте группу ресурсов для узла.</span><span class="sxs-lookup"><span data-stu-id="46f6d-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="46f6d-148">**Существующая группа ресурсов.** Укажите имеющуюся группу ресурсов из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="46f6d-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="46f6d-149">f.</span><span class="sxs-lookup"><span data-stu-id="46f6d-149">f.</span></span> <span data-ttu-id="46f6d-150">На hello **сети** выберите одно из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="46f6d-150">On hello **Network** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="46f6d-151">**New virtual network** (Новая виртуальная сеть). Создайте виртуальную сеть для узла.</span><span class="sxs-lookup"><span data-stu-id="46f6d-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="46f6d-152">**Existing virtual network** (Имеющаяся виртуальная сеть). Укажите имеющуюся виртуальную сеть из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="46f6d-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="46f6d-153">ж.</span><span class="sxs-lookup"><span data-stu-id="46f6d-153">g.</span></span> <span data-ttu-id="46f6d-154">На hello **хранения** выберите одно из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="46f6d-154">On hello **Storage** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="46f6d-155">**Создать учетную запись хранения.** Создайте учетную запись хранения для узла.</span><span class="sxs-lookup"><span data-stu-id="46f6d-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="46f6d-156">**Existing storage account** (Имеющаяся учетная запись хранения). Укажите имеющуюся учетную запись хранения из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="46f6d-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="46f6d-157">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="46f6d-157">Click **Next**.</span></span>  
     <span data-ttu-id="46f6d-158">Hello **настроить журнал учетные данные и параметры порта** открывается окно.</span><span class="sxs-lookup"><span data-stu-id="46f6d-158">hello **Configure log in credentials and port settings** window opens.</span></span>

      ![журнал настройки Hello в учетные данные и окно "Параметры" порт][PUB05]

6. <span data-ttu-id="46f6d-160">Выберите один из следующих вариантов hello.</span><span class="sxs-lookup"><span data-stu-id="46f6d-160">Select one of hello following options:</span></span>

      * <span data-ttu-id="46f6d-161">**Import credentials from Azure Key Vault** (Импортировать учетные данные из Azure Key Vault). Укажите сохраненный ранее набор учетных данных, хранящихся в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="46f6d-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="46f6d-162">Хранилище ключей Azure, созданная с определенной учетной записи или субъекта-службы автоматически недоступна по другой учетной записи или субъекта-службы, использующего hello подписки.</span><span class="sxs-lookup"><span data-stu-id="46f6d-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="46f6d-163">в хранилище другой учетной записи или служба ключ субъекта toouse hello tooallow, необходимо использовать учетную запись Azure портала tooadd hello hello или участника-службы.</span><span class="sxs-lookup"><span data-stu-id="46f6d-163">tooallow another account or service principal toouse hello key vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

      * <span data-ttu-id="46f6d-164">**New log in credentials** (Новые учетные данные для входа). Создайте набор учетных данных для входа в систему.</span><span class="sxs-lookup"><span data-stu-id="46f6d-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="46f6d-165">Если этот флажок установлен, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="46f6d-165">If you select this option, do hello following:</span></span>

        <span data-ttu-id="46f6d-166">а.</span><span class="sxs-lookup"><span data-stu-id="46f6d-166">a.</span></span> <span data-ttu-id="46f6d-167">На hello **учетные данные для виртуальной Машины** укажите следующую информацию для hello виртуальной машины учетных данных для узла Docker hello: * **Username**: Введите hello пользователя для имени входа виртуальной машины учетные данные.</span><span class="sxs-lookup"><span data-stu-id="46f6d-167">On hello **VM Credentials** tab, provide hello following information for hello virtual-machine login credentials of your Docker host: * **Username**: Enter hello username for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="46f6d-168">* **Пароль** и **Подтверждение**: hello пароль для учетных данных входа в систему виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="46f6d-168">* **Password** and **Confirm**: Enter hello password for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="46f6d-169">* **SSH**: Введите параметры hello Secure Shell (SSH) для узла Docker.</span><span class="sxs-lookup"><span data-stu-id="46f6d-169">* **SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="46f6d-170">Можно выбрать один из следующих вариантов hello: * **нет**: Указывает, что виртуальная машина не разрешают соединений по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="46f6d-170">You can select one of hello following options: * **None**: Specifies that your virtual machine does not allow SSH connections.</span></span>
                <span data-ttu-id="46f6d-171">* **Автоматическое создание**: автоматически создает hello необходимые параметры для подключения по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="46f6d-171">* **Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
                <span data-ttu-id="46f6d-172">* **Импорт из каталога**: позволяет toospecify каталог, содержащий набор ранее сохраненные параметры SSH.</span><span class="sxs-lookup"><span data-stu-id="46f6d-172">* **Import from directory**: Allows you toospecify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="46f6d-173">Hello каталог должен содержать hello, следующие два файла:</span><span class="sxs-lookup"><span data-stu-id="46f6d-173">hello directory must contain hello following two files:</span></span>
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        <span data-ttu-id="46f6d-174">b.</span><span class="sxs-lookup"><span data-stu-id="46f6d-174">b.</span></span> <span data-ttu-id="46f6d-175">На hello **доступа управляющей программы Docker** укажите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="46f6d-175">On hello **Docker Daemon Access** tab, provide hello following information:</span></span>

          ![Окно Create Docker Host (Создание узла Docker)][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. <span data-ttu-id="46f6d-177">После ввода hello необходимые сведения, нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="46f6d-177">After you have entered hello required information, click **Finish**.</span></span>  
    <span data-ttu-id="46f6d-178">Hello **развертывания контейнера Docker в Azure** снова появится мастер.</span><span class="sxs-lookup"><span data-stu-id="46f6d-178">hello **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Мастер развертывания контейнера Docker в Azure][PUB07]

8. <span data-ttu-id="46f6d-180">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="46f6d-180">Click **Next**.</span></span>  
    <span data-ttu-id="46f6d-181">Hello **Настройка hello Docker контейнера toobe создан** открывается окно.</span><span class="sxs-lookup"><span data-stu-id="46f6d-181">hello **Configure hello Docker container toobe created** window opens.</span></span>

   ![Настройка Hello hello контейнера Docker toobe создания окна][PUB08]

9. <span data-ttu-id="46f6d-183">В hello **Настройка hello Docker контейнера toobe создан** окна, предоставляют hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="46f6d-183">In hello **Configure hello Docker container toobe created** window, provide hello following information:</span></span> 

   <span data-ttu-id="46f6d-184">а.</span><span class="sxs-lookup"><span data-stu-id="46f6d-184">a.</span></span> <span data-ttu-id="46f6d-185">В hello **имя контейнера Docker** введите уникальное имя для контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="46f6d-185">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="46f6d-186">b.</span><span class="sxs-lookup"><span data-stu-id="46f6d-186">b.</span></span> <span data-ttu-id="46f6d-187">Выберите один из следующих образов Docker hello.</span><span class="sxs-lookup"><span data-stu-id="46f6d-187">Choose one of hello following Docker images:</span></span> 

      * <span data-ttu-id="46f6d-188">**Predefined Docker image** (Предопределенный образ Docker). Укажите имеющийся образ Docker из Azure.</span><span class="sxs-lookup"><span data-stu-id="46f6d-188">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="46f6d-189">Hello список образов Docker в этом поле состоит из нескольких изображений, hello, набор средств Azure был настроен toopatch так, что автоматически развертывается на артефакт.</span><span class="sxs-lookup"><span data-stu-id="46f6d-189">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="46f6d-190">**Custom Dockerfile** (Пользовательский Dockerfile). Укажите сохраненный ранее Dockerfile на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="46f6d-190">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="46f6d-191">Это еще одна возможность разработчикам, создающим собственные Dockerfile toodeploy.</span><span class="sxs-lookup"><span data-stu-id="46f6d-191">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="46f6d-192">Тем не менее он работает toodevelopers, использующих этот tooensure параметр, правильно ли построено их Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="46f6d-192">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="46f6d-193">Поскольку hello набора средств Azure не проверяет содержимое hello в пользовательских Dockerfile, hello может произойти сбой развертывания Если hello Dockerfile вызывает проблемы.</span><span class="sxs-lookup"><span data-stu-id="46f6d-193">Because hello Azure Toolkit does not validate hello content in a custom Dockerfile, hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="46f6d-194">Кроме того поскольку hello набора средств Azure ожидает hello пользовательских Dockerfile toocontain артефакт web app, он предпринимает tooopen HTTP-соединение.</span><span class="sxs-lookup"><span data-stu-id="46f6d-194">In addition, because hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, it attempts tooopen an HTTP connection.</span></span> <span data-ttu-id="46f6d-195">Если разработчики публикуют артефакт другого типа, то после развертывания могут возникнуть некритичные ошибки.</span><span class="sxs-lookup"><span data-stu-id="46f6d-195">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="46f6d-196">c.</span><span class="sxs-lookup"><span data-stu-id="46f6d-196">c.</span></span> <span data-ttu-id="46f6d-197">В hello **параметры порта** введите уникальную привязку порта TCP hello для контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="46f6d-197">In hello **Port settings** box, enter hello unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="46f6d-198">После завершения предыдущих шагах hello нажмите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="46f6d-198">After you have completed hello preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="46f6d-199">Hello набора средств Azure начинается развертывание вашей tooAzure приложения web в контейнер Docker.</span><span class="sxs-lookup"><span data-stu-id="46f6d-199">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> <span data-ttu-id="46f6d-200">Если вы настроили toobe IntelliJ, развернутых в фоновом режиме hello, **развертывание tooAzure** отображается индикатор хода выполнения.</span><span class="sxs-lookup"><span data-stu-id="46f6d-200">Unless you have configured IntelliJ toobe deployed in hello background, a **Deploying tooAzure** progress bar appears.</span></span> 

![индикатор хода выполнения развертывания Hello][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="46f6d-202">Дополнительные сведения о создании артефактов</span><span class="sxs-lookup"><span data-stu-id="46f6d-202">Additional information about creating artifacts</span></span>

<span data-ttu-id="46f6d-203">toocreate артефакт готовым к развертыванию hello следующие:</span><span class="sxs-lookup"><span data-stu-id="46f6d-203">toocreate a deployment-ready artifact, do hello following:</span></span>

1. <span data-ttu-id="46f6d-204">Откройте проект веб-приложения в IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="46f6d-204">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="46f6d-205">В меню **File** (Файл) выберите **Project Structure** (Структура проекта).</span><span class="sxs-lookup"><span data-stu-id="46f6d-205">Click **File**, and then click **Project Structure**.</span></span>

   ![Структура проекта команда Hello][ART01]

3. <span data-ttu-id="46f6d-207">tooadd на артефакт, щелкните зеленый hello "плюс" (**+**), а затем нажмите кнопку **веб-приложения: архив**.</span><span class="sxs-lookup"><span data-stu-id="46f6d-207">tooadd an artifact, click hello green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![Команда «Архива: веб-приложения» Hello][ART02]

4. <span data-ttu-id="46f6d-209">В hello **имя** введите имя для вашей артефакта (не включайте hello *.war* расширения) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="46f6d-209">In hello **Name** box, enter a name for your artifact (do not include hello *.war* extension), and then click **OK**.</span></span>

   ![поле "имя" Hello артефакта][ART03]

<span data-ttu-id="46f6d-211">Дополнительные сведения о создании артефактов в IntelliJ см. в разделе [Настройка артефакты] на веб-сайте JetBrains hello.</span><span class="sxs-lookup"><span data-stu-id="46f6d-211">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on hello JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46f6d-212">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="46f6d-212">Next steps</span></span>
<span data-ttu-id="46f6d-213">Дополнительные сведения о hello наборы инструментов Azure для Java интегрированные среды разработки см. следующие ресурсы hello:</span><span class="sxs-lookup"><span data-stu-id="46f6d-213">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="46f6d-214">[Набор средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="46f6d-214">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="46f6d-215">[Новые возможности средств Azure для Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="46f6d-215">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="46f6d-216">[Установка средств Azure для Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="46f6d-216">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="46f6d-217">[Инструкции вход для hello средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="46f6d-217">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="46f6d-218">[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]</span><span class="sxs-lookup"><span data-stu-id="46f6d-218">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="46f6d-219">[Набор средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="46f6d-219">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="46f6d-220">[Новые возможности средств Azure для IntelliJ hello]</span><span class="sxs-lookup"><span data-stu-id="46f6d-220">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="46f6d-221">[Установка hello Azure Toolkit для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="46f6d-221">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="46f6d-222">[Вход инструкции для hello Azure Toolkit для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="46f6d-222">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="46f6d-223">[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="46f6d-223">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="46f6d-224">Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure] и hello [Java средств для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="46f6d-224">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="46f6d-225">Дополнительные ресурсы для Docker см. в разделе официальные hello [веб-узел Docker].</span><span class="sxs-lookup"><span data-stu-id="46f6d-225">For additional resources for Docker, see hello official [Docker website].</span></span>

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

[центра разработчиков Java Azure]: https://azure.microsoft.com/develop/java/
[Java средств для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)

[веб-узел Docker]: https://www.docker.com/
[Настройка артефакты]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html (Настройка артефактов)

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
