---
title: "aaaLimitations в базе данных Azure для MySQL | Документы Microsoft"
description: "Описываются ограничения (предварительная версия) в базе данных Azure для MySQL."
services: mysql
author: jasonh
ms.author: kamathsun
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 9c877c592bf640f62182d8761c9c51363882d706
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-in-azure-database-for-mysql-preview"></a><span data-ttu-id="0a1be-103">Ограничения в базе данных Azure для MySQL (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="0a1be-103">Limitations in Azure Database for MySQL (Preview)</span></span>
<span data-ttu-id="0a1be-104">Hello базы данных Azure для службы MySQL находится в общедоступной предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="0a1be-104">hello Azure Database for MySQL service is in public preview.</span></span> <span data-ttu-id="0a1be-105">Hello следующих разделах описаны емкости и функциональные ограничения hello службы базы данных.</span><span class="sxs-lookup"><span data-stu-id="0a1be-105">hello following sections describe capacity and functional limits in hello database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="0a1be-106">Максимумы уровней служб</span><span class="sxs-lookup"><span data-stu-id="0a1be-106">Service Tier Maximums</span></span>
<span data-ttu-id="0a1be-107">База данных Azure для MySQL имеет несколько уровней служб, которые можно выбрать при создании сервера.</span><span class="sxs-lookup"><span data-stu-id="0a1be-107">Azure Database for MySQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="0a1be-108">Дополнительные сведения см. в статье [Уровни служб в базе данных Azure для MySQL](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="0a1be-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="0a1be-109">Есть максимальное число подключений, единицы вычислений и хранения на каждом уровне службы при использовании предварительной версии службы hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0a1be-109">There is a maximum number of connections, compute units, and storage in each service tier during hello service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="0a1be-110">**Максимальное число подключений**</span><span class="sxs-lookup"><span data-stu-id="0a1be-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="0a1be-111">Базовый, 50 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="0a1be-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="0a1be-112">50 подключений</span><span class="sxs-lookup"><span data-stu-id="0a1be-112">50 connections</span></span>    |
| <span data-ttu-id="0a1be-113">Базовый, 100 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="0a1be-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="0a1be-114">100 подключений</span><span class="sxs-lookup"><span data-stu-id="0a1be-114">100 connections</span></span>   |
| <span data-ttu-id="0a1be-115">Стандартный, 100 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="0a1be-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="0a1be-116">200 подключений</span><span class="sxs-lookup"><span data-stu-id="0a1be-116">200 connections</span></span>   |
| <span data-ttu-id="0a1be-117">Стандартный, 200 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="0a1be-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="0a1be-118">300 подключений</span><span class="sxs-lookup"><span data-stu-id="0a1be-118">300 connections</span></span>   |
| <span data-ttu-id="0a1be-119">Стандартный, 400 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="0a1be-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="0a1be-120">400 подключений</span><span class="sxs-lookup"><span data-stu-id="0a1be-120">400 connections</span></span>   |
| <span data-ttu-id="0a1be-121">Стандартный, 800 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="0a1be-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="0a1be-122">500 подключений</span><span class="sxs-lookup"><span data-stu-id="0a1be-122">500 connections</span></span>   |
| <span data-ttu-id="0a1be-123">**Максимальное число единиц вычислений**</span><span class="sxs-lookup"><span data-stu-id="0a1be-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="0a1be-124">Уровень службы "Базовый"</span><span class="sxs-lookup"><span data-stu-id="0a1be-124">Basic service tier</span></span>         | <span data-ttu-id="0a1be-125">100 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="0a1be-125">100 Compute Units</span></span> |
| <span data-ttu-id="0a1be-126">Уровень службы "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="0a1be-126">Standard service tier</span></span>      | <span data-ttu-id="0a1be-127">800 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="0a1be-127">800 Compute Units</span></span> |
| <span data-ttu-id="0a1be-128">**Максимальный объем хранилища**</span><span class="sxs-lookup"><span data-stu-id="0a1be-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="0a1be-129">Уровень службы "Базовый"</span><span class="sxs-lookup"><span data-stu-id="0a1be-129">Basic service tier</span></span>         | <span data-ttu-id="0a1be-130">1 TБ</span><span class="sxs-lookup"><span data-stu-id="0a1be-130">1 TB</span></span>              |
| <span data-ttu-id="0a1be-131">Уровень службы "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="0a1be-131">Standard service tier</span></span>      | <span data-ttu-id="0a1be-132">1 TБ</span><span class="sxs-lookup"><span data-stu-id="0a1be-132">1 TB</span></span>              |

<span data-ttu-id="0a1be-133">При достижении слишком много подключений, может появиться следующая ошибка hello:</span><span class="sxs-lookup"><span data-stu-id="0a1be-133">When too many connections are reached, you may receive hello following error:</span></span>
> <span data-ttu-id="0a1be-134">ОШИБКА 1040 (08004): Слишком много подключений</span><span class="sxs-lookup"><span data-stu-id="0a1be-134">ERROR 1040 (08004): Too many connections</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="0a1be-135">Ограничения функциональных возможностей предварительной версии</span><span class="sxs-lookup"><span data-stu-id="0a1be-135">Preview functional limitations:</span></span>
### <a name="scale-operations"></a><span data-ttu-id="0a1be-136">Операции масштабирования:</span><span class="sxs-lookup"><span data-stu-id="0a1be-136">Scale operations:</span></span>
1.  <span data-ttu-id="0a1be-137">В настоящее время динамическое масштабирование серверов между уровнями служб не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0a1be-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="0a1be-138">Имеется в виду переключение между уровнями служб "Базовый" и "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="0a1be-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="0a1be-139">В настоящее время динамическое увеличение объема хранилища по запросу на предварительно созданном сервере не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0a1be-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="0a1be-140">Уменьшение размера хранилища сервера не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0a1be-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="0a1be-141">Обновление версии сервера:</span><span class="sxs-lookup"><span data-stu-id="0a1be-141">Server version upgrades:</span></span>
- <span data-ttu-id="0a1be-142">В настоящее время автоматический переход между основными версиями ядра СУБД не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0a1be-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="0a1be-143">Управление подпиской:</span><span class="sxs-lookup"><span data-stu-id="0a1be-143">Subscription management:</span></span>
- <span data-ttu-id="0a1be-144">В настоящее время динамическое перемещение предварительно созданных серверов между подпиской и группой ресурсов не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0a1be-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="0a1be-145">Восстановление до точки во времени:</span><span class="sxs-lookup"><span data-stu-id="0a1be-145">Point-in-time-restore:</span></span>
1.  <span data-ttu-id="0a1be-146">Восстановление toodifferent уровень обслуживания или размера единицы вычислений и хранилище не допускается.</span><span class="sxs-lookup"><span data-stu-id="0a1be-146">Restoring toodifferent service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="0a1be-147">Восстановление удаленного сервера не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0a1be-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a1be-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0a1be-148">Next Steps:</span></span>
<span data-ttu-id="0a1be-149">[Уровни служб в базе данных Azure для MySQL](concepts-service-tiers.md)
[Поддерживаемые версии в базе данных Azure для MySQL](concepts-supported-versions.md)</span><span class="sxs-lookup"><span data-stu-id="0a1be-149">[What’s available in each service tier](concepts-service-tiers.md)
[Supported MySQL Database Versions](concepts-supported-versions.md)</span></span>
