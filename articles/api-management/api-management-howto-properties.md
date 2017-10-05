---
title: "Использование свойств в политиках управления API Azure"
description: "Узнайте, как использовать свойства в политиках управления API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f39b00f-cf6e-4cef-9bf2-1f89202c0bc0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3b0fe2a300038e13cc488bdb4f50f8be270ea8f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-properties-in-azure-api-management-policies"></a><span data-ttu-id="12e3f-103">Использование свойств в политиках управления API Azure</span><span class="sxs-lookup"><span data-stu-id="12e3f-103">How to use properties in Azure API Management policies</span></span>
<span data-ttu-id="12e3f-104">Политики управления API представляют собой одну из эффективных функций системы, позволяющих издателю изменять поведение интерфейса API путем его настройки.</span><span class="sxs-lookup"><span data-stu-id="12e3f-104">API Management policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="12e3f-105">Политика — это коллекция правил, которые выполняются последовательно над запросом или ответом API.</span><span class="sxs-lookup"><span data-stu-id="12e3f-105">Policies are a collection of statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="12e3f-106">Для создания правил политики можно использовать литеральные текстовые значения, выражения политики и свойства.</span><span class="sxs-lookup"><span data-stu-id="12e3f-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="12e3f-107">Каждый экземпляр службы управления API имеет коллекцию свойств пар "ключ-значение", которые являются глобальными для экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="12e3f-107">Each API Management service instance has a properties collection of key/value pairs that are global to the service instance.</span></span> <span data-ttu-id="12e3f-108">Эти свойства можно использовать для управления постоянными строковыми значениями во всей конфигурации и политиках API.</span><span class="sxs-lookup"><span data-stu-id="12e3f-108">These properties can be used to manage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="12e3f-109">Каждое свойство имеет следующие атрибуты.</span><span class="sxs-lookup"><span data-stu-id="12e3f-109">Each property has the following attributes.</span></span>

| <span data-ttu-id="12e3f-110">Атрибут</span><span class="sxs-lookup"><span data-stu-id="12e3f-110">Attribute</span></span> | <span data-ttu-id="12e3f-111">Тип</span><span class="sxs-lookup"><span data-stu-id="12e3f-111">Type</span></span> | <span data-ttu-id="12e3f-112">Описание</span><span class="sxs-lookup"><span data-stu-id="12e3f-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="12e3f-113">Name (Имя)</span><span class="sxs-lookup"><span data-stu-id="12e3f-113">Name</span></span> |<span data-ttu-id="12e3f-114">строка</span><span class="sxs-lookup"><span data-stu-id="12e3f-114">string</span></span> |<span data-ttu-id="12e3f-115">Имя свойства.</span><span class="sxs-lookup"><span data-stu-id="12e3f-115">The name of the property.</span></span> <span data-ttu-id="12e3f-116">Может содержать только буквы, цифры, точки, тире и знаки подчеркивания.</span><span class="sxs-lookup"><span data-stu-id="12e3f-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="12e3f-117">Значение</span><span class="sxs-lookup"><span data-stu-id="12e3f-117">Value</span></span> |<span data-ttu-id="12e3f-118">строка</span><span class="sxs-lookup"><span data-stu-id="12e3f-118">string</span></span> |<span data-ttu-id="12e3f-119">Значение свойства.</span><span class="sxs-lookup"><span data-stu-id="12e3f-119">The value of the property.</span></span> <span data-ttu-id="12e3f-120">Не может быть пустым или состоять только из пробелов.</span><span class="sxs-lookup"><span data-stu-id="12e3f-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="12e3f-121">Секрет</span><span class="sxs-lookup"><span data-stu-id="12e3f-121">Secret</span></span> |<span data-ttu-id="12e3f-122">Логическое</span><span class="sxs-lookup"><span data-stu-id="12e3f-122">boolean</span></span> |<span data-ttu-id="12e3f-123">Определяет, является ли значение секретом и должно ли быть зашифровано.</span><span class="sxs-lookup"><span data-stu-id="12e3f-123">Determines whether the value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="12e3f-124">Теги</span><span class="sxs-lookup"><span data-stu-id="12e3f-124">Tags</span></span> |<span data-ttu-id="12e3f-125">Массив строк</span><span class="sxs-lookup"><span data-stu-id="12e3f-125">array of string</span></span> |<span data-ttu-id="12e3f-126">Необязательные теги, которые (если указаны) можно использовать для фильтрации списка свойств.</span><span class="sxs-lookup"><span data-stu-id="12e3f-126">Optional tags that when provided can be used to filter the property list.</span></span> |

<span data-ttu-id="12e3f-127">Свойства настраиваются на портале издателя на вкладке **Свойства** .</span><span class="sxs-lookup"><span data-stu-id="12e3f-127">Properties are configured in the publisher portal on the **Properties** tab.</span></span> <span data-ttu-id="12e3f-128">В приведенном далее примере настраиваются три свойства.</span><span class="sxs-lookup"><span data-stu-id="12e3f-128">In the following example, three properties are configured.</span></span>

![Свойства][api-management-properties]

<span data-ttu-id="12e3f-130">Значения свойств могут содержать строковые литералы и [выражения политики](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span><span class="sxs-lookup"><span data-stu-id="12e3f-130">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="12e3f-131">В приведенной далее таблице приводятся предыдущие три примера свойств и их атрибуты.</span><span class="sxs-lookup"><span data-stu-id="12e3f-131">The following table shows the previous three sample properties and their attributes.</span></span> <span data-ttu-id="12e3f-132">Значение `ExpressionProperty` является выражением политики, которое возвращает строку, содержащую текущую дату и время.</span><span class="sxs-lookup"><span data-stu-id="12e3f-132">The value of `ExpressionProperty` is a policy expression that returns a string containing the current date and time.</span></span> <span data-ttu-id="12e3f-133">Свойство `ContosoHeaderValue` помечено как секрет, поэтому его значение не отображается.</span><span class="sxs-lookup"><span data-stu-id="12e3f-133">The property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="12e3f-134">Name (Имя)</span><span class="sxs-lookup"><span data-stu-id="12e3f-134">Name</span></span> | <span data-ttu-id="12e3f-135">Значение</span><span class="sxs-lookup"><span data-stu-id="12e3f-135">Value</span></span> | <span data-ttu-id="12e3f-136">Секрет</span><span class="sxs-lookup"><span data-stu-id="12e3f-136">Secret</span></span> | <span data-ttu-id="12e3f-137">Теги</span><span class="sxs-lookup"><span data-stu-id="12e3f-137">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="12e3f-138">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="12e3f-138">ContosoHeader</span></span> |<span data-ttu-id="12e3f-139">TrackingId</span><span class="sxs-lookup"><span data-stu-id="12e3f-139">TrackingId</span></span> |<span data-ttu-id="12e3f-140">Ложь</span><span class="sxs-lookup"><span data-stu-id="12e3f-140">False</span></span> |<span data-ttu-id="12e3f-141">Contoso</span><span class="sxs-lookup"><span data-stu-id="12e3f-141">Contoso</span></span> |
| <span data-ttu-id="12e3f-142">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="12e3f-142">ContosoHeaderValue</span></span> |<span data-ttu-id="12e3f-143">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="12e3f-143">••••••••••••••••••••••</span></span> |<span data-ttu-id="12e3f-144">Истина</span><span class="sxs-lookup"><span data-stu-id="12e3f-144">True</span></span> |<span data-ttu-id="12e3f-145">Contoso</span><span class="sxs-lookup"><span data-stu-id="12e3f-145">Contoso</span></span> |
| <span data-ttu-id="12e3f-146">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="12e3f-146">ExpressionProperty</span></span> |<span data-ttu-id="12e3f-147">@(DateTime.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="12e3f-147">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="12e3f-148">Ложь</span><span class="sxs-lookup"><span data-stu-id="12e3f-148">False</span></span> | |

## <a name="to-use-a-property"></a><span data-ttu-id="12e3f-149">Использование свойства</span><span class="sxs-lookup"><span data-stu-id="12e3f-149">To use a property</span></span>
<span data-ttu-id="12e3f-150">Чтобы использовать свойство в политике, поместите имя свойства внутри пары двойных фигурных скобок `{{ContosoHeader}}`, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="12e3f-150">To use a property in a policy, place the property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in the following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="12e3f-151">В этом примере `ContosoHeader` используется как имя заголовка в политике `set-header`, а `ContosoHeaderValue` — в качестве значения этого заголовка.</span><span class="sxs-lookup"><span data-stu-id="12e3f-151">In this example, `ContosoHeader` is used as the name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as the value of that header.</span></span> <span data-ttu-id="12e3f-152">При оценке этой политики во время запроса или ответа к шлюзу управления API `{{ContosoHeader}}` и `{{ContosoHeaderValue}}` заменяются соответствующими значениями свойств.</span><span class="sxs-lookup"><span data-stu-id="12e3f-152">When this policy is evaluated during a request or response to the API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="12e3f-153">Свойства можно использовать как полные значения атрибутов или элементов, как показано в предыдущем примере, но их можно также вставлять в литеральное текстовое выражение или комбинировать с частью этого выражения, как показано в следующем примере: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="12e3f-153">Properties can be used as complete attribute or element values as shown in the previous example, but they can also be inserted into or combined with part of a literal text expression as shown in the following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="12e3f-154">Свойства могут также содержать выражения политики.</span><span class="sxs-lookup"><span data-stu-id="12e3f-154">Properties can also contain policy expressions.</span></span> <span data-ttu-id="12e3f-155">В следующем примере используется `ExpressionProperty` .</span><span class="sxs-lookup"><span data-stu-id="12e3f-155">In the following example, the `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="12e3f-156">При оценке этой политики `{{ExpressionProperty}}` заменяется своим значением: `@(DateTime.Now.ToString())`.</span><span class="sxs-lookup"><span data-stu-id="12e3f-156">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="12e3f-157">Поскольку значение является выражением политики, выражение проходит оценку и политика продолжает выполнение.</span><span class="sxs-lookup"><span data-stu-id="12e3f-157">Since the value is a policy expression, the expression is evaluated and the policy proceeds with its execution.</span></span>

<span data-ttu-id="12e3f-158">Этот момент можно проверить на портале разработчика путем вызова операции, имеющей политику со свойствами.</span><span class="sxs-lookup"><span data-stu-id="12e3f-158">You can test this out in the developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="12e3f-159">В приведенном далее примере вызывается операция с двумя политиками `set-header` со свойствами из предыдущего примера.</span><span class="sxs-lookup"><span data-stu-id="12e3f-159">In the following example, an operation is called with the two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="12e3f-160">Обратите внимание, что ответ содержит два пользовательских заголовка, которые были настроены с помощью политик со свойствами.</span><span class="sxs-lookup"><span data-stu-id="12e3f-160">Note that the response contains two custom headers that were configured using policies with properties.</span></span>

![Портал разработчика][api-management-send-results]

<span data-ttu-id="12e3f-162">Если взглянуть на [трассировку инспектора API](api-management-howto-api-inspector.md) для вызова, который содержит две политики со свойствами из предыдущего примера, можно увидеть две политики `set-header` со вставленными значениями свойств, а также оценку выражения политики для свойства, содержащего выражение политики.</span><span class="sxs-lookup"><span data-stu-id="12e3f-162">If you look at the [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes the two previous sample policies with properties, you can see the two `set-header` policies with the property values inserted as well as the policy expression evaluation for the property that contained the policy expression.</span></span>

![Трассировка с помощью инспектора API][api-management-api-inspector-trace]

<span data-ttu-id="12e3f-164">Обратите внимание, что хотя значения свойств могут содержать выражения политики, они не могут содержать другие свойства.</span><span class="sxs-lookup"><span data-stu-id="12e3f-164">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="12e3f-165">Если текст, содержащий ссылку на свойство, используется для значения свойства, такого как `Property value text {{MyProperty}}`, эта ссылка на свойство не будет заменена и включится в значение свойства.</span><span class="sxs-lookup"><span data-stu-id="12e3f-165">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of the property value.</span></span>

## <a name="to-create-a-property"></a><span data-ttu-id="12e3f-166">Создание свойства</span><span class="sxs-lookup"><span data-stu-id="12e3f-166">To create a property</span></span>
<span data-ttu-id="12e3f-167">Чтобы создать свойство, нажмите кнопку **Добавить свойство** на вкладке **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="12e3f-167">To create a property, click **Add property** on the **Properties** tab.</span></span>

![Добавление свойства][api-management-properties-add-property-menu]

<span data-ttu-id="12e3f-169">Поля **Имя** и **Значение** обязательны для заполнения.</span><span class="sxs-lookup"><span data-stu-id="12e3f-169">**Name** and **Value** are required values.</span></span> <span data-ttu-id="12e3f-170">Если значением свойства является секрет, установите флажок **Это секрет** .</span><span class="sxs-lookup"><span data-stu-id="12e3f-170">If this property value is a secret, check the **This is a secret** checkbox.</span></span> <span data-ttu-id="12e3f-171">Введите один или несколько необязательных тегов, чтобы упорядочить свойства, и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="12e3f-171">Enter one or more optional tags to help with organizing your properties, and click **Save**.</span></span>

![Добавление свойства][api-management-properties-add-property]

<span data-ttu-id="12e3f-173">После сохранения нового свойства в текстовом поле **Свойство поиска** появляется имя нового свойства и отображается новое свойство.</span><span class="sxs-lookup"><span data-stu-id="12e3f-173">When a new property is saved, the **Search property** textbox is populated with the name of the new property and the new property is displayed.</span></span> <span data-ttu-id="12e3f-174">Чтобы отобразить все свойства, очистите поле **Свойство поиска** и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="12e3f-174">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![Свойства][api-management-properties-property-saved]

<span data-ttu-id="12e3f-176">Сведения о создании свойства с помощью REST API см. в [этом разделе](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span><span class="sxs-lookup"><span data-stu-id="12e3f-176">For information on creating a property using the REST API, see [Create a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="to-edit-a-property"></a><span data-ttu-id="12e3f-177">Изменение свойства</span><span class="sxs-lookup"><span data-stu-id="12e3f-177">To edit a property</span></span>
<span data-ttu-id="12e3f-178">Чтобы изменить свойство, щелкните **Изменить** рядом с нужным свойством.</span><span class="sxs-lookup"><span data-stu-id="12e3f-178">To edit a property, click **Edit** beside the property to edit.</span></span>

![Изменение свойства][api-management-properties-edit]

<span data-ttu-id="12e3f-180">Внесите необходимые изменения и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="12e3f-180">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="12e3f-181">Если изменяется имя свойства, все политики, которые ссылаются на это свойство, автоматически обновляются для использования нового имени.</span><span class="sxs-lookup"><span data-stu-id="12e3f-181">If you change the property name, any policies that reference that property are automatically updated to use the new name.</span></span>

![Изменение свойства][api-management-properties-edit-property]

<span data-ttu-id="12e3f-183">Сведения об изменении свойства с помощью REST API см. в [этом разделе](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span><span class="sxs-lookup"><span data-stu-id="12e3f-183">For information on editing a property using the REST API, see [Edit a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="to-delete-a-property"></a><span data-ttu-id="12e3f-184">Удаление свойства</span><span class="sxs-lookup"><span data-stu-id="12e3f-184">To delete a property</span></span>
<span data-ttu-id="12e3f-185">Чтобы удалить свойство, нажмите кнопку **Удалить** рядом с нужным свойством.</span><span class="sxs-lookup"><span data-stu-id="12e3f-185">To delete a property, click **Delete** beside the property to delete.</span></span>

![Изменение свойства][api-management-properties-delete]

<span data-ttu-id="12e3f-187">Чтобы подтвердить действие, нажмите кнопку **Yes, delete it** (Да, удалить).</span><span class="sxs-lookup"><span data-stu-id="12e3f-187">Click **Yes, delete it** to confirm.</span></span>

![Подтверждение удаления][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="12e3f-189">Если на свойство ссылаются какие-либо политики, его можно удалить только после удаления из всех политик, которые его используют.</span><span class="sxs-lookup"><span data-stu-id="12e3f-189">If the property is referenced by any policies, you will be unable to successfully delete it until you remove the property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="12e3f-190">Сведения об удалении свойства с помощью REST API см. в [этом разделе](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span><span class="sxs-lookup"><span data-stu-id="12e3f-190">For information on deleting a property using the REST API, see [Delete a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="to-search-and-filter-properties"></a><span data-ttu-id="12e3f-191">Поиск и фильтрация свойств</span><span class="sxs-lookup"><span data-stu-id="12e3f-191">To search and filter properties</span></span>
<span data-ttu-id="12e3f-192">На вкладке **Свойства** находятся функции поиска и фильтрации, упрощающие управление свойствами.</span><span class="sxs-lookup"><span data-stu-id="12e3f-192">The **Properties** tab includes searching and filtering capabilities to help you manage your properties.</span></span> <span data-ttu-id="12e3f-193">Чтобы отфильтровать список свойств по имени свойства, введите условие поиска в поле **Свойство поиска** .</span><span class="sxs-lookup"><span data-stu-id="12e3f-193">To filter the property list by property name, enter a search term in the **Search property** textbox.</span></span> <span data-ttu-id="12e3f-194">Чтобы отобразить все свойства, очистите поле **Свойство поиска** и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="12e3f-194">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![Поиск][api-management-properties-search]

<span data-ttu-id="12e3f-196">Чтобы отфильтровать список свойств по значениям тегов, введите один или несколько тегов в поле **Фильтровать по тегам** .</span><span class="sxs-lookup"><span data-stu-id="12e3f-196">To filter the property list by tag values, enter one or more tags into the **Filter by tags** textbox.</span></span> <span data-ttu-id="12e3f-197">Чтобы отобразить все свойства, очистите поле **Фильтровать по тегам** и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="12e3f-197">To display all properties, clear the **Filter by tags** textbox and press enter.</span></span>

![Фильтр][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="12e3f-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="12e3f-199">Next steps</span></span>
* <span data-ttu-id="12e3f-200">Узнайте больше о работе с политиками</span><span class="sxs-lookup"><span data-stu-id="12e3f-200">Learn more about working with policies</span></span>
  * [<span data-ttu-id="12e3f-201">Политики в управлении API</span><span class="sxs-lookup"><span data-stu-id="12e3f-201">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="12e3f-202">Справочник по политикам</span><span class="sxs-lookup"><span data-stu-id="12e3f-202">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="12e3f-203">Выражения политики</span><span class="sxs-lookup"><span data-stu-id="12e3f-203">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="12e3f-204">Просмотр видеообзора</span><span class="sxs-lookup"><span data-stu-id="12e3f-204">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Use-Properties-in-Policies/player]
> 
> 

[api-management-properties]: ./media/api-management-howto-properties/api-management-properties.png
[api-management-properties-add-property]: ./media/api-management-howto-properties/api-management-properties-add-property.png
[api-management-properties-edit-property]: ./media/api-management-howto-properties/api-management-properties-edit-property.png
[api-management-properties-add-property-menu]: ./media/api-management-howto-properties/api-management-properties-add-property-menu.png
[api-management-properties-property-saved]: ./media/api-management-howto-properties/api-management-properties-property-saved.png
[api-management-properties-delete]: ./media/api-management-howto-properties/api-management-properties-delete.png
[api-management-properties-edit]: ./media/api-management-howto-properties/api-management-properties-edit.png
[api-management-delete-confirm]: ./media/api-management-howto-properties/api-management-delete-confirm.png
[api-management-properties-search]: ./media/api-management-howto-properties/api-management-properties-search.png
[api-management-send-results]: ./media/api-management-howto-properties/api-management-send-results.png
[api-management-properties-filter]: ./media/api-management-howto-properties/api-management-properties-filter.png
[api-management-api-inspector-trace]: ./media/api-management-howto-properties/api-management-api-inspector-trace.png

