---
title: "Управление веб-приложением на платформе Linux с помощью Azure CLI 2.0 | Документация Майкрософт"
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
ms.openlocfilehash: 04aceecf0cb4cad5c838b7254bf7079a36bbd0d8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a><span data-ttu-id="e96dd-104">Управление веб-приложением на платформе Linux с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e96dd-104">Manage Web App on Linux using Azure CLI</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="e96dd-105">Используя команды в этой статье, вы сможете создать веб-приложение на платформе Linux с помощью Azure CLI 2.0 и управлять им.</span><span class="sxs-lookup"><span data-stu-id="e96dd-105">Using the commands in this article you are able to create and manage a Web App on Linux using Azure CLI 2.0.</span></span>
<span data-ttu-id="e96dd-106">Начать использовать новую версию CLI можно двумя способами:</span><span class="sxs-lookup"><span data-stu-id="e96dd-106">You can start using the new version of the CLI in two ways:</span></span>

* <span data-ttu-id="e96dd-107">[установить Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) на компьютер;</span><span class="sxs-lookup"><span data-stu-id="e96dd-107">[Installing Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span>
* <span data-ttu-id="e96dd-108">использовать [Azure Cloud Shell (предварительная версия)](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="e96dd-108">Using [Azure Cloud Shell (Preview)](../cloud-shell/overview.md)</span></span>


## <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="e96dd-109">Создание плана службы приложений Linux</span><span class="sxs-lookup"><span data-stu-id="e96dd-109">Create a Linux App Service Plan</span></span>

<span data-ttu-id="e96dd-110">Чтобы создать план службы приложений Linux, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e96dd-110">To create a Linux App Service Plan, you can use the following command:</span></span>

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a><span data-ttu-id="e96dd-111">Создание пользовательского веб-приложения контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="e96dd-111">Create a custom Docker container Web App</span></span>

<span data-ttu-id="e96dd-112">Чтобы создать веб-приложение и настроить его для запуска пользовательского контейнера Docker, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e96dd-112">To create a web app and configuring it to run a custom Docker container, you can use the following command:</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-the-docker-container-logging"></a><span data-ttu-id="e96dd-113">Активация ведения журнала контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="e96dd-113">Activate the Docker container logging</span></span>

<span data-ttu-id="e96dd-114">Чтобы включить ведение журнала для контейнера Docker, можно использовать следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e96dd-114">To activate the Docker container logging, you can use the following command:</span></span>

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-the-custom-docker-container-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="e96dd-115">Изменение пользовательского контейнера Docker для имеющегося веб-приложения в приложении Linux</span><span class="sxs-lookup"><span data-stu-id="e96dd-115">Change the custom Docker container for an existing Web App on Linux App</span></span>

<span data-ttu-id="e96dd-116">Чтобы изменить текущий образ Docker ранее созданного приложения на новый образ, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e96dd-116">To change a previously created app, from the current Docker image to a new image, you can use the following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a><span data-ttu-id="e96dd-117">Использование образов Docker из частного реестра</span><span class="sxs-lookup"><span data-stu-id="e96dd-117">Using Docker images from a private registry</span></span>

<span data-ttu-id="e96dd-118">Вы можете настроить свое приложение для использования образов из частного реестра.</span><span class="sxs-lookup"><span data-stu-id="e96dd-118">You can configure your app to use images from a private registry.</span></span> <span data-ttu-id="e96dd-119">Необходимо указать URL-адрес для реестра, имени пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="e96dd-119">You need to provide the url for your registry, user name, and password.</span></span> <span data-ttu-id="e96dd-120">Для этого выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e96dd-120">This can be achieved using the following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a><span data-ttu-id="e96dd-121">Включение непрерывного развертывания для пользовательских образов Docker</span><span class="sxs-lookup"><span data-stu-id="e96dd-121">Enable continuous deployments for custom Docker images</span></span>

<span data-ttu-id="e96dd-122">Выполните указанную ниже команду, чтобы обеспечить возможность использования компакт-диска и получить URL-адрес веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="e96dd-122">With the following command you can enable the CD functionality, and get the webhook url.</span></span> <span data-ttu-id="e96dd-123">Этот URL-адрес можно использовать для настройки репозиториев DockerHub или реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="e96dd-123">This url can be used to configure you DockerHub or Azure Container Registry repos.</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a><span data-ttu-id="e96dd-124">Создание веб-приложения в приложении Linux с помощью одной из наших встроенных платформ среды выполнения</span><span class="sxs-lookup"><span data-stu-id="e96dd-124">Create a Web App on Linux App using one of our built-in runtime frameworks</span></span>

<span data-ttu-id="e96dd-125">Чтобы создать веб-приложения PHP 5.6 в приложении Linux, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e96dd-125">To create a PHP 5.6 Web App on Linux App that, you can use the following command.</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="e96dd-126">Изменение версии платформы для имеющегося веб-приложения в приложении Linux</span><span class="sxs-lookup"><span data-stu-id="e96dd-126">Change framework version for an existing Web App on Linux App</span></span>

<span data-ttu-id="e96dd-127">Чтобы изменить ранее созданное приложение с текущей версии на Node.js 6.11, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e96dd-127">To change a previously created app, from the current framework version to Node.js 6.11, you can use the following command:</span></span>

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a><span data-ttu-id="e96dd-128">Настройка развертываний Git для веб-приложения</span><span class="sxs-lookup"><span data-stu-id="e96dd-128">Set up Git deployments for your Web App</span></span>

<span data-ttu-id="e96dd-129">Чтобы настроить развертывания Git для приложения, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e96dd-129">To set up Git deployments for your app, you can use the following command:</span></span>

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a><span data-ttu-id="e96dd-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e96dd-130">Next steps</span></span>
* [<span data-ttu-id="e96dd-131">Что такое веб-приложение Azure на платформе Linux?</span><span class="sxs-lookup"><span data-stu-id="e96dd-131">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* <span data-ttu-id="e96dd-132">[Установите Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e96dd-132">[Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)</span></span>
* [<span data-ttu-id="e96dd-133">Обзор Azure Cloud Shell (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="e96dd-133">Azure Cloud Shell (Preview)</span></span>](../cloud-shell/overview.md)
* [<span data-ttu-id="e96dd-134">Настройка промежуточных сред в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="e96dd-134">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="e96dd-135">Непрерывное развертывание для веб-приложения Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="e96dd-135">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
