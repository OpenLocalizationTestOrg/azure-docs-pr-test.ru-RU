---
title: "свойства toouse aaaHow в политики управления API Azure"
description: "Узнайте, как toouse свойств политики управления API Azure."
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
ms.openlocfilehash: 1ff096deeb97543b48dcf1f40be9dbfcbcd09542
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-properties-in-azure-api-management-policies"></a><span data-ttu-id="f9e71-103">Как toouse свойств политики управления API Azure</span><span class="sxs-lookup"><span data-stu-id="f9e71-103">How toouse properties in Azure API Management policies</span></span>
<span data-ttu-id="f9e71-104">Политики управления API — это мощная возможность системы hello, разрешить издателю hello поведение hello toochange hello API через конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="f9e71-104">API Management policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="f9e71-105">Политики представляют собой набор инструкций, которые выполняются последовательно, по запросу hello или ответу API-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="f9e71-105">Policies are a collection of statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="f9e71-106">Для создания правил политики можно использовать литеральные текстовые значения, выражения политики и свойства.</span><span class="sxs-lookup"><span data-stu-id="f9e71-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="f9e71-107">Каждый экземпляр службы управления API имеет свойства коллекцию пар "ключ значение", содержащихся toohello глобальный экземпляр службы.</span><span class="sxs-lookup"><span data-stu-id="f9e71-107">Each API Management service instance has a properties collection of key/value pairs that are global toohello service instance.</span></span> <span data-ttu-id="f9e71-108">Эти свойства можно использовать toomanage постоянные строковые значения для всех API конфигурации и политики.</span><span class="sxs-lookup"><span data-stu-id="f9e71-108">These properties can be used toomanage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="f9e71-109">Каждое свойство имеет следующие атрибуты hello.</span><span class="sxs-lookup"><span data-stu-id="f9e71-109">Each property has hello following attributes.</span></span>

| <span data-ttu-id="f9e71-110">Атрибут</span><span class="sxs-lookup"><span data-stu-id="f9e71-110">Attribute</span></span> | <span data-ttu-id="f9e71-111">Тип</span><span class="sxs-lookup"><span data-stu-id="f9e71-111">Type</span></span> | <span data-ttu-id="f9e71-112">Описание</span><span class="sxs-lookup"><span data-stu-id="f9e71-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f9e71-113">Name (Имя)</span><span class="sxs-lookup"><span data-stu-id="f9e71-113">Name</span></span> |<span data-ttu-id="f9e71-114">string</span><span class="sxs-lookup"><span data-stu-id="f9e71-114">string</span></span> |<span data-ttu-id="f9e71-115">Имя свойства hello Hello.</span><span class="sxs-lookup"><span data-stu-id="f9e71-115">hello name of hello property.</span></span> <span data-ttu-id="f9e71-116">Может содержать только буквы, цифры, точки, тире и знаки подчеркивания.</span><span class="sxs-lookup"><span data-stu-id="f9e71-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="f9e71-117">Значение</span><span class="sxs-lookup"><span data-stu-id="f9e71-117">Value</span></span> |<span data-ttu-id="f9e71-118">string</span><span class="sxs-lookup"><span data-stu-id="f9e71-118">string</span></span> |<span data-ttu-id="f9e71-119">значение свойства hello Hello.</span><span class="sxs-lookup"><span data-stu-id="f9e71-119">hello value of hello property.</span></span> <span data-ttu-id="f9e71-120">Не может быть пустым или состоять только из пробелов.</span><span class="sxs-lookup"><span data-stu-id="f9e71-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="f9e71-121">Секрет</span><span class="sxs-lookup"><span data-stu-id="f9e71-121">Secret</span></span> |<span data-ttu-id="f9e71-122">Логическое</span><span class="sxs-lookup"><span data-stu-id="f9e71-122">boolean</span></span> |<span data-ttu-id="f9e71-123">Определяет, является ли значение hello секрета и должны быть зашифрованы или нет.</span><span class="sxs-lookup"><span data-stu-id="f9e71-123">Determines whether hello value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="f9e71-124">Теги</span><span class="sxs-lookup"><span data-stu-id="f9e71-124">Tags</span></span> |<span data-ttu-id="f9e71-125">Массив строк</span><span class="sxs-lookup"><span data-stu-id="f9e71-125">array of string</span></span> |<span data-ttu-id="f9e71-126">Необязательный теги, если может быть список свойств используется toofilter hello.</span><span class="sxs-lookup"><span data-stu-id="f9e71-126">Optional tags that when provided can be used toofilter hello property list.</span></span> |

<span data-ttu-id="f9e71-127">Свойства настраиваются на портале издателю hello hello **свойства** вкладки. В следующем примере hello настраиваются три свойства.</span><span class="sxs-lookup"><span data-stu-id="f9e71-127">Properties are configured in hello publisher portal on hello **Properties** tab. In hello following example, three properties are configured.</span></span>

![Свойства][api-management-properties]

<span data-ttu-id="f9e71-129">Значения свойств могут содержать строковые литералы и [выражения политики](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span><span class="sxs-lookup"><span data-stu-id="f9e71-129">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="f9e71-130">Hello следующей таблице показаны hello предыдущие три свойства и их атрибуты.</span><span class="sxs-lookup"><span data-stu-id="f9e71-130">hello following table shows hello previous three sample properties and their attributes.</span></span> <span data-ttu-id="f9e71-131">Здравствуйте, значение `ExpressionProperty` является hello политики выражение, которое возвращает строку, содержащую текущую дату и время.</span><span class="sxs-lookup"><span data-stu-id="f9e71-131">hello value of `ExpressionProperty` is a policy expression that returns a string containing hello current date and time.</span></span> <span data-ttu-id="f9e71-132">Здравствуйте, свойство `ContosoHeaderValue` помечен как секретного кода, поэтому его значение не отображается.</span><span class="sxs-lookup"><span data-stu-id="f9e71-132">hello property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="f9e71-133">Имя</span><span class="sxs-lookup"><span data-stu-id="f9e71-133">Name</span></span> | <span data-ttu-id="f9e71-134">Значение</span><span class="sxs-lookup"><span data-stu-id="f9e71-134">Value</span></span> | <span data-ttu-id="f9e71-135">Секрет</span><span class="sxs-lookup"><span data-stu-id="f9e71-135">Secret</span></span> | <span data-ttu-id="f9e71-136">Теги</span><span class="sxs-lookup"><span data-stu-id="f9e71-136">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f9e71-137">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="f9e71-137">ContosoHeader</span></span> |<span data-ttu-id="f9e71-138">TrackingId</span><span class="sxs-lookup"><span data-stu-id="f9e71-138">TrackingId</span></span> |<span data-ttu-id="f9e71-139">Ложь</span><span class="sxs-lookup"><span data-stu-id="f9e71-139">False</span></span> |<span data-ttu-id="f9e71-140">Contoso</span><span class="sxs-lookup"><span data-stu-id="f9e71-140">Contoso</span></span> |
| <span data-ttu-id="f9e71-141">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="f9e71-141">ContosoHeaderValue</span></span> |<span data-ttu-id="f9e71-142">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="f9e71-142">••••••••••••••••••••••</span></span> |<span data-ttu-id="f9e71-143">Истина</span><span class="sxs-lookup"><span data-stu-id="f9e71-143">True</span></span> |<span data-ttu-id="f9e71-144">Contoso</span><span class="sxs-lookup"><span data-stu-id="f9e71-144">Contoso</span></span> |
| <span data-ttu-id="f9e71-145">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="f9e71-145">ExpressionProperty</span></span> |<span data-ttu-id="f9e71-146">@(DateTime.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="f9e71-146">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="f9e71-147">Ложь</span><span class="sxs-lookup"><span data-stu-id="f9e71-147">False</span></span> | |

## <a name="toouse-a-property"></a><span data-ttu-id="f9e71-148">Свойство toouse</span><span class="sxs-lookup"><span data-stu-id="f9e71-148">toouse a property</span></span>
<span data-ttu-id="f9e71-149">Имя свойства hello месте внутри пары двойных фигурных скобок toouse свойства в политике, например `{{ContosoHeader}}`, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="f9e71-149">toouse a property in a policy, place hello property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in hello following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="f9e71-150">В этом примере `ContosoHeader` используется как hello имя заголовка в `set-header` политики, и `ContosoHeaderValue` используется в качестве hello значение этого заголовка.</span><span class="sxs-lookup"><span data-stu-id="f9e71-150">In this example, `ContosoHeader` is used as hello name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as hello value of that header.</span></span> <span data-ttu-id="f9e71-151">Если эта политика вычисляется во время запроса или ответа toohello API управления шлюзом, `{{ContosoHeader}}` и `{{ContosoHeaderValue}}` будут заменены соответствующими значениями свойств.</span><span class="sxs-lookup"><span data-stu-id="f9e71-151">When this policy is evaluated during a request or response toohello API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="f9e71-152">Свойства можно использовать как полный атрибут или элемент значения, как показано в предыдущем примере hello, но они также быть вставлена или вместе с частью выражения литеральный текст, как показано в следующий пример hello:`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="f9e71-152">Properties can be used as complete attribute or element values as shown in hello previous example, but they can also be inserted into or combined with part of a literal text expression as shown in hello following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="f9e71-153">Свойства могут также содержать выражения политики.</span><span class="sxs-lookup"><span data-stu-id="f9e71-153">Properties can also contain policy expressions.</span></span> <span data-ttu-id="f9e71-154">В следующем примере hello, hello `ExpressionProperty` используется.</span><span class="sxs-lookup"><span data-stu-id="f9e71-154">In hello following example, hello `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="f9e71-155">При оценке этой политики `{{ExpressionProperty}}` заменяется своим значением: `@(DateTime.Now.ToString())`.</span><span class="sxs-lookup"><span data-stu-id="f9e71-155">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="f9e71-156">Поскольку значение hello выражения политики, вычисляется выражение hello и hello политики продолжается с его выполнением.</span><span class="sxs-lookup"><span data-stu-id="f9e71-156">Since hello value is a policy expression, hello expression is evaluated and hello policy proceeds with its execution.</span></span>

<span data-ttu-id="f9e71-157">Эту возможность можно проверить на портале разработчиков hello, вызвав операцию, которая имеет политику со свойствами в области.</span><span class="sxs-lookup"><span data-stu-id="f9e71-157">You can test this out in hello developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="f9e71-158">В следующем примере hello, эта операция называется hello два предыдущих примера `set-header` политики со свойствами.</span><span class="sxs-lookup"><span data-stu-id="f9e71-158">In hello following example, an operation is called with hello two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="f9e71-159">Обратите внимание, что ответ hello содержит два пользовательские заголовки, которые были настроены с помощью политик со свойствами.</span><span class="sxs-lookup"><span data-stu-id="f9e71-159">Note that hello response contains two custom headers that were configured using policies with properties.</span></span>

![Портал разработчика][api-management-send-results]

<span data-ttu-id="f9e71-161">Если взглянуть на hello [трассировки API инспектора](api-management-howto-api-inspector.md) для вызова, включающую hello два предыдущих примера политики со свойствами, можно увидеть два hello `set-header` политики со значениями свойств hello, вставки, а также выражение политики hello оценки для hello свойства, которое содержит выражение политики hello.</span><span class="sxs-lookup"><span data-stu-id="f9e71-161">If you look at hello [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes hello two previous sample policies with properties, you can see hello two `set-header` policies with hello property values inserted as well as hello policy expression evaluation for hello property that contained hello policy expression.</span></span>

![Трассировка с помощью инспектора API][api-management-api-inspector-trace]

<span data-ttu-id="f9e71-163">Обратите внимание, что хотя значения свойств могут содержать выражения политики, они не могут содержать другие свойства.</span><span class="sxs-lookup"><span data-stu-id="f9e71-163">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="f9e71-164">Если текст, содержащий ссылку на свойство используется для значения свойства, такие как `Property value text {{MyProperty}}`, что ссылку на свойство не будет заменена и будут включены в значение свойства hello.</span><span class="sxs-lookup"><span data-stu-id="f9e71-164">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of hello property value.</span></span>

## <a name="toocreate-a-property"></a><span data-ttu-id="f9e71-165">Свойство toocreate</span><span class="sxs-lookup"><span data-stu-id="f9e71-165">toocreate a property</span></span>
<span data-ttu-id="f9e71-166">toocreate свойство, нажмите кнопку **добавить свойство** на hello **свойства** вкладки.</span><span class="sxs-lookup"><span data-stu-id="f9e71-166">toocreate a property, click **Add property** on hello **Properties** tab.</span></span>

![Добавление свойства][api-management-properties-add-property-menu]

<span data-ttu-id="f9e71-168">Поля **Имя** и **Значение** обязательны для заполнения.</span><span class="sxs-lookup"><span data-stu-id="f9e71-168">**Name** and **Value** are required values.</span></span> <span data-ttu-id="f9e71-169">Если это свойство имеет значение секрета, проверьте hello **это секрет** флажок.</span><span class="sxs-lookup"><span data-stu-id="f9e71-169">If this property value is a secret, check hello **This is a secret** checkbox.</span></span> <span data-ttu-id="f9e71-170">Введите один или несколько необязательных тегов toohelp с упорядочение свои свойства и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f9e71-170">Enter one or more optional tags toohelp with organizing your properties, and click **Save**.</span></span>

![Добавление свойства][api-management-properties-add-property]

<span data-ttu-id="f9e71-172">При сохранении нового свойства hello **свойства поиска** текстовое поле заполняется hello имя нового свойства hello и отображается новое свойство hello.</span><span class="sxs-lookup"><span data-stu-id="f9e71-172">When a new property is saved, hello **Search property** textbox is populated with hello name of hello new property and hello new property is displayed.</span></span> <span data-ttu-id="f9e71-173">Очистить все свойства toodisplay hello **свойства поиска** текстовое поле и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="f9e71-173">toodisplay all properties, clear hello **Search property** textbox and press enter.</span></span>

![Свойства][api-management-properties-property-saved]

<span data-ttu-id="f9e71-175">Сведения о создании свойства с помощью hello REST API см. в разделе [создавать свойства с помощью API-интерфейса REST hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span><span class="sxs-lookup"><span data-stu-id="f9e71-175">For information on creating a property using hello REST API, see [Create a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="tooedit-a-property"></a><span data-ttu-id="f9e71-176">Свойство tooedit</span><span class="sxs-lookup"><span data-stu-id="f9e71-176">tooedit a property</span></span>
<span data-ttu-id="f9e71-177">tooedit свойство, нажмите кнопку **изменить** рядом с tooedit свойство hello.</span><span class="sxs-lookup"><span data-stu-id="f9e71-177">tooedit a property, click **Edit** beside hello property tooedit.</span></span>

![Изменение свойства][api-management-properties-edit]

<span data-ttu-id="f9e71-179">Внесите необходимые изменения и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f9e71-179">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="f9e71-180">Если изменить имя свойства hello, все политики, которые ссылаются на это свойство, автоматически обновляются toouse hello новое имя.</span><span class="sxs-lookup"><span data-stu-id="f9e71-180">If you change hello property name, any policies that reference that property are automatically updated toouse hello new name.</span></span>

![Изменение свойства][api-management-properties-edit-property]

<span data-ttu-id="f9e71-182">Сведения об изменении свойства с помощью API-интерфейса REST hello. в разделе [изменить свойства с помощью API-интерфейса REST hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span><span class="sxs-lookup"><span data-stu-id="f9e71-182">For information on editing a property using hello REST API, see [Edit a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="toodelete-a-property"></a><span data-ttu-id="f9e71-183">Свойство toodelete</span><span class="sxs-lookup"><span data-stu-id="f9e71-183">toodelete a property</span></span>
<span data-ttu-id="f9e71-184">toodelete свойство, нажмите кнопку **удалить** рядом с toodelete свойство hello.</span><span class="sxs-lookup"><span data-stu-id="f9e71-184">toodelete a property, click **Delete** beside hello property toodelete.</span></span>

![Изменение свойства][api-management-properties-delete]

<span data-ttu-id="f9e71-186">Нажмите кнопку **Да, удалите его** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="f9e71-186">Click **Yes, delete it** tooconfirm.</span></span>

![Подтверждение удаления][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="f9e71-188">Если свойство hello ссылается на какие-либо политики, будут недоступны toosuccessfully удалить его, пока вы не удалите hello свойств всех политик, которые его используют.</span><span class="sxs-lookup"><span data-stu-id="f9e71-188">If hello property is referenced by any policies, you will be unable toosuccessfully delete it until you remove hello property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="f9e71-189">Сведения об удалении свойства с помощью API-интерфейса REST hello. в разделе [удалить свойство, с помощью API-интерфейса REST hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span><span class="sxs-lookup"><span data-stu-id="f9e71-189">For information on deleting a property using hello REST API, see [Delete a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="toosearch-and-filter-properties"></a><span data-ttu-id="f9e71-190">свойства toosearch и фильтр</span><span class="sxs-lookup"><span data-stu-id="f9e71-190">toosearch and filter properties</span></span>
<span data-ttu-id="f9e71-191">Hello **свойства** вкладку включает в себя поиск и фильтрация toohelp возможности управлять свои свойства.</span><span class="sxs-lookup"><span data-stu-id="f9e71-191">hello **Properties** tab includes searching and filtering capabilities toohelp you manage your properties.</span></span> <span data-ttu-id="f9e71-192">Список свойств hello toofilter по имени свойства, введите условие поиска в hello **свойства поиска** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="f9e71-192">toofilter hello property list by property name, enter a search term in hello **Search property** textbox.</span></span> <span data-ttu-id="f9e71-193">Очистить все свойства toodisplay hello **свойства поиска** текстовое поле и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="f9e71-193">toodisplay all properties, clear hello **Search property** textbox and press enter.</span></span>

![Поиск][api-management-properties-search]

<span data-ttu-id="f9e71-195">Список свойств hello toofilter значениями tag, введите один или несколько тегов в hello **фильтрации по тегам** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="f9e71-195">toofilter hello property list by tag values, enter one or more tags into hello **Filter by tags** textbox.</span></span> <span data-ttu-id="f9e71-196">Очистить все свойства toodisplay hello **фильтрации по тегам** текстовое поле и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="f9e71-196">toodisplay all properties, clear hello **Filter by tags** textbox and press enter.</span></span>

![Фильтр][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="f9e71-198">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f9e71-198">Next steps</span></span>
* <span data-ttu-id="f9e71-199">Узнайте больше о работе с политиками</span><span class="sxs-lookup"><span data-stu-id="f9e71-199">Learn more about working with policies</span></span>
  * [<span data-ttu-id="f9e71-200">Политики в управлении API</span><span class="sxs-lookup"><span data-stu-id="f9e71-200">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="f9e71-201">Справочник по политикам</span><span class="sxs-lookup"><span data-stu-id="f9e71-201">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="f9e71-202">Выражения политики</span><span class="sxs-lookup"><span data-stu-id="f9e71-202">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="f9e71-203">Просмотр видеообзора</span><span class="sxs-lookup"><span data-stu-id="f9e71-203">Watch a video overview</span></span>
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

