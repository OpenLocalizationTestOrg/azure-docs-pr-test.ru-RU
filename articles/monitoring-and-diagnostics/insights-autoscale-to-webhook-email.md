---
title: "Использование действий автомасштабирования для отправки электронной почты и уведомлений об оповещениях веб-перехватчика. | Документация Майкрософт"
description: "Узнайте, как использовать действия автомасштабирования для вызова URL-адресов веб-сайтов или отправки уведомлений по электронной почте в Azure Monitor. "
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
ms.openlocfilehash: 16caf14028494800e9259f0296c292b606d0210a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-autoscale-actions-to-send-email-and-webhook-alert-notifications-in-azure-monitor"></a><span data-ttu-id="572a3-104">Использование действий автомасштабирования для отправки электронной почты и уведомлений об оповещениях веб-перехватчика в Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="572a3-104">Use autoscale actions to send email and webhook alert notifications in Azure Monitor</span></span>
<span data-ttu-id="572a3-105">В этой статье показано, как настраиваются триггеры, позволяющие вам обращаться к определенным URL-адресам или отправлять сообщения электронной почты на основе действий автоматического масштабирования в Azure.</span><span class="sxs-lookup"><span data-stu-id="572a3-105">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span></span>  

## <a name="webhooks"></a><span data-ttu-id="572a3-106">Объекты Webhook</span><span class="sxs-lookup"><span data-stu-id="572a3-106">Webhooks</span></span>
<span data-ttu-id="572a3-107">Объекты Webhook (веб-перехватчики) позволяют направлять уведомления об оповещениях Azure в другие системы для постобработки или отображения настраиваемых уведомлений.</span><span class="sxs-lookup"><span data-stu-id="572a3-107">Webhooks allow you to route the Azure alert notifications to other systems for post-processing or custom notifications.</span></span> <span data-ttu-id="572a3-108">Например, оповещения Azure могут направляться в службы, которые способны обрабатывать входящие веб-запросы для отправки SMS, ведения журналов, уведомления членов команды в чате или через службы обмена мгновенными сообщениями и т. д. Универсальный код ресурса (URI) веб-перехватчика должен быть допустимой конечной точкой HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="572a3-108">For example, routing the alert to services that can handle an incoming web request to send SMS, log bugs, notify a team using chat or messaging services, etc. The webhook URI must be a valid HTTP or HTTPS endpoint.</span></span>

## <a name="email"></a><span data-ttu-id="572a3-109">Email</span><span class="sxs-lookup"><span data-stu-id="572a3-109">Email</span></span>
<span data-ttu-id="572a3-110">Электронная почта может отправляться на любой допустимый адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="572a3-110">Email can be sent to any valid email address.</span></span> <span data-ttu-id="572a3-111">Также будут уведомляться администраторы и соадминистраторы подписки, где работает это правило.</span><span class="sxs-lookup"><span data-stu-id="572a3-111">Administrators and co-administrators of the subscription where the rule is running will also be notified.</span></span>

## <a name="cloud-services-and-web-apps"></a><span data-ttu-id="572a3-112">Облачные службы и веб-приложения</span><span class="sxs-lookup"><span data-stu-id="572a3-112">Cloud Services and Web Apps</span></span>
<span data-ttu-id="572a3-113">Вы можете явно согласиться на облачные службы и фермы серверов (веб-приложения) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="572a3-113">You can opt-in from the Azure portal for Cloud Services and Server Farms (Web Apps).</span></span>

* <span data-ttu-id="572a3-114">Выберите метрику **scale by (масштабировать по)** .</span><span class="sxs-lookup"><span data-stu-id="572a3-114">Choose the **scale by** metric.</span></span>

![scale by (масштабировать по)](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="572a3-116">Наборы для масштабирования виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="572a3-116">Virtual Machine scale sets</span></span>
<span data-ttu-id="572a3-117">Для новых виртуальных машин, созданных с помощью Resource Manager, наборы для масштабирования можно настроить с помощью REST API, шаблонов Resource Manager, PowerShell и интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="572a3-117">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span></span> <span data-ttu-id="572a3-118">Интерфейс портала еще недоступен.</span><span class="sxs-lookup"><span data-stu-id="572a3-118">A portal interface is not yet available.</span></span>
<span data-ttu-id="572a3-119">Если вы используете REST API или шаблон Resource Manager, включите элемент уведомлений с использованием следующих параметров:</span><span class="sxs-lookup"><span data-stu-id="572a3-119">When using the REST API or Resource Manager template, include the notifications element with the following options.</span></span>

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
| <span data-ttu-id="572a3-120">Поле</span><span class="sxs-lookup"><span data-stu-id="572a3-120">Field</span></span> | <span data-ttu-id="572a3-121">Обязательное?</span><span class="sxs-lookup"><span data-stu-id="572a3-121">Mandatory?</span></span> | <span data-ttu-id="572a3-122">Описание</span><span class="sxs-lookup"><span data-stu-id="572a3-122">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="572a3-123">операция</span><span class="sxs-lookup"><span data-stu-id="572a3-123">operation</span></span> |<span data-ttu-id="572a3-124">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-124">yes</span></span> |<span data-ttu-id="572a3-125">Значение должно быть Scale.</span><span class="sxs-lookup"><span data-stu-id="572a3-125">value must be "Scale"</span></span> |
| <span data-ttu-id="572a3-126">sendToSubscriptionAdministrator</span><span class="sxs-lookup"><span data-stu-id="572a3-126">sendToSubscriptionAdministrator</span></span> |<span data-ttu-id="572a3-127">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-127">yes</span></span> |<span data-ttu-id="572a3-128">Значение должно быть true или false.</span><span class="sxs-lookup"><span data-stu-id="572a3-128">value must be "true" or "false"</span></span> |
| <span data-ttu-id="572a3-129">sendToSubscriptionCoAdministrators</span><span class="sxs-lookup"><span data-stu-id="572a3-129">sendToSubscriptionCoAdministrators</span></span> |<span data-ttu-id="572a3-130">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-130">yes</span></span> |<span data-ttu-id="572a3-131">Значение должно быть true или false.</span><span class="sxs-lookup"><span data-stu-id="572a3-131">value must be "true" or "false"</span></span> |
| <span data-ttu-id="572a3-132">customEmails</span><span class="sxs-lookup"><span data-stu-id="572a3-132">customEmails</span></span> |<span data-ttu-id="572a3-133">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-133">yes</span></span> |<span data-ttu-id="572a3-134">Значение может быть null или массивом строк с адресами электронной почты.</span><span class="sxs-lookup"><span data-stu-id="572a3-134">value can be null [] or string array of emails</span></span> |
| <span data-ttu-id="572a3-135">Объекты Webhook</span><span class="sxs-lookup"><span data-stu-id="572a3-135">webhooks</span></span> |<span data-ttu-id="572a3-136">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-136">yes</span></span> |<span data-ttu-id="572a3-137">Значение может быть null или допустимым универсальным кодом ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="572a3-137">value can be null or valid Uri</span></span> |
| <span data-ttu-id="572a3-138">serviceUri</span><span class="sxs-lookup"><span data-stu-id="572a3-138">serviceUri</span></span> |<span data-ttu-id="572a3-139">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-139">yes</span></span> |<span data-ttu-id="572a3-140">Допустимый универсальный код ресурса (URI) HTTPS.</span><span class="sxs-lookup"><span data-stu-id="572a3-140">a valid https Uri</span></span> |
| <span data-ttu-id="572a3-141">properties</span><span class="sxs-lookup"><span data-stu-id="572a3-141">properties</span></span> |<span data-ttu-id="572a3-142">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-142">yes</span></span> |<span data-ttu-id="572a3-143">Значение должно быть пустым {} или может содержать пары "ключ — значение".</span><span class="sxs-lookup"><span data-stu-id="572a3-143">value must be empty {} or can contain key-value pairs</span></span> |

## <a name="authentication-in-webhooks"></a><span data-ttu-id="572a3-144">Проверка подлинности в веб-перехватчиках</span><span class="sxs-lookup"><span data-stu-id="572a3-144">Authentication in webhooks</span></span>
<span data-ttu-id="572a3-145">Для webhook может использоваться аутентификация на основе маркеров, заключающаяся в сохранении универсального кода ресурса (URI) webhook с идентификатором маркера в качестве параметра запроса.</span><span class="sxs-lookup"><span data-stu-id="572a3-145">The webhook can authenticate using token-based authentication, where you save the webhook URI with a token ID as a query parameter.</span></span> <span data-ttu-id="572a3-146">Например, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span><span class="sxs-lookup"><span data-stu-id="572a3-146">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span></span>

## <a name="autoscale-notification-webhook-payload-schema"></a><span data-ttu-id="572a3-147">Схема полезных данных веб-перехватчика уведомлений автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="572a3-147">Autoscale notification webhook payload schema</span></span>
<span data-ttu-id="572a3-148">При создании уведомлений автомасштабирования в полезные данные веб-перехватчика включаются следующие метаданные:</span><span class="sxs-lookup"><span data-stu-id="572a3-148">When the autoscale notification is generated, the following metadata is included in the webhook payload:</span></span>

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' to capacity '2'",
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


| <span data-ttu-id="572a3-149">Поле</span><span class="sxs-lookup"><span data-stu-id="572a3-149">Field</span></span> | <span data-ttu-id="572a3-150">Обязательное?</span><span class="sxs-lookup"><span data-stu-id="572a3-150">Mandatory?</span></span> | <span data-ttu-id="572a3-151">Описание</span><span class="sxs-lookup"><span data-stu-id="572a3-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="572a3-152">status</span><span class="sxs-lookup"><span data-stu-id="572a3-152">status</span></span> |<span data-ttu-id="572a3-153">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-153">yes</span></span> |<span data-ttu-id="572a3-154">Состояние, которое указывает, что создано действие автоматического масштабирования</span><span class="sxs-lookup"><span data-stu-id="572a3-154">The status that indicates that an autoscale action was generated</span></span> |
| <span data-ttu-id="572a3-155">операция</span><span class="sxs-lookup"><span data-stu-id="572a3-155">operation</span></span> |<span data-ttu-id="572a3-156">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-156">yes</span></span> |<span data-ttu-id="572a3-157">Для увеличения экземпляров это будет "Развернуть", а для уменьшения экземпляров — "Свернуть"</span><span class="sxs-lookup"><span data-stu-id="572a3-157">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span></span> |
| <span data-ttu-id="572a3-158">context</span><span class="sxs-lookup"><span data-stu-id="572a3-158">context</span></span> |<span data-ttu-id="572a3-159">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-159">yes</span></span> |<span data-ttu-id="572a3-160">Контекст действия автоматического масштабирования</span><span class="sxs-lookup"><span data-stu-id="572a3-160">The autoscale action context</span></span> |
| <span data-ttu-id="572a3-161">Timestamp</span><span class="sxs-lookup"><span data-stu-id="572a3-161">timestamp</span></span> |<span data-ttu-id="572a3-162">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-162">yes</span></span> |<span data-ttu-id="572a3-163">Отметка времени, когда было запущено действие автоматического масштабирования</span><span class="sxs-lookup"><span data-stu-id="572a3-163">Time stamp when the autoscale action was triggered</span></span> |
| <span data-ttu-id="572a3-164">id</span><span class="sxs-lookup"><span data-stu-id="572a3-164">id</span></span> |<span data-ttu-id="572a3-165">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-165">Yes</span></span> |<span data-ttu-id="572a3-166">Идентификатор Resource Manager для параметра автоматического масштабирования</span><span class="sxs-lookup"><span data-stu-id="572a3-166">Resource Manager ID of the autoscale setting</span></span> |
| <span data-ttu-id="572a3-167">name</span><span class="sxs-lookup"><span data-stu-id="572a3-167">name</span></span> |<span data-ttu-id="572a3-168">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-168">Yes</span></span> |<span data-ttu-id="572a3-169">Имя параметра автоматического масштабирования</span><span class="sxs-lookup"><span data-stu-id="572a3-169">The name of the autoscale setting</span></span> |
| <span data-ttu-id="572a3-170">сведения</span><span class="sxs-lookup"><span data-stu-id="572a3-170">details</span></span> |<span data-ttu-id="572a3-171">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-171">Yes</span></span> |<span data-ttu-id="572a3-172">Описание действия, предпринятого службой автоматического масштабирования, и изменение числа экземпляров</span><span class="sxs-lookup"><span data-stu-id="572a3-172">Explanation of the action that the autoscale service took and the change in the instance count</span></span> |
| <span data-ttu-id="572a3-173">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="572a3-173">subscriptionId</span></span> |<span data-ttu-id="572a3-174">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-174">Yes</span></span> |<span data-ttu-id="572a3-175">Идентификатор подписки для масштабируемого целевого ресурса</span><span class="sxs-lookup"><span data-stu-id="572a3-175">Subscription ID of the target resource that is being scaled</span></span> |
| <span data-ttu-id="572a3-176">имя_группы_ресурсов</span><span class="sxs-lookup"><span data-stu-id="572a3-176">resourceGroupName</span></span> |<span data-ttu-id="572a3-177">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-177">Yes</span></span> |<span data-ttu-id="572a3-178">Имя группы ресурсов для масштабируемого целевого ресурса</span><span class="sxs-lookup"><span data-stu-id="572a3-178">Resource Group name of the target resource that is being scaled</span></span> |
| <span data-ttu-id="572a3-179">resourceName</span><span class="sxs-lookup"><span data-stu-id="572a3-179">resourceName</span></span> |<span data-ttu-id="572a3-180">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-180">Yes</span></span> |<span data-ttu-id="572a3-181">Имя масштабируемого целевого ресурса</span><span class="sxs-lookup"><span data-stu-id="572a3-181">Name of the target resource that is being scaled</span></span> |
| <span data-ttu-id="572a3-182">тип_ресурса</span><span class="sxs-lookup"><span data-stu-id="572a3-182">resourceType</span></span> |<span data-ttu-id="572a3-183">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-183">Yes</span></span> |<span data-ttu-id="572a3-184">Поддерживается три значения: "microsoft.classiccompute/domainnames/slots/roles" — роли облачной службы, "microsoft.compute/virtualmachinescalesets" — наборы для масштабирования виртуальных машин и "Microsoft.Web/serverfarms" — веб-приложение</span><span class="sxs-lookup"><span data-stu-id="572a3-184">The three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span></span> |
| <span data-ttu-id="572a3-185">resourceId</span><span class="sxs-lookup"><span data-stu-id="572a3-185">resourceId</span></span> |<span data-ttu-id="572a3-186">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-186">Yes</span></span> |<span data-ttu-id="572a3-187">Идентификатор Resource Manager для масштабируемого целевого ресурса</span><span class="sxs-lookup"><span data-stu-id="572a3-187">Resource Manager ID of the target resource that is being scaled</span></span> |
| <span data-ttu-id="572a3-188">portalLink</span><span class="sxs-lookup"><span data-stu-id="572a3-188">portalLink</span></span> |<span data-ttu-id="572a3-189">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-189">Yes</span></span> |<span data-ttu-id="572a3-190">Ссылка на страницу сводки целевого ресурса на портале Azure</span><span class="sxs-lookup"><span data-stu-id="572a3-190">Azure portal link to the summary page of the target resource</span></span> |
| <span data-ttu-id="572a3-191">oldCapacity</span><span class="sxs-lookup"><span data-stu-id="572a3-191">oldCapacity</span></span> |<span data-ttu-id="572a3-192">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-192">Yes</span></span> |<span data-ttu-id="572a3-193">Текущее (старое) число экземпляров, когда автомасштабирование предпринимает действие масштабирования</span><span class="sxs-lookup"><span data-stu-id="572a3-193">The current (old) instance count when Autoscale took a scale action</span></span> |
| <span data-ttu-id="572a3-194">newCapacity</span><span class="sxs-lookup"><span data-stu-id="572a3-194">newCapacity</span></span> |<span data-ttu-id="572a3-195">Да</span><span class="sxs-lookup"><span data-stu-id="572a3-195">Yes</span></span> |<span data-ttu-id="572a3-196">Новое число экземпляров, до которого автомасштабирование масштабирует ресурс</span><span class="sxs-lookup"><span data-stu-id="572a3-196">The new instance count that Autoscale scaled the resource to</span></span> |
| <span data-ttu-id="572a3-197">properties</span><span class="sxs-lookup"><span data-stu-id="572a3-197">Properties</span></span> |<span data-ttu-id="572a3-198">Нет</span><span class="sxs-lookup"><span data-stu-id="572a3-198">No</span></span> |<span data-ttu-id="572a3-199">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="572a3-199">Optional.</span></span> <span data-ttu-id="572a3-200">Набор пар <ключ, значение> (например, Dictionary <String, String>).</span><span class="sxs-lookup"><span data-stu-id="572a3-200">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span></span> <span data-ttu-id="572a3-201">Поле свойства не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="572a3-201">The properties field is optional.</span></span> <span data-ttu-id="572a3-202">В настраиваемом пользовательском интерфейсе или рабочем процессе на основе приложения логики вы можете вводить ключи и значения для передачи в виде полезных данных.</span><span class="sxs-lookup"><span data-stu-id="572a3-202">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using the payload.</span></span> <span data-ttu-id="572a3-203">Еще один способ передачи пользовательских свойств обратно в исходящий вызов веб-перехватчика — использование самого универсального кода ресурса (URI) веб-перехватчика (в виде параметров запроса).</span><span class="sxs-lookup"><span data-stu-id="572a3-203">An alternate way to pass custom properties back to the outgoing webhook call is to use the webhook URI itself (as query parameters)</span></span> |
