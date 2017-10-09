---
title: "aaaManage ресурсов данных в каталоге данных Azure | Документы Microsoft"
description: "Hello статья описывает, как toocontrol видимость и владение ресурсов данных зарегистрированы в каталоге данных Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 623f5ed4-8da7-48f5-943a-448d0b7cba69
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 48a634b92d7da19c32c9e551f295eec257f54f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a><span data-ttu-id="8768f-103">Управление ресурсами данных в каталоге данных Azure</span><span class="sxs-lookup"><span data-stu-id="8768f-103">Manage data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="8768f-104">Введение</span><span class="sxs-lookup"><span data-stu-id="8768f-104">Introduction</span></span>
<span data-ttu-id="8768f-105">Каталог данных Azure предназначен для обнаружения источника данных, так что можно легко найти и понять hello источники данных должны tooperform анализа и принятия решений.</span><span class="sxs-lookup"><span data-stu-id="8768f-105">Azure Data Catalog is designed for data-source discovery, so that you can easily discover and understand hello data sources you need tooperform analysis and make decisions.</span></span> <span data-ttu-id="8768f-106">Эти возможности обнаружения делают hello наибольшее влияние, когда вы и другие пользователи могут найти и понять hello широкого доступных источников данных.</span><span class="sxs-lookup"><span data-stu-id="8768f-106">These discovery capabilities make hello biggest impact when you and other users can find and understand hello broadest range of available data sources.</span></span> <span data-ttu-id="8768f-107">С этими элементами в виду поведение по умолчанию hello каталога данных предназначен для всех зарегистрированных данных источников toobe видимым tooand обнаруживаемой всеми пользователями каталога.</span><span class="sxs-lookup"><span data-stu-id="8768f-107">With these elements in mind, hello default behavior of Data Catalog is for all registered data sources toobe visible tooand discoverable by all catalog users.</span></span>

<span data-ttu-id="8768f-108">Каталог данных не дает доступа к данным toohello сам.</span><span class="sxs-lookup"><span data-stu-id="8768f-108">Data Catalog does not give you access toohello data itself.</span></span> <span data-ttu-id="8768f-109">Доступ к данным управляется hello владельцем источника данных hello.</span><span class="sxs-lookup"><span data-stu-id="8768f-109">Data access is controlled by hello owner of hello data source.</span></span> <span data-ttu-id="8768f-110">С помощью каталога данных можно определить источники данных и просмотреть hello метаданные, связанные toohello источников, зарегистрированных в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="8768f-110">With Data Catalog, you can discover data sources and view hello metadata that's related toohello sources that are registered in hello catalog.</span></span>

<span data-ttu-id="8768f-111">Может возникнуть ситуация, тем не менее, когда источники данных должны только видимым toospecific пользователей или toomembers определенных групп.</span><span class="sxs-lookup"><span data-stu-id="8768f-111">There might be situations, however, where data sources should only be visible toospecific users, or toomembers of specific groups.</span></span> <span data-ttu-id="8768f-112">В таких случаях пользователи распоряжаться средствам зарегистрированных данных в пределах каталога hello и затем управлять видимостью hello активов hello, которыми они владеют.</span><span class="sxs-lookup"><span data-stu-id="8768f-112">In such scenarios, users can take ownership of registered data assets within hello catalog and then control hello visibility of hello assets they own.</span></span>

> [!NOTE]
> <span data-ttu-id="8768f-113">функции Hello, описанные в этой статье доступен только в hello Standard Edition из каталога данных Azure.</span><span class="sxs-lookup"><span data-stu-id="8768f-113">hello functionality described in this article is available only in hello Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="8768f-114">Hello бесплатный выпуск не предоставляет возможности для владения и ограничения видимости ресурса данных.</span><span class="sxs-lookup"><span data-stu-id="8768f-114">hello Free Edition does not provide capabilities for ownership and restricting data-asset visibility.</span></span>
>
>

## <a name="manage-ownership-of-data-assets"></a><span data-ttu-id="8768f-115">Управление владением ресурсами данных</span><span class="sxs-lookup"><span data-stu-id="8768f-115">Manage ownership of data assets</span></span>
<span data-ttu-id="8768f-116">По умолчанию ресурсы данных, зарегистрированные в каталоге данных, не имеют владельца.</span><span class="sxs-lookup"><span data-stu-id="8768f-116">By default, data assets that are registered in Data Catalog are unowned.</span></span> <span data-ttu-id="8768f-117">Любой пользователь, имеющий разрешение tooaccess hello каталога может обнаружить и пометить эти ресурсы.</span><span class="sxs-lookup"><span data-stu-id="8768f-117">Any user with permission tooaccess hello catalog can discover and annotate these assets.</span></span> <span data-ttu-id="8768f-118">Пользователи могут получать во владение ресурсов без ответственного данных и затем ограничить видимость hello активов hello, которыми они владеют.</span><span class="sxs-lookup"><span data-stu-id="8768f-118">Users can take ownership of unowned data assets and then limit hello visibility of hello assets they own.</span></span>

<span data-ttu-id="8768f-119">При ресурса данных в каталоге данных есть владелец, только тех пользователей, имеющих право владельцами hello можно обнаружить активов hello и просмотра его метаданных, и только hello владельцы могут удалять активов hello из каталога hello.</span><span class="sxs-lookup"><span data-stu-id="8768f-119">When a data asset in Data Catalog is owned, only users who are authorized by hello owners can discover hello asset and view its metadata, and only hello owners can delete hello asset from hello catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="8768f-120">Владение в каталоге данных затрагивает только метаданные hello, который хранится в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="8768f-120">Ownership in Data Catalog affects only hello metadata that's stored in hello catalog.</span></span> <span data-ttu-id="8768f-121">Владение не предоставляет никаких разрешений на hello базового источника данных.</span><span class="sxs-lookup"><span data-stu-id="8768f-121">Ownership does not confer any permissions on hello underlying data source.</span></span>
>
>

### <a name="take-ownership"></a><span data-ttu-id="8768f-122">Назначение владельца</span><span class="sxs-lookup"><span data-stu-id="8768f-122">Take ownership</span></span>
<span data-ttu-id="8768f-123">Пользователи могут стать владельцами ресурсов данных, выбрав hello **Take Ownership** параметр hello портале каталога данных.</span><span class="sxs-lookup"><span data-stu-id="8768f-123">Users can take ownership of data assets by selecting hello **Take Ownership** option in hello Data Catalog portal.</span></span> <span data-ttu-id="8768f-124">Специальные разрешения не являются обязательным tootake владения актива отсутствии владельца данных.</span><span class="sxs-lookup"><span data-stu-id="8768f-124">No special permissions are required tootake ownership of an unowned data asset.</span></span> <span data-ttu-id="8768f-125">Владельцем такого ресурса данных может стать любой пользователь.</span><span class="sxs-lookup"><span data-stu-id="8768f-125">Any user can take ownership of an unowned data asset.</span></span>

### <a name="add-owners-and-co-owners"></a><span data-ttu-id="8768f-126">Добавление владельцев и совладельцев</span><span class="sxs-lookup"><span data-stu-id="8768f-126">Add owners and co-owners</span></span>
<span data-ttu-id="8768f-127">Если у ресурса данных уже есть владелец, пользователи не могут просто стать владельцами.</span><span class="sxs-lookup"><span data-stu-id="8768f-127">If a data asset is already owned, other users cannot simply take ownership.</span></span> <span data-ttu-id="8768f-128">Существующий владелец должен добавить их в качестве совладельцев.</span><span class="sxs-lookup"><span data-stu-id="8768f-128">They must be added as co-owners by an existing owner.</span></span> <span data-ttu-id="8768f-129">Любой владелец может добавлять дополнительных пользователей или группы безопасности в качестве совладельцев.</span><span class="sxs-lookup"><span data-stu-id="8768f-129">Any owner can add additional users or security groups as co-owners.</span></span>

> [!NOTE]
> <span data-ttu-id="8768f-130">Он является наиболее toohave рекомендаций по крайней мере два отдельных пользователей в список владельцев для любой принадлежит ресурса данных.</span><span class="sxs-lookup"><span data-stu-id="8768f-130">It is a best practice toohave at least two individuals as owners for any owned data asset.</span></span>
>
>

### <a name="remove-owners"></a><span data-ttu-id="8768f-131">Удаление владельцев</span><span class="sxs-lookup"><span data-stu-id="8768f-131">Remove owners</span></span>
<span data-ttu-id="8768f-132">Любой владелец ресурса может не только добавлять совладельцев, но и удалять их.</span><span class="sxs-lookup"><span data-stu-id="8768f-132">Just as any asset owner can add co-owners, any asset owner can remove any co-owner.</span></span>

<span data-ttu-id="8768f-133">Владелец ресурса, который удаляет себя или в качестве владельца больше не может управлять hello активов.</span><span class="sxs-lookup"><span data-stu-id="8768f-133">An asset owner who removes him or herself as an owner can no longer manage hello asset.</span></span> <span data-ttu-id="8768f-134">Если владелец ресурса hello удаляет себя или в качестве владельца и других сопутствующих владельцы отсутствуют, hello активов возвращается tooan монитором состояния.</span><span class="sxs-lookup"><span data-stu-id="8768f-134">If hello asset owner removes him or herself as an owner and there are no other co-owners, hello asset reverts tooan unowned state.</span></span>

## <a name="control-visibility"></a><span data-ttu-id="8768f-135">Управление видимостью</span><span class="sxs-lookup"><span data-stu-id="8768f-135">Control visibility</span></span>
<span data-ttu-id="8768f-136">Владельцы ресурса данных можно управлять видимостью hello hello ресурсов данных, которыми они владеют.</span><span class="sxs-lookup"><span data-stu-id="8768f-136">Data-asset owners can control hello visibility of hello data assets they own.</span></span> <span data-ttu-id="8768f-137">toorestrict области видимости, что по умолчанию hello, там, где все пользователи могут обнаруживать каталога данных и представление hello ресурса данных hello владелец ресурса можно переключать видимость приветствия из **все** слишком**владельцев и эти пользователи** в свойствах hello hello активов.</span><span class="sxs-lookup"><span data-stu-id="8768f-137">toorestrict visibility as hello default, where all Data Catalog users can discover and view hello data asset, hello asset owner can toggle hello visibility setting from **Everyone** too**Owners & These Users** in hello properties for hello asset.</span></span> <span data-ttu-id="8768f-138">Затем владельцы могут добавить определенных пользователей и группы безопасности.</span><span class="sxs-lookup"><span data-stu-id="8768f-138">Owners can then add specific users and security groups.</span></span>

> [!NOTE]
> <span data-ttu-id="8768f-139">По возможности разрешения владельца и видимость активов следует назначать не tooindividual пользователей и групп toosecurity.</span><span class="sxs-lookup"><span data-stu-id="8768f-139">Whenever possible, asset ownership and visibility permissions should be assigned toosecurity groups and not tooindividual users.</span></span>
>
>

## <a name="catalog-administrators"></a><span data-ttu-id="8768f-140">Администраторы каталога</span><span class="sxs-lookup"><span data-stu-id="8768f-140">Catalog administrators</span></span>
<span data-ttu-id="8768f-141">Администраторы каталога данных являются неявно совладельцы все ресурсы в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="8768f-141">Data Catalog administrators are implicitly co-owners of all assets in hello catalog.</span></span> <span data-ttu-id="8768f-142">Владельцев ресурса не может снять Администраторы и Администраторы могут управлять владения и видимость для всех ресурсов данных в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="8768f-142">Asset owners cannot remove visibility from administrators, and administrators can manage ownership and visibility for all data assets in hello catalog.</span></span>

## <a name="summary"></a><span data-ttu-id="8768f-143">Сводка</span><span class="sxs-lookup"><span data-stu-id="8768f-143">Summary</span></span>
<span data-ttu-id="8768f-144">Hello каталога данных crowdsourcing модели toometadata обнаружение данных и средства позволяет все toocontribute каталога пользователей и обнаружения.</span><span class="sxs-lookup"><span data-stu-id="8768f-144">hello Data Catalog crowdsourcing model toometadata and data asset discovery allows all catalog users toocontribute and discover.</span></span> <span data-ttu-id="8768f-145">Hello Standard Edition каталог данных предназначен для удобного просмотра hello toolimit владения и управления и использования ресурсов конкретных данных.</span><span class="sxs-lookup"><span data-stu-id="8768f-145">hello Standard Edition of Data Catalog is designed for ownership and management toolimit hello visibility and use of specific data assets.</span></span>
