---
title: "Перемещение ресурсов Azure в новую подписку или группу ресурсов | Документация Майкрософт"
description: "Перемещайте ресурсы в новую группу ресурсов или новую подписку с помощью Azure Resource Manager."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: e138f80e808968ab4bf5c11cfd5fd46fe4a1bcce
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="move-resources-to-new-resource-group-or-subscription"></a><span data-ttu-id="54aa5-103">Перемещение ресурсов в новую группу ресурсов или подписку</span><span class="sxs-lookup"><span data-stu-id="54aa5-103">Move resources to new resource group or subscription</span></span>
<span data-ttu-id="54aa5-104">В этой статье показано, как переместить ресурсы в новую подписку или в новую группу ресурсов в той же подписке.</span><span class="sxs-lookup"><span data-stu-id="54aa5-104">This topic shows you how to move resources to either a new subscription or a new resource group in the same subscription.</span></span> <span data-ttu-id="54aa5-105">Для перемещения ресурса можно использовать портал, PowerShell, интерфейс командной строки Azure или REST API.</span><span class="sxs-lookup"><span data-stu-id="54aa5-105">You can use the portal, PowerShell, Azure CLI, or the REST API to move resource.</span></span> <span data-ttu-id="54aa5-106">Операции по перемещению, описанные в этой статье, вы можете выполнить самостоятельно, без помощи службы поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="54aa5-106">The move operations in this topic are available to you without any assistance from Azure support.</span></span>

<span data-ttu-id="54aa5-107">При перемещении ресурсов группа источника и группа назначения блокируются на время операции.</span><span class="sxs-lookup"><span data-stu-id="54aa5-107">When moving resources, both the source group and the target group are locked during the operation.</span></span> <span data-ttu-id="54aa5-108">Операции записи и удаления для групп ресурсов блокируются до завершения перемещения.</span><span class="sxs-lookup"><span data-stu-id="54aa5-108">Write and delete operations are blocked on the resource groups until the move completes.</span></span> <span data-ttu-id="54aa5-109">Эта блокировка означает, что невозможно добавить, обновить или удалить ресурсы в группах ресурсов, но не означает, что эти ресурсы закреплены.</span><span class="sxs-lookup"><span data-stu-id="54aa5-109">This lock means you cannot add, update, or delete resources in the resource groups, but it does not mean the resources are frozen.</span></span> <span data-ttu-id="54aa5-110">Например, если переместить в новую группу ресурсов экземпляр SQL Server и его базу данных, то приложение, использующее эту базу данных, не будет испытывать простоев в работе.</span><span class="sxs-lookup"><span data-stu-id="54aa5-110">For example, if you move a SQL Server and its database to a new resource group, an application that uses the database experiences no downtime.</span></span> <span data-ttu-id="54aa5-111">Оно по-прежнему сможет считывать данные из базы данных и записывать их в нее.</span><span class="sxs-lookup"><span data-stu-id="54aa5-111">It can still read and write to the database.</span></span>

<span data-ttu-id="54aa5-112">Расположение ресурса изменить невозможно.</span><span class="sxs-lookup"><span data-stu-id="54aa5-112">You cannot change the location of the resource.</span></span> <span data-ttu-id="54aa5-113">При перемещении ресурс всего лишь перемещается в новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="54aa5-113">Moving a resource only moves it to a new resource group.</span></span> <span data-ttu-id="54aa5-114">Даже если новая группа ресурсов находится в другом расположении, расположение ресурса не меняется.</span><span class="sxs-lookup"><span data-stu-id="54aa5-114">The new resource group may have a different location, but that does not change the location of the resource.</span></span>

> [!NOTE]
> <span data-ttu-id="54aa5-115">В этой статье описывается, как перемещать ресурсы в рамках существующего предложения для учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="54aa5-115">This article describes how to move resources within an existing Azure account offering.</span></span> <span data-ttu-id="54aa5-116">Если вы действительно хотите изменить предложение для своей учетной записи Azure (например, перейти с оплаты по мере использования на предоплату), продолжая работать с существующими ресурсами, см. статью [Переключение подписки Azure на другое предложение](../billing/billing-how-to-switch-azure-offer.md).</span><span class="sxs-lookup"><span data-stu-id="54aa5-116">If you actually want to change your Azure account offering (such as upgrading from pay-as-you-go to pre-pay) while continuing to work with your existing resources, see [Switch your Azure subscription to another offer](../billing/billing-how-to-switch-azure-offer.md).</span></span>
>
>

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="54aa5-117">Рекомендации перед перемещением ресурсов</span><span class="sxs-lookup"><span data-stu-id="54aa5-117">Checklist before moving resources</span></span>
<span data-ttu-id="54aa5-118">Вот некоторые важные особенности, которые следует учитывать перед перемещением ресурса.</span><span class="sxs-lookup"><span data-stu-id="54aa5-118">There are some important steps to perform before moving a resource.</span></span> <span data-ttu-id="54aa5-119">Проверив эти условия, можно избежать ошибок.</span><span class="sxs-lookup"><span data-stu-id="54aa5-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="54aa5-120">Исходная и целевая подписка должны существовать в пределах одного [клиента Azure Active Directory](../active-directory/active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="54aa5-120">The source and destination subscriptions must exist within the same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="54aa5-121">Используя Azure PowerShell или командную строку Azure, можно убедиться, что обе подписки имеют один и тот же идентификатор клиента.</span><span class="sxs-lookup"><span data-stu-id="54aa5-121">To check that both subscriptions have the same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="54aa5-122">Для Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="54aa5-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="54aa5-123">В Azure CLI 2.0 используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="54aa5-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="54aa5-124">Если идентификаторы клиентов для исходной и целевой подписок не совпадают, можно попробовать изменить каталог для подписки.</span><span class="sxs-lookup"><span data-stu-id="54aa5-124">If the tenant IDs for the source and destination subscriptions are not the same, you can attempt to change the directory for the subscription.</span></span> <span data-ttu-id="54aa5-125">Но эта возможность доступна только для администраторов службы, которые вошли в учетную запись Майкрософт (не корпоративную учетную запись).</span><span class="sxs-lookup"><span data-stu-id="54aa5-125">However, this option is only available to Service Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="54aa5-126">Чтобы попробовать изменить каталог, войдите на [классический портал](https://manage.windowsazure.com/), щелкните **Параметры** и выберите подписку.</span><span class="sxs-lookup"><span data-stu-id="54aa5-126">To attempt changing the directory, log in to the [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select the subscription.</span></span> <span data-ttu-id="54aa5-127">Если значок **Изменить каталог** доступен, щелкните его, чтобы изменить связанный Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="54aa5-127">If the **Edit Directory** icon is available, select it to change the associated Azure Active Directory.</span></span>

  ![Изменение каталога](./media/resource-group-move-resources/edit-directory.png)

  <span data-ttu-id="54aa5-129">Если значок недоступен, обратитесь в службу поддержки. Вам помогут переместить ресурсы в новый клиент.</span><span class="sxs-lookup"><span data-stu-id="54aa5-129">If that icon is not available, you must contact support to move the resources to a new tenant.</span></span>

2. <span data-ttu-id="54aa5-130">Служба должна иметь возможность перемещения ресурсов.</span><span class="sxs-lookup"><span data-stu-id="54aa5-130">The service must enable the ability to move resources.</span></span> <span data-ttu-id="54aa5-131">В этом разделе перечислено, какие службы позволяют перемещать ресурсы, а какие — нет.</span><span class="sxs-lookup"><span data-stu-id="54aa5-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="54aa5-132">Подписка назначения должна быть зарегистрирована для перемещаемого поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="54aa5-132">The destination subscription must be registered for the resource provider of the resource being moved.</span></span> <span data-ttu-id="54aa5-133">В противном случае отображается сообщение о том, что **подписка не зарегистрирована для типа ресурса**.</span><span class="sxs-lookup"><span data-stu-id="54aa5-133">If not, you receive an error stating that the **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="54aa5-134">Эта проблема может возникнуть при перемещении ресурса в новую подписку, которая никогда не использовалась с этим типом ресурса.</span><span class="sxs-lookup"><span data-stu-id="54aa5-134">You might encounter this problem when moving a resource to a new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="54aa5-135">Сведения о регистрации поставщиков ресурсов и проверке состояния регистрации см. в разделе [Поставщики и типы ресурсов](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="54aa5-135">To learn how to check the registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="when-to-call-support"></a><span data-ttu-id="54aa5-136">Когда обращаться в службу поддержки</span><span class="sxs-lookup"><span data-stu-id="54aa5-136">When to call support</span></span>
<span data-ttu-id="54aa5-137">Большинство ресурсов можно самостоятельно переместить с помощью операций, описанных в этой статье.</span><span class="sxs-lookup"><span data-stu-id="54aa5-137">You can move most resources through the self-service operations shown in this topic.</span></span> <span data-ttu-id="54aa5-138">С помощью этих операций можно выполнять такие действия:</span><span class="sxs-lookup"><span data-stu-id="54aa5-138">Use the self-service operations to:</span></span>

* <span data-ttu-id="54aa5-139">перемещение ресурсов Resource Manager;</span><span class="sxs-lookup"><span data-stu-id="54aa5-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="54aa5-140">перемещение классических ресурсов с учетом [ограничений классического развертывания](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="54aa5-140">Move classic resources according to the [classic deployment limitations](#classic-deployment-limitations).</span></span>

<span data-ttu-id="54aa5-141">Обратитесь в службу поддержки, если необходимо выполнить такие действия:</span><span class="sxs-lookup"><span data-stu-id="54aa5-141">Call support when you need to:</span></span>

* <span data-ttu-id="54aa5-142">перемещение ресурсов в новую учетную запись Azure (и клиент Azure Active Directory);</span><span class="sxs-lookup"><span data-stu-id="54aa5-142">Move your resources to a new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="54aa5-143">перемещение классических ресурсов, осложненное проблемами с ограничениями.</span><span class="sxs-lookup"><span data-stu-id="54aa5-143">Move classic resources but are having trouble with the limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="54aa5-144">Службы, поддерживающие перемещение</span><span class="sxs-lookup"><span data-stu-id="54aa5-144">Services that enable move</span></span>
<span data-ttu-id="54aa5-145">Указанные ниже службы сейчас поддерживают перемещение в новую группу ресурсов и подписку.</span><span class="sxs-lookup"><span data-stu-id="54aa5-145">For now, the services that enable moving to both a new resource group and subscription are:</span></span>

* <span data-ttu-id="54aa5-146">Управление API</span><span class="sxs-lookup"><span data-stu-id="54aa5-146">API Management</span></span>
* <span data-ttu-id="54aa5-147">Приложения службы приложений (веб-приложения) — см. раздел [Ограничения службы приложений](#app-service-limitations).</span><span class="sxs-lookup"><span data-stu-id="54aa5-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="54aa5-148">Application Insights</span><span class="sxs-lookup"><span data-stu-id="54aa5-148">Application Insights</span></span>
* <span data-ttu-id="54aa5-149">Автоматизация</span><span class="sxs-lookup"><span data-stu-id="54aa5-149">Automation</span></span>
* <span data-ttu-id="54aa5-150">Пакетная служба</span><span class="sxs-lookup"><span data-stu-id="54aa5-150">Batch</span></span>
* <span data-ttu-id="54aa5-151">Карты Bing</span><span class="sxs-lookup"><span data-stu-id="54aa5-151">Bing Maps</span></span>
* <span data-ttu-id="54aa5-152">CDN</span><span class="sxs-lookup"><span data-stu-id="54aa5-152">CDN</span></span>
* <span data-ttu-id="54aa5-153">Облачные службы — см. раздел [Ограничения классического развертывания](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="54aa5-153">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="54aa5-154">Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="54aa5-154">Cognitive Services</span></span>
* <span data-ttu-id="54aa5-155">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="54aa5-155">Content Moderator</span></span>
* <span data-ttu-id="54aa5-156">Каталог данных</span><span class="sxs-lookup"><span data-stu-id="54aa5-156">Data Catalog</span></span>
* <span data-ttu-id="54aa5-157">Фабрика данных</span><span class="sxs-lookup"><span data-stu-id="54aa5-157">Data Factory</span></span>
* <span data-ttu-id="54aa5-158">Аналитика озера данных</span><span class="sxs-lookup"><span data-stu-id="54aa5-158">Data Lake Analytics</span></span>
* <span data-ttu-id="54aa5-159">Хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="54aa5-159">Data Lake Store</span></span>
* <span data-ttu-id="54aa5-160">DNS</span><span class="sxs-lookup"><span data-stu-id="54aa5-160">DNS</span></span>
* <span data-ttu-id="54aa5-161">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="54aa5-161">Azure Cosmos DB</span></span>
* <span data-ttu-id="54aa5-162">Концентраторы событий</span><span class="sxs-lookup"><span data-stu-id="54aa5-162">Event Hubs</span></span>
* <span data-ttu-id="54aa5-163">Кластеры HDInsight — см. раздел [Ограничения HDInsight](#hdinsight-limitations).</span><span class="sxs-lookup"><span data-stu-id="54aa5-163">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="54aa5-164">Центры Интернета вещей;</span><span class="sxs-lookup"><span data-stu-id="54aa5-164">IoT Hubs</span></span>
* <span data-ttu-id="54aa5-165">Хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="54aa5-165">Key Vault</span></span>
* <span data-ttu-id="54aa5-166">Балансировщики нагрузки</span><span class="sxs-lookup"><span data-stu-id="54aa5-166">Load Balancers</span></span>
* <span data-ttu-id="54aa5-167">Приложения логики</span><span class="sxs-lookup"><span data-stu-id="54aa5-167">Logic Apps</span></span>
* <span data-ttu-id="54aa5-168">Машинное обучение</span><span class="sxs-lookup"><span data-stu-id="54aa5-168">Machine Learning</span></span>
* <span data-ttu-id="54aa5-169">Службы мультимедиа</span><span class="sxs-lookup"><span data-stu-id="54aa5-169">Media Services</span></span>
* <span data-ttu-id="54aa5-170">Службы мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="54aa5-170">Mobile Engagement</span></span>
* <span data-ttu-id="54aa5-171">Центры уведомлений</span><span class="sxs-lookup"><span data-stu-id="54aa5-171">Notification Hubs</span></span>
* <span data-ttu-id="54aa5-172">Operational Insights;</span><span class="sxs-lookup"><span data-stu-id="54aa5-172">Operational Insights</span></span>
* <span data-ttu-id="54aa5-173">Пакет Operations Management</span><span class="sxs-lookup"><span data-stu-id="54aa5-173">Operations Management</span></span>
* <span data-ttu-id="54aa5-174">Power BI</span><span class="sxs-lookup"><span data-stu-id="54aa5-174">Power BI</span></span>
* <span data-ttu-id="54aa5-175">Кэш Redis</span><span class="sxs-lookup"><span data-stu-id="54aa5-175">Redis Cache</span></span>
* <span data-ttu-id="54aa5-176">Планировщик</span><span class="sxs-lookup"><span data-stu-id="54aa5-176">Scheduler</span></span>
* <span data-ttu-id="54aa5-177">Поиск</span><span class="sxs-lookup"><span data-stu-id="54aa5-177">Search</span></span>
* <span data-ttu-id="54aa5-178">Управление сервером</span><span class="sxs-lookup"><span data-stu-id="54aa5-178">Server Management</span></span>
* <span data-ttu-id="54aa5-179">Служебная шина</span><span class="sxs-lookup"><span data-stu-id="54aa5-179">Service Bus</span></span>
* <span data-ttu-id="54aa5-180">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="54aa5-180">Service Fabric</span></span>
* <span data-ttu-id="54aa5-181">Хранилище</span><span class="sxs-lookup"><span data-stu-id="54aa5-181">Storage</span></span>
* <span data-ttu-id="54aa5-182">Служба хранилища (классическая) — см. раздел [Ограничения классического развертывания](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="54aa5-182">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="54aa5-183">Stream Analytics — задание Stream Analytics в состоянии выполнения нельзя переместить.</span><span class="sxs-lookup"><span data-stu-id="54aa5-183">Stream Analytics - Stream Analytics jobs cannot be moved when in running state.</span></span>
* <span data-ttu-id="54aa5-184">Сервер базы данных SQL — база данных и сервер должны находиться в одной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="54aa5-184">SQL Database server - The database and server must reside in the same resource group.</span></span> <span data-ttu-id="54aa5-185">При перемещении сервера SQL Server все его базы данных также перемещаются.</span><span class="sxs-lookup"><span data-stu-id="54aa5-185">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="54aa5-186">Диспетчер трафика</span><span class="sxs-lookup"><span data-stu-id="54aa5-186">Traffic Manager</span></span>
* <span data-ttu-id="54aa5-187">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="54aa5-187">Virtual Machines</span></span>
* <span data-ttu-id="54aa5-188">Виртуальные машины с сертификатами, хранящимися в Key Vault — переход на новую группу ресурсов в одной подписке включен, но перемещение между подписками не доступно.</span><span class="sxs-lookup"><span data-stu-id="54aa5-188">Virtual Machines with certificate stored in Key Vault - Move to new resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="54aa5-189">Виртуальные машины (классические) — см. раздел [Ограничения классического развертывания](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="54aa5-189">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="54aa5-190">Наборы для масштабирования виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="54aa5-190">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="54aa5-191">Виртуальные сети. В настоящее время невозможно переместить пиринговую виртуальную сеть, пока не будет отключен ее пиринг.</span><span class="sxs-lookup"><span data-stu-id="54aa5-191">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="54aa5-192">После этого ее можно переместить и включить пиринг.</span><span class="sxs-lookup"><span data-stu-id="54aa5-192">Once disabled, the Virtual Network can be moved successfully and the VNet peering can be enabled.</span></span> <span data-ttu-id="54aa5-193">Кроме того, виртуальную сеть невозможно переместить в другую подписку, если эта сеть содержит какую-либо подсеть со ссылками перехода к ресурсам.</span><span class="sxs-lookup"><span data-stu-id="54aa5-193">In addition, a Virtual Network cannot be moved to a different subscription if the Virtual Network contains any subnet with resource navigation links.</span></span> <span data-ttu-id="54aa5-194">Например, подсеть виртуальной сети содержит ссылку перехода к ресурсу, когда ресурс Redis Microsoft.Cache развертывается в этой подсети.</span><span class="sxs-lookup"><span data-stu-id="54aa5-194">For example, a Virtual Network subnet has a resource navigation link when a Microsoft.Cache redis resource is deployed into this subnet.</span></span>
* <span data-ttu-id="54aa5-195">VPN-шлюз</span><span class="sxs-lookup"><span data-stu-id="54aa5-195">VPN Gateway</span></span>


## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="54aa5-196">Службы, не поддерживающие перемещение</span><span class="sxs-lookup"><span data-stu-id="54aa5-196">Services that do not enable move</span></span>
<span data-ttu-id="54aa5-197">Службы, которые в настоящее время не поддерживают перемещение ресурсов:</span><span class="sxs-lookup"><span data-stu-id="54aa5-197">The services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="54aa5-198">доменные службы Active Directory;</span><span class="sxs-lookup"><span data-stu-id="54aa5-198">AD Domain Services</span></span>
* <span data-ttu-id="54aa5-199">служба работоспособности гибридного AD;</span><span class="sxs-lookup"><span data-stu-id="54aa5-199">AD Hybrid Health Service</span></span>
* <span data-ttu-id="54aa5-200">Шлюз приложений</span><span class="sxs-lookup"><span data-stu-id="54aa5-200">Application Gateway</span></span>
* <span data-ttu-id="54aa5-201">Группы доступности, содержащие виртуальные машины с управляемыми дисками.</span><span class="sxs-lookup"><span data-stu-id="54aa5-201">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="54aa5-202">Службы BizTalk</span><span class="sxs-lookup"><span data-stu-id="54aa5-202">BizTalk Services</span></span>
* <span data-ttu-id="54aa5-203">Служба контейнеров</span><span class="sxs-lookup"><span data-stu-id="54aa5-203">Container Service</span></span>
* <span data-ttu-id="54aa5-204">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="54aa5-204">Express Route</span></span>
* <span data-ttu-id="54aa5-205">DevTest Labs — переход на новую группу ресурсов в одной подписке включен, но перемещение между подписками не доступно.</span><span class="sxs-lookup"><span data-stu-id="54aa5-205">DevTest Labs - Move to new resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="54aa5-206">Dynamics LCS.</span><span class="sxs-lookup"><span data-stu-id="54aa5-206">Dynamics LCS</span></span>
* <span data-ttu-id="54aa5-207">Образы, созданные из управляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="54aa5-207">Images created from Managed Disks</span></span>
* <span data-ttu-id="54aa5-208">Управляемые диски</span><span class="sxs-lookup"><span data-stu-id="54aa5-208">Managed Disks</span></span>
* <span data-ttu-id="54aa5-209">Управляемые приложения.</span><span class="sxs-lookup"><span data-stu-id="54aa5-209">Managed Applications</span></span>
* <span data-ttu-id="54aa5-210">Хранилище служб восстановления. Не перемещайте ресурсы хранилища, а также вычислительные и сетевые ресурсы, связанные с хранилищем служб восстановления. См. раздел [Ограничения служб восстановления](#recovery-services-limitations).</span><span class="sxs-lookup"><span data-stu-id="54aa5-210">Recovery Services vault - also do not move the Compute, Network, and Storage resources associated with the Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="54aa5-211">Безопасность</span><span class="sxs-lookup"><span data-stu-id="54aa5-211">Security</span></span>
* <span data-ttu-id="54aa5-212">Моментальные снимки, созданные из управляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="54aa5-212">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="54aa5-213">Диспетчер устройств StorSimple</span><span class="sxs-lookup"><span data-stu-id="54aa5-213">StorSimple Device Manager</span></span>
* <span data-ttu-id="54aa5-214">Виртуальные машины с Управляемыми дисками</span><span class="sxs-lookup"><span data-stu-id="54aa5-214">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="54aa5-215">Виртуальные сети (классические) — см. раздел [Ограничения классического развертывания](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="54aa5-215">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="54aa5-216">Виртуальные машины, созданные из ресурсов Marketplace, невозможно переместить между подписками.</span><span class="sxs-lookup"><span data-stu-id="54aa5-216">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="54aa5-217">Необходимо отозвать ресурс в текущей подписке и развернуть его в новой подписке.</span><span class="sxs-lookup"><span data-stu-id="54aa5-217">Resource needs to be deprovisioned in the current subscription and deployed again in the new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="54aa5-218">Ограничения службы приложений</span><span class="sxs-lookup"><span data-stu-id="54aa5-218">App Service limitations</span></span>
<span data-ttu-id="54aa5-219">При работе с приложениями службы приложений невозможно переместить только план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="54aa5-219">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="54aa5-220">Далее приводятся варианты перемещения приложений службы приложений.</span><span class="sxs-lookup"><span data-stu-id="54aa5-220">To move App Service apps, your options are:</span></span>

* <span data-ttu-id="54aa5-221">Перемещение плана службы приложений и всех других ресурсов службы приложений из этой группы ресурсов в новую группу ресурсов, которая еще не содержит ресурсы службы приложений.</span><span class="sxs-lookup"><span data-stu-id="54aa5-221">Move the App Service plan and all other App Service resources in that resource group to a new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="54aa5-222">Это требование означает, что необходимо переместить даже те ресурсы службы приложений, которые не связаны с планом службы приложений.</span><span class="sxs-lookup"><span data-stu-id="54aa5-222">This requirement means you must move even the App Service resources that are not associated with the App Service plan.</span></span>
* <span data-ttu-id="54aa5-223">Перемещение приложений в другую группу ресурсов, но сохранение планов службы приложений в исходной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="54aa5-223">Move the apps to a different resource group, but keep all App Service plans in the original resource group.</span></span>

<span data-ttu-id="54aa5-224">Для корректной работы приложения план службы приложений и приложение не должны обязательно находиться в одной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="54aa5-224">The App Service plan does not need to reside in the same resource group as the app for the app to function correctly.</span></span>

<span data-ttu-id="54aa5-225">Например, если группа ресурсов содержит:</span><span class="sxs-lookup"><span data-stu-id="54aa5-225">For example, if your resource group contains:</span></span>

* <span data-ttu-id="54aa5-226">ресурс **web-a**, связанный с **plan-a**;</span><span class="sxs-lookup"><span data-stu-id="54aa5-226">**web-a** which is associated with **plan-a**</span></span>
* <span data-ttu-id="54aa5-227">ресурс **web-b**, связанный с **plan-b**.</span><span class="sxs-lookup"><span data-stu-id="54aa5-227">**web-b** which is associated with **plan-b**</span></span>

<span data-ttu-id="54aa5-228">Вам доступны следующие действия:</span><span class="sxs-lookup"><span data-stu-id="54aa5-228">Your options are:</span></span>

* <span data-ttu-id="54aa5-229">перемещение **web-a**, **plan-a**, **web-b**, и **plan-b**;</span><span class="sxs-lookup"><span data-stu-id="54aa5-229">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="54aa5-230">перемещение **web-a** и **web-b**;</span><span class="sxs-lookup"><span data-stu-id="54aa5-230">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="54aa5-231">перемещение **web-a**</span><span class="sxs-lookup"><span data-stu-id="54aa5-231">Move **web-a**</span></span>
* <span data-ttu-id="54aa5-232">перемещение **web-b**</span><span class="sxs-lookup"><span data-stu-id="54aa5-232">Move **web-b**</span></span>

<span data-ttu-id="54aa5-233">Все другие сочетания включают необходимость оставить тип ресурса, который нельзя оставлять при перемещении плана службы приложений (любой тип ресурса службы приложений).</span><span class="sxs-lookup"><span data-stu-id="54aa5-233">All other combinations involve leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="54aa5-234">Если веб-приложение находится в одной группе ресурсов, а его план службы приложений — в другой, но в новую группу ресурсов требуется переместить и веб-приложение, и план, то необходимо выполнить перемещение в два этапа.</span><span class="sxs-lookup"><span data-stu-id="54aa5-234">If your web app resides in a different resource group than its App Service plan but you want to move both to a new resource group, you must perform the move in two steps.</span></span> <span data-ttu-id="54aa5-235">Например:</span><span class="sxs-lookup"><span data-stu-id="54aa5-235">For example:</span></span>

* <span data-ttu-id="54aa5-236">**web-a** находится в группе **web-group**;</span><span class="sxs-lookup"><span data-stu-id="54aa5-236">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="54aa5-237">**plan-a** находится в группе **plan-group**;</span><span class="sxs-lookup"><span data-stu-id="54aa5-237">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="54aa5-238">вы хотите поместить **web-a** и **plan-a** в объединенную группу **combined-group**.</span><span class="sxs-lookup"><span data-stu-id="54aa5-238">You want **web-a** and **plan-a** to reside in **combined-group**</span></span>

<span data-ttu-id="54aa5-239">Чтобы осуществить это перемещение, выполните две отдельные операции перемещения в следующей последовательности:</span><span class="sxs-lookup"><span data-stu-id="54aa5-239">To accomplish this move, perform two separate move operations in the following sequence:</span></span>

1. <span data-ttu-id="54aa5-240">Переместите **web-a** в группу **plan-group**.</span><span class="sxs-lookup"><span data-stu-id="54aa5-240">Move the **web-a** to **plan-group**</span></span>
2. <span data-ttu-id="54aa5-241">Переместите **web-a** и **plan-a** в объединенную группу **combined-group**.</span><span class="sxs-lookup"><span data-stu-id="54aa5-241">Move **web-a** and **plan-a** to **combined-group**.</span></span>

<span data-ttu-id="54aa5-242">Сертификат службы приложений можно без проблем переместить в новую группу ресурсов или подписку.</span><span class="sxs-lookup"><span data-stu-id="54aa5-242">You can move an App Service Certificate to a new resource group or subscription without any issues.</span></span> <span data-ttu-id="54aa5-243">Но если веб-приложение включает сертификат SSL, приобретенный у стороннего поставщика и переданный в приложение, необходимо удалить сертификат перед перемещением веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="54aa5-243">However, if your web app includes an SSL certificate that you purchased externally and uploaded to the app, you must delete the certificate before moving the web app.</span></span> <span data-ttu-id="54aa5-244">Например, можно выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="54aa5-244">For example, you can perform the following steps:</span></span>

1. <span data-ttu-id="54aa5-245">Удалить отправленный сертификат из веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="54aa5-245">Delete the uploaded certificate from the web app</span></span>
2. <span data-ttu-id="54aa5-246">Переместить веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="54aa5-246">Move the web app</span></span>
3. <span data-ttu-id="54aa5-247">Добавить сертификат в веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="54aa5-247">Upload the certificate to the web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="54aa5-248">Ограничения служб восстановления</span><span class="sxs-lookup"><span data-stu-id="54aa5-248">Recovery Services limitations</span></span>
<span data-ttu-id="54aa5-249">Перемещение не поддерживается для ресурсов хранилища, сетевых и вычислительных ресурсов, используемых для настройки аварийного восстановления с помощью Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="54aa5-249">Move is not enabled for Storage, Network, or Compute resources used to set up disaster recovery with Azure Site Recovery.</span></span>

<span data-ttu-id="54aa5-250">Предположим, что вы настроили репликацию своих локальных компьютеров в учетную запись хранения (Storage1) и хотите, чтобы защищенный компьютер восстанавливался после отработки отказа в Azure как виртуальная машина (VM1), подключенная к виртуальной сети (Network1).</span><span class="sxs-lookup"><span data-stu-id="54aa5-250">For example, suppose you have set up replication of your on-premises machines to a storage account (Storage1) and want the protected machine to come up after failover to Azure as a virtual machine (VM1) attached to a virtual network (Network1).</span></span> <span data-ttu-id="54aa5-251">Ни один из этих ресурсов Azure (Storage1, VM1 и Network1) нельзя перемещать между группами ресурсов в пределах одной подписки или между подписками.</span><span class="sxs-lookup"><span data-stu-id="54aa5-251">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within the same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="54aa5-252">Ограничения HDInsight</span><span class="sxs-lookup"><span data-stu-id="54aa5-252">HDInsight limitations</span></span>

<span data-ttu-id="54aa5-253">Кластеры HDInsight можно переместить в новую подписку или группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="54aa5-253">You can move HDInsight clusters to a new subscription or resource group.</span></span> <span data-ttu-id="54aa5-254">Однако перемещение между подписками недоступно для сетевых ресурсов, связанных с кластером HDInsight (таких как виртуальная сеть, сетевая карта или балансировщик нагрузки).</span><span class="sxs-lookup"><span data-stu-id="54aa5-254">However, you cannot move across subscriptions the networking resources linked to the HDInsight cluster (such as the virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="54aa5-255">Также невозможно переместить в новую группу ресурсов сетевую карту, которая подключена к виртуальной машине кластера.</span><span class="sxs-lookup"><span data-stu-id="54aa5-255">In addition, you cannot move to a new resource group a NIC that is attached to a virtual machine for the cluster.</span></span>

<span data-ttu-id="54aa5-256">При перемещении кластера HDInsight в новую подписку сначала необходимо переместить другие ресурсы (такие как учетная запись хранения).</span><span class="sxs-lookup"><span data-stu-id="54aa5-256">When moving an HDInsight cluster to a new subscription, first move other resources (like the storage account).</span></span> <span data-ttu-id="54aa5-257">А затем переместить сам кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="54aa5-257">Then, move the HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="54aa5-258">Ограничения классического развертывания</span><span class="sxs-lookup"><span data-stu-id="54aa5-258">Classic deployment limitations</span></span>
<span data-ttu-id="54aa5-259">Процедуры перемещения ресурсов, развернутых с помощью классической модели, отличаются в зависимости от того, перемещаются ли ресурсы в пределах одной подписки, или они переносятся в новую подписку.</span><span class="sxs-lookup"><span data-stu-id="54aa5-259">The options for moving resources deployed through the classic model differ based on whether you are moving the resources within a subscription or to a new subscription.</span></span>

### <a name="same-subscription"></a><span data-ttu-id="54aa5-260">Та же подписка</span><span class="sxs-lookup"><span data-stu-id="54aa5-260">Same subscription</span></span>
<span data-ttu-id="54aa5-261">При перемещении ресурсов из одной группы ресурсов в другую в пределах одной подписки действуют следующие ограничения.</span><span class="sxs-lookup"><span data-stu-id="54aa5-261">When moving resources from one resource group to another resource group within the same subscription, the following restrictions apply:</span></span>

* <span data-ttu-id="54aa5-262">Нельзя перемещать виртуальные сети (классические).</span><span class="sxs-lookup"><span data-stu-id="54aa5-262">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="54aa5-263">Виртуальные машины (классические) необходимо перемещать с облачной службой.</span><span class="sxs-lookup"><span data-stu-id="54aa5-263">Virtual machines (classic) must be moved with the cloud service.</span></span>
* <span data-ttu-id="54aa5-264">Облачную службу можно перемещать только в тех случаях, когда перемещение включает в себя все виртуальные машины этой службы.</span><span class="sxs-lookup"><span data-stu-id="54aa5-264">Cloud service can only be moved when the move includes all its virtual machines.</span></span>
* <span data-ttu-id="54aa5-265">Одновременно можно перемещать только одну облачную службу.</span><span class="sxs-lookup"><span data-stu-id="54aa5-265">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="54aa5-266">Одновременно можно перемещать только одну учетную запись хранения (классическую).</span><span class="sxs-lookup"><span data-stu-id="54aa5-266">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="54aa5-267">Нельзя перемещать учетную запись хранения (классическую) в рамках одной операции с виртуальной машиной или облачной службой.</span><span class="sxs-lookup"><span data-stu-id="54aa5-267">Storage account (classic) cannot be moved in the same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="54aa5-268">Для перемещения классических ресурсов в новую группу ресурсов в пределах одной подписки используйте стандартные операции перемещения на [портале](#use-portal), в [Azure PowerShell](#use-powershell), [интерфейсе командной строки Azure](#use-azure-cli) или интерфейсе [REST API](#use-rest-api).</span><span class="sxs-lookup"><span data-stu-id="54aa5-268">To move classic resources to a new resource group within the same subscription, use the standard move operations through the [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="54aa5-269">При этом используются те же операции, что и для перемещения ресурсов Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="54aa5-269">You use the same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="54aa5-270">Новая подписка</span><span class="sxs-lookup"><span data-stu-id="54aa5-270">New subscription</span></span>
<span data-ttu-id="54aa5-271">При перемещении ресурсов в новую подписку действуют следующие ограничения.</span><span class="sxs-lookup"><span data-stu-id="54aa5-271">When moving resources to a new subscription, the following restrictions apply:</span></span>

* <span data-ttu-id="54aa5-272">Все классические ресурсы в подписке необходимо переместить в рамках одной операции.</span><span class="sxs-lookup"><span data-stu-id="54aa5-272">All classic resources in the subscription must be moved in the same operation.</span></span>
* <span data-ttu-id="54aa5-273">Целевая подписка не должна содержать никаких других классических ресурсов.</span><span class="sxs-lookup"><span data-stu-id="54aa5-273">The target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="54aa5-274">Перемещение можно запросить только через отдельный интерфейс REST API для классических перемещений.</span><span class="sxs-lookup"><span data-stu-id="54aa5-274">The move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="54aa5-275">Стандартные команды перемещения Resource Manager не работают, если перемещение классических ресурсов осуществляется в новую подписку.</span><span class="sxs-lookup"><span data-stu-id="54aa5-275">The standard Resource Manager move commands do not work when moving classic resources to a new subscription.</span></span>

<span data-ttu-id="54aa5-276">Для перемещения классических ресурсов в новую подписку используйте операции REST, предназначенные для классических ресурсов.</span><span class="sxs-lookup"><span data-stu-id="54aa5-276">To move classic resources to a new subscription, use the REST operations that are specific to classic resources.</span></span> <span data-ttu-id="54aa5-277">Чтобы воспользоваться REST, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="54aa5-277">To use REST, perform the following steps:</span></span>

1. <span data-ttu-id="54aa5-278">Проверьте, может ли исходная подписка участвовать в перемещении между подписками.</span><span class="sxs-lookup"><span data-stu-id="54aa5-278">Check if the source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="54aa5-279">Выполните такую операцию:</span><span class="sxs-lookup"><span data-stu-id="54aa5-279">Use the following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="54aa5-280">Включите в текст запроса такой код:</span><span class="sxs-lookup"><span data-stu-id="54aa5-280">In the request body, include:</span></span>

  ```json
  {
    "role": "source"
  }
  ```

     <span data-ttu-id="54aa5-281">Ответ на операцию проверки имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="54aa5-281">The response for the validation operation is in the following format:</span></span>

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="54aa5-282">Проверьте, может ли целевая подписка участвовать в перемещении между подписками.</span><span class="sxs-lookup"><span data-stu-id="54aa5-282">Check if the destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="54aa5-283">Выполните такую операцию:</span><span class="sxs-lookup"><span data-stu-id="54aa5-283">Use the following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="54aa5-284">Включите в текст запроса такой код:</span><span class="sxs-lookup"><span data-stu-id="54aa5-284">In the request body, include:</span></span>

  ```json
  {
    "role": "target"
  }
  ```

     <span data-ttu-id="54aa5-285">Ответ будет в том же формате, что и проверка исходной подписки.</span><span class="sxs-lookup"><span data-stu-id="54aa5-285">The response is in the same format as the source subscription validation.</span></span>
3. <span data-ttu-id="54aa5-286">Если обе подписки пройдут проверку, переместите все классические ресурсы из одной подписки в другую, выполнив следующее действие:</span><span class="sxs-lookup"><span data-stu-id="54aa5-286">If both subscriptions pass validation, move all classic resources from one subscription to another subscription with the following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="54aa5-287">Включите в текст запроса такой код:</span><span class="sxs-lookup"><span data-stu-id="54aa5-287">In the request body, include:</span></span>

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="54aa5-288">Операция может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="54aa5-288">The operation may run for several minutes.</span></span>

## <a name="use-portal"></a><span data-ttu-id="54aa5-289">С помощью портала</span><span class="sxs-lookup"><span data-stu-id="54aa5-289">Use portal</span></span>
<span data-ttu-id="54aa5-290">Чтобы переместить ресурсы, выберите группу ресурсов, которая содержит эти ресурсы, а затем нажмите кнопку **Переместить**.</span><span class="sxs-lookup"><span data-stu-id="54aa5-290">To move resources, select the resource group containing those resources, and then select the **Move** button.</span></span>

![перемещение ресурсов](./media/resource-group-move-resources/select-move.png)

<span data-ttu-id="54aa5-292">Укажите, куда будут перемещены ресурсы: в новую группу ресурсов или новую подписку.</span><span class="sxs-lookup"><span data-stu-id="54aa5-292">Select whether you are moving the resources to a new resource group or a new subscription.</span></span>

<span data-ttu-id="54aa5-293">Выберите ресурсы, которые необходимо переместить, и целевую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="54aa5-293">Select the resources to move and the destination resource group.</span></span> <span data-ttu-id="54aa5-294">Подтвердите обновление сценариев для этих ресурсов и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="54aa5-294">Acknowledge that you need to update scripts for these resources and select **OK**.</span></span> <span data-ttu-id="54aa5-295">Если на предыдущем шаге был выбран значок редактирования подписки, то также необходимо выбрать целевую подписку.</span><span class="sxs-lookup"><span data-stu-id="54aa5-295">If you selected the edit subscription icon in the previous step, you must also select the destination subscription.</span></span>

![выбор места назначения](./media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="54aa5-297">В области **уведомлений**вы увидите, что операция перемещения выполняется.</span><span class="sxs-lookup"><span data-stu-id="54aa5-297">In **Notifications**, you see that the move operation is running.</span></span>

![отображение состояния перемещения](./media/resource-group-move-resources/show-status.png)

<span data-ttu-id="54aa5-299">После ее завершения отобразится уведомление о результате.</span><span class="sxs-lookup"><span data-stu-id="54aa5-299">When it has completed, you are notified of the result.</span></span>

![отображение результата перемещения](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="54aa5-301">Использование PowerShell</span><span class="sxs-lookup"><span data-stu-id="54aa5-301">Use PowerShell</span></span>
<span data-ttu-id="54aa5-302">Чтобы переместить существующие ресурсы в другую группу ресурсов или подписку, выполните команду `Move-AzureRmResource`.</span><span class="sxs-lookup"><span data-stu-id="54aa5-302">To move existing resources to another resource group or subscription, use the `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="54aa5-303">В первом примере показано, как переместить один ресурс в новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="54aa5-303">The first example shows how to move one resource to a new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="54aa5-304">Во втором примере показано, как переместить несколько ресурсов в новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="54aa5-304">The second example shows how to move multiple resources to a new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="54aa5-305">Чтобы переместить ресурс в новую подписку, добавьте значение параметра `DestinationSubscriptionId`.</span><span class="sxs-lookup"><span data-stu-id="54aa5-305">To move to a new subscription, include a value for the `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="54aa5-306">Появится запрос на подтверждение перемещения указанных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="54aa5-306">You are asked to confirm that you want to move the specified resources.</span></span>

```powershell
Confirm
Are you sure you want to move these resources to the resource group
'/subscriptions/{guid}/resourceGroups/newRG' the resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="54aa5-307">Использование Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="54aa5-307">Use Azure CLI 2.0</span></span>
<span data-ttu-id="54aa5-308">Чтобы переместить существующие ресурсы в другую группу ресурсов или подписку, выполните команду `az resource move`.</span><span class="sxs-lookup"><span data-stu-id="54aa5-308">To move existing resources to another resource group or subscription, use the `az resource move` command.</span></span> <span data-ttu-id="54aa5-309">Укажите идентификаторы перемещаемых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="54aa5-309">Provide the resource IDs of the resources to move.</span></span> <span data-ttu-id="54aa5-310">Чтобы получить идентификаторы ресурсов, воспользуйтесь следующей командой.</span><span class="sxs-lookup"><span data-stu-id="54aa5-310">You can get resource IDs with the following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="54aa5-311">В следующем примере показано, как переместить учетную запись хранения в новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="54aa5-311">The following example shows how to move a storage account to a new resource group.</span></span> <span data-ttu-id="54aa5-312">В параметре `--ids` укажите перемещаемый список идентификаторов ресурсов с разделителями-пробелами.</span><span class="sxs-lookup"><span data-stu-id="54aa5-312">In the `--ids` parameter, provide a space-separated list of the resource IDs to move.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="54aa5-313">Для перемещения в новую подписку нужно указать параметр `--destination-subscription-id`.</span><span class="sxs-lookup"><span data-stu-id="54aa5-313">To move to a new subscription, provide the `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="54aa5-314">Использование Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="54aa5-314">Use Azure CLI 1.0</span></span>
<span data-ttu-id="54aa5-315">Чтобы переместить существующие ресурсы в другую группу ресурсов или подписку, выполните команду `azure resource move`.</span><span class="sxs-lookup"><span data-stu-id="54aa5-315">To move existing resources to another resource group or subscription, use the `azure resource move` command.</span></span> <span data-ttu-id="54aa5-316">Укажите идентификаторы перемещаемых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="54aa5-316">Provide the resource IDs of the resources to move.</span></span> <span data-ttu-id="54aa5-317">Чтобы получить идентификаторы ресурсов, воспользуйтесь следующей командой.</span><span class="sxs-lookup"><span data-stu-id="54aa5-317">You can get resource IDs with the following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="54aa5-318">Она вернет ответ в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="54aa5-318">Which returns the following format:</span></span>

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

<span data-ttu-id="54aa5-319">В следующем примере показано, как переместить учетную запись хранения в новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="54aa5-319">The following example shows how to move a storage account to a new resource group.</span></span> <span data-ttu-id="54aa5-320">В параметре `-i` укажите перемещаемый список идентификаторов ресурсов с разделителями-запятыми.</span><span class="sxs-lookup"><span data-stu-id="54aa5-320">In the `-i` parameter, provide a comma-separated list of the resource IDs to move.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="54aa5-321">Появится запрос на подтверждение перемещения указанного ресурса.</span><span class="sxs-lookup"><span data-stu-id="54aa5-321">You are asked to confirm that you want to move the specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="54aa5-322">Использование REST API</span><span class="sxs-lookup"><span data-stu-id="54aa5-322">Use REST API</span></span>
<span data-ttu-id="54aa5-323">Чтобы переместить существующие ресурсы в другую группу ресурсов или подписку, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="54aa5-323">To move existing resources to another resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

<span data-ttu-id="54aa5-324">В тексте запроса укажите целевую группу ресурсов и ресурсы для перемещения.</span><span class="sxs-lookup"><span data-stu-id="54aa5-324">In the request body, you specify the target resource group and the resources to move.</span></span> <span data-ttu-id="54aa5-325">Дополнительные сведения об операции перемещения в REST см. в статье [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx) (Перемещение ресурсов).</span><span class="sxs-lookup"><span data-stu-id="54aa5-325">For more information about the move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="54aa5-326">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="54aa5-326">Next steps</span></span>
* <span data-ttu-id="54aa5-327">Сведения о командлетах PowerShell для управления подпиской см. в статье [Использование Azure PowerShell с Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="54aa5-327">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="54aa5-328">Сведения о командах интерфейса командной строки Azure для управления подпиской см. в статье [Управление ресурсами и группами ресурсов Azure с помощью интерфейса командной строки Azure](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="54aa5-328">To learn about Azure CLI commands for managing your subscription, see [Using the Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="54aa5-329">Сведения о функциях портала для управления подпиской см. в статье [Управление ресурсами Azure через портал](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="54aa5-329">To learn about portal features for managing your subscription, see [Using the Azure portal to manage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="54aa5-330">Сведения о логической организации ресурсов см. в разделе [Использование тегов для организации ресурсов в Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="54aa5-330">To learn about applying a logical organization to your resources, see [Using tags to organize your resources](resource-group-using-tags.md).</span></span>
