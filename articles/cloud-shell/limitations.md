---
title: "aaaAzure ограничения оболочка облака (Предварительная версия) | Документы Microsoft"
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
ms.openlocfilehash: 8462b0b9850fcde790a386433009439bbab52c0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-cloud-shell"></a><span data-ttu-id="095ba-103">Ограничения Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="095ba-103">Limitations of Azure Cloud Shell</span></span>
<span data-ttu-id="095ba-104">Azure облачной оболочки имеет hello следующие известные ограничения.</span><span class="sxs-lookup"><span data-stu-id="095ba-104">Azure Cloud Shell has hello following known limitations:</span></span>

## <a name="system-state-and-persistence"></a><span data-ttu-id="095ba-105">Состояние системы и сохраняемость</span><span class="sxs-lookup"><span data-stu-id="095ba-105">System state and persistence</span></span>
<span data-ttu-id="095ba-106">Hello машины, которая предоставляет сеанс оболочки облако временный, и он будет перезапущен после сеанса не используется в течение 20 минут.</span><span class="sxs-lookup"><span data-stu-id="095ba-106">hello machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes.</span></span> <span data-ttu-id="095ba-107">Облако оболочки требуется подключить toobe папки файла.</span><span class="sxs-lookup"><span data-stu-id="095ba-107">Cloud Shell requires a file share toobe mounted.</span></span> <span data-ttu-id="095ba-108">В результате подписки должен быть может tooset копирование tooaccess ресурсы хранения оболочки облака.</span><span class="sxs-lookup"><span data-stu-id="095ba-108">As a result, your subscription must be able tooset up storage resources tooaccess Cloud Shell.</span></span> <span data-ttu-id="095ba-109">Дополнительные рекомендации:</span><span class="sxs-lookup"><span data-stu-id="095ba-109">Other considerations include:</span></span>
* <span data-ttu-id="095ba-110">С подключенным хранилищем сохраняются только изменения в каталоге `$Home` или каталоге `clouddrive`.</span><span class="sxs-lookup"><span data-stu-id="095ba-110">With mounted storage, only modifications within your `$Home` directory or `clouddrive` directory are persisted.</span></span>
* <span data-ttu-id="095ba-111">Общие папки можно подключить только в пределах [назначенного региона](persisting-shell-storage.md#mount-a-new-clouddrive).</span><span class="sxs-lookup"><span data-stu-id="095ba-111">File shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).</span></span>
* <span data-ttu-id="095ba-112">Файлы Azure поддерживают только локально избыточное хранилище в геоизбыточные учетные записи.</span><span class="sxs-lookup"><span data-stu-id="095ba-112">Azure Files supports only locally redundant storage and geo-redundant storage accounts.</span></span>

## <a name="user-permissions"></a><span data-ttu-id="095ba-113">Разрешения пользователя</span><span class="sxs-lookup"><span data-stu-id="095ba-113">User permissions</span></span>
<span data-ttu-id="095ba-114">Разрешения задаются как для обычных пользователей без доступа к sudo.</span><span class="sxs-lookup"><span data-stu-id="095ba-114">Permissions are set as regular users without sudo access.</span></span> <span data-ttu-id="095ba-115">Все, что устанавливается за пределами каталога `$Home`, не сохранится.</span><span class="sxs-lookup"><span data-stu-id="095ba-115">Any installation outside your `$Home` directory will not persist.</span></span>
<span data-ttu-id="095ba-116">Несмотря на то, что hello определенных команд в `clouddrive` каталога, такие как `git clone`, нет необходимых разрешений на `$Home` каталог имеет разрешения.</span><span class="sxs-lookup"><span data-stu-id="095ba-116">Although certain commands within hello `clouddrive` directory, such as `git clone`, do not have proper permissions, your `$Home` directory does have permissions.</span></span>

## <a name="browser-support"></a><span data-ttu-id="095ba-117">Поддержка браузеров</span><span class="sxs-lookup"><span data-stu-id="095ba-117">Browser support</span></span>
<span data-ttu-id="095ba-118">Облако оболочки поддерживает hello последние версии Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox и Apple Safari.</span><span class="sxs-lookup"><span data-stu-id="095ba-118">Cloud Shell supports hello latest versions of Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox, and Apple Safari.</span></span> <span data-ttu-id="095ba-119">Использование Safari в режиме защищенного просмотра не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="095ba-119">Safari in private mode is not supported.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="095ba-120">Копирование и вставка</span><span class="sxs-lookup"><span data-stu-id="095ba-120">Copy and paste</span></span>
<span data-ttu-id="095ba-121">CTRL + C и Ctrl + V работать скопируйте ярлыки в оболочке облака на компьютерах Windows, используйте сочетание клавиш Ctrl + Insert и Shift + Insert toocopy и вставьте соответственно.</span><span class="sxs-lookup"><span data-stu-id="095ba-121">Ctrl+C and Ctrl+V do not function as copy/paste shortcuts in Cloud Shell on Windows machines, use Ctrl+Insert and Shift+Insert toocopy and paste respectively.</span></span>

<span data-ttu-id="095ba-122">Параметры копирования и вставки контекстного меню также доступны, но функция щелкните правой кнопкой мыши имеет доступ к буферу обмена toobrowser определенного субъекта.</span><span class="sxs-lookup"><span data-stu-id="095ba-122">Right-click copy-and-paste options are also available, but right-click function is subject toobrowser-specific clipboard access.</span></span>

## <a name="editing-bashrc"></a><span data-ttu-id="095ba-123">Изменение файла .bashrc</span><span class="sxs-lookup"><span data-stu-id="095ba-123">Editing .bashrc</span></span>
<span data-ttu-id="095ba-124">Будьте внимательны при изменении файла .bashrc, так как некоторые изменения могут привести к непредвиденным ошибкам в Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="095ba-124">Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.</span></span>

## <a name="bashhistory"></a><span data-ttu-id="095ba-125">.bash_history</span><span class="sxs-lookup"><span data-stu-id="095ba-125">.bash_history</span></span>
<span data-ttu-id="095ba-126">Журнал команд bash может быть несогласованным из-за перебоев в сеансе Cloud Shell или из-за одновременных сеансов.</span><span class="sxs-lookup"><span data-stu-id="095ba-126">Your history of bash commands may be inconsistent because of Cloud Shell session disruption or concurrent sessions.</span></span>

## <a name="usage-limits"></a><span data-ttu-id="095ba-127">Ограничения использования</span><span class="sxs-lookup"><span data-stu-id="095ba-127">Usage limits</span></span>
<span data-ttu-id="095ba-128">Cloud Shell предназначен для интерактивного использования.</span><span class="sxs-lookup"><span data-stu-id="095ba-128">Cloud Shell is intended for interactive use cases.</span></span> <span data-ttu-id="095ba-129">В результате любые длительные неинтерактивные сеансы завершаются без предупреждения.</span><span class="sxs-lookup"><span data-stu-id="095ba-129">As a result, any long-running non-interactive sessions are ended without warning.</span></span>

## <a name="network-connectivity"></a><span data-ttu-id="095ba-130">Сетевое подключение</span><span class="sxs-lookup"><span data-stu-id="095ba-130">Network connectivity</span></span>
<span data-ttu-id="095ba-131">Задержек в оболочке облака подключение к Интернету toolocal субъекта, оболочка облако по-прежнему toocarry tooattempt out инструкции, отправленные.</span><span class="sxs-lookup"><span data-stu-id="095ba-131">Any latency in Cloud Shell is subject toolocal internet connectivity, Cloud Shell continues tooattempt toocarry out any instructions sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="095ba-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="095ba-132">Next steps</span></span>
[<span data-ttu-id="095ba-133">Краткое руководство по Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="095ba-133">Cloud Shell Quickstart</span></span>](quickstart.md)
