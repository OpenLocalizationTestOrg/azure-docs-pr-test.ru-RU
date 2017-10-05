---
title: "Обзор Azure Cloud Shell (предварительная версия) | Документация Майкрософт"
description: "Обзор Azure Cloud Shell."
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
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 7165633cd354eeea2e3619f839338e6af1524e56
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a><span data-ttu-id="73fdc-103">Обзор Azure Cloud Shell (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="73fdc-103">Overview of Azure Cloud Shell (Preview)</span></span>
<span data-ttu-id="73fdc-104">Azure Cloud Shell — это интерактивная доступная браузеру оболочка для управления ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="73fdc-104">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span>

![](media/overview-pic.png)

## <a name="features"></a><span data-ttu-id="73fdc-105">Функции</span><span class="sxs-lookup"><span data-stu-id="73fdc-105">Features</span></span>
### <a name="browser-based-shell-experience"></a><span data-ttu-id="73fdc-106">Оболочка на основе браузера</span><span class="sxs-lookup"><span data-stu-id="73fdc-106">Browser-based shell experience</span></span>
<span data-ttu-id="73fdc-107">Cloud Shell предоставляет доступ к браузерному интерфейсу командной строки, созданному с учетом задач управления Azure.</span><span class="sxs-lookup"><span data-stu-id="73fdc-107">Cloud Shell enables access to a browser-based command-line experience built with Azure management tasks in mind.</span></span> <span data-ttu-id="73fdc-108">Используйте Cloud Shell для работы из локального компьютера с неограниченными возможностями, которые может обеспечить только облако.</span><span class="sxs-lookup"><span data-stu-id="73fdc-108">Leverage Cloud Shell to work untethered from a local machine in a way only the cloud can provide.</span></span>

### <a name="pre-configured-azure-workstation"></a><span data-ttu-id="73fdc-109">Предварительно настроенная рабочая станция Azure</span><span class="sxs-lookup"><span data-stu-id="73fdc-109">Pre-configured Azure workstation</span></span>
<span data-ttu-id="73fdc-110">Cloud Shell поставляется с предварительно установленными популярными инструментами командной строки и поддержкой языков, чтобы вы могли работать быстрее.</span><span class="sxs-lookup"><span data-stu-id="73fdc-110">Cloud Shell comes pre-installed with popular command-line tools and language support so you can work faster.</span></span>

[<span data-ttu-id="73fdc-111">Полный список инструментария Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="73fdc-111">View the full tooling list for Azure Cloud Shell here.</span></span>](features.md#tools)

### <a name="automatic-authentication"></a><span data-ttu-id="73fdc-112">Автоматическая проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="73fdc-112">Automatic authentication</span></span>
<span data-ttu-id="73fdc-113">Cloud Shell автоматически безопасно проходит проверку подлинности при каждом сеансе, чтобы обеспечить мгновенный доступ к ресурсам через Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="73fdc-113">Cloud Shell securely authenticates automatically on each session for instant access to your resources through the Azure CLI 2.0.</span></span>

### <a name="connect-your-azure-file-storage"></a><span data-ttu-id="73fdc-114">Подключение хранилища файлов Azure</span><span class="sxs-lookup"><span data-stu-id="73fdc-114">Connect your Azure File storage</span></span>
<span data-ttu-id="73fdc-115">Машины Cloud Shell являются временными, поэтому требуют подключения общей папки Azure как `clouddrive` для хранения домашнего каталога.</span><span class="sxs-lookup"><span data-stu-id="73fdc-115">Cloud Shell machines are temporary and as a result require an Azure file share to be mounted as `clouddrive` to persist your $Home directory.</span></span>
<span data-ttu-id="73fdc-116">При первом запуске Cloud Shell предлагает создать группу ресурсов, учетную запись хранения и общую папку от вашего имени.</span><span class="sxs-lookup"><span data-stu-id="73fdc-116">On first launch Cloud Shell prompts to create a resource group, storage account, and file share on your behalf.</span></span> <span data-ttu-id="73fdc-117">Это одноразовое действие, которое автоматически применяется для всех сеансов.</span><span class="sxs-lookup"><span data-stu-id="73fdc-117">This is a one-time step and will be automatically attached for all sessions.</span></span> 

#### <a name="create-new-storage"></a><span data-ttu-id="73fdc-118">Создание хранилища</span><span class="sxs-lookup"><span data-stu-id="73fdc-118">Create new storage</span></span>
![](media/basic-storage.png)

<span data-ttu-id="73fdc-119">Учетная запись локально избыточного хранилища (LRS) может создаваться от вашего имени с общей папкой Azure, содержащей образ диска по умолчанию объемом 5 ГБ.</span><span class="sxs-lookup"><span data-stu-id="73fdc-119">A locally-redundant storage (LRS) account can be created on your behalf with an Azure file share containing a default 5-GB disk image.</span></span> <span data-ttu-id="73fdc-120">Общая папка подключается как `clouddrive`. Это обеспечивает взаимодействие с образом диска, используемым для синхронизации и сохранения каталога $Home.</span><span class="sxs-lookup"><span data-stu-id="73fdc-120">The file share mounts as `clouddrive` for file share interaction with the disk image being used to sync and persist your $Home directory.</span></span> <span data-ttu-id="73fdc-121">Применяются расходы на обычное хранение.</span><span class="sxs-lookup"><span data-stu-id="73fdc-121">Regular storage costs apply.</span></span>

<span data-ttu-id="73fdc-122">От вашего имени будет создано три ресурса:</span><span class="sxs-lookup"><span data-stu-id="73fdc-122">Three resources will be created on your behalf:</span></span>
1. <span data-ttu-id="73fdc-123">Группа ресурсов с именем: `cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="73fdc-123">Resource Group named: `cloud-shell-storage-<region>`</span></span>
2. <span data-ttu-id="73fdc-124">Учетная запись хранения с именем: `cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="73fdc-124">Storage Account named: `cs<uniqueGuid>`</span></span>
3. <span data-ttu-id="73fdc-125">Общая папка с именем: `cs-<user>-<domain>-com-uniqueGuid`</span><span class="sxs-lookup"><span data-stu-id="73fdc-125">File Share named: `cs-<user>-<domain>-com-uniqueGuid`</span></span>

> [!Note]
> <span data-ttu-id="73fdc-126">Все файлы в каталоге $Home, такие как ключи SSH, сохраняются в образе диска пользователя, который хранится в подключенной общей папке.</span><span class="sxs-lookup"><span data-stu-id="73fdc-126">All files in your $Home directory such as SSH keys are persisted in your user disk image stored in your mounted file share.</span></span> <span data-ttu-id="73fdc-127">Соблюдайте рекомендации при сохранении файлов в каталоге $Home и подключенной общей папке.</span><span class="sxs-lookup"><span data-stu-id="73fdc-127">Apply best practices when saving files in your $Home directory and mounted file share.</span></span>

#### <a name="use-existing-resources"></a><span data-ttu-id="73fdc-128">Использование существующих ресурсов</span><span class="sxs-lookup"><span data-stu-id="73fdc-128">Use existing resources</span></span>
![](media/advanced-storage.png)

<span data-ttu-id="73fdc-129">В Cloud Shell доступна дополнительная возможность, которая позволяет связывать существующие ресурсы с Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="73fdc-129">An advanced option is also provided allowing you to associate existing resources to Cloud Shell.</span></span> <span data-ttu-id="73fdc-130">При появлении запроса на настройку хранилища щелкните "Показать дополнительные настройки", чтобы выбрать дополнительные параметры.</span><span class="sxs-lookup"><span data-stu-id="73fdc-130">When presented with the storage setup prompt, click "Show advanced settings" to select additional options.</span></span> <span data-ttu-id="73fdc-131">Раскрывающиеся меню фильтруются с учетом назначенного региона Cloud Shell и учетных записей локально или глобально избыточных хранилищ.</span><span class="sxs-lookup"><span data-stu-id="73fdc-131">Dropdowns are filtered for your assigned Cloud Shell region and locally/globally-redundant storage accounts.</span></span>

<span data-ttu-id="73fdc-132">Дополнительные сведения о хранилище Cloud Shell, обновлении общих папок, а также о скачивании и отправке файлов см. в статье [Сохранение файлов в Azure Cloud Shell] (persisting-shell-storage.md).</span><span class="sxs-lookup"><span data-stu-id="73fdc-132">[Learn about Cloud Shell storage, updating file shares, and uploading/downloading files.] (persisting-shell-storage.md)</span></span>

## <a name="concepts"></a><span data-ttu-id="73fdc-133">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="73fdc-133">Concepts</span></span>
* <span data-ttu-id="73fdc-134">Cloud Shell работает на временной машине, предоставляемой для каждого сеанса и для каждого пользователя отдельно.</span><span class="sxs-lookup"><span data-stu-id="73fdc-134">Cloud Shell runs on a temporary machine provided on a per-session, per-user basis</span></span>
* <span data-ttu-id="73fdc-135">Время ожидания Cloud Shell истекает через 20 минут при отсутствии интерактивных действий.</span><span class="sxs-lookup"><span data-stu-id="73fdc-135">Cloud Shell times out after 20 minutes without interactive activity</span></span>
* <span data-ttu-id="73fdc-136">Доступ к Cloud Shell можно получить только при наличии присоединенной общей папки.</span><span class="sxs-lookup"><span data-stu-id="73fdc-136">Cloud Shell can only be accessed with a file share attached</span></span>
* <span data-ttu-id="73fdc-137">Cloud Shell назначается один компьютер на учетную запись пользователя.</span><span class="sxs-lookup"><span data-stu-id="73fdc-137">Cloud Shell is assigned one machine per user account</span></span>
* <span data-ttu-id="73fdc-138">Разрешения задаются как для обычного пользователя Linux.</span><span class="sxs-lookup"><span data-stu-id="73fdc-138">Permissions are set as a regular Linux user</span></span>

[<span data-ttu-id="73fdc-139">Дополнительные сведения о всех функциях Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="73fdc-139">Learn more about all Cloud Shell features.</span></span>](features.md)

## <a name="examples"></a><span data-ttu-id="73fdc-140">Примеры</span><span class="sxs-lookup"><span data-stu-id="73fdc-140">Examples</span></span>
* <span data-ttu-id="73fdc-141">Создание и изменение скриптов для автоматизации управления в Azure</span><span class="sxs-lookup"><span data-stu-id="73fdc-141">Create or edit scripts to automate Azure management</span></span>
* <span data-ttu-id="73fdc-142">Одновременное управление ресурсами через портал Azure и Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="73fdc-142">Simultaneously manage resources via Azure portal and Azure CLI 2.0</span></span>
* <span data-ttu-id="73fdc-143">Испытание Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="73fdc-143">Test-drive Azure CLI 2.0</span></span>

[<span data-ttu-id="73fdc-144">Опробуйте все эти примеры в кратком руководстве по Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="73fdc-144">Try out all these examples at the Cloud Shell quickstart.</span></span>](quickstart.md)

## <a name="pricing"></a><span data-ttu-id="73fdc-145">Цены</span><span class="sxs-lookup"><span data-stu-id="73fdc-145">Pricing</span></span>
<span data-ttu-id="73fdc-146">Машина, на которой размещена Cloud Shell, является бесплатной. На ней должна быть подключена общая папка Azure для хранения домашнего каталога.</span><span class="sxs-lookup"><span data-stu-id="73fdc-146">The machine hosting Cloud Shell is free, with a pre-requisite of a mounted Azure file share to persist your $Home directory.</span></span> <span data-ttu-id="73fdc-147">Применяются расходы на обычное хранение.</span><span class="sxs-lookup"><span data-stu-id="73fdc-147">Regular storage costs apply.</span></span>

## <a name="supported-browsers"></a><span data-ttu-id="73fdc-148">Поддерживаемые браузеры</span><span class="sxs-lookup"><span data-stu-id="73fdc-148">Supported browsers</span></span>
<span data-ttu-id="73fdc-149">Cloud Shell рекомендуется использовать с Chrome, Edge и Safari.</span><span class="sxs-lookup"><span data-stu-id="73fdc-149">Cloud Shell is recommended for Chrome, Edge, and Safari.</span></span> <span data-ttu-id="73fdc-150">Хотя служба Cloud Shell и поддерживается Chrome, Firefox, Safari, IE и Edge, она все еще зависит от определенных параметров браузера.</span><span class="sxs-lookup"><span data-stu-id="73fdc-150">While Cloud Shell is supported for Chrome, Firefox, Safari, IE, and Edge, Cloud Shell is subject to specific browser settings.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="73fdc-151">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="73fdc-151">Troubleshooting</span></span>
1. <span data-ttu-id="73fdc-152">Не удается создать хранилище, используя подписку Azure Active Directory, из-за ошибки 400 (DisallowedOperation).</span><span class="sxs-lookup"><span data-stu-id="73fdc-152">When using an Azure Active Directory subscription, I cannot create storage due to Error: 400 DisallowedOperation.</span></span> <span data-ttu-id="73fdc-153">Чтобы устранить эту ошибку, используйте подписку Azure, которая позволяет создавать ресурсы хранилища.</span><span class="sxs-lookup"><span data-stu-id="73fdc-153">To resolve this, please use an Azure subscription capable of creating storage resources.</span></span> <span data-ttu-id="73fdc-154">Подписки AD не поддерживают создание ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="73fdc-154">AD subscriptions are not able to create Azure resources.</span></span>

<span data-ttu-id="73fdc-155">Сведения об известных ограничениях Cloud Shell см. в [этой статье](limitations.md).</span><span class="sxs-lookup"><span data-stu-id="73fdc-155">For specific known limitations, visit [limitations of Cloud Shell](limitations.md).</span></span>
