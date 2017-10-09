---
title: "aaaAzure примеры PowerShell — службы приложений | Документы Microsoft"
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
ms.openlocfilehash: b7b4a030364f797195522c56fbae5b7f530d4d1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples"></a><span data-ttu-id="1cba5-103">Примеры сценариев Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1cba5-103">Azure PowerShell Samples</span></span>

<span data-ttu-id="1cba5-104">Hello следующей таблице представлены ссылки toobash сценариев, созданных с использованием hello Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1cba5-104">hello following table includes links toobash scripts built using hello Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="1cba5-105">**Создание приложения**</span><span class="sxs-lookup"><span data-stu-id="1cba5-105">**Create app**</span></span>||
| [<span data-ttu-id="1cba5-106">Создание веб-приложения с непрерывным развертыванием из GitHub</span><span class="sxs-lookup"><span data-stu-id="1cba5-106">Create a web app with deployment from GitHub</span></span>](./scripts/app-service-powershell-deploy-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="1cba5-107">Создает веб-приложение Azure, получающее код из GitHub.</span><span class="sxs-lookup"><span data-stu-id="1cba5-107">Creates an Azure web app which pulls code from GitHub.</span></span> |
| [<span data-ttu-id="1cba5-108">Создание веб-приложения с непрерывным развертыванием из GitHub</span><span class="sxs-lookup"><span data-stu-id="1cba5-108">Create a web app with continuous deployment from GitHub</span></span>](./scripts/app-service-powershell-continuous-deployment-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="1cba5-109">Создает веб-приложение Azure, непрерывно развертывающее код из GitHub.</span><span class="sxs-lookup"><span data-stu-id="1cba5-109">Creates an Azure web app which continuously deploys code from GitHub.</span></span> |
| [<span data-ttu-id="1cba5-110">Создание веб-приложения и развертывание кода с помощью протокола FTP</span><span class="sxs-lookup"><span data-stu-id="1cba5-110">Create a web app and deploy code with FTP</span></span>](./scripts/app-service-powershell-deploy-ftp.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="1cba5-111">Создает веб-приложение Azure и передает файлы из локального каталога с помощью протокола FTP.</span><span class="sxs-lookup"><span data-stu-id="1cba5-111">Creates an Azure web app and upload files from a local directory using FTP.</span></span> |
| [<span data-ttu-id="1cba5-112">Создание веб-приложения и развертывание кода из локального репозитория Git</span><span class="sxs-lookup"><span data-stu-id="1cba5-112">Create a web app and deploy code from a local Git repository</span></span>](./scripts/app-service-powershell-deploy-local-git.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="1cba5-113">Создает веб-приложение Azure и настраивает отправку кода из локального репозитория Git.</span><span class="sxs-lookup"><span data-stu-id="1cba5-113">Creates an Azure web app and configures code push from a local Git repository.</span></span> |
| [<span data-ttu-id="1cba5-114">Создание веб-приложения и развертывание кода tooa промежуточной среде</span><span class="sxs-lookup"><span data-stu-id="1cba5-114">Create a web app and deploy code tooa staging environment</span></span>](./scripts/app-service-powershell-deploy-staging-environment.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="1cba5-115">Создает веб-приложение Azure со слотом развертывания для изменений промежуточного кода.</span><span class="sxs-lookup"><span data-stu-id="1cba5-115">Creates an Azure web app with a deployment slot for staging code changes.</span></span> |
|<span data-ttu-id="1cba5-116">**Настройка приложения**</span><span class="sxs-lookup"><span data-stu-id="1cba5-116">**Configure app**</span></span>||
| [<span data-ttu-id="1cba5-117">Карта пользовательского домена tooa веб-приложения</span><span class="sxs-lookup"><span data-stu-id="1cba5-117">Map a custom domain tooa web app</span></span>](./scripts/app-service-powershell-configure-custom-domain.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="1cba5-118">Создает веб-приложение Azure и сопоставляет tooit имя пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="1cba5-118">Creates an Azure web app and maps a custom domain name tooit.</span></span> |
| [<span data-ttu-id="1cba5-119">Привязка пользовательских веб-приложения tooa SSL сертификата</span><span class="sxs-lookup"><span data-stu-id="1cba5-119">Bind a custom SSL certificate tooa web app</span></span>](./scripts/app-service-powershell-configure-ssl-certificate.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="1cba5-120">Создает веб-приложение Azure и привязывает hello SSL-сертификат tooit имя пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="1cba5-120">Creates an Azure web app and binds hello SSL certificate of a custom domain name tooit.</span></span> |
|<span data-ttu-id="1cba5-121">**Масштабирование приложения**</span><span class="sxs-lookup"><span data-stu-id="1cba5-121">**Scale app**</span></span>||
| [<span data-ttu-id="1cba5-122">Масштабирование веб-приложения вручную</span><span class="sxs-lookup"><span data-stu-id="1cba5-122">Scale a web app manually</span></span>](./scripts/app-service-powershell-scale-manual.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="1cba5-123">Создает веб-приложение Azure и масштабирует его по двум экземплярам.</span><span class="sxs-lookup"><span data-stu-id="1cba5-123">Creates an Azure web app and scales it across 2 instances.</span></span> |
| [<span data-ttu-id="1cba5-124">Глобальное масштабирование веб-приложения с помощью высокодоступной архитектуры</span><span class="sxs-lookup"><span data-stu-id="1cba5-124">Scale a web app worldwide with a high-availability architecture</span></span>](./scripts/app-service-powershell-scale-high-availability.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="1cba5-125">Создает два веб-приложения Azure в двух разных географических регионах и делает их доступными через одну конечную точку с помощью диспетчера трафика Azure.</span><span class="sxs-lookup"><span data-stu-id="1cba5-125">Creates two Azure web apps in two different geographical regions and makes them available through a single endpoint using Azure Traffic Manager.</span></span> |
|<span data-ttu-id="1cba5-126">**Подключение приложения tooresources**</span><span class="sxs-lookup"><span data-stu-id="1cba5-126">**Connect app tooresources**</span></span>||
| [<span data-ttu-id="1cba5-127">Подключение web app tooa базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="1cba5-127">Connect a web app tooa SQL Database</span></span>](./scripts/app-service-powershell-connect-to-sql.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="1cba5-128">Создает веб-приложение Azure и базы данных SQL, а затем добавляет параметры приложения toohello строки подключения hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="1cba5-128">Creates an Azure web app and a SQL database, then adds hello database connection string toohello app settings.</span></span> |
| [<span data-ttu-id="1cba5-129">Подключение приложения web tooa учетной записи хранилища</span><span class="sxs-lookup"><span data-stu-id="1cba5-129">Connect a web app tooa storage account</span></span>](./scripts/app-service-powershell-connect-to-storage.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="1cba5-130">Создает веб-приложение Azure и учетной записи хранилища, а затем добавляет параметры приложения toohello строки подключения хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="1cba5-130">Creates an Azure web app and a storage account, then adds hello storage connection string toohello app settings.</span></span> |
|<span data-ttu-id="1cba5-131">**Мониторинг приложения**</span><span class="sxs-lookup"><span data-stu-id="1cba5-131">**Monitor app**</span></span>||
| [<span data-ttu-id="1cba5-132">Мониторинг веб-приложения с помощью журналов веб-сервера</span><span class="sxs-lookup"><span data-stu-id="1cba5-132">Monitor a web app with web server logs</span></span>](./scripts/app-service-powershell-monitor.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="1cba5-133">Создает веб-приложение Azure, ведение журнала для него и загружает hello журналы tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="1cba5-133">Creates an Azure web app, enables logging for it, and downloads hello logs tooyour local machine.</span></span> |
| | |
