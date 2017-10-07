---
title: "действия запроса и ответа aaaUse | Документы Microsoft"
description: "Общие сведения о hello запроса и ответа триггера и действия в приложении Azure логики"
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
ms.openlocfilehash: 24c378cc12d5f3f65116d5e59278236186a99662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-request-and-response-components"></a><span data-ttu-id="74363-103">Начало работы с компонентами hello запросов и ответов</span><span class="sxs-lookup"><span data-stu-id="74363-103">Get started with hello request and response components</span></span>
<span data-ttu-id="74363-104">С hello запроса и ответа компонентов в приложение логики может отвечать в режиме реального времени tooevents.</span><span class="sxs-lookup"><span data-stu-id="74363-104">With hello request and response components in a logic app, you can respond in real time tooevents.</span></span>

<span data-ttu-id="74363-105">Вот что вы можете, к примеру, делать:</span><span class="sxs-lookup"><span data-stu-id="74363-105">For example, you can:</span></span>

* <span data-ttu-id="74363-106">Ответ tooan HTTP-запроса с данными из локальной базы данных через приложения логики.</span><span class="sxs-lookup"><span data-stu-id="74363-106">Respond tooan HTTP request with data from an on-premises database through a logic app.</span></span>
* <span data-ttu-id="74363-107">запуск приложения логики из внешнего события webhook;</span><span class="sxs-lookup"><span data-stu-id="74363-107">Trigger a logic app from an external webhook event.</span></span>
* <span data-ttu-id="74363-108">вызов приложения логики с помощью действия запроса и ответа из другого приложения логики.</span><span class="sxs-lookup"><span data-stu-id="74363-108">Call a logic app with a request and response action from within another logic app.</span></span>

<span data-ttu-id="74363-109">tooget к работе с использованием hello запросов и ответов в приложение логики, в разделе [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="74363-109">tooget started using hello request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-request-trigger"></a><span data-ttu-id="74363-110">Использовать hello триггер HTTP-запроса</span><span class="sxs-lookup"><span data-stu-id="74363-110">Use hello HTTP Request trigger</span></span>
<span data-ttu-id="74363-111">Триггер — это событие, которое может быть hello используется toostart рабочий процесс, который определен в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="74363-111">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="74363-112">[Дополнительные сведения о триггерах](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="74363-112">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="74363-113">Ниже приведен пример как tooset копирование HTTP запроса в конструктор логику приложения hello.</span><span class="sxs-lookup"><span data-stu-id="74363-113">Here’s an example sequence of how tooset up an HTTP request in hello Logic App Designer.</span></span>

1. <span data-ttu-id="74363-114">Добавить триггер hello **запрос — при HTTP-запрос получен** в логике приложения.</span><span class="sxs-lookup"><span data-stu-id="74363-114">Add hello trigger **Request - When an HTTP request is received** in your logic app.</span></span> <span data-ttu-id="74363-115">При необходимости можно указать схему JSON (с помощью таких средств, как [JSONSchema.net](http://jsonschema.net)) для hello текст запроса.</span><span class="sxs-lookup"><span data-stu-id="74363-115">You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for hello request body.</span></span> <span data-ttu-id="74363-116">Это позволяет маркерах свойства конструктора toogenerate hello hello HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="74363-116">This allows hello designer toogenerate tokens for properties in hello HTTP request.</span></span>
2. <span data-ttu-id="74363-117">Добавьте еще одно действие, чтобы можно было сохранить логику приложения hello.</span><span class="sxs-lookup"><span data-stu-id="74363-117">Add another action so that you can save hello logic app.</span></span>
3. <span data-ttu-id="74363-118">После сохранения приложения hello логики, можно получить URL-адрес запроса hello HTTP из карты hello запроса.</span><span class="sxs-lookup"><span data-stu-id="74363-118">After saving hello logic app, you can get hello HTTP request URL from hello request card.</span></span>
4. <span data-ttu-id="74363-119">HTTP POST (можно использовать средства, подобного [почтальон](https://www.getpostman.com/)) триггеры URL-адрес toohello hello приложения логики.</span><span class="sxs-lookup"><span data-stu-id="74363-119">An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) toohello URL triggers hello logic app.</span></span>

> [!NOTE]
> <span data-ttu-id="74363-120">Если разработчик не определил ответное действие `202 ACCEPTED` toohello вызывающий объект немедленно возвращается ответ.</span><span class="sxs-lookup"><span data-stu-id="74363-120">If you don't define a response action, a `202 ACCEPTED` response is immediately returned toohello caller.</span></span> <span data-ttu-id="74363-121">Можно использовать toocustomize действие ответа hello ответа.</span><span class="sxs-lookup"><span data-stu-id="74363-121">You can use hello response action toocustomize a response.</span></span>
> 
> 

![Триггер ответа](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-hello-http-response-action"></a><span data-ttu-id="74363-123">Использовать hello действия HTTP-ответа</span><span class="sxs-lookup"><span data-stu-id="74363-123">Use hello HTTP Response action</span></span>
<span data-ttu-id="74363-124">Hello действие ответа HTTP допустимо только при использовании в рабочем процессе, запускаемая по HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="74363-124">hello HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request.</span></span> <span data-ttu-id="74363-125">Если разработчик не определил ответное действие `202 ACCEPTED` toohello вызывающий объект немедленно возвращается ответ.</span><span class="sxs-lookup"><span data-stu-id="74363-125">If you don't define a response action, a `202 ACCEPTED` response is immediately returned toohello caller.</span></span>  <span data-ttu-id="74363-126">Можно добавить действие ответа в какой-либо шаг в рабочем процессе hello.</span><span class="sxs-lookup"><span data-stu-id="74363-126">You can add a response action at any step within hello workflow.</span></span> <span data-ttu-id="74363-127">только приложение Hello логику поддерживает hello входящий запрос открытым в течение одной минуты для ответа.</span><span class="sxs-lookup"><span data-stu-id="74363-127">hello logic app only keeps hello incoming request open for one minute for a response.</span></span>  <span data-ttu-id="74363-128">Через одну минуту, если ответ не был отправлен hello рабочего процесса (существует ответное действие в определении hello) `504 GATEWAY TIMEOUT` возвращается toohello вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="74363-128">After one minute, if no response was sent from hello workflow (and a response action exists in hello definition), a `504 GATEWAY TIMEOUT` is returned toohello caller.</span></span>

<span data-ttu-id="74363-129">Вот как tooadd действие HTTP-ответа:</span><span class="sxs-lookup"><span data-stu-id="74363-129">Here's how tooadd an HTTP Response action:</span></span>

1. <span data-ttu-id="74363-130">Выберите hello **новый шаг** кнопки.</span><span class="sxs-lookup"><span data-stu-id="74363-130">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="74363-131">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="74363-131">Choose **Add an action**.</span></span>
3. <span data-ttu-id="74363-132">Введите в поле поиска действие hello **ответ** toolist hello ответное действие.</span><span class="sxs-lookup"><span data-stu-id="74363-132">In hello action search box, type **response** toolist hello Response action.</span></span>
   
    ![Выберите ответное действие hello](./media/connectors-native-reqres/using-action-1.png)
4. <span data-ttu-id="74363-134">Добавьте параметры, необходимые для сообщения hello HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="74363-134">Add in any parameters that are required for hello HTTP response message.</span></span>
   
    ![Ответное действие завершения hello](./media/connectors-native-reqres/using-action-2.png)
5. <span data-ttu-id="74363-136">Щелкните hello верхнего левого угла toosave инструментов hello и вашей логики приложения будет как сохранять и публикации (активировать).</span><span class="sxs-lookup"><span data-stu-id="74363-136">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="request-trigger"></a><span data-ttu-id="74363-137">Триггер запросов</span><span class="sxs-lookup"><span data-stu-id="74363-137">Request trigger</span></span>
<span data-ttu-id="74363-138">Ниже приведены сведения hello для hello триггера, который поддерживает этот соединитель.</span><span class="sxs-lookup"><span data-stu-id="74363-138">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="74363-139">Здесь приведен триггер одного запроса.</span><span class="sxs-lookup"><span data-stu-id="74363-139">There is a single request trigger.</span></span>

| <span data-ttu-id="74363-140">Триггер</span><span class="sxs-lookup"><span data-stu-id="74363-140">Trigger</span></span> | <span data-ttu-id="74363-141">Описание</span><span class="sxs-lookup"><span data-stu-id="74363-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="74363-142">Запрос</span><span class="sxs-lookup"><span data-stu-id="74363-142">Request</span></span> |<span data-ttu-id="74363-143">Случается при получении HTTP-запроса</span><span class="sxs-lookup"><span data-stu-id="74363-143">Occurs when an HTTP request is received</span></span> |

## <a name="response-action"></a><span data-ttu-id="74363-144">Действие ответа</span><span class="sxs-lookup"><span data-stu-id="74363-144">Response action</span></span>
<span data-ttu-id="74363-145">Ниже приведены hello сведения для действия hello, поддерживающий этот соединитель.</span><span class="sxs-lookup"><span data-stu-id="74363-145">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="74363-146">Здесь приведено действие одного ответа, которое может использоваться только вместе с триггером запроса.</span><span class="sxs-lookup"><span data-stu-id="74363-146">There is a single response action that can only be used when it is accompanied by a request trigger.</span></span>

| <span data-ttu-id="74363-147">Действие</span><span class="sxs-lookup"><span data-stu-id="74363-147">Action</span></span> | <span data-ttu-id="74363-148">Описание</span><span class="sxs-lookup"><span data-stu-id="74363-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="74363-149">Ответ</span><span class="sxs-lookup"><span data-stu-id="74363-149">Response</span></span> |<span data-ttu-id="74363-150">Возвращает связь toohello ответа HTTP-запроса</span><span class="sxs-lookup"><span data-stu-id="74363-150">Returns a response toohello correlated HTTP request</span></span> |

### <a name="trigger-and-action-details"></a><span data-ttu-id="74363-151">Сведения о триггерах и действиях</span><span class="sxs-lookup"><span data-stu-id="74363-151">Trigger and action details</span></span>
<span data-ttu-id="74363-152">Hello следующие таблицы описывают поля ввода hello для hello триггера и действия и hello соответствующие сведения о выходных данных.</span><span class="sxs-lookup"><span data-stu-id="74363-152">hello following tables describe hello input fields for hello trigger and action, and hello corresponding output details.</span></span>

#### <a name="request-trigger"></a><span data-ttu-id="74363-153">Триггер запросов</span><span class="sxs-lookup"><span data-stu-id="74363-153">Request trigger</span></span>
<span data-ttu-id="74363-154">Hello Приведем поле ввода для hello триггера из входящего HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="74363-154">hello following is an input field for hello trigger from an incoming HTTP request.</span></span>

| <span data-ttu-id="74363-155">Отображаемое имя</span><span class="sxs-lookup"><span data-stu-id="74363-155">Display name</span></span> | <span data-ttu-id="74363-156">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="74363-156">Property name</span></span> | <span data-ttu-id="74363-157">Описание</span><span class="sxs-lookup"><span data-stu-id="74363-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="74363-158">Схема JSON</span><span class="sxs-lookup"><span data-stu-id="74363-158">JSON Schema</span></span> |<span data-ttu-id="74363-159">schema</span><span class="sxs-lookup"><span data-stu-id="74363-159">schema</span></span> |<span data-ttu-id="74363-160">Схема JSON Hello текста hello HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="74363-160">hello JSON schema of hello HTTP request body</span></span> |

<br>

<span data-ttu-id="74363-161">**Сведения о выходных данных**</span><span class="sxs-lookup"><span data-stu-id="74363-161">**Output details**</span></span>

<span data-ttu-id="74363-162">Hello ниже приведены сведения о выходных данных для запроса hello.</span><span class="sxs-lookup"><span data-stu-id="74363-162">hello following are output details for hello request.</span></span>

| <span data-ttu-id="74363-163">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="74363-163">Property name</span></span> | <span data-ttu-id="74363-164">Тип данных</span><span class="sxs-lookup"><span data-stu-id="74363-164">Data type</span></span> | <span data-ttu-id="74363-165">Описание</span><span class="sxs-lookup"><span data-stu-id="74363-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="74363-166">Заголовки</span><span class="sxs-lookup"><span data-stu-id="74363-166">Headers</span></span> |<span data-ttu-id="74363-167">object</span><span class="sxs-lookup"><span data-stu-id="74363-167">object</span></span> |<span data-ttu-id="74363-168">Заголовки запросов</span><span class="sxs-lookup"><span data-stu-id="74363-168">Request headers</span></span> |
| <span data-ttu-id="74363-169">Текст</span><span class="sxs-lookup"><span data-stu-id="74363-169">Body</span></span> |<span data-ttu-id="74363-170">object</span><span class="sxs-lookup"><span data-stu-id="74363-170">object</span></span> |<span data-ttu-id="74363-171">Объект запроса</span><span class="sxs-lookup"><span data-stu-id="74363-171">Request object</span></span> |

#### <a name="response-action"></a><span data-ttu-id="74363-172">Действие ответа</span><span class="sxs-lookup"><span data-stu-id="74363-172">Response action</span></span>
<span data-ttu-id="74363-173">Здесь представлены Hello полей ввода для hello действия HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="74363-173">hello following are input fields for hello HTTP Response action.</span></span> <span data-ttu-id="74363-174">Звездочка (*) означает, что это поле обязательное для заполнения.</span><span class="sxs-lookup"><span data-stu-id="74363-174">A * means that it is a required field.</span></span>

| <span data-ttu-id="74363-175">Отображаемое имя</span><span class="sxs-lookup"><span data-stu-id="74363-175">Display name</span></span> | <span data-ttu-id="74363-176">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="74363-176">Property name</span></span> | <span data-ttu-id="74363-177">Описание</span><span class="sxs-lookup"><span data-stu-id="74363-177">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="74363-178">Код состояния*</span><span class="sxs-lookup"><span data-stu-id="74363-178">Status Code*</span></span> |<span data-ttu-id="74363-179">statusCode</span><span class="sxs-lookup"><span data-stu-id="74363-179">statusCode</span></span> |<span data-ttu-id="74363-180">Код состояния HTTP Hello</span><span class="sxs-lookup"><span data-stu-id="74363-180">hello HTTP status code</span></span> |
| <span data-ttu-id="74363-181">Заголовки</span><span class="sxs-lookup"><span data-stu-id="74363-181">Headers</span></span> |<span data-ttu-id="74363-182">headers</span><span class="sxs-lookup"><span data-stu-id="74363-182">headers</span></span> |<span data-ttu-id="74363-183">Объект JSON любой tooinclude заголовки ответа</span><span class="sxs-lookup"><span data-stu-id="74363-183">A JSON object of any response headers tooinclude</span></span> |
| <span data-ttu-id="74363-184">Текст</span><span class="sxs-lookup"><span data-stu-id="74363-184">Body</span></span> |<span data-ttu-id="74363-185">текст</span><span class="sxs-lookup"><span data-stu-id="74363-185">body</span></span> |<span data-ttu-id="74363-186">текст ответа Hello</span><span class="sxs-lookup"><span data-stu-id="74363-186">hello response body</span></span> |

## <a name="next-steps"></a><span data-ttu-id="74363-187">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="74363-187">Next steps</span></span>
<span data-ttu-id="74363-188">Теперь попробуйте платформы hello и [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="74363-188">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="74363-189">Вы можете просматривать hello других доступных соединителей в приложении логики, просмотрев нашей [список API-интерфейсы](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="74363-189">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

