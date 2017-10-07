---
title: "aaaPolicies в службе управления API Azure | Документы Microsoft"
description: "Узнайте, как toocreate, изменить и настроить политики в службе управления API."
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
ms.openlocfilehash: 9ab0f884a655004cb10c05085034df1795f512e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="0345e-103">Политики в Azure API Management</span><span class="sxs-lookup"><span data-stu-id="0345e-103">Policies in Azure API Management</span></span>
<span data-ttu-id="0345e-104">В Azure API Management политик — это мощная возможность системы hello, разрешить издателю hello поведение hello toochange hello API через конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="0345e-104">In Azure API Management, policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="0345e-105">Политики представляют собой набор инструкций, которые выполняются последовательно, по запросу hello или ответу API-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="0345e-105">Policies are a collection of Statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="0345e-106">Среди наиболее популярных инструкций вспомнить преобразование формата XML tooJSON и toorestrict hello объема входящих вызовов от разработчика ограничение частоты вызовов.</span><span class="sxs-lookup"><span data-stu-id="0345e-106">Popular Statements include format conversion from XML tooJSON and call rate limiting toorestrict hello amount of incoming calls from a developer.</span></span> <span data-ttu-id="0345e-107">Стандартной hello доступны многие дополнительные политики.</span><span class="sxs-lookup"><span data-stu-id="0345e-107">Many more policies are available out of hello box.</span></span>

<span data-ttu-id="0345e-108">В разделе hello [ссылка на политику] [ Policy Reference] полный список инструкций политики и их параметры.</span><span class="sxs-lookup"><span data-stu-id="0345e-108">See hello [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="0345e-109">Политики применяются внутри hello шлюза, который располагается между потребителя API hello и hello управляемых API.</span><span class="sxs-lookup"><span data-stu-id="0345e-109">Policies are applied inside hello gateway which sits between hello API consumer and hello managed API.</span></span> <span data-ttu-id="0345e-110">Hello шлюз получает все запросы и пересылает их без изменений обычно toohello базовый API.</span><span class="sxs-lookup"><span data-stu-id="0345e-110">hello gateway receives all requests and usually forwards them unaltered toohello underlying API.</span></span> <span data-ttu-id="0345e-111">Однако политика может применяться изменения tooboth hello входящего запроса и исходящего ответа.</span><span class="sxs-lookup"><span data-stu-id="0345e-111">However a policy can apply changes tooboth hello inbound request and outbound response.</span></span>

<span data-ttu-id="0345e-112">Выражения политики может использоваться как значения атрибутов или текстовыми значениями в любой hello политиках управления интерфейсами API, если политика hello не указывает иное.</span><span class="sxs-lookup"><span data-stu-id="0345e-112">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="0345e-113">Некоторые политики, такие как hello [поток управления] [ Control flow] и [переменным] [ Set variable] политики основаны на выражениях политики.</span><span class="sxs-lookup"><span data-stu-id="0345e-113">Some policies such as hello [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="0345e-114">Чтобы узнать больше, ознакомьтесь с [расширенными политиками][Advanced policies] и [выражениями политики][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="0345e-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="0345e-115"><a name="scopes"></a>Как tooconfigure политики</span><span class="sxs-lookup"><span data-stu-id="0345e-115"><a name="scopes"> </a>How tooconfigure policies</span></span>
<span data-ttu-id="0345e-116">Политики можно настроить глобально или в области hello [продукта][Product], [API] [ API] или [операции] [Operation].</span><span class="sxs-lookup"><span data-stu-id="0345e-116">Policies can be configured globally or at hello scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="0345e-117">tooconfigure политики, перейдите в редактор политики toohello hello портала издателя.</span><span class="sxs-lookup"><span data-stu-id="0345e-117">tooconfigure a policy, navigate toohello Policies editor in hello publisher portal.</span></span>

![Меню «Политики»][policies-menu]

<span data-ttu-id="0345e-119">Редактор политики Hello состоит из трех основных частей: hello области (верхнего) hello политики определения политики где инструкций hello список (справа) и (слева) для изменения политики:</span><span class="sxs-lookup"><span data-stu-id="0345e-119">hello policies editor consists of three main sections: hello policy scope (top), hello policy definition where policies are edited (left) and hello statements list (right):</span></span>

![Редактор политик][policies-editor]

<span data-ttu-id="0345e-121">Настройка политики, необходимо сначала выбрать область hello, на какие hello должна применяться политика toobegin.</span><span class="sxs-lookup"><span data-stu-id="0345e-121">toobegin configuring a policy you must first select hello scope at which hello policy should apply.</span></span> <span data-ttu-id="0345e-122">На снимке экрана приветствия ниже hello **начальный** выбранного продукта.</span><span class="sxs-lookup"><span data-stu-id="0345e-122">In hello screenshot below hello **Starter** product is selected.</span></span> <span data-ttu-id="0345e-123">Обратите внимание, что hello объект Далее toohello имя политики указывает на этом уровне уже применяется политика.</span><span class="sxs-lookup"><span data-stu-id="0345e-123">Note that hello square symbol next toohello policy name indicates that a policy is already applied at this level.</span></span>

![Область][policies-scope]

<span data-ttu-id="0345e-125">Так как уже применена политика, hello конфигурация показана на просмотр определения hello.</span><span class="sxs-lookup"><span data-stu-id="0345e-125">Since a policy has already been applied, hello configuration is shown in hello definition view.</span></span>

![Настройка][policies-configure]

<span data-ttu-id="0345e-127">политика Hello отображается только для чтения на первом.</span><span class="sxs-lookup"><span data-stu-id="0345e-127">hello policy is displayed read-only at first.</span></span> <span data-ttu-id="0345e-128">В порядке tooedit определение hello щелкните hello **Настройка политики** действие.</span><span class="sxs-lookup"><span data-stu-id="0345e-128">In order tooedit hello definition click hello **Configure Policy** action.</span></span>

![Редактирование][policies-edit]

<span data-ttu-id="0345e-130">Определение политики Hello — простой XML-документ, описывающий последовательность инструкций, входящих и исходящих подключений.</span><span class="sxs-lookup"><span data-stu-id="0345e-130">hello policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="0345e-131">Hello XML можно изменять непосредственно в окне определения hello.</span><span class="sxs-lookup"><span data-stu-id="0345e-131">hello XML can be edited directly in hello definition window.</span></span> <span data-ttu-id="0345e-132">Список инструкций предоставляется право toohello и инструкций применимо toohello текущей области включены и выделяются; как видно hello **ограничение скорости вызова** инструкции снимке экрана приветствия выше.</span><span class="sxs-lookup"><span data-stu-id="0345e-132">A list of statements is provided toohello right and statements applicable toohello current scope are enabled and highlighted; as demonstrated by hello **Limit Call Rate** statement in hello screenshot above.</span></span>

<span data-ttu-id="0345e-133">Щелкнув оператор включен добавит hello соответствующий XML в расположении hello hello курсора в представлении определения hello.</span><span class="sxs-lookup"><span data-stu-id="0345e-133">Clicking an enabled statement will add hello appropriate XML at hello location of hello cursor in hello definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="0345e-134">Hello политики, которые должны tooadd не включена, убедитесь, что находятся в неправильной области hello для этой политики.</span><span class="sxs-lookup"><span data-stu-id="0345e-134">If hello policy that you want tooadd is not enabled, ensure that you are in hello correct scope for that policy.</span></span> <span data-ttu-id="0345e-135">Каждая инструкция политики предназначена для использования в определенных областях и разделах политики.</span><span class="sxs-lookup"><span data-stu-id="0345e-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="0345e-136">разделы политики tooreview hello и области для политики, проверьте hello **использование** раздел для этой политики в hello [ссылка на политику][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="0345e-136">tooreview hello policy sections and scopes for a policy, check hello **Usage** section for that policy in hello [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="0345e-137">Полный список инструкций политики и их параметры доступны в hello [ссылка на политику][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="0345e-137">A full list of policy statements and their settings are available in hello [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="0345e-138">Например, tooadd новый оператор toorestrict входящих запросов toospecified IP-адресов, поместите курсор hello внутри содержимого hello hello `inbound` hello XML элемент и нажмите кнопку **вызывающий объект ограничение IP-адресов** инструкции.</span><span class="sxs-lookup"><span data-stu-id="0345e-138">For example, tooadd a new statement toorestrict incoming requests toospecified IP addresses, place hello cursor just inside hello content of hello `inbound` XML element and click hello **Restrict caller IPs** statement.</span></span>

![Политики ограничения][policies-restrict]

<span data-ttu-id="0345e-140">При этом будет добавлено toohello фрагмент XML `inbound` элемент, описано, как tooconfigure hello инструкции.</span><span class="sxs-lookup"><span data-stu-id="0345e-140">This will add an XML snippet toohello `inbound` element that provides guidance on how tooconfigure hello statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="0345e-141">toolimit входящие запросы и принимать только те из IP-адрес 1.2.3.4 изменить hello XML следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0345e-141">toolimit inbound requests and accept only those from an IP address of 1.2.3.4 modify hello XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Сохранить][policies-save]

<span data-ttu-id="0345e-143">По завершении настройки hello инструкций для hello политики щелкните **Сохранить** hello изменения немедленно будут распространенный toohello API Management gateway.</span><span class="sxs-lookup"><span data-stu-id="0345e-143">When complete configuring hello statements for hello policy, click **Save** and hello changes will be propagated toohello API Management gateway immediately.</span></span>

## <span data-ttu-id="0345e-144"><a name="sections"> </a>Общая информация о конфигурации политики</span><span class="sxs-lookup"><span data-stu-id="0345e-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="0345e-145">Политика — это набор операторов, которые выполняются для создания запроса и получения ответа.</span><span class="sxs-lookup"><span data-stu-id="0345e-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="0345e-146">Hello конфигурации состоит из соответствующим образом `inbound`, `backend`, `outbound`, и `on-error` разделов, как показано в hello следующая конфигурация.</span><span class="sxs-lookup"><span data-stu-id="0345e-146">hello configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in hello following configuration.</span></span>

```xml
<policies>
  <inbound>
    <!-- statements toobe applied toohello request go here -->
  </inbound>
  <backend>
    <!-- statements toobe applied before hello request is forwarded too
         hello backend service go here -->
  </backend>
  <outbound>
    <!-- statements toobe applied toohello response go here -->
  </outbound>
  <on-error>
    <!-- statements toobe applied if there is an error condition go here -->
  </on-error>
</policies> 
```

<span data-ttu-id="0345e-147">Если возникает ошибка во время обработки запроса hello, все остальные шаги в hello `inbound`, `backend`, или `outbound` разделы пропускаются, и выполнение переходит toohello инструкций в hello `on-error` раздела.</span><span class="sxs-lookup"><span data-stu-id="0345e-147">If there is an error during hello processing of a request, any remaining steps in hello `inbound`, `backend`, or `outbound` sections are skipped and execution jumps toohello statements in hello `on-error` section.</span></span> <span data-ttu-id="0345e-148">Путем размещения операторов политики в hello `on-error` раздел hello ошибки можно просмотреть с помощью hello `context.LastError` свойства, проверка и настройка с помощью hello hello отклик `set-body` политики и настроить, что происходит при возникновении ошибки.</span><span class="sxs-lookup"><span data-stu-id="0345e-148">By placing policy statements in hello `on-error` section you can review hello error by using hello `context.LastError` property, inspect and customize hello error response using hello `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="0345e-149">Предусмотрено кодов ошибок для встроенных действий и ошибки, возникающие во время обработки hello инструкций политики.</span><span class="sxs-lookup"><span data-stu-id="0345e-149">There are error codes for built-in steps and for errors that may occur during hello processing of policy statements.</span></span> <span data-ttu-id="0345e-150">Дополнительные сведения см. в статье [Обработка ошибок в политиках управления API](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span><span class="sxs-lookup"><span data-stu-id="0345e-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="0345e-151">Так как на различных уровнях (глобальные, продукт, api и операции) можно указать политики конфигурации hello предоставляет способ для вас toospecify hello порядок, в котором определения политики hello инструкции выполняются с учетом toohello родительской политики.</span><span class="sxs-lookup"><span data-stu-id="0345e-151">Since policies can be specified at different levels (global, product, api and operation) hello configuration provides a way for you toospecify hello order in which hello policy definition's statements execute with respect toohello parent policy.</span></span> 

<span data-ttu-id="0345e-152">Области политики оцениваются в hello последовательностью.</span><span class="sxs-lookup"><span data-stu-id="0345e-152">Policy scopes are evaluated in hello following order.</span></span>

1. <span data-ttu-id="0345e-153">Глобальная область</span><span class="sxs-lookup"><span data-stu-id="0345e-153">Global scope</span></span>
2. <span data-ttu-id="0345e-154">Область продукта</span><span class="sxs-lookup"><span data-stu-id="0345e-154">Product scope</span></span>
3. <span data-ttu-id="0345e-155">Область API</span><span class="sxs-lookup"><span data-stu-id="0345e-155">API scope</span></span>
4. <span data-ttu-id="0345e-156">Область операций</span><span class="sxs-lookup"><span data-stu-id="0345e-156">Operation scope</span></span>

<span data-ttu-id="0345e-157">Hello инструкций в них вычисляются toohello размещение hello в соответствии с `base` элемента, если он имеется.</span><span class="sxs-lookup"><span data-stu-id="0345e-157">hello statements within them are evaluated according toohello placement of hello `base` element, if it is present.</span></span> <span data-ttu-id="0345e-158">Глобальные политики имеет нет родительской политики и с помощью hello `<base>` элемент в нем не делает ничего.</span><span class="sxs-lookup"><span data-stu-id="0345e-158">Global policy has no parent policy and using hello `<base>` element in it has no effect.</span></span>

<span data-ttu-id="0345e-159">Например при наличии политики на глобальном уровне hello и политика, заданная для API-Интерфейс, затем всякий раз, когда используется этот конкретный API обе политики применяются.</span><span class="sxs-lookup"><span data-stu-id="0345e-159">For example, if you have a policy at hello global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="0345e-160">Управление API позволяет детерминированным упорядочение инструкций объединенный политики через hello базового элемента.</span><span class="sxs-lookup"><span data-stu-id="0345e-160">API Management allows for deterministic ordering of combined policy statements via hello base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="0345e-161">В определении политики пример hello выше, hello `cross-domain` инструкция выполняется перед любой более поздней версии политики, которые в свою очередь, будет следовать hello `find-and-replace` политики.</span><span class="sxs-lookup"><span data-stu-id="0345e-161">In hello example policy definition above, hello `cross-domain` statement would execute before any higher policies which would in turn, be followed by hello `find-and-replace` policy.</span></span> 

<span data-ttu-id="0345e-162">политики hello toosee в текущей области hello в редакторе hello политики, щелкните **пересчитать эффективную политику для выбранной области**.</span><span class="sxs-lookup"><span data-stu-id="0345e-162">toosee hello policies in hello current scope in hello policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0345e-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0345e-163">Next steps</span></span>
<span data-ttu-id="0345e-164">Посмотрите следующие видео о выражениях политики.</span><span class="sxs-lookup"><span data-stu-id="0345e-164">Check out following video on policy expressions.</span></span>

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
