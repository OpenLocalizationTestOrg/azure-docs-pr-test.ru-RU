---
title: "Ограничения Azure Cloud Shell (предварительная версия) | Документация Майкрософт"
description: "Обзор ограничений Azure Cloud Shell."
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
ms.openlocfilehash: e42841b126a9df9240bec3f489589d5ce4a6db80
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="limitations-of-azure-cloud-shell"></a><span data-ttu-id="bbf02-103">Ограничения Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="bbf02-103">Limitations of Azure Cloud Shell</span></span>
<span data-ttu-id="bbf02-104">Azure Cloud Shell имеет следующие известные ограничения:</span><span class="sxs-lookup"><span data-stu-id="bbf02-104">Azure Cloud Shell has the following known limitations:</span></span>

## <a name="system-state-and-persistence"></a><span data-ttu-id="bbf02-105">Состояние системы и сохраняемость</span><span class="sxs-lookup"><span data-stu-id="bbf02-105">System state and persistence</span></span>
<span data-ttu-id="bbf02-106">Компьютер, предоставляющий сеанс Cloud Shell, является временным и перезапускается, если сеанс не используется в течение 20 минут.</span><span class="sxs-lookup"><span data-stu-id="bbf02-106">The machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes.</span></span> <span data-ttu-id="bbf02-107">Для подключения Cloud Shell требуется общая папка.</span><span class="sxs-lookup"><span data-stu-id="bbf02-107">Cloud Shell requires a file share to be mounted.</span></span> <span data-ttu-id="bbf02-108">Поэтому ваша подписка должна иметь возможность настраивать ресурсы хранилища для доступа к Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="bbf02-108">As a result, your subscription must be able to set up storage resources to access Cloud Shell.</span></span> <span data-ttu-id="bbf02-109">Дополнительные рекомендации:</span><span class="sxs-lookup"><span data-stu-id="bbf02-109">Other considerations include:</span></span>
* <span data-ttu-id="bbf02-110">С подключенным хранилищем сохраняются только изменения в каталоге `$Home` или каталоге `clouddrive`.</span><span class="sxs-lookup"><span data-stu-id="bbf02-110">With mounted storage, only modifications within your `$Home` directory or `clouddrive` directory are persisted.</span></span>
* <span data-ttu-id="bbf02-111">Общие папки можно подключить только в пределах [назначенного региона](persisting-shell-storage.md#mount-a-new-clouddrive).</span><span class="sxs-lookup"><span data-stu-id="bbf02-111">File shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).</span></span>
* <span data-ttu-id="bbf02-112">Файлы Azure поддерживают только локально избыточное хранилище в геоизбыточные учетные записи.</span><span class="sxs-lookup"><span data-stu-id="bbf02-112">Azure Files supports only locally redundant storage and geo-redundant storage accounts.</span></span>

## <a name="user-permissions"></a><span data-ttu-id="bbf02-113">Разрешения пользователя</span><span class="sxs-lookup"><span data-stu-id="bbf02-113">User permissions</span></span>
<span data-ttu-id="bbf02-114">Разрешения задаются как для обычных пользователей без доступа к sudo.</span><span class="sxs-lookup"><span data-stu-id="bbf02-114">Permissions are set as regular users without sudo access.</span></span> <span data-ttu-id="bbf02-115">Все, что устанавливается за пределами каталога `$Home`, не сохранится.</span><span class="sxs-lookup"><span data-stu-id="bbf02-115">Any installation outside your `$Home` directory will not persist.</span></span>
<span data-ttu-id="bbf02-116">Хотя некоторые команды в каталоге `clouddrive`, такие как `git clone`, не имеют необходимых разрешений, каталог `$Home` их имеет.</span><span class="sxs-lookup"><span data-stu-id="bbf02-116">Although certain commands within the `clouddrive` directory, such as `git clone`, do not have proper permissions, your `$Home` directory does have permissions.</span></span>

## <a name="browser-support"></a><span data-ttu-id="bbf02-117">Поддержка браузеров</span><span class="sxs-lookup"><span data-stu-id="bbf02-117">Browser support</span></span>
<span data-ttu-id="bbf02-118">Cloud Shell поддерживает последние версии Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox и Apple Safari.</span><span class="sxs-lookup"><span data-stu-id="bbf02-118">Cloud Shell supports the latest versions of Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox, and Apple Safari.</span></span> <span data-ttu-id="bbf02-119">Использование Safari в режиме защищенного просмотра не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="bbf02-119">Safari in private mode is not supported.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="bbf02-120">Копирование и вставка</span><span class="sxs-lookup"><span data-stu-id="bbf02-120">Copy and paste</span></span>
<span data-ttu-id="bbf02-121">Так как в Azure Cloud Shell сочетания клавиш Ctrl+C и Ctrl+V не работают в качестве команд копирования и вставки на компьютерах с операционной системой Windows, используйте для этого сочетания клавиш Ctrl+Ins и Shift+Ins соответственно.</span><span class="sxs-lookup"><span data-stu-id="bbf02-121">Ctrl+C and Ctrl+V do not function as copy/paste shortcuts in Cloud Shell on Windows machines, use Ctrl+Insert and Shift+Insert to copy and paste respectively.</span></span>

<span data-ttu-id="bbf02-122">Вызов команд копирования и вставки щелчком правой кнопки мыши также доступен, но эта функция зависит от параметров доступа к буферу обмена в каждом конкретном браузере.</span><span class="sxs-lookup"><span data-stu-id="bbf02-122">Right-click copy-and-paste options are also available, but right-click function is subject to browser-specific clipboard access.</span></span>

## <a name="editing-bashrc"></a><span data-ttu-id="bbf02-123">Изменение файла .bashrc</span><span class="sxs-lookup"><span data-stu-id="bbf02-123">Editing .bashrc</span></span>
<span data-ttu-id="bbf02-124">Будьте внимательны при изменении файла .bashrc, так как некоторые изменения могут привести к непредвиденным ошибкам в Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="bbf02-124">Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.</span></span>

## <a name="bashhistory"></a><span data-ttu-id="bbf02-125">.bash_history</span><span class="sxs-lookup"><span data-stu-id="bbf02-125">.bash_history</span></span>
<span data-ttu-id="bbf02-126">Журнал команд bash может быть несогласованным из-за перебоев в сеансе Cloud Shell или из-за одновременных сеансов.</span><span class="sxs-lookup"><span data-stu-id="bbf02-126">Your history of bash commands may be inconsistent because of Cloud Shell session disruption or concurrent sessions.</span></span>

## <a name="usage-limits"></a><span data-ttu-id="bbf02-127">Ограничения использования</span><span class="sxs-lookup"><span data-stu-id="bbf02-127">Usage limits</span></span>
<span data-ttu-id="bbf02-128">Cloud Shell предназначен для интерактивного использования.</span><span class="sxs-lookup"><span data-stu-id="bbf02-128">Cloud Shell is intended for interactive use cases.</span></span> <span data-ttu-id="bbf02-129">В результате любые длительные неинтерактивные сеансы завершаются без предупреждения.</span><span class="sxs-lookup"><span data-stu-id="bbf02-129">As a result, any long-running non-interactive sessions are ended without warning.</span></span>

## <a name="network-connectivity"></a><span data-ttu-id="bbf02-130">Сетевое подключение</span><span class="sxs-lookup"><span data-stu-id="bbf02-130">Network connectivity</span></span>
<span data-ttu-id="bbf02-131">Задержки в Cloud Shell зависят от локального подключения к Интернету. Cloud Shell будет пытаться продолжать выполнять любые отправленные инструкции.</span><span class="sxs-lookup"><span data-stu-id="bbf02-131">Any latency in Cloud Shell is subject to local internet connectivity, Cloud Shell continues to attempt to carry out any instructions sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbf02-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bbf02-132">Next steps</span></span>
[<span data-ttu-id="bbf02-133">Краткое руководство по Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="bbf02-133">Cloud Shell Quickstart</span></span>](quickstart.md)
