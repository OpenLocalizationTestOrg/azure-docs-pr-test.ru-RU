---
title: "веб-приложения на платформе Linux с помощью Azure CLI 2.0 aaaManage | Документы Microsoft"
description: "Управляйте веб-приложением на платформе Linux с помощью Azure CLI."
keywords: "служба приложений azure, веб-приложение, cli, linux, oss"
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
ms.date: 08/22/2017
ms.author: aelnably
ms.openlocfilehash: 5e8e0da8a362450c56d2e87e087f77598ec874ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a><span data-ttu-id="524e4-104">Управление веб-приложением на платформе Linux с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="524e4-104">Manage Web App on Linux using Azure CLI</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="524e4-105">С помощью команд hello в этой статье вы можете toocreate и управлять веб-приложения на платформе Linux с помощью Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="524e4-105">Using hello commands in this article you are able toocreate and manage a Web App on Linux using Azure CLI 2.0.</span></span>
<span data-ttu-id="524e4-106">Можно приступить к использованию новой версии hello hello CLI двумя способами:</span><span class="sxs-lookup"><span data-stu-id="524e4-106">You can start using hello new version of hello CLI in two ways:</span></span>

* <span data-ttu-id="524e4-107">[установить Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) на компьютер;</span><span class="sxs-lookup"><span data-stu-id="524e4-107">[Installing Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span>
* <span data-ttu-id="524e4-108">использовать [Azure Cloud Shell (предварительная версия)](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="524e4-108">Using [Azure Cloud Shell (Preview)](../cloud-shell/overview.md)</span></span>


## <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="524e4-109">Создание плана службы приложений Linux</span><span class="sxs-lookup"><span data-stu-id="524e4-109">Create a Linux App Service Plan</span></span>

<span data-ttu-id="524e4-110">toocreate план службы Linux приложений, можно использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="524e4-110">toocreate a Linux App Service Plan, you can use hello following command:</span></span>

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a><span data-ttu-id="524e4-111">Создание пользовательского веб-приложения контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="524e4-111">Create a custom Docker container Web App</span></span>

<span data-ttu-id="524e4-112">toocreate веб-приложения и его настройки toorun пользовательский контейнер Docker, можно использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="524e4-112">toocreate a web app and configuring it toorun a custom Docker container, you can use hello following command:</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-hello-docker-container-logging"></a><span data-ttu-id="524e4-113">Активация ведения журнала контейнера Docker hello</span><span class="sxs-lookup"><span data-stu-id="524e4-113">Activate hello Docker container logging</span></span>

<span data-ttu-id="524e4-114">tooactivate Здравствуйте ведения журнала контейнера Docker, можно использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="524e4-114">tooactivate hello Docker container logging, you can use hello following command:</span></span>

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-hello-custom-docker-container-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="524e4-115">Изменить пользовательский контейнер Docker hello для существующего веб-приложения, для приложения Linux</span><span class="sxs-lookup"><span data-stu-id="524e4-115">Change hello custom Docker container for an existing Web App on Linux App</span></span>

<span data-ttu-id="524e4-116">toochange ранее созданное приложение, из hello текущего изображения tooa нового образа Docker, можно использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="524e4-116">toochange a previously created app, from hello current Docker image tooa new image, you can use hello following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a><span data-ttu-id="524e4-117">Использование образов Docker из частного реестра</span><span class="sxs-lookup"><span data-stu-id="524e4-117">Using Docker images from a private registry</span></span>

<span data-ttu-id="524e4-118">Вы можете настроить toouse изображений для вашего приложения из частного реестра.</span><span class="sxs-lookup"><span data-stu-id="524e4-118">You can configure your app toouse images from a private registry.</span></span> <span data-ttu-id="524e4-119">Требуется URL-адрес hello tooprovide для реестра, имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="524e4-119">You need tooprovide hello url for your registry, user name, and password.</span></span> <span data-ttu-id="524e4-120">Это можно сделать с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="524e4-120">This can be achieved using hello following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a><span data-ttu-id="524e4-121">Включение непрерывного развертывания для пользовательских образов Docker</span><span class="sxs-lookup"><span data-stu-id="524e4-121">Enable continuous deployments for custom Docker images</span></span>

<span data-ttu-id="524e4-122">С hello следующую команду можно включить функции hello компакт-диска и получить URL-адрес веб-перехватчика hello.</span><span class="sxs-lookup"><span data-stu-id="524e4-122">With hello following command you can enable hello CD functionality, and get hello webhook url.</span></span> <span data-ttu-id="524e4-123">Этот URL-адрес может быть используется tooconfigure вы DockerHub или реестр контейнера Azure репозиториев.</span><span class="sxs-lookup"><span data-stu-id="524e4-123">This url can be used tooconfigure you DockerHub or Azure Container Registry repos.</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a><span data-ttu-id="524e4-124">Создание веб-приложения в приложении Linux с помощью одной из наших встроенных платформ среды выполнения</span><span class="sxs-lookup"><span data-stu-id="524e4-124">Create a Web App on Linux App using one of our built-in runtime frameworks</span></span>

<span data-ttu-id="524e4-125">toocreate веб-приложения PHP 5.6 приложения Linux, можно использовать следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="524e4-125">toocreate a PHP 5.6 Web App on Linux App that, you can use hello following command.</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="524e4-126">Изменение версии платформы для имеющегося веб-приложения в приложении Linux</span><span class="sxs-lookup"><span data-stu-id="524e4-126">Change framework version for an existing Web App on Linux App</span></span>

<span data-ttu-id="524e4-127">toochange ранее созданное приложение, из версии tooNode.js hello текущего framework 6.11 можно использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="524e4-127">toochange a previously created app, from hello current framework version tooNode.js 6.11, you can use hello following command:</span></span>

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a><span data-ttu-id="524e4-128">Настройка развертываний Git для веб-приложения</span><span class="sxs-lookup"><span data-stu-id="524e4-128">Set up Git deployments for your Web App</span></span>

<span data-ttu-id="524e4-129">tooset копирование Git развертывания для приложения можно использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="524e4-129">tooset up Git deployments for your app, you can use hello following command:</span></span>

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a><span data-ttu-id="524e4-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="524e4-130">Next steps</span></span>
* [<span data-ttu-id="524e4-131">Что такое веб-приложение Azure на платформе Linux?</span><span class="sxs-lookup"><span data-stu-id="524e4-131">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* <span data-ttu-id="524e4-132">[Установите Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="524e4-132">[Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)</span></span>
* [<span data-ttu-id="524e4-133">Обзор Azure Cloud Shell (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="524e4-133">Azure Cloud Shell (Preview)</span></span>](../cloud-shell/overview.md)
* [<span data-ttu-id="524e4-134">Настройка промежуточных сред в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="524e4-134">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="524e4-135">Непрерывное развертывание для веб-приложения Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="524e4-135">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
