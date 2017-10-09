---
title: "aaaCreate функция приложения hello портал Azure | Документы Microsoft"
description: "Создание нового приложения функции в службе приложений Azure с портала hello."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/11/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c531fc71c798edf22e25a5f4b79c15413809dc86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-from-hello-azure-portal"></a><span data-ttu-id="083e6-103">Создание приложения функции из hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="083e6-103">Create a function app from hello Azure portal</span></span>

<span data-ttu-id="083e6-104">Приложения Azure функция использует инфраструктуру службы приложений Azure hello.</span><span class="sxs-lookup"><span data-stu-id="083e6-104">Azure Function Apps uses hello Azure App Service infrastructure.</span></span> <span data-ttu-id="083e6-105">В этом разделе показано, как toocreate приложении функции в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="083e6-105">This topic shows you how toocreate a function app in hello Azure portal.</span></span> <span data-ttu-id="083e6-106">Функция приложения — hello контейнер, содержащий hello выполнения отдельных функций.</span><span class="sxs-lookup"><span data-stu-id="083e6-106">A function app is hello container that hosts hello execution of individual functions.</span></span> <span data-ttu-id="083e6-107">При создании приложения функции в план размещения службы приложения hello функции приложения могут использовать все возможности hello приложения службы.</span><span class="sxs-lookup"><span data-stu-id="083e6-107">When you create a function app in hello App Service hosting plan, your function app can use all hello features of App Service.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="083e6-108">Создание приложения-функции</span><span class="sxs-lookup"><span data-stu-id="083e6-108">Create a function app</span></span>

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="083e6-109">При создании приложения-функции укажите допустимое **имя приложения**, содержащее только буквы, цифры и дефисы.</span><span class="sxs-lookup"><span data-stu-id="083e6-109">When you create a function app, supply a valid **App name**, which can contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="083e6-110">Символ подчеркивания (**_**) использовать нельзя.</span><span class="sxs-lookup"><span data-stu-id="083e6-110">Underscore (**_**) is not an allowed character.</span></span>

<span data-ttu-id="083e6-111">Имя учетной записи хранения должно содержать от 3 до 24 символов и состоять только из цифр и строчных букв.</span><span class="sxs-lookup"><span data-stu-id="083e6-111">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="083e6-112">Имя учетной записи хранения должно быть уникальным в Azure.</span><span class="sxs-lookup"><span data-stu-id="083e6-112">Your storage account name must be unique within Azure.</span></span> 

<span data-ttu-id="083e6-113">После создания функции приложение hello можно создать отдельные функции в один или несколько разных языков.</span><span class="sxs-lookup"><span data-stu-id="083e6-113">After hello function app is created, you can create individual functions in one or more different languages.</span></span> <span data-ttu-id="083e6-114">Создание функций [с помощью портала hello](functions-create-first-azure-function.md#create-function), [непрерывного развертывания](functions-continuous-deployment.md), или [загрузка с FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span><span class="sxs-lookup"><span data-stu-id="083e6-114">Create functions [by using hello portal](functions-create-first-azure-function.md#create-function), [continuous deployment](functions-continuous-deployment.md), or by [uploading with FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span></span>

## <a name="service-plans"></a><span data-ttu-id="083e6-115">Планы обслуживания</span><span class="sxs-lookup"><span data-stu-id="083e6-115">Service plans</span></span>

<span data-ttu-id="083e6-116">В Функциях Azure имеются два разных плана обслуживания: план потребления и план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="083e6-116">Azure Functions has two different service plans: Consumption plan and App Service plan.</span></span> <span data-ttu-id="083e6-117">план потребления Hello автоматически размещает вычислительной мощности, когда выполняется ваш код, шкал при необходимости toohandle загрузки и затем шкал-Если код не выполняется.</span><span class="sxs-lookup"><span data-stu-id="083e6-117">hello Consumption plan automatically allocates compute power when your code is running, scales-out as necessary toohandle load, and then scales-in when code is not running.</span></span> <span data-ttu-id="083e6-118">Hello план служб приложений дает функции приложения access tooall hello приложения службы.</span><span class="sxs-lookup"><span data-stu-id="083e6-118">hello App Service plan gives your function app access tooall hello facilities of App Service.</span></span> <span data-ttu-id="083e6-119">План обслуживания нужно выбрать при создании приложения-функции, и в настоящее время невозможно изменить выбранный план.</span><span class="sxs-lookup"><span data-stu-id="083e6-119">You must choose your service plan when your function app is created, and it cannot currently be changed.</span></span> <span data-ttu-id="083e6-120">Дополнительные сведения см. в разделе [Выбор правильного плана обслуживания для Функций Azure](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="083e6-120">For more information, see [Choose an Azure Functions hosting plan](functions-scale.md).</span></span>

<span data-ttu-id="083e6-121">Если вы планируете toorun функции JavaScript для план служб приложений, следует выбрать план с меньшим числом ядер.</span><span class="sxs-lookup"><span data-stu-id="083e6-121">If you are planning toorun JavaScript functions on an App Service plan, you should choose a plan with fewer cores.</span></span> <span data-ttu-id="083e6-122">Дополнительные сведения см. в разделе hello [Справочник по JavaScript для функций](functions-reference-node.md#choose-single-core-app-service-plans).</span><span class="sxs-lookup"><span data-stu-id="083e6-122">For more information, see hello [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span>

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a><span data-ttu-id="083e6-123">Требования к учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="083e6-123">Storage account requirements</span></span>

<span data-ttu-id="083e6-124">При создании приложения функции в службе приложений, необходимо создать или связать tooa общего назначения учетной записи хранилища Azure, поддерживающий хранение больших двоичных объектов, очередей и таблиц.</span><span class="sxs-lookup"><span data-stu-id="083e6-124">When creating a function app in App Service, you must create or link tooa general-purpose Azure Storage account that supports Blob, Queue, and Table storage.</span></span> <span data-ttu-id="083e6-125">Для внутренних операций, таких как управление триггерами и ведение журнала выполнения функций, Функции Azure используют службу хранилища.</span><span class="sxs-lookup"><span data-stu-id="083e6-125">Internally, Functions uses Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="083e6-126">Некоторые учетные записи хранения не поддерживают очереди и таблицы. Например, это относится к учетным записям хранения только для больших двоичных объектов, службе хранилища Azure уровня "Премиум" и учетным записям хранения общего назначения с репликацией ZRS.</span><span class="sxs-lookup"><span data-stu-id="083e6-126">Some storage accounts do not support queues and tables, such as blob-only storage accounts, Azure Premium Storage, and general-purpose storage accounts with ZRS replication.</span></span> <span data-ttu-id="083e6-127">Эти учетные записи отфильтровываются из колонки hello учетной записи хранилища при создании приложения функции.</span><span class="sxs-lookup"><span data-stu-id="083e6-127">These accounts are filtered out of from hello Storage Account blade when creating a function app.</span></span>

>[!NOTE]
><span data-ttu-id="083e6-128">При использовании плана размещения потребления hello, функция кода и привязкой файлы конфигурации хранятся в хранилище файлов Azure в учетной записи основного хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="083e6-128">When using hello Consumption hosting plan, your function code and binding configuration files are stored in Azure File storage in hello main storage account.</span></span> <span data-ttu-id="083e6-129">При удалении учетной записи основного хранилища hello это содержимое удаляется и не может быть восстановлена.</span><span class="sxs-lookup"><span data-stu-id="083e6-129">When you delete hello main storage account, this content is deleted and cannot be recovered.</span></span>

<span data-ttu-id="083e6-130">toolearn Дополнительные сведения о типы учетных записей хранения, в разделе [введение в службы хранилища Azure hello](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span><span class="sxs-lookup"><span data-stu-id="083e6-130">toolearn more about storage account types, see [Introducing hello Azure Storage Services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="083e6-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="083e6-131">Next steps</span></span>

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



