---
title: "Поддержка aaaSSH Azure приложение службы веб-приложения на платформе Linux | Документы Microsoft"
description: "Сведения об использовании SSH для веб-приложения Azure на платформе Linux."
keywords: "служба приложений azure, веб-приложение, linux, oss"
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 66f9988f-8ffa-414a-9137-3a9b15a5573c
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: wesmc
ms.openlocfilehash: e00be6d4631e8936a2a8bc106da1fc06237a4b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a><span data-ttu-id="f3fe2-104">Поддержка SSH для веб-приложения Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="f3fe2-104">SSH support for Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="f3fe2-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="f3fe2-105">Overview</span></span>

<span data-ttu-id="f3fe2-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) —это сетевой протокол шифрования, предназначенный для безопасного использования сетевых служб.</span><span class="sxs-lookup"><span data-stu-id="f3fe2-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is a cryptographic network protocol for using network services securely.</span></span> <span data-ttu-id="f3fe2-107">Это наиболее часто используемые toolog в систему удаленно безопасно из командной строки и выполнение административных команд удаленно.</span><span class="sxs-lookup"><span data-stu-id="f3fe2-107">It is most commonly used toolog into a system remotely securely from a command-line and execute administrative commands remotely.</span></span>

<span data-ttu-id="f3fe2-108">Веб-приложения на платформе Linux обеспечивает поддержку SSH в контейнер приложения hello с каждым hello встроенных Docker изображения для hello стека выполнения новых веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="f3fe2-108">Web App on Linux provides SSH support into hello app container with each of hello built-in Docker images used for hello Runtime Stack of new web apps.</span></span> 

![Стеки времени выполнения](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

<span data-ttu-id="f3fe2-110">Можно также использовать SSH с пользовательских образов Docker, включая сервера SSH hello как часть изображения hello и его настройки, как описано в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="f3fe2-110">You can also use SSH with your custom Docker images by including hello SSH server as part of hello image and configuring it as described in this topic.</span></span>



## <a name="making-a-client-connection"></a><span data-ttu-id="f3fe2-111">Создание подключения клиента</span><span class="sxs-lookup"><span data-stu-id="f3fe2-111">Making a client connection</span></span>

<span data-ttu-id="f3fe2-112">toomake подключение клиента SSH hello основного сайта должна быть запущена.</span><span class="sxs-lookup"><span data-stu-id="f3fe2-112">toomake an SSH client connection, hello main site must be started.</span></span> 

<span data-ttu-id="f3fe2-113">Конечная точка управления элемента управления источника (SCM) hello веб-приложения, вставьте в адресную строку браузера, используя hello следующие формы:</span><span class="sxs-lookup"><span data-stu-id="f3fe2-113">Paste hello Source Control Management (SCM) endpoint for your web app into your browser using hello following form:</span></span>

        https://<your sitename>.scm.azurewebsites.net/webssh/host

<span data-ttu-id="f3fe2-114">Если вы не прошли проверку подлинности, не требуется tooauthenticate с tooconnect вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="f3fe2-114">If you are not already authenticated, you are required tooauthenticate with your Azure subscription tooconnect.</span></span>

![SSL-подключение](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a><span data-ttu-id="f3fe2-116">Поддержка SSH в пользовательских образах Docker</span><span class="sxs-lookup"><span data-stu-id="f3fe2-116">SSH support with custom Docker images</span></span>

<span data-ttu-id="f3fe2-117">Чтобы сообщение SSH toosupport изображения пользовательских Docker между контейнера hello и клиента hello в hello портал Azure выполните следующие шаги для образа Docker hello.</span><span class="sxs-lookup"><span data-stu-id="f3fe2-117">In order for a custom Docker image toosupport SSH communication between hello container and hello client in hello Azure portal, perform hello following steps for your Docker image.</span></span> 

<span data-ttu-id="f3fe2-118">Эти действия не отображаются в hello репозитория службы приложений Azure в качестве примера [здесь](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span><span class="sxs-lookup"><span data-stu-id="f3fe2-118">These steps are are shown in hello Azure App Service repository as an example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span></span>

1. <span data-ttu-id="f3fe2-119">Включить hello `openssh-server` установки в [ `RUN` инструкция](https://docs.docker.com/engine/reference/builder/#run) в hello Dockerfile для изображения и hello пароля для учетной записи root hello слишком`"Docker!"`.</span><span class="sxs-lookup"><span data-stu-id="f3fe2-119">Include hello `openssh-server` installation in [`RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) in hello Dockerfile for your image and set hello password for hello root account too`"Docker!"`.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="f3fe2-120">Эта конфигурация не позволяет контейнера toohello внешних подключений.</span><span class="sxs-lookup"><span data-stu-id="f3fe2-120">This configuration does not allow external connections toohello container.</span></span> <span data-ttu-id="f3fe2-121">SSH может осуществляться только через hello Kudu / SCM сайта, который проходит проверку подлинности с помощью hello учетные данные для публикации.</span><span class="sxs-lookup"><span data-stu-id="f3fe2-121">SSH can only be accessed via hello Kudu / SCM Site, which is authenticated using hello publishing credentials.</span></span>

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. <span data-ttu-id="f3fe2-122">Добавить [ `COPY` инструкция](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy [sshd_config](http://man.openbsd.org/sshd_config) файл toohello */д/ssh/* каталога.</span><span class="sxs-lookup"><span data-stu-id="f3fe2-122">Add a [`COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy a [sshd_config](http://man.openbsd.org/sshd_config) file toohello */etc/ssh/* directory.</span></span> <span data-ttu-id="f3fe2-123">Файл конфигурации должны быть основаны на наш файл sshd_config в репозитории GitHub службе приложений Azure hello [здесь](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span><span class="sxs-lookup"><span data-stu-id="f3fe2-123">Your configuration file should be based on our sshd_config file in hello Azure-App-Service GitHub repository [here](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f3fe2-124">Hello *sshd_config* файл должен включать следующие hello или сбой подключения hello:</span><span class="sxs-lookup"><span data-stu-id="f3fe2-124">hello *sshd_config* file must include hello following or hello connection fails:</span></span> 
    > * <span data-ttu-id="f3fe2-125">`Ciphers`должно содержать по крайней мере одно из следующих hello: `aes128-cbc,3des-cbc,aes256-cbc`.</span><span class="sxs-lookup"><span data-stu-id="f3fe2-125">`Ciphers` must include at least one of hello following: `aes128-cbc,3des-cbc,aes256-cbc`.</span></span>
    > * <span data-ttu-id="f3fe2-126">`MACs`должно содержать по крайней мере одно из следующих hello: `hmac-sha1,hmac-sha1-96`.</span><span class="sxs-lookup"><span data-stu-id="f3fe2-126">`MACs` must include at least one of hello following: `hmac-sha1,hmac-sha1-96`.</span></span>

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. <span data-ttu-id="f3fe2-127">Включить порт 2222 в hello [ `EXPOSE` инструкции](https://docs.docker.com/engine/reference/builder/#expose) для hello Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="f3fe2-127">Include port 2222 in hello [`EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) for hello Dockerfile.</span></span> <span data-ttu-id="f3fe2-128">Несмотря на то, что известен пароль учетной записи root hello, порт 2222 нельзя получить доступ из hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="f3fe2-128">Although hello root password is known, port 2222 cannot be accessed from hello internet.</span></span> <span data-ttu-id="f3fe2-129">Это внутренняя только порт доступен только по контейнерам внутри сетевого bridge hello частной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="f3fe2-129">It is an internal only port accessible only by containers within hello bridge network of a private virtual network.</span></span>

    ```docker
    EXPOSE 2222 80
    ```

4. <span data-ttu-id="f3fe2-130">Убедитесь, что toostart hello ssh службы.</span><span class="sxs-lookup"><span data-stu-id="f3fe2-130">Make sure toostart hello ssh service.</span></span> <span data-ttu-id="f3fe2-131">пример Hello [здесь](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) использует сценарий оболочки в */bin* каталога.</span><span class="sxs-lookup"><span data-stu-id="f3fe2-131">hello example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) uses a shell script in */bin* directory.</span></span>

    ```bash
    #!/bin/bash
    service ssh start
    ```

    <span data-ttu-id="f3fe2-132">Hello Dockerfile использует hello [ `CMD` инструкция](https://docs.docker.com/engine/reference/builder/#cmd) toorun hello скрипта.</span><span class="sxs-lookup"><span data-stu-id="f3fe2-132">hello Dockerfile uses hello [`CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) toorun hello script.</span></span>

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a><span data-ttu-id="f3fe2-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f3fe2-133">Next steps</span></span>
<span data-ttu-id="f3fe2-134">См. следующие ссылки для получения дополнительных сведений о веб-приложения на платформе Linux hello.</span><span class="sxs-lookup"><span data-stu-id="f3fe2-134">See hello following links for more information regarding Web App on Linux.</span></span> <span data-ttu-id="f3fe2-135">Если у вас возникли вопросы, опубликуйте их на [нашем форуме](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="f3fe2-135">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="f3fe2-136">Как toouse пользовательские Docker изображения для веб-приложения Azure в Linux</span><span class="sxs-lookup"><span data-stu-id="f3fe2-136">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="f3fe2-137">Использование конфигурации PM2 для Node.js в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="f3fe2-137">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="f3fe2-138">Использование .NET Core в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="f3fe2-138">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="f3fe2-139">Использование Ruby в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="f3fe2-139">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="f3fe2-140">Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="f3fe2-140">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

