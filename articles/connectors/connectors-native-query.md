---
title: "Действие запроса aaaAdd hello в приложениях для логики | Документы Microsoft"
description: "Обзор hello действие по запросу для выполнения действий, таких как массив фильтра."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a><span data-ttu-id="22c82-103">Начало работы с действием запроса hello</span><span class="sxs-lookup"><span data-stu-id="22c82-103">Get started with hello query action</span></span>
<span data-ttu-id="22c82-104">С помощью действия запроса hello, можно работать с пакетами и массивы tooaccomplish рабочих процессов:</span><span class="sxs-lookup"><span data-stu-id="22c82-104">By using hello query action, you can work with batches and arrays tooaccomplish workflows to:</span></span>

* <span data-ttu-id="22c82-105">создать задачу для всех записей с высоким приоритетом, имеющихся в базе данных;</span><span class="sxs-lookup"><span data-stu-id="22c82-105">Create a task for all high-priority records from a database.</span></span>
* <span data-ttu-id="22c82-106">сохранить все вложения в формате PDF для электронной почты в большой двоичный объект Azure.</span><span class="sxs-lookup"><span data-stu-id="22c82-106">Save all PDF attachments for emails into an Azure blob.</span></span>

<span data-ttu-id="22c82-107">tooget работы с использованием действия запроса hello в приложении логику в разделе [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="22c82-107">tooget started using hello query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-query-action"></a><span data-ttu-id="22c82-108">Используйте действие hello запроса</span><span class="sxs-lookup"><span data-stu-id="22c82-108">Use hello query action</span></span>
<span data-ttu-id="22c82-109">Действие — это операции, выполняемые hello рабочего процесса, определенные в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="22c82-109">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="22c82-110">[Дополнительные сведения о действиях](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="22c82-110">[Learn more about actions](connectors-overview.md).</span></span>  

<span data-ttu-id="22c82-111">Действие запроса Hello в настоящее время имеет одну операцию с именем hello фильтра массива, который предоставляется в конструкторе hello.</span><span class="sxs-lookup"><span data-stu-id="22c82-111">hello query action currently has one operation, called hello filter array, that is exposed in hello designer.</span></span> <span data-ttu-id="22c82-112">Это дает tooquery массив и возвращения набора отфильтрованные результаты.</span><span class="sxs-lookup"><span data-stu-id="22c82-112">This allows you tooquery an array and return a set of filtered results.</span></span>

<span data-ttu-id="22c82-113">Ниже описан процесс добавления этой операции в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="22c82-113">Here's how you can add it in a logic app:</span></span>

1. <span data-ttu-id="22c82-114">Выберите hello **новый шаг** кнопки.</span><span class="sxs-lookup"><span data-stu-id="22c82-114">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="22c82-115">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="22c82-115">Choose **Add an action**.</span></span>
3. <span data-ttu-id="22c82-116">Введите в поле поиска действие hello **фильтра** toolist hello **массив фильтра** действие.</span><span class="sxs-lookup"><span data-stu-id="22c82-116">In hello action search box, type **filter** toolist hello **Filter array** action.</span></span>
   
    ![Выберите действие запроса hello](./media/connectors-native-query/using-action-1.png)
4. <span data-ttu-id="22c82-118">Выберите toofilter массива.</span><span class="sxs-lookup"><span data-stu-id="22c82-118">Select an array toofilter.</span></span> <span data-ttu-id="22c82-119">(hello следующем снимке экрана показано hello массив результатов поиска Twitter.)</span><span class="sxs-lookup"><span data-stu-id="22c82-119">(hello following screenshot shows hello array of results from a Twitter search.)</span></span>
5. <span data-ttu-id="22c82-120">Создайте tooevaluate условие для каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="22c82-120">Create a condition tooevaluate on each item.</span></span> <span data-ttu-id="22c82-121">(следующий снимок экрана приветствия фильтры твиты пользователей, имеющих более 100 последователи.)</span><span class="sxs-lookup"><span data-stu-id="22c82-121">(hello following screenshot filters tweets from users who have more than 100 followers.)</span></span>
   
    ![Действие запроса завершения hello](./media/connectors-native-query/using-action-2.png)
   
    <span data-ttu-id="22c82-123">Действие Hello будет выдавать новый массив, содержащий только результатов, соответствующих требованиям фильтра hello.</span><span class="sxs-lookup"><span data-stu-id="22c82-123">hello action will output a new array that contains only results that met hello filter requirements.</span></span>
6. <span data-ttu-id="22c82-124">Щелкните hello верхнего левого угла toosave инструментов hello и вашей логики приложения будет как сохранять и публикации (активировать).</span><span class="sxs-lookup"><span data-stu-id="22c82-124">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="query-action"></a><span data-ttu-id="22c82-125">Действие запроса</span><span class="sxs-lookup"><span data-stu-id="22c82-125">Query action</span></span>
<span data-ttu-id="22c82-126">Ниже приведены hello сведения для действия hello, поддерживающий этот соединитель.</span><span class="sxs-lookup"><span data-stu-id="22c82-126">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="22c82-127">Соединитель Hello имеет единственным возможным действием.</span><span class="sxs-lookup"><span data-stu-id="22c82-127">hello connector has one possible action.</span></span>

| <span data-ttu-id="22c82-128">Действие</span><span class="sxs-lookup"><span data-stu-id="22c82-128">Action</span></span> | <span data-ttu-id="22c82-129">Описание</span><span class="sxs-lookup"><span data-stu-id="22c82-129">Description</span></span> |
| --- | --- |
| <span data-ttu-id="22c82-130">Фильтрация массива</span><span class="sxs-lookup"><span data-stu-id="22c82-130">Filter array</span></span> |<span data-ttu-id="22c82-131">Проверяет условие для каждого элемента в массиве и возвращает результаты hello</span><span class="sxs-lookup"><span data-stu-id="22c82-131">Evaluates a condition for each item in an array and returns hello results</span></span> |

## <a name="action-details"></a><span data-ttu-id="22c82-132">Сведения о действиях</span><span class="sxs-lookup"><span data-stu-id="22c82-132">Action details</span></span>
<span data-ttu-id="22c82-133">Действие по запросу Hello поставляется с единственным возможным действием.</span><span class="sxs-lookup"><span data-stu-id="22c82-133">hello query action comes with one possible action.</span></span> <span data-ttu-id="22c82-134">Hello следующих таблицах описаны необходимые hello и необязательные поля ввода для действия hello и hello соответствующие сведения о выходных данных, связанных с помощью hello действия.</span><span class="sxs-lookup"><span data-stu-id="22c82-134">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

### <a name="filter-array"></a><span data-ttu-id="22c82-135">Фильтрация массива</span><span class="sxs-lookup"><span data-stu-id="22c82-135">Filter array</span></span>
<span data-ttu-id="22c82-136">Здесь представлены Hello поля входных данных для действия hello, поэтому исходящих HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="22c82-136">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="22c82-137">Звездочка (*) означает, что это поле обязательное для заполнения.</span><span class="sxs-lookup"><span data-stu-id="22c82-137">A * means that it is a required field.</span></span>

| <span data-ttu-id="22c82-138">Отображаемое имя</span><span class="sxs-lookup"><span data-stu-id="22c82-138">Display name</span></span> | <span data-ttu-id="22c82-139">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="22c82-139">Property name</span></span> | <span data-ttu-id="22c82-140">Описание</span><span class="sxs-lookup"><span data-stu-id="22c82-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="22c82-141">Из*</span><span class="sxs-lookup"><span data-stu-id="22c82-141">From*</span></span> |<span data-ttu-id="22c82-142">from</span><span class="sxs-lookup"><span data-stu-id="22c82-142">from</span></span> |<span data-ttu-id="22c82-143">Массив toofilter Hello</span><span class="sxs-lookup"><span data-stu-id="22c82-143">hello array toofilter</span></span> |
| <span data-ttu-id="22c82-144">Условие*</span><span class="sxs-lookup"><span data-stu-id="22c82-144">Condition*</span></span> |<span data-ttu-id="22c82-145">где:</span><span class="sxs-lookup"><span data-stu-id="22c82-145">where</span></span> |<span data-ttu-id="22c82-146">Здравствуйте, tooevaluate условие для каждого элемента</span><span class="sxs-lookup"><span data-stu-id="22c82-146">hello condition tooevaluate for each item</span></span> |

<br>

### <a name="output-details"></a><span data-ttu-id="22c82-147">Сведения о выходных данных</span><span class="sxs-lookup"><span data-stu-id="22c82-147">Output details</span></span>
<span data-ttu-id="22c82-148">Hello ниже приведены сведения о выходных данных для hello HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="22c82-148">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="22c82-149">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="22c82-149">Property name</span></span> | <span data-ttu-id="22c82-150">Тип данных</span><span class="sxs-lookup"><span data-stu-id="22c82-150">Data type</span></span> | <span data-ttu-id="22c82-151">Описание</span><span class="sxs-lookup"><span data-stu-id="22c82-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="22c82-152">Отфильтрованный массив</span><span class="sxs-lookup"><span data-stu-id="22c82-152">Filtered array</span></span> |<span data-ttu-id="22c82-153">array</span><span class="sxs-lookup"><span data-stu-id="22c82-153">array</span></span> |<span data-ttu-id="22c82-154">Массив, содержащий объект для каждого результата фильтрации.</span><span class="sxs-lookup"><span data-stu-id="22c82-154">An array that contains an object for each filtered result</span></span> |

## <a name="next-steps"></a><span data-ttu-id="22c82-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="22c82-155">Next steps</span></span>
<span data-ttu-id="22c82-156">Теперь попробуйте платформы hello и [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="22c82-156">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="22c82-157">Вы можете просматривать hello других доступных соединителей в приложении логики, просмотрев нашей [список API-интерфейсы](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="22c82-157">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

