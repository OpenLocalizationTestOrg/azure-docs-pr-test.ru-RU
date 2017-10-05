---
title: "Операции Synchronization Service Manager Azure AD Connect | Документация Майкрософт"
description: "Общие сведения о вкладке \"Operations\" (Операции) в Synchronization Service Manager для Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 97a26565-618f-4313-8711-5925eeb47cdc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1475e4fcd11eb008badba49665f4af6029a1697
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="using-the-sync-service-manager-operations-tab"></a><span data-ttu-id="9e2d5-103">Использование вкладки "Operations" (Операции) в Synchronization Service Manager</span><span class="sxs-lookup"><span data-stu-id="9e2d5-103">Using the Sync Service Manager Operations tab</span></span>

![Диспетчер службы синхронизации](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

<span data-ttu-id="9e2d5-105">На вкладке "Operations" (Операции) отображаются результаты последних операций.</span><span class="sxs-lookup"><span data-stu-id="9e2d5-105">The operations tab shows the results from the most recent operations.</span></span> <span data-ttu-id="9e2d5-106">Эта вкладка крайне важна для понимания и устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="9e2d5-106">This tab is key to understand and troubleshoot issues.</span></span>

## <a name="understand-the-information-visible-in-the-operations-tab"></a><span data-ttu-id="9e2d5-107">Пояснение информации, отображаемой на вкладке "Operations" (Операции)</span><span class="sxs-lookup"><span data-stu-id="9e2d5-107">Understand the information visible in the operations tab</span></span>
<span data-ttu-id="9e2d5-108">В верхней части отображены все операции выполнения в хронологическом порядке.</span><span class="sxs-lookup"><span data-stu-id="9e2d5-108">The top half shows all runs in chronological order.</span></span> <span data-ttu-id="9e2d5-109">По умолчанию журнал операций содержит сведения за последние семь дней, но эту цифру можно изменить с помощью [планировщика](active-directory-aadconnectsync-feature-scheduler.md).</span><span class="sxs-lookup"><span data-stu-id="9e2d5-109">By default, the operations log keeps information about the last seven days, but this setting can be changed with the [scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span> <span data-ttu-id="9e2d5-110">Вы можете найти любую операцию выполнения, которая не была завершена успешно.</span><span class="sxs-lookup"><span data-stu-id="9e2d5-110">You want to look for any run that does not show a success status.</span></span> <span data-ttu-id="9e2d5-111">Вы также можете изменить порядок сортировки, щелкая заголовки.</span><span class="sxs-lookup"><span data-stu-id="9e2d5-111">You can change the sorting by clicking the headers.</span></span>

<span data-ttu-id="9e2d5-112">Столбец **Status** (Состояние) является самым важным, он показывает наиболее серьезную проблему при выполнении.</span><span class="sxs-lookup"><span data-stu-id="9e2d5-112">The **Status** column is the most important information and shows the most severe problem for a run.</span></span> <span data-ttu-id="9e2d5-113">Ниже приводится краткая сводка наиболее распространенных состояний в порядке приоритета для анализа (где * означает, что возможно несколько строк ошибки).</span><span class="sxs-lookup"><span data-stu-id="9e2d5-113">Here is a quick summary of the most common statuses in order of priority to investigate (where * indicate several possible error strings).</span></span>

| <span data-ttu-id="9e2d5-114">Status</span><span class="sxs-lookup"><span data-stu-id="9e2d5-114">Status</span></span> | <span data-ttu-id="9e2d5-115">Комментарий</span><span class="sxs-lookup"><span data-stu-id="9e2d5-115">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="9e2d5-116">stopped-*</span><span class="sxs-lookup"><span data-stu-id="9e2d5-116">stopped-*</span></span> |<span data-ttu-id="9e2d5-117">Не удалось завершить выполнение.</span><span class="sxs-lookup"><span data-stu-id="9e2d5-117">The run could not complete.</span></span> <span data-ttu-id="9e2d5-118">Например, если удаленная система не работает и с ней не удается связаться.</span><span class="sxs-lookup"><span data-stu-id="9e2d5-118">For example, if the remote system is down and cannot be contacted.</span></span> |
| <span data-ttu-id="9e2d5-119">stopped-error-limit</span><span class="sxs-lookup"><span data-stu-id="9e2d5-119">stopped-error-limit</span></span> |<span data-ttu-id="9e2d5-120">Обнаружено более 5000 ошибок.</span><span class="sxs-lookup"><span data-stu-id="9e2d5-120">There are more than 5,000 errors.</span></span> <span data-ttu-id="9e2d5-121">Выполнение было автоматически остановлено из-за большого количества ошибок.</span><span class="sxs-lookup"><span data-stu-id="9e2d5-121">The run was automatically stopped due to the large number of errors.</span></span> |
| <span data-ttu-id="9e2d5-122">completed-\*-errors</span><span class="sxs-lookup"><span data-stu-id="9e2d5-122">completed-\*-errors</span></span> |<span data-ttu-id="9e2d5-123">Выполнение завершено, но есть ошибки (меньше 5000), которые необходимо изучить.</span><span class="sxs-lookup"><span data-stu-id="9e2d5-123">The run completed, but there are errors (fewer than 5,000) that should be investigated.</span></span> |
| <span data-ttu-id="9e2d5-124">completed-\*-warnings</span><span class="sxs-lookup"><span data-stu-id="9e2d5-124">completed-\*-warnings</span></span> |<span data-ttu-id="9e2d5-125">Запуск завершен, но некоторые данные не находятся в ожидаемом состоянии.</span><span class="sxs-lookup"><span data-stu-id="9e2d5-125">The run completed, but some data is not in the expected state.</span></span> <span data-ttu-id="9e2d5-126">Если обнаружены ошибки, такое сообщение обычно является указателем.</span><span class="sxs-lookup"><span data-stu-id="9e2d5-126">If you have errors, then this message is usually only a symptom.</span></span> <span data-ttu-id="9e2d5-127">Пока вы не исправили ошибки, не следует рассматривать предупреждения.</span><span class="sxs-lookup"><span data-stu-id="9e2d5-127">Until you have addressed errors, you should not investigate warnings.</span></span> |
| <span data-ttu-id="9e2d5-128">Успешное завершение</span><span class="sxs-lookup"><span data-stu-id="9e2d5-128">success</span></span> |<span data-ttu-id="9e2d5-129">Проблемы отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="9e2d5-129">No issues.</span></span> |

<span data-ttu-id="9e2d5-130">При выборе строки в нижней части отображаются сведения об этой операции выполнения.</span><span class="sxs-lookup"><span data-stu-id="9e2d5-130">When you select a row, the bottom updates to show the details of that run.</span></span> <span data-ttu-id="9e2d5-131">Слева внизу может отображаться список **Step #**(Шаг №).</span><span class="sxs-lookup"><span data-stu-id="9e2d5-131">To the far left of the bottom, you might have a list saying **Step #**.</span></span> <span data-ttu-id="9e2d5-132">Он отображается, только если у вас в лесу несколько доменов, где каждый домен представлен шагом.</span><span class="sxs-lookup"><span data-stu-id="9e2d5-132">This list only appears if you have multiple domains in your forest where each domain is represented by a step.</span></span> <span data-ttu-id="9e2d5-133">Имя домена можно найти в разделе **Partition**(Секция).</span><span class="sxs-lookup"><span data-stu-id="9e2d5-133">The domain name can be found under the heading **Partition**.</span></span> <span data-ttu-id="9e2d5-134">В разделе **Synchronization Statistics**(Статистика синхронизации) можно найти дополнительные сведения о числе обработанных изменений.</span><span class="sxs-lookup"><span data-stu-id="9e2d5-134">Under **Synchronization Statistics**, you can find more information about the number of changes that were processed.</span></span> <span data-ttu-id="9e2d5-135">Щелкая ссылки, можно получить список измененных объектов.</span><span class="sxs-lookup"><span data-stu-id="9e2d5-135">You can click the links to get a list of the changed objects.</span></span> <span data-ttu-id="9e2d5-136">Если у вас есть объекты с ошибкой, они отображаются в разделе **Synchronization Errors**(Ошибки синхронизации).</span><span class="sxs-lookup"><span data-stu-id="9e2d5-136">If you have objects with errors, those errors show up under **Synchronization Errors**.</span></span>

<span data-ttu-id="9e2d5-137">Дополнительные сведения см. в разделе [Устранение неполадок синхронизации объекта с Azure AD](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md).</span><span class="sxs-lookup"><span data-stu-id="9e2d5-137">For more information, see [troubleshoot an object that is not synchronizing](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e2d5-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9e2d5-138">Next steps</span></span>
<span data-ttu-id="9e2d5-139">Узнайте больше о настройке [службы синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md) .</span><span class="sxs-lookup"><span data-stu-id="9e2d5-139">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="9e2d5-140">Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="9e2d5-140">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
