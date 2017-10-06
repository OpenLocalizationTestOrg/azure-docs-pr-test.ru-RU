---
title: "aaaLimitations в базе данных Azure для PostgreSQL | Документы Microsoft"
description: "Описываются ограничения в базе данных Azure для PostgreSQL."
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.topic: article
ms.date: 06/01/2017
ms.openlocfilehash: f53dd240e55e0633bc1dfb8ad25e1818fa8ae18c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-in-azure-database-for-postgresql"></a><span data-ttu-id="23830-103">Ограничения в базе данных Azure для PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="23830-103">Limitations in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="23830-104">Hello базы данных Azure для службы PostgreSQL находится в общедоступной предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="23830-104">hello Azure Database for PostgreSQL service is in public preview.</span></span> <span data-ttu-id="23830-105">Hello следующих разделах описаны емкости и функциональные ограничения hello службы базы данных.</span><span class="sxs-lookup"><span data-stu-id="23830-105">hello following sections describe capacity and functional limits in hello database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="23830-106">Максимумы уровней служб</span><span class="sxs-lookup"><span data-stu-id="23830-106">Service Tier Maximums</span></span>
<span data-ttu-id="23830-107">База данных Azure для PostgreSQL имеет несколько уровней служб, которые можно выбрать при создании сервера.</span><span class="sxs-lookup"><span data-stu-id="23830-107">Azure Database for PostgreSQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="23830-108">Дополнительные сведения см. в статье [Уровни служб в базе данных Azure для MySQL](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="23830-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="23830-109">Есть максимальное число подключений, единицы вычислений и хранения на каждом уровне службы при использовании предварительной версии службы hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="23830-109">There is a maximum number of connections, compute units, and storage in each service tier during hello service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="23830-110">**Максимальное число подключений**</span><span class="sxs-lookup"><span data-stu-id="23830-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="23830-111">Базовый, 50 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="23830-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="23830-112">50 подключений</span><span class="sxs-lookup"><span data-stu-id="23830-112">50 connections</span></span>    |
| <span data-ttu-id="23830-113">Базовый, 100 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="23830-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="23830-114">100 подключений</span><span class="sxs-lookup"><span data-stu-id="23830-114">100 connections</span></span>   |
| <span data-ttu-id="23830-115">Стандартный, 100 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="23830-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="23830-116">200 подключений</span><span class="sxs-lookup"><span data-stu-id="23830-116">200 connections</span></span>   |
| <span data-ttu-id="23830-117">Стандартный, 200 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="23830-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="23830-118">300 подключений</span><span class="sxs-lookup"><span data-stu-id="23830-118">300 connections</span></span>   |
| <span data-ttu-id="23830-119">Стандартный, 400 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="23830-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="23830-120">400 подключений</span><span class="sxs-lookup"><span data-stu-id="23830-120">400 connections</span></span>   |
| <span data-ttu-id="23830-121">Стандартный, 800 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="23830-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="23830-122">500 подключений</span><span class="sxs-lookup"><span data-stu-id="23830-122">500 connections</span></span>   |
| <span data-ttu-id="23830-123">**Максимальное число единиц вычислений**</span><span class="sxs-lookup"><span data-stu-id="23830-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="23830-124">Уровень службы "Базовый"</span><span class="sxs-lookup"><span data-stu-id="23830-124">Basic service tier</span></span>         | <span data-ttu-id="23830-125">100 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="23830-125">100 Compute Units</span></span> |
| <span data-ttu-id="23830-126">Уровень службы "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="23830-126">Standard service tier</span></span>      | <span data-ttu-id="23830-127">800 единиц вычислений</span><span class="sxs-lookup"><span data-stu-id="23830-127">800 Compute Units</span></span> |
| <span data-ttu-id="23830-128">**Максимальный объем хранилища**</span><span class="sxs-lookup"><span data-stu-id="23830-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="23830-129">Уровень службы "Базовый"</span><span class="sxs-lookup"><span data-stu-id="23830-129">Basic service tier</span></span>         | <span data-ttu-id="23830-130">1 TБ</span><span class="sxs-lookup"><span data-stu-id="23830-130">1 TB</span></span>              |
| <span data-ttu-id="23830-131">Уровень службы "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="23830-131">Standard service tier</span></span>      | <span data-ttu-id="23830-132">1 TБ</span><span class="sxs-lookup"><span data-stu-id="23830-132">1 TB</span></span>              |

<span data-ttu-id="23830-133">При достижении слишком много подключений, может появиться следующая ошибка hello:</span><span class="sxs-lookup"><span data-stu-id="23830-133">When too many connections are reached, you may receive hello following error:</span></span>
> <span data-ttu-id="23830-134">FATAL: sorry, too many clients already (Неустранимая ошибка: уже подключено слишком много клиентов)</span><span class="sxs-lookup"><span data-stu-id="23830-134">FATAL:  sorry, too many clients already</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="23830-135">Ограничения функциональных возможностей предварительной версии</span><span class="sxs-lookup"><span data-stu-id="23830-135">Preview functional limitations</span></span>
### <a name="scale-operations"></a><span data-ttu-id="23830-136">Операции масштабирования</span><span class="sxs-lookup"><span data-stu-id="23830-136">Scale operations</span></span>
1.  <span data-ttu-id="23830-137">В настоящее время динамическое масштабирование серверов между уровнями служб не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="23830-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="23830-138">Имеется в виду переключение между уровнями служб "Базовый" и "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="23830-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="23830-139">В настоящее время динамическое увеличение объема хранилища по запросу на предварительно созданном сервере не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="23830-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="23830-140">Уменьшение размера хранилища сервера не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="23830-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="23830-141">Обновления версии сервера</span><span class="sxs-lookup"><span data-stu-id="23830-141">Server version upgrades</span></span>
- <span data-ttu-id="23830-142">В настоящее время автоматический переход между основными версиями ядра СУБД не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="23830-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="23830-143">Управление подпиской</span><span class="sxs-lookup"><span data-stu-id="23830-143">Subscription management</span></span>
- <span data-ttu-id="23830-144">В настоящее время динамическое перемещение предварительно созданных серверов между подпиской и группой ресурсов не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="23830-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="23830-145">Восстановление до точки во времени</span><span class="sxs-lookup"><span data-stu-id="23830-145">Point-in-time-restore</span></span>
1.  <span data-ttu-id="23830-146">Восстановление toodifferent уровень обслуживания или размера единицы вычислений и хранилище не допускается.</span><span class="sxs-lookup"><span data-stu-id="23830-146">Restoring toodifferent service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="23830-147">Восстановление удаленного сервера не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="23830-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23830-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="23830-148">Next steps</span></span>
- <span data-ttu-id="23830-149">Ознакомьтесь со статьей [Параметры и производительность базы данных Azure для MySQL: возможности разных уровней служб](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="23830-149">Understand [What’s available in each pricing tier](concepts-service-tiers.md)</span></span>
- <span data-ttu-id="23830-150">Ознакомьтесь со статьей [Поддерживаемые версии в базе данных Azure для PostgreSQL](concepts-supported-versions.md).</span><span class="sxs-lookup"><span data-stu-id="23830-150">Understand [Supported PostgreSQL Database Versions](concepts-supported-versions.md)</span></span>
- <span data-ttu-id="23830-151">Просмотрите [как tooBack копирования и восстановления сервера в базе данных Azure для использования PostgreSQL hello портал Azure](howto-restore-server-portal.md)</span><span class="sxs-lookup"><span data-stu-id="23830-151">Review [How tooBack up and Restore a server in Azure Database for PostgreSQL using hello Azure portal](howto-restore-server-portal.md)</span></span>
