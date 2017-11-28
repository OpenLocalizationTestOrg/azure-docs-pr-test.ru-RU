---
title: "Примеры Azure PowerShell. Служба приложений | Документация Майкрософт"
description: "Примеры Azure PowerShell для службы приложений."
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: b48d1137-8c04-46e0-b430-101e07d7e470
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 3254fdd57cfcd170f22374c1e3b058e6081d8e8e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples"></a><span data-ttu-id="c8c55-103">Примеры сценариев Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c8c55-103">Azure PowerShell Samples</span></span>

<span data-ttu-id="c8c55-104">В следующей таблице приведены ссылки на сценарии bash, созданные с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c8c55-104">The following table includes links to bash scripts built using the Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="c8c55-105">**Создание приложения**</span><span class="sxs-lookup"><span data-stu-id="c8c55-105">**Create app**</span></span>||
| [<span data-ttu-id="c8c55-106">Создание веб-приложения с непрерывным развертыванием из GitHub</span><span class="sxs-lookup"><span data-stu-id="c8c55-106">Create a web app with deployment from GitHub</span></span>](./scripts/app-service-powershell-deploy-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="c8c55-107">Создает веб-приложение Azure, получающее код из GitHub.</span><span class="sxs-lookup"><span data-stu-id="c8c55-107">Creates an Azure web app which pulls code from GitHub.</span></span> |
| [<span data-ttu-id="c8c55-108">Создание веб-приложения с непрерывным развертыванием из GitHub</span><span class="sxs-lookup"><span data-stu-id="c8c55-108">Create a web app with continuous deployment from GitHub</span></span>](./scripts/app-service-powershell-continuous-deployment-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="c8c55-109">Создает веб-приложение Azure, непрерывно развертывающее код из GitHub.</span><span class="sxs-lookup"><span data-stu-id="c8c55-109">Creates an Azure web app which continuously deploys code from GitHub.</span></span> |
| [<span data-ttu-id="c8c55-110">Создание веб-приложения и развертывание кода с помощью протокола FTP</span><span class="sxs-lookup"><span data-stu-id="c8c55-110">Create a web app and deploy code with FTP</span></span>](./scripts/app-service-powershell-deploy-ftp.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="c8c55-111">Создает веб-приложение Azure и передает файлы из локального каталога с помощью протокола FTP.</span><span class="sxs-lookup"><span data-stu-id="c8c55-111">Creates an Azure web app and upload files from a local directory using FTP.</span></span> |
| [<span data-ttu-id="c8c55-112">Создание веб-приложения и развертывание кода из локального репозитория Git</span><span class="sxs-lookup"><span data-stu-id="c8c55-112">Create a web app and deploy code from a local Git repository</span></span>](./scripts/app-service-powershell-deploy-local-git.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="c8c55-113">Создает веб-приложение Azure и настраивает отправку кода из локального репозитория Git.</span><span class="sxs-lookup"><span data-stu-id="c8c55-113">Creates an Azure web app and configures code push from a local Git repository.</span></span> |
| [<span data-ttu-id="c8c55-114">Создание веб-приложения и развертывание кода в промежуточной среде</span><span class="sxs-lookup"><span data-stu-id="c8c55-114">Create a web app and deploy code to a staging environment</span></span>](./scripts/app-service-powershell-deploy-staging-environment.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="c8c55-115">Создает веб-приложение Azure со слотом развертывания для изменений промежуточного кода.</span><span class="sxs-lookup"><span data-stu-id="c8c55-115">Creates an Azure web app with a deployment slot for staging code changes.</span></span> |
|<span data-ttu-id="c8c55-116">**Настройка приложения**</span><span class="sxs-lookup"><span data-stu-id="c8c55-116">**Configure app**</span></span>||
| [<span data-ttu-id="c8c55-117">Сопоставление пользовательского домена с веб-приложением</span><span class="sxs-lookup"><span data-stu-id="c8c55-117">Map a custom domain to a web app</span></span>](./scripts/app-service-powershell-configure-custom-domain.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="c8c55-118">Создает веб-приложение Azure и сопоставляет c ним имя пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="c8c55-118">Creates an Azure web app and maps a custom domain name to it.</span></span> |
| [<span data-ttu-id="c8c55-119">Привязка пользовательского SSL-сертификата к веб-приложению</span><span class="sxs-lookup"><span data-stu-id="c8c55-119">Bind a custom SSL certificate to a web app</span></span>](./scripts/app-service-powershell-configure-ssl-certificate.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="c8c55-120">Создает веб-приложение Azure и привязывает к нему SSL-сертификат имени личного домена.</span><span class="sxs-lookup"><span data-stu-id="c8c55-120">Creates an Azure web app and binds the SSL certificate of a custom domain name to it.</span></span> |
|<span data-ttu-id="c8c55-121">**Масштабирование приложения**</span><span class="sxs-lookup"><span data-stu-id="c8c55-121">**Scale app**</span></span>||
| [<span data-ttu-id="c8c55-122">Масштабирование веб-приложения вручную</span><span class="sxs-lookup"><span data-stu-id="c8c55-122">Scale a web app manually</span></span>](./scripts/app-service-powershell-scale-manual.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="c8c55-123">Создает веб-приложение Azure и масштабирует его по двум экземплярам.</span><span class="sxs-lookup"><span data-stu-id="c8c55-123">Creates an Azure web app and scales it across 2 instances.</span></span> |
| [<span data-ttu-id="c8c55-124">Глобальное масштабирование веб-приложения с помощью высокодоступной архитектуры</span><span class="sxs-lookup"><span data-stu-id="c8c55-124">Scale a web app worldwide with a high-availability architecture</span></span>](./scripts/app-service-powershell-scale-high-availability.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="c8c55-125">Создает два веб-приложения Azure в двух разных географических регионах и делает их доступными через одну конечную точку с помощью диспетчера трафика Azure.</span><span class="sxs-lookup"><span data-stu-id="c8c55-125">Creates two Azure web apps in two different geographical regions and makes them available through a single endpoint using Azure Traffic Manager.</span></span> |
|<span data-ttu-id="c8c55-126">**Подключение приложения к ресурсам**</span><span class="sxs-lookup"><span data-stu-id="c8c55-126">**Connect app to resources**</span></span>||
| [<span data-ttu-id="c8c55-127">Подключение веб-приложения к базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="c8c55-127">Connect a web app to a SQL Database</span></span>](./scripts/app-service-powershell-connect-to-sql.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="c8c55-128">Создает веб-приложение Azure и базу данных SQL, а затем добавляет строку подключения базы данных к параметрам приложения.</span><span class="sxs-lookup"><span data-stu-id="c8c55-128">Creates an Azure web app and a SQL database, then adds the database connection string to the app settings.</span></span> |
| [<span data-ttu-id="c8c55-129">Подключение веб-приложения к учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="c8c55-129">Connect a web app to a storage account</span></span>](./scripts/app-service-powershell-connect-to-storage.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="c8c55-130">Создает веб-приложение Azure и учетную запись хранения, а затем добавляет строку подключения хранилища к параметрам приложения.</span><span class="sxs-lookup"><span data-stu-id="c8c55-130">Creates an Azure web app and a storage account, then adds the storage connection string to the app settings.</span></span> |
|<span data-ttu-id="c8c55-131">**Мониторинг приложения**</span><span class="sxs-lookup"><span data-stu-id="c8c55-131">**Monitor app**</span></span>||
| [<span data-ttu-id="c8c55-132">Мониторинг веб-приложения с помощью журналов веб-сервера</span><span class="sxs-lookup"><span data-stu-id="c8c55-132">Monitor a web app with web server logs</span></span>](./scripts/app-service-powershell-monitor.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="c8c55-133">Создает веб-приложение Azure, включает ведение журналов и скачивает их на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="c8c55-133">Creates an Azure web app, enables logging for it, and downloads the logs to your local machine.</span></span> |
| | |
