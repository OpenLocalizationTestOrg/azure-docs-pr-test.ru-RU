---
title: "Ограничения в базе данных Azure для MySQL | Документация Майкрософт"
description: "Описываются ограничения (предварительная версия) в базе данных Azure для MySQL."
services: mysql
author: jasonh
ms.author: kamathsun
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c61d70897b66c2ffee819ac98c38ab75000db907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="limitations-in-azure-database-for-mysql-preview"></a><span data-ttu-id="e7f44-103">Ограничения в базе данных Azure для MySQL (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="e7f44-103">Limitations in Azure Database for MySQL (Preview)</span></span>
<span data-ttu-id="e7f44-104">Служба базы данных Azure для MySQL работает в режиме общедоступной предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="e7f44-104">The Azure Database for MySQL service is in public preview.</span></span> <span data-ttu-id="e7f44-105">В следующих разделах описываются действующие ограничения емкости и функциональных возможностей в службе базы данных.</span><span class="sxs-lookup"><span data-stu-id="e7f44-105">The following sections describe capacity and functional limits in the database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="e7f44-106">Максимумы уровней служб</span><span class="sxs-lookup"><span data-stu-id="e7f44-106">Service Tier Maximums</span></span>
<span data-ttu-id="e7f44-107">База данных Azure для MySQL имеет несколько уровней служб, которые можно выбрать при создании сервера.</span><span class="sxs-lookup"><span data-stu-id="e7f44-107">Azure Database for MySQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="e7f44-108">Дополнительные сведения см. в статье [Уровни служб в базе данных Azure для MySQL](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="e7f44-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="e7f44-109">На каждом уровне служб в предварительной версии службы существует максимальное число подключений, единиц вычислений и максимальный объем хранилища. Ниже перечислены эти ограничения.</span><span class="sxs-lookup"><span data-stu-id="e7f44-109">There is a maximum number of connections, compute units, and storage in each service tier during the service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="e7f44-110">**Максимальное число подключений**</span><span class="sxs-lookup"><span data-stu-id="e7f44-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="e7f44-111">Базовый, 50 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="e7f44-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="e7f44-112">50 подключений</span><span class="sxs-lookup"><span data-stu-id="e7f44-112">50 connections</span></span>    |
| <span data-ttu-id="e7f44-113">Базовый, 100 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="e7f44-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="e7f44-114">100 подключений</span><span class="sxs-lookup"><span data-stu-id="e7f44-114">100 connections</span></span>   |
| <span data-ttu-id="e7f44-115">Стандартный, 100 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="e7f44-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="e7f44-116">200 подключений</span><span class="sxs-lookup"><span data-stu-id="e7f44-116">200 connections</span></span>   |
| <span data-ttu-id="e7f44-117">Стандартный, 200 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="e7f44-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="e7f44-118">300 подключений</span><span class="sxs-lookup"><span data-stu-id="e7f44-118">300 connections</span></span>   |
| <span data-ttu-id="e7f44-119">Стандартный, 400 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="e7f44-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="e7f44-120">400 подключений</span><span class="sxs-lookup"><span data-stu-id="e7f44-120">400 connections</span></span>   |
| <span data-ttu-id="e7f44-121">Стандартный, 800 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="e7f44-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="e7f44-122">500 подключений</span><span class="sxs-lookup"><span data-stu-id="e7f44-122">500 connections</span></span>   |
| <span data-ttu-id="e7f44-123">**Максимальное число единиц вычислений**</span><span class="sxs-lookup"><span data-stu-id="e7f44-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="e7f44-124">Уровень службы "Базовый"</span><span class="sxs-lookup"><span data-stu-id="e7f44-124">Basic service tier</span></span>         | <span data-ttu-id="e7f44-125">100 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="e7f44-125">100 Compute Units</span></span> |
| <span data-ttu-id="e7f44-126">Уровень службы "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="e7f44-126">Standard service tier</span></span>      | <span data-ttu-id="e7f44-127">800 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="e7f44-127">800 Compute Units</span></span> |
| <span data-ttu-id="e7f44-128">**Максимальный объем хранилища**</span><span class="sxs-lookup"><span data-stu-id="e7f44-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="e7f44-129">Уровень службы "Базовый"</span><span class="sxs-lookup"><span data-stu-id="e7f44-129">Basic service tier</span></span>         | <span data-ttu-id="e7f44-130">1 TБ</span><span class="sxs-lookup"><span data-stu-id="e7f44-130">1 TB</span></span>              |
| <span data-ttu-id="e7f44-131">Уровень службы "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="e7f44-131">Standard service tier</span></span>      | <span data-ttu-id="e7f44-132">1 TБ</span><span class="sxs-lookup"><span data-stu-id="e7f44-132">1 TB</span></span>              |

<span data-ttu-id="e7f44-133">Когда число подключений превышается, может появиться следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="e7f44-133">When too many connections are reached, you may receive the following error:</span></span>
> <span data-ttu-id="e7f44-134">ОШИБКА 1040 (08004): Слишком много подключений</span><span class="sxs-lookup"><span data-stu-id="e7f44-134">ERROR 1040 (08004): Too many connections</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="e7f44-135">Ограничения функциональных возможностей предварительной версии</span><span class="sxs-lookup"><span data-stu-id="e7f44-135">Preview functional limitations:</span></span>
### <a name="scale-operations"></a><span data-ttu-id="e7f44-136">Операции масштабирования:</span><span class="sxs-lookup"><span data-stu-id="e7f44-136">Scale operations:</span></span>
1.  <span data-ttu-id="e7f44-137">В настоящее время динамическое масштабирование серверов между уровнями служб не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="e7f44-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="e7f44-138">Имеется в виду переключение между уровнями служб "Базовый" и "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="e7f44-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="e7f44-139">В настоящее время динамическое увеличение объема хранилища по запросу на предварительно созданном сервере не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="e7f44-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="e7f44-140">Уменьшение размера хранилища сервера не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="e7f44-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="e7f44-141">Обновление версии сервера:</span><span class="sxs-lookup"><span data-stu-id="e7f44-141">Server version upgrades:</span></span>
- <span data-ttu-id="e7f44-142">В настоящее время автоматический переход между основными версиями ядра СУБД не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="e7f44-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="e7f44-143">Управление подпиской:</span><span class="sxs-lookup"><span data-stu-id="e7f44-143">Subscription management:</span></span>
- <span data-ttu-id="e7f44-144">В настоящее время динамическое перемещение предварительно созданных серверов между подпиской и группой ресурсов не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="e7f44-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="e7f44-145">Восстановление до точки во времени:</span><span class="sxs-lookup"><span data-stu-id="e7f44-145">Point-in-time-restore:</span></span>
1.  <span data-ttu-id="e7f44-146">Восстановление в другой уровень служб и (или) до другого числа единиц вычислений и размера хранилища не допускается.</span><span class="sxs-lookup"><span data-stu-id="e7f44-146">Restoring to different service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="e7f44-147">Восстановление удаленного сервера не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="e7f44-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7f44-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e7f44-148">Next Steps:</span></span>
<span data-ttu-id="e7f44-149">[Уровни служб в базе данных Azure для MySQL](concepts-service-tiers.md)
[Поддерживаемые версии в базе данных Azure для MySQL](concepts-supported-versions.md)</span><span class="sxs-lookup"><span data-stu-id="e7f44-149">[What’s available in each service tier](concepts-service-tiers.md)
[Supported MySQL Database Versions](concepts-supported-versions.md)</span></span>
