---
title: "aaaHow toouse пользовательского образа Docker для веб-приложения Azure для Linux | Документы Microsoft"
description: "Как пользовательские Docker toouse изображения для веб-приложения Azure в Linux."
keywords: "служба приложений azure, веб-приложение, docker, контейнер"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: b97bd4e6-dff0-4976-ac20-d5c109a559a8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 8853095d0e1067cfea4297bbd23b622fe4a0d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a><span data-ttu-id="d0b04-104">Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="d0b04-104">Using a custom Docker image for Azure Web App on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="d0b04-105">Служба приложений включает предопределенные стеки приложений на платформе Linux с поддержкой определенных версий, включая PHP 7.0 и Node.js 4.5.</span><span class="sxs-lookup"><span data-stu-id="d0b04-105">App Service provides pre-defined application stacks on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span></span> <span data-ttu-id="d0b04-106">Службы приложений на платформе Linux использует контейнеры Docker toohost эти готовые стеки приложений.</span><span class="sxs-lookup"><span data-stu-id="d0b04-106">App Service on Linux uses Docker containers toohost these pre-built application stacks.</span></span> <span data-ttu-id="d0b04-107">Также можно использовать пользовательские toodeploy образа Docker вашего веб-приложения tooan приложения решения, еще не определен в Azure.</span><span class="sxs-lookup"><span data-stu-id="d0b04-107">You can also use a custom Docker image toodeploy your web app tooan application stack that is not already defined in Azure.</span></span> <span data-ttu-id="d0b04-108">Пользовательские образы Docker могут размещаться как в открытых, так и закрытых репозиториях Docker.</span><span class="sxs-lookup"><span data-stu-id="d0b04-108">Custom Docker images can be hosted on either a public or private Docker repository.</span></span>


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a><span data-ttu-id="d0b04-109">Практическое руководство. Определение пользовательского образа Docker для веб-приложения</span><span class="sxs-lookup"><span data-stu-id="d0b04-109">How to: set a custom Docker image for a web app</span></span>
<span data-ttu-id="d0b04-110">Можно задать hello пользовательского образа Docker для обоих новых и существующих приложений веб-узлов.</span><span class="sxs-lookup"><span data-stu-id="d0b04-110">You can set hello custom Docker image for both new and existing webs apps.</span></span> <span data-ttu-id="d0b04-111">При создании веб-приложения на платформе Linux в hello [портал Azure](https://portal.azure.com/#create/Microsoft.AppSvcLinux), нажмите кнопку **Настройка контейнера** tooset пользовательского образа Docker:</span><span class="sxs-lookup"><span data-stu-id="d0b04-111">When you create a web app on Linux in hello [Azure portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), click **Configure container** tooset a custom Docker image:</span></span>

![Определение пользовательского образа Docker для нового веб-приложения на платформе Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a><span data-ttu-id="d0b04-113">Практическое руководство. Применение пользовательского образа Docker из Docker Hub</span><span class="sxs-lookup"><span data-stu-id="d0b04-113">How to: use a custom Docker image from Docker Hub</span></span> ##
<span data-ttu-id="d0b04-114">toouse пользовательского образа Docker из Docker Hub:</span><span class="sxs-lookup"><span data-stu-id="d0b04-114">toouse a custom Docker image from Docker Hub:</span></span>

1. <span data-ttu-id="d0b04-115">В hello [портал Azure](https://portal.azure.com), найдите веб-приложения в Linux, затем в **параметры** щелкните **контейнера Docker**.</span><span class="sxs-lookup"><span data-stu-id="d0b04-115">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="d0b04-116">Выберите **Docker Hub** как hello **источник изображения**, либо нажмите кнопку **открытый** или **закрытый** и типа hello **изображения и Имя тега необязательно**, такие как `node:4.5`.</span><span class="sxs-lookup"><span data-stu-id="d0b04-116">Select **Docker Hub** as hello **Image source**, then click either **Public** or **Private** and type hello **Image and optional tag name**, such as `node:4.5`.</span></span> <span data-ttu-id="d0b04-117">Hello **команду запуска** задан автоматически на основе сеть, определенная в файле образа Docker hello, но можно задать собственные команды.</span><span class="sxs-lookup"><span data-stu-id="d0b04-117">hello **Startup command** is set automatically based on what is defined in hello Docker image file, but you can set your own commands.</span></span>  

    ![Настройка образа из открытого репозитория Docker Hub][2]

    <span data-ttu-id="d0b04-119">Если образ доступен из частного хранилища, необходимо также tooenter hello Docker Hub учетные данные (**пользователя для входа** и **пароль**) для hello частном репозитории Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="d0b04-119">When your image is from a private repository, you also need tooenter hello Docker Hub credentials as (**Login username** and **Password**) for hello private Docker Hub repository.</span></span>

    ![Настройка образа из закрытого репозитория Docker Hub][3]

3. <span data-ttu-id="d0b04-121">После настройки контейнера hello установите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d0b04-121">After you have configured hello container, click **Save**.</span></span>

## <a name="how-toouse-a-docker-image-from-a-private-image-registry"></a><span data-ttu-id="d0b04-122">Как toouse Docker изображение из реестра частный образ</span><span class="sxs-lookup"><span data-stu-id="d0b04-122">How toouse a Docker image from a private image registry</span></span> ##
<span data-ttu-id="d0b04-123">toouse пользовательского образа Docker из реестра частных образов:</span><span class="sxs-lookup"><span data-stu-id="d0b04-123">toouse a custom Docker image from a private image registry:</span></span>

1. <span data-ttu-id="d0b04-124">В hello [портал Azure](https://portal.azure.com), найдите веб-приложения в Linux, затем в **параметры** щелкните **контейнера Docker**.</span><span class="sxs-lookup"><span data-stu-id="d0b04-124">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="d0b04-125">Нажмите кнопку **частного реестра** как hello **источник изображения**.</span><span class="sxs-lookup"><span data-stu-id="d0b04-125">Click **Private registry** as hello **Image source**.</span></span> <span data-ttu-id="d0b04-126">Введите hello **изображения, а имя дополнительного тега**, **URL-адрес сервера** для частного реестра hello, вместе с учетными данными hello (**пользователя для входа** и **пароль** ).</span><span class="sxs-lookup"><span data-stu-id="d0b04-126">Enter hello **Image and optional tag name**, **Server URL** for hello private registry, along with hello credentials (**Login username** and **Password**).</span></span> <span data-ttu-id="d0b04-127">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d0b04-127">Click **Save**.</span></span>

    ![Настройка образа Docker из закрытого реестра][4]


## <a name="how-to-set-hello-port-used-by-your-docker-image"></a><span data-ttu-id="d0b04-129">Как: задать hello порт, используемый образ Docker</span><span class="sxs-lookup"><span data-stu-id="d0b04-129">How to: set hello port used by your Docker image</span></span> ##

<span data-ttu-id="d0b04-130">При использовании настраиваемого образа Docker для веб-приложения можно использовать hello `WEBSITES_PORT` переменной среды в Dockerfile, который добавляется созданный toohello контейнера.</span><span class="sxs-lookup"><span data-stu-id="d0b04-130">When you use a custom Docker image for your web app, you can use hello `WEBSITES_PORT` environment variable in your Dockerfile, which gets added toohello generated container.</span></span> <span data-ttu-id="d0b04-131">Рассмотрим следующий пример файла docker для Ruby приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d0b04-131">Consider hello following example of a docker file for a Ruby application:</span></span>

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

<span data-ttu-id="d0b04-132">В последней строке команды hello можно видно, что переменная WEBSITES_PORT hello передается во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="d0b04-132">On last line of hello command, you can see that hello WEBSITES_PORT environment variable is passed at runtime.</span></span> <span data-ttu-id="d0b04-133">Помните, что в командах учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="d0b04-133">Remember that casing matters in commands.</span></span>

<span data-ttu-id="d0b04-134">Ранее с помощью платформы hello `PORT` приложение, мы планирования toodeprecate hello использования этого параметра приложения и перемещение toousing `WEBSITES_PORT` исключительно.</span><span class="sxs-lookup"><span data-stu-id="d0b04-134">Previously hello platform was using `PORT` app setting, we are planning toodeprecate hello use this app setting and move toousing `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="d0b04-135">При использовании существующий образ Docker, построенный другим пользователем, может возникнуть необходимость toospecify порт, отличный от порта 80 для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d0b04-135">When you use an existing Docker image built by someone else, you may need toospecify a port other than port 80 for hello application.</span></span> <span data-ttu-id="d0b04-136">tooconfigure Здравствуйте, порт, добавьте параметр `WEBSITES_PORT` со значением hello, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="d0b04-136">tooconfigure hello port, add an application setting named `WEBSITES_PORT` with hello value as shown below:</span></span>

![Настройка параметра приложения PORT для пользовательского образа Docker][6]

## <a name="how-to-set-hello-startup-time-for-your-docker-image"></a><span data-ttu-id="d0b04-138">Как: задать время запуска hello образа Docker</span><span class="sxs-lookup"><span data-stu-id="d0b04-138">How to: set hello startup time for your Docker image</span></span> ##

<span data-ttu-id="d0b04-139">По умолчанию если контейнер не запускается до 230 секунд платформы hello перезапуск контейнера.</span><span class="sxs-lookup"><span data-stu-id="d0b04-139">By default, if your container does not start before 230 seconds, hello platform will restart your container.</span></span> <span data-ttu-id="d0b04-140">Если в более 230 секунд начинается настраиваемого образа Docker, можно использовать hello `WEBSITES_CONTAINER_START_TIME_LIMIT` параметр приложения hello значение для этого параметра задается в секундах, это позволит сохранить платформы hello запущены, прежде чем его контейнера.</span><span class="sxs-lookup"><span data-stu-id="d0b04-140">If your custom Docker image starts in more than 230 seconds, you can use hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting, hello value for this setting is in seconds, this will allow hello platform keep your container running before restarting it.</span></span> <span data-ttu-id="d0b04-141">значение по умолчанию Hello 230 секунд, и hello максимальное допустимое значение составляет 600 секунд.</span><span class="sxs-lookup"><span data-stu-id="d0b04-141">hello default value is 230 seconds, and hello max allowed value is 600 seconds.</span></span>

## <a name="how-to-unmount-hello-platform-provided-storage"></a><span data-ttu-id="d0b04-142">Как: отключить hello, предоставленного платформой хранилища</span><span class="sxs-lookup"><span data-stu-id="d0b04-142">How to: unmount hello platform provided storage</span></span> ##

<span data-ttu-id="d0b04-143">По умолчанию hello платформы, будет подключать постоянное хранилище общей папки toohello `\home\` каталога.</span><span class="sxs-lookup"><span data-stu-id="d0b04-143">By default, hello platform will mount a persistent storage share toohello `\home\` directory.</span></span> <span data-ttu-id="d0b04-144">Если образ контейнера не требуется постоянное папки, можно отключить подключение, хранилища, установка hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` приложения задание слишком`false`.</span><span class="sxs-lookup"><span data-stu-id="d0b04-144">If your container image does not need a persistent share, you can disable mounting that storage by setting hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting too`false`.</span></span> <span data-ttu-id="d0b04-145">По-прежнему будет иметь toothat доступ к хранилищу с сайта scm hello и toohello файлы журнала, созданные платформой hello будут записаны все журналы Docker (если он включен).</span><span class="sxs-lookup"><span data-stu-id="d0b04-145">You will still have access toothat storage from hello scm site, and all Docker logs (if enabled) will be written toohello log files generated by hello platform.</span></span>

## <a name="how-to-switch-back-toousing-a-built-in-image"></a><span data-ttu-id="d0b04-146">Как: коммутатора резервное toousing встроенного изображения</span><span class="sxs-lookup"><span data-stu-id="d0b04-146">How to: Switch back toousing a built-in image</span></span> ##

<span data-ttu-id="d0b04-147">tooswitch из toousing настраиваемого образа встроенного изображения с помощью:</span><span class="sxs-lookup"><span data-stu-id="d0b04-147">tooswitch from using a custom image toousing a built-in image:</span></span>

1. <span data-ttu-id="d0b04-148">В hello [портал Azure](https://portal.azure.com), найдите веб-приложения в Linux, затем в **параметры** щелкните **службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="d0b04-148">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **App Service**.</span></span>

2. <span data-ttu-id="d0b04-149">Выберите ваш **стек времени выполнения** toouse для hello встроенного изображения, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d0b04-149">Select your **Runtime Stack** toouse for hello built-in image, then click **Save**.</span></span> 

![Настройка встроенного образа Docker][5]


## <a name="troubleshooting"></a><span data-ttu-id="d0b04-151">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="d0b04-151">Troubleshooting</span></span> ##

<span data-ttu-id="d0b04-152">Toostart с настраиваемого образа Docker в случае сбоя приложения, проверьте журналы Docker в каталог LogFiles hello hello.</span><span class="sxs-lookup"><span data-stu-id="d0b04-152">When your application fails toostart with your custom Docker image, check hello Docker logs in hello LogFiles directory.</span></span> <span data-ttu-id="d0b04-153">Доступ к этому каталогу можно получить либо на сайте SCM, либо через FTP.</span><span class="sxs-lookup"><span data-stu-id="d0b04-153">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="d0b04-154">toolog hello `stdout` и `stderr` из контейнера, необходимо tooenable **ведения журнала контейнера Docker** под **журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="d0b04-154">toolog hello `stdout` and `stderr` from your container, you need tooenable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Включение ведения журнала][8]

![С помощью журналов Docker tooview Kudu][7]

<span data-ttu-id="d0b04-157">Получить доступ к сайту SCM hello **дополнительные средства** в hello **средства разработки** меню.</span><span class="sxs-lookup"><span data-stu-id="d0b04-157">You can access hello SCM site from **Advanced Tools** in hello **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0b04-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d0b04-158">Next Steps</span></span> ##

<span data-ttu-id="d0b04-159">Выполните следующие ссылки tooget работы с веб-приложения на платформе Linux hello.</span><span class="sxs-lookup"><span data-stu-id="d0b04-159">Follow hello following links tooget started with Web App on Linux.</span></span>   

* [<span data-ttu-id="d0b04-160">Введение tooAzure веб-приложения в Linux</span><span class="sxs-lookup"><span data-stu-id="d0b04-160">Introduction tooAzure Web App on Linux</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="d0b04-161">Использование конфигурации PM2 для Node.js в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="d0b04-161">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](./app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="d0b04-162">Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="d0b04-162">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<span data-ttu-id="d0b04-163">Если у вас возникли вопросы или проблемы, вы можете опубликовать их на [нашем форуме](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="d0b04-163">Post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
