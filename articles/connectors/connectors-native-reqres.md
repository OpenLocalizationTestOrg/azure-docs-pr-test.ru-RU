---
title: "Использование действий запроса и ответа | Документация Майкрософт"
description: "Обзор триггера запроса и ответа, а также их действий в приложении логики Azure"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 566924a4-0988-4d86-9ecd-ad22507858c0
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e45b07d709927af64cfba28dfb0d8ee9cb8893b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-request-and-response-components"></a><span data-ttu-id="07f1e-103">Начало работы с компонентами запросов и ответов</span><span class="sxs-lookup"><span data-stu-id="07f1e-103">Get started with the request and response components</span></span>
<span data-ttu-id="07f1e-104">Благодаря использованию компонентов запросов и ответов в приложении логики можно отвечать на события в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="07f1e-104">With the request and response components in a logic app, you can respond in real time to events.</span></span>

<span data-ttu-id="07f1e-105">Например, вы можете просматривать:</span><span class="sxs-lookup"><span data-stu-id="07f1e-105">For example, you can:</span></span>

* <span data-ttu-id="07f1e-106">ответ на HTTP-запрос, использующий данные из локальной базы данных, через приложение логики;</span><span class="sxs-lookup"><span data-stu-id="07f1e-106">Respond to an HTTP request with data from an on-premises database through a logic app.</span></span>
* <span data-ttu-id="07f1e-107">запуск приложения логики из внешнего события webhook;</span><span class="sxs-lookup"><span data-stu-id="07f1e-107">Trigger a logic app from an external webhook event.</span></span>
* <span data-ttu-id="07f1e-108">вызов приложения логики с помощью действия запроса и ответа из другого приложения логики.</span><span class="sxs-lookup"><span data-stu-id="07f1e-108">Call a logic app with a request and response action from within another logic app.</span></span>

<span data-ttu-id="07f1e-109">Сведения о начале работы с действиями запросов и ответов в приложении логики см. в статье [Создание нового приложения логики, подключающего службы SaaS](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="07f1e-109">To get started using the request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-http-request-trigger"></a><span data-ttu-id="07f1e-110">Использование триггера HTTP-запросов</span><span class="sxs-lookup"><span data-stu-id="07f1e-110">Use the HTTP Request trigger</span></span>
<span data-ttu-id="07f1e-111">Триггер — это событие, которое можно использовать для запуска рабочего процесса, определенного в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="07f1e-111">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="07f1e-112">[Дополнительные сведения о триггерах](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="07f1e-112">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="07f1e-113">Ниже приведен пример последовательности настройки HTTP-запроса в конструкторе приложений логики.</span><span class="sxs-lookup"><span data-stu-id="07f1e-113">Here’s an example sequence of how to set up an HTTP request in the Logic App Designer.</span></span>

1. <span data-ttu-id="07f1e-114">Добавьте триггер **Request - When an HTTP request is received** (Запрос: при получении HTTP-запроса) в свое приложение логики.</span><span class="sxs-lookup"><span data-stu-id="07f1e-114">Add the trigger **Request - When an HTTP request is received** in your logic app.</span></span> <span data-ttu-id="07f1e-115">При необходимости можно предоставить схему JSON (с помощью такого средства, как [JSONSchema.net](http://jsonschema.net)) для текста запроса.</span><span class="sxs-lookup"><span data-stu-id="07f1e-115">You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for the request body.</span></span> <span data-ttu-id="07f1e-116">Это позволит конструктору создать токены свойств в HTTP-запросе.</span><span class="sxs-lookup"><span data-stu-id="07f1e-116">This allows the designer to generate tokens for properties in the HTTP request.</span></span>
2. <span data-ttu-id="07f1e-117">Добавьте еще одно действие, чтобы сохранить приложение логики.</span><span class="sxs-lookup"><span data-stu-id="07f1e-117">Add another action so that you can save the logic app.</span></span>
3. <span data-ttu-id="07f1e-118">После сохранения приложения логики вы можете получить URL-адрес HTTP-запроса из карточки запроса.</span><span class="sxs-lookup"><span data-stu-id="07f1e-118">After saving the logic app, you can get the HTTP request URL from the request card.</span></span>
4. <span data-ttu-id="07f1e-119">Запрос HTTP POST (к примеру, можно использовать средство [Postman](https://www.getpostman.com/)) на URL-адрес запустит приложение логики.</span><span class="sxs-lookup"><span data-stu-id="07f1e-119">An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) to the URL triggers the logic app.</span></span>

> [!NOTE]
> <span data-ttu-id="07f1e-120">Если не определить действие ответа, вызывающему немедленно будет возвращен ответ `202 ACCEPTED` .</span><span class="sxs-lookup"><span data-stu-id="07f1e-120">If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.</span></span> <span data-ttu-id="07f1e-121">Действие ответа можно использовать для настройки ответа.</span><span class="sxs-lookup"><span data-stu-id="07f1e-121">You can use the response action to customize a response.</span></span>
> 
> 

![Триггер ответа](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-the-http-response-action"></a><span data-ttu-id="07f1e-123">Использование действия ответа HTTP</span><span class="sxs-lookup"><span data-stu-id="07f1e-123">Use the HTTP Response action</span></span>
<span data-ttu-id="07f1e-124">Действие ответа HTTP действительно, только если вы используете его в рабочем процессе, запускаемом HTTP-запросом.</span><span class="sxs-lookup"><span data-stu-id="07f1e-124">The HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request.</span></span> <span data-ttu-id="07f1e-125">Если не определить действие ответа, вызывающему немедленно будет возвращен ответ `202 ACCEPTED`.</span><span class="sxs-lookup"><span data-stu-id="07f1e-125">If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.</span></span>  <span data-ttu-id="07f1e-126">Вы можете добавить действие ответа на любом шаге рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="07f1e-126">You can add a response action at any step within the workflow.</span></span> <span data-ttu-id="07f1e-127">Приложение логики не будет закрывать входящий запрос для ответа только в течение 1 минуты.</span><span class="sxs-lookup"><span data-stu-id="07f1e-127">The logic app only keeps the incoming request open for one minute for a response.</span></span>  <span data-ttu-id="07f1e-128">Если ответ не был отправлен из рабочего процесса (а в определении есть действие ответа) в течение 1 минуты, вызывающему будет возвращен ответ `504 GATEWAY TIMEOUT` .</span><span class="sxs-lookup"><span data-stu-id="07f1e-128">After one minute, if no response was sent from the workflow (and a response action exists in the definition), a `504 GATEWAY TIMEOUT` is returned to the caller.</span></span>

<span data-ttu-id="07f1e-129">Вот как можно добавить действие ответа HTTP.</span><span class="sxs-lookup"><span data-stu-id="07f1e-129">Here's how to add an HTTP Response action:</span></span>

1. <span data-ttu-id="07f1e-130">Нажмите кнопку **Новый шаг** .</span><span class="sxs-lookup"><span data-stu-id="07f1e-130">Select the **New Step** button.</span></span>
2. <span data-ttu-id="07f1e-131">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="07f1e-131">Choose **Add an action**.</span></span>
3. <span data-ttu-id="07f1e-132">Чтобы открыть список с действиями ответа, в поле поиска действий введите **Ответ** .</span><span class="sxs-lookup"><span data-stu-id="07f1e-132">In the action search box, type **response** to list the Response action.</span></span>
   
    ![Выбор действия ответа](./media/connectors-native-reqres/using-action-1.png)
4. <span data-ttu-id="07f1e-134">Добавьте параметры, необходимые для сообщения ответа HTTP.</span><span class="sxs-lookup"><span data-stu-id="07f1e-134">Add in any parameters that are required for the HTTP response message.</span></span>
   
    ![Выполнение действия ответа](./media/connectors-native-reqres/using-action-2.png)
5. <span data-ttu-id="07f1e-136">Щелкните верхний левый угол панели для сохранения. После этого приложение логики будет сохранено и опубликовано (активировано).</span><span class="sxs-lookup"><span data-stu-id="07f1e-136">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span></span>

## <a name="request-trigger"></a><span data-ttu-id="07f1e-137">Триггер запросов</span><span class="sxs-lookup"><span data-stu-id="07f1e-137">Request trigger</span></span>
<span data-ttu-id="07f1e-138">Ниже приведены подробные сведения о триггерах, поддерживаемых этим соединителем.</span><span class="sxs-lookup"><span data-stu-id="07f1e-138">Here are the details for the trigger that this connector supports.</span></span> <span data-ttu-id="07f1e-139">Здесь приведен триггер одного запроса.</span><span class="sxs-lookup"><span data-stu-id="07f1e-139">There is a single request trigger.</span></span>

| <span data-ttu-id="07f1e-140">Триггер</span><span class="sxs-lookup"><span data-stu-id="07f1e-140">Trigger</span></span> | <span data-ttu-id="07f1e-141">Описание</span><span class="sxs-lookup"><span data-stu-id="07f1e-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="07f1e-142">Запрос</span><span class="sxs-lookup"><span data-stu-id="07f1e-142">Request</span></span> |<span data-ttu-id="07f1e-143">Случается при получении HTTP-запроса</span><span class="sxs-lookup"><span data-stu-id="07f1e-143">Occurs when an HTTP request is received</span></span> |

## <a name="response-action"></a><span data-ttu-id="07f1e-144">Действие ответа</span><span class="sxs-lookup"><span data-stu-id="07f1e-144">Response action</span></span>
<span data-ttu-id="07f1e-145">Ниже приведены подробные сведения о действии, которое поддерживает этот соединитель.</span><span class="sxs-lookup"><span data-stu-id="07f1e-145">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="07f1e-146">Здесь приведено действие одного ответа, которое может использоваться только вместе с триггером запроса.</span><span class="sxs-lookup"><span data-stu-id="07f1e-146">There is a single response action that can only be used when it is accompanied by a request trigger.</span></span>

| <span data-ttu-id="07f1e-147">Действие</span><span class="sxs-lookup"><span data-stu-id="07f1e-147">Action</span></span> | <span data-ttu-id="07f1e-148">Описание</span><span class="sxs-lookup"><span data-stu-id="07f1e-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="07f1e-149">Ответ</span><span class="sxs-lookup"><span data-stu-id="07f1e-149">Response</span></span> |<span data-ttu-id="07f1e-150">Возвращает ответ на связанный HTTP запрос</span><span class="sxs-lookup"><span data-stu-id="07f1e-150">Returns a response to the correlated HTTP request</span></span> |

### <a name="trigger-and-action-details"></a><span data-ttu-id="07f1e-151">Сведения о триггерах и действиях</span><span class="sxs-lookup"><span data-stu-id="07f1e-151">Trigger and action details</span></span>
<span data-ttu-id="07f1e-152">В следующих таблицах описаны поля ввода для триггеров и действий и соответствующие сведения о выходных данных.</span><span class="sxs-lookup"><span data-stu-id="07f1e-152">The following tables describe the input fields for the trigger and action, and the corresponding output details.</span></span>

#### <a name="request-trigger"></a><span data-ttu-id="07f1e-153">Триггер запросов</span><span class="sxs-lookup"><span data-stu-id="07f1e-153">Request trigger</span></span>
<span data-ttu-id="07f1e-154">Ниже приведено поле ввода для триггера из входящего HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="07f1e-154">The following is an input field for the trigger from an incoming HTTP request.</span></span>

| <span data-ttu-id="07f1e-155">Отображаемое имя</span><span class="sxs-lookup"><span data-stu-id="07f1e-155">Display name</span></span> | <span data-ttu-id="07f1e-156">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="07f1e-156">Property name</span></span> | <span data-ttu-id="07f1e-157">Описание</span><span class="sxs-lookup"><span data-stu-id="07f1e-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="07f1e-158">Схема JSON</span><span class="sxs-lookup"><span data-stu-id="07f1e-158">JSON Schema</span></span> |<span data-ttu-id="07f1e-159">schema</span><span class="sxs-lookup"><span data-stu-id="07f1e-159">schema</span></span> |<span data-ttu-id="07f1e-160">Схема JSON текста HTTP-запроса</span><span class="sxs-lookup"><span data-stu-id="07f1e-160">The JSON schema of the HTTP request body</span></span> |

<br>

<span data-ttu-id="07f1e-161">**Сведения о выходных данных**</span><span class="sxs-lookup"><span data-stu-id="07f1e-161">**Output details**</span></span>

<span data-ttu-id="07f1e-162">Ниже приведены сведения о выходных данных для запроса.</span><span class="sxs-lookup"><span data-stu-id="07f1e-162">The following are output details for the request.</span></span>

| <span data-ttu-id="07f1e-163">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="07f1e-163">Property name</span></span> | <span data-ttu-id="07f1e-164">Тип данных</span><span class="sxs-lookup"><span data-stu-id="07f1e-164">Data type</span></span> | <span data-ttu-id="07f1e-165">Описание</span><span class="sxs-lookup"><span data-stu-id="07f1e-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="07f1e-166">Заголовки</span><span class="sxs-lookup"><span data-stu-id="07f1e-166">Headers</span></span> |<span data-ttu-id="07f1e-167">object</span><span class="sxs-lookup"><span data-stu-id="07f1e-167">object</span></span> |<span data-ttu-id="07f1e-168">Заголовки запросов</span><span class="sxs-lookup"><span data-stu-id="07f1e-168">Request headers</span></span> |
| <span data-ttu-id="07f1e-169">Текст</span><span class="sxs-lookup"><span data-stu-id="07f1e-169">Body</span></span> |<span data-ttu-id="07f1e-170">object</span><span class="sxs-lookup"><span data-stu-id="07f1e-170">object</span></span> |<span data-ttu-id="07f1e-171">Объект запроса</span><span class="sxs-lookup"><span data-stu-id="07f1e-171">Request object</span></span> |

#### <a name="response-action"></a><span data-ttu-id="07f1e-172">Действие ответа</span><span class="sxs-lookup"><span data-stu-id="07f1e-172">Response action</span></span>
<span data-ttu-id="07f1e-173">Ниже перечислены поля ввода для действия HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="07f1e-173">The following are input fields for the HTTP Response action.</span></span> <span data-ttu-id="07f1e-174">Звездочка (*) означает, что это поле обязательное для заполнения.</span><span class="sxs-lookup"><span data-stu-id="07f1e-174">A * means that it is a required field.</span></span>

| <span data-ttu-id="07f1e-175">Отображаемое имя</span><span class="sxs-lookup"><span data-stu-id="07f1e-175">Display name</span></span> | <span data-ttu-id="07f1e-176">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="07f1e-176">Property name</span></span> | <span data-ttu-id="07f1e-177">Описание</span><span class="sxs-lookup"><span data-stu-id="07f1e-177">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="07f1e-178">Код состояния*</span><span class="sxs-lookup"><span data-stu-id="07f1e-178">Status Code*</span></span> |<span data-ttu-id="07f1e-179">statusCode</span><span class="sxs-lookup"><span data-stu-id="07f1e-179">statusCode</span></span> |<span data-ttu-id="07f1e-180">Код состояния HTTP</span><span class="sxs-lookup"><span data-stu-id="07f1e-180">The HTTP status code</span></span> |
| <span data-ttu-id="07f1e-181">Заголовки</span><span class="sxs-lookup"><span data-stu-id="07f1e-181">Headers</span></span> |<span data-ttu-id="07f1e-182">headers</span><span class="sxs-lookup"><span data-stu-id="07f1e-182">headers</span></span> |<span data-ttu-id="07f1e-183">Объект JSON заголовков ответов, которые нужно включить</span><span class="sxs-lookup"><span data-stu-id="07f1e-183">A JSON object of any response headers to include</span></span> |
| <span data-ttu-id="07f1e-184">Текст</span><span class="sxs-lookup"><span data-stu-id="07f1e-184">Body</span></span> |<span data-ttu-id="07f1e-185">текст</span><span class="sxs-lookup"><span data-stu-id="07f1e-185">body</span></span> |<span data-ttu-id="07f1e-186">Текст ответа</span><span class="sxs-lookup"><span data-stu-id="07f1e-186">The response body</span></span> |

## <a name="next-steps"></a><span data-ttu-id="07f1e-187">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="07f1e-187">Next steps</span></span>
<span data-ttu-id="07f1e-188">Теперь опробуйте платформу и [создайте приложение логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="07f1e-188">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="07f1e-189">Чтобы узнать, какие еще соединители доступны в приложениях логики, ознакомьтесь со [списком интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="07f1e-189">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

