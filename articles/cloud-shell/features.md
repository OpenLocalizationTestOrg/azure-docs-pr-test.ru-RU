---
title: "Функции Azure Cloud Shell (предварительная версия) | Документация Майкрософт"
description: "Обзор функций Azure Cloud Shell."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 67f03d5857e37b253ac57536e289b5468d69e9b5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a><span data-ttu-id="475b8-103">Функции и средства Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="475b8-103">Features and Tools for Azure Cloud Shell</span></span>
<span data-ttu-id="475b8-104">Azure Cloud Shell — это браузерная оболочка, предназначенная для разработки ресурсов Azure и управления ими.</span><span class="sxs-lookup"><span data-stu-id="475b8-104">Azure Cloud Shell is a browser-based shell experience to manage and develop Azure resources.</span></span>

<span data-ttu-id="475b8-105">Cloud Shell предлагает предварительно настроенную и доступную из браузера оболочку для управления ресурсами Azure, которая избавит вас от необходимости самостоятельно устанавливать ПО, управлять версиями и обслуживать компьютер.</span><span class="sxs-lookup"><span data-stu-id="475b8-105">Cloud Shell offers a browser-accessible, pre-configured shell experience for managing Azure resources without the overhead of installing, versioning, and maintaining a machine yourself.</span></span>

<span data-ttu-id="475b8-106">Cloud Shell подготавливает компьютеры по запросу, в результате чего состояние компьютера не сохраняется между сеансами.</span><span class="sxs-lookup"><span data-stu-id="475b8-106">Cloud Shell provisions machines on a per-request basis and as a result machine state will not persist across sessions.</span></span> <span data-ttu-id="475b8-107">Поскольку Cloud Shell создана для интерактивных сеансов, оболочки автоматически завершают работу после 20 минут бездействия.</span><span class="sxs-lookup"><span data-stu-id="475b8-107">Since Cloud Shell is built for interactive sessions, shells automatically terminate after 20 minutes of shell inactivity.</span></span>

## <a name="bash-in-cloud-shell"></a><span data-ttu-id="475b8-108">Bash в Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="475b8-108">Bash in Cloud Shell</span></span>
### <a name="tools"></a><span data-ttu-id="475b8-109">Средства</span><span class="sxs-lookup"><span data-stu-id="475b8-109">Tools</span></span>
|<span data-ttu-id="475b8-110">Категория</span><span class="sxs-lookup"><span data-stu-id="475b8-110">Category</span></span>   |<span data-ttu-id="475b8-111">Имя</span><span class="sxs-lookup"><span data-stu-id="475b8-111">Name</span></span>   |
|---|---|
|<span data-ttu-id="475b8-112">Интерпретатор оболочки Linux</span><span class="sxs-lookup"><span data-stu-id="475b8-112">Linux shell interpreter</span></span>|<span data-ttu-id="475b8-113">Bash</span><span class="sxs-lookup"><span data-stu-id="475b8-113">Bash</span></span><br> <span data-ttu-id="475b8-114">sh</span><span class="sxs-lookup"><span data-stu-id="475b8-114">sh</span></span>               |
|<span data-ttu-id="475b8-115">Инструменты Azure</span><span class="sxs-lookup"><span data-stu-id="475b8-115">Azure tools</span></span>            |<span data-ttu-id="475b8-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) и [1.0](https://github.com/Azure/azure-xplat-cli)</span><span class="sxs-lookup"><span data-stu-id="475b8-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) and [1.0](https://github.com/Azure/azure-xplat-cli)</span></span><br> [<span data-ttu-id="475b8-117">AzCopy</span><span class="sxs-lookup"><span data-stu-id="475b8-117">AzCopy</span></span>](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [<span data-ttu-id="475b8-118">Batch Shipyard</span><span class="sxs-lookup"><span data-stu-id="475b8-118">Batch Shipyard</span></span>](https://github.com/Azure/batch-shipyard)     |
|<span data-ttu-id="475b8-119">Текстовые редакторы</span><span class="sxs-lookup"><span data-stu-id="475b8-119">Text editors</span></span>           |<span data-ttu-id="475b8-120">vim</span><span class="sxs-lookup"><span data-stu-id="475b8-120">vim</span></span><br> <span data-ttu-id="475b8-121">nano</span><span class="sxs-lookup"><span data-stu-id="475b8-121">nano</span></span><br> <span data-ttu-id="475b8-122">emacs</span><span class="sxs-lookup"><span data-stu-id="475b8-122">emacs</span></span>       |
|<span data-ttu-id="475b8-123">Система управления версиями</span><span class="sxs-lookup"><span data-stu-id="475b8-123">Source control</span></span>         |<span data-ttu-id="475b8-124">git</span><span class="sxs-lookup"><span data-stu-id="475b8-124">git</span></span>                    |
|<span data-ttu-id="475b8-125">Инструменты сборки</span><span class="sxs-lookup"><span data-stu-id="475b8-125">Build tools</span></span>            |<span data-ttu-id="475b8-126">make</span><span class="sxs-lookup"><span data-stu-id="475b8-126">make</span></span><br> <span data-ttu-id="475b8-127">maven</span><span class="sxs-lookup"><span data-stu-id="475b8-127">maven</span></span><br> <span data-ttu-id="475b8-128">npm</span><span class="sxs-lookup"><span data-stu-id="475b8-128">npm</span></span><br> <span data-ttu-id="475b8-129">pip</span><span class="sxs-lookup"><span data-stu-id="475b8-129">pip</span></span>         |
|<span data-ttu-id="475b8-130">Контейнеры</span><span class="sxs-lookup"><span data-stu-id="475b8-130">Containers</span></span>             |<span data-ttu-id="475b8-131">[Docker CLI](https://github.com/docker/cli)/[Компьютер Docker](https://github.com/docker/machine)</span><span class="sxs-lookup"><span data-stu-id="475b8-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span></span><br> [<span data-ttu-id="475b8-132">Kubectl</span><span class="sxs-lookup"><span data-stu-id="475b8-132">Kubectl</span></span>](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [<span data-ttu-id="475b8-133">Draft</span><span class="sxs-lookup"><span data-stu-id="475b8-133">Draft</span></span>](https://github.com/Azure/draft)<br> [<span data-ttu-id="475b8-134">Интерфейс командной строки DC/OS</span><span class="sxs-lookup"><span data-stu-id="475b8-134">DC/OS CLI</span></span>](https://github.com/dcos/dcos-cli)         |
|<span data-ttu-id="475b8-135">Базы данных</span><span class="sxs-lookup"><span data-stu-id="475b8-135">Databases</span></span>              |<span data-ttu-id="475b8-136">Клиент MySQL</span><span class="sxs-lookup"><span data-stu-id="475b8-136">MySQL client</span></span><br> <span data-ttu-id="475b8-137">Клиент PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="475b8-137">PostgreSql client</span></span><br> [<span data-ttu-id="475b8-138">Служебная программа sqlcmd</span><span class="sxs-lookup"><span data-stu-id="475b8-138">sqlcmd Utility</span></span>](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [<span data-ttu-id="475b8-139">mssql-scripter</span><span class="sxs-lookup"><span data-stu-id="475b8-139">mssql-scripter</span></span>](https://github.com/Microsoft/sql-xplat-cli) |
|<span data-ttu-id="475b8-140">Другие</span><span class="sxs-lookup"><span data-stu-id="475b8-140">Other</span></span>                  |<span data-ttu-id="475b8-141">Клиент iPython</span><span class="sxs-lookup"><span data-stu-id="475b8-141">iPython Client</span></span><br> [<span data-ttu-id="475b8-142">Интерфейс командной строки Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="475b8-142">Cloud Foundry CLI</span></span>](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a><span data-ttu-id="475b8-143">Поддержка языков</span><span class="sxs-lookup"><span data-stu-id="475b8-143">Language support</span></span>
|<span data-ttu-id="475b8-144">язык</span><span class="sxs-lookup"><span data-stu-id="475b8-144">Language</span></span>   |<span data-ttu-id="475b8-145">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="475b8-145">Version</span></span>   |
|---|---|
|<span data-ttu-id="475b8-146">.NET</span><span class="sxs-lookup"><span data-stu-id="475b8-146">.NET</span></span>       |<span data-ttu-id="475b8-147">1.01</span><span class="sxs-lookup"><span data-stu-id="475b8-147">1.01</span></span>       |
|<span data-ttu-id="475b8-148">Go</span><span class="sxs-lookup"><span data-stu-id="475b8-148">Go</span></span>         |<span data-ttu-id="475b8-149">1.7</span><span class="sxs-lookup"><span data-stu-id="475b8-149">1.7</span></span>        |
|<span data-ttu-id="475b8-150">Java</span><span class="sxs-lookup"><span data-stu-id="475b8-150">Java</span></span>       |<span data-ttu-id="475b8-151">1.8</span><span class="sxs-lookup"><span data-stu-id="475b8-151">1.8</span></span>        |
|<span data-ttu-id="475b8-152">Node.js</span><span class="sxs-lookup"><span data-stu-id="475b8-152">Node.js</span></span>    |<span data-ttu-id="475b8-153">6.9.4</span><span class="sxs-lookup"><span data-stu-id="475b8-153">6.9.4</span></span>      |
|<span data-ttu-id="475b8-154">Python</span><span class="sxs-lookup"><span data-stu-id="475b8-154">Python</span></span>     |<span data-ttu-id="475b8-155">2.7 и 3.5 (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="475b8-155">2.7 and 3.5 (default)</span></span>|

## <a name="secure-automatic-authentication"></a><span data-ttu-id="475b8-156">Безопасная автоматическая аутентификация</span><span class="sxs-lookup"><span data-stu-id="475b8-156">Secure automatic authentication</span></span>
<span data-ttu-id="475b8-157">Cloud Shell безопасно и автоматически выполняет аутентификацию доступа к учетной записи для Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="475b8-157">Cloud Shell securely and automatically authenticates account access for the Azure CLI 2.0.</span></span>

## <a name="azure-files-persistence"></a><span data-ttu-id="475b8-158">Сохраняемость файлов Azure</span><span class="sxs-lookup"><span data-stu-id="475b8-158">Azure Files persistence</span></span>
<span data-ttu-id="475b8-159">Поскольку Cloud Shell выделяется по запросу с использованием временного компьютера, файлы за пределами каталога $Home и сведения о состоянии компьютера не сохраняются между сеансами.</span><span class="sxs-lookup"><span data-stu-id="475b8-159">Since Cloud Shell is allocated on a per-request basis using a temporary machine, files outside of your $Home and machine state are not persisted across sessions.</span></span>
<span data-ttu-id="475b8-160">Чтобы сохранять файлы между сеансами, при первом запуске Cloud Shell предлагается присоединить общую папку Azure.</span><span class="sxs-lookup"><span data-stu-id="475b8-160">To persist files across sessions, Cloud Shell walks you through attaching an Azure file share on first launch.</span></span>
<span data-ttu-id="475b8-161">По завершении настройки Cloud Shell будет автоматически присоединять хранилище для всех будущих сеансов.</span><span class="sxs-lookup"><span data-stu-id="475b8-161">Once completed Cloud Shell will automatically attach your storage for all future sessions.</span></span>

<span data-ttu-id="475b8-162">Дополнительные сведения см. в статье [Сохранение файлов в Azure Cloud Shell](persisting-shell-storage.md).</span><span class="sxs-lookup"><span data-stu-id="475b8-162">[Learn more about attaching Azure file shares to Cloud Shell.](persisting-shell-storage.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="475b8-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="475b8-163">Next steps</span></span>
[<span data-ttu-id="475b8-164">Краткое руководство по Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="475b8-164">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="475b8-165">
[Подробное описание Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="475b8-165">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br>