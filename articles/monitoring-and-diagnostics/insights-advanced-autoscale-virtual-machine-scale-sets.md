---
title: "aaaAdvanced автоматического масштабирования с использованием виртуальных машин Azure | Документы Microsoft"
description: "Использование Resource Manager и Масштабируемых наборов ВМ с несколькими правилами и профилями, которые отправляют сообщения электронной почты и вызывают URL-адреса объектов webhook с действиями масштабирования."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 7e3576e2-4a2b-4736-b5ae-98c4689cdd2b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2016
ms.author: ancav
ms.openlocfilehash: ecb01e3094f715837b75ef07a7dbecdf0f2e78f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a><span data-ttu-id="0821e-103">Расширенная настройка автомасштабирования с помощью шаблонов Resource Manager для набора масштабирования виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="0821e-103">Advanced autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>
<span data-ttu-id="0821e-104">Масштабируемые наборы виртуальных машин можно свертывать и развертывать на основе пороговых значений метрик производительности по расписанию или на определенную дату.</span><span class="sxs-lookup"><span data-stu-id="0821e-104">You can scale-in and scale-out in Virtual Machine Scale Sets based on performance metric thresholds, by a recurring schedule, or by a particular date.</span></span> <span data-ttu-id="0821e-105">Можно также настроить уведомления с помощью электронной почты и webhook для действий масштабирования.</span><span class="sxs-lookup"><span data-stu-id="0821e-105">You can also configure email and webhook notifications for scale actions.</span></span> <span data-ttu-id="0821e-106">В этом пошаговом руководстве показан пример настройки всех этих объектов для масштабируемого набора виртуальных машин с помощью шаблона Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0821e-106">This walkthrough shows an example of configuring all these objects using a Resource Manager template on a VM Scale Set.</span></span>

> [!NOTE]
> <span data-ttu-id="0821e-107">Хотя в этом пошаговом руководстве описаны шаги hello для набора масштабирования виртуальных Машин, hello же информация относится tooautoscaling [облачные службы](https://azure.microsoft.com/services/cloud-services/), и [службы приложений — веб-приложений](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="0821e-107">While this walkthrough explains hello steps for VM Scale Sets, hello same information applies tooautoscaling [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span>
> <span data-ttu-id="0821e-108">Простой шкале in/out параметр в наборе масштабирования виртуальных Машин на основании метрики производительности простой как ЦП, описаны в toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) и [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) документов</span><span class="sxs-lookup"><span data-stu-id="0821e-108">For a simple scale in/out setting on a VM Scale Set based on a simple performance metric such as CPU, refer toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) and [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents</span></span>
>
>

## <a name="walkthrough"></a><span data-ttu-id="0821e-109">Пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="0821e-109">Walkthrough</span></span>
<span data-ttu-id="0821e-110">В этом пошаговом руководстве мы используем [обозревателя ресурсов Azure](https://resources.azure.com/) tooconfigure и обновления параметров автоматического масштабирования hello для набора масштабирования.</span><span class="sxs-lookup"><span data-stu-id="0821e-110">In this walkthrough, we use [Azure Resource Explorer](https://resources.azure.com/) tooconfigure and update hello autoscale setting for a scale set.</span></span> <span data-ttu-id="0821e-111">Azure обозреватель ресурсов — простой способ toomanage ресурсы Azure через шаблоны диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0821e-111">Azure Resource Explorer is an easy way toomanage Azure resources via Resource Manager templates.</span></span> <span data-ttu-id="0821e-112">Новое средство обозревателя ресурсов tooAzure, прочитайте [вводном разделе](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span><span class="sxs-lookup"><span data-stu-id="0821e-112">If you are new tooAzure Resource Explorer tool, read [this introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span></span>

1. <span data-ttu-id="0821e-113">Разверните новый набор масштабирования с базовой конфигурацией автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="0821e-113">Deploy a new scale set with a basic autoscale setting.</span></span> <span data-ttu-id="0821e-114">В этой статье используется hello один из коллекции Azure краткое руководство, имеющая Windows hello в наборе с помощью шаблона основные автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="0821e-114">This article uses hello one from hello Azure QuickStart Gallery, which has a Windows scale set with a basic autoscale template.</span></span> <span data-ttu-id="0821e-115">Масштаб Linux задает hello рабочих таким же образом.</span><span class="sxs-lookup"><span data-stu-id="0821e-115">Linux scale sets work hello same way.</span></span>
2. <span data-ttu-id="0821e-116">После создания набора масштабирования hello перейдите toohello шкалы набор ресурсов из обозревателя ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="0821e-116">After hello scale set is created, navigate toohello scale set resource from Azure Resource Explorer.</span></span> <span data-ttu-id="0821e-117">Вы увидите следующее hello в узле с помощью Microsoft.Insights.</span><span class="sxs-lookup"><span data-stu-id="0821e-117">You see hello following under Microsoft.Insights node.</span></span>

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    <span data-ttu-id="0821e-119">выполнения шаблона Hello создал автомасштабирования по умолчанию с именем hello **«autoscalewad»**.</span><span class="sxs-lookup"><span data-stu-id="0821e-119">hello template execution has created a default autoscale setting with hello name **'autoscalewad'**.</span></span> <span data-ttu-id="0821e-120">На правой стороне hello можно просмотреть hello полное определение этого параметра автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="0821e-120">On hello right-hand side, you can view hello full definition of this autoscale setting.</span></span> <span data-ttu-id="0821e-121">В этом случае по умолчанию автомасштабирования hello поставляется с правила масштабирования и масштабирования в основе % ЦП.</span><span class="sxs-lookup"><span data-stu-id="0821e-121">In this case, hello default autoscale setting comes with a CPU% based scale-out and scale-in rule.</span></span>  

3. <span data-ttu-id="0821e-122">Теперь можно добавить дополнительные профили и правила на основе расписания hello или конкретных требований.</span><span class="sxs-lookup"><span data-stu-id="0821e-122">You can now add more profiles and rules based on hello schedule or specific requirements.</span></span> <span data-ttu-id="0821e-123">Мы создадим конфигурацию автомасштабирования с тремя профилями.</span><span class="sxs-lookup"><span data-stu-id="0821e-123">We create an autoscale setting with three profiles.</span></span> <span data-ttu-id="0821e-124">профили toounderstand и правила в автоматического масштабирования, просмотрите [автомасштабирования рекомендации](insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="0821e-124">toounderstand profiles and rules in autoscale, review [Autoscale Best Practices](insights-autoscale-best-practices.md).</span></span>  

    | <span data-ttu-id="0821e-125">Профили и правила</span><span class="sxs-lookup"><span data-stu-id="0821e-125">Profiles & Rules</span></span> | <span data-ttu-id="0821e-126">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="0821e-126">Description</span></span> |
    |--- | --- |
    | <span data-ttu-id="0821e-127">**Профиль**</span><span class="sxs-lookup"><span data-stu-id="0821e-127">**Profile**</span></span> |<span data-ttu-id="0821e-128">**На основе производительности или метрики**</span><span class="sxs-lookup"><span data-stu-id="0821e-128">**Performance/metric based**</span></span> |
    | <span data-ttu-id="0821e-129">правило;</span><span class="sxs-lookup"><span data-stu-id="0821e-129">Rule</span></span> |<span data-ttu-id="0821e-130">Количество сообщений в очереди служебной шины > x</span><span class="sxs-lookup"><span data-stu-id="0821e-130">Service Bus Queue Message Count > x</span></span> |
    | <span data-ttu-id="0821e-131">правило;</span><span class="sxs-lookup"><span data-stu-id="0821e-131">Rule</span></span> |<span data-ttu-id="0821e-132">Количество сообщений в очереди служебной шины < y</span><span class="sxs-lookup"><span data-stu-id="0821e-132">Service Bus Queue Message Count < y</span></span> |
    | <span data-ttu-id="0821e-133">правило;</span><span class="sxs-lookup"><span data-stu-id="0821e-133">Rule</span></span> |<span data-ttu-id="0821e-134">% загрузки ЦП > n</span><span class="sxs-lookup"><span data-stu-id="0821e-134">CPU% > n</span></span> |
    | <span data-ttu-id="0821e-135">правило;</span><span class="sxs-lookup"><span data-stu-id="0821e-135">Rule</span></span> |<span data-ttu-id="0821e-136">% загрузки ЦП < p</span><span class="sxs-lookup"><span data-stu-id="0821e-136">CPU% < p</span></span> |
    | <span data-ttu-id="0821e-137">**Профиль**</span><span class="sxs-lookup"><span data-stu-id="0821e-137">**Profile**</span></span> |<span data-ttu-id="0821e-138">**Утренние часы в рабочие дни (без правил)**</span><span class="sxs-lookup"><span data-stu-id="0821e-138">**Weekday morning hours (no rules)**</span></span> |
    | <span data-ttu-id="0821e-139">**Профиль**</span><span class="sxs-lookup"><span data-stu-id="0821e-139">**Profile**</span></span> |<span data-ttu-id="0821e-140">**День запуска продукта (без правил)**</span><span class="sxs-lookup"><span data-stu-id="0821e-140">**Product Launch day (no rules)**</span></span> |

4. <span data-ttu-id="0821e-141">Ниже приведен гипотетический сценарий масштабирования, который используется в данном пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="0821e-141">Here is a hypothetical scaling scenario that we use for this walk-through.</span></span>

    * <span data-ttu-id="0821e-142">**На основе нагрузки** -как tooscale out или в зависимости от нагрузки hello в тестируемом приложении, размещенных на мой set.* шкалы</span><span class="sxs-lookup"><span data-stu-id="0821e-142">**Load based** - I'd like tooscale out or in based on hello load on my application hosted on my scale set.*</span></span>
    * <span data-ttu-id="0821e-143">**Размер очереди сообщения** -использовать очередь служебной шины для hello входящих сообщений toomy приложения.</span><span class="sxs-lookup"><span data-stu-id="0821e-143">**Message Queue size** - I use a Service Bus Queue for hello incoming messages toomy application.</span></span> <span data-ttu-id="0821e-144">Я использую количество сообщений в очереди hello и % ЦП и настройка tootrigger профиля по умолчанию действие масштабирования, если число сообщений или ЦП попаданий hello threshold.*</span><span class="sxs-lookup"><span data-stu-id="0821e-144">I use hello queue's message count and CPU% and configure a default profile tootrigger a scale action if either of message count or CPU hits hello threshold.*</span></span>
    * <span data-ttu-id="0821e-145">**Время недели и дня** -требуется еженедельного повторения «время дня hello» на основе профиля называется «Часов утра рабочего дня».</span><span class="sxs-lookup"><span data-stu-id="0821e-145">**Time of week and day** - I want a weekly recurring 'time of hello day' based profile called 'Weekday Morning Hours'.</span></span> <span data-ttu-id="0821e-146">На основе исторических данных, я знаю, что это лучше toohave уверенности, что количество виртуальных Машин экземпляров toohandle нагрузки моего приложения во время этого time.*</span><span class="sxs-lookup"><span data-stu-id="0821e-146">Based on historical data, I know it is better toohave certain number of VM instances toohandle my application's load during this time.*</span></span>
    * <span data-ttu-id="0821e-147">**Особые даты** — добавлен профиль "День запуска продукта".</span><span class="sxs-lookup"><span data-stu-id="0821e-147">**Special Dates** - I added a 'Product Launch Day' profile.</span></span> <span data-ttu-id="0821e-148">Я заранее определенных дат что мое приложение готово toohandle hello нагрузки из-за объявления маркетинга и когда мы поместили новый продукт hello application.*</span><span class="sxs-lookup"><span data-stu-id="0821e-148">I plan ahead for specific dates so my application is ready toohandle hello load due marketing announcements and when we put a new product in hello application.*</span></span>
    * <span data-ttu-id="0821e-149">*Hello двух последних профили могут также иметь другие метрики на основе правила производительности в них. В этом случае я решил не toohave один, и вместо этого правила на основе toorely на метрики производительности по умолчанию hello. Правила являются необязательными для hello повторяющейся основе даты и профили.*</span><span class="sxs-lookup"><span data-stu-id="0821e-149">*hello last two profiles can also have other performance metric based rules within them. In this case, I decided not toohave one and instead toorely on hello default performance metric based rules. Rules are optional for hello recurring and date-based profiles.*</span></span>

    <span data-ttu-id="0821e-150">Приоритетов автомасштабирования engine профилей hello и правила также фиксируется при hello [автоматическое масштабирование рекомендации](insights-autoscale-best-practices.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="0821e-150">Autoscale engine's prioritization of hello profiles and rules is also captured in hello [autoscaling best practices](insights-autoscale-best-practices.md) article.</span></span>
    <span data-ttu-id="0821e-151">Список стандартных метрик для автомасштабирования см. в статье [Общие метрики автомасштабирования Azure Insights](insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="0821e-151">For a list of common metrics for autoscale, refer [Common metrics for Autoscale](insights-autoscale-common-metrics.md)</span></span>

5. <span data-ttu-id="0821e-152">Убедитесь, что вы используете hello **чтения и записи** режим в обозревателе ресурсов</span><span class="sxs-lookup"><span data-stu-id="0821e-152">Make sure you are on hello **Read/Write** mode in Resource Explorer</span></span>

    ![Autoscalewad, конфигурация автомасштабирования по умолчанию](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. <span data-ttu-id="0821e-154">Нажмите кнопку «Изменить».</span><span class="sxs-lookup"><span data-stu-id="0821e-154">Click Edit.</span></span> <span data-ttu-id="0821e-155">**Замените** элемент hello «профили» в заданной настройке автомасштабирования с hello следующая конфигурация:</span><span class="sxs-lookup"><span data-stu-id="0821e-155">**Replace** hello 'profiles' element in autoscale setting with hello following configuration:</span></span>

    ![профили](./media/insights-advanced-autoscale-vmss/profiles.png)

    ```
    {
            "name": "Perf_Based_Scale",
            "capacity": {
              "minimum": "2",
              "maximum": "12",
              "default": "2"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 10
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 3
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 85
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          },
          {
            "name": "Weekday_Morning_Hours_Scale",
            "capacity": {
              "minimum": "4",
              "maximum": "12",
              "default": "4"
            },
            "rules": [],
            "recurrence": {
              "frequency": "Week",
              "schedule": {
                "timeZone": "Pacific Standard Time",
                "days": [
                  "Monday",
                  "Tuesday",
                  "Wednesday",
                  "Thursday",
                  "Friday"
                ],
                "hours": [
                  6
                ],
                "minutes": [
                  0
                ]
              }
            }
          },
          {
            "name": "Product_Launch_Day",
            "capacity": {
              "minimum": "6",
              "maximum": "20",
              "default": "6"
            },
            "rules": [],
            "fixedDate": {
              "timeZone": "Pacific Standard Time",
              "start": "2016-06-20T00:06:00Z",
              "end": "2016-06-21T23:59:00Z"
            }
          }
    ```
    <span data-ttu-id="0821e-157">Описание поддерживаемых полей и их значений см. в [документации по REST API автомасштабирования](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="0821e-157">For supported fields and their values, see [Autoscale REST API documentation](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span></span> <span data-ttu-id="0821e-158">Теперь параметры автомасштабирования содержит три профиля hello описан ранее.</span><span class="sxs-lookup"><span data-stu-id="0821e-158">Now your autoscale setting contains hello three profiles explained previously.</span></span>

7. <span data-ttu-id="0821e-159">Наконец, просмотрите hello автомасштабирования **уведомления** раздела.</span><span class="sxs-lookup"><span data-stu-id="0821e-159">Finally, look at hello Autoscale **notification** section.</span></span> <span data-ttu-id="0821e-160">Автомасштабирование уведомлений позволяют toodo три действия, когда к масштабному развертыванию или в действие успешно запущено.</span><span class="sxs-lookup"><span data-stu-id="0821e-160">Autoscale notifications allow you toodo three things when a scale-out or in action is successfully triggered.</span></span>
   - <span data-ttu-id="0821e-161">Уведомлять об Здравствуйте, администратор и соадминистраторы подписки</span><span class="sxs-lookup"><span data-stu-id="0821e-161">Notify hello admin and co-admins of your subscription</span></span>
   - <span data-ttu-id="0821e-162">от править электронное сообщение набору пользователей;</span><span class="sxs-lookup"><span data-stu-id="0821e-162">Email a set of users</span></span>
   - <span data-ttu-id="0821e-163">активировать вызов webhook.</span><span class="sxs-lookup"><span data-stu-id="0821e-163">Trigger a webhook call.</span></span> <span data-ttu-id="0821e-164">При создании этого веб-перехватчика отправляет метаданные об условии автоматическое масштабирование hello и задать масштаб hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0821e-164">When fired, this webhook sends metadata about hello autoscaling condition and hello scale set resource.</span></span> <span data-ttu-id="0821e-165">toolearn Дополнительные сведения о полезных данных hello автомасштабирования веб-перехватчика, в разделе [настроить веб-перехватчика & уведомления по электронной почте для автомасштабирования](insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="0821e-165">toolearn more about hello payload of autoscale webhook, see [Configure Webhook & Email Notifications for Autoscale](insights-autoscale-to-webhook-email.md).</span></span>

   <span data-ttu-id="0821e-166">Добавить после замены параметра автомасштабирования toohello hello вашей **уведомления** элемент, значение которого равно null</span><span class="sxs-lookup"><span data-stu-id="0821e-166">Add hello following toohello Autoscale setting replacing your **notification** element whose value is null</span></span>

   ```
   "notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": true,
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

   <span data-ttu-id="0821e-167">Попаданий **поместить** кнопку в настройке автомасштабирования hello tooupdate обозреватель ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0821e-167">Hit **Put** button in Resource Explorer tooupdate hello autoscale setting.</span></span>

<span data-ttu-id="0821e-168">Обновили параметр на tooinclude набор масштабирования виртуальных Машин нескольких профилей масштабирования автомасштабирования и масштабировать уведомления.</span><span class="sxs-lookup"><span data-stu-id="0821e-168">You have updated an autoscale setting on a VM Scale set tooinclude multiple scale profiles and scale notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0821e-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0821e-169">Next Steps</span></span>
<span data-ttu-id="0821e-170">Используйте эти ссылки toolearn Дополнительные сведения об автоматическом масштабировании.</span><span class="sxs-lookup"><span data-stu-id="0821e-170">Use these links toolearn more about autoscaling.</span></span>

[<span data-ttu-id="0821e-171">Устранение неполадок при автомасштабировании масштабируемых наборов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="0821e-171">TroubleShoot Autoscale with Virtual Machine Scale Sets</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[<span data-ttu-id="0821e-172">Общие метрики автомасштабирования Azure Insights</span><span class="sxs-lookup"><span data-stu-id="0821e-172">Common Metrics for Autoscale</span></span>](insights-autoscale-common-metrics.md)

[<span data-ttu-id="0821e-173">Рекомендации по автомасштабированию Azure Insights</span><span class="sxs-lookup"><span data-stu-id="0821e-173">Best Practices for Azure Autoscale</span></span>](insights-autoscale-best-practices.md)

[<span data-ttu-id="0821e-174">Создание параметров автомасштабирования и управление ими</span><span class="sxs-lookup"><span data-stu-id="0821e-174">Manage Autoscale using PowerShell</span></span>](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[<span data-ttu-id="0821e-175">Автомасштабирование</span><span class="sxs-lookup"><span data-stu-id="0821e-175">Manage Autoscale using CLI</span></span>](insights-cli-samples.md#autoscale)

[<span data-ttu-id="0821e-176">Использование действий автомасштабирования для отправки электронной почты и уведомлений об оповещениях веб-перехватчика в Azure Insights</span><span class="sxs-lookup"><span data-stu-id="0821e-176">Configure Webhook & Email Notifications for Autoscale</span></span>](insights-autoscale-to-webhook-email.md)
