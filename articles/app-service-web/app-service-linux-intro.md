---
title: "aaaIntroduction tooAzure веб-приложения на платформе Linux | Документы Microsoft"
description: "Сведения о веб-приложении Azure на платформе Linux."
keywords: "служба приложений azure, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 43b9865ade251909a77429eb3e18fe0bcaac3bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-web-app-on-linux"></a><span data-ttu-id="2aa29-104">Введение tooAzure веб-приложения в Linux</span><span class="sxs-lookup"><span data-stu-id="2aa29-104">Introduction tooAzure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="2aa29-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="2aa29-105">Overview</span></span>
<span data-ttu-id="2aa29-106">Клиенты могут использовать веб-приложения в Linux toohost веб-приложениях в Linux для приложений поддерживаются стеки.</span><span class="sxs-lookup"><span data-stu-id="2aa29-106">Customers can use Web App on Linux toohost web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="2aa29-107">Hello в подразделе ниже приведены стеки приложения hello, которые в настоящее время поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="2aa29-107">hello following section lists hello application stacks that are currently supported.</span></span> 

## <a name="features"></a><span data-ttu-id="2aa29-108">Функции</span><span class="sxs-lookup"><span data-stu-id="2aa29-108">Features</span></span>
<span data-ttu-id="2aa29-109">Веб-приложения на платформе Linux в настоящее время поддерживает следующие стеки приложения hello:</span><span class="sxs-lookup"><span data-stu-id="2aa29-109">Web App on Linux currently supports hello following application stacks:</span></span>

* <span data-ttu-id="2aa29-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="2aa29-110">Node.js</span></span>
    * <span data-ttu-id="2aa29-111">4.4.</span><span class="sxs-lookup"><span data-stu-id="2aa29-111">4.4</span></span>
    * <span data-ttu-id="2aa29-112">4.5.</span><span class="sxs-lookup"><span data-stu-id="2aa29-112">4.5</span></span>
    * <span data-ttu-id="2aa29-113">6.2</span><span class="sxs-lookup"><span data-stu-id="2aa29-113">6.2</span></span>
    * <span data-ttu-id="2aa29-114">6.6</span><span class="sxs-lookup"><span data-stu-id="2aa29-114">6.6</span></span>
    * <span data-ttu-id="2aa29-115">6.9</span><span class="sxs-lookup"><span data-stu-id="2aa29-115">6.9</span></span>
    * <span data-ttu-id="2aa29-116">6.10</span><span class="sxs-lookup"><span data-stu-id="2aa29-116">6.10</span></span>
    * <span data-ttu-id="2aa29-117">6.11</span><span class="sxs-lookup"><span data-stu-id="2aa29-117">6.11</span></span>
    * <span data-ttu-id="2aa29-118">8.0</span><span class="sxs-lookup"><span data-stu-id="2aa29-118">8.0</span></span>
    * <span data-ttu-id="2aa29-119">8.1</span><span class="sxs-lookup"><span data-stu-id="2aa29-119">8.1</span></span>
* <span data-ttu-id="2aa29-120">PHP</span><span class="sxs-lookup"><span data-stu-id="2aa29-120">PHP</span></span>
    * <span data-ttu-id="2aa29-121">5.6</span><span class="sxs-lookup"><span data-stu-id="2aa29-121">5.6</span></span>
    * <span data-ttu-id="2aa29-122">7.0</span><span class="sxs-lookup"><span data-stu-id="2aa29-122">7.0</span></span>
* <span data-ttu-id="2aa29-123">.NET Core.</span><span class="sxs-lookup"><span data-stu-id="2aa29-123">.Net Core</span></span>
    * <span data-ttu-id="2aa29-124">1.0</span><span class="sxs-lookup"><span data-stu-id="2aa29-124">1.0</span></span>
    * <span data-ttu-id="2aa29-125">1,1</span><span class="sxs-lookup"><span data-stu-id="2aa29-125">1.1</span></span>
* <span data-ttu-id="2aa29-126">Ruby</span><span class="sxs-lookup"><span data-stu-id="2aa29-126">Ruby</span></span>
    * <span data-ttu-id="2aa29-127">2.3</span><span class="sxs-lookup"><span data-stu-id="2aa29-127">2.3</span></span>

<span data-ttu-id="2aa29-128">Чтобы развертывать собственные приложения, клиенты могут использовать следующее:</span><span class="sxs-lookup"><span data-stu-id="2aa29-128">Customers can deploy their applications by using:</span></span>

* <span data-ttu-id="2aa29-129">FTP</span><span class="sxs-lookup"><span data-stu-id="2aa29-129">FTP</span></span>
* <span data-ttu-id="2aa29-130">локальный репозиторий Git;</span><span class="sxs-lookup"><span data-stu-id="2aa29-130">Local Git</span></span>
* <span data-ttu-id="2aa29-131">GitHub</span><span class="sxs-lookup"><span data-stu-id="2aa29-131">GitHub</span></span>
* <span data-ttu-id="2aa29-132">Bitbucket;</span><span class="sxs-lookup"><span data-stu-id="2aa29-132">Bitbucket</span></span>

<span data-ttu-id="2aa29-133">Масштабирование приложения осуществляется следующими способами:</span><span class="sxs-lookup"><span data-stu-id="2aa29-133">For application scaling:</span></span>

* <span data-ttu-id="2aa29-134">Клиенты вверх и вниз масштабирование веб-приложений можно изменить уровень hello их план служб приложений</span><span class="sxs-lookup"><span data-stu-id="2aa29-134">Customers can scale web apps up and down by changing hello tier of their App Service plan</span></span>
* <span data-ttu-id="2aa29-135">Клиентов можно масштабировать приложения и запустить несколько экземпляров приложения в рамках ограничивающее hello их номера SKU</span><span class="sxs-lookup"><span data-stu-id="2aa29-135">Customers can scale out applications and run multiple app instances within hello confines of their SKU</span></span>

<span data-ttu-id="2aa29-136">Для Kudu некоторые основные функциональные возможности hello:</span><span class="sxs-lookup"><span data-stu-id="2aa29-136">For Kudu, some of hello basic functionality:</span></span>

* <span data-ttu-id="2aa29-137">средами;</span><span class="sxs-lookup"><span data-stu-id="2aa29-137">Environments</span></span>
* <span data-ttu-id="2aa29-138">Развернутые приложения</span><span class="sxs-lookup"><span data-stu-id="2aa29-138">Deployments</span></span>
* <span data-ttu-id="2aa29-139">базовая консоль;</span><span class="sxs-lookup"><span data-stu-id="2aa29-139">Basic console</span></span>
* <span data-ttu-id="2aa29-140">SSH</span><span class="sxs-lookup"><span data-stu-id="2aa29-140">SSH</span></span>

<span data-ttu-id="2aa29-141">Функции для DevOps:</span><span class="sxs-lookup"><span data-stu-id="2aa29-141">For devops:</span></span>

* <span data-ttu-id="2aa29-142">Промежуточные среды</span><span class="sxs-lookup"><span data-stu-id="2aa29-142">Staging environments</span></span>
* <span data-ttu-id="2aa29-143">запись контроля доступа и непрерывная интеграция и развертывание Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="2aa29-143">ACR and DockerHub CI/CD</span></span>

## <a name="limitations"></a><span data-ttu-id="2aa29-144">Ограничения</span><span class="sxs-lookup"><span data-stu-id="2aa29-144">Limitations</span></span>
<span data-ttu-id="2aa29-145">Hello портал Azure показывает только функции, которые в настоящее время работают для веб-приложения на платформе Linux и скрывает hello rest.</span><span class="sxs-lookup"><span data-stu-id="2aa29-145">hello Azure portal shows only features that currently work for Web App on Linux and hides hello rest.</span></span> <span data-ttu-id="2aa29-146">Как мы включить дополнительные функции, они будут видны на портале hello.</span><span class="sxs-lookup"><span data-stu-id="2aa29-146">As we enable more features, they will be visible on hello portal.</span></span>

<span data-ttu-id="2aa29-147">Некоторые функции, такие как интеграция виртуальной сети, аутентификация Azure Active Directory, сторонняя аутентификация или расширения сайтов Kudu, в настоящее время недоступны.</span><span class="sxs-lookup"><span data-stu-id="2aa29-147">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span></span> <span data-ttu-id="2aa29-148">Когда эти возможности доступны, мы обновим наши документацию и блог об изменениях hello.</span><span class="sxs-lookup"><span data-stu-id="2aa29-148">Once these features are available, we will update our documentation and blog about hello changes.</span></span>

<span data-ttu-id="2aa29-149">Это общедоступной предварительной версии в данный момент доступна только в hello следующие области:</span><span class="sxs-lookup"><span data-stu-id="2aa29-149">This public preview is currently only available in hello following regions:</span></span>

* <span data-ttu-id="2aa29-150">Запад США</span><span class="sxs-lookup"><span data-stu-id="2aa29-150">West US</span></span>
* <span data-ttu-id="2aa29-151">Восток США</span><span class="sxs-lookup"><span data-stu-id="2aa29-151">East US</span></span>
* <span data-ttu-id="2aa29-152">Западная Европа</span><span class="sxs-lookup"><span data-stu-id="2aa29-152">West Europe</span></span>
* <span data-ttu-id="2aa29-153">Северная Европа</span><span class="sxs-lookup"><span data-stu-id="2aa29-153">North Europe</span></span>
* <span data-ttu-id="2aa29-154">Южно-центральный регион США</span><span class="sxs-lookup"><span data-stu-id="2aa29-154">South Central US</span></span>
* <span data-ttu-id="2aa29-155">Северо-центральный регион США</span><span class="sxs-lookup"><span data-stu-id="2aa29-155">North Central US</span></span>
* <span data-ttu-id="2aa29-156">Юго-Восточная Азия</span><span class="sxs-lookup"><span data-stu-id="2aa29-156">Southeast Asia</span></span>
* <span data-ttu-id="2aa29-157">Восточная Азия</span><span class="sxs-lookup"><span data-stu-id="2aa29-157">East Asia</span></span>
* <span data-ttu-id="2aa29-158">Восточная часть Австралии</span><span class="sxs-lookup"><span data-stu-id="2aa29-158">Australia East</span></span>
* <span data-ttu-id="2aa29-159">Восточная часть Японии</span><span class="sxs-lookup"><span data-stu-id="2aa29-159">Japan East</span></span>
* <span data-ttu-id="2aa29-160">Южная часть Бразилии</span><span class="sxs-lookup"><span data-stu-id="2aa29-160">Brazil South</span></span>
* <span data-ttu-id="2aa29-161">Южная Индия</span><span class="sxs-lookup"><span data-stu-id="2aa29-161">South India</span></span>

<span data-ttu-id="2aa29-162">Веб-приложения на платформе Linux поддерживаются только в планах службы выделенного приложения hello и не имеет бесплатном или общем уровне.</span><span class="sxs-lookup"><span data-stu-id="2aa29-162">Web Apps on Linux is only supported in hello Dedicated app service plans and does not have a Free or Shared tier.</span></span> <span data-ttu-id="2aa29-163">Кроме того, планы службы приложений для обычных веб-приложений и веб-приложений Linux взаимоисключающие. Это значит, что веб-приложение Linux нельзя создать в рамках плана службы приложений не для платформы Linux.</span><span class="sxs-lookup"><span data-stu-id="2aa29-163">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span></span>

<span data-ttu-id="2aa29-164">Веб-приложения на платформе Linux необходимо создать в группе ресурсов, который не содержит веб-приложений не Linux в hello одного региона.</span><span class="sxs-lookup"><span data-stu-id="2aa29-164">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in hello same region.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2aa29-165">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="2aa29-165">Troubleshooting</span></span> ##

<span data-ttu-id="2aa29-166">При сбое приложения toostart или требуется ведение журнала hello toocheck из приложения, проверьте журналы Docker в каталог LogFiles hello hello.</span><span class="sxs-lookup"><span data-stu-id="2aa29-166">When your application fails toostart or you want toocheck hello logging from your app, check hello Docker logs in hello LogFiles directory.</span></span> <span data-ttu-id="2aa29-167">Доступ к этому каталогу можно получить либо на сайте SCM, либо через FTP.</span><span class="sxs-lookup"><span data-stu-id="2aa29-167">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="2aa29-168">toolog hello `stdout` и `stderr` из контейнера, необходимо tooenable **ведения журнала контейнера Docker** под **журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="2aa29-168">toolog hello `stdout` and `stderr` from your container, you need tooenable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Включение ведения журнала][2]

![С помощью журналов Docker tooview Kudu][1]

<span data-ttu-id="2aa29-171">Получить доступ к сайту SCM hello **дополнительные средства** в hello **средства разработки** меню.</span><span class="sxs-lookup"><span data-stu-id="2aa29-171">You can access hello SCM site from **Advanced Tools** in hello **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2aa29-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2aa29-172">Next steps</span></span>
<span data-ttu-id="2aa29-173">См. следующие ссылки tooget к работе со службой приложения на платформе Linux hello.</span><span class="sxs-lookup"><span data-stu-id="2aa29-173">See hello following links tooget started with App Service on Linux.</span></span> <span data-ttu-id="2aa29-174">Если у вас возникли вопросы, опубликуйте их на [нашем форуме](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="2aa29-174">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="2aa29-175">Как toouse пользовательские Docker изображения для веб-приложения Azure в Linux</span><span class="sxs-lookup"><span data-stu-id="2aa29-175">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="2aa29-176">Использование конфигурации PM2 для Node.js в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="2aa29-176">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="2aa29-177">Использование .NET Core в веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="2aa29-177">Using .NET Core in Azure App Service Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="2aa29-178">Использование Ruby в веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="2aa29-178">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="2aa29-179">Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="2aa29-179">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="2aa29-180">Поддержка SSH для веб-приложения Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="2aa29-180">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="2aa29-181">Настройка промежуточных сред в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="2aa29-181">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="2aa29-182">Непрерывное развертывание Docker Hub для веб-приложения Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="2aa29-182">Docker Hub Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png