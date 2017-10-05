---
title: "Введение в веб-приложение Azure на платформе Linux | Документация Майкрософт"
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
ms.openlocfilehash: 0870f811845ec7c705da13f08abdfa762d25b209
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-azure-web-app-on-linux"></a><span data-ttu-id="98c40-104">Введение в веб-приложение Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="98c40-104">Introduction to Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="98c40-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="98c40-105">Overview</span></span>
<span data-ttu-id="98c40-106">Веб-приложение на платформе Linux позволяет клиентам размещать веб-приложения из поддерживаемых стеков приложений изначально в Linux.</span><span class="sxs-lookup"><span data-stu-id="98c40-106">Customers can use Web App on Linux to host web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="98c40-107">В следующем разделе перечислены поддерживаемые в настоящее время стеки приложений.</span><span class="sxs-lookup"><span data-stu-id="98c40-107">The following section lists the application stacks that are currently supported.</span></span> 

## <a name="features"></a><span data-ttu-id="98c40-108">Функции</span><span class="sxs-lookup"><span data-stu-id="98c40-108">Features</span></span>
<span data-ttu-id="98c40-109">Сейчас веб-приложение на платформе Linux поддерживает следующие стеки приложений.</span><span class="sxs-lookup"><span data-stu-id="98c40-109">Web App on Linux currently supports the following application stacks:</span></span>

* <span data-ttu-id="98c40-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="98c40-110">Node.js</span></span>
    * <span data-ttu-id="98c40-111">4.4.</span><span class="sxs-lookup"><span data-stu-id="98c40-111">4.4</span></span>
    * <span data-ttu-id="98c40-112">4.5.</span><span class="sxs-lookup"><span data-stu-id="98c40-112">4.5</span></span>
    * <span data-ttu-id="98c40-113">6.2</span><span class="sxs-lookup"><span data-stu-id="98c40-113">6.2</span></span>
    * <span data-ttu-id="98c40-114">6.6</span><span class="sxs-lookup"><span data-stu-id="98c40-114">6.6</span></span>
    * <span data-ttu-id="98c40-115">6.9</span><span class="sxs-lookup"><span data-stu-id="98c40-115">6.9</span></span>
    * <span data-ttu-id="98c40-116">6.10</span><span class="sxs-lookup"><span data-stu-id="98c40-116">6.10</span></span>
    * <span data-ttu-id="98c40-117">6.11</span><span class="sxs-lookup"><span data-stu-id="98c40-117">6.11</span></span>
    * <span data-ttu-id="98c40-118">8.0</span><span class="sxs-lookup"><span data-stu-id="98c40-118">8.0</span></span>
    * <span data-ttu-id="98c40-119">8.1</span><span class="sxs-lookup"><span data-stu-id="98c40-119">8.1</span></span>
* <span data-ttu-id="98c40-120">PHP</span><span class="sxs-lookup"><span data-stu-id="98c40-120">PHP</span></span>
    * <span data-ttu-id="98c40-121">5.6</span><span class="sxs-lookup"><span data-stu-id="98c40-121">5.6</span></span>
    * <span data-ttu-id="98c40-122">7.0</span><span class="sxs-lookup"><span data-stu-id="98c40-122">7.0</span></span>
* <span data-ttu-id="98c40-123">.NET Core.</span><span class="sxs-lookup"><span data-stu-id="98c40-123">.Net Core</span></span>
    * <span data-ttu-id="98c40-124">1.0</span><span class="sxs-lookup"><span data-stu-id="98c40-124">1.0</span></span>
    * <span data-ttu-id="98c40-125">1,1</span><span class="sxs-lookup"><span data-stu-id="98c40-125">1.1</span></span>
* <span data-ttu-id="98c40-126">Ruby</span><span class="sxs-lookup"><span data-stu-id="98c40-126">Ruby</span></span>
    * <span data-ttu-id="98c40-127">2.3</span><span class="sxs-lookup"><span data-stu-id="98c40-127">2.3</span></span>

<span data-ttu-id="98c40-128">Чтобы развертывать собственные приложения, клиенты могут использовать следующее:</span><span class="sxs-lookup"><span data-stu-id="98c40-128">Customers can deploy their applications by using:</span></span>

* <span data-ttu-id="98c40-129">FTP</span><span class="sxs-lookup"><span data-stu-id="98c40-129">FTP</span></span>
* <span data-ttu-id="98c40-130">локальный репозиторий Git;</span><span class="sxs-lookup"><span data-stu-id="98c40-130">Local Git</span></span>
* <span data-ttu-id="98c40-131">GitHub</span><span class="sxs-lookup"><span data-stu-id="98c40-131">GitHub</span></span>
* <span data-ttu-id="98c40-132">Bitbucket;</span><span class="sxs-lookup"><span data-stu-id="98c40-132">Bitbucket</span></span>

<span data-ttu-id="98c40-133">Масштабирование приложения осуществляется следующими способами:</span><span class="sxs-lookup"><span data-stu-id="98c40-133">For application scaling:</span></span>

* <span data-ttu-id="98c40-134">клиенты могут масштабировать веб-приложения, изменяя уровень плана службы приложений;</span><span class="sxs-lookup"><span data-stu-id="98c40-134">Customers can scale web apps up and down by changing the tier of their App Service plan</span></span>
* <span data-ttu-id="98c40-135">клиенты могут разворачивать приложения и запускать несколько экземпляров приложения в пределах используемого номера SKU.</span><span class="sxs-lookup"><span data-stu-id="98c40-135">Customers can scale out applications and run multiple app instances within the confines of their SKU</span></span>

<span data-ttu-id="98c40-136">Ниже перечислены некоторые основные функции для Kudu:</span><span class="sxs-lookup"><span data-stu-id="98c40-136">For Kudu, some of the basic functionality:</span></span>

* <span data-ttu-id="98c40-137">средами;</span><span class="sxs-lookup"><span data-stu-id="98c40-137">Environments</span></span>
* <span data-ttu-id="98c40-138">Развернутые приложения</span><span class="sxs-lookup"><span data-stu-id="98c40-138">Deployments</span></span>
* <span data-ttu-id="98c40-139">базовая консоль;</span><span class="sxs-lookup"><span data-stu-id="98c40-139">Basic console</span></span>
* <span data-ttu-id="98c40-140">SSH</span><span class="sxs-lookup"><span data-stu-id="98c40-140">SSH</span></span>

<span data-ttu-id="98c40-141">Функции для DevOps:</span><span class="sxs-lookup"><span data-stu-id="98c40-141">For devops:</span></span>

* <span data-ttu-id="98c40-142">Промежуточные среды</span><span class="sxs-lookup"><span data-stu-id="98c40-142">Staging environments</span></span>
* <span data-ttu-id="98c40-143">запись контроля доступа и непрерывная интеграция и развертывание Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="98c40-143">ACR and DockerHub CI/CD</span></span>

## <a name="limitations"></a><span data-ttu-id="98c40-144">Ограничения</span><span class="sxs-lookup"><span data-stu-id="98c40-144">Limitations</span></span>
<span data-ttu-id="98c40-145">На портале Azure отображаются только те функции, которые уже доступны в веб-приложении на платформе Linux. Остальные функции скрыты.</span><span class="sxs-lookup"><span data-stu-id="98c40-145">The Azure portal shows only features that currently work for Web App on Linux and hides the rest.</span></span> <span data-ttu-id="98c40-146">Дополнительные функции будут отображаться на портале по мере добавления.</span><span class="sxs-lookup"><span data-stu-id="98c40-146">As we enable more features, they will be visible on the portal.</span></span>

<span data-ttu-id="98c40-147">Некоторые функции, такие как интеграция виртуальной сети, аутентификация Azure Active Directory, сторонняя аутентификация или расширения сайтов Kudu, в настоящее время недоступны.</span><span class="sxs-lookup"><span data-stu-id="98c40-147">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span></span> <span data-ttu-id="98c40-148">После того, как эти функции станут доступны, мы обновим нашу документацию и блог, добавив информацию об изменениях.</span><span class="sxs-lookup"><span data-stu-id="98c40-148">Once these features are available, we will update our documentation and blog about the changes.</span></span>

<span data-ttu-id="98c40-149">В настоящее время эта общедоступная предварительная версия доступна в следующих регионах:</span><span class="sxs-lookup"><span data-stu-id="98c40-149">This public preview is currently only available in the following regions:</span></span>

* <span data-ttu-id="98c40-150">Запад США</span><span class="sxs-lookup"><span data-stu-id="98c40-150">West US</span></span>
* <span data-ttu-id="98c40-151">Восток США</span><span class="sxs-lookup"><span data-stu-id="98c40-151">East US</span></span>
* <span data-ttu-id="98c40-152">Западная Европа</span><span class="sxs-lookup"><span data-stu-id="98c40-152">West Europe</span></span>
* <span data-ttu-id="98c40-153">Северная Европа</span><span class="sxs-lookup"><span data-stu-id="98c40-153">North Europe</span></span>
* <span data-ttu-id="98c40-154">Южно-центральный регион США</span><span class="sxs-lookup"><span data-stu-id="98c40-154">South Central US</span></span>
* <span data-ttu-id="98c40-155">Северо-центральный регион США</span><span class="sxs-lookup"><span data-stu-id="98c40-155">North Central US</span></span>
* <span data-ttu-id="98c40-156">Юго-Восточная Азия</span><span class="sxs-lookup"><span data-stu-id="98c40-156">Southeast Asia</span></span>
* <span data-ttu-id="98c40-157">Восточная Азия</span><span class="sxs-lookup"><span data-stu-id="98c40-157">East Asia</span></span>
* <span data-ttu-id="98c40-158">Восточная часть Австралии</span><span class="sxs-lookup"><span data-stu-id="98c40-158">Australia East</span></span>
* <span data-ttu-id="98c40-159">Восточная часть Японии</span><span class="sxs-lookup"><span data-stu-id="98c40-159">Japan East</span></span>
* <span data-ttu-id="98c40-160">Южная часть Бразилии</span><span class="sxs-lookup"><span data-stu-id="98c40-160">Brazil South</span></span>
* <span data-ttu-id="98c40-161">Южная Индия</span><span class="sxs-lookup"><span data-stu-id="98c40-161">South India</span></span>

<span data-ttu-id="98c40-162">Веб-приложения под управлением Linux поддерживаются только в рамках выделенных планов службы приложений. Уровни "Бесплатный" и "Общий" недоступны.</span><span class="sxs-lookup"><span data-stu-id="98c40-162">Web Apps on Linux is only supported in the Dedicated app service plans and does not have a Free or Shared tier.</span></span> <span data-ttu-id="98c40-163">Кроме того, планы службы приложений для обычных веб-приложений и веб-приложений Linux взаимоисключающие. Это значит, что веб-приложение Linux нельзя создать в рамках плана службы приложений не для платформы Linux.</span><span class="sxs-lookup"><span data-stu-id="98c40-163">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span></span>

<span data-ttu-id="98c40-164">Веб-приложения Linux необходимо создавать в группе ресурсов, в которой отсутствуют веб-приложения под управлением других платформ в том же регионе.</span><span class="sxs-lookup"><span data-stu-id="98c40-164">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in the same region.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="98c40-165">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="98c40-165">Troubleshooting</span></span> ##

<span data-ttu-id="98c40-166">Если не удается запустить приложение или необходимо проверить ведение журнала приложения, просмотрите журналы Docker в каталоге LogFiles.</span><span class="sxs-lookup"><span data-stu-id="98c40-166">When your application fails to start or you want to check the logging from your app, check the Docker logs in the LogFiles directory.</span></span> <span data-ttu-id="98c40-167">Доступ к этому каталогу можно получить либо на сайте SCM, либо через FTP.</span><span class="sxs-lookup"><span data-stu-id="98c40-167">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="98c40-168">Чтобы записать `stdout` и `stderr` из контейнера, необходимо включить **ведение журнала контейнера Docker** в разделе **Журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="98c40-168">To log the `stdout` and `stderr` from your container, you need to enable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Включение ведения журнала][2]

![Просмотр журналов Docker с помощью Kudu][1]

<span data-ttu-id="98c40-171">Получить доступ к сайту SCM можно, щелкнув **Дополнительные средства** в меню **Средства разработки**.</span><span class="sxs-lookup"><span data-stu-id="98c40-171">You can access the SCM site from **Advanced Tools** in the **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98c40-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="98c40-172">Next steps</span></span>
<span data-ttu-id="98c40-173">Просмотрите следующие материалы, чтобы приступить к работе со службой приложений в Linux.</span><span class="sxs-lookup"><span data-stu-id="98c40-173">See the following links to get started with App Service on Linux.</span></span> <span data-ttu-id="98c40-174">Если у вас возникли вопросы, опубликуйте их на [нашем форуме](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="98c40-174">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="98c40-175">Как применить пользовательский образ Docker для веб-приложения Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="98c40-175">How to use a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="98c40-176">Использование конфигурации PM2 для Node.js в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="98c40-176">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="98c40-177">Использование .NET Core в веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="98c40-177">Using .NET Core in Azure App Service Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="98c40-178">Использование Ruby в веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="98c40-178">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="98c40-179">Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="98c40-179">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="98c40-180">Поддержка SSH для веб-приложения Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="98c40-180">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="98c40-181">Настройка промежуточных сред в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="98c40-181">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="98c40-182">Непрерывное развертывание Docker Hub для веб-приложения Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="98c40-182">Docker Hub Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png