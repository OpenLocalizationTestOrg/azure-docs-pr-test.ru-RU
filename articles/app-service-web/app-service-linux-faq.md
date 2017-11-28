---
title: "aaaAzure приложения службы веб-приложения на часто задаваемые вопросы о Linux | Документы Microsoft"
description: "Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux."
keywords: "служба приложений azure, веб-приложение, вопросы и ответы, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: c7798d9144d936eecdc0e191fc870b0ee0b220c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a><span data-ttu-id="2409a-104">Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="2409a-104">Azure App Service Web App on Linux FAQ</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="2409a-105">С выпуском hello веб-приложения на платформе Linux мы работаем над ситуацией и добавление функций платформы tooour улучшения.</span><span class="sxs-lookup"><span data-stu-id="2409a-105">With hello release of Web App on Linux, we're working on adding features and making improvements tooour platform.</span></span> <span data-ttu-id="2409a-106">Здесь представлены некоторые часто задаваемые вопросы (FAQ), которые наших клиентов пользователя может возникнуть вопрос нам по hello последнего месяца.</span><span class="sxs-lookup"><span data-stu-id="2409a-106">Here are some frequently asked questions (FAQ) that our customers have been asking us over hello last months.</span></span>
<span data-ttu-id="2409a-107">Если у вас есть вопрос, комментарий в статье hello и Мы ответим на его как можно быстрее.</span><span class="sxs-lookup"><span data-stu-id="2409a-107">If you have a question, comment on hello article and we'll answer it as soon as possible.</span></span>

## <a name="built-in-images"></a><span data-ttu-id="2409a-108">Встроенные образы</span><span class="sxs-lookup"><span data-stu-id="2409a-108">Built-in images</span></span>

<span data-ttu-id="2409a-109">**Вопрос** требуется предоставляет toofork hello встроенные контейнеры Docker, hello платформы.</span><span class="sxs-lookup"><span data-stu-id="2409a-109">**Q:** I want toofork hello built-in Docker containers that hello platform provides.</span></span> <span data-ttu-id="2409a-110">Где находятся эти файлы?</span><span class="sxs-lookup"><span data-stu-id="2409a-110">Where can I find those files?</span></span>

<span data-ttu-id="2409a-111">**О.** Все файлы Docker можно найти на портале [GitHub](https://github.com/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="2409a-111">**A:** You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span></span> <span data-ttu-id="2409a-112">Все контейнеры Docker можно найти в репозитории [Docker Hub](https://hub.docker.com/u/appsvc/).</span><span class="sxs-lookup"><span data-stu-id="2409a-112">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span></span>

<span data-ttu-id="2409a-113">**Вопрос** Каковы hello ожидаемые значения для hello раздел файла запуска при настроить стек времени выполнения hello?</span><span class="sxs-lookup"><span data-stu-id="2409a-113">**Q:** What are hello expected values for hello Startup File section when I configure hello runtime stack?</span></span>

<span data-ttu-id="2409a-114">**Ответ** для Node.Js указать файл конфигурации hello PM2 или файла скрипта.</span><span class="sxs-lookup"><span data-stu-id="2409a-114">**A:** For Node.Js, you specify hello PM2 configuration file or your script file.</span></span> <span data-ttu-id="2409a-115">Для .NET Core укажите имя скомпилированной библиотеки DLL.</span><span class="sxs-lookup"><span data-stu-id="2409a-115">For .NET Core, specify your compiled DLL name.</span></span> <span data-ttu-id="2409a-116">Для Ruby, вы можете указать hello Ruby сценария требуется tooinitialize приложения с.</span><span class="sxs-lookup"><span data-stu-id="2409a-116">For Ruby, you can specify hello Ruby script that you want tooinitialize your app with.</span></span>

## <a name="management"></a><span data-ttu-id="2409a-117">управления</span><span class="sxs-lookup"><span data-stu-id="2409a-117">Management</span></span>

<span data-ttu-id="2409a-118">**Вопрос** что происходит при нажатии кнопки перезагрузки hello в hello портал Azure?</span><span class="sxs-lookup"><span data-stu-id="2409a-118">**Q:** What happens when I press hello restart button in hello Azure portal?</span></span>

<span data-ttu-id="2409a-119">**Ответ** это hello эквивалент перезапуска Docker.</span><span class="sxs-lookup"><span data-stu-id="2409a-119">**A:** This is hello equivalent of Docker restart.</span></span>

<span data-ttu-id="2409a-120">**Вопрос** используется Secure Shell (SSH) tooconnect toohello приложения контейнера виртуальной машины (VM)?</span><span class="sxs-lookup"><span data-stu-id="2409a-120">**Q:** Can I use Secure Shell (SSH) tooconnect toohello app container virtual machine (VM)?</span></span>

<span data-ttu-id="2409a-121">**Ответ** Да, можно сделать, через сайт SCM hello, проверка hello следующие статьи для получения дополнительной информации [поддержка SSH для веб-приложения в Linux](./app-service-linux-ssh-support.md)</span><span class="sxs-lookup"><span data-stu-id="2409a-121">**A:** Yes, you can do that through hello SCM site, check hello following article for more information [SSH support for Web App on Linux](./app-service-linux-ssh-support.md)</span></span>

<span data-ttu-id="2409a-122">**Вопрос** требуется toocreate плоскость службы приложения Linux пакета SDK или шаблон ARM, как этого добиться?</span><span class="sxs-lookup"><span data-stu-id="2409a-122">**Q:** I want toocreate a Linux App Service plane through SDK or an ARM template, how can I achieve this?</span></span>

<span data-ttu-id="2409a-123">**Ответ** необходимо tooset hello `reserved` поле приложение hello службы слишком`true`.</span><span class="sxs-lookup"><span data-stu-id="2409a-123">**A:** You need tooset hello `reserved` field of hello app service too`true`.</span></span>

## <a name="continuous-integrationdeployment"></a><span data-ttu-id="2409a-124">Непрерывная интеграция и развертывание</span><span class="sxs-lookup"><span data-stu-id="2409a-124">Continuous integration/deployment</span></span>

<span data-ttu-id="2409a-125">**Вопрос** Мое веб-приложение по-прежнему используется старый образ контейнера Docker, после обновления образа hello в концентраторе Docker.</span><span class="sxs-lookup"><span data-stu-id="2409a-125">**Q:** My web app still uses an old Docker container image after I've updated hello image on Docker Hub.</span></span> <span data-ttu-id="2409a-126">Поддерживается ли непрерывная интеграция и развертывание пользовательских контейнеров?</span><span class="sxs-lookup"><span data-stu-id="2409a-126">Do you support continuous integration/deployment of custom containers?</span></span>

<span data-ttu-id="2409a-127">**Ответ** tooset копии непрерывной интеграции и развертыванию для реестра контейнера Azure или DockerHub изображений путем проверки hello следующей статьей [непрерывного развертывания с веб-приложения Azure в Linux](./app-service-linux-ci-cd.md).</span><span class="sxs-lookup"><span data-stu-id="2409a-127">**A:** tooset up continuous integration/deployment for Azure Container Registry or DockerHub images by check hello following article [Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md).</span></span> <span data-ttu-id="2409a-128">Для частных реестрах hello контейнера можно обновить, остановите и запустите веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="2409a-128">For private registries, you can refresh hello container by stopping and then starting your web app.</span></span> <span data-ttu-id="2409a-129">Или можно изменить или добавить макет приложения параметр tooforce обновления контейнера.</span><span class="sxs-lookup"><span data-stu-id="2409a-129">Or you can change or add a dummy application setting tooforce a refresh of your container.</span></span>

<span data-ttu-id="2409a-130">**Вопрос.** Поддерживаются ли промежуточные среды?</span><span class="sxs-lookup"><span data-stu-id="2409a-130">**Q:** Do you support staging environments?</span></span>

<span data-ttu-id="2409a-131">**Ответ.** Да.</span><span class="sxs-lookup"><span data-stu-id="2409a-131">**A:** Yes.</span></span>

<span data-ttu-id="2409a-132">**Вопрос** можно использовать **веб-развертывания** toodeploy Мое веб-приложение?</span><span class="sxs-lookup"><span data-stu-id="2409a-132">**Q:** Can I use **web deploy** toodeploy my web app?</span></span>

<span data-ttu-id="2409a-133">**Ответ** необходимо tooset названием приложения `WEBSITE_WEBDEPLOY_USE_SCM` слишком`false`.</span><span class="sxs-lookup"><span data-stu-id="2409a-133">**A:** Yes, you need tooset an app setting called `WEBSITE_WEBDEPLOY_USE_SCM` too`false`.</span></span>

## <a name="language-support"></a><span data-ttu-id="2409a-134">Поддержка языков</span><span class="sxs-lookup"><span data-stu-id="2409a-134">Language support</span></span>

<span data-ttu-id="2409a-135">**В.** Поддерживаются ли некомпилированные приложения .NET Core?</span><span class="sxs-lookup"><span data-stu-id="2409a-135">**Q:** Do you support uncompiled .NET Core apps?</span></span>

<span data-ttu-id="2409a-136">**Ответ.** Да.</span><span class="sxs-lookup"><span data-stu-id="2409a-136">**A:** Yes.</span></span>

<span data-ttu-id="2409a-137">**Вопрос.** Поддерживает ли Composer диспетчер зависимостей для приложений PHP?</span><span class="sxs-lookup"><span data-stu-id="2409a-137">**Q:** Do you support Composer as a dependency manager for PHP apps?</span></span>

<span data-ttu-id="2409a-138">**Ответ.** Да.</span><span class="sxs-lookup"><span data-stu-id="2409a-138">**A:** Yes.</span></span> <span data-ttu-id="2409a-139">Во время развертывания Git Kudu должен определить, выполняется развертывание приложения PHP (спасибо toohello наличие composer.json файла) и автоматически запустит установить редактор.</span><span class="sxs-lookup"><span data-stu-id="2409a-139">During a Git deployment, Kudu should detect that you are deploying a PHP application (thanks toohello presence of a composer.json file) and will trigger a composer install for you.</span></span>

## <a name="custom-containers"></a><span data-ttu-id="2409a-140">Пользовательские контейнеры</span><span class="sxs-lookup"><span data-stu-id="2409a-140">Custom containers</span></span>

<span data-ttu-id="2409a-141">**В.** Я использую собственный пользовательский контейнер.</span><span class="sxs-lookup"><span data-stu-id="2409a-141">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="2409a-142">Мое приложение находится в hello `\home\` каталога, но не удается найти файлы, при просмотре содержимого hello с помощью hello [SCM сайта](https://github.com/projectkudu/kudu) или FTP-клиент.</span><span class="sxs-lookup"><span data-stu-id="2409a-142">My app resides in hello `\home\` directory, but I can't find my files when I browse hello content by using hello [SCM site](https://github.com/projectkudu/kudu) or an FTP client.</span></span> <span data-ttu-id="2409a-143">Где находятся мои файлы?</span><span class="sxs-lookup"><span data-stu-id="2409a-143">Where are my files?</span></span>

<span data-ttu-id="2409a-144">**Ответ** подключении toohello общей папки SMB `\home\` каталога.</span><span class="sxs-lookup"><span data-stu-id="2409a-144">**A:** We mount an SMB share toohello `\home\` directory.</span></span> <span data-ttu-id="2409a-145">При этом переопределяется любое содержимое, которое там находится.</span><span class="sxs-lookup"><span data-stu-id="2409a-145">This will override any content that's there.</span></span>

<span data-ttu-id="2409a-146">**В.** Я использую собственный пользовательский контейнер.</span><span class="sxs-lookup"><span data-stu-id="2409a-146">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="2409a-147">Я не хочу toomount платформы hello toohello общей папки SMB `\home\`.</span><span class="sxs-lookup"><span data-stu-id="2409a-147">I don't want hello platform toomount an SMB share toohello `\home\`.</span></span>

<span data-ttu-id="2409a-148">**Ответ** это можно сделать путем установки hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` приложения задание слишком`false`.</span><span class="sxs-lookup"><span data-stu-id="2409a-148">**A:** You can do that by setting hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting too`false`.</span></span>

<span data-ttu-id="2409a-149">**Вопрос** Мой пользовательский контейнер принимает toostart много времени и контейнер hello hello платформа перезапуска перед его завершения запуска.</span><span class="sxs-lookup"><span data-stu-id="2409a-149">**Q:** My custom container takes a long time toostart, and hello platform restart hello container before it finishes starting up.</span></span>

<span data-ttu-id="2409a-150">**Ответ** можно настроить время hello hello платформы будет ожидать перед повторным запуском контейнера.</span><span class="sxs-lookup"><span data-stu-id="2409a-150">**A:** You can configure hello time hello platform will wait before restarting your container.</span></span> <span data-ttu-id="2409a-151">Это можно сделать путем установки hello `WEBSITES_CONTAINER_START_TIME_LIMIT` toohello параметр приложения требуемое значение в секундах.</span><span class="sxs-lookup"><span data-stu-id="2409a-151">This can be done by setting hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting toohello desired value in seconds.</span></span> <span data-ttu-id="2409a-152">по умолчанию Hello 230 секунд и hello max — 600 секунд.</span><span class="sxs-lookup"><span data-stu-id="2409a-152">hello default is 230 seconds, and hello max is 600 seconds.</span></span>

<span data-ttu-id="2409a-153">**Вопрос** hello формат URL-адреса сервера частного реестра?</span><span class="sxs-lookup"><span data-stu-id="2409a-153">**Q:** What is hello format for private registry server url?</span></span>

<span data-ttu-id="2409a-154">**Ответ** необходимо tooprovide hello полный URL-адрес включая `http://` или `https://`.</span><span class="sxs-lookup"><span data-stu-id="2409a-154">**A:** You need tooprovide hello full registry url including `http://` or `https://`.</span></span>

<span data-ttu-id="2409a-155">**Вопрос** hello формат имени образа hello в параметре реестра закрытый?</span><span class="sxs-lookup"><span data-stu-id="2409a-155">**Q:** What is hello format for hello image name in private registry option?</span></span>

<span data-ttu-id="2409a-156">**Ответ** требуется имя полного образа hello tooadd, включая hello url частного реестра (например)</span><span class="sxs-lookup"><span data-stu-id="2409a-156">**A:** You need tooadd hello full image name including hello private registry url (eg.</span></span> <span data-ttu-id="2409a-157">myacr.azurecr.io/dotnet:latest)</span><span class="sxs-lookup"><span data-stu-id="2409a-157">myacr.azurecr.io/dotnet:latest)</span></span>

<span data-ttu-id="2409a-158">**Вопрос** требуется tooexpose несколько портов на моем пользовательские образы.</span><span class="sxs-lookup"><span data-stu-id="2409a-158">**Q:** I want tooexpose more than one port on my custom container image.</span></span> <span data-ttu-id="2409a-159">Это возможно?</span><span class="sxs-lookup"><span data-stu-id="2409a-159">Is that possible?</span></span>

<span data-ttu-id="2409a-160">**О.** В настоящее время такая возможность не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="2409a-160">**A:** Currently, that isn't supported.</span></span>

<span data-ttu-id="2409a-161">**В.** Я могу использовать собственное хранилище?</span><span class="sxs-lookup"><span data-stu-id="2409a-161">**Q:** Can I bring my own storage?</span></span>

<span data-ttu-id="2409a-162">**О.** В настоящее время такая возможность не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="2409a-162">**A:** Currently that isn't supported.</span></span>

<span data-ttu-id="2409a-163">**Вопрос** мне не удается просмотреть Мой пользовательский контейнер системы или под управлением процесса файла с сайта SCM hello.</span><span class="sxs-lookup"><span data-stu-id="2409a-163">**Q:** I can't browse my custom container's file system or running processes from hello SCM site.</span></span> <span data-ttu-id="2409a-164">Почему?</span><span class="sxs-lookup"><span data-stu-id="2409a-164">Why is that?</span></span>

<span data-ttu-id="2409a-165">**Ответ** hello SCM сайта выполняется в отдельном контейнере.</span><span class="sxs-lookup"><span data-stu-id="2409a-165">**A:** hello SCM site runs in a separate container.</span></span> <span data-ttu-id="2409a-166">Не удается проверить hello файловой системы или выполняющихся процессов контейнера приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2409a-166">You can't check hello file system or running processes of hello app container.</span></span>

<span data-ttu-id="2409a-167">**Вопрос** Мой пользовательский контейнер прослушивает tooa порт, отличный от порта 80.</span><span class="sxs-lookup"><span data-stu-id="2409a-167">**Q:** My custom container listens tooa port other than port 80.</span></span> <span data-ttu-id="2409a-168">Как настроить Мои приложения tooroute hello запросов toothat порта</span><span class="sxs-lookup"><span data-stu-id="2409a-168">How can I configure my app tooroute hello requests toothat port?</span></span>

<span data-ttu-id="2409a-169">**Ответ** у нас есть порта автоопределения, также можно указать параметр приложения **WEBSITES_PORT**и присвойте ей значение hello hello ожидается номер порта.</span><span class="sxs-lookup"><span data-stu-id="2409a-169">**A:** We have auto port detection, also you can specify an application setting called **WEBSITES_PORT**, and give it hello value of hello expected port number.</span></span> <span data-ttu-id="2409a-170">Ранее с помощью платформы hello `PORT` приложение, мы планирования toodeprecate hello использования этого параметра приложения и перемещение toousing `WEBSITES_PORT` исключительно.</span><span class="sxs-lookup"><span data-stu-id="2409a-170">Previously hello platform was using `PORT` app setting, we are planning toodeprecate hello use this app setting and move toousing `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="2409a-171">**Вопрос** требуется tooimplement HTTPS в моей настраиваемого контейнера.</span><span class="sxs-lookup"><span data-stu-id="2409a-171">**Q:** Do I need tooimplement HTTPS in my custom container.</span></span>

<span data-ttu-id="2409a-172">**Ответ** нет, платформа hello обрабатывает завершение HTTPS на hello общих серверах переднего плана.</span><span class="sxs-lookup"><span data-stu-id="2409a-172">**A:** No, hello platform handles HTTPS termination at hello shared frontends.</span></span>

## <a name="pricing-and-sla"></a><span data-ttu-id="2409a-173">Цены и соглашение об уровне обслуживания</span><span class="sxs-lookup"><span data-stu-id="2409a-173">Pricing and SLA</span></span>

<span data-ttu-id="2409a-174">**Вопрос** что hello цены при использовании общедоступной предварительной версии hello?</span><span class="sxs-lookup"><span data-stu-id="2409a-174">**Q:** What's hello pricing while you're using hello public preview?</span></span>

<span data-ttu-id="2409a-175">**Ответ** взимается половину hello количество часов, ваше приложение запускается с hello обычный Azure цены на службу приложений.</span><span class="sxs-lookup"><span data-stu-id="2409a-175">**A:** You are charged half hello number of hours that your app runs, with hello normal Azure App Service pricing.</span></span> <span data-ttu-id="2409a-176">Это означает, что вы получаете 50-процентную скидку на цены службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="2409a-176">This means that you get a 50 percent discount on normal Azure App Service pricing.</span></span>

## <a name="other"></a><span data-ttu-id="2409a-177">Другие</span><span class="sxs-lookup"><span data-stu-id="2409a-177">Other</span></span>

<span data-ttu-id="2409a-178">**Вопрос** Каковы hello поддерживается символы в именах параметров приложения?</span><span class="sxs-lookup"><span data-stu-id="2409a-178">**Q:** What are hello supported characters in application settings names?</span></span>

<span data-ttu-id="2409a-179">**Ответ** только можно использовать A-Z, a-z, 0-9 и символ подчеркивания для параметров приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2409a-179">**A:** You can only use A-Z, a-z, 0-9, and hello underscore for application settings.</span></span>

<span data-ttu-id="2409a-180">**В.** Где можно отправить запрос на новые функции?</span><span class="sxs-lookup"><span data-stu-id="2409a-180">**Q:** Where can I request new features?</span></span>

<span data-ttu-id="2409a-181">**Ответ** можно отправить ваши идеи по hello [форуме обратной связи веб-приложений](https://aka.ms/webapps-uservoice).</span><span class="sxs-lookup"><span data-stu-id="2409a-181">**A:** You can submit your idea at hello [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span></span> <span data-ttu-id="2409a-182">Добавьте заголовок «[Linux]» toohello ваша идея.</span><span class="sxs-lookup"><span data-stu-id="2409a-182">Add "[Linux]" toohello title of your idea.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2409a-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2409a-183">Next steps</span></span>
* [<span data-ttu-id="2409a-184">Что такое веб-приложение Azure на платформе Linux?</span><span class="sxs-lookup"><span data-stu-id="2409a-184">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="2409a-185">Поддержка SSH для веб-приложения Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="2409a-185">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="2409a-186">Настройка промежуточных сред в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="2409a-186">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="2409a-187">Непрерывное развертывание для веб-приложения Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="2409a-187">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
