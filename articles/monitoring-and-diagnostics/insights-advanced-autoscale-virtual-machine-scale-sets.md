---
title: "Расширенное автомасштабирование с помощью виртуальных машин Azure | Документация Майкрософт"
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
ms.openlocfilehash: 80955535c8d863cd3d8d1b77e2ab8bc016b6d9f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a><span data-ttu-id="6c509-103">Расширенная настройка автомасштабирования с помощью шаблонов Resource Manager для набора масштабирования виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="6c509-103">Advanced autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>
<span data-ttu-id="6c509-104">Масштабируемые наборы виртуальных машин можно свертывать и развертывать на основе пороговых значений метрик производительности по расписанию или на определенную дату.</span><span class="sxs-lookup"><span data-stu-id="6c509-104">You can scale-in and scale-out in Virtual Machine Scale Sets based on performance metric thresholds, by a recurring schedule, or by a particular date.</span></span> <span data-ttu-id="6c509-105">Можно также настроить уведомления с помощью электронной почты и webhook для действий масштабирования.</span><span class="sxs-lookup"><span data-stu-id="6c509-105">You can also configure email and webhook notifications for scale actions.</span></span> <span data-ttu-id="6c509-106">В этом пошаговом руководстве показан пример настройки всех этих объектов для масштабируемого набора виртуальных машин с помощью шаблона Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6c509-106">This walkthrough shows an example of configuring all these objects using a Resource Manager template on a VM Scale Set.</span></span>

> [!NOTE]
> <span data-ttu-id="6c509-107">Хотя в этом пошаговом руководстве приведены сведения для масштабируемых наборов виртуальных машин, их можно применить и для автомасштабирования [облачных служб](https://azure.microsoft.com/services/cloud-services/) и [веб-приложений службы приложений](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="6c509-107">While this walkthrough explains the steps for VM Scale Sets, the same information applies to autoscaling [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span>
> <span data-ttu-id="6c509-108">Простые параметры масштабирования набора масштабирования виртуальных машин, основанные на простой метрике производительности, например метрике ЦП, описаны в документации по [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) и [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="6c509-108">For a simple scale in/out setting on a VM Scale Set based on a simple performance metric such as CPU, refer to the [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) and [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents</span></span>
>
>

## <a name="walkthrough"></a><span data-ttu-id="6c509-109">Пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="6c509-109">Walkthrough</span></span>
<span data-ttu-id="6c509-110">В этом пошаговом руководстве для настройки и обновления конфигурации автомасштабирования набора масштабирования используется [Azure Resource Explorer](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6c509-110">In this walkthrough, we use [Azure Resource Explorer](https://resources.azure.com/) to configure and update the autoscale setting for a scale set.</span></span> <span data-ttu-id="6c509-111">Azure Resource Explorer — простой инструмент управления ресурсами Azure с помощью шаблонов Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6c509-111">Azure Resource Explorer is an easy way to manage Azure resources via Resource Manager templates.</span></span> <span data-ttu-id="6c509-112">Если вы еще не работали с Azure Resource Explorer, ознакомьтесь с [этой информацией](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span><span class="sxs-lookup"><span data-stu-id="6c509-112">If you are new to Azure Resource Explorer tool, read [this introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span></span>

1. <span data-ttu-id="6c509-113">Разверните новый набор масштабирования с базовой конфигурацией автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="6c509-113">Deploy a new scale set with a basic autoscale setting.</span></span> <span data-ttu-id="6c509-114">В этой статье используется конфигурация из коллекции быстрого запуска Azure, в которой есть набор масштабирования Windows с базовым шаблоном автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="6c509-114">This article uses the one from the Azure QuickStart Gallery, which has a Windows scale set with a basic autoscale template.</span></span> <span data-ttu-id="6c509-115">Наборы масштабирования Linux работают точно так же.</span><span class="sxs-lookup"><span data-stu-id="6c509-115">Linux scale sets work the same way.</span></span>
2. <span data-ttu-id="6c509-116">После создания набора масштабирования перейдите к его ресурсу из Azure Resource Explorer.</span><span class="sxs-lookup"><span data-stu-id="6c509-116">After the scale set is created, navigate to the scale set resource from Azure Resource Explorer.</span></span> <span data-ttu-id="6c509-117">Под узлом Microsoft.Insights вы увидите следующую структуру.</span><span class="sxs-lookup"><span data-stu-id="6c509-117">You see the following under Microsoft.Insights node.</span></span>

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    <span data-ttu-id="6c509-119">С помощью шаблона была создана конфигурация автомасштабирования по умолчанию **autoscalewad**.</span><span class="sxs-lookup"><span data-stu-id="6c509-119">The template execution has created a default autoscale setting with the name **'autoscalewad'**.</span></span> <span data-ttu-id="6c509-120">Справа можно просмотреть полное определение этой конфигурации автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="6c509-120">On the right-hand side, you can view the full definition of this autoscale setting.</span></span> <span data-ttu-id="6c509-121">В данном случае в конфигурации автомасштабирования по умолчанию используется правило масштабирования на основе загрузки ЦП в процентах.</span><span class="sxs-lookup"><span data-stu-id="6c509-121">In this case, the default autoscale setting comes with a CPU% based scale-out and scale-in rule.</span></span>  

3. <span data-ttu-id="6c509-122">Теперь можно добавить профили и правила на основе расписания или специальных требований.</span><span class="sxs-lookup"><span data-stu-id="6c509-122">You can now add more profiles and rules based on the schedule or specific requirements.</span></span> <span data-ttu-id="6c509-123">Мы создадим конфигурацию автомасштабирования с тремя профилями.</span><span class="sxs-lookup"><span data-stu-id="6c509-123">We create an autoscale setting with three profiles.</span></span> <span data-ttu-id="6c509-124">Чтобы узнать больше о профилях и правилах автомасштабирования, ознакомьтесь со статьей [Рекомендации по автомасштабированию Azure Insights](insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="6c509-124">To understand profiles and rules in autoscale, review [Autoscale Best Practices](insights-autoscale-best-practices.md).</span></span>  

    | <span data-ttu-id="6c509-125">Профили и правила</span><span class="sxs-lookup"><span data-stu-id="6c509-125">Profiles & Rules</span></span> | <span data-ttu-id="6c509-126">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="6c509-126">Description</span></span> |
    |--- | --- |
    | <span data-ttu-id="6c509-127">**Профиль**</span><span class="sxs-lookup"><span data-stu-id="6c509-127">**Profile**</span></span> |<span data-ttu-id="6c509-128">**На основе производительности или метрики**</span><span class="sxs-lookup"><span data-stu-id="6c509-128">**Performance/metric based**</span></span> |
    | <span data-ttu-id="6c509-129">правило;</span><span class="sxs-lookup"><span data-stu-id="6c509-129">Rule</span></span> |<span data-ttu-id="6c509-130">Количество сообщений в очереди служебной шины > x</span><span class="sxs-lookup"><span data-stu-id="6c509-130">Service Bus Queue Message Count > x</span></span> |
    | <span data-ttu-id="6c509-131">правило;</span><span class="sxs-lookup"><span data-stu-id="6c509-131">Rule</span></span> |<span data-ttu-id="6c509-132">Количество сообщений в очереди служебной шины < y</span><span class="sxs-lookup"><span data-stu-id="6c509-132">Service Bus Queue Message Count < y</span></span> |
    | <span data-ttu-id="6c509-133">правило;</span><span class="sxs-lookup"><span data-stu-id="6c509-133">Rule</span></span> |<span data-ttu-id="6c509-134">% загрузки ЦП > n</span><span class="sxs-lookup"><span data-stu-id="6c509-134">CPU% > n</span></span> |
    | <span data-ttu-id="6c509-135">правило;</span><span class="sxs-lookup"><span data-stu-id="6c509-135">Rule</span></span> |<span data-ttu-id="6c509-136">% загрузки ЦП < p</span><span class="sxs-lookup"><span data-stu-id="6c509-136">CPU% < p</span></span> |
    | <span data-ttu-id="6c509-137">**Профиль**</span><span class="sxs-lookup"><span data-stu-id="6c509-137">**Profile**</span></span> |<span data-ttu-id="6c509-138">**Утренние часы в рабочие дни (без правил)**</span><span class="sxs-lookup"><span data-stu-id="6c509-138">**Weekday morning hours (no rules)**</span></span> |
    | <span data-ttu-id="6c509-139">**Профиль**</span><span class="sxs-lookup"><span data-stu-id="6c509-139">**Profile**</span></span> |<span data-ttu-id="6c509-140">**День запуска продукта (без правил)**</span><span class="sxs-lookup"><span data-stu-id="6c509-140">**Product Launch day (no rules)**</span></span> |

4. <span data-ttu-id="6c509-141">Ниже приведен гипотетический сценарий масштабирования, который используется в данном пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="6c509-141">Here is a hypothetical scaling scenario that we use for this walk-through.</span></span>

    * <span data-ttu-id="6c509-142">**На основе нагрузки** — мне хотелось бы, чтобы масштаб изменялся соответственно нагрузке на мое приложение, размещенное в масштабируемом наборе.*</span><span class="sxs-lookup"><span data-stu-id="6c509-142">**Load based** - I'd like to scale out or in based on the load on my application hosted on my scale set.*</span></span>
    * <span data-ttu-id="6c509-143">**Размер очереди сообщений** — я использую очередь служебной шины для входящих сообщений, поступающих в приложение.</span><span class="sxs-lookup"><span data-stu-id="6c509-143">**Message Queue size** - I use a Service Bus Queue for the incoming messages to my application.</span></span> <span data-ttu-id="6c509-144">Я использую количество сообщений в очереди и загрузку ЦП в процентах и настрою профиль по умолчанию для активации действия масштабирования в случае, если количество сообщений или загрузка ЦП достигнет порогового значения.*</span><span class="sxs-lookup"><span data-stu-id="6c509-144">I use the queue's message count and CPU% and configure a default profile to trigger a scale action if either of message count or CPU hits the threshold.*</span></span>
    * <span data-ttu-id="6c509-145">**День недели и время суток** — мне нужен профиль для еженедельного повторения в определенное время дня, который называется "Утренние часы в рабочие дни".</span><span class="sxs-lookup"><span data-stu-id="6c509-145">**Time of week and day** - I want a weekly recurring 'time of the day' based profile called 'Weekday Morning Hours'.</span></span> <span data-ttu-id="6c509-146">На основе хронологических данных я знаю, что в это время лучше иметь определенное число экземпляров виртуальных машин для обработки нагрузки на приложение.*</span><span class="sxs-lookup"><span data-stu-id="6c509-146">Based on historical data, I know it is better to have certain number of VM instances to handle my application's load during this time.*</span></span>
    * <span data-ttu-id="6c509-147">**Особые даты** — добавлен профиль "День запуска продукта".</span><span class="sxs-lookup"><span data-stu-id="6c509-147">**Special Dates** - I added a 'Product Launch Day' profile.</span></span> <span data-ttu-id="6c509-148">Я заранее планирую особые даты, чтобы мое приложение было готово к обработке нагрузки после публикации рекламных объявлений или при добавлении нового продукта в приложение.*</span><span class="sxs-lookup"><span data-stu-id="6c509-148">I plan ahead for specific dates so my application is ready to handle the load due marketing announcements and when we put a new product in the application.*</span></span>
    * <span data-ttu-id="6c509-149">*Последние два профили могут также содержать другие правила на основе метрик производительности. В данном случае было решено не добавлять их, а положиться на правила, основанные на метриках производительности по умолчанию. Правила являются необязательными для профилей на основе повторения и дат.*</span><span class="sxs-lookup"><span data-stu-id="6c509-149">*The last two profiles can also have other performance metric based rules within them. In this case, I decided not to have one and instead to rely on the default performance metric based rules. Rules are optional for the recurring and date-based profiles.*</span></span>

    <span data-ttu-id="6c509-150">Определение приоритетов правил и профилей в механизме автомасштабирования описано также в статье [Рекомендации по автомасштабированию Azure Insights](insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="6c509-150">Autoscale engine's prioritization of the profiles and rules is also captured in the [autoscaling best practices](insights-autoscale-best-practices.md) article.</span></span>
    <span data-ttu-id="6c509-151">Список стандартных метрик для автомасштабирования см. в статье [Общие метрики автомасштабирования Azure Insights](insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="6c509-151">For a list of common metrics for autoscale, refer [Common metrics for Autoscale](insights-autoscale-common-metrics.md)</span></span>

5. <span data-ttu-id="6c509-152">Убедитесь, что в Resource Explorer включен режим **Read/Write** (Чтение и запись).</span><span class="sxs-lookup"><span data-stu-id="6c509-152">Make sure you are on the **Read/Write** mode in Resource Explorer</span></span>

    ![Autoscalewad, конфигурация автомасштабирования по умолчанию](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. <span data-ttu-id="6c509-154">Нажмите кнопку «Изменить».</span><span class="sxs-lookup"><span data-stu-id="6c509-154">Click Edit.</span></span> <span data-ttu-id="6c509-155">**Замените** элемент profiles в конфигурации автомасштабирования следующим текстом:</span><span class="sxs-lookup"><span data-stu-id="6c509-155">**Replace** the 'profiles' element in autoscale setting with the following configuration:</span></span>

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
    <span data-ttu-id="6c509-157">Описание поддерживаемых полей и их значений см. в [документации по REST API автомасштабирования](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c509-157">For supported fields and their values, see [Autoscale REST API documentation](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span></span> <span data-ttu-id="6c509-158">Теперь конфигурация автомасштабирования содержит три профиля, описанных выше.</span><span class="sxs-lookup"><span data-stu-id="6c509-158">Now your autoscale setting contains the three profiles explained previously.</span></span>

7. <span data-ttu-id="6c509-159">Наконец, рассмотрим раздел **notification** конфигурации автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="6c509-159">Finally, look at the Autoscale **notification** section.</span></span> <span data-ttu-id="6c509-160">Уведомления об автомасштабировании позволяют выполнить три действия при активации масштабирования:</span><span class="sxs-lookup"><span data-stu-id="6c509-160">Autoscale notifications allow you to do three things when a scale-out or in action is successfully triggered.</span></span>
   - <span data-ttu-id="6c509-161">уведомить администратора и соадминистраторов подписки;</span><span class="sxs-lookup"><span data-stu-id="6c509-161">Notify the admin and co-admins of your subscription</span></span>
   - <span data-ttu-id="6c509-162">от править электронное сообщение набору пользователей;</span><span class="sxs-lookup"><span data-stu-id="6c509-162">Email a set of users</span></span>
   - <span data-ttu-id="6c509-163">активировать вызов webhook.</span><span class="sxs-lookup"><span data-stu-id="6c509-163">Trigger a webhook call.</span></span> <span data-ttu-id="6c509-164">При активации этот webhook отправляет метаданные об условии автомасштабирования и ресурсе набора масштабирования.</span><span class="sxs-lookup"><span data-stu-id="6c509-164">When fired, this webhook sends metadata about the autoscaling condition and the scale set resource.</span></span> <span data-ttu-id="6c509-165">Чтобы узнать больше о полезных данных webhook автомасштабирования, ознакомьтесь со статьей разделом [Использование действий автомасштабирования для отправки электронной почты и уведомлений об оповещениях веб-перехватчика в Azure Insights](insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="6c509-165">To learn more about the payload of autoscale webhook, see [Configure Webhook & Email Notifications for Autoscale](insights-autoscale-to-webhook-email.md).</span></span>

   <span data-ttu-id="6c509-166">Добавьте следующий текст в конфигурацию автомасштабирования, заменив элемент **notification**, имеющий значение NULL.</span><span class="sxs-lookup"><span data-stu-id="6c509-166">Add the following to the Autoscale setting replacing your **notification** element whose value is null</span></span>

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

   <span data-ttu-id="6c509-167">Нажмите кнопку **Put** (Поместить) в Resource Explorer, чтобы обновить конфигурацию автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="6c509-167">Hit **Put** button in Resource Explorer to update the autoscale setting.</span></span>

<span data-ttu-id="6c509-168">Вы обновили конфигурацию автомасштабирования для набора масштабирования виртуальных машин, добавив в нее несколько профилей и уведомления.</span><span class="sxs-lookup"><span data-stu-id="6c509-168">You have updated an autoscale setting on a VM Scale set to include multiple scale profiles and scale notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c509-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6c509-169">Next Steps</span></span>
<span data-ttu-id="6c509-170">Воспользуйтесь следующими ссылками, чтобы получить дополнительную информацию об автомасштабировании.</span><span class="sxs-lookup"><span data-stu-id="6c509-170">Use these links to learn more about autoscaling.</span></span>

[<span data-ttu-id="6c509-171">Устранение неполадок при автомасштабировании масштабируемых наборов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="6c509-171">TroubleShoot Autoscale with Virtual Machine Scale Sets</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[<span data-ttu-id="6c509-172">Общие метрики автомасштабирования Azure Insights</span><span class="sxs-lookup"><span data-stu-id="6c509-172">Common Metrics for Autoscale</span></span>](insights-autoscale-common-metrics.md)

[<span data-ttu-id="6c509-173">Рекомендации по автомасштабированию Azure Insights</span><span class="sxs-lookup"><span data-stu-id="6c509-173">Best Practices for Azure Autoscale</span></span>](insights-autoscale-best-practices.md)

[<span data-ttu-id="6c509-174">Создание параметров автомасштабирования и управление ими</span><span class="sxs-lookup"><span data-stu-id="6c509-174">Manage Autoscale using PowerShell</span></span>](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[<span data-ttu-id="6c509-175">Автомасштабирование</span><span class="sxs-lookup"><span data-stu-id="6c509-175">Manage Autoscale using CLI</span></span>](insights-cli-samples.md#autoscale)

[<span data-ttu-id="6c509-176">Использование действий автомасштабирования для отправки электронной почты и уведомлений об оповещениях веб-перехватчика в Azure Insights</span><span class="sxs-lookup"><span data-stu-id="6c509-176">Configure Webhook & Email Notifications for Autoscale</span></span>](insights-autoscale-to-webhook-email.md)
