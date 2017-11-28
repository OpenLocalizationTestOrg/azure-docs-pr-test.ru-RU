---
title: "возможности оболочки облака (Предварительная версия) aaaAzure | Документы Microsoft"
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
ms.openlocfilehash: 65482ca6caeac01dda18a6b12eabe943e3d68a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a><span data-ttu-id="ac1b0-103">Функции и средства Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="ac1b0-103">Features and Tools for Azure Cloud Shell</span></span>
<span data-ttu-id="ac1b0-104">Azure облачной оболочки является toomanage взаимодействие на основе браузера оболочки и разработке ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="ac1b0-104">Azure Cloud Shell is a browser-based shell experience toomanage and develop Azure resources.</span></span>

<span data-ttu-id="ac1b0-105">Облако оболочки предлагает браузер, доступный, предварительно настроенных качества оболочки для управления ресурсами Azure без издержек hello установки, управления версиями, и обслуживание компьютера самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="ac1b0-105">Cloud Shell offers a browser-accessible, pre-configured shell experience for managing Azure resources without hello overhead of installing, versioning, and maintaining a machine yourself.</span></span>

<span data-ttu-id="ac1b0-106">Cloud Shell подготавливает компьютеры по запросу, в результате чего состояние компьютера не сохраняется между сеансами.</span><span class="sxs-lookup"><span data-stu-id="ac1b0-106">Cloud Shell provisions machines on a per-request basis and as a result machine state will not persist across sessions.</span></span> <span data-ttu-id="ac1b0-107">Поскольку Cloud Shell создана для интерактивных сеансов, оболочки автоматически завершают работу после 20 минут бездействия.</span><span class="sxs-lookup"><span data-stu-id="ac1b0-107">Since Cloud Shell is built for interactive sessions, shells automatically terminate after 20 minutes of shell inactivity.</span></span>

## <a name="bash-in-cloud-shell"></a><span data-ttu-id="ac1b0-108">Bash в Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="ac1b0-108">Bash in Cloud Shell</span></span>
### <a name="tools"></a><span data-ttu-id="ac1b0-109">Средства</span><span class="sxs-lookup"><span data-stu-id="ac1b0-109">Tools</span></span>
|<span data-ttu-id="ac1b0-110">Категория</span><span class="sxs-lookup"><span data-stu-id="ac1b0-110">Category</span></span>   |<span data-ttu-id="ac1b0-111">Имя</span><span class="sxs-lookup"><span data-stu-id="ac1b0-111">Name</span></span>   |
|---|---|
|<span data-ttu-id="ac1b0-112">Интерпретатор оболочки Linux</span><span class="sxs-lookup"><span data-stu-id="ac1b0-112">Linux shell interpreter</span></span>|<span data-ttu-id="ac1b0-113">Bash</span><span class="sxs-lookup"><span data-stu-id="ac1b0-113">Bash</span></span><br> <span data-ttu-id="ac1b0-114">sh</span><span class="sxs-lookup"><span data-stu-id="ac1b0-114">sh</span></span>               |
|<span data-ttu-id="ac1b0-115">Инструменты Azure</span><span class="sxs-lookup"><span data-stu-id="ac1b0-115">Azure tools</span></span>            |<span data-ttu-id="ac1b0-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) и [1.0](https://github.com/Azure/azure-xplat-cli)</span><span class="sxs-lookup"><span data-stu-id="ac1b0-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) and [1.0](https://github.com/Azure/azure-xplat-cli)</span></span><br> [<span data-ttu-id="ac1b0-117">AzCopy</span><span class="sxs-lookup"><span data-stu-id="ac1b0-117">AzCopy</span></span>](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [<span data-ttu-id="ac1b0-118">Batch Shipyard</span><span class="sxs-lookup"><span data-stu-id="ac1b0-118">Batch Shipyard</span></span>](https://github.com/Azure/batch-shipyard)     |
|<span data-ttu-id="ac1b0-119">Текстовые редакторы</span><span class="sxs-lookup"><span data-stu-id="ac1b0-119">Text editors</span></span>           |<span data-ttu-id="ac1b0-120">vim</span><span class="sxs-lookup"><span data-stu-id="ac1b0-120">vim</span></span><br> <span data-ttu-id="ac1b0-121">nano</span><span class="sxs-lookup"><span data-stu-id="ac1b0-121">nano</span></span><br> <span data-ttu-id="ac1b0-122">emacs</span><span class="sxs-lookup"><span data-stu-id="ac1b0-122">emacs</span></span>       |
|<span data-ttu-id="ac1b0-123">Система управления версиями</span><span class="sxs-lookup"><span data-stu-id="ac1b0-123">Source control</span></span>         |<span data-ttu-id="ac1b0-124">git</span><span class="sxs-lookup"><span data-stu-id="ac1b0-124">git</span></span>                    |
|<span data-ttu-id="ac1b0-125">Инструменты сборки</span><span class="sxs-lookup"><span data-stu-id="ac1b0-125">Build tools</span></span>            |<span data-ttu-id="ac1b0-126">make</span><span class="sxs-lookup"><span data-stu-id="ac1b0-126">make</span></span><br> <span data-ttu-id="ac1b0-127">maven</span><span class="sxs-lookup"><span data-stu-id="ac1b0-127">maven</span></span><br> <span data-ttu-id="ac1b0-128">npm</span><span class="sxs-lookup"><span data-stu-id="ac1b0-128">npm</span></span><br> <span data-ttu-id="ac1b0-129">pip</span><span class="sxs-lookup"><span data-stu-id="ac1b0-129">pip</span></span>         |
|<span data-ttu-id="ac1b0-130">Контейнеры</span><span class="sxs-lookup"><span data-stu-id="ac1b0-130">Containers</span></span>             |<span data-ttu-id="ac1b0-131">[Docker CLI](https://github.com/docker/cli)/[Компьютер Docker](https://github.com/docker/machine)</span><span class="sxs-lookup"><span data-stu-id="ac1b0-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span></span><br> [<span data-ttu-id="ac1b0-132">Kubectl</span><span class="sxs-lookup"><span data-stu-id="ac1b0-132">Kubectl</span></span>](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [<span data-ttu-id="ac1b0-133">Draft</span><span class="sxs-lookup"><span data-stu-id="ac1b0-133">Draft</span></span>](https://github.com/Azure/draft)<br> [<span data-ttu-id="ac1b0-134">Интерфейс командной строки DC/OS</span><span class="sxs-lookup"><span data-stu-id="ac1b0-134">DC/OS CLI</span></span>](https://github.com/dcos/dcos-cli)         |
|<span data-ttu-id="ac1b0-135">Базы данных</span><span class="sxs-lookup"><span data-stu-id="ac1b0-135">Databases</span></span>              |<span data-ttu-id="ac1b0-136">Клиент MySQL</span><span class="sxs-lookup"><span data-stu-id="ac1b0-136">MySQL client</span></span><br> <span data-ttu-id="ac1b0-137">Клиент PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ac1b0-137">PostgreSql client</span></span><br> [<span data-ttu-id="ac1b0-138">Служебная программа sqlcmd</span><span class="sxs-lookup"><span data-stu-id="ac1b0-138">sqlcmd Utility</span></span>](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [<span data-ttu-id="ac1b0-139">mssql-scripter</span><span class="sxs-lookup"><span data-stu-id="ac1b0-139">mssql-scripter</span></span>](https://github.com/Microsoft/sql-xplat-cli) |
|<span data-ttu-id="ac1b0-140">Другие</span><span class="sxs-lookup"><span data-stu-id="ac1b0-140">Other</span></span>                  |<span data-ttu-id="ac1b0-141">Клиент iPython</span><span class="sxs-lookup"><span data-stu-id="ac1b0-141">iPython Client</span></span><br> [<span data-ttu-id="ac1b0-142">Интерфейс командной строки Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="ac1b0-142">Cloud Foundry CLI</span></span>](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a><span data-ttu-id="ac1b0-143">Поддержка языков</span><span class="sxs-lookup"><span data-stu-id="ac1b0-143">Language support</span></span>
|<span data-ttu-id="ac1b0-144">язык</span><span class="sxs-lookup"><span data-stu-id="ac1b0-144">Language</span></span>   |<span data-ttu-id="ac1b0-145">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="ac1b0-145">Version</span></span>   |
|---|---|
|<span data-ttu-id="ac1b0-146">.NET</span><span class="sxs-lookup"><span data-stu-id="ac1b0-146">.NET</span></span>       |<span data-ttu-id="ac1b0-147">1.01</span><span class="sxs-lookup"><span data-stu-id="ac1b0-147">1.01</span></span>       |
|<span data-ttu-id="ac1b0-148">Go</span><span class="sxs-lookup"><span data-stu-id="ac1b0-148">Go</span></span>         |<span data-ttu-id="ac1b0-149">1.7</span><span class="sxs-lookup"><span data-stu-id="ac1b0-149">1.7</span></span>        |
|<span data-ttu-id="ac1b0-150">Java</span><span class="sxs-lookup"><span data-stu-id="ac1b0-150">Java</span></span>       |<span data-ttu-id="ac1b0-151">1.8</span><span class="sxs-lookup"><span data-stu-id="ac1b0-151">1.8</span></span>        |
|<span data-ttu-id="ac1b0-152">Node.js</span><span class="sxs-lookup"><span data-stu-id="ac1b0-152">Node.js</span></span>    |<span data-ttu-id="ac1b0-153">6.9.4</span><span class="sxs-lookup"><span data-stu-id="ac1b0-153">6.9.4</span></span>      |
|<span data-ttu-id="ac1b0-154">Python</span><span class="sxs-lookup"><span data-stu-id="ac1b0-154">Python</span></span>     |<span data-ttu-id="ac1b0-155">2.7 и 3.5 (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="ac1b0-155">2.7 and 3.5 (default)</span></span>|

## <a name="secure-automatic-authentication"></a><span data-ttu-id="ac1b0-156">Безопасная автоматическая аутентификация</span><span class="sxs-lookup"><span data-stu-id="ac1b0-156">Secure automatic authentication</span></span>
<span data-ttu-id="ac1b0-157">Облако оболочки безопасно и автоматически выполняет проверку подлинности доступа к учетной записи для hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="ac1b0-157">Cloud Shell securely and automatically authenticates account access for hello Azure CLI 2.0.</span></span>

## <a name="azure-files-persistence"></a><span data-ttu-id="ac1b0-158">Сохраняемость файлов Azure</span><span class="sxs-lookup"><span data-stu-id="ac1b0-158">Azure Files persistence</span></span>
<span data-ttu-id="ac1b0-159">Поскольку Cloud Shell выделяется по запросу с использованием временного компьютера, файлы за пределами каталога $Home и сведения о состоянии компьютера не сохраняются между сеансами.</span><span class="sxs-lookup"><span data-stu-id="ac1b0-159">Since Cloud Shell is allocated on a per-request basis using a temporary machine, files outside of your $Home and machine state are not persisted across sessions.</span></span>
<span data-ttu-id="ac1b0-160">файлы toopersist во всех сеансах обходов оболочки облака через подключение файла Azure отправляемого при первом запуске.</span><span class="sxs-lookup"><span data-stu-id="ac1b0-160">toopersist files across sessions, Cloud Shell walks you through attaching an Azure file share on first launch.</span></span>
<span data-ttu-id="ac1b0-161">По завершении настройки Cloud Shell будет автоматически присоединять хранилище для всех будущих сеансов.</span><span class="sxs-lookup"><span data-stu-id="ac1b0-161">Once completed Cloud Shell will automatically attach your storage for all future sessions.</span></span>

[<span data-ttu-id="ac1b0-162">Дополнительные сведения о присоединении tooCloud общие папки файлов Azure оболочки.</span><span class="sxs-lookup"><span data-stu-id="ac1b0-162">Learn more about attaching Azure file shares tooCloud Shell.</span></span>](persisting-shell-storage.md)

## <a name="next-steps"></a><span data-ttu-id="ac1b0-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ac1b0-163">Next steps</span></span>
[<span data-ttu-id="ac1b0-164">Краткое руководство по Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="ac1b0-164">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="ac1b0-165">
[Подробное описание Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="ac1b0-165">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br>