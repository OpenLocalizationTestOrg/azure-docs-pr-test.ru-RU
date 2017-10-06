---
title: "aaaContinuous развертывания с веб-приложения Azure для Linux | Документы Microsoft"
description: "Как toosetup непрерывного развертывания в веб-приложения Azure в Linux."
keywords: "служба приложений azure, linux, oss, acr"
services: app-service
documentationcenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: f94d837e27605da58428f507ab2b0eb3af3297e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a><span data-ttu-id="3fd39-104">Непрерывное развертывание для веб-приложения Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="3fd39-104">Continuous deployment with Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="3fd39-105">В этом руководстве описывается настройка непрерывного развертывания для настраиваемого образа контейнера из управляемых репозиториев [реестра контейнеров Azure](https://azure.microsoft.com/en-us/services/container-registry/) или [Docker Hub](https://hub.docker.com).</span><span class="sxs-lookup"><span data-stu-id="3fd39-105">In this tutorial, you configure continuous deployment for a custom container image from Managed [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span></span>

## <a name="step-1---sign-in-tooazure"></a><span data-ttu-id="3fd39-106">Шаг 1. вход tooAzure</span><span class="sxs-lookup"><span data-stu-id="3fd39-106">Step 1 - Sign in tooAzure</span></span>

<span data-ttu-id="3fd39-107">Войдите в toohello портал Azure по адресу http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="3fd39-107">Sign in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---enable-container-continuous-deployment-feature"></a><span data-ttu-id="3fd39-108">Шаг 2. Включение функции непрерывного развертывания контейнера</span><span class="sxs-lookup"><span data-stu-id="3fd39-108">Step 2 - Enable container continuous deployment feature</span></span>

<span data-ttu-id="3fd39-109">Можно включить с помощью функции hello непрерывного развертывания [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) и выполнив следующую команду hello</span><span class="sxs-lookup"><span data-stu-id="3fd39-109">You can enable hello continuous deployment feature using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

<span data-ttu-id="3fd39-110">В hello  **[портал Azure](https://portal.azure.com/)**, нажмите кнопку hello **службы приложений** параметр hello левой части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="3fd39-110">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="3fd39-111">Щелкните имя нужного tooconfigure Docker Hub непрерывного развертывания для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3fd39-111">Click on hello name of your app that you want tooconfigure Docker Hub continuous deployment for.</span></span>

<span data-ttu-id="3fd39-112">В hello **параметры приложения**, добавьте параметр приложения `DOCKER_ENABLE_CI` со значением hello `true`.</span><span class="sxs-lookup"><span data-stu-id="3fd39-112">In hello **App settings**, add an app setting called `DOCKER_ENABLE_CI` with hello value `true`.</span></span>

![Изображение добавления параметра приложения](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a><span data-ttu-id="3fd39-114">Шаг 3 . Подготовка URL-адреса Webhook</span><span class="sxs-lookup"><span data-stu-id="3fd39-114">Step 3 - Prepare Webhook URL</span></span>

<span data-ttu-id="3fd39-115">Можно получить с помощью URL-адрес веб-перехватчика hello [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) и выполнив следующую команду hello</span><span class="sxs-lookup"><span data-stu-id="3fd39-115">You can obtain hello Webhook URL using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

<span data-ttu-id="3fd39-116">Для hello URL-адрес веб-перехватчика необходимо toohave hello, следующая конечная точка: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span><span class="sxs-lookup"><span data-stu-id="3fd39-116">For hello Webhook URL, you need toohave hello following endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span></span>

<span data-ttu-id="3fd39-117">Вы можете получить ваш `publishingusername` и `publishingpwd` путем загрузки веб-приложения hello опубликовать профиль, воспользовавшись hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3fd39-117">You can obtain your `publishingusername` and `publishingpwd` by downloading hello web app publish profile using hello Azure portal.</span></span>

![Изображение добавления webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a><span data-ttu-id="3fd39-119">Шаг 4. Добавление webhook</span><span class="sxs-lookup"><span data-stu-id="3fd39-119">Step 4 - Add a web hook</span></span>

### <a name="azure-container-registry"></a><span data-ttu-id="3fd39-120">Реестр контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="3fd39-120">Azure Container Registry</span></span>

<span data-ttu-id="3fd39-121">В колонке реестра щелкните **Webhooks** (Объекты webhook), создайте webhook, нажав кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3fd39-121">In your registry portal blade, click **Webhooks**, create a new webhook by clicking **Add**.</span></span> <span data-ttu-id="3fd39-122">В hello **создать веб-перехватчика** колонки, присвойте имя вашего веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="3fd39-122">In hello **Create webhook** blade, give your webhook a name.</span></span> <span data-ttu-id="3fd39-123">Для hello URI веб-перехватчика необходимо hello tooprovide URL-адрес, полученный от **шаг 3**</span><span class="sxs-lookup"><span data-stu-id="3fd39-123">For hello Webhook URI, you need tooprovide hello URL obtained from **Step 3**</span></span>

<span data-ttu-id="3fd39-124">Убедитесь, что определение области hello как hello репозитория, который содержит образ контейнера.</span><span class="sxs-lookup"><span data-stu-id="3fd39-124">Make sure that you define hello scope as hello repo that contains your container image.</span></span>

![изображение webhook](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

<span data-ttu-id="3fd39-126">При обновлении образа hello, веб-приложения hello автоматически обновляться при hello нового образа.</span><span class="sxs-lookup"><span data-stu-id="3fd39-126">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

### <a name="docker-hub"></a><span data-ttu-id="3fd39-127">Docker Hub</span><span class="sxs-lookup"><span data-stu-id="3fd39-127">Docker Hub</span></span>

<span data-ttu-id="3fd39-128">На своей странице Docker Hub щелкните **Webhooks** (Объекты webhook), затем щелкните **CREATE A WEBHOOK** (Создать webhook).</span><span class="sxs-lookup"><span data-stu-id="3fd39-128">In your Docker Hub page, click **Webhooks**, then **CREATE A WEBHOOK**.</span></span>

![Изображение добавления webhook 1](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

<span data-ttu-id="3fd39-130">Для hello URL-адрес веб-перехватчика необходимо hello tooprovide URL-адрес, полученный от **шаг 3**</span><span class="sxs-lookup"><span data-stu-id="3fd39-130">For hello Webhook URL, you need tooprovide hello URL obtained from **Step 3**</span></span>

![Изображение добавления webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

<span data-ttu-id="3fd39-132">При обновлении образа hello, веб-приложения hello автоматически обновляться при hello нового образа.</span><span class="sxs-lookup"><span data-stu-id="3fd39-132">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fd39-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3fd39-133">Next steps</span></span>
* [<span data-ttu-id="3fd39-134">Что такое веб-приложение Azure на платформе Linux?</span><span class="sxs-lookup"><span data-stu-id="3fd39-134">What is Azure Web App on Linux?</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="3fd39-135">Реестр контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="3fd39-135">Azure Container Registry</span></span>](https://azure.microsoft.com/en-us/services/container-registry/)
* [<span data-ttu-id="3fd39-136">Использование конфигурации PM2 для Node.js в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="3fd39-136">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="3fd39-137">Использование .NET Core в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="3fd39-137">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="3fd39-138">Использование Ruby в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="3fd39-138">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="3fd39-139">Как toouse пользовательские Docker изображения для веб-приложения Azure в Linux</span><span class="sxs-lookup"><span data-stu-id="3fd39-139">How toouse a custom Docker image for Azure Web App on Linux</span></span>](./app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="3fd39-140">Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="3fd39-140">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md) 
* [<span data-ttu-id="3fd39-141">Управление веб-приложением на платформе Linux с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3fd39-141">Manage Web App on Linux using Azure CLI 2.0</span></span>](./app-service-linux-cli.md)



