---
title: "Общие сведения о aaaAzure оболочки облака (Предварительная версия) | Документы Microsoft"
description: "Обзор hello оболочки облако Azure."
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
ms.openlocfilehash: 45c6c85b167a90947a333f44a9186e2c01b4fa7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a><span data-ttu-id="7b6c1-103">Обзор Azure Cloud Shell (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="7b6c1-103">Overview of Azure Cloud Shell (Preview)</span></span>
<span data-ttu-id="7b6c1-104">Azure Cloud Shell — это интерактивная доступная браузеру оболочка для управления ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-104">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span>

![](media/overview-pic.png)

## <a name="features"></a><span data-ttu-id="7b6c1-105">Функции</span><span class="sxs-lookup"><span data-stu-id="7b6c1-105">Features</span></span>
### <a name="browser-based-shell-experience"></a><span data-ttu-id="7b6c1-106">Оболочка на основе браузера</span><span class="sxs-lookup"><span data-stu-id="7b6c1-106">Browser-based shell experience</span></span>
<span data-ttu-id="7b6c1-107">Облака оболочки включает tooa на основе браузера командной строки функциональность доступа созданного с помощью задачи управления Azure в виду.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-107">Cloud Shell enables access tooa browser-based command-line experience built with Azure management tasks in mind.</span></span> <span data-ttu-id="7b6c1-108">Используйте высокоэффективные мобильные с локального компьютера, можно предоставить только облако hello как toowork оболочки облака.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-108">Leverage Cloud Shell toowork untethered from a local machine in a way only hello cloud can provide.</span></span>

### <a name="pre-configured-azure-workstation"></a><span data-ttu-id="7b6c1-109">Предварительно настроенная рабочая станция Azure</span><span class="sxs-lookup"><span data-stu-id="7b6c1-109">Pre-configured Azure workstation</span></span>
<span data-ttu-id="7b6c1-110">Cloud Shell поставляется с предварительно установленными популярными инструментами командной строки и поддержкой языков, чтобы вы могли работать быстрее.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-110">Cloud Shell comes pre-installed with popular command-line tools and language support so you can work faster.</span></span>

[<span data-ttu-id="7b6c1-111">Просмотр hello полный набор инструментов списка для оболочки облако Azure здесь.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-111">View hello full tooling list for Azure Cloud Shell here.</span></span>](features.md#tools)

### <a name="automatic-authentication"></a><span data-ttu-id="7b6c1-112">Автоматическая проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="7b6c1-112">Automatic authentication</span></span>
<span data-ttu-id="7b6c1-113">Облако оболочки безопасно выполняет проверку подлинности автоматически для каждого сеанса для мгновенного доступа к ресурсам tooyour через hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-113">Cloud Shell securely authenticates automatically on each session for instant access tooyour resources through hello Azure CLI 2.0.</span></span>

### <a name="connect-your-azure-file-storage"></a><span data-ttu-id="7b6c1-114">Подключение хранилища файлов Azure</span><span class="sxs-lookup"><span data-stu-id="7b6c1-114">Connect your Azure File storage</span></span>
<span data-ttu-id="7b6c1-115">Оболочки компьютерах облака являются временными и таким образом требуется toobe общую папку файлов Azure, подключено в качестве `clouddrive` toopersist каталог $Home.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-115">Cloud Shell machines are temporary and as a result require an Azure file share toobe mounted as `clouddrive` toopersist your $Home directory.</span></span>
<span data-ttu-id="7b6c1-116">При первом запуске оболочки облака предлагает toocreate группы ресурсов, учетной записи хранилища и файл общей папки от вашего имени.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-116">On first launch Cloud Shell prompts toocreate a resource group, storage account, and file share on your behalf.</span></span> <span data-ttu-id="7b6c1-117">Это одноразовое действие, которое автоматически применяется для всех сеансов.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-117">This is a one-time step and will be automatically attached for all sessions.</span></span> 

#### <a name="create-new-storage"></a><span data-ttu-id="7b6c1-118">Создание хранилища</span><span class="sxs-lookup"><span data-stu-id="7b6c1-118">Create new storage</span></span>
![](media/basic-storage.png)

<span data-ttu-id="7b6c1-119">Учетная запись локально избыточного хранилища (LRS) может создаваться от вашего имени с общей папкой Azure, содержащей образ диска по умолчанию объемом 5 ГБ.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-119">A locally-redundant storage (LRS) account can be created on your behalf with an Azure file share containing a default 5-GB disk image.</span></span> <span data-ttu-id="7b6c1-120">Подключает Hello общей папки как `clouddrive` для файла совместное использование взаимодействия с hello образ диска, используемых toosync и сохраняются в каталоге $Home.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-120">hello file share mounts as `clouddrive` for file share interaction with hello disk image being used toosync and persist your $Home directory.</span></span> <span data-ttu-id="7b6c1-121">Применяются расходы на обычное хранение.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-121">Regular storage costs apply.</span></span>

<span data-ttu-id="7b6c1-122">От вашего имени будет создано три ресурса:</span><span class="sxs-lookup"><span data-stu-id="7b6c1-122">Three resources will be created on your behalf:</span></span>
1. <span data-ttu-id="7b6c1-123">Группа ресурсов с именем: `cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="7b6c1-123">Resource Group named: `cloud-shell-storage-<region>`</span></span>
2. <span data-ttu-id="7b6c1-124">Учетная запись хранения с именем: `cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="7b6c1-124">Storage Account named: `cs<uniqueGuid>`</span></span>
3. <span data-ttu-id="7b6c1-125">Общая папка с именем: `cs-<user>-<domain>-com-uniqueGuid`</span><span class="sxs-lookup"><span data-stu-id="7b6c1-125">File Share named: `cs-<user>-<domain>-com-uniqueGuid`</span></span>

> [!Note]
> <span data-ttu-id="7b6c1-126">Все файлы в каталоге $Home, такие как ключи SSH, сохраняются в образе диска пользователя, который хранится в подключенной общей папке.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-126">All files in your $Home directory such as SSH keys are persisted in your user disk image stored in your mounted file share.</span></span> <span data-ttu-id="7b6c1-127">Соблюдайте рекомендации при сохранении файлов в каталоге $Home и подключенной общей папке.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-127">Apply best practices when saving files in your $Home directory and mounted file share.</span></span>

#### <a name="use-existing-resources"></a><span data-ttu-id="7b6c1-128">Использование существующих ресурсов</span><span class="sxs-lookup"><span data-stu-id="7b6c1-128">Use existing resources</span></span>
![](media/advanced-storage.png)

<span data-ttu-id="7b6c1-129">Дополнительным также предоставляется разрешение вы tooassociate существующие ресурсы tooCloud оболочки.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-129">An advanced option is also provided allowing you tooassociate existing resources tooCloud Shell.</span></span> <span data-ttu-id="7b6c1-130">В появившемся подсказки при установке хранилища hello, нажмите кнопку «Показать дополнительные параметры» tooselect Дополнительные параметры.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-130">When presented with hello storage setup prompt, click "Show advanced settings" tooselect additional options.</span></span> <span data-ttu-id="7b6c1-131">Раскрывающиеся меню фильтруются с учетом назначенного региона Cloud Shell и учетных записей локально или глобально избыточных хранилищ.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-131">Dropdowns are filtered for your assigned Cloud Shell region and locally/globally-redundant storage accounts.</span></span>

<span data-ttu-id="7b6c1-132">Дополнительные сведения о хранилище Cloud Shell, обновлении общих папок, а также о скачивании и отправке файлов см. в статье [Сохранение файлов в Azure Cloud Shell] (persisting-shell-storage.md).</span><span class="sxs-lookup"><span data-stu-id="7b6c1-132">[Learn about Cloud Shell storage, updating file shares, and uploading/downloading files.] (persisting-shell-storage.md)</span></span>

## <a name="concepts"></a><span data-ttu-id="7b6c1-133">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="7b6c1-133">Concepts</span></span>
* <span data-ttu-id="7b6c1-134">Cloud Shell работает на временной машине, предоставляемой для каждого сеанса и для каждого пользователя отдельно.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-134">Cloud Shell runs on a temporary machine provided on a per-session, per-user basis</span></span>
* <span data-ttu-id="7b6c1-135">Время ожидания Cloud Shell истекает через 20 минут при отсутствии интерактивных действий.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-135">Cloud Shell times out after 20 minutes without interactive activity</span></span>
* <span data-ttu-id="7b6c1-136">Доступ к Cloud Shell можно получить только при наличии присоединенной общей папки.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-136">Cloud Shell can only be accessed with a file share attached</span></span>
* <span data-ttu-id="7b6c1-137">Cloud Shell назначается один компьютер на учетную запись пользователя.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-137">Cloud Shell is assigned one machine per user account</span></span>
* <span data-ttu-id="7b6c1-138">Разрешения задаются как для обычного пользователя Linux.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-138">Permissions are set as a regular Linux user</span></span>

[<span data-ttu-id="7b6c1-139">Дополнительные сведения о всех функциях Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-139">Learn more about all Cloud Shell features.</span></span>](features.md)

## <a name="examples"></a><span data-ttu-id="7b6c1-140">Примеры</span><span class="sxs-lookup"><span data-stu-id="7b6c1-140">Examples</span></span>
* <span data-ttu-id="7b6c1-141">Создание или изменение tooautomate сценариев управления Azure</span><span class="sxs-lookup"><span data-stu-id="7b6c1-141">Create or edit scripts tooautomate Azure management</span></span>
* <span data-ttu-id="7b6c1-142">Одновременное управление ресурсами через портал Azure и Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-142">Simultaneously manage resources via Azure portal and Azure CLI 2.0</span></span>
* <span data-ttu-id="7b6c1-143">Испытание Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-143">Test-drive Azure CLI 2.0</span></span>

[<span data-ttu-id="7b6c1-144">Опробуйте все примеры примеры использования оболочки облака hello.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-144">Try out all these examples at hello Cloud Shell quickstart.</span></span>](quickstart.md)

## <a name="pricing"></a><span data-ttu-id="7b6c1-145">Цены</span><span class="sxs-lookup"><span data-stu-id="7b6c1-145">Pricing</span></span>
<span data-ttu-id="7b6c1-146">Hello компьютере, где размещается оболочки облака предоставляется бесплатно, с необходимым компонентом для установленный файл Azure обмениваться toopersist каталог $Home.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-146">hello machine hosting Cloud Shell is free, with a pre-requisite of a mounted Azure file share toopersist your $Home directory.</span></span> <span data-ttu-id="7b6c1-147">Применяются расходы на обычное хранение.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-147">Regular storage costs apply.</span></span>

## <a name="supported-browsers"></a><span data-ttu-id="7b6c1-148">Поддерживаемые браузеры</span><span class="sxs-lookup"><span data-stu-id="7b6c1-148">Supported browsers</span></span>
<span data-ttu-id="7b6c1-149">Cloud Shell рекомендуется использовать с Chrome, Edge и Safari.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-149">Cloud Shell is recommended for Chrome, Edge, and Safari.</span></span> <span data-ttu-id="7b6c1-150">Параметры браузера toospecific субъекта — выполняемая облака оболочки для Chrome, Firefox, Safari, IE и граничных оболочки облака.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-150">While Cloud Shell is supported for Chrome, Firefox, Safari, IE, and Edge, Cloud Shell is subject toospecific browser settings.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7b6c1-151">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="7b6c1-151">Troubleshooting</span></span>
1. <span data-ttu-id="7b6c1-152">При использовании подписки на Azure Active Directory, не удается создать хранилище из-за tooError: 400 DisallowedOperation.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-152">When using an Azure Active Directory subscription, I cannot create storage due tooError: 400 DisallowedOperation.</span></span> <span data-ttu-id="7b6c1-153">tooresolve это, используйте подписки Azure для создания ресурсов хранилища.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-153">tooresolve this, please use an Azure subscription capable of creating storage resources.</span></span> <span data-ttu-id="7b6c1-154">AD подписки, не удается toocreate ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="7b6c1-154">AD subscriptions are not able toocreate Azure resources.</span></span>

<span data-ttu-id="7b6c1-155">Сведения об известных ограничениях Cloud Shell см. в [этой статье](limitations.md).</span><span class="sxs-lookup"><span data-stu-id="7b6c1-155">For specific known limitations, visit [limitations of Cloud Shell](limitations.md).</span></span>
