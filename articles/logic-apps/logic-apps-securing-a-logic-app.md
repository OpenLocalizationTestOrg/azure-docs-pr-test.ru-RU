---
title: "Безопасный доступ в Azure Logic Apps | Документация Майкрософт"
description: "Узнайте, как повысить уровень безопасности для защиты доступа к триггерам, входным и выходным данным, параметрам действий и службам, используемым с рабочими процессами в Azure Logic Apps."
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
ms.openlocfilehash: 0528d660f590e106f61729f10f8f68da3fe58cb7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="secure-access-to-your-logic-apps"></a><span data-ttu-id="31b19-103">Безопасный доступ к приложениям логики</span><span class="sxs-lookup"><span data-stu-id="31b19-103">Secure access to your logic apps</span></span>

<span data-ttu-id="31b19-104">Существует множество средств для защиты приложения логики.</span><span class="sxs-lookup"><span data-stu-id="31b19-104">There are many tools available to help you secure your logic app.</span></span>

* <span data-ttu-id="31b19-105">Защита доступа к активации приложения логики (триггер HTTP-запросов).</span><span class="sxs-lookup"><span data-stu-id="31b19-105">Securing access to trigger a logic app (HTTP Request Trigger)</span></span>
* <span data-ttu-id="31b19-106">Защита доступа к управлению приложением логики, а также изменению или считыванию его.</span><span class="sxs-lookup"><span data-stu-id="31b19-106">Securing access to manage, edit, or read a logic app</span></span>
* <span data-ttu-id="31b19-107">Защита доступа к содержимому входных и выходных данных для выполнения.</span><span class="sxs-lookup"><span data-stu-id="31b19-107">Securing access to contents of inputs and outputs for a run</span></span>
* <span data-ttu-id="31b19-108">Обеспечение безопасности параметров или входных данных в рамках действий в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="31b19-108">Securing parameters or inputs within actions in a workflow</span></span>
* <span data-ttu-id="31b19-109">Защита доступа к службам, которые получают запросы от рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="31b19-109">Securing access to services that receive requests from a workflow</span></span>

## <a name="secure-access-to-trigger"></a><span data-ttu-id="31b19-110">Защита доступа к активации</span><span class="sxs-lookup"><span data-stu-id="31b19-110">Secure access to trigger</span></span>

<span data-ttu-id="31b19-111">При работе с приложением логики, которое запускает HTTP-запрос ([запрос](../connectors/connectors-native-reqres.md) или [webhook](../connectors/connectors-native-webhook.md)), можно ограничить доступ таким образом, чтобы его могли запускать только авторизованные клиенты.</span><span class="sxs-lookup"><span data-stu-id="31b19-111">When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire the logic app.</span></span> <span data-ttu-id="31b19-112">Все запросы к приложению логики зашифрованы и защищены с помощью SSL.</span><span class="sxs-lookup"><span data-stu-id="31b19-112">All requests into a logic app are encrypted and secured via SSL.</span></span>

### <a name="shared-access-signature"></a><span data-ttu-id="31b19-113">Подписанный URL-адрес</span><span class="sxs-lookup"><span data-stu-id="31b19-113">Shared Access Signature</span></span>

<span data-ttu-id="31b19-114">Как часть URL-адреса каждой конечной точки запроса для приложения логики используется [подписанный URL-адрес](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAS).</span><span class="sxs-lookup"><span data-stu-id="31b19-114">Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) as part of the URL.</span></span> <span data-ttu-id="31b19-115">Каждый URL-адрес содержит параметр запроса `sp`, `sv` и `sig`.</span><span class="sxs-lookup"><span data-stu-id="31b19-115">Each URL contains a `sp`, `sv`, and `sig` query parameter.</span></span> <span data-ttu-id="31b19-116">Разрешения указываются с помощью параметра `sp` и соответствуют разрешенным методам HTTP. `sv` — это версия, используемая для создания, а `sig` используется для проверки подлинности доступа к активации.</span><span class="sxs-lookup"><span data-stu-id="31b19-116">Permissions are specified by `sp`, and correspond to HTTP methods allowed, `sv` is the version used to generate, and `sig` is used to authenticate access to trigger.</span></span> <span data-ttu-id="31b19-117">Подпись создается с использованием алгоритма SHA256 с секретным ключом для всех URL-путей и свойств.</span><span class="sxs-lookup"><span data-stu-id="31b19-117">The signature is generated using the SHA256 algorithm with a secret key on all the URL paths and properties.</span></span> <span data-ttu-id="31b19-118">Секретный ключ хранится как часть приложения логики в зашифрованном виде, никогда не раскрывается и не публикуется.</span><span class="sxs-lookup"><span data-stu-id="31b19-118">The secret key is never exposed and published, and is kept encrypted and stored as part of the logic app.</span></span> <span data-ttu-id="31b19-119">Приложение логики авторизует только те триггеры, которые содержат действительную подпись, созданную с помощью секретного ключа.</span><span class="sxs-lookup"><span data-stu-id="31b19-119">Your logic app only authorizes triggers that contain a valid signature created with the secret key.</span></span>

#### <a name="regenerate-access-keys"></a><span data-ttu-id="31b19-120">Повторное создание ключей доступа</span><span class="sxs-lookup"><span data-stu-id="31b19-120">Regenerate access keys</span></span>

<span data-ttu-id="31b19-121">Вы можете в любое время повторно создать ключ безопасности с помощью REST API или портала Azure.</span><span class="sxs-lookup"><span data-stu-id="31b19-121">You can regenerate a new secure key at anytime through the REST API or Azure portal.</span></span> <span data-ttu-id="31b19-122">Все текущие URL-адреса, созданные ранее с помощью старого ключа, станут недействительны, и их нельзя будет использовать для запуска приложения логики.</span><span class="sxs-lookup"><span data-stu-id="31b19-122">All current URLs that were generated previously using the old key are invalidated and no longer authorized to fire the logic app.</span></span>

1. <span data-ttu-id="31b19-123">На портале Azure откройте приложение логики, для которого необходимо повторно создать ключ.</span><span class="sxs-lookup"><span data-stu-id="31b19-123">In the Azure portal, open the logic app you want to regenerate a key</span></span>
1. <span data-ttu-id="31b19-124">В разделе **Параметры** щелкните пункт меню **Ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="31b19-124">Click the **Access Keys** menu item under **Settings**</span></span>
1. <span data-ttu-id="31b19-125">Выберите ключ, который необходимо создать повторно, и завершите процесс.</span><span class="sxs-lookup"><span data-stu-id="31b19-125">Choose the key to regenerate and complete the process</span></span>

<span data-ttu-id="31b19-126">URL-адреса, полученные после повторного создания, будут подписаны с помощью нового ключа доступа.</span><span class="sxs-lookup"><span data-stu-id="31b19-126">URLs you retrieve after regeneration are signed with the new access key.</span></span>

#### <a name="creating-callback-urls-with-an-expiration-date"></a><span data-ttu-id="31b19-127">Создание URL-адреса обратного вызова с истекшим сроком действия</span><span class="sxs-lookup"><span data-stu-id="31b19-127">Creating callback URLs with an expiration date</span></span>

<span data-ttu-id="31b19-128">Если URL-адрес используется совместно с другими участниками, можно создать URL-адреса с конкретными ключами и датами окончания срока действия.</span><span class="sxs-lookup"><span data-stu-id="31b19-128">If you are sharing the URL with other parties, you can generate URLs with specific keys and expiration dates as needed.</span></span> <span data-ttu-id="31b19-129">Это позволит легко изменять ключи и обеспечит ограничение на допуск к приложению в течение определенного интервала времени.</span><span class="sxs-lookup"><span data-stu-id="31b19-129">You can then seamlessly roll keys, or ensure access to fire an app is restricted to a certain timespan.</span></span> <span data-ttu-id="31b19-130">Вы можете задать дату окончания срока действия для URL-адреса с помощью [REST API для Logic Apps](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span><span class="sxs-lookup"><span data-stu-id="31b19-130">You can specify an expiration date for a URL through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="31b19-131">Добавьте свойство `NotAfter` в текст как строку даты JSON, возвращающую URL-адрес обратного вызова, который будет действителен только до даты и времени, заданных в параметре `NotAfter`.</span><span class="sxs-lookup"><span data-stu-id="31b19-131">In the body, include the property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until the `NotAfter` date and time.</span></span>

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a><span data-ttu-id="31b19-132">Создание URL-адресов с использованием первичного или вторичного секретного ключа</span><span class="sxs-lookup"><span data-stu-id="31b19-132">Creating URLs with primary or secondary secret key</span></span>

<span data-ttu-id="31b19-133">При создании или перечислении URL-адресов обратного вызова для триггеров на основе запросов можно указать ключ, который нужно использовать для подписи URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="31b19-133">When you generate or list callback URLs for request-based triggers, you can also specify which key to use to sign the URL.</span></span>  <span data-ttu-id="31b19-134">Вы можете создать URL-адрес, подписанный с использованием конкретного ключа, с помощью [REST API для Logic Apps](https://docs.microsoft.com/rest/api/logic/workflowtriggers) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="31b19-134">You can generate a URL signed by a specific key through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="31b19-135">Добавьте свойство `KeyType` в текст со значением `Primary` или `Secondary`.</span><span class="sxs-lookup"><span data-stu-id="31b19-135">In the body, include the property `KeyType` as either `Primary` or `Secondary`.</span></span>  <span data-ttu-id="31b19-136">В результате будет возвращен URL-адрес, подписанный с помощью указанного ключа безопасности.</span><span class="sxs-lookup"><span data-stu-id="31b19-136">This returns a URL signed by the secure key specified.</span></span>

### <a name="restrict-incoming-ip-addresses"></a><span data-ttu-id="31b19-137">Ограничение входящих IP-адресов</span><span class="sxs-lookup"><span data-stu-id="31b19-137">Restrict incoming IP addresses</span></span>

<span data-ttu-id="31b19-138">В дополнение к подписанному URL-адресу можно разрешить вызов приложения логики только конкретным клиентам.</span><span class="sxs-lookup"><span data-stu-id="31b19-138">In addition to the Shared Access Signature, you may wish to restrict calling a logic app only from specific clients.</span></span>  <span data-ttu-id="31b19-139">Например, если вы управляете своей конечной точкой с помощью управления API Azure, можно настроить приложение логики принимать только те запросы, которые поступают с IP-адреса экземпляра управления API.</span><span class="sxs-lookup"><span data-stu-id="31b19-139">For example, if you manage your endpoint through Azure API Management, you can restrict the logic app to only accept the request when the request comes from the API Management instance IP address.</span></span>

<span data-ttu-id="31b19-140">Этот параметр можно настроить в настройках приложения логики, выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="31b19-140">This setting can be configured within the logic app settings:</span></span>

1. <span data-ttu-id="31b19-141">На портале Azure откройте приложение логики, для которого необходимо добавить ограничения IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="31b19-141">In the Azure portal, open the logic app you want to add IP address restrictions</span></span>
1. <span data-ttu-id="31b19-142">В разделе **Параметры** щелкните пункт меню **Access control configuration** (Конфигурация контроля доступа).</span><span class="sxs-lookup"><span data-stu-id="31b19-142">Click the **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="31b19-143">Укажите список диапазонов IP-адресов, которые будет принимать триггер.</span><span class="sxs-lookup"><span data-stu-id="31b19-143">Specify the list of IP address ranges to be accepted by the trigger</span></span>

<span data-ttu-id="31b19-144">Допустимый диапазон IP-адресов имеет формат `192.168.1.1/255`.</span><span class="sxs-lookup"><span data-stu-id="31b19-144">A valid IP range takes the format `192.168.1.1/255`.</span></span> <span data-ttu-id="31b19-145">Если нужно запускать приложение логики только в виде вложенного приложения, установите параметр **Only other logic apps** (Только другие приложения логики).</span><span class="sxs-lookup"><span data-stu-id="31b19-145">If you want the logic app to only fire as a nested logic app, select the **Only other logic apps** option.</span></span> <span data-ttu-id="31b19-146">В ресурс будет записан пустой массив, а это означает, что будут запускаться только вызовы из самой службы (родительского приложения логики).</span><span class="sxs-lookup"><span data-stu-id="31b19-146">This option writes an empty array to the resource, meaning only calls from the service itself (parent logic apps) fire successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="31b19-147">Приложение логики с триггером запросов может по-прежнему выполняться с помощью REST API или управления API `/triggers/{triggerName}/run` независимо от IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="31b19-147">You can still run a logic app with a request trigger through the REST API / Management `/triggers/{triggerName}/run` regardless of IP.</span></span> <span data-ttu-id="31b19-148">Для этого потребуется аутентификация с помощью Azure REST API, а все события отобразятся в журнале аудита Azure.</span><span class="sxs-lookup"><span data-stu-id="31b19-148">This scenario requires authentication against the Azure REST API, and all events would appear in the Azure Audit Log.</span></span> <span data-ttu-id="31b19-149">Настройте политики контроля доступа соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="31b19-149">Set access control policies accordingly.</span></span>

#### <a name="setting-ip-ranges-on-the-resource-definition"></a><span data-ttu-id="31b19-150">Задание диапазонов IP-адресов в определении ресурсов</span><span class="sxs-lookup"><span data-stu-id="31b19-150">Setting IP ranges on the resource definition</span></span>

<span data-ttu-id="31b19-151">При использовании [шаблона развертывания](logic-apps-create-deploy-template.md) для автоматизации развертывания можно настроить параметры диапазона IP-адресов в шаблоне ресурсов.</span><span class="sxs-lookup"><span data-stu-id="31b19-151">If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.</span></span>  

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

### <a name="adding-azure-active-directory-oauth-or-other-security"></a><span data-ttu-id="31b19-152">Добавление Azure Active Directory, OAuth или других механизмов безопасности</span><span class="sxs-lookup"><span data-stu-id="31b19-152">Adding Azure Active Directory, OAuth, or other security</span></span>

<span data-ttu-id="31b19-153">Если нужно добавить дополнительные протоколы авторизации для приложения логики, используйте [управление API Azure](https://azure.microsoft.com/services/api-management/). Это обеспечит обширные возможности мониторинга, дополнительные средства безопасности, политики и документацию для любой конечной точки, а также возможность предоставлять приложение логики в качестве API.</span><span class="sxs-lookup"><span data-stu-id="31b19-153">To add more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with the capability to expose a logic app as an API.</span></span> <span data-ttu-id="31b19-154">Служба управления API Azure может предоставлять общедоступную или частную конечную точку для приложения логики, которая может использовать Azure Active Directory, сертификат, OAuth или другие методы безопасности.</span><span class="sxs-lookup"><span data-stu-id="31b19-154">Azure API Management can expose a public or private endpoint for the logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards.</span></span> <span data-ttu-id="31b19-155">После получения запроса служба управления API Azure пересылает запрос в приложение логики (выполняя все необходимые преобразования или ограничения на лету).</span><span class="sxs-lookup"><span data-stu-id="31b19-155">When a request is received, Azure API Management forwards the request to the logic app (performing any needed transformations or restrictions in-flight).</span></span> <span data-ttu-id="31b19-156">Чтобы разрешить приложению запускаться только с помощью управления API, можно использовать параметры диапазона входящих IP-адресов для приложения логики.</span><span class="sxs-lookup"><span data-stu-id="31b19-156">You can use the incoming IP range settings on the logic app to only allow the logic app to be triggered from API Management.</span></span>

## <a name="secure-access-to-manage-or-edit-logic-apps"></a><span data-ttu-id="31b19-157">Безопасный доступ для изменения приложений логики или управления ими</span><span class="sxs-lookup"><span data-stu-id="31b19-157">Secure access to manage or edit logic apps</span></span>

<span data-ttu-id="31b19-158">Можно ограничить доступ к операциям управления в приложении логики таким образом, чтобы только определенные пользователи или группы могли выполнять операции с ресурсом.</span><span class="sxs-lookup"><span data-stu-id="31b19-158">You can restrict access to management operations on a logic app so that only specific users or groups are able to perform operations on the resource.</span></span> <span data-ttu-id="31b19-159">Приложения логики используют функцию [управления доступом на основе ролей (RBAC)](../active-directory/role-based-access-control-configure.md) Azure, и их можно настроить с помощью тех же средств.</span><span class="sxs-lookup"><span data-stu-id="31b19-159">Logic apps use the Azure [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) feature, and can be customized with the same tools.</span></span>  <span data-ttu-id="31b19-160">Существует несколько встроенных ролей, которые также можно назначить членам подписки:</span><span class="sxs-lookup"><span data-stu-id="31b19-160">There are a few built-in roles you can assign members of your subscription to as well:</span></span>

* <span data-ttu-id="31b19-161">**Создатель приложений логики** — просмотр, редактирование и обновление приложения логики.</span><span class="sxs-lookup"><span data-stu-id="31b19-161">**Logic App Contributor** - Provides access to view, edit, and update a logic app.</span></span>  <span data-ttu-id="31b19-162">Эта роль не позволяет удалить ресурс или выполнять операции администрирования.</span><span class="sxs-lookup"><span data-stu-id="31b19-162">Cannot remove the resource or perform admin operations.</span></span>
* <span data-ttu-id="31b19-163">**Оператор приложений логики** — просмотр приложения логики и журнала выполнения, а также включение или отключение приложения.</span><span class="sxs-lookup"><span data-stu-id="31b19-163">**Logic App Operator** - Can view the logic app and run history, and enable/disable.</span></span>  <span data-ttu-id="31b19-164">Эта роль не позволяет изменять или обновлять определение.</span><span class="sxs-lookup"><span data-stu-id="31b19-164">Cannot edit or update the definition.</span></span>

<span data-ttu-id="31b19-165">Кроме того, можно использовать [блокировку ресурсов Azure](../azure-resource-manager/resource-group-lock-resources.md), чтобы предотвратить изменение или удаление приложений логики.</span><span class="sxs-lookup"><span data-stu-id="31b19-165">You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) to prevent changing or deleting logic apps.</span></span> <span data-ttu-id="31b19-166">Это позволяет предотвратить непреднамеренное изменение или удаление рабочих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="31b19-166">This capability is valuable to prevent production resources from changes or deletions.</span></span>

## <a name="secure-access-to-contents-of-the-run-history"></a><span data-ttu-id="31b19-167">Защита доступа к содержимому журнала выполнения</span><span class="sxs-lookup"><span data-stu-id="31b19-167">Secure access to contents of the run history</span></span>

<span data-ttu-id="31b19-168">Вы можете ограничить доступ к содержимому входных и выходных данных из предыдущих выполнений, разрешив его только для определенных диапазонов IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="31b19-168">You can restrict access to contents of inputs or outputs from previous runs to specific IP address ranges.</span></span>  

<span data-ttu-id="31b19-169">Все данные в рамках выполнения рабочего процесса шифруются при передаче и хранении.</span><span class="sxs-lookup"><span data-stu-id="31b19-169">All data within a workflow run is encrypted in transit and at rest.</span></span> <span data-ttu-id="31b19-170">После вызова журнала выполнения служба проверяет подлинность запроса и предоставляет ссылки на входные и выходные данные запроса и ответа.</span><span class="sxs-lookup"><span data-stu-id="31b19-170">When a call to run history is made, the service authenticates the request and provides links to the request and response inputs and outputs.</span></span> <span data-ttu-id="31b19-171">Ссылка может быть защищена таким образом, что возвращать содержимое будут только запросы на просмотр содержимого из указанного диапазона IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="31b19-171">This link can be protected so only requests to view content from a designated IP address range return the contents.</span></span> <span data-ttu-id="31b19-172">Эту возможность можно использовать в качестве дополнительного метода контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="31b19-172">You can use this capability for additional access control.</span></span> <span data-ttu-id="31b19-173">Можно также указать IP-адрес в виде `0.0.0.0`, тогда никто не сможет получить доступ к входным и выходным данным.</span><span class="sxs-lookup"><span data-stu-id="31b19-173">You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs.</span></span> <span data-ttu-id="31b19-174">Только пользователь с правами администратора может снять это ограничение и предоставить возможность JIT-доступа к содержимому рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="31b19-174">Only someone with admin permissions could remove this restriction, providing the possibility for 'just-in-time' access to workflow contents.</span></span>

<span data-ttu-id="31b19-175">Этот параметр можно настроить в параметрах ресурсов на портале Azure, выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="31b19-175">This setting can be configured within the resource settings of the Azure portal:</span></span>

1. <span data-ttu-id="31b19-176">На портале Azure откройте приложение логики, для которого необходимо добавить ограничения IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="31b19-176">In the Azure portal, open the logic app you want to add IP address restrictions</span></span>
1. <span data-ttu-id="31b19-177">В разделе **Параметры** щелкните пункт меню **Access control configuration** (Конфигурация контроля доступа).</span><span class="sxs-lookup"><span data-stu-id="31b19-177">Click the **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="31b19-178">Укажите список диапазонов IP-адресов для доступа к содержимому.</span><span class="sxs-lookup"><span data-stu-id="31b19-178">Specify the list of IP address ranges for access to content</span></span>

#### <a name="setting-ip-ranges-on-the-resource-definition"></a><span data-ttu-id="31b19-179">Задание диапазонов IP-адресов в определении ресурсов</span><span class="sxs-lookup"><span data-stu-id="31b19-179">Setting IP ranges on the resource definition</span></span>

<span data-ttu-id="31b19-180">При использовании [шаблона развертывания](logic-apps-create-deploy-template.md) для автоматизации развертывания можно настроить параметры диапазона IP-адресов в шаблоне ресурсов.</span><span class="sxs-lookup"><span data-stu-id="31b19-180">If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.</span></span>  

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

## <a name="secure-parameters-and-inputs-within-a-workflow"></a><span data-ttu-id="31b19-181">Параметры безопасности и входные данные в рабочем процессе</span><span class="sxs-lookup"><span data-stu-id="31b19-181">Secure parameters and inputs within a workflow</span></span>

<span data-ttu-id="31b19-182">При развертывании в разных средах для определения рабочего процесса может потребоваться задать некоторые параметры.</span><span class="sxs-lookup"><span data-stu-id="31b19-182">You might want to parameterize some aspects of a workflow definition for deployment across environments.</span></span> <span data-ttu-id="31b19-183">Это могут быть параметры безопасности, которые не должны отображаться при редактировании рабочего процесса, например идентификатор или секрет клиента для [аутентификации Azure Active Directory](../connectors/connectors-native-http.md#authentication) действия HTTP.</span><span class="sxs-lookup"><span data-stu-id="31b19-183">Also, some parameters might be secure parameters you don't want to appear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.</span></span>

### <a name="using-parameters-and-secure-parameters"></a><span data-ttu-id="31b19-184">Использование параметров и параметров безопасности</span><span class="sxs-lookup"><span data-stu-id="31b19-184">Using parameters and secure parameters</span></span>

<span data-ttu-id="31b19-185">[Язык определения рабочего процесса](http://aka.ms/logicappsdocs) предоставляет операцию `@parameters()` для доступа к значению параметра ресурса во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="31b19-185">To access the value of a resource parameter at runtime, the [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation.</span></span> <span data-ttu-id="31b19-186">Вы можете также [указать параметры в шаблоне развертывания ресурсов](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="31b19-186">Also, you can [specify parameters in the resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span></span> <span data-ttu-id="31b19-187">Если указать тип параметра `securestring`, он не будет возвращен с остальной частью определения ресурсов и не будет доступен при просмотре ресурса после развертывания.</span><span class="sxs-lookup"><span data-stu-id="31b19-187">But if you specify the parameter type as `securestring`, the parameter won't be returned with the rest of the resource definition, and won't be accessible by viewing the resource after deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="31b19-188">Если параметр используется в заголовках или тексте запроса, он может отображаться при доступе к журналу выполнения или исходящему HTTP-запросу.</span><span class="sxs-lookup"><span data-stu-id="31b19-188">If your parameter is used in the headers or body of a request, the parameter might be visible by accessing the run history and outgoing HTTP request.</span></span> <span data-ttu-id="31b19-189">Настройте политики доступа к содержимому соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="31b19-189">Make sure to set your content access policies accordingly.</span></span>
> <span data-ttu-id="31b19-190">Заголовки авторизации никогда не отображаются во входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="31b19-190">Authorization headers are never visible through inputs or outputs.</span></span> <span data-ttu-id="31b19-191">При использовании секрета в этих данных его нельзя будет извлечь.</span><span class="sxs-lookup"><span data-stu-id="31b19-191">So if the secret is being used there, the secret is not retrievable.</span></span>

#### <a name="resource-deployment-template-with-secrets"></a><span data-ttu-id="31b19-192">Шаблон развертывания ресурсов с использованием секретов</span><span class="sxs-lookup"><span data-stu-id="31b19-192">Resource deployment template with secrets</span></span>

<span data-ttu-id="31b19-193">Ниже приведен пример развертывания, который во время выполнения ссылается на безопасный параметр `secret`.</span><span class="sxs-lookup"><span data-stu-id="31b19-193">The following example shows a deployment that references a secure parameter of `secret` at runtime.</span></span> <span data-ttu-id="31b19-194">В отдельном файле параметров можно указать значения среды для `secret` или использовать [хранилище ключей Azure Resource Manager](../azure-resource-manager/resource-manager-keyvault-parameter.md) для получения секретов во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="31b19-194">In a separate parameters file, you could specify the environment value for the `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) to retrieve secrets at deploy time.</span></span>

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
                "body": "This is the request"
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

## <a name="secure-access-to-services-receiving-requests-from-a-workflow"></a><span data-ttu-id="31b19-195">Защита доступа к службам, которые получают запросы от рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="31b19-195">Secure access to services receiving requests from a workflow</span></span>

<span data-ttu-id="31b19-196">Существует множество способов защиты конечных точек, доступ к которым требуется приложению логики.</span><span class="sxs-lookup"><span data-stu-id="31b19-196">There are many ways to help secure any endpoint the logic app needs to access.</span></span>

### <a name="using-authentication-on-outbound-requests"></a><span data-ttu-id="31b19-197">Использование проверки подлинности при исходящих запросах</span><span class="sxs-lookup"><span data-stu-id="31b19-197">Using authentication on outbound requests</span></span>

<span data-ttu-id="31b19-198">При работе с HTTP, HTTP + Swagger (открытый API) или с действием webhook можно добавить проверку подлинности отправляемого запроса.</span><span class="sxs-lookup"><span data-stu-id="31b19-198">When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication to the request being sent.</span></span> <span data-ttu-id="31b19-199">Это может быть обычная аутентификация, аутентификация на основе сертификата или аутентификация Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="31b19-199">You could include basic authentication, certificate authentication, or Azure Active Directory authentication.</span></span> <span data-ttu-id="31b19-200">Дополнительные сведения о настройке проверки подлинности см. [в этой статье](../connectors/connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="31b19-200">Details on how to configure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).</span></span>

### <a name="restricting-access-to-logic-app-ip-addresses"></a><span data-ttu-id="31b19-201">Разрешение доступа для определенных IP-адресов приложения логики</span><span class="sxs-lookup"><span data-stu-id="31b19-201">Restricting access to logic app IP addresses</span></span>

<span data-ttu-id="31b19-202">Все вызовы из приложений логики поступают из определенного набора IP-адресов для каждого региона.</span><span class="sxs-lookup"><span data-stu-id="31b19-202">All calls from logic apps come from a specific set of IP addresses per region.</span></span> <span data-ttu-id="31b19-203">Можно добавить дополнительные фильтры, чтобы принимать запросы только из указанных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="31b19-203">You can add additional filtering to only accept requests from those designated IP addresses.</span></span> <span data-ttu-id="31b19-204">Список этих IP-адресов можно найти в статье [Ограничения и настройка приложений логики](logic-apps-limits-and-config.md#configuration).</span><span class="sxs-lookup"><span data-stu-id="31b19-204">For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).</span></span>

### <a name="on-premises-connectivity"></a><span data-ttu-id="31b19-205">Локальные возможности подключения</span><span class="sxs-lookup"><span data-stu-id="31b19-205">On-premises connectivity</span></span>

<span data-ttu-id="31b19-206">Приложения логики обеспечивают интеграцию с рядом служб для обеспечения безопасных и надежных локальных подключений.</span><span class="sxs-lookup"><span data-stu-id="31b19-206">Logic apps provide integration with several services to provide secure and reliable on-premises communication.</span></span>

#### <a name="on-premises-data-gateway"></a><span data-ttu-id="31b19-207">Локальный шлюз данных</span><span class="sxs-lookup"><span data-stu-id="31b19-207">On-premises data gateway</span></span>

<span data-ttu-id="31b19-208">Многие управляемые соединители для приложений логики предоставляют безопасное подключение к локальным системам, включая файловую систему, SQL, SharePoint, DB2 и другие.</span><span class="sxs-lookup"><span data-stu-id="31b19-208">Many managed connectors for logic apps provide secure connectivity to on-premises systems, including File System, SQL, SharePoint, DB2, and more.</span></span> <span data-ttu-id="31b19-209">Шлюз ретранслирует данные из локальных источников по шифрованным каналам через служебную шину Azure.</span><span class="sxs-lookup"><span data-stu-id="31b19-209">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="31b19-210">Весь трафик поступает как безопасный исходящий трафик от агента шлюза.</span><span class="sxs-lookup"><span data-stu-id="31b19-210">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="31b19-211">Дополнительные сведения см. в разделе [Как работает шлюз](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="31b19-211">Learn more about [how the data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span>

#### <a name="azure-api-management"></a><span data-ttu-id="31b19-212">Cлужба управления Azure API </span><span class="sxs-lookup"><span data-stu-id="31b19-212">Azure API Management</span></span>

<span data-ttu-id="31b19-213">[Служба управления API Azure](https://azure.microsoft.com/services/api-management/) имеет возможности локального подключения, включая VPN типа "сеть — сеть" и интеграцию ExpressRoute, для защищенного прокси-сервера и подключения к локальным системам.</span><span class="sxs-lookup"><span data-stu-id="31b19-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication to on-premises systems.</span></span> <span data-ttu-id="31b19-214">В конструкторе приложений логики можно быстро выбрать API, предоставляемый службой управления API в рамках рабочего процесса, который обеспечивает быстрый доступ к локальным системам.</span><span class="sxs-lookup"><span data-stu-id="31b19-214">In the Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access to on-premises systems.</span></span>

#### <a name="hybrid-connections-from-azure-app-service"></a><span data-ttu-id="31b19-215">Гибридные подключения из службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="31b19-215">Hybrid connections from Azure App Service</span></span>

<span data-ttu-id="31b19-216">Вы можете использовать локальное гибридное подключение для локальных подключений для Azure API и веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="31b19-216">You can use the on-premises hybrid connection feature for Azure API and Web apps to communicate on-premises.</span></span>  <span data-ttu-id="31b19-217">Дополнительные сведения о гибридных подключениях и их настройке см. [в этой статье](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="31b19-217">Details on hybrid connections and how to configure can be found [in this article](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="31b19-218">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="31b19-218">Next steps</span></span>
[<span data-ttu-id="31b19-219">Создание шаблона развертывания приложения логики</span><span class="sxs-lookup"><span data-stu-id="31b19-219">Create a deployment template</span></span>](logic-apps-create-deploy-template.md)  
[<span data-ttu-id="31b19-220">Обработка исключений</span><span class="sxs-lookup"><span data-stu-id="31b19-220">Exception handling</span></span>](logic-apps-exception-handling.md)  
[<span data-ttu-id="31b19-221">См. статью Мониторинг приложений логики.</span><span class="sxs-lookup"><span data-stu-id="31b19-221">Monitor your logic apps</span></span>](logic-apps-monitor-your-logic-apps.md)  
[<span data-ttu-id="31b19-222">Диагностика сбоев приложений логики</span><span class="sxs-lookup"><span data-stu-id="31b19-222">Diagnosing logic app failures and issues</span></span>](logic-apps-diagnosing-failures.md)  
