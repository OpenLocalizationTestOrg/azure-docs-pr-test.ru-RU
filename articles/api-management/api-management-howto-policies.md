---
title: "Политики в службе управления API Azure | Документация Майкрософт"
description: "Сведения о создании, изменении и настройке политик в службе управления API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 537e5caf-708b-430e-a83f-72b70af28aa9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7c1f235343074ec11c635097f2b094a10f3fe781
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="17463-103">Политики в Azure API Management</span><span class="sxs-lookup"><span data-stu-id="17463-103">Policies in Azure API Management</span></span>
<span data-ttu-id="17463-104">В службе управления API Azure политики представляют собой одну из эффективных функций системы, позволяющих издателю изменять поведение интерфейса API путем его настройки.</span><span class="sxs-lookup"><span data-stu-id="17463-104">In Azure API Management, policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="17463-105">Политика — это коллекция операторов, которые выполняются последовательно по запросу интерфейса API или при получении из него ответа.</span><span class="sxs-lookup"><span data-stu-id="17463-105">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="17463-106">К часто используемым операторам относятся преобразование формата из XML в JSON, а также ограничение скорости вызовов, позволяющее ограничивать количество входящих вызовов от разработчика.</span><span class="sxs-lookup"><span data-stu-id="17463-106">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="17463-107">Также существует много готовых политик.</span><span class="sxs-lookup"><span data-stu-id="17463-107">Many more policies are available out of the box.</span></span>

<span data-ttu-id="17463-108">Полный перечень операторов политик и их параметров см. в [справочнике по политикам][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="17463-108">See the [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="17463-109">Политики применяются внутри шлюза, который находится между потребителем интерфейса API и управляемым API.</span><span class="sxs-lookup"><span data-stu-id="17463-109">Policies are applied inside the gateway which sits between the API consumer and the managed API.</span></span> <span data-ttu-id="17463-110">Шлюз получает все запросы и обычно отправляет их без изменения в базовый API.</span><span class="sxs-lookup"><span data-stu-id="17463-110">The gateway receives all requests and usually forwards them unaltered to the underlying API.</span></span> <span data-ttu-id="17463-111">Однако политика может применять изменения как для входящего запроса, так и для исходящего ответа.</span><span class="sxs-lookup"><span data-stu-id="17463-111">However a policy can apply changes to both the inbound request and outbound response.</span></span>

<span data-ttu-id="17463-112">Выражения политики можно использовать в качестве значений атрибутов или текстовых значений в любой политике управления API, если в ней не указано иное.</span><span class="sxs-lookup"><span data-stu-id="17463-112">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="17463-113">Некоторые политики (включая [Поток управления][Control flow] и [Задание переменной][Set variable]) основаны на выражениях политики.</span><span class="sxs-lookup"><span data-stu-id="17463-113">Some policies such as the [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="17463-114">Чтобы узнать больше, ознакомьтесь с [расширенными политиками][Advanced policies] и [выражениями политики][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="17463-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="17463-115"><a name="scopes"> </a>Как настраивать политики</span><span class="sxs-lookup"><span data-stu-id="17463-115"><a name="scopes"> </a>How to configure policies</span></span>
<span data-ttu-id="17463-116">Политики можно настраивать глобально или на уровне [продукта][Product], [API][API] или [операции][Operation].</span><span class="sxs-lookup"><span data-stu-id="17463-116">Policies can be configured globally or at the scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="17463-117">Для настройки политики перейдите в редактор политик на портале издателя.</span><span class="sxs-lookup"><span data-stu-id="17463-117">To configure a policy, navigate to the Policies editor in the publisher portal.</span></span>

![Меню «Политики»][policies-menu]

<span data-ttu-id="17463-119">Редактор политик состоит из трех основных разделов: область политики (сверху), определение политики, где политики можно редактировать, (слева) и список операторов (справа):</span><span class="sxs-lookup"><span data-stu-id="17463-119">The policies editor consists of three main sections: the policy scope (top), the policy definition where policies are edited (left) and the statements list (right):</span></span>

![Редактор политик][policies-editor]

<span data-ttu-id="17463-121">Чтобы начать процесс настройки политики, необходимо сначала выбрать область, в которой эта политика должна применяться.</span><span class="sxs-lookup"><span data-stu-id="17463-121">To begin configuring a policy you must first select the scope at which the policy should apply.</span></span> <span data-ttu-id="17463-122">На снимке экрана ниже выбран продукт **Starter** .</span><span class="sxs-lookup"><span data-stu-id="17463-122">In the screenshot below the **Starter** product is selected.</span></span> <span data-ttu-id="17463-123">Следует отметить, что символ квадрата рядом с именем политики указывает, что политика уже применена на этом уровне.</span><span class="sxs-lookup"><span data-stu-id="17463-123">Note that the square symbol next to the policy name indicates that a policy is already applied at this level.</span></span>

![Область][policies-scope]

<span data-ttu-id="17463-125">Так как политика уже применена, конфигурация показана в виде определения.</span><span class="sxs-lookup"><span data-stu-id="17463-125">Since a policy has already been applied, the configuration is shown in the definition view.</span></span>

![Настройка][policies-configure]

<span data-ttu-id="17463-127">Сначала политика отображается в режиме «только для чтения».</span><span class="sxs-lookup"><span data-stu-id="17463-127">The policy is displayed read-only at first.</span></span> <span data-ttu-id="17463-128">Чтобы изменить определение, щелкните действие **Настроить политику** .</span><span class="sxs-lookup"><span data-stu-id="17463-128">In order to edit the definition click the **Configure Policy** action.</span></span>

![Редактирование][policies-edit]

<span data-ttu-id="17463-130">Определение политики представляет собой простой XML-документ, который описывает последовательность входящих и исходящих операторов.</span><span class="sxs-lookup"><span data-stu-id="17463-130">The policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="17463-131">Файл XML можно редактировать прямо в окне определения.</span><span class="sxs-lookup"><span data-stu-id="17463-131">The XML can be edited directly in the definition window.</span></span> <span data-ttu-id="17463-132">Перечень операторов отображается справа, а операторы, применимые к текущей области, включены и выделены (как показано в примере **Ограничить скорость вызовов** на снимке экрана выше).</span><span class="sxs-lookup"><span data-stu-id="17463-132">A list of statements is provided to the right and statements applicable to the current scope are enabled and highlighted; as demonstrated by the **Limit Call Rate** statement in the screenshot above.</span></span>

<span data-ttu-id="17463-133">При щелчке разрешенного оператора будет добавлен соответствующий XML-код в местоположении курсора в виде определения.</span><span class="sxs-lookup"><span data-stu-id="17463-133">Clicking an enabled statement will add the appropriate XML at the location of the cursor in the definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="17463-134">Если политика, которую требуется добавить, не включена, убедитесь, что вы находитесь в правильной области действия этой политики.</span><span class="sxs-lookup"><span data-stu-id="17463-134">If the policy that you want to add is not enabled, ensure that you are in the correct scope for that policy.</span></span> <span data-ttu-id="17463-135">Каждая инструкция политики предназначена для использования в определенных областях и разделах политики.</span><span class="sxs-lookup"><span data-stu-id="17463-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="17463-136">Чтобы просмотреть разделы политики и области ее действия, ознакомьтесь с разделом **Использование** для этой политики в [справочнике по политикам][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="17463-136">To review the policy sections and scopes for a policy, check the **Usage** section for that policy in the [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="17463-137">Полный перечень операторов политик и их параметров см. в [справочнике по политикам][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="17463-137">A full list of policy statements and their settings are available in the [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="17463-138">Например, для добавления нового оператора с целью ограничения входящих запросов на указанные IP-адреса поместите курсор внутрь XML-элемента `inbound` и щелкните оператор **Ограничить IP-адреса вызывающего объекта** .</span><span class="sxs-lookup"><span data-stu-id="17463-138">For example, to add a new statement to restrict incoming requests to specified IP addresses, place the cursor just inside the content of the `inbound` XML element and click the **Restrict caller IPs** statement.</span></span>

![Политики ограничения][policies-restrict]

<span data-ttu-id="17463-140">При этом будет добавлен фрагмент XML-кода в элемент `inbound` , который будет содержать указания о том, как настроить оператор.</span><span class="sxs-lookup"><span data-stu-id="17463-140">This will add an XML snippet to the `inbound` element that provides guidance on how to configure the statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="17463-141">Для ограничения входящих запросов и принятия только тех запросов, которые поступают с IP-адреса 1.2.3.4, измените XML-код следующим образом:</span><span class="sxs-lookup"><span data-stu-id="17463-141">To limit inbound requests and accept only those from an IP address of 1.2.3.4 modify the XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Сохранить][policies-save]

<span data-ttu-id="17463-143">По окончании процесса настройки операторов для политики щелкните **Сохранить** , и изменения будут немедленно распространены на шлюз управления API.</span><span class="sxs-lookup"><span data-stu-id="17463-143">When complete configuring the statements for the policy, click **Save** and the changes will be propagated to the API Management gateway immediately.</span></span>

## <span data-ttu-id="17463-144"><a name="sections"> </a>Общая информация о конфигурации политики</span><span class="sxs-lookup"><span data-stu-id="17463-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="17463-145">Политика — это набор операторов, которые выполняются для создания запроса и получения ответа.</span><span class="sxs-lookup"><span data-stu-id="17463-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="17463-146">Конфигурация делится соответствующим образом на разделы `inbound`, `backend`, `outbound` и `on-error`, как показано в следующей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="17463-146">The configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in the following configuration.</span></span>

```xml
<policies>
  <inbound>
    <!-- statements to be applied to the request go here -->
  </inbound>
  <backend>
    <!-- statements to be applied before the request is forwarded to 
         the backend service go here -->
  </backend>
  <outbound>
    <!-- statements to be applied to the response go here -->
  </outbound>
  <on-error>
    <!-- statements to be applied if there is an error condition go here -->
  </on-error>
</policies> 
```

<span data-ttu-id="17463-147">Если во время обработки запроса произошла ошибка, все оставшиеся действия в разделах `inbound`, `backend` или `outbound` пропускаются, и начинают выполняться операторы из раздела `on-error`.</span><span class="sxs-lookup"><span data-stu-id="17463-147">If there is an error during the processing of a request, any remaining steps in the `inbound`, `backend`, or `outbound` sections are skipped and execution jumps to the statements in the `on-error` section.</span></span> <span data-ttu-id="17463-148">Поместив операторы политики в раздел `on-error`, вы можете просмотреть ошибку с помощью свойства `context.LastError`, изучить и настроить ответ на ошибку с помощью политики `set-body`, а также настроить, что именно происходит при возникновении ошибки.</span><span class="sxs-lookup"><span data-stu-id="17463-148">By placing policy statements in the `on-error` section you can review the error by using the `context.LastError` property, inspect and customize the error response using the `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="17463-149">Существуют коды ошибок для встроенных действий и для ошибок, которые могут возникать во время обработки оператора политики.</span><span class="sxs-lookup"><span data-stu-id="17463-149">There are error codes for built-in steps and for errors that may occur during the processing of policy statements.</span></span> <span data-ttu-id="17463-150">Дополнительные сведения см. в статье [Обработка ошибок в политиках управления API](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span><span class="sxs-lookup"><span data-stu-id="17463-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="17463-151">Так как политики могут быть указаны на разных уровнях (глобальном, продукта, API и операции), конфигурация позволяет указать порядок, в котором операторы определения политики будут выполняться применительно к родительской политике.</span><span class="sxs-lookup"><span data-stu-id="17463-151">Since policies can be specified at different levels (global, product, api and operation) the configuration provides a way for you to specify the order in which the policy definition's statements execute with respect to the parent policy.</span></span> 

<span data-ttu-id="17463-152">Области политики вычисляются в следующем порядке.</span><span class="sxs-lookup"><span data-stu-id="17463-152">Policy scopes are evaluated in the following order.</span></span>

1. <span data-ttu-id="17463-153">Глобальная область</span><span class="sxs-lookup"><span data-stu-id="17463-153">Global scope</span></span>
2. <span data-ttu-id="17463-154">Область продукта</span><span class="sxs-lookup"><span data-stu-id="17463-154">Product scope</span></span>
3. <span data-ttu-id="17463-155">Область API</span><span class="sxs-lookup"><span data-stu-id="17463-155">API scope</span></span>
4. <span data-ttu-id="17463-156">Область операций</span><span class="sxs-lookup"><span data-stu-id="17463-156">Operation scope</span></span>

<span data-ttu-id="17463-157">Операторы внутри них вычисляются с учетом размещения элемента `base` при его наличии.</span><span class="sxs-lookup"><span data-stu-id="17463-157">The statements within them are evaluated according to the placement of the `base` element, if it is present.</span></span> <span data-ttu-id="17463-158">Для глобальной политики не существует родительской политики, поэтому использовать в ней элемент `<base>` бесполезно.</span><span class="sxs-lookup"><span data-stu-id="17463-158">Global policy has no parent policy and using the `<base>` element in it has no effect.</span></span>

<span data-ttu-id="17463-159">Например, если у вас есть политика на глобальном уровне и политика, настроенная для API, то при каждом использовании этого API будут применяться обе политики.</span><span class="sxs-lookup"><span data-stu-id="17463-159">For example, if you have a policy at the global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="17463-160">API Management позволяет детерминированным образом упорядочивать объединенные операторы политик через основной элемент.</span><span class="sxs-lookup"><span data-stu-id="17463-160">API Management allows for deterministic ordering of combined policy statements via the base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="17463-161">В примере определения политики, приведенном выше, оператор `cross-domain` будет выполняться перед любыми более высокими политиками, после которых, в свою очередь, будет следовать политика `find-and-replace`.</span><span class="sxs-lookup"><span data-stu-id="17463-161">In the example policy definition above, the `cross-domain` statement would execute before any higher policies which would in turn, be followed by the `find-and-replace` policy.</span></span> 

<span data-ttu-id="17463-162">Чтобы просмотреть политики в текущей области в редакторе политик, щелкните **Recalculate effective policy for selected scope**(Пересчитать эффективную политику для выбранной области).</span><span class="sxs-lookup"><span data-stu-id="17463-162">To see the policies in the current scope in the policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17463-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="17463-163">Next steps</span></span>
<span data-ttu-id="17463-164">Посмотрите следующие видео о выражениях политики.</span><span class="sxs-lookup"><span data-stu-id="17463-164">Check out following video on policy expressions.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Policy Reference]: api-management-policy-reference.md
[Product]: api-management-howto-add-products.md
[API]: api-management-howto-add-products.md#add-apis 
[Operation]: api-management-howto-add-operations.md

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx

[policies-menu]: ./media/api-management-howto-policies/api-management-policies-menu.png
[policies-editor]: ./media/api-management-howto-policies/api-management-policies-editor.png
[policies-scope]: ./media/api-management-howto-policies/api-management-policies-scope.png
[policies-configure]: ./media/api-management-howto-policies/api-management-policies-configure.png
[policies-edit]: ./media/api-management-howto-policies/api-management-policies-edit.png
[policies-restrict]: ./media/api-management-howto-policies/api-management-policies-restrict.png
[policies-save]: ./media/api-management-howto-policies/api-management-policies-save.png
