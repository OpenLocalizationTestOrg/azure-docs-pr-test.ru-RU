---
title: "aaaData политики доступа в Azure Insights ряда времени | Документы Microsoft"
description: "В этом учебнике вы узнаете toomanage политикам доступа в серии аналитики времени"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a><span data-ttu-id="e6e16-103">Предоставьте среда доступа к данным tooa аналитики ряда времени с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="e6e16-103">Grant data access tooa Time Series Insights environment using Azure portal</span></span>

<span data-ttu-id="e6e16-104">Среда Time Series Insights содержит 2 типа независимых политик доступа:</span><span class="sxs-lookup"><span data-stu-id="e6e16-104">Time Series Insights environments have two independent types of access policies:</span></span>

* <span data-ttu-id="e6e16-105">политики управления доступом;</span><span class="sxs-lookup"><span data-stu-id="e6e16-105">Management access policies</span></span>
* <span data-ttu-id="e6e16-106">политики доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="e6e16-106">Data access policies</span></span>

<span data-ttu-id="e6e16-107">Оба типа политик предоставляют субъектам Azure Active Directory (пользователям или приложениям) различные разрешения для конкретной среды.</span><span class="sxs-lookup"><span data-stu-id="e6e16-107">Both policies grant Azure Active Directory principals (users and apps) various permissions on a particular environment.</span></span> <span data-ttu-id="e6e16-108">Hello субъекты (пользователи и приложения) должны принадлежать toohello active directory (или «Клиент Windows Azure»), связанных с hello подписку, содержащую hello среды.</span><span class="sxs-lookup"><span data-stu-id="e6e16-108">hello principals (users and apps) must belong toohello active directory (or “Azure tenant”) associated with hello subscription containing hello environment.</span></span>

<span data-ttu-id="e6e16-109">Политики управления доступом предоставить разрешения связанных toohello конфигурация hello среды, такие как</span><span class="sxs-lookup"><span data-stu-id="e6e16-109">Management access policies grant permissions related toohello configuration of hello environment, such as</span></span>
*   <span data-ttu-id="e6e16-110">Создание и удаление среды hello, источники событий ссылаться на наборы данных и</span><span class="sxs-lookup"><span data-stu-id="e6e16-110">Creation and deletion of hello environment, event sources, reference data sets, and</span></span>
*   <span data-ttu-id="e6e16-111">Управление данными hello политики доступа.</span><span class="sxs-lookup"><span data-stu-id="e6e16-111">Management of hello data access policies.</span></span>

<span data-ttu-id="e6e16-112">Политики доступа данных tooissue запросы данных, разрешения ссылочных данных в среде hello, совместное и сохраненные запросы и перспективам, связанным со средой hello.</span><span class="sxs-lookup"><span data-stu-id="e6e16-112">Data access policies grant permissions tooissue data queries, manipulate reference data in hello environment, and share saved queries and perspectives associated with hello environment.</span></span>

<span data-ttu-id="e6e16-113">Hello два вида политики позволяют четкое разделение между toohello управления доступом hello среды и доступ к данным toohello внутри среды hello.</span><span class="sxs-lookup"><span data-stu-id="e6e16-113">hello two kinds of policies allow clear separation between access toohello management of hello environment and access toohello data inside hello environment.</span></span> <span data-ttu-id="e6e16-114">Например это возможно toosetup среду таким образом, что hello владелец создатель hello среды удаляется из hello доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="e6e16-114">For example, it is possible toosetup an environment such that hello owner/creator of hello environment is removed from hello data access.</span></span> <span data-ttu-id="e6e16-115">А также пользователей и служб, которые допускаются tooread данные из среды hello могут предоставляться без настройки доступа toohello hello среды.</span><span class="sxs-lookup"><span data-stu-id="e6e16-115">As well as users and services that are allowed tooread data from hello environment may be granted no access toohello configuration of hello environment.</span></span>

## <a name="grant-data-access"></a><span data-ttu-id="e6e16-116">Предоставление доступа к данным</span><span class="sxs-lookup"><span data-stu-id="e6e16-116">Grant data access</span></span>
<span data-ttu-id="e6e16-117">Hello следующие шаги показывают, как доступ к данным toogrant для участника-пользователя:</span><span class="sxs-lookup"><span data-stu-id="e6e16-117">hello following steps show how toogrant data access for a user principal:</span></span>

1.  <span data-ttu-id="e6e16-118">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e6e16-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="e6e16-119">В меню hello hello левой части hello портал Azure, выберите «Все ресурсы».</span><span class="sxs-lookup"><span data-stu-id="e6e16-119">Click “All resources” in hello menu on hello left side of hello Azure portal.</span></span>
3.  <span data-ttu-id="e6e16-120">Выберите среду Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="e6e16-120">Select your Time Series Insights environment.</span></span>

  ![Управление источником времени серии аналитики hello - среды](media/data-access/getstarted-grant-data-access1.png)

4.  <span data-ttu-id="e6e16-122">Выберите Data Plane Access (Доступ к плоскости данных) и щелкните "Добавить".</span><span class="sxs-lookup"><span data-stu-id="e6e16-122">Select “Data Plane Access”, click “Add”</span></span>

  ![Управление источником времени серии аналитики hello - Добавление](media/data-access/getstarted-grant-data-access2.png)

5.  <span data-ttu-id="e6e16-124">Щелкните "Выбор пользователя".</span><span class="sxs-lookup"><span data-stu-id="e6e16-124">Click “Select user”.</span></span>
6.  <span data-ttu-id="e6e16-125">Поиск и выбор пользователя по электронной почте hello.</span><span class="sxs-lookup"><span data-stu-id="e6e16-125">Search and select user by hello email.</span></span>
7.  <span data-ttu-id="e6e16-126">В колонке "Выбор пользователя" нажмите кнопку "Выбрать".</span><span class="sxs-lookup"><span data-stu-id="e6e16-126">Click “Select” in “Select User” blade.</span></span>

  ![Управление источником времени серии аналитики hello — Выбор пользователя](media/data-access/getstarted-grant-data-access3.png)

8.  <span data-ttu-id="e6e16-128">Щелкните "Выбор ролей".</span><span class="sxs-lookup"><span data-stu-id="e6e16-128">Click “Select role”.</span></span>
9.  <span data-ttu-id="e6e16-129">Выберите «Участник», tooallow пользователя toochange ссылочных данных и предоставить другим пользователям среды hello сохраненные запросы и перспективы.</span><span class="sxs-lookup"><span data-stu-id="e6e16-129">Select “Contributor” if you want tooallow user toochange reference data and share saved queries and perspectives with other users of hello environment.</span></span> <span data-ttu-id="e6e16-130">В противном случае выберите «Чтения» tooallow пользователь запросов данных в среде hello и сохранение личных (не общем) запросов в среде hello.</span><span class="sxs-lookup"><span data-stu-id="e6e16-130">Otherwise select “Reader” tooallow user query data in hello environment and save personal (not shared) queries in hello environment.</span></span>
10. <span data-ttu-id="e6e16-131">В колонке «Выберите роль» hello, нажмите кнопку «ОК».</span><span class="sxs-lookup"><span data-stu-id="e6e16-131">Click “Ok” in hello “Select Role” blade.</span></span>

  ![Управление источником времени серии аналитики hello — выберите роль](media/data-access/getstarted-grant-data-access4.png)

11. <span data-ttu-id="e6e16-133">В колонке «Выберите роль пользователя» hello, нажмите кнопку «ОК».</span><span class="sxs-lookup"><span data-stu-id="e6e16-133">Click “Ok” in hello “Select User Role” blade.</span></span>
12. <span data-ttu-id="e6e16-134">Вы должны увидеть следующее:</span><span class="sxs-lookup"><span data-stu-id="e6e16-134">You should see:</span></span>

  ![Управление источником времени серии аналитики hello - результаты](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a><span data-ttu-id="e6e16-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e6e16-136">Next steps</span></span>

* [<span data-ttu-id="e6e16-137">Создание источника событий</span><span class="sxs-lookup"><span data-stu-id="e6e16-137">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="e6e16-138">[Отправлять события](time-series-insights-send-events.md) toohello источник события</span><span class="sxs-lookup"><span data-stu-id="e6e16-138">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="e6e16-139">Просмотрите свою среду на [портале Time Series Insights](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e6e16-139">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
