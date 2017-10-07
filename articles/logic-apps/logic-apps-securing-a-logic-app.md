---
title: "aaaSecure доступа к приложениям логику tooAzure | Документы Microsoft"
description: "Добавьте безопасности для защиты tootriggers доступ, входов и выходов, параметров действия и службы, используемые с рабочими процессами в логике приложения Azure."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: abda2179e4cc2d2295cd8332ec017c848a456264
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="secure-access-tooyour-logic-apps"></a><span data-ttu-id="05166-103">Защита доступа к tooyour логику приложения</span><span class="sxs-lookup"><span data-stu-id="05166-103">Secure access tooyour logic apps</span></span>

<span data-ttu-id="05166-104">Существует много доступных toohelp средств защиты логику приложения.</span><span class="sxs-lookup"><span data-stu-id="05166-104">There are many tools available toohelp you secure your logic app.</span></span>

* <span data-ttu-id="05166-105">Обеспечение безопасности доступа tootrigger логику приложения (триггер запрос HTTP)</span><span class="sxs-lookup"><span data-stu-id="05166-105">Securing access tootrigger a logic app (HTTP Request Trigger)</span></span>
* <span data-ttu-id="05166-106">Защита доступа к toomanage, изменение или чтение приложения логики</span><span class="sxs-lookup"><span data-stu-id="05166-106">Securing access toomanage, edit, or read a logic app</span></span>
* <span data-ttu-id="05166-107">Обеспечение безопасности доступа toocontents входов и выходов для запуска</span><span class="sxs-lookup"><span data-stu-id="05166-107">Securing access toocontents of inputs and outputs for a run</span></span>
* <span data-ttu-id="05166-108">Обеспечение безопасности параметров или входных данных в рамках действий в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="05166-108">Securing parameters or inputs within actions in a workflow</span></span>
* <span data-ttu-id="05166-109">Защита доступа к tooservices, получать запросы из рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="05166-109">Securing access tooservices that receive requests from a workflow</span></span>

## <a name="secure-access-tootrigger"></a><span data-ttu-id="05166-110">Tootrigger безопасный доступ</span><span class="sxs-lookup"><span data-stu-id="05166-110">Secure access tootrigger</span></span>

<span data-ttu-id="05166-111">При работе с логики приложения, вызывающего событие HTTP-запроса ([запроса](../connectors/connectors-native-reqres.md) или [веб-перехватчика](../connectors/connectors-native-webhook.md)), вы можете ограничить доступ, чтобы только авторизованные клиенты могут запускать приложение hello логику.</span><span class="sxs-lookup"><span data-stu-id="05166-111">When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire hello logic app.</span></span> <span data-ttu-id="05166-112">Все запросы к приложению логики зашифрованы и защищены с помощью SSL.</span><span class="sxs-lookup"><span data-stu-id="05166-112">All requests into a logic app are encrypted and secured via SSL.</span></span>

### <a name="shared-access-signature"></a><span data-ttu-id="05166-113">Подписанный URL-адрес</span><span class="sxs-lookup"><span data-stu-id="05166-113">Shared Access Signature</span></span>

<span data-ttu-id="05166-114">Включает каждой конечной точки запроса для приложения логики [подписи общего доступа (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) как часть URL-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="05166-114">Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) as part of hello URL.</span></span> <span data-ttu-id="05166-115">Каждый URL-адрес содержит параметр запроса `sp`, `sv` и `sig`.</span><span class="sxs-lookup"><span data-stu-id="05166-115">Each URL contains a `sp`, `sv`, and `sig` query parameter.</span></span> <span data-ttu-id="05166-116">Разрешения задаются `sp`, и соответствующие методы tooHTTP может быть, `sv` — toogenerate версия, используемая hello, и `sig` является tootrigger используется tooauthenticate доступа.</span><span class="sxs-lookup"><span data-stu-id="05166-116">Permissions are specified by `sp`, and correspond tooHTTP methods allowed, `sv` is hello version used toogenerate, and `sig` is used tooauthenticate access tootrigger.</span></span> <span data-ttu-id="05166-117">Сигнатура Hello создается с помощью алгоритма hello SHA256 с открытым ключом для всех путей hello URL-адрес и свойства.</span><span class="sxs-lookup"><span data-stu-id="05166-117">hello signature is generated using hello SHA256 algorithm with a secret key on all hello URL paths and properties.</span></span> <span data-ttu-id="05166-118">Hello секретный ключ никогда не предоставляется и не опубликован, а хранятся зашифрованные и хранимые как часть логики приложения hello.</span><span class="sxs-lookup"><span data-stu-id="05166-118">hello secret key is never exposed and published, and is kept encrypted and stored as part of hello logic app.</span></span> <span data-ttu-id="05166-119">Логика приложения авторизует только триггеры, содержащие действительной подписи, созданных с помощью hello секретный ключ.</span><span class="sxs-lookup"><span data-stu-id="05166-119">Your logic app only authorizes triggers that contain a valid signature created with hello secret key.</span></span>

#### <a name="regenerate-access-keys"></a><span data-ttu-id="05166-120">Повторное создание ключей доступа</span><span class="sxs-lookup"><span data-stu-id="05166-120">Regenerate access keys</span></span>

<span data-ttu-id="05166-121">Можно повторно создать новый ключ безопасного в любое время через портал hello API-интерфейса REST или Azure.</span><span class="sxs-lookup"><span data-stu-id="05166-121">You can regenerate a new secure key at anytime through hello REST API or Azure portal.</span></span> <span data-ttu-id="05166-122">Все текущие URL-адреса, созданные ранее с помощью старого ключа hello являются недействительными и больше не авторизованным toofire hello логику приложения.</span><span class="sxs-lookup"><span data-stu-id="05166-122">All current URLs that were generated previously using hello old key are invalidated and no longer authorized toofire hello logic app.</span></span>

1. <span data-ttu-id="05166-123">В hello портал Azure откройте приложение hello логику, нужно tooregenerate ключ</span><span class="sxs-lookup"><span data-stu-id="05166-123">In hello Azure portal, open hello logic app you want tooregenerate a key</span></span>
1. <span data-ttu-id="05166-124">Нажмите кнопку hello **клавиши доступа** пункт **параметры**</span><span class="sxs-lookup"><span data-stu-id="05166-124">Click hello **Access Keys** menu item under **Settings**</span></span>
1. <span data-ttu-id="05166-125">Выберите процесс завершения hello и ключа tooregenerate hello</span><span class="sxs-lookup"><span data-stu-id="05166-125">Choose hello key tooregenerate and complete hello process</span></span>

<span data-ttu-id="05166-126">URL-адреса, получаемых после повторного создания должны быть подписаны hello новый ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="05166-126">URLs you retrieve after regeneration are signed with hello new access key.</span></span>

#### <a name="creating-callback-urls-with-an-expiration-date"></a><span data-ttu-id="05166-127">Создание URL-адреса обратного вызова с истекшим сроком действия</span><span class="sxs-lookup"><span data-stu-id="05166-127">Creating callback URLs with an expiration date</span></span>

<span data-ttu-id="05166-128">Если URL-адрес hello совместно с другими участниками, можно создать URL-адреса с конкретным разделам и даты окончания срока действия при необходимости.</span><span class="sxs-lookup"><span data-stu-id="05166-128">If you are sharing hello URL with other parties, you can generate URLs with specific keys and expiration dates as needed.</span></span> <span data-ttu-id="05166-129">Можно затем легко развертывания ключей или обеспечения доступа toofire приложение имеет ограниченные tooa определенных timespan.</span><span class="sxs-lookup"><span data-stu-id="05166-129">You can then seamlessly roll keys, or ensure access toofire an app is restricted tooa certain timespan.</span></span> <span data-ttu-id="05166-130">Можно указать дату окончания срока действия для URL-адреса через hello [логику приложения REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span><span class="sxs-lookup"><span data-stu-id="05166-130">You can specify an expiration date for a URL through hello [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="05166-131">В тексте hello включить свойство hello `NotAfter` как строку даты в JSON, который возвращает URL-адрес обратного вызова, действительна только до hello `NotAfter` даты и времени.</span><span class="sxs-lookup"><span data-stu-id="05166-131">In hello body, include hello property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until hello `NotAfter` date and time.</span></span>

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a><span data-ttu-id="05166-132">Создание URL-адресов с использованием первичного или вторичного секретного ключа</span><span class="sxs-lookup"><span data-stu-id="05166-132">Creating URLs with primary or secondary secret key</span></span>

<span data-ttu-id="05166-133">После создания или список URL-адресов обратного вызова для триггеров на основе запросов, можно также указать какой URL-адрес ключа toouse toosign hello.</span><span class="sxs-lookup"><span data-stu-id="05166-133">When you generate or list callback URLs for request-based triggers, you can also specify which key toouse toosign hello URL.</span></span>  <span data-ttu-id="05166-134">Можно создать URL-адрес, подписанный указанным ключом через hello [логику приложения REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="05166-134">You can generate a URL signed by a specific key through hello [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="05166-135">В тексте hello включить свойство hello `KeyType` либо как `Primary` или `Secondary`.</span><span class="sxs-lookup"><span data-stu-id="05166-135">In hello body, include hello property `KeyType` as either `Primary` or `Secondary`.</span></span>  <span data-ttu-id="05166-136">Возвращает подписанный hello безопасного ключ, указанный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="05166-136">This returns a URL signed by hello secure key specified.</span></span>

### <a name="restrict-incoming-ip-addresses"></a><span data-ttu-id="05166-137">Ограничение входящих IP-адресов</span><span class="sxs-lookup"><span data-stu-id="05166-137">Restrict incoming IP addresses</span></span>

<span data-ttu-id="05166-138">В дополнение к этому toohello подпись общего доступа, вы можете toorestrict вызов приложения логики только из конкретных клиентов.</span><span class="sxs-lookup"><span data-stu-id="05166-138">In addition toohello Shared Access Signature, you may wish toorestrict calling a logic app only from specific clients.</span></span>  <span data-ttu-id="05166-139">Например, при управлении конечной точки через API управления Azure, можно ограничить hello логику приложения tooonly принять hello при запросе hello из hello IP-адрес экземпляра управления API.</span><span class="sxs-lookup"><span data-stu-id="05166-139">For example, if you manage your endpoint through Azure API Management, you can restrict hello logic app tooonly accept hello request when hello request comes from hello API Management instance IP address.</span></span>

<span data-ttu-id="05166-140">Этот параметр можно настроить в параметрах приложения hello логику:</span><span class="sxs-lookup"><span data-stu-id="05166-140">This setting can be configured within hello logic app settings:</span></span>

1. <span data-ttu-id="05166-141">В hello портал Azure откройте приложение hello логику, нужно tooadd ограничения IP-адресов</span><span class="sxs-lookup"><span data-stu-id="05166-141">In hello Azure portal, open hello logic app you want tooadd IP address restrictions</span></span>
1. <span data-ttu-id="05166-142">Нажмите кнопку hello **конфигурации контроля доступа** пункт **параметры**</span><span class="sxs-lookup"><span data-stu-id="05166-142">Click hello **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="05166-143">Укажите список hello toobe диапазоны адресов IP, принимаемое hello триггера</span><span class="sxs-lookup"><span data-stu-id="05166-143">Specify hello list of IP address ranges toobe accepted by hello trigger</span></span>

<span data-ttu-id="05166-144">Допустимый диапазон IP имеет формат hello `192.168.1.1/255`.</span><span class="sxs-lookup"><span data-stu-id="05166-144">A valid IP range takes hello format `192.168.1.1/255`.</span></span> <span data-ttu-id="05166-145">Пожара tooonly hello логику приложения как вложенные логики приложения, установите hello **только в другие приложения логики** параметр.</span><span class="sxs-lookup"><span data-stu-id="05166-145">If you want hello logic app tooonly fire as a nested logic app, select hello **Only other logic apps** option.</span></span> <span data-ttu-id="05166-146">Этот параметр записывает ресурс toohello пустой массив, это означает, что только вызовы из hello самой службой fire (родительского логики приложения) успешно.</span><span class="sxs-lookup"><span data-stu-id="05166-146">This option writes an empty array toohello resource, meaning only calls from hello service itself (parent logic apps) fire successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="05166-147">Можно запустить приложение логики с триггером запроса через API-Интерфейс REST hello и управления `/triggers/{triggerName}/run` независимо от IP.</span><span class="sxs-lookup"><span data-stu-id="05166-147">You can still run a logic app with a request trigger through hello REST API / Management `/triggers/{triggerName}/run` regardless of IP.</span></span> <span data-ttu-id="05166-148">Данный сценарий требует проверки подлинности hello Azure REST API, и все события будут отображаться в hello журналов аудита Azure.</span><span class="sxs-lookup"><span data-stu-id="05166-148">This scenario requires authentication against hello Azure REST API, and all events would appear in hello Azure Audit Log.</span></span> <span data-ttu-id="05166-149">Настройте политики контроля доступа соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="05166-149">Set access control policies accordingly.</span></span>

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a><span data-ttu-id="05166-150">Задание диапазонов IP-адресов для определения ресурса hello</span><span class="sxs-lookup"><span data-stu-id="05166-150">Setting IP ranges on hello resource definition</span></span>

<span data-ttu-id="05166-151">Если вы используете [шаблон развертывания](logic-apps-create-deploy-template.md) tooautomate развертываниям параметры диапазона hello IP-адреса можно настроить на шаблон ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="05166-151">If you are using a [deployment template](logic-apps-create-deploy-template.md) tooautomate your deployments, hello IP range settings can be configured on hello resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a><span data-ttu-id="05166-152">Добавление Azure Active Directory, OAuth или других механизмов безопасности</span><span class="sxs-lookup"><span data-stu-id="05166-152">Adding Azure Active Directory, OAuth, or other security</span></span>

<span data-ttu-id="05166-153">Дополнительные авторизации протоколов поверх приложения логики, tooadd [управления API Azure](https://azure.microsoft.com/services/api-management/) предлагает широкие возможности мониторинга, безопасности, политики и документации для любой конечной точки с возможностью tooexpose hello приложения логики как интерфейс API.</span><span class="sxs-lookup"><span data-stu-id="05166-153">tooadd more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with hello capability tooexpose a logic app as an API.</span></span> <span data-ttu-id="05166-154">Управления API Azure можно предоставлять конечную точку открытые или закрытые приложение hello логики, которую может использовать Azure Active Directory, сертификат, OAuth или других стандартов безопасности.</span><span class="sxs-lookup"><span data-stu-id="05166-154">Azure API Management can expose a public or private endpoint for hello logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards.</span></span> <span data-ttu-id="05166-155">При получении запроса API управления Azure пересылает hello запроса toohello логику приложения (выполняются все необходимые преобразования или ограничения на лету).</span><span class="sxs-lookup"><span data-stu-id="05166-155">When a request is received, Azure API Management forwards hello request toohello logic app (performing any needed transformations or restrictions in-flight).</span></span> <span data-ttu-id="05166-156">Можно использовать hello входящих диапазон IP-адресов параметры на hello логику приложения tooonly разрешить hello логику приложения toobe запускается из API-интерфейса управления.</span><span class="sxs-lookup"><span data-stu-id="05166-156">You can use hello incoming IP range settings on hello logic app tooonly allow hello logic app toobe triggered from API Management.</span></span>

## <a name="secure-access-toomanage-or-edit-logic-apps"></a><span data-ttu-id="05166-157">Защита доступа к toomanage или изменить логику приложений</span><span class="sxs-lookup"><span data-stu-id="05166-157">Secure access toomanage or edit logic apps</span></span>

<span data-ttu-id="05166-158">Вы можете ограничить операции доступа к toomanagement для логики приложения таким образом, может tooperform операции с ресурсом hello только определенным пользователям или группам.</span><span class="sxs-lookup"><span data-stu-id="05166-158">You can restrict access toomanagement operations on a logic app so that only specific users or groups are able tooperform operations on hello resource.</span></span> <span data-ttu-id="05166-159">Логика приложения используют hello Azure [управление доступом на основе ролей (RBAC)](../active-directory/role-based-access-control-configure.md) компонентов и могут настраиваться с помощью hello тех же средств.</span><span class="sxs-lookup"><span data-stu-id="05166-159">Logic apps use hello Azure [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) feature, and can be customized with hello same tools.</span></span>  <span data-ttu-id="05166-160">Существует несколько встроенных ролей, которые также можно назначать члены tooas вашей подписки:</span><span class="sxs-lookup"><span data-stu-id="05166-160">There are a few built-in roles you can assign members of your subscription tooas well:</span></span>

* <span data-ttu-id="05166-161">**Логика приложения участника** -предоставляет доступ tooview, изменение и обновление приложения логики.</span><span class="sxs-lookup"><span data-stu-id="05166-161">**Logic App Contributor** - Provides access tooview, edit, and update a logic app.</span></span>  <span data-ttu-id="05166-162">Невозможно удалить ресурс hello или выполнять операции администрирования.</span><span class="sxs-lookup"><span data-stu-id="05166-162">Cannot remove hello resource or perform admin operations.</span></span>
* <span data-ttu-id="05166-163">**Оператор логику приложения** — можно просматривать приложения логики hello и журнал выполнения и включить или отключить.</span><span class="sxs-lookup"><span data-stu-id="05166-163">**Logic App Operator** - Can view hello logic app and run history, and enable/disable.</span></span>  <span data-ttu-id="05166-164">Не удается изменить или обновить определение hello.</span><span class="sxs-lookup"><span data-stu-id="05166-164">Cannot edit or update hello definition.</span></span>

<span data-ttu-id="05166-165">Можно также использовать [блокировка ресурса Azure](../azure-resource-manager/resource-group-lock-resources.md) tooprevent изменением или удалением приложения логики.</span><span class="sxs-lookup"><span data-stu-id="05166-165">You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) tooprevent changing or deleting logic apps.</span></span> <span data-ttu-id="05166-166">Эта возможность является ценным tooprevent производственных ресурсов от изменения или удаления.</span><span class="sxs-lookup"><span data-stu-id="05166-166">This capability is valuable tooprevent production resources from changes or deletions.</span></span>

## <a name="secure-access-toocontents-of-hello-run-history"></a><span data-ttu-id="05166-167">Toocontents безопасный доступ из hello, журнал выполнения</span><span class="sxs-lookup"><span data-stu-id="05166-167">Secure access toocontents of hello run history</span></span>

<span data-ttu-id="05166-168">Вы можете ограничить доступ toocontents входов или выходов из предыдущих запусков toospecific IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="05166-168">You can restrict access toocontents of inputs or outputs from previous runs toospecific IP address ranges.</span></span>  

<span data-ttu-id="05166-169">Все данные в рамках выполнения рабочего процесса шифруются при передаче и хранении.</span><span class="sxs-lookup"><span data-stu-id="05166-169">All data within a workflow run is encrypted in transit and at rest.</span></span> <span data-ttu-id="05166-170">При внесении toorun журнал вызовов, hello служба проверяет подлинность запроса hello и предоставляет ссылки toohello запроса ответа входов и выходов.</span><span class="sxs-lookup"><span data-stu-id="05166-170">When a call toorun history is made, hello service authenticates hello request and provides links toohello request and response inputs and outputs.</span></span> <span data-ttu-id="05166-171">Эта ссылка может указывать на защищенном поэтому только запросы, tooview содержимое из указанного диапазона IP-адресов возврата hello содержимого.</span><span class="sxs-lookup"><span data-stu-id="05166-171">This link can be protected so only requests tooview content from a designated IP address range return hello contents.</span></span> <span data-ttu-id="05166-172">Эту возможность можно использовать в качестве дополнительного метода контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="05166-172">You can use this capability for additional access control.</span></span> <span data-ttu-id="05166-173">Можно также указать IP-адрес в виде `0.0.0.0`, тогда никто не сможет получить доступ к входным и выходным данным.</span><span class="sxs-lookup"><span data-stu-id="05166-173">You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs.</span></span> <span data-ttu-id="05166-174">Только пользователь с правами администратора удалось удалить это ограничение, предоставляя возможность hello содержимое tooworkflow доступа «just-in-time».</span><span class="sxs-lookup"><span data-stu-id="05166-174">Only someone with admin permissions could remove this restriction, providing hello possibility for 'just-in-time' access tooworkflow contents.</span></span>

<span data-ttu-id="05166-175">Этот параметр можно настроить в параметров ресурсов hello hello портала Azure:</span><span class="sxs-lookup"><span data-stu-id="05166-175">This setting can be configured within hello resource settings of hello Azure portal:</span></span>

1. <span data-ttu-id="05166-176">В hello портал Azure откройте приложение hello логику, нужно tooadd ограничения IP-адресов</span><span class="sxs-lookup"><span data-stu-id="05166-176">In hello Azure portal, open hello logic app you want tooadd IP address restrictions</span></span>
1. <span data-ttu-id="05166-177">Нажмите кнопку hello **конфигурации контроля доступа** пункт **параметры**</span><span class="sxs-lookup"><span data-stu-id="05166-177">Click hello **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="05166-178">Укажите список диапазонов IP-адресов для доступа к toocontent hello</span><span class="sxs-lookup"><span data-stu-id="05166-178">Specify hello list of IP address ranges for access toocontent</span></span>

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a><span data-ttu-id="05166-179">Задание диапазонов IP-адресов для определения ресурса hello</span><span class="sxs-lookup"><span data-stu-id="05166-179">Setting IP ranges on hello resource definition</span></span>

<span data-ttu-id="05166-180">Если вы используете [шаблон развертывания](logic-apps-create-deploy-template.md) tooautomate развертываниям параметры диапазона hello IP-адреса можно настроить на шаблон ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="05166-180">If you are using a [deployment template](logic-apps-create-deploy-template.md) tooautomate your deployments, hello IP range settings can be configured on hello resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a><span data-ttu-id="05166-181">Параметры безопасности и входные данные в рабочем процессе</span><span class="sxs-lookup"><span data-stu-id="05166-181">Secure parameters and inputs within a workflow</span></span>

<span data-ttu-id="05166-182">Может потребоваться tooparameterize некоторые аспекты определение рабочего процесса для развертывания в средах.</span><span class="sxs-lookup"><span data-stu-id="05166-182">You might want tooparameterize some aspects of a workflow definition for deployment across environments.</span></span> <span data-ttu-id="05166-183">Кроме того, некоторые параметры могут быть безопасные параметры, необходимо исключить tooappear при изменении рабочего процесса, такие как идентификатор клиента и секрет клиента для [проверки подлинности Azure Active Directory](../connectors/connectors-native-http.md#authentication) действия HTTP.</span><span class="sxs-lookup"><span data-stu-id="05166-183">Also, some parameters might be secure parameters you don't want tooappear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.</span></span>

### <a name="using-parameters-and-secure-parameters"></a><span data-ttu-id="05166-184">Использование параметров и параметров безопасности</span><span class="sxs-lookup"><span data-stu-id="05166-184">Using parameters and secure parameters</span></span>

<span data-ttu-id="05166-185">tooaccess hello значение параметра ресурсов во время выполнения, hello [язык определения рабочих процессов](http://aka.ms/logicappsdocs) предоставляет `@parameters()` операции.</span><span class="sxs-lookup"><span data-stu-id="05166-185">tooaccess hello value of a resource parameter at runtime, hello [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation.</span></span> <span data-ttu-id="05166-186">Кроме того, вы можете [укажите параметры в шаблон развертывания ресурсов hello](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="05166-186">Also, you can [specify parameters in hello resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span></span> <span data-ttu-id="05166-187">Однако если указан тип параметра hello `securestring`, параметр hello не будет возвращен с rest hello hello определения ресурса и не будет доступен, просмотрев hello ресурса после развертывания.</span><span class="sxs-lookup"><span data-stu-id="05166-187">But if you specify hello parameter type as `securestring`, hello parameter won't be returned with hello rest of hello resource definition, and won't be accessible by viewing hello resource after deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="05166-188">Если параметра используется в заголовках hello или основной текст запроса, hello параметра может быть видимой осуществлять доступ к истории выполнения hello и исходящих HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="05166-188">If your parameter is used in hello headers or body of a request, hello parameter might be visible by accessing hello run history and outgoing HTTP request.</span></span> <span data-ttu-id="05166-189">Убедитесь, что tooset политик доступа к содержимому соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="05166-189">Make sure tooset your content access policies accordingly.</span></span>
> <span data-ttu-id="05166-190">Заголовки авторизации никогда не отображаются во входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="05166-190">Authorization headers are never visible through inputs or outputs.</span></span> <span data-ttu-id="05166-191">Поэтому если существует используется секрет hello, секрет hello не удается найти.</span><span class="sxs-lookup"><span data-stu-id="05166-191">So if hello secret is being used there, hello secret is not retrievable.</span></span>

#### <a name="resource-deployment-template-with-secrets"></a><span data-ttu-id="05166-192">Шаблон развертывания ресурсов с использованием секретов</span><span class="sxs-lookup"><span data-stu-id="05166-192">Resource deployment template with secrets</span></span>

<span data-ttu-id="05166-193">Hello пример развертывания, который ссылается на безопасный параметр `secret` во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="05166-193">hello following example shows a deployment that references a secure parameter of `secret` at runtime.</span></span> <span data-ttu-id="05166-194">В файле отдельные параметры, можно указать значение hello среды для hello `secret`, или используйте [KeyVault диспетчера ресурсов Azure](../azure-resource-manager/resource-manager-keyvault-parameter.md) секреты tooretrieve во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="05166-194">In a separate parameters file, you could specify hello environment value for hello `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve secrets at deploy time.</span></span>

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is hello request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a><span data-ttu-id="05166-195">Защита доступа к tooservices получения запросов из рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="05166-195">Secure access tooservices receiving requests from a workflow</span></span>

<span data-ttu-id="05166-196">Много способов toohelp являются безопасными по любой конечной точки hello логику приложению tooaccess.</span><span class="sxs-lookup"><span data-stu-id="05166-196">There are many ways toohelp secure any endpoint hello logic app needs tooaccess.</span></span>

### <a name="using-authentication-on-outbound-requests"></a><span data-ttu-id="05166-197">Использование проверки подлинности при исходящих запросах</span><span class="sxs-lookup"><span data-stu-id="05166-197">Using authentication on outbound requests</span></span>

<span data-ttu-id="05166-198">При работе с HTTP, HTTP + Swagger (открытых API) или веб-перехватчика действие, можно добавить отправляемого запроса toohello проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="05166-198">When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication toohello request being sent.</span></span> <span data-ttu-id="05166-199">Это может быть обычная аутентификация, аутентификация на основе сертификата или аутентификация Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="05166-199">You could include basic authentication, certificate authentication, or Azure Active Directory authentication.</span></span> <span data-ttu-id="05166-200">Сведения о том, как tooconfigure этой проверки подлинности можно найти [в этой статье](../connectors/connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="05166-200">Details on how tooconfigure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).</span></span>

### <a name="restricting-access-toologic-app-ip-addresses"></a><span data-ttu-id="05166-201">Ограничения IP-адресов доступа toologic приложения</span><span class="sxs-lookup"><span data-stu-id="05166-201">Restricting access toologic app IP addresses</span></span>

<span data-ttu-id="05166-202">Все вызовы из приложений логики поступают из определенного набора IP-адресов для каждого региона.</span><span class="sxs-lookup"><span data-stu-id="05166-202">All calls from logic apps come from a specific set of IP addresses per region.</span></span> <span data-ttu-id="05166-203">Можно добавить дополнительную фильтрацию tooonly прием запросов по сравнению с указанных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="05166-203">You can add additional filtering tooonly accept requests from those designated IP addresses.</span></span> <span data-ttu-id="05166-204">Список этих IP-адресов можно найти в статье [Ограничения и настройка приложений логики](logic-apps-limits-and-config.md#configuration).</span><span class="sxs-lookup"><span data-stu-id="05166-204">For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).</span></span>

### <a name="on-premises-connectivity"></a><span data-ttu-id="05166-205">Локальные возможности подключения</span><span class="sxs-lookup"><span data-stu-id="05166-205">On-premises connectivity</span></span>

<span data-ttu-id="05166-206">Приложения логики обеспечивают интеграцию с несколькими tooprovide служб, безопасную и надежную локальной связи.</span><span class="sxs-lookup"><span data-stu-id="05166-206">Logic apps provide integration with several services tooprovide secure and reliable on-premises communication.</span></span>

#### <a name="on-premises-data-gateway"></a><span data-ttu-id="05166-207">Локальный шлюз данных</span><span class="sxs-lookup"><span data-stu-id="05166-207">On-premises data gateway</span></span>

<span data-ttu-id="05166-208">Многие управляемых соединители для логики приложений обеспечивают безопасное подключение между tooon локальной системы, включая файловой системы, SQL, SharePoint, DB2 и многое другое.</span><span class="sxs-lookup"><span data-stu-id="05166-208">Many managed connectors for logic apps provide secure connectivity tooon-premises systems, including File System, SQL, SharePoint, DB2, and more.</span></span> <span data-ttu-id="05166-209">шлюз Hello передает данные из локальных источников шифрованные каналы через hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="05166-209">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="05166-210">Весь трафик поступает как безопасный исходящий трафик от агента hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="05166-210">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="05166-211">Дополнительные сведения о [как работает шлюз данных hello](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="05166-211">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span>

#### <a name="azure-api-management"></a><span data-ttu-id="05166-212">Cлужба управления Azure API </span><span class="sxs-lookup"><span data-stu-id="05166-212">Azure API Management</span></span>

<span data-ttu-id="05166-213">[Управления API Azure](https://azure.microsoft.com/services/api-management/) имеет возможности подключения в локальной среде, включая интеграцию сеть сеть VPN и ExpressRoute для защищенных систем tooon локальный прокси-сервера и обмена данными.</span><span class="sxs-lookup"><span data-stu-id="05166-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication tooon-premises systems.</span></span> <span data-ttu-id="05166-214">В hello конструктор логики приложения можно быстро выбрать интерфейс API, предоставляемых API управления Azure в рамках рабочего процесса, предоставляют быстрый доступ tooon локальные системы.</span><span class="sxs-lookup"><span data-stu-id="05166-214">In hello Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access tooon-premises systems.</span></span>

#### <a name="hybrid-connections-from-azure-app-service"></a><span data-ttu-id="05166-215">Гибридные подключения из службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="05166-215">Hybrid connections from Azure App Service</span></span>

<span data-ttu-id="05166-216">Hello локальной гибридного подключения можно использовать для Azure API и веб-приложений toocommunicate локальной.</span><span class="sxs-lookup"><span data-stu-id="05166-216">You can use hello on-premises hybrid connection feature for Azure API and Web apps toocommunicate on-premises.</span></span>  <span data-ttu-id="05166-217">Сведения о гибридных подключений и обнаружение tooconfigure [в этой статье](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="05166-217">Details on hybrid connections and how tooconfigure can be found [in this article](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="05166-218">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="05166-218">Next steps</span></span>
[<span data-ttu-id="05166-219">Создание шаблона развертывания приложения логики</span><span class="sxs-lookup"><span data-stu-id="05166-219">Create a deployment template</span></span>](logic-apps-create-deploy-template.md)  
[<span data-ttu-id="05166-220">Обработка исключений</span><span class="sxs-lookup"><span data-stu-id="05166-220">Exception handling</span></span>](logic-apps-exception-handling.md)  
[<span data-ttu-id="05166-221">См. статью Мониторинг приложений логики.</span><span class="sxs-lookup"><span data-stu-id="05166-221">Monitor your logic apps</span></span>](logic-apps-monitor-your-logic-apps.md)  
[<span data-ttu-id="05166-222">Диагностика сбоев приложений логики</span><span class="sxs-lookup"><span data-stu-id="05166-222">Diagnosing logic app failures and issues</span></span>](logic-apps-diagnosing-failures.md)  
