---
title: "Политики доступа к данным в Azure Time Series Insights | Документация Майкрософт"
description: "Это руководство содержит сведения об управлении политиками доступа к данным в Time Series Insights"
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
ms.openlocfilehash: e975c6d8f217bc73948c0c046204b16b1a742bc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="grant-data-access-to-a-time-series-insights-environment-using-azure-portal"></a><span data-ttu-id="665f1-103">Предоставление доступа к данным для среды Time Series Insights с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="665f1-103">Grant data access to a Time Series Insights environment using Azure portal</span></span>

<span data-ttu-id="665f1-104">Среда Time Series Insights содержит 2 типа независимых политик доступа:</span><span class="sxs-lookup"><span data-stu-id="665f1-104">Time Series Insights environments have two independent types of access policies:</span></span>

* <span data-ttu-id="665f1-105">политики управления доступом;</span><span class="sxs-lookup"><span data-stu-id="665f1-105">Management access policies</span></span>
* <span data-ttu-id="665f1-106">политики доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="665f1-106">Data access policies</span></span>

<span data-ttu-id="665f1-107">Оба типа политик предоставляют субъектам Azure Active Directory (пользователям или приложениям) различные разрешения для конкретной среды.</span><span class="sxs-lookup"><span data-stu-id="665f1-107">Both policies grant Azure Active Directory principals (users and apps) various permissions on a particular environment.</span></span> <span data-ttu-id="665f1-108">Субъекты (пользователи и приложения) должны принадлежать к службе Active Directory (или клиенту Azure), связанной с подпиской, содержащей среду.</span><span class="sxs-lookup"><span data-stu-id="665f1-108">The principals (users and apps) must belong to the active directory (or “Azure tenant”) associated with the subscription containing the environment.</span></span>

<span data-ttu-id="665f1-109">Политики управления доступом предоставляют разрешения, связанные с конфигурацией среды, например:</span><span class="sxs-lookup"><span data-stu-id="665f1-109">Management access policies grant permissions related to the configuration of the environment, such as</span></span>
*   <span data-ttu-id="665f1-110">создание и удаление среды, источников событий и справочных наборов данных;</span><span class="sxs-lookup"><span data-stu-id="665f1-110">Creation and deletion of the environment, event sources, reference data sets, and</span></span>
*   <span data-ttu-id="665f1-111">управление политиками доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="665f1-111">Management of the data access policies.</span></span>

<span data-ttu-id="665f1-112">Политики доступа к данным предоставляют разрешения для отправки запросов данных, обработки ссылочных данных в среде, а также предоставляют другим пользователям среды доступ к сохраненным запросам и перспективам.</span><span class="sxs-lookup"><span data-stu-id="665f1-112">Data access policies grant permissions to issue data queries, manipulate reference data in the environment, and share saved queries and perspectives associated with the environment.</span></span>

<span data-ttu-id="665f1-113">Эти политики позволяют четко разделить доступ к управлению среды и доступ к данным в среде.</span><span class="sxs-lookup"><span data-stu-id="665f1-113">The two kinds of policies allow clear separation between access to the management of the environment and access to the data inside the environment.</span></span> <span data-ttu-id="665f1-114">Например, можно установить среду таким образом, что владелец или создатель среды не будет иметь доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="665f1-114">For example, it is possible to setup an environment such that the owner/creator of the environment is removed from the data access.</span></span> <span data-ttu-id="665f1-115">Пользователи и службы, которые могут считывать данные из среды, также могут не иметь доступа к конфигурации среды.</span><span class="sxs-lookup"><span data-stu-id="665f1-115">As well as users and services that are allowed to read data from the environment may be granted no access to the configuration of the environment.</span></span>

## <a name="grant-data-access"></a><span data-ttu-id="665f1-116">Предоставление доступа к данным</span><span class="sxs-lookup"><span data-stu-id="665f1-116">Grant data access</span></span>
<span data-ttu-id="665f1-117">Ниже показано, как предоставить доступ к данным для участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="665f1-117">The following steps show how to grant data access for a user principal:</span></span>

1.  <span data-ttu-id="665f1-118">Выполните вход на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="665f1-118">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="665f1-119">Щелкните "Все ресурсы" в меню слева на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="665f1-119">Click “All resources” in the menu on the left side of the Azure portal.</span></span>
3.  <span data-ttu-id="665f1-120">Выберите среду Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="665f1-120">Select your Time Series Insights environment.</span></span>

  ![Управление исходной средой Time Series Insights](media/data-access/getstarted-grant-data-access1.png)

4.  <span data-ttu-id="665f1-122">Выберите Data Plane Access (Доступ к плоскости данных) и щелкните "Добавить".</span><span class="sxs-lookup"><span data-stu-id="665f1-122">Select “Data Plane Access”, click “Add”</span></span>

  ![Управление источником Time Series Insights — "Добавить"](media/data-access/getstarted-grant-data-access2.png)

5.  <span data-ttu-id="665f1-124">Щелкните "Выбор пользователя".</span><span class="sxs-lookup"><span data-stu-id="665f1-124">Click “Select user”.</span></span>
6.  <span data-ttu-id="665f1-125">Найдите пользователя по электронной почте и выберите его.</span><span class="sxs-lookup"><span data-stu-id="665f1-125">Search and select user by the email.</span></span>
7.  <span data-ttu-id="665f1-126">В колонке "Выбор пользователя" нажмите кнопку "Выбрать".</span><span class="sxs-lookup"><span data-stu-id="665f1-126">Click “Select” in “Select User” blade.</span></span>

  ![Управление источником Time Series Insights — "Выбор пользователя"](media/data-access/getstarted-grant-data-access3.png)

8.  <span data-ttu-id="665f1-128">Щелкните "Выбор ролей".</span><span class="sxs-lookup"><span data-stu-id="665f1-128">Click “Select role”.</span></span>
9.  <span data-ttu-id="665f1-129">Выберите "Участник", если вы хотите разрешить пользователю изменять ссылочные данные и предоставить другим пользователям среды доступ к сохраненным запросам и перспективам.</span><span class="sxs-lookup"><span data-stu-id="665f1-129">Select “Contributor” if you want to allow user to change reference data and share saved queries and perspectives with other users of the environment.</span></span> <span data-ttu-id="665f1-130">В противном случае выберите "Читатель", чтобы разрешить пользователю запрашивать данные в среде и сохранять в ней личные (не общие) запросы.</span><span class="sxs-lookup"><span data-stu-id="665f1-130">Otherwise select “Reader” to allow user query data in the environment and save personal (not shared) queries in the environment.</span></span>
10. <span data-ttu-id="665f1-131">В колонке "Выбор ролей" нажмите кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="665f1-131">Click “Ok” in the “Select Role” blade.</span></span>

  ![Управление источником Time Series Insights — "Выбор ролей"](media/data-access/getstarted-grant-data-access4.png)

11. <span data-ttu-id="665f1-133">В колонке Select User Role (Выбор роли пользователя) нажмите кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="665f1-133">Click “Ok” in the “Select User Role” blade.</span></span>
12. <span data-ttu-id="665f1-134">Вы должны увидеть следующее:</span><span class="sxs-lookup"><span data-stu-id="665f1-134">You should see:</span></span>

  ![Управление источником Time Series Insights — результаты](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a><span data-ttu-id="665f1-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="665f1-136">Next steps</span></span>

* <span data-ttu-id="665f1-137">[Создайте источник событий](time-series-insights-add-event-source.md).</span><span class="sxs-lookup"><span data-stu-id="665f1-137">[Create an event source](time-series-insights-add-event-source.md)</span></span>
* <span data-ttu-id="665f1-138">[Отправьте события](time-series-insights-send-events.md) в источник событий.</span><span class="sxs-lookup"><span data-stu-id="665f1-138">[Send events](time-series-insights-send-events.md) to the event source</span></span>
* <span data-ttu-id="665f1-139">Просмотрите свою среду на [портале Time Series Insights](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="665f1-139">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
