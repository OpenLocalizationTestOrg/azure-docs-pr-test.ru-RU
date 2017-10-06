---
title: "журнал аудита aaaHow toouse hello в Azure AD Privileged Identity Management | Документы Microsoft"
description: "Узнайте, как toouse hello аудита входа в расширении управления привилегированными пользователями Azure hello."
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
ms.openlocfilehash: 36987eaab9fe02c5dd7b4f4705e487299430745d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-audit-log-in-pim"></a><span data-ttu-id="cc6fa-103">Использование журнала аудита hello в PIM</span><span class="sxs-lookup"><span data-stu-id="cc6fa-103">Using hello audit log in PIM</span></span>
<span data-ttu-id="cc6fa-104">Можно использовать toosee журнала аудита управления привилегированных удостоверений (PIM) hello всех назначений пользователя hello и активаций в течение заданного периода времени.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-104">You can use hello Privileged Identity Management (PIM) audit log toosee all hello user assignments and activations within a given time period.</span></span> <span data-ttu-id="cc6fa-105">Если требуется toosee hello аудита полного журнала действий в клиенте, включая администратора, пользователь и действий по синхронизации, можно использовать hello [отчеты о доступе и использовании Azure Active Directory.](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="cc6fa-105">If you want toosee hello full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use hello [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-toohello-audit-log"></a><span data-ttu-id="cc6fa-106">Перейдите в журнал аудита toohello</span><span class="sxs-lookup"><span data-stu-id="cc6fa-106">Navigate toohello audit log</span></span>
<span data-ttu-id="cc6fa-107">Из hello [портал Azure](https://portal.azure.com) панели мониторинга, выберите hello **Azure AD Privileged Identity Management** приложения.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-107">From hello [Azure portal](https://portal.azure.com) dashboard, select hello **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="cc6fa-108">После этого доступ к журналу аудита hello, щелкнув **управление привилегированных ролей** > **журнал аудита** в панели мониторинга PIM hello.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-108">From there, access hello audit log by clicking **Manage privileged roles** > **Audit history** in hello PIM dashboard.</span></span>

## <a name="hello-audit-log-graph"></a><span data-ttu-id="cc6fa-109">График журнала аудита Hello</span><span class="sxs-lookup"><span data-stu-id="cc6fa-109">hello audit log graph</span></span>
<span data-ttu-id="cc6fa-110">Можно использовать hello аудита журнала tooview hello общее количество активаций, max активаций в день и среднее количество активаций в день в виде графика.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-110">You can use hello audit log tooview hello total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="cc6fa-111">Можно также фильтровать данные hello по ролям при наличии более чем одной роли в журнал аудита hello.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-111">You can also filter hello data by role if there is more than one role in hello audit history.</span></span>

<span data-ttu-id="cc6fa-112">Используйте hello **время**, **действия**, и **роли** журнала hello toosort кнопки.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-112">Use hello **time**, **action**, and **role** buttons toosort hello log.</span></span>

## <a name="hello-audit-log-list"></a><span data-ttu-id="cc6fa-113">Список журналов аудита Hello</span><span class="sxs-lookup"><span data-stu-id="cc6fa-113">hello audit log list</span></span>
<span data-ttu-id="cc6fa-114">содержит столбцы Hello hello список журналов аудита.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-114">hello columns in hello audit log list are:</span></span>

* <span data-ttu-id="cc6fa-115">**Запрашивающая сторона** -hello пользователя, запросившего активации роли hello или изменение.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-115">**Requestor** - hello user who requested hello role activation or change.</span></span>  <span data-ttu-id="cc6fa-116">Если значение hello «Azure система», проверьте журнал аудита Azure hello Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-116">If hello value is "Azure System", check hello Azure audit log for more information.</span></span>
* <span data-ttu-id="cc6fa-117">**Пользователь** -hello пользователя выполняется активация или tooa роль.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-117">**User** - hello user who is activating or assigned tooa role.</span></span>
* <span data-ttu-id="cc6fa-118">**Роль** -hello роли назначения или активизации пользователем hello.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-118">**Role** - hello role assigned or activated by hello user.</span></span>
* <span data-ttu-id="cc6fa-119">**Действие** - hello действия, производимые hello запрашивающей стороны.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-119">**Action** - hello actions taken by hello requestor.</span></span> <span data-ttu-id="cc6fa-120">Они могут включать назначение, отмену назначения, активацию или отмену активации.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="cc6fa-121">**Время** — Если выполнялось действие hello.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-121">**Time** - when hello action occurred.</span></span>
* <span data-ttu-id="cc6fa-122">**Рассуждения** -Если текст был введен в поле Причина hello во время активации, он будет отображаться здесь.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-122">**Reasoning** - if any text was entered into hello reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="cc6fa-123">**Срок действия** — применимо только для активации ролей.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-hello-audit-log"></a><span data-ttu-id="cc6fa-124">Настройте фильтрацию журнала аудита hello</span><span class="sxs-lookup"><span data-stu-id="cc6fa-124">Filter hello audit log</span></span>
<span data-ttu-id="cc6fa-125">Можно фильтровать информацию hello, который отображается в журнал аудита hello, щелкнув hello **фильтра** кнопки.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-125">You can filter hello information that shows up in hello audit log by clicking hello **Filter** button.</span></span>  <span data-ttu-id="cc6fa-126">Hello **колонку параметров диаграммы обновления** будут отображаться.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-126">hello **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="cc6fa-127">После выбора hello фильтры, нажмите кнопку **обновление** toofilter hello данных журнала hello.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-127">After you set hello filters, click **Update** toofilter hello data in hello log.</span></span>  <span data-ttu-id="cc6fa-128">Если данные hello не отображаются прямо сейчас, обновите страницу приветствия.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-128">If hello data doesn't appear right away, refresh hello page.</span></span>

### <a name="change-hello-date-range"></a><span data-ttu-id="cc6fa-129">Изменить диапазон дат hello</span><span class="sxs-lookup"><span data-stu-id="cc6fa-129">Change hello date range</span></span>
<span data-ttu-id="cc6fa-130">Используйте hello **сегодня**, **прошлой неделе**, **прошлый месяц**, или **настраиваемый** кнопки toochange hello временной диапазон журнала аудита hello.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-130">Use hello **Today**, **Past Week**, **Past Month**, or **Custom** buttons toochange hello time range of hello audit log.</span></span>

<span data-ttu-id="cc6fa-131">При выборе hello **настраиваемый** кнопки, вам будет предоставлена **из** поля «Дата» и **для** Дата поле toospecify диапазон дат для журнала hello.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-131">When you choose hello **Custom** button, you will be given a **From** date field and a **To** date field toospecify a range of dates for hello log.</span></span>  <span data-ttu-id="cc6fa-132">Можно вводить даты hello в формате мм/дд/гггг или щелкнуть hello **календаря** значок и выберите hello дату из календаря.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-132">You can either enter hello dates in MM/DD/YYYY format or click on hello **calendar** icon and choose hello date from a calendar.</span></span>

### <a name="change-hello-roles-included-in-hello-log"></a><span data-ttu-id="cc6fa-133">Изменить роли hello, включенные в журнал hello</span><span class="sxs-lookup"><span data-stu-id="cc6fa-133">Change hello roles included in hello log</span></span>
<span data-ttu-id="cc6fa-134">Установите или снимите hello **роли** журнала флажок Далее tooeach роли tooinclude или исключить его из hello.</span><span class="sxs-lookup"><span data-stu-id="cc6fa-134">Check or uncheck hello **Role** checkbox next tooeach role tooinclude or exclude it from hello log.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="cc6fa-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cc6fa-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

