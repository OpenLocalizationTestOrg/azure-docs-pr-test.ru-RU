---
title: "aaaUse автомасштабирования действия toosend электронной почты и веб-перехватчика уведомлений о предупреждениях. | Документация Майкрософт"
description: "См. как toocall действий автомасштабирования toouse веб-URL-адреса или отправлять уведомления по электронной почте в мониторе Azure. "
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: eb9a4c98-0894-488c-8ee8-5df0065d094f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: ancav
ms.openlocfilehash: f611a18f5a808412fbdd0c89e3addb36437064c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-autoscale-actions-toosend-email-and-webhook-alert-notifications-in-azure-monitor"></a><span data-ttu-id="7923e-104">Используйте автомасштабирования действия toosend электронной почты и веб-перехватчика уведомлений о предупреждениях в мониторе Azure</span><span class="sxs-lookup"><span data-stu-id="7923e-104">Use autoscale actions toosend email and webhook alert notifications in Azure Monitor</span></span>
<span data-ttu-id="7923e-105">В этой статье показано, как настраиваются триггеры, позволяющие вам обращаться к определенным URL-адресам или отправлять сообщения электронной почты на основе действий автоматического масштабирования в Azure.</span><span class="sxs-lookup"><span data-stu-id="7923e-105">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span></span>  

## <a name="webhooks"></a><span data-ttu-id="7923e-106">Объекты Webhook</span><span class="sxs-lookup"><span data-stu-id="7923e-106">Webhooks</span></span>
<span data-ttu-id="7923e-107">Веб-Перехватчики позволяют tooroute hello Azure уведомления о предупреждениях tooother системы, после обработки или пользовательские уведомления.</span><span class="sxs-lookup"><span data-stu-id="7923e-107">Webhooks allow you tooroute hello Azure alert notifications tooother systems for post-processing or custom notifications.</span></span> <span data-ttu-id="7923e-108">Например маршрутизации tooservices предупреждения hello, которые могут обрабатывать входящие web запроса toosend SMS, журнал ошибок, уведомлять команды с помощью чата или служб обмена сообщениями, веб-перехватчика hello и т.д. URI должен быть действительной конечной точке HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7923e-108">For example, routing hello alert tooservices that can handle an incoming web request toosend SMS, log bugs, notify a team using chat or messaging services, etc. hello webhook URI must be a valid HTTP or HTTPS endpoint.</span></span>

## <a name="email"></a><span data-ttu-id="7923e-109">Email</span><span class="sxs-lookup"><span data-stu-id="7923e-109">Email</span></span>
<span data-ttu-id="7923e-110">Tooany допустимый адрес электронной почты могут отправляться по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="7923e-110">Email can be sent tooany valid email address.</span></span> <span data-ttu-id="7923e-111">Администраторы и соадминистраторы подписки hello, где запущено правило hello также получать уведомления.</span><span class="sxs-lookup"><span data-stu-id="7923e-111">Administrators and co-administrators of hello subscription where hello rule is running will also be notified.</span></span>

## <a name="cloud-services-and-web-apps"></a><span data-ttu-id="7923e-112">Облачные службы и веб-приложения</span><span class="sxs-lookup"><span data-stu-id="7923e-112">Cloud Services and Web Apps</span></span>
<span data-ttu-id="7923e-113">Можно включить в из hello портал Azure для облачных служб и ферм серверов (веб-приложений).</span><span class="sxs-lookup"><span data-stu-id="7923e-113">You can opt-in from hello Azure portal for Cloud Services and Server Farms (Web Apps).</span></span>

* <span data-ttu-id="7923e-114">Выберите hello **масштабирования по** метрику.</span><span class="sxs-lookup"><span data-stu-id="7923e-114">Choose hello **scale by** metric.</span></span>

![scale by (масштабировать по)](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="7923e-116">Наборы для масштабирования виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="7923e-116">Virtual Machine scale sets</span></span>
<span data-ttu-id="7923e-117">Для новых виртуальных машин, созданных с помощью Resource Manager, наборы для масштабирования можно настроить с помощью REST API, шаблонов Resource Manager, PowerShell и интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="7923e-117">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span></span> <span data-ttu-id="7923e-118">Интерфейс портала еще недоступен.</span><span class="sxs-lookup"><span data-stu-id="7923e-118">A portal interface is not yet available.</span></span>
<span data-ttu-id="7923e-119">При использовании hello API-интерфейса REST или шаблона диспетчера ресурсов, включите элемент уведомления hello hello следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="7923e-119">When using hello REST API or Resource Manager template, include hello notifications element with hello following options.</span></span>

```
"notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": false,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]
```
| <span data-ttu-id="7923e-120">Поле</span><span class="sxs-lookup"><span data-stu-id="7923e-120">Field</span></span> | <span data-ttu-id="7923e-121">Обязательное?</span><span class="sxs-lookup"><span data-stu-id="7923e-121">Mandatory?</span></span> | <span data-ttu-id="7923e-122">Описание</span><span class="sxs-lookup"><span data-stu-id="7923e-122">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7923e-123">операция</span><span class="sxs-lookup"><span data-stu-id="7923e-123">operation</span></span> |<span data-ttu-id="7923e-124">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-124">yes</span></span> |<span data-ttu-id="7923e-125">Значение должно быть Scale.</span><span class="sxs-lookup"><span data-stu-id="7923e-125">value must be "Scale"</span></span> |
| <span data-ttu-id="7923e-126">sendToSubscriptionAdministrator</span><span class="sxs-lookup"><span data-stu-id="7923e-126">sendToSubscriptionAdministrator</span></span> |<span data-ttu-id="7923e-127">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-127">yes</span></span> |<span data-ttu-id="7923e-128">Значение должно быть true или false.</span><span class="sxs-lookup"><span data-stu-id="7923e-128">value must be "true" or "false"</span></span> |
| <span data-ttu-id="7923e-129">sendToSubscriptionCoAdministrators</span><span class="sxs-lookup"><span data-stu-id="7923e-129">sendToSubscriptionCoAdministrators</span></span> |<span data-ttu-id="7923e-130">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-130">yes</span></span> |<span data-ttu-id="7923e-131">Значение должно быть true или false.</span><span class="sxs-lookup"><span data-stu-id="7923e-131">value must be "true" or "false"</span></span> |
| <span data-ttu-id="7923e-132">customEmails</span><span class="sxs-lookup"><span data-stu-id="7923e-132">customEmails</span></span> |<span data-ttu-id="7923e-133">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-133">yes</span></span> |<span data-ttu-id="7923e-134">Значение может быть null или массивом строк с адресами электронной почты.</span><span class="sxs-lookup"><span data-stu-id="7923e-134">value can be null [] or string array of emails</span></span> |
| <span data-ttu-id="7923e-135">Объекты Webhook</span><span class="sxs-lookup"><span data-stu-id="7923e-135">webhooks</span></span> |<span data-ttu-id="7923e-136">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-136">yes</span></span> |<span data-ttu-id="7923e-137">Значение может быть null или допустимым универсальным кодом ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="7923e-137">value can be null or valid Uri</span></span> |
| <span data-ttu-id="7923e-138">serviceUri</span><span class="sxs-lookup"><span data-stu-id="7923e-138">serviceUri</span></span> |<span data-ttu-id="7923e-139">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-139">yes</span></span> |<span data-ttu-id="7923e-140">Допустимый универсальный код ресурса (URI) HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7923e-140">a valid https Uri</span></span> |
| <span data-ttu-id="7923e-141">properties</span><span class="sxs-lookup"><span data-stu-id="7923e-141">properties</span></span> |<span data-ttu-id="7923e-142">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-142">yes</span></span> |<span data-ttu-id="7923e-143">Значение должно быть пустым {} или может содержать пары "ключ — значение".</span><span class="sxs-lookup"><span data-stu-id="7923e-143">value must be empty {} or can contain key-value pairs</span></span> |

## <a name="authentication-in-webhooks"></a><span data-ttu-id="7923e-144">Проверка подлинности в веб-перехватчиках</span><span class="sxs-lookup"><span data-stu-id="7923e-144">Authentication in webhooks</span></span>
<span data-ttu-id="7923e-145">веб-перехватчика Hello могут проходить проверку подлинности с помощью проверки подлинности на основе токенов, где сохранить веб-перехватчика hello URI с маркера идентификатор как параметр запроса.</span><span class="sxs-lookup"><span data-stu-id="7923e-145">hello webhook can authenticate using token-based authentication, where you save hello webhook URI with a token ID as a query parameter.</span></span> <span data-ttu-id="7923e-146">Например, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span><span class="sxs-lookup"><span data-stu-id="7923e-146">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span></span>

## <a name="autoscale-notification-webhook-payload-schema"></a><span data-ttu-id="7923e-147">Схема полезных данных веб-перехватчика уведомлений автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="7923e-147">Autoscale notification webhook payload schema</span></span>
<span data-ttu-id="7923e-148">При создании уведомлений автомасштабирования hello hello следующие метаданные входит в полезные данные веб-перехватчика hello:</span><span class="sxs-lookup"><span data-stu-id="7923e-148">When hello autoscale notification is generated, hello following metadata is included in hello webhook payload:</span></span>

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' toocapacity '2'",
                "subscriptionId": "s1",
                "resourceGroupName": "rg1",
                "resourceName": "MyCSRole",
                "resourceType": "microsoft.classiccompute/domainnames/slots/roles",
                "resourceId": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService/slots/Production/roles/MyCSRole",
                "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService",
                "oldCapacity": "3",
                "newCapacity": "2"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```


| <span data-ttu-id="7923e-149">Поле</span><span class="sxs-lookup"><span data-stu-id="7923e-149">Field</span></span> | <span data-ttu-id="7923e-150">Обязательное?</span><span class="sxs-lookup"><span data-stu-id="7923e-150">Mandatory?</span></span> | <span data-ttu-id="7923e-151">Описание</span><span class="sxs-lookup"><span data-stu-id="7923e-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7923e-152">status</span><span class="sxs-lookup"><span data-stu-id="7923e-152">status</span></span> |<span data-ttu-id="7923e-153">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-153">yes</span></span> |<span data-ttu-id="7923e-154">состояние Hello, которое указывает, что действие автоматического масштабирования была создана</span><span class="sxs-lookup"><span data-stu-id="7923e-154">hello status that indicates that an autoscale action was generated</span></span> |
| <span data-ttu-id="7923e-155">операция</span><span class="sxs-lookup"><span data-stu-id="7923e-155">operation</span></span> |<span data-ttu-id="7923e-156">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-156">yes</span></span> |<span data-ttu-id="7923e-157">Для увеличения экземпляров это будет "Развернуть", а для уменьшения экземпляров — "Свернуть"</span><span class="sxs-lookup"><span data-stu-id="7923e-157">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span></span> |
| <span data-ttu-id="7923e-158">context</span><span class="sxs-lookup"><span data-stu-id="7923e-158">context</span></span> |<span data-ttu-id="7923e-159">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-159">yes</span></span> |<span data-ttu-id="7923e-160">контекст действия автомасштабирования Hello</span><span class="sxs-lookup"><span data-stu-id="7923e-160">hello autoscale action context</span></span> |
| <span data-ttu-id="7923e-161">Timestamp</span><span class="sxs-lookup"><span data-stu-id="7923e-161">timestamp</span></span> |<span data-ttu-id="7923e-162">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-162">yes</span></span> |<span data-ttu-id="7923e-163">Метка времени, когда было запущено действие hello автоматического масштабирования</span><span class="sxs-lookup"><span data-stu-id="7923e-163">Time stamp when hello autoscale action was triggered</span></span> |
| <span data-ttu-id="7923e-164">id</span><span class="sxs-lookup"><span data-stu-id="7923e-164">id</span></span> |<span data-ttu-id="7923e-165">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-165">Yes</span></span> |<span data-ttu-id="7923e-166">Идентификатор диспетчера ресурсов параметра автомасштабирования hello</span><span class="sxs-lookup"><span data-stu-id="7923e-166">Resource Manager ID of hello autoscale setting</span></span> |
| <span data-ttu-id="7923e-167">name</span><span class="sxs-lookup"><span data-stu-id="7923e-167">name</span></span> |<span data-ttu-id="7923e-168">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-168">Yes</span></span> |<span data-ttu-id="7923e-169">Имя настройки автомасштабирования hello Hello</span><span class="sxs-lookup"><span data-stu-id="7923e-169">hello name of hello autoscale setting</span></span> |
| <span data-ttu-id="7923e-170">сведения</span><span class="sxs-lookup"><span data-stu-id="7923e-170">details</span></span> |<span data-ttu-id="7923e-171">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-171">Yes</span></span> |<span data-ttu-id="7923e-172">Описание действия hello, заняла службы автомасштабирования hello и hello изменение количества экземпляров hello</span><span class="sxs-lookup"><span data-stu-id="7923e-172">Explanation of hello action that hello autoscale service took and hello change in hello instance count</span></span> |
| <span data-ttu-id="7923e-173">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7923e-173">subscriptionId</span></span> |<span data-ttu-id="7923e-174">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-174">Yes</span></span> |<span data-ttu-id="7923e-175">Идентификатор подписки целевой ресурс hello, масштаб изменяется</span><span class="sxs-lookup"><span data-stu-id="7923e-175">Subscription ID of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="7923e-176">имя_группы_ресурсов</span><span class="sxs-lookup"><span data-stu-id="7923e-176">resourceGroupName</span></span> |<span data-ttu-id="7923e-177">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-177">Yes</span></span> |<span data-ttu-id="7923e-178">Имя группы ресурсов целевой ресурс hello, масштаб изменяется</span><span class="sxs-lookup"><span data-stu-id="7923e-178">Resource Group name of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="7923e-179">resourceName</span><span class="sxs-lookup"><span data-stu-id="7923e-179">resourceName</span></span> |<span data-ttu-id="7923e-180">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-180">Yes</span></span> |<span data-ttu-id="7923e-181">Имя ресурса целевой hello, масштаб изменяется</span><span class="sxs-lookup"><span data-stu-id="7923e-181">Name of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="7923e-182">тип_ресурса</span><span class="sxs-lookup"><span data-stu-id="7923e-182">resourceType</span></span> |<span data-ttu-id="7923e-183">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-183">Yes</span></span> |<span data-ttu-id="7923e-184">Здравствуйте, три поддерживаемые значения: «microsoft.classiccompute/domainnames/slots/roles» - ролей облачной службы «microsoft.compute/virtualmachinescalesets» - наборы масштабирования виртуальной машины и «Microsoft.Web/serverfarms» — веб-приложения</span><span class="sxs-lookup"><span data-stu-id="7923e-184">hello three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span></span> |
| <span data-ttu-id="7923e-185">resourceId</span><span class="sxs-lookup"><span data-stu-id="7923e-185">resourceId</span></span> |<span data-ttu-id="7923e-186">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-186">Yes</span></span> |<span data-ttu-id="7923e-187">Идентификатор целевого ресурса hello, масштабируется диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="7923e-187">Resource Manager ID of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="7923e-188">portalLink</span><span class="sxs-lookup"><span data-stu-id="7923e-188">portalLink</span></span> |<span data-ttu-id="7923e-189">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-189">Yes</span></span> |<span data-ttu-id="7923e-190">Ссылка на портал Azure toohello hello целевого ресурса "Сводка"</span><span class="sxs-lookup"><span data-stu-id="7923e-190">Azure portal link toohello summary page of hello target resource</span></span> |
| <span data-ttu-id="7923e-191">oldCapacity</span><span class="sxs-lookup"><span data-stu-id="7923e-191">oldCapacity</span></span> |<span data-ttu-id="7923e-192">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-192">Yes</span></span> |<span data-ttu-id="7923e-193">Hello текущего (старая) число экземпляров когда Автомасштабирование были действие масштабирования</span><span class="sxs-lookup"><span data-stu-id="7923e-193">hello current (old) instance count when Autoscale took a scale action</span></span> |
| <span data-ttu-id="7923e-194">newCapacity</span><span class="sxs-lookup"><span data-stu-id="7923e-194">newCapacity</span></span> |<span data-ttu-id="7923e-195">Да</span><span class="sxs-lookup"><span data-stu-id="7923e-195">Yes</span></span> |<span data-ttu-id="7923e-196">число экземпляров новый Hello, автомасштабирования слишком масштабировать hello ресурсов</span><span class="sxs-lookup"><span data-stu-id="7923e-196">hello new instance count that Autoscale scaled hello resource too</span></span>|
| <span data-ttu-id="7923e-197">Свойства</span><span class="sxs-lookup"><span data-stu-id="7923e-197">Properties</span></span> |<span data-ttu-id="7923e-198">Нет</span><span class="sxs-lookup"><span data-stu-id="7923e-198">No</span></span> |<span data-ttu-id="7923e-199">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="7923e-199">Optional.</span></span> <span data-ttu-id="7923e-200">Набор пар <ключ, значение> (например, Dictionary <String, String>).</span><span class="sxs-lookup"><span data-stu-id="7923e-200">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span></span> <span data-ttu-id="7923e-201">поле свойств Hello является необязательным.</span><span class="sxs-lookup"><span data-stu-id="7923e-201">hello properties field is optional.</span></span> <span data-ttu-id="7923e-202">Настраиваемый пользовательский интерфейс или логики приложения на основе рабочего процесса можно ввести ключи и значения, которые могут быть переданы в полезных данных hello.</span><span class="sxs-lookup"><span data-stu-id="7923e-202">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using hello payload.</span></span> <span data-ttu-id="7923e-203">Пользовательские свойства toopass резервное toohello исходящий вызов веб-перехватчика альтернативный способ — веб-перехватчика hello toouse URI себя (как параметры запроса)</span><span class="sxs-lookup"><span data-stu-id="7923e-203">An alternate way toopass custom properties back toohello outgoing webhook call is toouse hello webhook URI itself (as query parameters)</span></span> |
