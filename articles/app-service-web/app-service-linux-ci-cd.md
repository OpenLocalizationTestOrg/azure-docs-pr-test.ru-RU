---
title: "Непрерывное развертывание для веб-приложения Azure на платформе Linux | Документы Майкрософт"
description: "Как настроить непрерывное развертывание в веб-приложении Azure на платформе Linux."
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
ms.openlocfilehash: f8f7d51003f8a55b7f51e8cc2cea838e8e5a6196
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a><span data-ttu-id="3dc0c-104">Непрерывное развертывание для веб-приложения Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="3dc0c-104">Continuous deployment with Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="3dc0c-105">В этом руководстве описывается настройка непрерывного развертывания для настраиваемого образа контейнера из управляемых репозиториев [реестра контейнеров Azure](https://azure.microsoft.com/en-us/services/container-registry/) или [Docker Hub](https://hub.docker.com).</span><span class="sxs-lookup"><span data-stu-id="3dc0c-105">In this tutorial, you configure continuous deployment for a custom container image from Managed [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span></span>

## <a name="step-1---sign-in-to-azure"></a><span data-ttu-id="3dc0c-106">Шаг 1. Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="3dc0c-106">Step 1 - Sign in to Azure</span></span>

<span data-ttu-id="3dc0c-107">Войдите на портал Azure по адресу http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="3dc0c-107">Sign in to the Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---enable-container-continuous-deployment-feature"></a><span data-ttu-id="3dc0c-108">Шаг 2. Включение функции непрерывного развертывания контейнера</span><span class="sxs-lookup"><span data-stu-id="3dc0c-108">Step 2 - Enable container continuous deployment feature</span></span>

<span data-ttu-id="3dc0c-109">Включить функцию непрерывного развертывания можно с помощью [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) и выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3dc0c-109">You can enable the continuous deployment feature using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing the following command</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

<span data-ttu-id="3dc0c-110">На **[портале Azure](https://portal.azure.com/)** щелкните **Служба приложений** в левой части страницы.</span><span class="sxs-lookup"><span data-stu-id="3dc0c-110">In the **[Azure portal](https://portal.azure.com/)**, click the **App Service** option on the left of the page.</span></span>

<span data-ttu-id="3dc0c-111">Щелкните имя приложения, для которого вы хотите настроить непрерывное развертывание Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="3dc0c-111">Click on the name of your app that you want to configure Docker Hub continuous deployment for.</span></span>

<span data-ttu-id="3dc0c-112">В разделе **Параметры приложения** добавьте параметр приложения `DOCKER_ENABLE_CI` со значением `true`.</span><span class="sxs-lookup"><span data-stu-id="3dc0c-112">In the **App settings**, add an app setting called `DOCKER_ENABLE_CI` with the value `true`.</span></span>

![Изображение добавления параметра приложения](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a><span data-ttu-id="3dc0c-114">Шаг 3 . Подготовка URL-адреса Webhook</span><span class="sxs-lookup"><span data-stu-id="3dc0c-114">Step 3 - Prepare Webhook URL</span></span>

<span data-ttu-id="3dc0c-115">Получить URL-адрес можно с помощью [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) и выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3dc0c-115">You can obtain the Webhook URL using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing the following command</span></span>

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

<span data-ttu-id="3dc0c-116">Для URL-адреса webhook необходима следующая конечная точка: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span><span class="sxs-lookup"><span data-stu-id="3dc0c-116">For the Webhook URL, you need to have the following endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span></span>

<span data-ttu-id="3dc0c-117">Вы можете получить `publishingusername` и `publishingpwd`, скачав профиль публикации веб-приложения с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="3dc0c-117">You can obtain your `publishingusername` and `publishingpwd` by downloading the web app publish profile using the Azure portal.</span></span>

![Изображение добавления webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a><span data-ttu-id="3dc0c-119">Шаг 4. Добавление webhook</span><span class="sxs-lookup"><span data-stu-id="3dc0c-119">Step 4 - Add a web hook</span></span>

### <a name="azure-container-registry"></a><span data-ttu-id="3dc0c-120">Реестр контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="3dc0c-120">Azure Container Registry</span></span>

<span data-ttu-id="3dc0c-121">В колонке реестра щелкните **Webhooks** (Объекты webhook), создайте webhook, нажав кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3dc0c-121">In your registry portal blade, click **Webhooks**, create a new webhook by clicking **Add**.</span></span> <span data-ttu-id="3dc0c-122">В колонке **Создание webhook** задайте имя для webhook.</span><span class="sxs-lookup"><span data-stu-id="3dc0c-122">In the **Create webhook** blade, give your webhook a name.</span></span> <span data-ttu-id="3dc0c-123">В качестве URI webhook необходимо указать URL-адрес, полученный на **шаге 3**.</span><span class="sxs-lookup"><span data-stu-id="3dc0c-123">For the Webhook URI, you need to provide the URL obtained from **Step 3**</span></span>

<span data-ttu-id="3dc0c-124">Убедитесь, что вы определили область в качестве репозитория, который содержит образ контейнера.</span><span class="sxs-lookup"><span data-stu-id="3dc0c-124">Make sure that you define the scope as the repo that contains your container image.</span></span>

![изображение webhook](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

<span data-ttu-id="3dc0c-126">При обновлении образа веб-приложение будет автоматически обновлено с использованием нового образа.</span><span class="sxs-lookup"><span data-stu-id="3dc0c-126">When the image gets updated, the web app get updated automatically with the new image.</span></span>

### <a name="docker-hub"></a><span data-ttu-id="3dc0c-127">Docker Hub</span><span class="sxs-lookup"><span data-stu-id="3dc0c-127">Docker Hub</span></span>

<span data-ttu-id="3dc0c-128">На своей странице Docker Hub щелкните **Webhooks** (Объекты webhook), затем щелкните **CREATE A WEBHOOK** (Создать webhook).</span><span class="sxs-lookup"><span data-stu-id="3dc0c-128">In your Docker Hub page, click **Webhooks**, then **CREATE A WEBHOOK**.</span></span>

![Изображение добавления webhook 1](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

<span data-ttu-id="3dc0c-130">В качестве URL-адреса Webhook необходимо указать URL-адрес, полученный на **шаге 3**.</span><span class="sxs-lookup"><span data-stu-id="3dc0c-130">For the Webhook URL, you need to provide the URL obtained from **Step 3**</span></span>

![Изображение добавления webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

<span data-ttu-id="3dc0c-132">При обновлении образа веб-приложение будет автоматически обновлено с использованием нового образа.</span><span class="sxs-lookup"><span data-stu-id="3dc0c-132">When the image gets updated, the web app get updated automatically with the new image.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3dc0c-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3dc0c-133">Next steps</span></span>
* [<span data-ttu-id="3dc0c-134">Что такое веб-приложение Azure на платформе Linux?</span><span class="sxs-lookup"><span data-stu-id="3dc0c-134">What is Azure Web App on Linux?</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="3dc0c-135">Реестр контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="3dc0c-135">Azure Container Registry</span></span>](https://azure.microsoft.com/en-us/services/container-registry/)
* [<span data-ttu-id="3dc0c-136">Использование конфигурации PM2 для Node.js в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="3dc0c-136">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="3dc0c-137">Использование .NET Core в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="3dc0c-137">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="3dc0c-138">Использование Ruby в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="3dc0c-138">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="3dc0c-139">Как применить пользовательский образ Docker для веб-приложения Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="3dc0c-139">How to use a custom Docker image for Azure Web App on Linux</span></span>](./app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="3dc0c-140">Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="3dc0c-140">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md) 
* [<span data-ttu-id="3dc0c-141">Управление веб-приложением на платформе Linux с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3dc0c-141">Manage Web App on Linux using Azure CLI 2.0</span></span>](./app-service-linux-cli.md)



