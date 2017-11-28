---
title: "Вызовы, срабатывания триггеров и создание вложенных рабочих процессов c помощью конечных точек HTTP в Azure Logic Apps | Документация Майкрософт"
description: "Настройка конечных точек HTTP для вызова, срабатывания триггеров или создания вложенных рабочих процессов для Azure Logic Apps"
services: logic-apps
keywords: "рабочие процессы, конечные точки HTTP"
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 73ba2a70-03e9-4982-bfc8-ebfaad798bc2
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 03/31/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: c92692db23ac59f67890e26cce6b2d3272e8901d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a><span data-ttu-id="6a26e-104">Вызовы, срабатывания триггеров и создание вложенных рабочих процессов в приложениях логики</span><span class="sxs-lookup"><span data-stu-id="6a26e-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span></span>

<span data-ttu-id="6a26e-105">Вы можете предоставлять доступ к синхронным конечным точкам HTTP, выступающим в качестве триггеров в приложениях логики, с помощью которых можно активировать или вызвать приложение логики через URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="6a26e-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span></span> <span data-ttu-id="6a26e-106">Также вы можете создавать вложенные рабочие процессы в приложениях логики с помощью шаблона вызываемых конечных точек.</span><span class="sxs-lookup"><span data-stu-id="6a26e-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span></span>

<span data-ttu-id="6a26e-107">Для создания конечных точек HTTP, чтобы ваши приложения логики могли получать входящие запросы, добавьте эти триггеры:</span><span class="sxs-lookup"><span data-stu-id="6a26e-107">To create HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span></span>

* [<span data-ttu-id="6a26e-108">Запрос</span><span class="sxs-lookup"><span data-stu-id="6a26e-108">Request</span></span>](../connectors/connectors-native-reqres.md)

* [<span data-ttu-id="6a26e-109">webhook API подключения;</span><span class="sxs-lookup"><span data-stu-id="6a26e-109">API Connection Webhook</span></span>](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* <span data-ttu-id="6a26e-110">[webhook HTTP](../connectors/connectors-native-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="6a26e-110">[HTTP Webhook](../connectors/connectors-native-webhook.md)</span></span>

   > [!NOTE]
   > <span data-ttu-id="6a26e-111">Несмотря на то что в наших примерах используется триггер **запроса**, все принципы аналогично применимы для других типов триггеров, поэтому вы можете использовать любой из перечисленных триггеров HTTP.</span><span class="sxs-lookup"><span data-stu-id="6a26e-111">Although our examples use the **Request** trigger, you can use any of the listed HTTP triggers, and all principles identically apply to the other trigger types.</span></span>

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a><span data-ttu-id="6a26e-112">Настройка конечной точки HTTP для приложения логики</span><span class="sxs-lookup"><span data-stu-id="6a26e-112">Set up an HTTP endpoint for your logic app</span></span>

<span data-ttu-id="6a26e-113">Чтобы создать конечную точку HTTP, добавьте триггер, который может принимать входящие запросы.</span><span class="sxs-lookup"><span data-stu-id="6a26e-113">To create an HTTP endpoint, add a trigger that can receive incoming requests.</span></span>

1. <span data-ttu-id="6a26e-114">Войдите на [портал Azure](https://portal.azure.com "Портал Azure").</span><span class="sxs-lookup"><span data-stu-id="6a26e-114">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="6a26e-115">В вашем приложении логики откройте конструктор приложений логики.</span><span class="sxs-lookup"><span data-stu-id="6a26e-115">Go to your logic app, and open Logic App Designer.</span></span>

2. <span data-ttu-id="6a26e-116">Добавьте триггер, который позволяет приложению логики получать входящие запросы.</span><span class="sxs-lookup"><span data-stu-id="6a26e-116">Add a trigger that lets your logic app receive incoming requests.</span></span> <span data-ttu-id="6a26e-117">Например, добавьте триггер **Request** в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="6a26e-117">For example, add the **Request** trigger to your logic app.</span></span>

3.  <span data-ttu-id="6a26e-118">В разделе **Схема JSON текста запроса** вы можете при необходимости ввести схему JSON для полезных данных, которые должен получить триггер.</span><span class="sxs-lookup"><span data-stu-id="6a26e-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for the payload (data) that you expect the trigger to receive.</span></span>

    <span data-ttu-id="6a26e-119">Конструктор использует эту схему для создания токенов, с помощью которых приложение логики получает, анализирует и передает данные от триггера через рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="6a26e-119">The designer uses this schema for generating tokens that your logic app can use to consume, parse, and pass data from the trigger through your workflow.</span></span> 
    <span data-ttu-id="6a26e-120">Дополнительные сведения о [токенах, созданных из схем JSON](#generated-tokens).</span><span class="sxs-lookup"><span data-stu-id="6a26e-120">More about [tokens generated from JSON schemas](#generated-tokens).</span></span>

    <span data-ttu-id="6a26e-121">В этом примере введите схему, показанную в конструкторе:</span><span class="sxs-lookup"><span data-stu-id="6a26e-121">For this example, enter the schema shown in the designer:</span></span>

    ```json
    {
      "type": "object",
      "properties": {
        "address": {
          "type": "string"
        }
      },
      "required": [
        "address"
      ]
    }
    ```

    ![Добавление действия Request][1]

    > [!TIP]
    > 
    > <span data-ttu-id="6a26e-123">Вы можете создать схему для примера полезных данных JSON с помощью такого инструмента, как [jsonschema.net](http://jsonschema.net/), или с помощью триггера **запроса**, выбрав **Использовать пример полезной нагрузки, чтобы создать схему**.</span><span class="sxs-lookup"><span data-stu-id="6a26e-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in the **Request** trigger by choosing **Use sample payload to generate schema**.</span></span> 
    > <span data-ttu-id="6a26e-124">Введите образец полезных данных и выберите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="6a26e-124">Enter your sample payload, and choose **Done**.</span></span>

    <span data-ttu-id="6a26e-125">Например, образец полезных данных</span><span class="sxs-lookup"><span data-stu-id="6a26e-125">For example, this sample payload:</span></span>

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    <span data-ttu-id="6a26e-126">создает эту схему:</span><span class="sxs-lookup"><span data-stu-id="6a26e-126">generates this schema:</span></span>

    ```json
    }
       "type": "object",
       "properties": {
          "address": {
             "type": "string" 
          }
       }
    }
    ```

4.  <span data-ttu-id="6a26e-127">Сохраните приложение логики.</span><span class="sxs-lookup"><span data-stu-id="6a26e-127">Save your logic app.</span></span> <span data-ttu-id="6a26e-128">В поле **HTTP POST на этот URL-адрес** необходимо указать созданный URL-адрес обратного вызова:</span><span class="sxs-lookup"><span data-stu-id="6a26e-128">Under **HTTP POST to this URL**, you should now find a generated callback URL, like this example:</span></span>

    ![Созданный URL-адрес обратного вызова для конечной точки](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    <span data-ttu-id="6a26e-130">Этот URL-адрес содержит ключ подписанного URL-адреса в параметрах запроса, используемого для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6a26e-130">This URL contains a Shared Access Signature (SAS) key in the query parameters that are used for authentication.</span></span> 
    <span data-ttu-id="6a26e-131">Вы также можете получить URL-адрес конечной точки HTTP из колонки обзора приложения логики на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="6a26e-131">You can also get the HTTP endpoint URL from your logic app overview in the Azure portal.</span></span> <span data-ttu-id="6a26e-132">В разделе **Журнал триггеров** выберите триггер:</span><span class="sxs-lookup"><span data-stu-id="6a26e-132">Under **Trigger History**, select your trigger:</span></span>

    ![Получение URL-адреса конечной точки HTTP на портале Azure][2]

    <span data-ttu-id="6a26e-134">URL-адрес также можно получить, выполнив этот вызов:</span><span class="sxs-lookup"><span data-stu-id="6a26e-134">Or you can get the URL by making this call:</span></span>

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-the-http-method-for-your-trigger"></a><span data-ttu-id="6a26e-135">Изменение метода HTTP для триггера</span><span class="sxs-lookup"><span data-stu-id="6a26e-135">Change the HTTP method for your trigger</span></span>

<span data-ttu-id="6a26e-136">По умолчанию триггер **запроса** ожидает запрос HTTP POST, но вы можете воспользоваться другим методом HTTP.</span><span class="sxs-lookup"><span data-stu-id="6a26e-136">By default, the **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span></span> 

> [!NOTE]
> <span data-ttu-id="6a26e-137">Вы можете указать только один тип метода.</span><span class="sxs-lookup"><span data-stu-id="6a26e-137">You can specify only one method type.</span></span>

1. <span data-ttu-id="6a26e-138">Для триггера **запроса** выберите **Показать дополнительные параметры**.</span><span class="sxs-lookup"><span data-stu-id="6a26e-138">On your **Request** trigger, choose **Show advanced options**.</span></span>

2. <span data-ttu-id="6a26e-139">Откройте список **Метод**.</span><span class="sxs-lookup"><span data-stu-id="6a26e-139">Open the **Method** list.</span></span> <span data-ttu-id="6a26e-140">В этом примере выберите **GET**, чтобы вы могли позже проверить URL-адрес конечной точки HTTP.</span><span class="sxs-lookup"><span data-stu-id="6a26e-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6a26e-141">Вы можете выбрать любой другой метод HTTP или указать пользовательский метод для своего приложения логики.</span><span class="sxs-lookup"><span data-stu-id="6a26e-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span></span>

    ![Изменение метода HTTP](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a><span data-ttu-id="6a26e-143">Принятие параметров через URL-адрес конечной точки HTTP</span><span class="sxs-lookup"><span data-stu-id="6a26e-143">Accept parameters through your HTTP endpoint URL</span></span>

<span data-ttu-id="6a26e-144">Если вы хотите, чтобы ваш URL-адрес конечной точки HTTP принял параметры, следует настроить относительный путь триггера.</span><span class="sxs-lookup"><span data-stu-id="6a26e-144">When you want your HTTP endpoint URL to accept parameters, customize your trigger's relative path.</span></span>

1. <span data-ttu-id="6a26e-145">Для триггера **запроса** выберите **Показать дополнительные параметры**.</span><span class="sxs-lookup"><span data-stu-id="6a26e-145">On your **Request** trigger, choose **Show advanced options**.</span></span> 

2. <span data-ttu-id="6a26e-146">В разделе **Метод** укажите метод HTTP, который будет использовать запрос.</span><span class="sxs-lookup"><span data-stu-id="6a26e-146">Under **Method**, specify the HTTP method that you want your request to use.</span></span> <span data-ttu-id="6a26e-147">В этом примере выберите метод **GET**, чтобы проверить свой URL-адрес конечной точки HTTP.</span><span class="sxs-lookup"><span data-stu-id="6a26e-147">For this example, select the **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span></span>

      > [!NOTE]
      > <span data-ttu-id="6a26e-148">Когда вы указываете относительный путь для своего триггера, вы должны явно указать для триггера метод HTTP.</span><span class="sxs-lookup"><span data-stu-id="6a26e-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span></span>

3. <span data-ttu-id="6a26e-149">В поле **Относительный путь** укажите относительный путь для параметра, который ваш URL-адрес должен принять, например `customers/{customerID}`.</span><span class="sxs-lookup"><span data-stu-id="6a26e-149">Under **Relative path**, specify the relative path for the parameter that your URL should accept, for example, `customers/{customerID}`.</span></span>

    ![Указание метода HTTP и относительного пути для параметра](./media/logic-apps-http-endpoint/relativeurl.png)

4. <span data-ttu-id="6a26e-151">Чтобы использовать параметр, добавьте действие **Ответ** для приложения логики.</span><span class="sxs-lookup"><span data-stu-id="6a26e-151">To use the parameter, add a **Response** action to your logic app.</span></span> <span data-ttu-id="6a26e-152">(Для вашего триггера выберите **Новый шаг** > **Добавить действие** > **Ответ**.)</span><span class="sxs-lookup"><span data-stu-id="6a26e-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span></span> 

5. <span data-ttu-id="6a26e-153">В **тексте** ответа добавьте токен для параметра, который вы указали в относительном пути триггера.</span><span class="sxs-lookup"><span data-stu-id="6a26e-153">In your response's **Body**, include the token for the parameter that you specified in your trigger's relative path.</span></span>

    <span data-ttu-id="6a26e-154">Например, чтобы вернуть `Hello {customerID}`, добавьте в **текст** ответа `Hello {customerID token}`.</span><span class="sxs-lookup"><span data-stu-id="6a26e-154">For example, to return `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span></span> 
    <span data-ttu-id="6a26e-155">Должны отображаться и демонстрировать динамического содержимого списка `customerID` для выбора маркера.</span><span class="sxs-lookup"><span data-stu-id="6a26e-155">The dynamic content list should appear and show the `customerID` token for you to select.</span></span>

    ![Добавление параметра в текст ответа](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    <span data-ttu-id="6a26e-157">Поле **текста** должно выглядеть, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="6a26e-157">Your **Body** should look like this example:</span></span>

    ![Поле текста ответа с параметром](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. <span data-ttu-id="6a26e-159">Сохраните приложение логики.</span><span class="sxs-lookup"><span data-stu-id="6a26e-159">Save your logic app.</span></span> 

    <span data-ttu-id="6a26e-160">URL-адрес конечной точки HTTP теперь включает относительный путь, например:</span><span class="sxs-lookup"><span data-stu-id="6a26e-160">Your HTTP endpoint URL now includes the relative path, for example:</span></span> 

    <span data-ttu-id="6a26e-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span><span class="sxs-lookup"><span data-stu-id="6a26e-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span></span>

7. <span data-ttu-id="6a26e-162">Для проверки конечной точки HTTP скопируйте и вставьте обновленный URL-адрес в другом окне браузера, но замените `{customerID}` на `123456` и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="6a26e-162">To test your HTTP endpoint, copy and paste the updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span></span>

    <span data-ttu-id="6a26e-163">Браузер должен вывести следующий текст:</span><span class="sxs-lookup"><span data-stu-id="6a26e-163">Your browser should show this text:</span></span> 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a><span data-ttu-id="6a26e-164">Токены, создаваемые из схем JSON для вашего приложения логики</span><span class="sxs-lookup"><span data-stu-id="6a26e-164">Tokens generated from JSON schemas for your logic app</span></span>

<span data-ttu-id="6a26e-165">При указании схемы JSON для триггера **запроса** в конструкторе приложений логики создаются токены для свойств в этой схеме.</span><span class="sxs-lookup"><span data-stu-id="6a26e-165">When you provide a JSON schema in your **Request** trigger, the Logic App Designer generates tokens for properties in that schema.</span></span> <span data-ttu-id="6a26e-166">Затем эти токены можно использовать для передачи данных через рабочий процесс приложения логики.</span><span class="sxs-lookup"><span data-stu-id="6a26e-166">You can then use those tokens for passing data through your logic app workflow.</span></span>

<span data-ttu-id="6a26e-167">В этом примере, если вы добавили свойства `title` и `name` для схемы JSON, их токены теперь доступны для использования на последующих шагах рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="6a26e-167">For this example, if you add the `title` and `name` properties to your JSON schema, their tokens are now available to use in later workflow steps.</span></span> 

<span data-ttu-id="6a26e-168">Ниже приведена полная схема JSON.</span><span class="sxs-lookup"><span data-stu-id="6a26e-168">Here is the complete JSON schema:</span></span>

```json
{
   "type": "object",
   "properties": {
      "address": {
         "type": "string"
      },
      "title": {
         "type": "string"
      },
      "name": {
         "type": "string"
      }
   },
   "required": [
      "address",
      "title",
      "name"
   ]
}
```

## <a name="create-nested-workflows-for-logic-apps"></a><span data-ttu-id="6a26e-169">Создание вложенных рабочих процессов для приложений логики</span><span class="sxs-lookup"><span data-stu-id="6a26e-169">Create nested workflows for logic apps</span></span>

<span data-ttu-id="6a26e-170">Вы можете вкладывать рабочие процессы в свое приложение логики путем добавления других приложений логики, которые могут принимать запросы.</span><span class="sxs-lookup"><span data-stu-id="6a26e-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span></span> <span data-ttu-id="6a26e-171">Чтобы включить приложения логики, добавьте действие **Azure Logic Apps — Выберите рабочий процесс Logic Apps** в свой триггер.</span><span class="sxs-lookup"><span data-stu-id="6a26e-171">To include these logic apps, add the **Azure Logic Apps - Choose a Logic Apps workflow** action to your trigger.</span></span> <span data-ttu-id="6a26e-172">Затем вы можете выбрать подходящие приложения логики.</span><span class="sxs-lookup"><span data-stu-id="6a26e-172">You can then select from eligible logic apps.</span></span>

![Добавление другого приложения логики](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a><span data-ttu-id="6a26e-174">Вызов или запуск приложений логики через конечные точки HTTP</span><span class="sxs-lookup"><span data-stu-id="6a26e-174">Call or trigger logic apps through HTTP endpoints</span></span>

<span data-ttu-id="6a26e-175">После создания конечной точки HTTP можно вызвать приложение логики, добавив метод `POST` к полному URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="6a26e-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method to the full URL.</span></span> <span data-ttu-id="6a26e-176">Приложения логики имеют встроенную поддержку конечных точек прямого доступа.</span><span class="sxs-lookup"><span data-stu-id="6a26e-176">Logic apps have built-in support for direct-access endpoints.</span></span>

## <a name="reference-content-from-an-incoming-request"></a><span data-ttu-id="6a26e-177">Ссылка на содержимое входящего запроса</span><span class="sxs-lookup"><span data-stu-id="6a26e-177">Reference content from an incoming request</span></span>

<span data-ttu-id="6a26e-178">При использовании типа содержимого `application/json` можно ссылаться на свойства из входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="6a26e-178">If the content's type is `application/json`, you can reference properties from the incoming request.</span></span> <span data-ttu-id="6a26e-179">Иначе содержимое обрабатывается как единая двоичная единица, которую можно передать в другие интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="6a26e-179">Otherwise, content is treated as a single binary unit that you can pass to other APIs.</span></span> <span data-ttu-id="6a26e-180">Чтобы сослаться на это содержимое внутри рабочего процесса, необходимо преобразовать его.</span><span class="sxs-lookup"><span data-stu-id="6a26e-180">To reference this content inside the workflow, you must convert that content.</span></span> <span data-ttu-id="6a26e-181">Например, если передать содержимое `application/xml`, можно использовать `@xpath()` для извлечения XPath или `@json()` для преобразования XML в JSON.</span><span class="sxs-lookup"><span data-stu-id="6a26e-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML to JSON.</span></span> <span data-ttu-id="6a26e-182">Дополнительные сведения о [работе с типами содержимого](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="6a26e-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span></span>

<span data-ttu-id="6a26e-183">Чтобы получить выходные данные из входящего запроса, можно использовать функцию `@triggerOutputs()`.</span><span class="sxs-lookup"><span data-stu-id="6a26e-183">To get the output from an incoming request, you can use the `@triggerOutputs()` function.</span></span> <span data-ttu-id="6a26e-184">Выходные данные выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6a26e-184">The output might look like this example:</span></span>

```json
{
    "headers": {
        "content-type" : "application/json"
    },
    "body": {
        "myProperty" : "property value"
    }
}
```

<span data-ttu-id="6a26e-185">Для доступа к свойству `body` можно использовать сокращенный вариант `@triggerBody()`.</span><span class="sxs-lookup"><span data-stu-id="6a26e-185">To access the `body` property specifically, you can use the `@triggerBody()` shortcut.</span></span> 

## <a name="respond-to-requests"></a><span data-ttu-id="6a26e-186">Ответ на запросы</span><span class="sxs-lookup"><span data-stu-id="6a26e-186">Respond to requests</span></span>

<span data-ttu-id="6a26e-187">Возможно, вы захотите ответить на определенные запросы, которые запускают логическое приложение, возвращая содержимое вызывающему объекту.</span><span class="sxs-lookup"><span data-stu-id="6a26e-187">You might want to respond to certain requests that start a logic app by returning content to the caller.</span></span> <span data-ttu-id="6a26e-188">Чтобы создать код состояния, заголовок и текст вашего ответа, вы можете использовать действие **Ответ**.</span><span class="sxs-lookup"><span data-stu-id="6a26e-188">To construct the status code, header, and body for your response, you can use the **Response** action.</span></span> <span data-ttu-id="6a26e-189">Это действие может находиться в любом месте приложения логики, а не только в конце рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="6a26e-189">This action can appear anywhere in your logic app, not just at the end of your workflow.</span></span>

> [!NOTE] 
> <span data-ttu-id="6a26e-190">Если ваше приложение логики не включает действие **Ответ**, конечная точка HTTP *немедленно* отвечает состоянием **202 — Принят**.</span><span class="sxs-lookup"><span data-stu-id="6a26e-190">If your logic app doesn't include a **Response**, the HTTP endpoint responds *immediately* with a **202 Accepted** status.</span></span> <span data-ttu-id="6a26e-191">Кроме того, для получения ответа на исходный запрос следует завершить все шаги, необходимые для получения ответа, в течение [времени ожидания запроса](./logic-apps-limits-and-config.md). Исключение составляет только вызов рабочего процесса в качестве вложенного приложения логики.</span><span class="sxs-lookup"><span data-stu-id="6a26e-191">Also, for the original request to get the response, all steps required for the response must finish within the [request timeout limit](./logic-apps-limits-and-config.md) unless you call the workflow as a nested logic app.</span></span> <span data-ttu-id="6a26e-192">Если в течение этого времени ответ не получен, срок действия входящего запроса истечет и будет получен ответ HTTP **408 время ожидания клиента истекло**.</span><span class="sxs-lookup"><span data-stu-id="6a26e-192">If no response happens within this limit, the incoming request times out and receives the HTTP response **408 Client timeout**.</span></span> <span data-ttu-id="6a26e-193">Для вложенных приложений логики родительское приложение логики будет ожидать ответ до конца, независимо от того, сколько времени на это потребуется.</span><span class="sxs-lookup"><span data-stu-id="6a26e-193">For nested logic apps, the parent logic app continues to wait for a response until completed, regardless of how much time is required.</span></span>

### <a name="construct-the-response"></a><span data-ttu-id="6a26e-194">Создание ответа</span><span class="sxs-lookup"><span data-stu-id="6a26e-194">Construct the response</span></span>

<span data-ttu-id="6a26e-195">Вы можете включить несколько заголовков и любой тип содержимого в тексте ответа.</span><span class="sxs-lookup"><span data-stu-id="6a26e-195">You can include more than one header and any type of content in the response body.</span></span> <span data-ttu-id="6a26e-196">В нашем примере ответа заголовок указывает, что ответ имеет тип содержимого `application/json`,</span><span class="sxs-lookup"><span data-stu-id="6a26e-196">In our example response, the header specifies that the response has content type `application/json`.</span></span> <span data-ttu-id="6a26e-197">а текст содержит `title` и `name`, на основе обновленной ранее схемы JSON для триггера **запроса**.</span><span class="sxs-lookup"><span data-stu-id="6a26e-197">and the body contains `title` and `name`, based on the JSON schema updated previously for the **Request** trigger.</span></span>

![Действие ответа HTTP][3]

<span data-ttu-id="6a26e-199">У ответов есть следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="6a26e-199">Responses have these properties:</span></span>

| <span data-ttu-id="6a26e-200">Свойство</span><span class="sxs-lookup"><span data-stu-id="6a26e-200">Property</span></span> | <span data-ttu-id="6a26e-201">Описание</span><span class="sxs-lookup"><span data-stu-id="6a26e-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6a26e-202">statusCode</span><span class="sxs-lookup"><span data-stu-id="6a26e-202">statusCode</span></span> |<span data-ttu-id="6a26e-203">Указывает код состояния HTTP для ответа на входящий запрос.</span><span class="sxs-lookup"><span data-stu-id="6a26e-203">Specifies the HTTP status code for responding to the incoming request.</span></span> <span data-ttu-id="6a26e-204">Это может быть любой допустимый код состояния, который начинается с 2xx, 4xx или 5xx.</span><span class="sxs-lookup"><span data-stu-id="6a26e-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span></span> <span data-ttu-id="6a26e-205">Но коды состояния 3xx не допускаются.</span><span class="sxs-lookup"><span data-stu-id="6a26e-205">However, 3xx status codes are not permitted.</span></span> |
| <span data-ttu-id="6a26e-206">headers</span><span class="sxs-lookup"><span data-stu-id="6a26e-206">headers</span></span> |<span data-ttu-id="6a26e-207">Определяет число заголовков для включения в ответ.</span><span class="sxs-lookup"><span data-stu-id="6a26e-207">Defines any number of headers to include in the response.</span></span> |
| <span data-ttu-id="6a26e-208">текст</span><span class="sxs-lookup"><span data-stu-id="6a26e-208">body</span></span> |<span data-ttu-id="6a26e-209">Определяет объект текста. Это может быть строка, объект JSON и даже двоичное содержимое из предыдущего шага.</span><span class="sxs-lookup"><span data-stu-id="6a26e-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span></span> |

<span data-ttu-id="6a26e-210">Вот как выглядит схема JSON для действия **Ответ**:</span><span class="sxs-lookup"><span data-stu-id="6a26e-210">Here's what the JSON schema looks like now for the **Response** action:</span></span>

``` json
"Response": {
   "inputs": {
      "body": {
         "title": "@{triggerBody()?['title']}",
         "name": "@{triggerBody()?['name']}"
      },
      "headers": {
           "content-type": "application/json"
      },
      "statusCode": 200
   },
   "runAfter": {},
   "type": "Response"
}
```

> [!TIP]
> <span data-ttu-id="6a26e-211">Чтобы просмотреть полное определение JSON для приложения логики, в конструкторе приложений логики выберите **Представление кода**.</span><span class="sxs-lookup"><span data-stu-id="6a26e-211">To view the complete JSON definition for your logic app, on the Logic App Designer, choose **Code view**.</span></span>

## <a name="q--a"></a><span data-ttu-id="6a26e-212">Вопросы и ответы</span><span class="sxs-lookup"><span data-stu-id="6a26e-212">Q & A</span></span>

#### <a name="q-what-about-url-security"></a><span data-ttu-id="6a26e-213">Вопрос. Как обеспечивается безопасность URL-адресов?</span><span class="sxs-lookup"><span data-stu-id="6a26e-213">Q: What about URL security?</span></span>

<span data-ttu-id="6a26e-214">Ответ. При создании URL-адресов обратного вызова Azure обеспечивает безопасность с помощью подписанного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="6a26e-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="6a26e-215">Подпись передается в качестве параметра запроса и проверяется перед запуском приложения логики.</span><span class="sxs-lookup"><span data-stu-id="6a26e-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span></span> <span data-ttu-id="6a26e-216">Azure создает эту подпись на основе уникального сочетания секретного ключа для каждого приложения логики, имени триггера и выполняемой операции.</span><span class="sxs-lookup"><span data-stu-id="6a26e-216">Azure generates the signature using a unique combination of a secret key per logic app, the trigger name, and the operation that's performed.</span></span> <span data-ttu-id="6a26e-217">Не имея доступа к секретному ключу приложения логики, создать действительную подпись невозможно.</span><span class="sxs-lookup"><span data-stu-id="6a26e-217">So unless someone has access to the secret logic app key, they cannot generate a valid signature.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="6a26e-218">Для рабочих и безопасных систем настоятельно не рекомендуется вызывать приложения логики напрямую из браузера, так как:</span><span class="sxs-lookup"><span data-stu-id="6a26e-218">For production and secure systems, we strongly recommend against calling your logic app directly from the browser because:</span></span>
   > 
   > * <span data-ttu-id="6a26e-219">ключ общего доступа отображается в URL-адресе;</span><span class="sxs-lookup"><span data-stu-id="6a26e-219">The shared access key appears in the URL.</span></span>
   > * <span data-ttu-id="6a26e-220">невозможно управлять политиками безопасного содержимого из-за общих доменов, используемых клиентами приложения логики.</span><span class="sxs-lookup"><span data-stu-id="6a26e-220">You can't manage secure content policies due to shared domains across Logic App customers.</span></span>

#### <a name="q-can-i-configure-http-endpoints-further"></a><span data-ttu-id="6a26e-221">Вопрос. Могу ли я дополнительно настроить конечные точки HTTP?</span><span class="sxs-lookup"><span data-stu-id="6a26e-221">Q: Can I configure HTTP endpoints further?</span></span>

<span data-ttu-id="6a26e-222">Ответ. Да, конечные точки HTTP поддерживают расширенную конфигурацию через [**управление API**](../api-management/api-management-key-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="6a26e-222">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span></span> <span data-ttu-id="6a26e-223">Эта служба также предлагает вам возможность согласованно управлять всеми своими API, включая приложения логики, настраивать имена домена, использовать дополнительные методы проверки подлинности и т. д. В частности она предоставляет следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="6a26e-223">This service also offers the capability for you to consistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span></span>

* [<span data-ttu-id="6a26e-224">Изменение метода запроса</span><span class="sxs-lookup"><span data-stu-id="6a26e-224">Change the request method</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [<span data-ttu-id="6a26e-225">Изменение сегментов URL-адреса запроса</span><span class="sxs-lookup"><span data-stu-id="6a26e-225">Change the URL segments of the request</span></span>](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* <span data-ttu-id="6a26e-226">настройка доменов управления API на [портале Azure](https://portal.azure.com/ "портал Azure");</span><span class="sxs-lookup"><span data-stu-id="6a26e-226">Set up your API Management domains in the [Azure portal](https://portal.azure.com/ "Azure portal")</span></span>
* <span data-ttu-id="6a26e-227">настройка политики для проверки базовой проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6a26e-227">Set up policy to check for Basic authentication</span></span>

#### <a name="q-what-changed-when-the-schema-migrated-from-the-december-1-2014-preview"></a><span data-ttu-id="6a26e-228">Вопрос. Что изменилось после миграции схемы с предварительной версии от 1 декабря 2014 года?</span><span class="sxs-lookup"><span data-stu-id="6a26e-228">Q: What changed when the schema migrated from the December 1, 2014 preview?</span></span>

<span data-ttu-id="6a26e-229">Ответ. Вот сводка об этих изменениях:</span><span class="sxs-lookup"><span data-stu-id="6a26e-229">A: Here's a summary about these changes:</span></span>

| <span data-ttu-id="6a26e-230">Предварительная версия от 1 декабря 2014 года</span><span class="sxs-lookup"><span data-stu-id="6a26e-230">December 1, 2014 preview</span></span> | <span data-ttu-id="6a26e-231">1 июня 2016 года</span><span class="sxs-lookup"><span data-stu-id="6a26e-231">June 1, 2016</span></span> |
| --- | --- |
| <span data-ttu-id="6a26e-232">Щелкните приложение API **Прослушиватель HTTP**.</span><span class="sxs-lookup"><span data-stu-id="6a26e-232">Click **HTTP Listener** API App</span></span> |<span data-ttu-id="6a26e-233">Щелкните **Ручной триггер** (приложение API не требуется).</span><span class="sxs-lookup"><span data-stu-id="6a26e-233">Click **Manual trigger** (no API App required)</span></span> |
| <span data-ttu-id="6a26e-234">Параметр прослушивателя HTTP*Sends response automatically*(Отправляет ответ автоматически).</span><span class="sxs-lookup"><span data-stu-id="6a26e-234">HTTP Listener setting "*Sends response automatically*"</span></span> |<span data-ttu-id="6a26e-235">Добавьте действие **Ответ** в определение рабочего процесса или не делайте этого</span><span class="sxs-lookup"><span data-stu-id="6a26e-235">Either include a **Response** action or not in the workflow definition</span></span> |
| <span data-ttu-id="6a26e-236">Настройка базовой проверки подлинности или OAuth</span><span class="sxs-lookup"><span data-stu-id="6a26e-236">Configure Basic or OAuth authentication</span></span> |<span data-ttu-id="6a26e-237">с помощью управления API</span><span class="sxs-lookup"><span data-stu-id="6a26e-237">via API Management</span></span> |
| <span data-ttu-id="6a26e-238">Настройка метода HTTP</span><span class="sxs-lookup"><span data-stu-id="6a26e-238">Configure HTTP method</span></span> |<span data-ttu-id="6a26e-239">В разделе **Показать дополнительные параметры** выберите метод HTTP</span><span class="sxs-lookup"><span data-stu-id="6a26e-239">Under **Show advanced options**, choose an HTTP method</span></span> |
| <span data-ttu-id="6a26e-240">Настройка относительного пути</span><span class="sxs-lookup"><span data-stu-id="6a26e-240">Configure relative path</span></span> |<span data-ttu-id="6a26e-241">В разделе **Показать дополнительные параметры** добавьте относительный путь</span><span class="sxs-lookup"><span data-stu-id="6a26e-241">Under **Show advanced options**, add a relative path</span></span> |
| <span data-ttu-id="6a26e-242">Ссылка на текст входящего ответа через `@triggerOutputs().body.Content`</span><span class="sxs-lookup"><span data-stu-id="6a26e-242">Reference the incoming body through `@triggerOutputs().body.Content`</span></span> |<span data-ttu-id="6a26e-243">Используйте для ссылки `@triggerOutputs().body`</span><span class="sxs-lookup"><span data-stu-id="6a26e-243">Reference through `@triggerOutputs().body`</span></span> |
| <span data-ttu-id="6a26e-244">**Отправка HTTP-ответа** для прослушивателя HTTP.</span><span class="sxs-lookup"><span data-stu-id="6a26e-244">**Send HTTP response** action on the HTTP Listener</span></span> |<span data-ttu-id="6a26e-245">Щелкните **Ответить на запрос HTTP** (приложение API не требуется)</span><span class="sxs-lookup"><span data-stu-id="6a26e-245">Click **Respond to HTTP request** (no API App required)</span></span> |

## <a name="get-help"></a><span data-ttu-id="6a26e-246">Получение справки</span><span class="sxs-lookup"><span data-stu-id="6a26e-246">Get help</span></span>

<span data-ttu-id="6a26e-247">Чтобы задать вопросы, помочь другим пользователям и узнать, что делают другие пользователи, посетите [форум по Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="6a26e-247">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="6a26e-248">Чтобы улучшить Azure Logic Apps и соединители, голосуйте за идеи или предлагайте собственные на [сайте обратной связи Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="6a26e-248">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a26e-249">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6a26e-249">Next steps</span></span>

* [<span data-ttu-id="6a26e-250">Создание определений приложений логики</span><span class="sxs-lookup"><span data-stu-id="6a26e-250">Author logic app definitions</span></span>](./logic-apps-author-definitions.md)
* [<span data-ttu-id="6a26e-251">Обработка ошибок и исключений</span><span class="sxs-lookup"><span data-stu-id="6a26e-251">Handle errors and exceptions</span></span>](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
