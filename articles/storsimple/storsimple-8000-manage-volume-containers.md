---
title: "aaaManage контейнерами томов StorSimple на устройства серии StorSimple 8000 hello | Документы Microsoft"
description: "Объясняется, как можно использовать диспетчер устройств StorSimple контейнеры томов службы страницы tooadd, изменить или удалить контейнер томов hello."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="9a054-103">Используйте контейнеры томов StorSimple toomanage службы hello диспетчер устройств StorSimple</span><span class="sxs-lookup"><span data-stu-id="9a054-103">Use hello StorSimple Device Manager service toomanage StorSimple volume containers</span></span>

## <a name="overview"></a><span data-ttu-id="9a054-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="9a054-104">Overview</span></span>
<span data-ttu-id="9a054-105">Этот учебник объясняется, как toouse hello toocreate службы диспетчера StorSimple устройств и Управление контейнерами томов StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9a054-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="9a054-106">Контейнер томов в устройстве Microsoft Azure StorSimple содержит один или несколько томов, которые совместно используют учетную запись хранения, функцию шифрования и параметры потребления полосы пропускания.</span><span class="sxs-lookup"><span data-stu-id="9a054-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="9a054-107">В устройстве может быть несколько контейнеров томов для всех его томов.</span><span class="sxs-lookup"><span data-stu-id="9a054-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="9a054-108">Контейнер томов обладает hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="9a054-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="9a054-109">**Тома** — hello многоуровневого или локально закрепленного тома StorSimple, содержащиеся в контейнере томов hello.</span><span class="sxs-lookup"><span data-stu-id="9a054-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> 
* <span data-ttu-id="9a054-110">**Шифрование** — ключ шифрования, который можно задать для каждого контейнера томов.</span><span class="sxs-lookup"><span data-stu-id="9a054-110">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="9a054-111">Этот ключ используется для шифрования данных hello, который отправляется в облаке toohello устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9a054-111">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="9a054-112">Ключ оборонному стандарту AES-256 бит используется с вводимым пользователем ключом hello.</span><span class="sxs-lookup"><span data-stu-id="9a054-112">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="9a054-113">toosecure данных, рекомендуется всегда применять шифрование в облаке.</span><span class="sxs-lookup"><span data-stu-id="9a054-113">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="9a054-114">**Учетная запись хранения** — hello учетной записи хранилища Azure, — это данные, используемые toostore hello.</span><span class="sxs-lookup"><span data-stu-id="9a054-114">**Storage account** – hello Azure storage account that is used toostore hello data.</span></span> <span data-ttu-id="9a054-115">Все тома hello, находящихся в контейнере томов совместно использовать эту учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="9a054-115">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="9a054-116">Можно выбрать учетную запись из существующего списка или создайте новую учетную запись, при создании контейнера томов hello и затем укажите учетные данные для hello доступа для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="9a054-116">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="9a054-117">**Пропускная способность облака** — hello пропускной способностью, используемой hello устройства при отправке облака toohello hello данные с устройства hello.</span><span class="sxs-lookup"><span data-stu-id="9a054-117">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="9a054-118">При создании контейнера можно ограничить пропускную способность, указав значение от 1 до 1000 Мбит/с.</span><span class="sxs-lookup"><span data-stu-id="9a054-118">You can enforce a bandwidth control by specifying a value between 1 Mbps and 1,000 Mbps when you create this container.</span></span> <span data-ttu-id="9a054-119">Hello устройства tooconsume всю доступную пропускную способность, установите это поле слишком**неограниченное количество**.</span><span class="sxs-lookup"><span data-stu-id="9a054-119">If you want hello device tooconsume all available bandwidth, set this field too**Unlimited**.</span></span> <span data-ttu-id="9a054-120">Можно также создать и применить пропускной способности tooallocate шаблона пропускной способности на основе расписания.</span><span class="sxs-lookup"><span data-stu-id="9a054-120">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

<span data-ttu-id="9a054-121">Hello следующих процедурах объясняется, как toouse hello StorSimple **контейнеры томов** hello toocomplete колонке следующие общие операции:</span><span class="sxs-lookup"><span data-stu-id="9a054-121">hello following procedures explain how toouse hello StorSimple **Volume containers** blade toocomplete hello following common operations:</span></span>

* <span data-ttu-id="9a054-122">Добавить контейнер томов</span><span class="sxs-lookup"><span data-stu-id="9a054-122">Add a volume container</span></span>
* <span data-ttu-id="9a054-123">Изменение контейнера томов</span><span class="sxs-lookup"><span data-stu-id="9a054-123">Modify a volume container</span></span>
* <span data-ttu-id="9a054-124">Удаление контейнера томов</span><span class="sxs-lookup"><span data-stu-id="9a054-124">Delete a volume container</span></span>

## <a name="add-a-volume-container"></a><span data-ttu-id="9a054-125">Добавить контейнер томов</span><span class="sxs-lookup"><span data-stu-id="9a054-125">Add a volume container</span></span>
<span data-ttu-id="9a054-126">Выполните следующие шаги tooadd контейнер томов hello.</span><span class="sxs-lookup"><span data-stu-id="9a054-126">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="9a054-127">Изменение контейнера томов</span><span class="sxs-lookup"><span data-stu-id="9a054-127">Modify a volume container</span></span>
<span data-ttu-id="9a054-128">Выполните следующие шаги toomodify контейнер томов hello.</span><span class="sxs-lookup"><span data-stu-id="9a054-128">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="9a054-129">Удаление контейнера томов</span><span class="sxs-lookup"><span data-stu-id="9a054-129">Delete a volume container</span></span>
<span data-ttu-id="9a054-130">Контейнер томов содержит тома.</span><span class="sxs-lookup"><span data-stu-id="9a054-130">A volume container has volumes within it.</span></span> <span data-ttu-id="9a054-131">Его можно удалить только в том случае, если сначала удаляются все содержащиеся в нем тома hello.</span><span class="sxs-lookup"><span data-stu-id="9a054-131">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="9a054-132">Выполните следующие шаги toodelete контейнер томов hello.</span><span class="sxs-lookup"><span data-stu-id="9a054-132">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="9a054-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9a054-133">Next steps</span></span>
* <span data-ttu-id="9a054-134">Узнайте больше об [управлении томами StorSimple](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="9a054-134">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span> 
* <span data-ttu-id="9a054-135">Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="9a054-135">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

