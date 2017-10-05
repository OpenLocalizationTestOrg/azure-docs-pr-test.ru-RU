---
title: "Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux | Документация Майкрософт"
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
ms.openlocfilehash: 6122f28b35d143ec26a379ae9aa8aee9bdaaff9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a><span data-ttu-id="feb92-104">Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="feb92-104">Azure App Service Web App on Linux FAQ</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="feb92-105">После выпуска веб-приложения на платформе Linux мы работаем над добавлением функций и усовершенствованиями нашей платформы.</span><span class="sxs-lookup"><span data-stu-id="feb92-105">With the release of Web App on Linux, we're working on adding features and making improvements to our platform.</span></span> <span data-ttu-id="feb92-106">Ниже приведены часто задаваемые вопросы, которые пользователи задавали нам за последние месяцы.</span><span class="sxs-lookup"><span data-stu-id="feb92-106">Here are some frequently asked questions (FAQ) that our customers have been asking us over the last months.</span></span>
<span data-ttu-id="feb92-107">Если у вас есть вопрос, то оставьте свой комментарий к этой статье, и мы ответим в кратчайшие сроки.</span><span class="sxs-lookup"><span data-stu-id="feb92-107">If you have a question, comment on the article and we'll answer it as soon as possible.</span></span>

## <a name="built-in-images"></a><span data-ttu-id="feb92-108">Встроенные образы</span><span class="sxs-lookup"><span data-stu-id="feb92-108">Built-in images</span></span>

<span data-ttu-id="feb92-109">**В.** Мне необходимо выполнить разветвление встроенных контейнеров Docker, предоставляемых этой платформой.</span><span class="sxs-lookup"><span data-stu-id="feb92-109">**Q:** I want to fork the built-in Docker containers that the platform provides.</span></span> <span data-ttu-id="feb92-110">Где находятся эти файлы?</span><span class="sxs-lookup"><span data-stu-id="feb92-110">Where can I find those files?</span></span>

<span data-ttu-id="feb92-111">**О.** Все файлы Docker можно найти на портале [GitHub](https://github.com/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="feb92-111">**A:** You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span></span> <span data-ttu-id="feb92-112">Все контейнеры Docker можно найти в репозитории [Docker Hub](https://hub.docker.com/u/appsvc/).</span><span class="sxs-lookup"><span data-stu-id="feb92-112">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span></span>

<span data-ttu-id="feb92-113">**В.** Какие значения будут доступны в разделе "Загрузочный файл" при настройке стека времени выполнения?</span><span class="sxs-lookup"><span data-stu-id="feb92-113">**Q:** What are the expected values for the Startup File section when I configure the runtime stack?</span></span>

<span data-ttu-id="feb92-114">**О.** Для Node.Js укажите файл конфигурации PM2 или свой файл сценария.</span><span class="sxs-lookup"><span data-stu-id="feb92-114">**A:** For Node.Js, you specify the PM2 configuration file or your script file.</span></span> <span data-ttu-id="feb92-115">Для .NET Core укажите имя скомпилированной библиотеки DLL.</span><span class="sxs-lookup"><span data-stu-id="feb92-115">For .NET Core, specify your compiled DLL name.</span></span> <span data-ttu-id="feb92-116">Для Ruby можно указать сценарий Ruby, с помощью которого вы хотите инициализировать приложение.</span><span class="sxs-lookup"><span data-stu-id="feb92-116">For Ruby, you can specify the Ruby script that you want to initialize your app with.</span></span>

## <a name="management"></a><span data-ttu-id="feb92-117">управления</span><span class="sxs-lookup"><span data-stu-id="feb92-117">Management</span></span>

<span data-ttu-id="feb92-118">**Вопрос.** Что происходит при нажатии кнопки перезагрузки на портале Azure?</span><span class="sxs-lookup"><span data-stu-id="feb92-118">**Q:** What happens when I press the restart button in the Azure portal?</span></span>

<span data-ttu-id="feb92-119">**Ответ.** Это аналогично перезагрузке Docker.</span><span class="sxs-lookup"><span data-stu-id="feb92-119">**A:** This is the equivalent of Docker restart.</span></span>

<span data-ttu-id="feb92-120">**В.** Можно ли использовать Secure Shell (SSH) для подключения к виртуальной машине контейнера приложения?</span><span class="sxs-lookup"><span data-stu-id="feb92-120">**Q:** Can I use Secure Shell (SSH) to connect to the app container virtual machine (VM)?</span></span>

<span data-ttu-id="feb92-121">**Ответ.** Да, это можно сделать через сайт SCM. Дополнительные сведения можно получить в статье о [поддержке SSH для веб-приложения на платформе Linux](./app-service-linux-ssh-support.md).</span><span class="sxs-lookup"><span data-stu-id="feb92-121">**A:** Yes, you can do that through the SCM site, check the following article for more information [SSH support for Web App on Linux](./app-service-linux-ssh-support.md)</span></span>

<span data-ttu-id="feb92-122">**Вопрос.** Как создать плоскость службы приложения Linux с помощью пакета SDK или шаблона ARM?</span><span class="sxs-lookup"><span data-stu-id="feb92-122">**Q:** I want to create a Linux App Service plane through SDK or an ARM template, how can I achieve this?</span></span>

<span data-ttu-id="feb92-123">**Ответ.** Необходимо указать для поля `reserved` службы приложения значение `true`.</span><span class="sxs-lookup"><span data-stu-id="feb92-123">**A:** You need to set the `reserved` field of the app service to `true`.</span></span>

## <a name="continuous-integrationdeployment"></a><span data-ttu-id="feb92-124">Непрерывная интеграция и развертывание</span><span class="sxs-lookup"><span data-stu-id="feb92-124">Continuous integration/deployment</span></span>

<span data-ttu-id="feb92-125">**В.** Мое веб-приложение по-прежнему использует старый образ контейнера Docker после обновления образа в Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="feb92-125">**Q:** My web app still uses an old Docker container image after I've updated the image on Docker Hub.</span></span> <span data-ttu-id="feb92-126">Поддерживается ли непрерывная интеграция и развертывание пользовательских контейнеров?</span><span class="sxs-lookup"><span data-stu-id="feb92-126">Do you support continuous integration/deployment of custom containers?</span></span>

<span data-ttu-id="feb92-127">**Ответ.** Сведения о настройке непрерывной интеграции и развертывания для образов реестра контейнеров Azure и Docker Hub приведены в статье [Непрерывное развертывание для веб-приложения Azure на платформе Linux](./app-service-linux-ci-cd.md).</span><span class="sxs-lookup"><span data-stu-id="feb92-127">**A:** To set up continuous integration/deployment for Azure Container Registry or DockerHub images by check the following article [Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md).</span></span> <span data-ttu-id="feb92-128">Для частных реестров контейнер можно обновить, остановив и снова запустив свое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="feb92-128">For private registries, you can refresh the container by stopping and then starting your web app.</span></span> <span data-ttu-id="feb92-129">Либо измените (добавьте) пустой параметр приложения, чтобы принудительно обновить контейнер.</span><span class="sxs-lookup"><span data-stu-id="feb92-129">Or you can change or add a dummy application setting to force a refresh of your container.</span></span>

<span data-ttu-id="feb92-130">**Вопрос.** Поддерживаются ли промежуточные среды?</span><span class="sxs-lookup"><span data-stu-id="feb92-130">**Q:** Do you support staging environments?</span></span>

<span data-ttu-id="feb92-131">**Ответ.** Да.</span><span class="sxs-lookup"><span data-stu-id="feb92-131">**A:** Yes.</span></span>

<span data-ttu-id="feb92-132">**Вопрос.** Можно ли развернуть веб-приложение с помощью **веб-развертывания**?</span><span class="sxs-lookup"><span data-stu-id="feb92-132">**Q:** Can I use **web deploy** to deploy my web app?</span></span>

<span data-ttu-id="feb92-133">**Ответ.** Да. Для параметра `WEBSITE_WEBDEPLOY_USE_SCM` приложения необходимо задать значение `false`.</span><span class="sxs-lookup"><span data-stu-id="feb92-133">**A:** Yes, you need to set an app setting called `WEBSITE_WEBDEPLOY_USE_SCM` to `false`.</span></span>

## <a name="language-support"></a><span data-ttu-id="feb92-134">Поддержка языков</span><span class="sxs-lookup"><span data-stu-id="feb92-134">Language support</span></span>

<span data-ttu-id="feb92-135">**В.** Поддерживаются ли некомпилированные приложения .NET Core?</span><span class="sxs-lookup"><span data-stu-id="feb92-135">**Q:** Do you support uncompiled .NET Core apps?</span></span>

<span data-ttu-id="feb92-136">**Ответ.** Да.</span><span class="sxs-lookup"><span data-stu-id="feb92-136">**A:** Yes.</span></span>

<span data-ttu-id="feb92-137">**Вопрос.** Поддерживает ли Composer диспетчер зависимостей для приложений PHP?</span><span class="sxs-lookup"><span data-stu-id="feb92-137">**Q:** Do you support Composer as a dependency manager for PHP apps?</span></span>

<span data-ttu-id="feb92-138">**Ответ.** Да.</span><span class="sxs-lookup"><span data-stu-id="feb92-138">**A:** Yes.</span></span> <span data-ttu-id="feb92-139">Во время развертывания Git Kudu определяет развертывание приложения PHP (благодаря файлу composer.json) и активирует установку Composer.</span><span class="sxs-lookup"><span data-stu-id="feb92-139">During a Git deployment, Kudu should detect that you are deploying a PHP application (thanks to the presence of a composer.json file) and will trigger a composer install for you.</span></span>

## <a name="custom-containers"></a><span data-ttu-id="feb92-140">Пользовательские контейнеры</span><span class="sxs-lookup"><span data-stu-id="feb92-140">Custom containers</span></span>

<span data-ttu-id="feb92-141">**В.** Я использую собственный пользовательский контейнер.</span><span class="sxs-lookup"><span data-stu-id="feb92-141">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="feb92-142">Мое приложение находится в каталоге `\home\`, но мне не удается найти файлы при просмотре содержимого с [сайта SCM](https://github.com/projectkudu/kudu) или FTP-клиента.</span><span class="sxs-lookup"><span data-stu-id="feb92-142">My app resides in the `\home\` directory, but I can't find my files when I browse the content by using the [SCM site](https://github.com/projectkudu/kudu) or an FTP client.</span></span> <span data-ttu-id="feb92-143">Где находятся мои файлы?</span><span class="sxs-lookup"><span data-stu-id="feb92-143">Where are my files?</span></span>

<span data-ttu-id="feb92-144">**Ответ.** Мы подключили общедоступный ресурс SMB к каталогу `\home\`.</span><span class="sxs-lookup"><span data-stu-id="feb92-144">**A:** We mount an SMB share to the `\home\` directory.</span></span> <span data-ttu-id="feb92-145">При этом переопределяется любое содержимое, которое там находится.</span><span class="sxs-lookup"><span data-stu-id="feb92-145">This will override any content that's there.</span></span>

<span data-ttu-id="feb92-146">**В.** Я использую собственный пользовательский контейнер.</span><span class="sxs-lookup"><span data-stu-id="feb92-146">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="feb92-147">Я не хочу, чтобы платформа подключила общий ресурс SMB к `\home\`.</span><span class="sxs-lookup"><span data-stu-id="feb92-147">I don't want the platform to mount an SMB share to the `\home\`.</span></span>

<span data-ttu-id="feb92-148">**Ответ.** Укажите для параметра `WEBSITES_ENABLE_APP_SERVICE_STORAGE` приложения значение `false`.</span><span class="sxs-lookup"><span data-stu-id="feb92-148">**A:** You can do that by setting the `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting to `false`.</span></span>

<span data-ttu-id="feb92-149">**Вопрос.** Мой пользовательский контейнер долго запускается, и платформа перезапускает контейнер до завершения его запуска.</span><span class="sxs-lookup"><span data-stu-id="feb92-149">**Q:** My custom container takes a long time to start, and the platform restart the container before it finishes starting up.</span></span>

<span data-ttu-id="feb92-150">**Ответ.** Можно настроить для платформы время ожидания перед перезапуском контейнера.</span><span class="sxs-lookup"><span data-stu-id="feb92-150">**A:** You can configure the time the platform will wait before restarting your container.</span></span> <span data-ttu-id="feb92-151">Это можно сделать, указав для параметра `WEBSITES_CONTAINER_START_TIME_LIMIT` приложения нужное значение в секундах.</span><span class="sxs-lookup"><span data-stu-id="feb92-151">This can be done by setting the `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting to the desired value in seconds.</span></span> <span data-ttu-id="feb92-152">Значение по умолчанию — 230 секунд; максимальное значение — 600 секунд.</span><span class="sxs-lookup"><span data-stu-id="feb92-152">The default is 230 seconds, and the max is 600 seconds.</span></span>

<span data-ttu-id="feb92-153">**В.** Какой формат используется для URL-адреса сервера частного реестра?</span><span class="sxs-lookup"><span data-stu-id="feb92-153">**Q:** What is the format for private registry server url?</span></span>

<span data-ttu-id="feb92-154">**Ответ.** Нужно указать полный URL-адрес реестра, включая `http://` или `https://`.</span><span class="sxs-lookup"><span data-stu-id="feb92-154">**A:** You need to provide the full registry url including `http://` or `https://`.</span></span>

<span data-ttu-id="feb92-155">**В.** Какой формат используется для имени образа в частном реестре?</span><span class="sxs-lookup"><span data-stu-id="feb92-155">**Q:** What is the format for the image name in private registry option?</span></span>

<span data-ttu-id="feb92-156">**О.** нужно добавить полное имя образа, включая URL-адрес частного реестра (например,</span><span class="sxs-lookup"><span data-stu-id="feb92-156">**A:** You need to add the full image name including the private registry url (eg.</span></span> <span data-ttu-id="feb92-157">myacr.azurecr.io/dotnet:latest)</span><span class="sxs-lookup"><span data-stu-id="feb92-157">myacr.azurecr.io/dotnet:latest)</span></span>

<span data-ttu-id="feb92-158">**В.** Я хочу предоставить несколько портов в образе настраиваемого контейнера.</span><span class="sxs-lookup"><span data-stu-id="feb92-158">**Q:** I want to expose more than one port on my custom container image.</span></span> <span data-ttu-id="feb92-159">Это возможно?</span><span class="sxs-lookup"><span data-stu-id="feb92-159">Is that possible?</span></span>

<span data-ttu-id="feb92-160">**О.** В настоящее время такая возможность не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="feb92-160">**A:** Currently, that isn't supported.</span></span>

<span data-ttu-id="feb92-161">**В.** Я могу использовать собственное хранилище?</span><span class="sxs-lookup"><span data-stu-id="feb92-161">**Q:** Can I bring my own storage?</span></span>

<span data-ttu-id="feb92-162">**О.** В настоящее время такая возможность не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="feb92-162">**A:** Currently that isn't supported.</span></span>

<span data-ttu-id="feb92-163">**В.** Мне не удается просматривать файловую систему или выполняющиеся процессы своего пользовательского контейнера на сайте SCM.</span><span class="sxs-lookup"><span data-stu-id="feb92-163">**Q:** I can't browse my custom container's file system or running processes from the SCM site.</span></span> <span data-ttu-id="feb92-164">Почему?</span><span class="sxs-lookup"><span data-stu-id="feb92-164">Why is that?</span></span>

<span data-ttu-id="feb92-165">**О.** Сайт SCM выполняется в отдельном контейнере.</span><span class="sxs-lookup"><span data-stu-id="feb92-165">**A:** The SCM site runs in a separate container.</span></span> <span data-ttu-id="feb92-166">Поэтому вы не можете проверить файловую систему или выполняющиеся процессы контейнера приложения.</span><span class="sxs-lookup"><span data-stu-id="feb92-166">You can't check the file system or running processes of the app container.</span></span>

<span data-ttu-id="feb92-167">**В.** Мой настраиваемый контейнер ожидает передачи данных через порт, отличный от порта 80.</span><span class="sxs-lookup"><span data-stu-id="feb92-167">**Q:** My custom container listens to a port other than port 80.</span></span> <span data-ttu-id="feb92-168">Как настроить приложение для перенаправления запросов в этот порт?</span><span class="sxs-lookup"><span data-stu-id="feb92-168">How can I configure my app to route the requests to that port?</span></span>

<span data-ttu-id="feb92-169">**Ответ.** Мы используем автоматическое определение портов. Вы также можете указать параметр приложения **WEBSITES_PORT** и присвоить ему номер нужного порта.</span><span class="sxs-lookup"><span data-stu-id="feb92-169">**A:** We have auto port detection, also you can specify an application setting called **WEBSITES_PORT**, and give it the value of the expected port number.</span></span> <span data-ttu-id="feb92-170">Ранее платформа использовала параметр приложения `PORT`. Мы планируем отказаться от этого параметра приложения и перейти исключительно к `WEBSITES_PORT`.</span><span class="sxs-lookup"><span data-stu-id="feb92-170">Previously the platform was using `PORT` app setting, we are planning to deprecate the use this app setting and move to using `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="feb92-171">**В.** Нужно ли реализовать HTTPS в своем настраиваемом контейнере?</span><span class="sxs-lookup"><span data-stu-id="feb92-171">**Q:** Do I need to implement HTTPS in my custom container.</span></span>

<span data-ttu-id="feb92-172">**О.** Нет, платформа обрабатывает завершение HTTPS на общих интерфейсных серверах.</span><span class="sxs-lookup"><span data-stu-id="feb92-172">**A:** No, the platform handles HTTPS termination at the shared frontends.</span></span>

## <a name="pricing-and-sla"></a><span data-ttu-id="feb92-173">Цены и соглашение об уровне обслуживания</span><span class="sxs-lookup"><span data-stu-id="feb92-173">Pricing and SLA</span></span>

<span data-ttu-id="feb92-174">**В.** Какая модель ценообразования используется в общедоступной предварительной версии?</span><span class="sxs-lookup"><span data-stu-id="feb92-174">**Q:** What's the pricing while you're using the public preview?</span></span>

<span data-ttu-id="feb92-175">**Ответ.** При использовании обычной модели ценообразования службы приложений Azure с вас взимается плата за половину количества часов работы вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="feb92-175">**A:** You are charged half the number of hours that your app runs, with the normal Azure App Service pricing.</span></span> <span data-ttu-id="feb92-176">Это означает, что вы получаете 50-процентную скидку на цены службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="feb92-176">This means that you get a 50 percent discount on normal Azure App Service pricing.</span></span>

## <a name="other"></a><span data-ttu-id="feb92-177">Другие</span><span class="sxs-lookup"><span data-stu-id="feb92-177">Other</span></span>

<span data-ttu-id="feb92-178">**В.** Какие знаки поддерживаются в именах параметров приложения?</span><span class="sxs-lookup"><span data-stu-id="feb92-178">**Q:** What are the supported characters in application settings names?</span></span>

<span data-ttu-id="feb92-179">**О.** Для параметров приложения можно использовать только знаки A–Z, a–z, 0–9 и символ подчеркивания.</span><span class="sxs-lookup"><span data-stu-id="feb92-179">**A:** You can only use A-Z, a-z, 0-9, and the underscore for application settings.</span></span>

<span data-ttu-id="feb92-180">**В.** Где можно отправить запрос на новые функции?</span><span class="sxs-lookup"><span data-stu-id="feb92-180">**Q:** Where can I request new features?</span></span>

<span data-ttu-id="feb92-181">**О.** Вы можете отправить свои идеи на [форуме отзывов о веб-приложениях](https://aka.ms/webapps-uservoice).</span><span class="sxs-lookup"><span data-stu-id="feb92-181">**A:** You can submit your idea at the [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span></span> <span data-ttu-id="feb92-182">Добавьте [Linux] в заголовок своей идеи.</span><span class="sxs-lookup"><span data-stu-id="feb92-182">Add "[Linux]" to the title of your idea.</span></span>

## <a name="next-steps"></a><span data-ttu-id="feb92-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="feb92-183">Next steps</span></span>
* [<span data-ttu-id="feb92-184">Что такое веб-приложение Azure на платформе Linux?</span><span class="sxs-lookup"><span data-stu-id="feb92-184">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="feb92-185">Поддержка SSH для веб-приложения Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="feb92-185">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="feb92-186">Настройка промежуточных сред в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="feb92-186">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="feb92-187">Непрерывное развертывание для веб-приложения Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="feb92-187">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
