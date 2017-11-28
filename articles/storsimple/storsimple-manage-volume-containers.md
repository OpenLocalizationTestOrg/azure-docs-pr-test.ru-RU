---
title: "aaaManage контейнерами томов StorSimple | Документы Microsoft"
description: "Объясняется, как можно использовать hello StorSimple Manager контейнеры томов службы страницы tooadd, изменить или удалить контейнер томов."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 1c64ce75-1fd3-4d3b-9304-d4dc0fc2b069
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 9b29536e0072306e53ac92bacca78a13d932c2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="8298e-103">Используйте контейнеры томов StorSimple toomanage службы hello диспетчера StorSimple</span><span class="sxs-lookup"><span data-stu-id="8298e-103">Use hello StorSimple Manager service toomanage StorSimple volume containers</span></span>
## <a name="overview"></a><span data-ttu-id="8298e-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="8298e-104">Overview</span></span>
<span data-ttu-id="8298e-105">Этот учебник объясняется, как toouse hello toocreate службы StorSimple Manager и Управление контейнерами томов StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8298e-105">This tutorial explains how toouse hello StorSimple Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="8298e-106">Контейнер томов в устройстве Microsoft Azure StorSimple содержит один или несколько томов, которые совместно используют учетную запись хранения, функцию шифрования и параметры потребления полосы пропускания.</span><span class="sxs-lookup"><span data-stu-id="8298e-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="8298e-107">В устройстве может быть несколько контейнеров томов для всех его томов.</span><span class="sxs-lookup"><span data-stu-id="8298e-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="8298e-108">Контейнер томов обладает hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="8298e-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="8298e-109">**Тома** — hello многоуровневого или локально закрепленного тома StorSimple, содержащиеся в контейнере томов hello.</span><span class="sxs-lookup"><span data-stu-id="8298e-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> <span data-ttu-id="8298e-110">Контейнер томов может содержать too256 томов StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8298e-110">A volume container may contain up too256 StorSimple volumes.</span></span>
* <span data-ttu-id="8298e-111">**Шифрование** — ключ шифрования, который можно задать для каждого контейнера томов.</span><span class="sxs-lookup"><span data-stu-id="8298e-111">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="8298e-112">Этот ключ используется для шифрования данных hello, который отправляется в облаке toohello устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8298e-112">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="8298e-113">Ключ оборонному стандарту AES-256 бит используется с вводимым пользователем ключом hello.</span><span class="sxs-lookup"><span data-stu-id="8298e-113">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="8298e-114">toosecure данных, рекомендуется всегда применять шифрование в облаке.</span><span class="sxs-lookup"><span data-stu-id="8298e-114">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="8298e-115">**Учетная запись хранения** — hello учетной записи хранилища, связанный tooyour поставщика услуг облачного хранилища.</span><span class="sxs-lookup"><span data-stu-id="8298e-115">**Storage account** – hello storage account that is linked tooyour cloud storage service provider.</span></span> <span data-ttu-id="8298e-116">Все тома hello, находящихся в контейнере томов совместно использовать эту учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="8298e-116">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="8298e-117">Можно выбрать учетную запись из существующего списка или создайте новую учетную запись, при создании контейнера томов hello и затем укажите учетные данные для hello доступа для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="8298e-117">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="8298e-118">**Пропускная способность облака** — hello пропускной способностью, используемой hello устройства при отправке облака toohello hello данные с устройства hello.</span><span class="sxs-lookup"><span data-stu-id="8298e-118">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="8298e-119">При настройке контейнера можно ограничить пропускную способность, указав значение от 1 до 1000 Мбит/с.</span><span class="sxs-lookup"><span data-stu-id="8298e-119">You can enforce a bandwidth control by specifying a value between 1 and 1000 Mbps when you define this container.</span></span> <span data-ttu-id="8298e-120">Если вы хотите tooconsume устройства hello всю доступную пропускную способность, задайте tooUnlimited этого поля.</span><span class="sxs-lookup"><span data-stu-id="8298e-120">If you want hello device tooconsume all available bandwidth, set this field tooUnlimited.</span></span> <span data-ttu-id="8298e-121">Можно также создать и применить пропускной способности tooallocate шаблона пропускной способности на основе расписания.</span><span class="sxs-lookup"><span data-stu-id="8298e-121">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

![Страница контейнеров томов](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

<span data-ttu-id="8298e-123">Это следующие процедуры показывают, как toouse hello StorSimple **контейнеры томов** hello toocomplete страницы, следующие общие операции:</span><span class="sxs-lookup"><span data-stu-id="8298e-123">This following procedures explain how toouse hello StorSimple **Volume containers** page toocomplete hello following common operations:</span></span>

* <span data-ttu-id="8298e-124">Добавление контейнера томов</span><span class="sxs-lookup"><span data-stu-id="8298e-124">Add a volume container</span></span> 
* <span data-ttu-id="8298e-125">Изменение контейнера томов</span><span class="sxs-lookup"><span data-stu-id="8298e-125">Modify a volume container</span></span> 
* <span data-ttu-id="8298e-126">Удаление контейнера томов</span><span class="sxs-lookup"><span data-stu-id="8298e-126">Delete a volume container</span></span> 

## <a name="add-a-volume-container"></a><span data-ttu-id="8298e-127">Добавление контейнера томов</span><span class="sxs-lookup"><span data-stu-id="8298e-127">Add a volume container</span></span>
<span data-ttu-id="8298e-128">Выполните следующие шаги tooadd контейнер томов hello.</span><span class="sxs-lookup"><span data-stu-id="8298e-128">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="8298e-129">Изменение контейнера томов</span><span class="sxs-lookup"><span data-stu-id="8298e-129">Modify a volume container</span></span>
<span data-ttu-id="8298e-130">Выполните следующие шаги toomodify контейнер томов hello.</span><span class="sxs-lookup"><span data-stu-id="8298e-130">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="8298e-131">Удаление контейнера томов</span><span class="sxs-lookup"><span data-stu-id="8298e-131">Delete a volume container</span></span>
<span data-ttu-id="8298e-132">Контейнер томов содержит тома.</span><span class="sxs-lookup"><span data-stu-id="8298e-132">A volume container has volumes within it.</span></span> <span data-ttu-id="8298e-133">Его можно удалить только в том случае, если сначала удаляются все содержащиеся в нем тома hello.</span><span class="sxs-lookup"><span data-stu-id="8298e-133">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="8298e-134">Выполните следующие шаги toodelete контейнер томов hello.</span><span class="sxs-lookup"><span data-stu-id="8298e-134">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="8298e-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8298e-135">Next steps</span></span>
* <span data-ttu-id="8298e-136">Узнайте больше об [управлении томами StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="8298e-136">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span> 
* <span data-ttu-id="8298e-137">Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="8298e-137">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

