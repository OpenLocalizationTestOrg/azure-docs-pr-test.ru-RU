---
title: "aaaCommunicate с любой конечной точке по протоколу HTTP - приложения логики Azure | Документы Microsoft"
description: "Создание приложений логики, которые обмениваются данными с любой конечной точкой по протоколу HTTP."
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: 9793601839437a2b880bdb81e15881270cacc963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http-action"></a><span data-ttu-id="28de9-103">Приступая к работе с hello действия HTTP</span><span class="sxs-lookup"><span data-stu-id="28de9-103">Get started with hello HTTP action</span></span>

<span data-ttu-id="28de9-104">С hello действия HTTP можно расширить рабочие процессы для вашей организации и передачи конечной точки tooany по протоколу HTTP.</span><span class="sxs-lookup"><span data-stu-id="28de9-104">With hello HTTP action, you can extend workflows for your organization and communicate tooany endpoint over HTTP.</span></span>

<span data-ttu-id="28de9-105">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="28de9-105">You can:</span></span>

* <span data-ttu-id="28de9-106">Создайте рабочие процессы приложений логики, которые будут активироваться, когда управляемый вами веб-сайт выйдет из строя.</span><span class="sxs-lookup"><span data-stu-id="28de9-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="28de9-107">Связь tooany конечной точки через HTTP tooextend рабочие процессы в другие службы.</span><span class="sxs-lookup"><span data-stu-id="28de9-107">Communicate tooany endpoint over HTTP tooextend your workflows into other services.</span></span>

<span data-ttu-id="28de9-108">tooget к работе с помощью действия hello HTTP в приложении логику в разделе [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="28de9-108">tooget started using hello HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-trigger"></a><span data-ttu-id="28de9-109">Использование триггера hello HTTP</span><span class="sxs-lookup"><span data-stu-id="28de9-109">Use hello HTTP trigger</span></span>
<span data-ttu-id="28de9-110">Триггер — это событие, которое может быть hello используется toostart рабочий процесс, который определен в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="28de9-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="28de9-111">[Дополнительные сведения о триггерах](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="28de9-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="28de9-112">Вот пример последовательность как триггер tooset копирование hello HTTP в конструктор логику приложения hello.</span><span class="sxs-lookup"><span data-stu-id="28de9-112">Here’s an example sequence of how tooset up hello HTTP trigger in hello Logic App Designer.</span></span>

1. <span data-ttu-id="28de9-113">Добавьте триггер HTTP hello в логике приложения.</span><span class="sxs-lookup"><span data-stu-id="28de9-113">Add hello HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="28de9-114">Заполните параметры hello для hello HTTP конечной точки, которые должны toopoll.</span><span class="sxs-lookup"><span data-stu-id="28de9-114">Fill in hello parameters for hello HTTP endpoint that you want toopoll.</span></span>
3. <span data-ttu-id="28de9-115">Измените интервал повторения hello на том, как часто должна опрашивать.</span><span class="sxs-lookup"><span data-stu-id="28de9-115">Modify hello recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="28de9-116">приложения логики Hello теперь срабатывает содержимым, который возвращается при каждой проверке.</span><span class="sxs-lookup"><span data-stu-id="28de9-116">hello logic app now fires with any content that is returned during each check.</span></span>

   ![Триггер HTTP](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a><span data-ttu-id="28de9-118">Как работает триггер HTTP hello</span><span class="sxs-lookup"><span data-stu-id="28de9-118">How hello HTTP trigger works</span></span>

<span data-ttu-id="28de9-119">триггер Hello HTTP отправляет конечную точку tooHTTP вызов через заданный интервал.</span><span class="sxs-lookup"><span data-stu-id="28de9-119">hello HTTP trigger sends a call tooHTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="28de9-120">По умолчанию любой код HTTP-ответа, которое меньше 300 вызывает toorun логику приложения.</span><span class="sxs-lookup"><span data-stu-id="28de9-120">By default, any HTTP response code that is lower than 300 causes a logic app toorun.</span></span> <span data-ttu-id="28de9-121">toospecify ли приложение hello логики должен срабатывать, можно изменить логику приложение hello в окне просмотра кода и добавьте условие, которое принимает после hello вызовов HTTP.</span><span class="sxs-lookup"><span data-stu-id="28de9-121">toospecify whether hello logic app should fire, you can edit hello logic app in code view, and add a condition that evaluates after hello HTTP call.</span></span> <span data-ttu-id="28de9-122">Ниже приведен пример HTTP триггер, срабатывающий при hello вернул код состояния, больше или равно слишком`400`.</span><span class="sxs-lookup"><span data-stu-id="28de9-122">Here's an example of an HTTP trigger that fires when hello returned status code is greater than or equal too`400`.</span></span>

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

<span data-ttu-id="28de9-123">Полные сведения о параметрах триггер hello HTTP доступны на [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span><span class="sxs-lookup"><span data-stu-id="28de9-123">Full details about hello HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-hello-http-action"></a><span data-ttu-id="28de9-124">Используйте действие hello HTTP</span><span class="sxs-lookup"><span data-stu-id="28de9-124">Use hello HTTP action</span></span>

<span data-ttu-id="28de9-125">Действие — это операции, выполняемые hello рабочего процесса, определенные в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="28de9-125">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="28de9-126">[Дополнительные сведения о действиях](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="28de9-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="28de9-127">Выберите **Новый шаг** > **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="28de9-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="28de9-128">Введите в поле поиска действие hello **http** действия toolist hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="28de9-128">In hello action search box, type **http** toolist hello HTTP actions.</span></span>
   
    ![Выберите действие hello HTTP](./media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="28de9-130">Добавьте все необходимые параметры для вызова hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="28de9-130">Add any required parameters for hello HTTP call.</span></span>
   
    ![Полный hello действия HTTP](./media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="28de9-132">На панели инструментов конструктора hello, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="28de9-132">On hello designer toolbar, click **Save**.</span></span> <span data-ttu-id="28de9-133">Логику приложения будет сохранен и опубликован (активированной) на hello то же время.</span><span class="sxs-lookup"><span data-stu-id="28de9-133">Your logic app is saved and published (activated) at hello same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="28de9-134">Триггер HTTP</span><span class="sxs-lookup"><span data-stu-id="28de9-134">HTTP trigger</span></span>
<span data-ttu-id="28de9-135">Ниже приведены сведения hello для hello триггера, который поддерживает этот соединитель.</span><span class="sxs-lookup"><span data-stu-id="28de9-135">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="28de9-136">Соединитель Hello HTTP имеет один триггер.</span><span class="sxs-lookup"><span data-stu-id="28de9-136">hello HTTP connector has one trigger.</span></span>

| <span data-ttu-id="28de9-137">Триггер</span><span class="sxs-lookup"><span data-stu-id="28de9-137">Trigger</span></span> | <span data-ttu-id="28de9-138">Описание</span><span class="sxs-lookup"><span data-stu-id="28de9-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="28de9-139">HTTP</span><span class="sxs-lookup"><span data-stu-id="28de9-139">HTTP</span></span> |<span data-ttu-id="28de9-140">Отправляет вызов HTTP и возвращает содержимое ответа hello.</span><span class="sxs-lookup"><span data-stu-id="28de9-140">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="28de9-141">Действие HTTP</span><span class="sxs-lookup"><span data-stu-id="28de9-141">HTTP action</span></span>
<span data-ttu-id="28de9-142">Ниже приведены hello сведения для действия hello, поддерживающий этот соединитель.</span><span class="sxs-lookup"><span data-stu-id="28de9-142">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="28de9-143">Соединитель Hello HTTP имеет один возможным действием.</span><span class="sxs-lookup"><span data-stu-id="28de9-143">hello HTTP connector has one possible action.</span></span>

| <span data-ttu-id="28de9-144">Действие</span><span class="sxs-lookup"><span data-stu-id="28de9-144">Action</span></span> | <span data-ttu-id="28de9-145">Описание</span><span class="sxs-lookup"><span data-stu-id="28de9-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="28de9-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="28de9-146">HTTP</span></span> |<span data-ttu-id="28de9-147">Отправляет вызов HTTP и возвращает содержимое ответа hello.</span><span class="sxs-lookup"><span data-stu-id="28de9-147">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="28de9-148">Сведения о HTTP</span><span class="sxs-lookup"><span data-stu-id="28de9-148">HTTP details</span></span>
<span data-ttu-id="28de9-149">Hello следующих таблицах описаны необходимые hello и необязательные поля ввода для действия hello и hello соответствующие сведения о выходных данных, связанных с помощью hello действия.</span><span class="sxs-lookup"><span data-stu-id="28de9-149">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="28de9-150">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="28de9-150">HTTP request</span></span>
<span data-ttu-id="28de9-151">Здесь представлены Hello поля входных данных для действия hello, поэтому исходящих HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="28de9-151">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="28de9-152">Звездочка (*) означает, что это поле обязательное для заполнения.</span><span class="sxs-lookup"><span data-stu-id="28de9-152">A * means that it is a required field.</span></span>

| <span data-ttu-id="28de9-153">Отображаемое имя</span><span class="sxs-lookup"><span data-stu-id="28de9-153">Display name</span></span> | <span data-ttu-id="28de9-154">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="28de9-154">Property name</span></span> | <span data-ttu-id="28de9-155">Описание</span><span class="sxs-lookup"><span data-stu-id="28de9-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="28de9-156">Метод*</span><span class="sxs-lookup"><span data-stu-id="28de9-156">Method*</span></span> |<span data-ttu-id="28de9-157">метод</span><span class="sxs-lookup"><span data-stu-id="28de9-157">method</span></span> |<span data-ttu-id="28de9-158">Команда toouse Hello HTTP</span><span class="sxs-lookup"><span data-stu-id="28de9-158">hello HTTP verb toouse</span></span> |
| <span data-ttu-id="28de9-159">URI*</span><span class="sxs-lookup"><span data-stu-id="28de9-159">URI*</span></span> |<span data-ttu-id="28de9-160">uri</span><span class="sxs-lookup"><span data-stu-id="28de9-160">uri</span></span> |<span data-ttu-id="28de9-161">Hello URI для hello HTTP-запроса</span><span class="sxs-lookup"><span data-stu-id="28de9-161">hello URI for hello HTTP request</span></span> |
| <span data-ttu-id="28de9-162">Заголовки</span><span class="sxs-lookup"><span data-stu-id="28de9-162">Headers</span></span> |<span data-ttu-id="28de9-163">headers</span><span class="sxs-lookup"><span data-stu-id="28de9-163">headers</span></span> |<span data-ttu-id="28de9-164">Объект JSON tooinclude заголовки HTTP</span><span class="sxs-lookup"><span data-stu-id="28de9-164">A JSON object of HTTP headers tooinclude</span></span> |
| <span data-ttu-id="28de9-165">Текст</span><span class="sxs-lookup"><span data-stu-id="28de9-165">Body</span></span> |<span data-ttu-id="28de9-166">текст</span><span class="sxs-lookup"><span data-stu-id="28de9-166">body</span></span> |<span data-ttu-id="28de9-167">Hello HTTP-запроса</span><span class="sxs-lookup"><span data-stu-id="28de9-167">hello HTTP request body</span></span> |
| <span data-ttu-id="28de9-168">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="28de9-168">Authentication</span></span> |<span data-ttu-id="28de9-169">authentication</span><span class="sxs-lookup"><span data-stu-id="28de9-169">authentication</span></span> |<span data-ttu-id="28de9-170">Сведения в hello [проверки подлинности](#authentication) раздела</span><span class="sxs-lookup"><span data-stu-id="28de9-170">Details in hello [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="28de9-171">Сведения о выходных данных</span><span class="sxs-lookup"><span data-stu-id="28de9-171">Output details</span></span>
<span data-ttu-id="28de9-172">Hello ниже приведены сведения о выходных данных для hello HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="28de9-172">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="28de9-173">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="28de9-173">Property name</span></span> | <span data-ttu-id="28de9-174">Тип данных</span><span class="sxs-lookup"><span data-stu-id="28de9-174">Data type</span></span> | <span data-ttu-id="28de9-175">Описание</span><span class="sxs-lookup"><span data-stu-id="28de9-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="28de9-176">Заголовки</span><span class="sxs-lookup"><span data-stu-id="28de9-176">Headers</span></span> |<span data-ttu-id="28de9-177">object</span><span class="sxs-lookup"><span data-stu-id="28de9-177">object</span></span> |<span data-ttu-id="28de9-178">Заголовки ответов</span><span class="sxs-lookup"><span data-stu-id="28de9-178">Response headers</span></span> |
| <span data-ttu-id="28de9-179">Текст</span><span class="sxs-lookup"><span data-stu-id="28de9-179">Body</span></span> |<span data-ttu-id="28de9-180">object</span><span class="sxs-lookup"><span data-stu-id="28de9-180">object</span></span> |<span data-ttu-id="28de9-181">Объект ответа</span><span class="sxs-lookup"><span data-stu-id="28de9-181">Response object</span></span> |
| <span data-ttu-id="28de9-182">Код состояния</span><span class="sxs-lookup"><span data-stu-id="28de9-182">Status Code</span></span> |<span data-ttu-id="28de9-183">int</span><span class="sxs-lookup"><span data-stu-id="28de9-183">int</span></span> |<span data-ttu-id="28de9-184">HTTP status code (Код состояния HTTP)</span><span class="sxs-lookup"><span data-stu-id="28de9-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="28de9-185">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="28de9-185">Authentication</span></span>
<span data-ttu-id="28de9-186">функция логики приложения Hello позволяет toouse разные типы проверки подлинности на основе конечных точек HTTP.</span><span class="sxs-lookup"><span data-stu-id="28de9-186">hello Logic Apps feature allows you toouse different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="28de9-187">Способ проверки подлинности можно использовать с hello **HTTP**,  **[HTTP + Swagger](connectors-native-http-swagger.md)**, и  **[HTTP веб-перехватчика](connectors-native-webhook.md)**  соединители.</span><span class="sxs-lookup"><span data-stu-id="28de9-187">You can use this authentication with hello **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="28de9-188">Привет, следующие типы проверки подлинности можно настроить:</span><span class="sxs-lookup"><span data-stu-id="28de9-188">hello following types of authentication are configurable:</span></span>

* [<span data-ttu-id="28de9-189">Обычная аутентификация</span><span class="sxs-lookup"><span data-stu-id="28de9-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="28de9-190">Аутентификация на основе сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="28de9-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="28de9-191">Аутентификация Azure Active Directory (Azure AD) OAuth</span><span class="sxs-lookup"><span data-stu-id="28de9-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="28de9-192">Обычная аутентификация</span><span class="sxs-lookup"><span data-stu-id="28de9-192">Basic authentication</span></span>

<span data-ttu-id="28de9-193">для обычной проверки подлинности требуется Hello следующий объект проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="28de9-193">hello following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="28de9-194">Звездочка (*) означает, что это поле обязательное для заполнения.</span><span class="sxs-lookup"><span data-stu-id="28de9-194">A * means that it is a required field.</span></span>

| <span data-ttu-id="28de9-195">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="28de9-195">Property name</span></span> | <span data-ttu-id="28de9-196">Тип данных</span><span class="sxs-lookup"><span data-stu-id="28de9-196">Data type</span></span> | <span data-ttu-id="28de9-197">Описание</span><span class="sxs-lookup"><span data-stu-id="28de9-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="28de9-198">Тип*</span><span class="sxs-lookup"><span data-stu-id="28de9-198">Type*</span></span> |<span data-ttu-id="28de9-199">type</span><span class="sxs-lookup"><span data-stu-id="28de9-199">type</span></span> |<span data-ttu-id="28de9-200">Тип аутентификации (для обычной аутентификации значение должно быть `Basic`)</span><span class="sxs-lookup"><span data-stu-id="28de9-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="28de9-201">Имя пользователя*</span><span class="sxs-lookup"><span data-stu-id="28de9-201">Username*</span></span> |<span data-ttu-id="28de9-202">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="28de9-202">username</span></span> |<span data-ttu-id="28de9-203">Tooauthenticate имя пользователя</span><span class="sxs-lookup"><span data-stu-id="28de9-203">User name tooauthenticate</span></span> |
| <span data-ttu-id="28de9-204">Пароль*</span><span class="sxs-lookup"><span data-stu-id="28de9-204">Password*</span></span> |<span data-ttu-id="28de9-205">пароль</span><span class="sxs-lookup"><span data-stu-id="28de9-205">password</span></span> |<span data-ttu-id="28de9-206">Пароль tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="28de9-206">Password tooauthenticate</span></span> |

> [!TIP]
> <span data-ttu-id="28de9-207">Пароль, который не удается получить из определения hello toouse используйте `securestring` параметр и hello `@parameters()`  
>  [функции определения рабочего процесса](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="28de9-207">If you want toouse a password that cannot be retrieved from hello definition, use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="28de9-208">Например:</span><span class="sxs-lookup"><span data-stu-id="28de9-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="28de9-209">Аутентификация на основе сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="28de9-209">Client certificate authentication</span></span>

<span data-ttu-id="28de9-210">Hello следующий объект проверки подлинности требуется для проверки подлинности сертификата клиента.</span><span class="sxs-lookup"><span data-stu-id="28de9-210">hello following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="28de9-211">Звездочка (*) означает, что это поле обязательное для заполнения.</span><span class="sxs-lookup"><span data-stu-id="28de9-211">A * means that it is a required field.</span></span>

| <span data-ttu-id="28de9-212">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="28de9-212">Property name</span></span> | <span data-ttu-id="28de9-213">Тип данных</span><span class="sxs-lookup"><span data-stu-id="28de9-213">Data type</span></span> | <span data-ttu-id="28de9-214">Описание</span><span class="sxs-lookup"><span data-stu-id="28de9-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="28de9-215">Тип*</span><span class="sxs-lookup"><span data-stu-id="28de9-215">Type*</span></span> |<span data-ttu-id="28de9-216">type</span><span class="sxs-lookup"><span data-stu-id="28de9-216">type</span></span> |<span data-ttu-id="28de9-217">Здравствуйте, тип проверки подлинности (должно быть `ClientCertificate` для SSL-сертификатов клиента)</span><span class="sxs-lookup"><span data-stu-id="28de9-217">hello type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="28de9-218">PFX*</span><span class="sxs-lookup"><span data-stu-id="28de9-218">PFX*</span></span> |<span data-ttu-id="28de9-219">pfx</span><span class="sxs-lookup"><span data-stu-id="28de9-219">pfx</span></span> |<span data-ttu-id="28de9-220">Hello кодировке Base64 содержимое файла обмена личной информацией (PFX) hello</span><span class="sxs-lookup"><span data-stu-id="28de9-220">hello Base64-encoded contents of hello Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="28de9-221">Пароль*</span><span class="sxs-lookup"><span data-stu-id="28de9-221">Password*</span></span> |<span data-ttu-id="28de9-222">пароль</span><span class="sxs-lookup"><span data-stu-id="28de9-222">password</span></span> |<span data-ttu-id="28de9-223">Здравствуйте, tooaccess Hello пароль PFX-файла</span><span class="sxs-lookup"><span data-stu-id="28de9-223">hello password tooaccess hello PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="28de9-224">toouse параметр, который невозможен в определении hello после сохранения приложения hello логики, можно использовать `securestring` параметр и hello `@parameters()`  
>  [функции определения рабочего процесса](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="28de9-224">toouse a parameter that won't be readable in hello definition after saving hello logic app, you can use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="28de9-225">Например:</span><span class="sxs-lookup"><span data-stu-id="28de9-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="28de9-226">Аутентификация Azure AD OAuth</span><span class="sxs-lookup"><span data-stu-id="28de9-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="28de9-227">После проверки подлинности объекта Hello необходим для проверки подлинности Azure AD OAuth.</span><span class="sxs-lookup"><span data-stu-id="28de9-227">hello following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="28de9-228">Звездочка (*) означает, что это поле обязательное для заполнения.</span><span class="sxs-lookup"><span data-stu-id="28de9-228">A * means that it is a required field.</span></span>

| <span data-ttu-id="28de9-229">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="28de9-229">Property name</span></span> | <span data-ttu-id="28de9-230">Тип данных</span><span class="sxs-lookup"><span data-stu-id="28de9-230">Data type</span></span> | <span data-ttu-id="28de9-231">Описание</span><span class="sxs-lookup"><span data-stu-id="28de9-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="28de9-232">Тип*</span><span class="sxs-lookup"><span data-stu-id="28de9-232">Type*</span></span> |<span data-ttu-id="28de9-233">type</span><span class="sxs-lookup"><span data-stu-id="28de9-233">type</span></span> |<span data-ttu-id="28de9-234">Здравствуйте, тип проверки подлинности (должно быть `ActiveDirectoryOAuth` для Azure AD OAuth)</span><span class="sxs-lookup"><span data-stu-id="28de9-234">hello type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="28de9-235">Клиент*</span><span class="sxs-lookup"><span data-stu-id="28de9-235">Tenant*</span></span> |<span data-ttu-id="28de9-236">tenant</span><span class="sxs-lookup"><span data-stu-id="28de9-236">tenant</span></span> |<span data-ttu-id="28de9-237">Здравствуйте, идентификатор клиента для клиента hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="28de9-237">hello tenant identifier for hello Azure AD tenant</span></span> |
| <span data-ttu-id="28de9-238">Аудитория*</span><span class="sxs-lookup"><span data-stu-id="28de9-238">Audience*</span></span> |<span data-ttu-id="28de9-239">audience</span><span class="sxs-lookup"><span data-stu-id="28de9-239">audience</span></span> |<span data-ttu-id="28de9-240">Hello ресурс запрашивается toouse авторизации.</span><span class="sxs-lookup"><span data-stu-id="28de9-240">hello resource you are requesting authorization toouse.</span></span> <span data-ttu-id="28de9-241">Например: `https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="28de9-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="28de9-242">Идентификатор клиента*</span><span class="sxs-lookup"><span data-stu-id="28de9-242">Client ID*</span></span> |<span data-ttu-id="28de9-243">clientid</span><span class="sxs-lookup"><span data-stu-id="28de9-243">clientId</span></span> |<span data-ttu-id="28de9-244">Здравствуйте, идентификатор клиента приложения hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="28de9-244">hello client identifier for hello Azure AD application</span></span> |
| <span data-ttu-id="28de9-245">Секрет*</span><span class="sxs-lookup"><span data-stu-id="28de9-245">Secret*</span></span> |<span data-ttu-id="28de9-246">secret</span><span class="sxs-lookup"><span data-stu-id="28de9-246">secret</span></span> |<span data-ttu-id="28de9-247">секрет Hello hello клиента, который запрашивает токен hello</span><span class="sxs-lookup"><span data-stu-id="28de9-247">hello secret of hello client that is requesting hello token</span></span> |

> [!TIP]
> <span data-ttu-id="28de9-248">Можно использовать `securestring` параметр и hello `@parameters()` [функции определения рабочего процесса](http://aka.ms/logicappdocs) toouse параметр, который не будет доступной для чтения в определении hello после сохранения.</span><span class="sxs-lookup"><span data-stu-id="28de9-248">You can use a `securestring` parameter and hello `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) toouse a parameter that won't be readable in hello definition after saving.</span></span>
> 
> 

<span data-ttu-id="28de9-249">Например:</span><span class="sxs-lookup"><span data-stu-id="28de9-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="28de9-250">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="28de9-250">Next steps</span></span>
<span data-ttu-id="28de9-251">Теперь попробуйте платформы hello и [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="28de9-251">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="28de9-252">Вы можете просматривать hello другие доступные соединители в приложениях для логики, просмотрев нашей [список API-интерфейсы](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="28de9-252">You can explore hello other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>

