---
title: "Поддержка SSH для веб-приложения службы приложений Azure на платформе Linux | Документация Майкрософт"
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
ms.openlocfilehash: feee7a5c91d213a6b0bfdaf264a4da4d9e79cbe7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a><span data-ttu-id="3c34b-104">Поддержка SSH для веб-приложения Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="3c34b-104">SSH support for Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="3c34b-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="3c34b-105">Overview</span></span>

<span data-ttu-id="3c34b-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) —это сетевой протокол шифрования, предназначенный для безопасного использования сетевых служб.</span><span class="sxs-lookup"><span data-stu-id="3c34b-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is a cryptographic network protocol for using network services securely.</span></span> <span data-ttu-id="3c34b-107">Чаще всего он используется для безопасного удаленного входа в систему из командной строки и удаленного выполнения административных команд.</span><span class="sxs-lookup"><span data-stu-id="3c34b-107">It is most commonly used to log into a system remotely securely from a command-line and execute administrative commands remotely.</span></span>

<span data-ttu-id="3c34b-108">Веб-приложение на платформе Linux предоставляет поддержку SSH в контейнере приложения в каждом из встроенных образов Docker, используемых для стека времени выполнения новых веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="3c34b-108">Web App on Linux provides SSH support into the app container with each of the built-in Docker images used for the Runtime Stack of new web apps.</span></span> 

![Стеки времени выполнения](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

<span data-ttu-id="3c34b-110">Протокол SSH можно также использовать с помощью пользовательских образов Docker, добавив в них сервер SSH и настроив его, как описано в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="3c34b-110">You can also use SSH with your custom Docker images by including the SSH server as part of the image and configuring it as described in this topic.</span></span>



## <a name="making-a-client-connection"></a><span data-ttu-id="3c34b-111">Создание подключения клиента</span><span class="sxs-lookup"><span data-stu-id="3c34b-111">Making a client connection</span></span>

<span data-ttu-id="3c34b-112">Для создания SSH-подключения клиента должен быть запущен основной сайт.</span><span class="sxs-lookup"><span data-stu-id="3c34b-112">To make an SSH client connection, the main site must be started.</span></span> 

<span data-ttu-id="3c34b-113">Вставьте конечную точку управления системой управления версиями (SCM) для веб-приложения в браузер, используя приведенный ниже формат.</span><span class="sxs-lookup"><span data-stu-id="3c34b-113">Paste the Source Control Management (SCM) endpoint for your web app into your browser using the following form:</span></span>

        https://<your sitename>.scm.azurewebsites.net/webssh/host

<span data-ttu-id="3c34b-114">Если вы еще не прошли аутентификацию, это потребуется сделать, воспользовавшись подпиской Azure, чтобы подключиться.</span><span class="sxs-lookup"><span data-stu-id="3c34b-114">If you are not already authenticated, you are required to authenticate with your Azure subscription to connect.</span></span>

![SSL-подключение](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a><span data-ttu-id="3c34b-116">Поддержка SSH в пользовательских образах Docker</span><span class="sxs-lookup"><span data-stu-id="3c34b-116">SSH support with custom Docker images</span></span>

<span data-ttu-id="3c34b-117">Чтобы пользовательский образ Docker поддерживал обмен данными по протоколу SSH между контейнером и клиентом на портале Azure, выполните следующие действия с образом Docker.</span><span class="sxs-lookup"><span data-stu-id="3c34b-117">In order for a custom Docker image to support SSH communication between the container and the client in the Azure portal, perform the following steps for your Docker image.</span></span> 

<span data-ttu-id="3c34b-118">[Здесь](https://github.com/Azure-App-Service/node/blob/master/6.9.3/) в качестве примера эти действия показаны в репозитории службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="3c34b-118">These steps are are shown in the Azure App Service repository as an example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span></span>

1. <span data-ttu-id="3c34b-119">Добавьте установку `openssh-server` в инструкцию [`RUN` ](https://docs.docker.com/engine/reference/builder/#run)в Dockerfile для образа и установите пароль для учетной записи привилегированного пользователя `"Docker!"`.</span><span class="sxs-lookup"><span data-stu-id="3c34b-119">Include the `openssh-server` installation in [`RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) in the Dockerfile for your image and set the password for the root account to `"Docker!"`.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="3c34b-120">Эта конфигурация не разрешает внешние подключения к контейнеру.</span><span class="sxs-lookup"><span data-stu-id="3c34b-120">This configuration does not allow external connections to the container.</span></span> <span data-ttu-id="3c34b-121">SSH-подключение доступно только для Kudu и сайта SCM, который аутентифицирован с помощью учетных данных для публикации.</span><span class="sxs-lookup"><span data-stu-id="3c34b-121">SSH can only be accessed via the Kudu / SCM Site, which is authenticated using the publishing credentials.</span></span>

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. <span data-ttu-id="3c34b-122">Добавьте [инструкцию `COPY`](https://docs.docker.com/engine/reference/builder/#copy) в Dockerfile, чтобы скопировать файл [sshd_config](http://man.openbsd.org/sshd_config) в каталог */etc/ssh/*.</span><span class="sxs-lookup"><span data-stu-id="3c34b-122">Add a [`COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) to the Dockerfile to copy a [sshd_config](http://man.openbsd.org/sshd_config) file to the */etc/ssh/* directory.</span></span> <span data-ttu-id="3c34b-123">Ваш файл конфигурации должен быть создан на основе нашего файла sshd_config из репозитория GitHub Azure-App-Service, который доступен [здесь](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span><span class="sxs-lookup"><span data-stu-id="3c34b-123">Your configuration file should be based on our sshd_config file in the Azure-App-Service GitHub repository [here](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3c34b-124">Файл *sshd_config* должен содержать приведенные ниже компоненты, иначе установить подключение будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="3c34b-124">The *sshd_config* file must include the following or the connection fails:</span></span> 
    > * <span data-ttu-id="3c34b-125">`Ciphers` должен содержать по крайней мере одно из следующих значений: `aes128-cbc,3des-cbc,aes256-cbc`.</span><span class="sxs-lookup"><span data-stu-id="3c34b-125">`Ciphers` must include at least one of the following: `aes128-cbc,3des-cbc,aes256-cbc`.</span></span>
    > * <span data-ttu-id="3c34b-126">`MACs` должен содержать по крайней мере одно из следующих значений: `hmac-sha1,hmac-sha1-96`.</span><span class="sxs-lookup"><span data-stu-id="3c34b-126">`MACs` must include at least one of the following: `hmac-sha1,hmac-sha1-96`.</span></span>

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. <span data-ttu-id="3c34b-127">Добавьте порт 2222 в инструкцию [`EXPOSE` ](https://docs.docker.com/engine/reference/builder/#expose)для Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="3c34b-127">Include port 2222 in the [`EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) for the Dockerfile.</span></span> <span data-ttu-id="3c34b-128">Даже при указании пароля привилегированного пользователя порт 2222 недоступен из Интернета.</span><span class="sxs-lookup"><span data-stu-id="3c34b-128">Although the root password is known, port 2222 cannot be accessed from the internet.</span></span> <span data-ttu-id="3c34b-129">Это внутренний порт, который доступен только контейнерам внутри мостовой сети виртуальной частной сети.</span><span class="sxs-lookup"><span data-stu-id="3c34b-129">It is an internal only port accessible only by containers within the bridge network of a private virtual network.</span></span>

    ```docker
    EXPOSE 2222 80
    ```

4. <span data-ttu-id="3c34b-130">Обязательно запустите службу ssh.</span><span class="sxs-lookup"><span data-stu-id="3c34b-130">Make sure to start the ssh service.</span></span> <span data-ttu-id="3c34b-131">[Этот](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) пример использует сценарий оболочки в каталоге */bin*.</span><span class="sxs-lookup"><span data-stu-id="3c34b-131">The example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) uses a shell script in */bin* directory.</span></span>

    ```bash
    #!/bin/bash
    service ssh start
    ```

    <span data-ttu-id="3c34b-132">Dockerfile использует инструкцию [`CMD` ](https://docs.docker.com/engine/reference/builder/#cmd)для выполнения этого сценария.</span><span class="sxs-lookup"><span data-stu-id="3c34b-132">The Dockerfile uses the [`CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) to run the script.</span></span>

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a><span data-ttu-id="3c34b-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3c34b-133">Next steps</span></span>
<span data-ttu-id="3c34b-134">Дополнительные сведения о веб-приложении Azure на платформе Linux можно получить, воспользовавшись приведенными ниже ссылками.</span><span class="sxs-lookup"><span data-stu-id="3c34b-134">See the following links for more information regarding Web App on Linux.</span></span> <span data-ttu-id="3c34b-135">Если у вас возникли вопросы, опубликуйте их на [нашем форуме](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="3c34b-135">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="3c34b-136">Как применить пользовательский образ Docker для веб-приложения Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="3c34b-136">How to use a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="3c34b-137">Использование конфигурации PM2 для Node.js в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="3c34b-137">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="3c34b-138">Использование .NET Core в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="3c34b-138">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="3c34b-139">Использование Ruby в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="3c34b-139">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="3c34b-140">Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="3c34b-140">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

