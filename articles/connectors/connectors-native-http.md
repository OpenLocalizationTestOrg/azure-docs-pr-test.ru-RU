---
title: "Обмен данными с любой конечной точкой по протоколу HTTP в Azure Logic Apps | Документация Майкрософт"
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
ms.openlocfilehash: d422a07a27ffa62a673bd2d471ae4fc837251dee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-http-action"></a><span data-ttu-id="6c17c-103">Начало работы с действием HTTP</span><span class="sxs-lookup"><span data-stu-id="6c17c-103">Get started with the HTTP action</span></span>

<span data-ttu-id="6c17c-104">Благодаря действию HTTP можно расширить рабочие процессы своей организации и взаимодействовать с конечной точкой по протоколу HTTP.</span><span class="sxs-lookup"><span data-stu-id="6c17c-104">With the HTTP action, you can extend workflows for your organization and communicate to any endpoint over HTTP.</span></span>

<span data-ttu-id="6c17c-105">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="6c17c-105">You can:</span></span>

* <span data-ttu-id="6c17c-106">Создайте рабочие процессы приложений логики, которые будут активироваться, когда управляемый вами веб-сайт выйдет из строя.</span><span class="sxs-lookup"><span data-stu-id="6c17c-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="6c17c-107">Настройте взаимодействие с конечной точкой по протоколу HTTP, чтобы распространить рабочие процессы на другие службы.</span><span class="sxs-lookup"><span data-stu-id="6c17c-107">Communicate to any endpoint over HTTP to extend your workflows into other services.</span></span>

<span data-ttu-id="6c17c-108">Сведения о начале работы с действием HTTP в приложении логики см. в статье [Создание нового приложения логики, подключающего службы SaaS](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="6c17c-108">To get started using the HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-http-trigger"></a><span data-ttu-id="6c17c-109">Использование триггера HTTP</span><span class="sxs-lookup"><span data-stu-id="6c17c-109">Use the HTTP trigger</span></span>
<span data-ttu-id="6c17c-110">Триггер — это событие, которое можно использовать для запуска рабочего процесса, определенного в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="6c17c-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="6c17c-111">[Дополнительные сведения о триггерах](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6c17c-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="6c17c-112">Ниже приведен пример последовательности настройки триггера HTTP в конструкторе приложений логики.</span><span class="sxs-lookup"><span data-stu-id="6c17c-112">Here’s an example sequence of how to set up the HTTP trigger in the Logic App Designer.</span></span>

1. <span data-ttu-id="6c17c-113">Добавьте триггер HTTP в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="6c17c-113">Add the HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="6c17c-114">Заполните параметры конечной точки HTTP, которую нужно опросить.</span><span class="sxs-lookup"><span data-stu-id="6c17c-114">Fill in the parameters for the HTTP endpoint that you want to poll.</span></span>
3. <span data-ttu-id="6c17c-115">Измените интервал повторения на частоту опроса.</span><span class="sxs-lookup"><span data-stu-id="6c17c-115">Modify the recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="6c17c-116">Теперь приложение логики запускается с любым содержимым, возвращаемым при проверке.</span><span class="sxs-lookup"><span data-stu-id="6c17c-116">The logic app now fires with any content that is returned during each check.</span></span>

   ![Триггер HTTP](./media/connectors-native-http/using-trigger.png)

### <a name="how-the-http-trigger-works"></a><span data-ttu-id="6c17c-118">Принцип работы триггера HTTP</span><span class="sxs-lookup"><span data-stu-id="6c17c-118">How the HTTP trigger works</span></span>

<span data-ttu-id="6c17c-119">Триггер HTTP отправляет вызов к конечной точке HTTP в соответствии с интервалом повторения.</span><span class="sxs-lookup"><span data-stu-id="6c17c-119">The HTTP trigger sends a call to HTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="6c17c-120">По умолчанию любой код HTTP-ответа меньше 300 вызывает запуск приложения логики.</span><span class="sxs-lookup"><span data-stu-id="6c17c-120">By default, any HTTP response code that is lower than 300 causes a logic app to run.</span></span> <span data-ttu-id="6c17c-121">Чтобы указать, следует ли запускать приложение логики, можно изменить его в представлении кода и добавить условие, оцениваемое после HTTP-вызова.</span><span class="sxs-lookup"><span data-stu-id="6c17c-121">To specify whether the logic app should fire, you can edit the logic app in code view, and add a condition that evaluates after the HTTP call.</span></span> <span data-ttu-id="6c17c-122">Ниже приведен пример триггера HTTP, который срабатывает, когда возвращаемый код состояния больше или равен `400`.</span><span class="sxs-lookup"><span data-stu-id="6c17c-122">Here's an example of an HTTP trigger that fires when the returned status code is greater than or equal to `400`.</span></span>

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

<span data-ttu-id="6c17c-123">Подробные сведения о параметрах триггера HTTP можно найти в библиотеке [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span><span class="sxs-lookup"><span data-stu-id="6c17c-123">Full details about the HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-the-http-action"></a><span data-ttu-id="6c17c-124">Использование действия HTTP</span><span class="sxs-lookup"><span data-stu-id="6c17c-124">Use the HTTP action</span></span>

<span data-ttu-id="6c17c-125">Действие — это операция, выполняемая рабочим процессом, определенным в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="6c17c-125">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="6c17c-126">[Дополнительные сведения о действиях](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6c17c-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="6c17c-127">Выберите **Новый шаг** > **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="6c17c-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="6c17c-128">В поле поиска действий введите **http**, чтобы отобразить список действий HTTP.</span><span class="sxs-lookup"><span data-stu-id="6c17c-128">In the action search box, type **http** to list the HTTP actions.</span></span>
   
    ![Выбор действия HTTP](./media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="6c17c-130">Добавьте все необходимые параметры для HTTP-вызова.</span><span class="sxs-lookup"><span data-stu-id="6c17c-130">Add any required parameters for the HTTP call.</span></span>
   
    ![Выполнение действия HTTP](./media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="6c17c-132">На панели инструментов конструктора нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="6c17c-132">On the designer toolbar, click **Save**.</span></span> <span data-ttu-id="6c17c-133">Приложение логики будет сохранено и опубликовано (активировано).</span><span class="sxs-lookup"><span data-stu-id="6c17c-133">Your logic app is saved and published (activated) at the same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="6c17c-134">Триггер HTTP</span><span class="sxs-lookup"><span data-stu-id="6c17c-134">HTTP trigger</span></span>
<span data-ttu-id="6c17c-135">Ниже приведены подробные сведения о триггере, поддерживаемом этим соединителем.</span><span class="sxs-lookup"><span data-stu-id="6c17c-135">Here are the details for the trigger that this connector supports.</span></span> <span data-ttu-id="6c17c-136">У соединителя HTTP один триггер.</span><span class="sxs-lookup"><span data-stu-id="6c17c-136">The HTTP connector has one trigger.</span></span>

| <span data-ttu-id="6c17c-137">Триггер</span><span class="sxs-lookup"><span data-stu-id="6c17c-137">Trigger</span></span> | <span data-ttu-id="6c17c-138">Описание</span><span class="sxs-lookup"><span data-stu-id="6c17c-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6c17c-139">HTTP</span><span class="sxs-lookup"><span data-stu-id="6c17c-139">HTTP</span></span> |<span data-ttu-id="6c17c-140">Совершает вызов HTTP и возвращает содержимое ответа.</span><span class="sxs-lookup"><span data-stu-id="6c17c-140">Makes an HTTP call and returns the response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="6c17c-141">Действие HTTP</span><span class="sxs-lookup"><span data-stu-id="6c17c-141">HTTP action</span></span>
<span data-ttu-id="6c17c-142">Ниже приведены подробные сведения о действии, которое поддерживает этот соединитель.</span><span class="sxs-lookup"><span data-stu-id="6c17c-142">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="6c17c-143">У соединителя HTTP одно возможное действие.</span><span class="sxs-lookup"><span data-stu-id="6c17c-143">The HTTP connector has one possible action.</span></span>

| <span data-ttu-id="6c17c-144">Действие</span><span class="sxs-lookup"><span data-stu-id="6c17c-144">Action</span></span> | <span data-ttu-id="6c17c-145">Описание</span><span class="sxs-lookup"><span data-stu-id="6c17c-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6c17c-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="6c17c-146">HTTP</span></span> |<span data-ttu-id="6c17c-147">Совершает вызов HTTP и возвращает содержимое ответа.</span><span class="sxs-lookup"><span data-stu-id="6c17c-147">Makes an HTTP call and returns the response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="6c17c-148">Сведения о HTTP</span><span class="sxs-lookup"><span data-stu-id="6c17c-148">HTTP details</span></span>
<span data-ttu-id="6c17c-149">В следующих таблицах приведены обязательные и необязательные поля ввода для действия, а также соответствующие выходные данные, связанные с его использованием.</span><span class="sxs-lookup"><span data-stu-id="6c17c-149">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="6c17c-150">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="6c17c-150">HTTP request</span></span>
<span data-ttu-id="6c17c-151">Ниже перечислены поля ввода для действия, выполняющего исходящий HTTP-запрос.</span><span class="sxs-lookup"><span data-stu-id="6c17c-151">The following are input fields for the action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="6c17c-152">Звездочка (*) означает, что это поле обязательное для заполнения.</span><span class="sxs-lookup"><span data-stu-id="6c17c-152">A * means that it is a required field.</span></span>

| <span data-ttu-id="6c17c-153">Отображаемое имя</span><span class="sxs-lookup"><span data-stu-id="6c17c-153">Display name</span></span> | <span data-ttu-id="6c17c-154">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="6c17c-154">Property name</span></span> | <span data-ttu-id="6c17c-155">Описание</span><span class="sxs-lookup"><span data-stu-id="6c17c-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c17c-156">Метод*</span><span class="sxs-lookup"><span data-stu-id="6c17c-156">Method*</span></span> |<span data-ttu-id="6c17c-157">метод</span><span class="sxs-lookup"><span data-stu-id="6c17c-157">method</span></span> |<span data-ttu-id="6c17c-158">HTTP-команда для использования</span><span class="sxs-lookup"><span data-stu-id="6c17c-158">The HTTP verb to use</span></span> |
| <span data-ttu-id="6c17c-159">URI*</span><span class="sxs-lookup"><span data-stu-id="6c17c-159">URI*</span></span> |<span data-ttu-id="6c17c-160">uri</span><span class="sxs-lookup"><span data-stu-id="6c17c-160">uri</span></span> |<span data-ttu-id="6c17c-161">URI HTTP-запроса</span><span class="sxs-lookup"><span data-stu-id="6c17c-161">The URI for the HTTP request</span></span> |
| <span data-ttu-id="6c17c-162">Заголовки</span><span class="sxs-lookup"><span data-stu-id="6c17c-162">Headers</span></span> |<span data-ttu-id="6c17c-163">headers</span><span class="sxs-lookup"><span data-stu-id="6c17c-163">headers</span></span> |<span data-ttu-id="6c17c-164">Объект JSON заголовков HTTP, который нужно включить</span><span class="sxs-lookup"><span data-stu-id="6c17c-164">A JSON object of HTTP headers to include</span></span> |
| <span data-ttu-id="6c17c-165">Текст</span><span class="sxs-lookup"><span data-stu-id="6c17c-165">Body</span></span> |<span data-ttu-id="6c17c-166">текст</span><span class="sxs-lookup"><span data-stu-id="6c17c-166">body</span></span> |<span data-ttu-id="6c17c-167">Текст HTTP-запроса</span><span class="sxs-lookup"><span data-stu-id="6c17c-167">The HTTP request body</span></span> |
| <span data-ttu-id="6c17c-168">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="6c17c-168">Authentication</span></span> |<span data-ttu-id="6c17c-169">метод проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="6c17c-169">authentication</span></span> |<span data-ttu-id="6c17c-170">Дополнительные сведения см. в разделе [Аутентификация](#authentication).</span><span class="sxs-lookup"><span data-stu-id="6c17c-170">Details in the [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="6c17c-171">Сведения о выходных данных</span><span class="sxs-lookup"><span data-stu-id="6c17c-171">Output details</span></span>
<span data-ttu-id="6c17c-172">Ниже приведены сведения о выходных данных для ответа HTTP.</span><span class="sxs-lookup"><span data-stu-id="6c17c-172">The following are output details for the HTTP response.</span></span>

| <span data-ttu-id="6c17c-173">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="6c17c-173">Property name</span></span> | <span data-ttu-id="6c17c-174">Тип данных</span><span class="sxs-lookup"><span data-stu-id="6c17c-174">Data type</span></span> | <span data-ttu-id="6c17c-175">Описание</span><span class="sxs-lookup"><span data-stu-id="6c17c-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c17c-176">Заголовки</span><span class="sxs-lookup"><span data-stu-id="6c17c-176">Headers</span></span> |<span data-ttu-id="6c17c-177">object</span><span class="sxs-lookup"><span data-stu-id="6c17c-177">object</span></span> |<span data-ttu-id="6c17c-178">Заголовки ответов</span><span class="sxs-lookup"><span data-stu-id="6c17c-178">Response headers</span></span> |
| <span data-ttu-id="6c17c-179">Текст</span><span class="sxs-lookup"><span data-stu-id="6c17c-179">Body</span></span> |<span data-ttu-id="6c17c-180">object</span><span class="sxs-lookup"><span data-stu-id="6c17c-180">object</span></span> |<span data-ttu-id="6c17c-181">Объект ответа</span><span class="sxs-lookup"><span data-stu-id="6c17c-181">Response object</span></span> |
| <span data-ttu-id="6c17c-182">Код состояния</span><span class="sxs-lookup"><span data-stu-id="6c17c-182">Status Code</span></span> |<span data-ttu-id="6c17c-183">int</span><span class="sxs-lookup"><span data-stu-id="6c17c-183">int</span></span> |<span data-ttu-id="6c17c-184">HTTP status code (Код состояния HTTP)</span><span class="sxs-lookup"><span data-stu-id="6c17c-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="6c17c-185">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="6c17c-185">Authentication</span></span>
<span data-ttu-id="6c17c-186">Компонент Logic Apps позволяет использовать разные типы аутентификации для конечных точек HTTP.</span><span class="sxs-lookup"><span data-stu-id="6c17c-186">The Logic Apps feature allows you to use different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="6c17c-187">Такую аутентификацию можно применять с соединителями **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)** и **[HTTP Webhook](connectors-native-webhook.md)**.</span><span class="sxs-lookup"><span data-stu-id="6c17c-187">You can use this authentication with the **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="6c17c-188">Ниже приведены типы аутентификации, которые можно настроить.</span><span class="sxs-lookup"><span data-stu-id="6c17c-188">The following types of authentication are configurable:</span></span>

* [<span data-ttu-id="6c17c-189">Обычная аутентификация</span><span class="sxs-lookup"><span data-stu-id="6c17c-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="6c17c-190">Аутентификация на основе сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="6c17c-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="6c17c-191">Аутентификация Azure Active Directory (Azure AD) OAuth</span><span class="sxs-lookup"><span data-stu-id="6c17c-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="6c17c-192">Обычная аутентификация</span><span class="sxs-lookup"><span data-stu-id="6c17c-192">Basic authentication</span></span>

<span data-ttu-id="6c17c-193">Для обычной аутентификации требуется следующий объект аутентификации.</span><span class="sxs-lookup"><span data-stu-id="6c17c-193">The following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="6c17c-194">Звездочка (*) означает, что это поле обязательное для заполнения.</span><span class="sxs-lookup"><span data-stu-id="6c17c-194">A * means that it is a required field.</span></span>

| <span data-ttu-id="6c17c-195">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="6c17c-195">Property name</span></span> | <span data-ttu-id="6c17c-196">Тип данных</span><span class="sxs-lookup"><span data-stu-id="6c17c-196">Data type</span></span> | <span data-ttu-id="6c17c-197">Описание</span><span class="sxs-lookup"><span data-stu-id="6c17c-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c17c-198">Тип*</span><span class="sxs-lookup"><span data-stu-id="6c17c-198">Type*</span></span> |<span data-ttu-id="6c17c-199">type</span><span class="sxs-lookup"><span data-stu-id="6c17c-199">type</span></span> |<span data-ttu-id="6c17c-200">Тип аутентификации (для обычной аутентификации значение должно быть `Basic`)</span><span class="sxs-lookup"><span data-stu-id="6c17c-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="6c17c-201">Имя пользователя*</span><span class="sxs-lookup"><span data-stu-id="6c17c-201">Username*</span></span> |<span data-ttu-id="6c17c-202">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="6c17c-202">username</span></span> |<span data-ttu-id="6c17c-203">Имя пользователя для аутентификации</span><span class="sxs-lookup"><span data-stu-id="6c17c-203">User name to authenticate</span></span> |
| <span data-ttu-id="6c17c-204">Пароль*</span><span class="sxs-lookup"><span data-stu-id="6c17c-204">Password*</span></span> |<span data-ttu-id="6c17c-205">пароль</span><span class="sxs-lookup"><span data-stu-id="6c17c-205">password</span></span> |<span data-ttu-id="6c17c-206">Пароль для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="6c17c-206">Password to authenticate</span></span> |

> [!TIP]
> <span data-ttu-id="6c17c-207">Если вы хотите использовать пароль, который не удается получить из определения, используйте параметр `securestring` и  
> [функцию определения рабочего процесса](http://aka.ms/logicappdocs) `@parameters()`.</span><span class="sxs-lookup"><span data-stu-id="6c17c-207">If you want to use a password that cannot be retrieved from the definition, use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="6c17c-208">Например:</span><span class="sxs-lookup"><span data-stu-id="6c17c-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="6c17c-209">Аутентификация на основе сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="6c17c-209">Client certificate authentication</span></span>

<span data-ttu-id="6c17c-210">Для аутентификации на основе сертификата клиента требуется следующий объект аутентификации.</span><span class="sxs-lookup"><span data-stu-id="6c17c-210">The following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="6c17c-211">Звездочка (*) означает, что это поле обязательное для заполнения.</span><span class="sxs-lookup"><span data-stu-id="6c17c-211">A * means that it is a required field.</span></span>

| <span data-ttu-id="6c17c-212">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="6c17c-212">Property name</span></span> | <span data-ttu-id="6c17c-213">Тип данных</span><span class="sxs-lookup"><span data-stu-id="6c17c-213">Data type</span></span> | <span data-ttu-id="6c17c-214">Описание</span><span class="sxs-lookup"><span data-stu-id="6c17c-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c17c-215">Тип*</span><span class="sxs-lookup"><span data-stu-id="6c17c-215">Type*</span></span> |<span data-ttu-id="6c17c-216">type</span><span class="sxs-lookup"><span data-stu-id="6c17c-216">type</span></span> |<span data-ttu-id="6c17c-217">Тип аутентификации (для аутентификации на основе SSL-сертификатов клиента значение должно быть `ClientCertificate`)</span><span class="sxs-lookup"><span data-stu-id="6c17c-217">The type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="6c17c-218">PFX*</span><span class="sxs-lookup"><span data-stu-id="6c17c-218">PFX*</span></span> |<span data-ttu-id="6c17c-219">pfx</span><span class="sxs-lookup"><span data-stu-id="6c17c-219">pfx</span></span> |<span data-ttu-id="6c17c-220">Содержимое файла обмена личной информацией (PFX-файла) с кодировкой Base64</span><span class="sxs-lookup"><span data-stu-id="6c17c-220">The Base64-encoded contents of the Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="6c17c-221">Пароль*</span><span class="sxs-lookup"><span data-stu-id="6c17c-221">Password*</span></span> |<span data-ttu-id="6c17c-222">пароль</span><span class="sxs-lookup"><span data-stu-id="6c17c-222">password</span></span> |<span data-ttu-id="6c17c-223">Пароль для доступа к PFX-файлу</span><span class="sxs-lookup"><span data-stu-id="6c17c-223">The password to access the PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="6c17c-224">Чтобы применить параметр, который после сохранения приложения логики будет недоступным для чтения в определении, можно использовать параметр `securestring` и  
> [функцию определения рабочего процесса](http://aka.ms/logicappdocs) `@parameters()`.</span><span class="sxs-lookup"><span data-stu-id="6c17c-224">To use a parameter that won't be readable in the definition after saving the logic app, you can use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="6c17c-225">Например:</span><span class="sxs-lookup"><span data-stu-id="6c17c-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="6c17c-226">Аутентификация Azure AD OAuth</span><span class="sxs-lookup"><span data-stu-id="6c17c-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="6c17c-227">Для аутентификации Azure AD OAuth требуется следующий объект аутентификации.</span><span class="sxs-lookup"><span data-stu-id="6c17c-227">The following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="6c17c-228">Звездочка (*) означает, что это поле обязательное для заполнения.</span><span class="sxs-lookup"><span data-stu-id="6c17c-228">A * means that it is a required field.</span></span>

| <span data-ttu-id="6c17c-229">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="6c17c-229">Property name</span></span> | <span data-ttu-id="6c17c-230">Тип данных</span><span class="sxs-lookup"><span data-stu-id="6c17c-230">Data type</span></span> | <span data-ttu-id="6c17c-231">Описание</span><span class="sxs-lookup"><span data-stu-id="6c17c-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c17c-232">Тип*</span><span class="sxs-lookup"><span data-stu-id="6c17c-232">Type*</span></span> |<span data-ttu-id="6c17c-233">type</span><span class="sxs-lookup"><span data-stu-id="6c17c-233">type</span></span> |<span data-ttu-id="6c17c-234">Тип аутентификации (для аутентификации Azure AD OAuth значение должно быть `ActiveDirectoryOAuth`)</span><span class="sxs-lookup"><span data-stu-id="6c17c-234">The type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="6c17c-235">Клиент*</span><span class="sxs-lookup"><span data-stu-id="6c17c-235">Tenant*</span></span> |<span data-ttu-id="6c17c-236">tenant</span><span class="sxs-lookup"><span data-stu-id="6c17c-236">tenant</span></span> |<span data-ttu-id="6c17c-237">Идентификатор клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c17c-237">The tenant identifier for the Azure AD tenant</span></span> |
| <span data-ttu-id="6c17c-238">Аудитория*</span><span class="sxs-lookup"><span data-stu-id="6c17c-238">Audience*</span></span> |<span data-ttu-id="6c17c-239">audience</span><span class="sxs-lookup"><span data-stu-id="6c17c-239">audience</span></span> |<span data-ttu-id="6c17c-240">Ресурс, для которого запрашивается разрешение на использование.</span><span class="sxs-lookup"><span data-stu-id="6c17c-240">The resource you are requesting authorization to use.</span></span> <span data-ttu-id="6c17c-241">Например: `https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="6c17c-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="6c17c-242">Идентификатор клиента*</span><span class="sxs-lookup"><span data-stu-id="6c17c-242">Client ID*</span></span> |<span data-ttu-id="6c17c-243">clientid</span><span class="sxs-lookup"><span data-stu-id="6c17c-243">clientId</span></span> |<span data-ttu-id="6c17c-244">Идентификатор клиента для приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c17c-244">The client identifier for the Azure AD application</span></span> |
| <span data-ttu-id="6c17c-245">Секрет*</span><span class="sxs-lookup"><span data-stu-id="6c17c-245">Secret*</span></span> |<span data-ttu-id="6c17c-246">secret</span><span class="sxs-lookup"><span data-stu-id="6c17c-246">secret</span></span> |<span data-ttu-id="6c17c-247">Секретные данные клиента, запрашивающего маркер</span><span class="sxs-lookup"><span data-stu-id="6c17c-247">The secret of the client that is requesting the token</span></span> |

> [!TIP]
> <span data-ttu-id="6c17c-248">Можно использовать параметр `securestring` и [функцию определения рабочего процесса](http://aka.ms/logicappdocs) `@parameters()`, чтобы применить параметр, который после сохранения будет недоступным для чтения в определении.</span><span class="sxs-lookup"><span data-stu-id="6c17c-248">You can use a `securestring` parameter and the `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) to use a parameter that won't be readable in the definition after saving.</span></span>
> 
> 

<span data-ttu-id="6c17c-249">Например:</span><span class="sxs-lookup"><span data-stu-id="6c17c-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="6c17c-250">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6c17c-250">Next steps</span></span>
<span data-ttu-id="6c17c-251">Теперь опробуйте платформу и [создайте приложение логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="6c17c-251">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="6c17c-252">Чтобы узнать, какие еще соединители доступны в приложениях логики, ознакомьтесь со [списком интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="6c17c-252">You can explore the other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>

