---
title: "Использование журнала аудита в Azure AD Privileged Identity Management | Документация Майкрософт"
description: "Узнайте, как использовать журнал аудита в расширении для управления привилегированными пользователями Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 7d9a5255a64d46c1388d328a606b3f297d61262b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-audit-log-in-pim"></a><span data-ttu-id="cf78d-103">Использование журнала аудита для управления привилегированными пользователями</span><span class="sxs-lookup"><span data-stu-id="cf78d-103">Using the audit log in PIM</span></span>
<span data-ttu-id="cf78d-104">Вы можете использовать журнал аудита управления привилегированными пользователями (PIM) для просмотра всех назначенных пользователям и активированных ролей за определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="cf78d-104">You can use the Privileged Identity Management (PIM) audit log to see all the user assignments and activations within a given time period.</span></span> <span data-ttu-id="cf78d-105">Если требуется просмотреть весь журнал аудита действий в клиенте, включая действия администратора, пользователя и действия при синхронизации, можно использовать [отчеты о доступе и использовании Azure Active Directory.](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="cf78d-105">If you want to see the full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use the [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-to-the-audit-log"></a><span data-ttu-id="cf78d-106">Переход к журналу аудита</span><span class="sxs-lookup"><span data-stu-id="cf78d-106">Navigate to the audit log</span></span>
<span data-ttu-id="cf78d-107">На панели мониторинга [портала Azure](https://portal.azure.com) выберите приложение **Управление привилегированными пользователями Azure AD** .</span><span class="sxs-lookup"><span data-stu-id="cf78d-107">From the [Azure portal](https://portal.azure.com) dashboard, select the **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="cf78d-108">Чтобы открыть журнал аудита, на панели мониторинга PIM щелкните **Управление привилегированными ролями** > **Журнал аудита**.</span><span class="sxs-lookup"><span data-stu-id="cf78d-108">From there, access the audit log by clicking **Manage privileged roles** > **Audit history** in the PIM dashboard.</span></span>

## <a name="the-audit-log-graph"></a><span data-ttu-id="cf78d-109">Диаграмма журнала аудита</span><span class="sxs-lookup"><span data-stu-id="cf78d-109">The audit log graph</span></span>
<span data-ttu-id="cf78d-110">Вы можете использовать диаграмму журнала аудита для просмотра общего количества активаций, а также максимального и среднего количества активаций в день.</span><span class="sxs-lookup"><span data-stu-id="cf78d-110">You can use the audit log to view the total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="cf78d-111">Если в журнале аудита представлены данные для нескольких ролей, их можно отфильтровать.</span><span class="sxs-lookup"><span data-stu-id="cf78d-111">You can also filter the data by role if there is more than one role in the audit history.</span></span>

<span data-ttu-id="cf78d-112">Используйте кнопки **времени**, **действия** и **роли**, чтобы отсортировать данные в журнале.</span><span class="sxs-lookup"><span data-stu-id="cf78d-112">Use the **time**, **action**, and **role** buttons to sort the log.</span></span>

## <a name="the-audit-log-list"></a><span data-ttu-id="cf78d-113">Список журнала аудита</span><span class="sxs-lookup"><span data-stu-id="cf78d-113">The audit log list</span></span>
<span data-ttu-id="cf78d-114">Список журнала аудита содержит следующие столбцы:</span><span class="sxs-lookup"><span data-stu-id="cf78d-114">The columns in the audit log list are:</span></span>

* <span data-ttu-id="cf78d-115">**Запросившая сторона** — пользователь, запросивший активацию или изменение роли.</span><span class="sxs-lookup"><span data-stu-id="cf78d-115">**Requestor** - the user who requested the role activation or change.</span></span>  <span data-ttu-id="cf78d-116">Если значение — "Система Azure", проверьте журнал аудита Azure для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="cf78d-116">If the value is "Azure System", check the Azure audit log for more information.</span></span>
* <span data-ttu-id="cf78d-117">**Пользователь** — пользователь, активирующий роль или назначенный роли.</span><span class="sxs-lookup"><span data-stu-id="cf78d-117">**User** - the user who is activating or assigned to a role.</span></span>
* <span data-ttu-id="cf78d-118">**Роль** — роль, назначенная или активированная пользователем.</span><span class="sxs-lookup"><span data-stu-id="cf78d-118">**Role** - the role assigned or activated by the user.</span></span>
* <span data-ttu-id="cf78d-119">**Действие** — действия, предпринятые запросившей стороной.</span><span class="sxs-lookup"><span data-stu-id="cf78d-119">**Action** - the actions taken by the requestor.</span></span> <span data-ttu-id="cf78d-120">Они могут включать назначение, отмену назначения, активацию или отмену активации.</span><span class="sxs-lookup"><span data-stu-id="cf78d-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="cf78d-121">**Время** — время выполнения действия.</span><span class="sxs-lookup"><span data-stu-id="cf78d-121">**Time** - when the action occurred.</span></span>
* <span data-ttu-id="cf78d-122">**Причины**. Если во время активации в поле "Причина" был введен какой-либо текст, он будет отображаться здесь.</span><span class="sxs-lookup"><span data-stu-id="cf78d-122">**Reasoning** - if any text was entered into the reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="cf78d-123">**Срок действия** — применимо только для активации ролей.</span><span class="sxs-lookup"><span data-stu-id="cf78d-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-the-audit-log"></a><span data-ttu-id="cf78d-124">Фильтрация журнала аудита</span><span class="sxs-lookup"><span data-stu-id="cf78d-124">Filter the audit log</span></span>
<span data-ttu-id="cf78d-125">Данные в журнале аудита можно фильтровать, используя кнопку **Фильтр** .</span><span class="sxs-lookup"><span data-stu-id="cf78d-125">You can filter the information that shows up in the audit log by clicking the **Filter** button.</span></span>  <span data-ttu-id="cf78d-126">Откроется колонка **Обновление параметров диаграммы** .</span><span class="sxs-lookup"><span data-stu-id="cf78d-126">The **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="cf78d-127">Задав фильтры, нажмите кнопку **Обновить** , чтобы отфильтровать данные в журнале.</span><span class="sxs-lookup"><span data-stu-id="cf78d-127">After you set the filters, click **Update** to filter the data in the log.</span></span>  <span data-ttu-id="cf78d-128">Если данные не появятся сразу же, обновите страницу.</span><span class="sxs-lookup"><span data-stu-id="cf78d-128">If the data doesn't appear right away, refresh the page.</span></span>

### <a name="change-the-date-range"></a><span data-ttu-id="cf78d-129">Изменение диапазона дат</span><span class="sxs-lookup"><span data-stu-id="cf78d-129">Change the date range</span></span>
<span data-ttu-id="cf78d-130">Чтобы изменить диапазон времени журнала аудита, нажмите кнопку **Сегодня**, **Прошлая неделя**, **Прошлый месяц** или **Другое**.</span><span class="sxs-lookup"><span data-stu-id="cf78d-130">Use the **Today**, **Past Week**, **Past Month**, or **Custom** buttons to change the time range of the audit log.</span></span>

<span data-ttu-id="cf78d-131">При выборе варианта **Другое** появятся поля **начальной** и **конечной** дат, где можно указать диапазон времени журнала.</span><span class="sxs-lookup"><span data-stu-id="cf78d-131">When you choose the **Custom** button, you will be given a **From** date field and a **To** date field to specify a range of dates for the log.</span></span>  <span data-ttu-id="cf78d-132">Можно ввести дату в формате ММ/ДД/ГГГГ или щелкнуть значок **календаря** и выбрать дату в нем.</span><span class="sxs-lookup"><span data-stu-id="cf78d-132">You can either enter the dates in MM/DD/YYYY format or click on the **calendar** icon and choose the date from a calendar.</span></span>

### <a name="change-the-roles-included-in-the-log"></a><span data-ttu-id="cf78d-133">Изменение ролей, включенных в журнал</span><span class="sxs-lookup"><span data-stu-id="cf78d-133">Change the roles included in the log</span></span>
<span data-ttu-id="cf78d-134">Установите флажок **Роль** для ролей, которые требуется включить в журнал, и снимите его для остальных ролей.</span><span class="sxs-lookup"><span data-stu-id="cf78d-134">Check or uncheck the **Role** checkbox next to each role to include or exclude it from the log.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="cf78d-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cf78d-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

