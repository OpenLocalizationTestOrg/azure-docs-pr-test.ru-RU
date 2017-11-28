---
title: "aaaMove ресурсы Azure toonew подписка или группа ресурсов | Документы Microsoft"
description: "С помощью диспетчера ресурсов Azure toomove ресурсов tooa новую группу ресурсов или подписки."
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
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a><span data-ttu-id="53ca4-103">Переместить группу ресурсов toonew ресурсов или подписку</span><span class="sxs-lookup"><span data-stu-id="53ca4-103">Move resources toonew resource group or subscription</span></span>
<span data-ttu-id="53ca4-104">В этом разделе показано, как ресурсы tooeither toomove новую подписку или новый ресурс в группы hello одной подписке.</span><span class="sxs-lookup"><span data-stu-id="53ca4-104">This topic shows you how toomove resources tooeither a new subscription or a new resource group in hello same subscription.</span></span> <span data-ttu-id="53ca4-105">Можно использовать портал hello, PowerShell, Azure CLI или hello ресурс toomove REST API.</span><span class="sxs-lookup"><span data-stu-id="53ca4-105">You can use hello portal, PowerShell, Azure CLI, or hello REST API toomove resource.</span></span> <span data-ttu-id="53ca4-106">операции перемещения Hello в этом разделе, доступны tooyou безо всякой помощи со службой поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="53ca4-106">hello move operations in this topic are available tooyou without any assistance from Azure support.</span></span>

<span data-ttu-id="53ca4-107">При перемещении ресурсов, исходная группа hello и целевая группа hello блокируются во время операции hello.</span><span class="sxs-lookup"><span data-stu-id="53ca4-107">When moving resources, both hello source group and hello target group are locked during hello operation.</span></span> <span data-ttu-id="53ca4-108">Записи и удаления операций заблокированы для групп ресурсов hello до завершения перемещения hello.</span><span class="sxs-lookup"><span data-stu-id="53ca4-108">Write and delete operations are blocked on hello resource groups until hello move completes.</span></span> <span data-ttu-id="53ca4-109">Эта блокировка означает невозможно добавить, обновить или удалить ресурсов в группах ресурсов hello, но это означает, что ресурсы hello, зафиксированы.</span><span class="sxs-lookup"><span data-stu-id="53ca4-109">This lock means you cannot add, update, or delete resources in hello resource groups, but it does not mean hello resources are frozen.</span></span> <span data-ttu-id="53ca4-110">Например при перемещении SQL Server и его базы данных tooa группы ресурсов, приложение, использующее hello базы данных приложений без простоев.</span><span class="sxs-lookup"><span data-stu-id="53ca4-110">For example, if you move a SQL Server and its database tooa new resource group, an application that uses hello database experiences no downtime.</span></span> <span data-ttu-id="53ca4-111">Он по-прежнему могут читать и записывать toohello базы данных.</span><span class="sxs-lookup"><span data-stu-id="53ca4-111">It can still read and write toohello database.</span></span>

<span data-ttu-id="53ca4-112">Невозможно изменить расположение hello hello ресурса.</span><span class="sxs-lookup"><span data-stu-id="53ca4-112">You cannot change hello location of hello resource.</span></span> <span data-ttu-id="53ca4-113">Перемещение ресурса только перемещение его tooa новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="53ca4-113">Moving a resource only moves it tooa new resource group.</span></span> <span data-ttu-id="53ca4-114">Hello группы ресурсов может иметь другое расположение, но не изменяет расположение hello hello ресурса.</span><span class="sxs-lookup"><span data-stu-id="53ca4-114">hello new resource group may have a different location, but that does not change hello location of hello resource.</span></span>

> [!NOTE]
> <span data-ttu-id="53ca4-115">В этой статье описывается, как toomove ресурсов в Azure существующей учетной записи предложения.</span><span class="sxs-lookup"><span data-stu-id="53ca4-115">This article describes how toomove resources within an existing Azure account offering.</span></span> <span data-ttu-id="53ca4-116">См. учетную запись Azure предложения (например, обновление с оплатой по мере использования toopre зарплаты), продолжая toowork с существующие ресурсы, если требуется фактически toochange [переключения вашего предложения подписки Azure tooanother](../billing/billing-how-to-switch-azure-offer.md).</span><span class="sxs-lookup"><span data-stu-id="53ca4-116">If you actually want toochange your Azure account offering (such as upgrading from pay-as-you-go toopre-pay) while continuing toowork with your existing resources, see [Switch your Azure subscription tooanother offer](../billing/billing-how-to-switch-azure-offer.md).</span></span>
>
>

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="53ca4-117">Рекомендации перед перемещением ресурсов</span><span class="sxs-lookup"><span data-stu-id="53ca4-117">Checklist before moving resources</span></span>
<span data-ttu-id="53ca4-118">Существуют некоторые важные действия tooperform перед перемещением ресурса.</span><span class="sxs-lookup"><span data-stu-id="53ca4-118">There are some important steps tooperform before moving a resource.</span></span> <span data-ttu-id="53ca4-119">Проверив эти условия, можно избежать ошибок.</span><span class="sxs-lookup"><span data-stu-id="53ca4-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="53ca4-120">Hello источника и назначения подписки должен существовать внутри hello же [клиента Azure Active Directory](../active-directory/active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="53ca4-120">hello source and destination subscriptions must exist within hello same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="53ca4-121">toocheck, что обе подписки имеют hello таким же Идентификатором клиента, с помощью Azure PowerShell или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="53ca4-121">toocheck that both subscriptions have hello same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="53ca4-122">Для Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="53ca4-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="53ca4-123">В Azure CLI 2.0 используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="53ca4-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="53ca4-124">Если идентификаторы клиента hello hello исходный и целевой подписки не же hello, можно попытаться каталога hello toochange для hello подписки.</span><span class="sxs-lookup"><span data-stu-id="53ca4-124">If hello tenant IDs for hello source and destination subscriptions are not hello same, you can attempt toochange hello directory for hello subscription.</span></span> <span data-ttu-id="53ca4-125">Тем не менее это может быть только доступные tooService Администраторы, выполнившие вход с учетной записью Майкрософт (не учетная запись организации).</span><span class="sxs-lookup"><span data-stu-id="53ca4-125">However, this option is only available tooService Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="53ca4-126">Изменение каталога hello, вход toohello tooattempt [классический портал](https://manage.windowsazure.com/)и выберите **параметры**и выберите подписку hello.</span><span class="sxs-lookup"><span data-stu-id="53ca4-126">tooattempt changing hello directory, log in toohello [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select hello subscription.</span></span> <span data-ttu-id="53ca4-127">Если hello **изменить каталог** значок, выберите его toochange hello связанные Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="53ca4-127">If hello **Edit Directory** icon is available, select it toochange hello associated Azure Active Directory.</span></span>

  ![Изменение каталога](./media/resource-group-move-resources/edit-directory.png)

  <span data-ttu-id="53ca4-129">Если этот значок недоступен, необходимо обратитесь в службу поддержки toomove hello ресурсы tooa новым клиентом.</span><span class="sxs-lookup"><span data-stu-id="53ca4-129">If that icon is not available, you must contact support toomove hello resources tooa new tenant.</span></span>

2. <span data-ttu-id="53ca4-130">Hello службы необходимо включить hello возможность toomove ресурсов.</span><span class="sxs-lookup"><span data-stu-id="53ca4-130">hello service must enable hello ability toomove resources.</span></span> <span data-ttu-id="53ca4-131">В этом разделе перечислено, какие службы позволяют перемещать ресурсы, а какие — нет.</span><span class="sxs-lookup"><span data-stu-id="53ca4-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="53ca4-132">Hello назначения подписки должны быть зарегистрированы для поставщика ресурсов hello перемещения ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="53ca4-132">hello destination subscription must be registered for hello resource provider of hello resource being moved.</span></span> <span data-ttu-id="53ca4-133">Если нет, появится сообщение о том, что hello **подписка не зарегистрирована для типа ресурса**.</span><span class="sxs-lookup"><span data-stu-id="53ca4-133">If not, you receive an error stating that hello **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="53ca4-134">Этой проблемы могут возникнуть при перемещении ресурсов tooa новую подписку, но никогда не использовалось этой подписки с этим типом ресурса.</span><span class="sxs-lookup"><span data-stu-id="53ca4-134">You might encounter this problem when moving a resource tooa new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="53ca4-135">toolearn toocheck hello состояние регистрации и регистрации поставщиков ресурсов разделе [поставщиков ресурсов и типы](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="53ca4-135">toolearn how toocheck hello registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="when-toocall-support"></a><span data-ttu-id="53ca4-136">Когда поддержка toocall</span><span class="sxs-lookup"><span data-stu-id="53ca4-136">When toocall support</span></span>
<span data-ttu-id="53ca4-137">Можно переместить больше всего ресурсов через операции самообслуживания hello, приведенные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="53ca4-137">You can move most resources through hello self-service operations shown in this topic.</span></span> <span data-ttu-id="53ca4-138">Используйте hello самообслуживания операций:</span><span class="sxs-lookup"><span data-stu-id="53ca4-138">Use hello self-service operations to:</span></span>

* <span data-ttu-id="53ca4-139">перемещение ресурсов Resource Manager;</span><span class="sxs-lookup"><span data-stu-id="53ca4-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="53ca4-140">Переместить классические ресурсы в соответствии с toohello [ограничения классического развертывания](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="53ca4-140">Move classic resources according toohello [classic deployment limitations](#classic-deployment-limitations).</span></span>

<span data-ttu-id="53ca4-141">Обратитесь в службу поддержки, если необходимо выполнить такие действия:</span><span class="sxs-lookup"><span data-stu-id="53ca4-141">Call support when you need to:</span></span>

* <span data-ttu-id="53ca4-142">Перемещение ресурсов tooa новую учетную запись Azure (и клиент Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="53ca4-142">Move your resources tooa new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="53ca4-143">Переместить классические ресурсы, но возникают проблемы с ограничениями hello.</span><span class="sxs-lookup"><span data-stu-id="53ca4-143">Move classic resources but are having trouble with hello limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="53ca4-144">Службы, поддерживающие перемещение</span><span class="sxs-lookup"><span data-stu-id="53ca4-144">Services that enable move</span></span>
<span data-ttu-id="53ca4-145">Пока используются следующие службы hello, позволяющие выполнять перемещение tooboth новую группу ресурсов и подписки:</span><span class="sxs-lookup"><span data-stu-id="53ca4-145">For now, hello services that enable moving tooboth a new resource group and subscription are:</span></span>

* <span data-ttu-id="53ca4-146">Управление API</span><span class="sxs-lookup"><span data-stu-id="53ca4-146">API Management</span></span>
* <span data-ttu-id="53ca4-147">Приложения службы приложений (веб-приложения) — см. раздел [Ограничения службы приложений](#app-service-limitations).</span><span class="sxs-lookup"><span data-stu-id="53ca4-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="53ca4-148">Application Insights</span><span class="sxs-lookup"><span data-stu-id="53ca4-148">Application Insights</span></span>
* <span data-ttu-id="53ca4-149">Автоматизация</span><span class="sxs-lookup"><span data-stu-id="53ca4-149">Automation</span></span>
* <span data-ttu-id="53ca4-150">Пакетная служба</span><span class="sxs-lookup"><span data-stu-id="53ca4-150">Batch</span></span>
* <span data-ttu-id="53ca4-151">Карты Bing</span><span class="sxs-lookup"><span data-stu-id="53ca4-151">Bing Maps</span></span>
* <span data-ttu-id="53ca4-152">CDN</span><span class="sxs-lookup"><span data-stu-id="53ca4-152">CDN</span></span>
* <span data-ttu-id="53ca4-153">Облачные службы — см. раздел [Ограничения классического развертывания](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="53ca4-153">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="53ca4-154">Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="53ca4-154">Cognitive Services</span></span>
* <span data-ttu-id="53ca4-155">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="53ca4-155">Content Moderator</span></span>
* <span data-ttu-id="53ca4-156">Каталог данных</span><span class="sxs-lookup"><span data-stu-id="53ca4-156">Data Catalog</span></span>
* <span data-ttu-id="53ca4-157">Фабрика данных</span><span class="sxs-lookup"><span data-stu-id="53ca4-157">Data Factory</span></span>
* <span data-ttu-id="53ca4-158">Аналитика озера данных</span><span class="sxs-lookup"><span data-stu-id="53ca4-158">Data Lake Analytics</span></span>
* <span data-ttu-id="53ca4-159">Хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="53ca4-159">Data Lake Store</span></span>
* <span data-ttu-id="53ca4-160">DNS</span><span class="sxs-lookup"><span data-stu-id="53ca4-160">DNS</span></span>
* <span data-ttu-id="53ca4-161">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="53ca4-161">Azure Cosmos DB</span></span>
* <span data-ttu-id="53ca4-162">Концентраторы событий</span><span class="sxs-lookup"><span data-stu-id="53ca4-162">Event Hubs</span></span>
* <span data-ttu-id="53ca4-163">Кластеры HDInsight — см. раздел [Ограничения HDInsight](#hdinsight-limitations).</span><span class="sxs-lookup"><span data-stu-id="53ca4-163">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="53ca4-164">Центры Интернета вещей;</span><span class="sxs-lookup"><span data-stu-id="53ca4-164">IoT Hubs</span></span>
* <span data-ttu-id="53ca4-165">Хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="53ca4-165">Key Vault</span></span>
* <span data-ttu-id="53ca4-166">Балансировщики нагрузки</span><span class="sxs-lookup"><span data-stu-id="53ca4-166">Load Balancers</span></span>
* <span data-ttu-id="53ca4-167">Приложения логики</span><span class="sxs-lookup"><span data-stu-id="53ca4-167">Logic Apps</span></span>
* <span data-ttu-id="53ca4-168">Машинное обучение</span><span class="sxs-lookup"><span data-stu-id="53ca4-168">Machine Learning</span></span>
* <span data-ttu-id="53ca4-169">Службы мультимедиа</span><span class="sxs-lookup"><span data-stu-id="53ca4-169">Media Services</span></span>
* <span data-ttu-id="53ca4-170">Службы мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="53ca4-170">Mobile Engagement</span></span>
* <span data-ttu-id="53ca4-171">Центры уведомлений</span><span class="sxs-lookup"><span data-stu-id="53ca4-171">Notification Hubs</span></span>
* <span data-ttu-id="53ca4-172">Operational Insights;</span><span class="sxs-lookup"><span data-stu-id="53ca4-172">Operational Insights</span></span>
* <span data-ttu-id="53ca4-173">Пакет Operations Management</span><span class="sxs-lookup"><span data-stu-id="53ca4-173">Operations Management</span></span>
* <span data-ttu-id="53ca4-174">Power BI</span><span class="sxs-lookup"><span data-stu-id="53ca4-174">Power BI</span></span>
* <span data-ttu-id="53ca4-175">Кэш Redis</span><span class="sxs-lookup"><span data-stu-id="53ca4-175">Redis Cache</span></span>
* <span data-ttu-id="53ca4-176">Планировщик</span><span class="sxs-lookup"><span data-stu-id="53ca4-176">Scheduler</span></span>
* <span data-ttu-id="53ca4-177">Поиск</span><span class="sxs-lookup"><span data-stu-id="53ca4-177">Search</span></span>
* <span data-ttu-id="53ca4-178">Управление сервером</span><span class="sxs-lookup"><span data-stu-id="53ca4-178">Server Management</span></span>
* <span data-ttu-id="53ca4-179">Служебная шина</span><span class="sxs-lookup"><span data-stu-id="53ca4-179">Service Bus</span></span>
* <span data-ttu-id="53ca4-180">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="53ca4-180">Service Fabric</span></span>
* <span data-ttu-id="53ca4-181">Хранилище</span><span class="sxs-lookup"><span data-stu-id="53ca4-181">Storage</span></span>
* <span data-ttu-id="53ca4-182">Служба хранилища (классическая) — см. раздел [Ограничения классического развертывания](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="53ca4-182">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="53ca4-183">Stream Analytics — задание Stream Analytics в состоянии выполнения нельзя переместить.</span><span class="sxs-lookup"><span data-stu-id="53ca4-183">Stream Analytics - Stream Analytics jobs cannot be moved when in running state.</span></span>
* <span data-ttu-id="53ca4-184">Сервер базы данных SQL - hello базы данных и сервер должны находиться в hello одну группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="53ca4-184">SQL Database server - hello database and server must reside in hello same resource group.</span></span> <span data-ttu-id="53ca4-185">При перемещении сервера SQL Server все его базы данных также перемещаются.</span><span class="sxs-lookup"><span data-stu-id="53ca4-185">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="53ca4-186">Диспетчер трафика</span><span class="sxs-lookup"><span data-stu-id="53ca4-186">Traffic Manager</span></span>
* <span data-ttu-id="53ca4-187">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="53ca4-187">Virtual Machines</span></span>
* <span data-ttu-id="53ca4-188">Виртуальные машины с сертификатом, который хранится в хранилище ключей — перемещение группы ресурсов toonew в той же подписке включена, но перемещения перекрестного подписки не включен.</span><span class="sxs-lookup"><span data-stu-id="53ca4-188">Virtual Machines with certificate stored in Key Vault - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="53ca4-189">Виртуальные машины (классические) — см. раздел [Ограничения классического развертывания](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="53ca4-189">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="53ca4-190">Наборы для масштабирования виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="53ca4-190">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="53ca4-191">Виртуальные сети. В настоящее время невозможно переместить пиринговую виртуальную сеть, пока не будет отключен ее пиринг.</span><span class="sxs-lookup"><span data-stu-id="53ca4-191">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="53ca4-192">После отключения hello виртуальной сети успешно перенести и пиринг hello виртуальной сети можно включить.</span><span class="sxs-lookup"><span data-stu-id="53ca4-192">Once disabled, hello Virtual Network can be moved successfully and hello VNet peering can be enabled.</span></span> <span data-ttu-id="53ca4-193">Кроме того виртуальной сети не может быть перемещенный tooa другую подписку, если какой-либо подсети с ссылками для перехода ресурса содержит hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="53ca4-193">In addition, a Virtual Network cannot be moved tooa different subscription if hello Virtual Network contains any subnet with resource navigation links.</span></span> <span data-ttu-id="53ca4-194">Например, подсеть виртуальной сети содержит ссылку перехода к ресурсу, когда ресурс Redis Microsoft.Cache развертывается в этой подсети.</span><span class="sxs-lookup"><span data-stu-id="53ca4-194">For example, a Virtual Network subnet has a resource navigation link when a Microsoft.Cache redis resource is deployed into this subnet.</span></span>
* <span data-ttu-id="53ca4-195">VPN-шлюз</span><span class="sxs-lookup"><span data-stu-id="53ca4-195">VPN Gateway</span></span>


## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="53ca4-196">Службы, не поддерживающие перемещение</span><span class="sxs-lookup"><span data-stu-id="53ca4-196">Services that do not enable move</span></span>
<span data-ttu-id="53ca4-197">Hello службы, которые в настоящее время не включайте Перемещение ресурса:</span><span class="sxs-lookup"><span data-stu-id="53ca4-197">hello services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="53ca4-198">доменные службы Active Directory;</span><span class="sxs-lookup"><span data-stu-id="53ca4-198">AD Domain Services</span></span>
* <span data-ttu-id="53ca4-199">служба работоспособности гибридного AD;</span><span class="sxs-lookup"><span data-stu-id="53ca4-199">AD Hybrid Health Service</span></span>
* <span data-ttu-id="53ca4-200">Шлюз приложений</span><span class="sxs-lookup"><span data-stu-id="53ca4-200">Application Gateway</span></span>
* <span data-ttu-id="53ca4-201">Группы доступности, содержащие виртуальные машины с управляемыми дисками.</span><span class="sxs-lookup"><span data-stu-id="53ca4-201">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="53ca4-202">Службы BizTalk</span><span class="sxs-lookup"><span data-stu-id="53ca4-202">BizTalk Services</span></span>
* <span data-ttu-id="53ca4-203">Служба контейнеров</span><span class="sxs-lookup"><span data-stu-id="53ca4-203">Container Service</span></span>
* <span data-ttu-id="53ca4-204">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="53ca4-204">Express Route</span></span>
* <span data-ttu-id="53ca4-205">DevTest Labs - переместить группу ресурсов toonew в той же подписке включена, но кросс-перемещение подписки не включен.</span><span class="sxs-lookup"><span data-stu-id="53ca4-205">DevTest Labs - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="53ca4-206">Dynamics LCS.</span><span class="sxs-lookup"><span data-stu-id="53ca4-206">Dynamics LCS</span></span>
* <span data-ttu-id="53ca4-207">Образы, созданные из управляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="53ca4-207">Images created from Managed Disks</span></span>
* <span data-ttu-id="53ca4-208">Управляемые диски</span><span class="sxs-lookup"><span data-stu-id="53ca4-208">Managed Disks</span></span>
* <span data-ttu-id="53ca4-209">Управляемые приложения.</span><span class="sxs-lookup"><span data-stu-id="53ca4-209">Managed Applications</span></span>
* <span data-ttu-id="53ca4-210">Хранилище служб восстановления — также не перемещения hello вычисления, сети и хранилища ресурсы, связанные с подстроку hello служб восстановления хранилище см. в разделе [ограничения службы восстановления](#recovery-services-limitations).</span><span class="sxs-lookup"><span data-stu-id="53ca4-210">Recovery Services vault - also do not move hello Compute, Network, and Storage resources associated with hello Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="53ca4-211">Безопасность</span><span class="sxs-lookup"><span data-stu-id="53ca4-211">Security</span></span>
* <span data-ttu-id="53ca4-212">Моментальные снимки, созданные из управляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="53ca4-212">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="53ca4-213">Диспетчер устройств StorSimple</span><span class="sxs-lookup"><span data-stu-id="53ca4-213">StorSimple Device Manager</span></span>
* <span data-ttu-id="53ca4-214">Виртуальные машины с Управляемыми дисками</span><span class="sxs-lookup"><span data-stu-id="53ca4-214">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="53ca4-215">Виртуальные сети (классические) — см. раздел [Ограничения классического развертывания](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="53ca4-215">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="53ca4-216">Виртуальные машины, созданные из ресурсов Marketplace, невозможно переместить между подписками.</span><span class="sxs-lookup"><span data-stu-id="53ca4-216">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="53ca4-217">Ресурс должен toobe отозваны в текущей подписке hello и выполнить развертывание повторно в новой подписки hello</span><span class="sxs-lookup"><span data-stu-id="53ca4-217">Resource needs toobe deprovisioned in hello current subscription and deployed again in hello new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="53ca4-218">Ограничения службы приложений</span><span class="sxs-lookup"><span data-stu-id="53ca4-218">App Service limitations</span></span>
<span data-ttu-id="53ca4-219">При работе с приложениями службы приложений невозможно переместить только план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="53ca4-219">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="53ca4-220">приложения служб приложений toomove, имеются следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="53ca4-220">toomove App Service apps, your options are:</span></span>

* <span data-ttu-id="53ca4-221">Переместите hello план служб приложений и остальные ресурсы службы приложения, ресурсов группы tooa группы ресурсов, не имеет ресурсы службы приложений.</span><span class="sxs-lookup"><span data-stu-id="53ca4-221">Move hello App Service plan and all other App Service resources in that resource group tooa new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="53ca4-222">Это требование, что означает, что необходимо переместить даже hello ресурсов приложения службы, не связаны с hello план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="53ca4-222">This requirement means you must move even hello App Service resources that are not associated with hello App Service plan.</span></span>
* <span data-ttu-id="53ca4-223">Переместить hello приложений tooa другой группе ресурсов, но сохранить все планы служб приложений в hello исходной группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="53ca4-223">Move hello apps tooa different resource group, but keep all App Service plans in hello original resource group.</span></span>

<span data-ttu-id="53ca4-224">Hello необязательно tooreside в плане служб приложений hello же группе ресурсов, что приложение hello для toofunction приложения hello правильно.</span><span class="sxs-lookup"><span data-stu-id="53ca4-224">hello App Service plan does not need tooreside in hello same resource group as hello app for hello app toofunction correctly.</span></span>

<span data-ttu-id="53ca4-225">Например, если группа ресурсов содержит:</span><span class="sxs-lookup"><span data-stu-id="53ca4-225">For example, if your resource group contains:</span></span>

* <span data-ttu-id="53ca4-226">ресурс **web-a**, связанный с **plan-a**;</span><span class="sxs-lookup"><span data-stu-id="53ca4-226">**web-a** which is associated with **plan-a**</span></span>
* <span data-ttu-id="53ca4-227">ресурс **web-b**, связанный с **plan-b**.</span><span class="sxs-lookup"><span data-stu-id="53ca4-227">**web-b** which is associated with **plan-b**</span></span>

<span data-ttu-id="53ca4-228">Вам доступны следующие действия:</span><span class="sxs-lookup"><span data-stu-id="53ca4-228">Your options are:</span></span>

* <span data-ttu-id="53ca4-229">перемещение **web-a**, **plan-a**, **web-b**, и **plan-b**;</span><span class="sxs-lookup"><span data-stu-id="53ca4-229">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="53ca4-230">перемещение **web-a** и **web-b**;</span><span class="sxs-lookup"><span data-stu-id="53ca4-230">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="53ca4-231">перемещение **web-a**</span><span class="sxs-lookup"><span data-stu-id="53ca4-231">Move **web-a**</span></span>
* <span data-ttu-id="53ca4-232">перемещение **web-b**</span><span class="sxs-lookup"><span data-stu-id="53ca4-232">Move **web-b**</span></span>

<span data-ttu-id="53ca4-233">Все другие сочетания включают необходимость оставить тип ресурса, который нельзя оставлять при перемещении плана службы приложений (любой тип ресурса службы приложений).</span><span class="sxs-lookup"><span data-stu-id="53ca4-233">All other combinations involve leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="53ca4-234">Если веб-приложение находится в группе ресурсов, отличной от его план служб приложений, но требуется toomove оба tooa группы ресурсов, необходимо выполнить перемещение hello в два этапа.</span><span class="sxs-lookup"><span data-stu-id="53ca4-234">If your web app resides in a different resource group than its App Service plan but you want toomove both tooa new resource group, you must perform hello move in two steps.</span></span> <span data-ttu-id="53ca4-235">Например:</span><span class="sxs-lookup"><span data-stu-id="53ca4-235">For example:</span></span>

* <span data-ttu-id="53ca4-236">**web-a** находится в группе **web-group**;</span><span class="sxs-lookup"><span data-stu-id="53ca4-236">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="53ca4-237">**plan-a** находится в группе **plan-group**;</span><span class="sxs-lookup"><span data-stu-id="53ca4-237">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="53ca4-238">Вы хотите **веб a** и **плана a** tooreside в **объединять группы**</span><span class="sxs-lookup"><span data-stu-id="53ca4-238">You want **web-a** and **plan-a** tooreside in **combined-group**</span></span>

<span data-ttu-id="53ca4-239">tooaccomplish необходимо переместить, выполнять операции два отдельных перемещения в hello следующая последовательность:</span><span class="sxs-lookup"><span data-stu-id="53ca4-239">tooaccomplish this move, perform two separate move operations in hello following sequence:</span></span>

1. <span data-ttu-id="53ca4-240">Переместить hello **веб a** слишком**группа планов**</span><span class="sxs-lookup"><span data-stu-id="53ca4-240">Move hello **web-a** too**plan-group**</span></span>
2. <span data-ttu-id="53ca4-241">Переместить **веб a** и **плана a** слишком**объединять группы**.</span><span class="sxs-lookup"><span data-stu-id="53ca4-241">Move **web-a** and **plan-a** too**combined-group**.</span></span>

<span data-ttu-id="53ca4-242">Можно переместить сертификат службы приложения tooa группы ресурсов или подписку без проблем.</span><span class="sxs-lookup"><span data-stu-id="53ca4-242">You can move an App Service Certificate tooa new resource group or subscription without any issues.</span></span> <span data-ttu-id="53ca4-243">Тем не менее если веб-приложение включает сертификат SSL, приобретенных извне и отправлены toohello приложения, необходимо удалить сертификат hello до перемещения веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="53ca4-243">However, if your web app includes an SSL certificate that you purchased externally and uploaded toohello app, you must delete hello certificate before moving hello web app.</span></span> <span data-ttu-id="53ca4-244">Например можно выполнить hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="53ca4-244">For example, you can perform hello following steps:</span></span>

1. <span data-ttu-id="53ca4-245">Удалить сертификат hello загружен из веб-приложения hello</span><span class="sxs-lookup"><span data-stu-id="53ca4-245">Delete hello uploaded certificate from hello web app</span></span>
2. <span data-ttu-id="53ca4-246">Перемещение веб-приложения hello</span><span class="sxs-lookup"><span data-stu-id="53ca4-246">Move hello web app</span></span>
3. <span data-ttu-id="53ca4-247">Отправка hello сертификат toohello веб-приложения</span><span class="sxs-lookup"><span data-stu-id="53ca4-247">Upload hello certificate toohello web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="53ca4-248">Ограничения служб восстановления</span><span class="sxs-lookup"><span data-stu-id="53ca4-248">Recovery Services limitations</span></span>
<span data-ttu-id="53ca4-249">Перемещение не включена для хранилища, сети, или вычислительные ресурсы используются tooset настройки аварийного восстановления с помощью Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="53ca4-249">Move is not enabled for Storage, Network, or Compute resources used tooset up disaster recovery with Azure Site Recovery.</span></span>

<span data-ttu-id="53ca4-250">Например предположим, что вы настроили репликации из локальной машины tooa учетной записи хранения (Storage1) и хотите hello защищенные машины toocome копии после отработки отказа tooAzure как виртуальной машины (VM1) подключенные tooa виртуальной сети (Network1).</span><span class="sxs-lookup"><span data-stu-id="53ca4-250">For example, suppose you have set up replication of your on-premises machines tooa storage account (Storage1) and want hello protected machine toocome up after failover tooAzure as a virtual machine (VM1) attached tooa virtual network (Network1).</span></span> <span data-ttu-id="53ca4-251">Не удается переместить любой из этих ресурсов Azure - Storage1, VM1, и Network1 - через ресурсов группирует в hello же подписки или в подписках.</span><span class="sxs-lookup"><span data-stu-id="53ca4-251">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within hello same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="53ca4-252">Ограничения HDInsight</span><span class="sxs-lookup"><span data-stu-id="53ca4-252">HDInsight limitations</span></span>

<span data-ttu-id="53ca4-253">Можно переместить HDInsight кластеры tooa новую подписку или группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="53ca4-253">You can move HDInsight clusters tooa new subscription or resource group.</span></span> <span data-ttu-id="53ca4-254">Однако не удалось переместить между подписками hello сети кластера HDInsight toohello связанные ресурсы (например, «hello виртуальной сети, Сетевых или подсистемы балансировки нагрузки).</span><span class="sxs-lookup"><span data-stu-id="53ca4-254">However, you cannot move across subscriptions hello networking resources linked toohello HDInsight cluster (such as hello virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="53ca4-255">Кроме того невозможно переместить tooa группы ресурсов сетевого Адаптера, подключенных tooa виртуальной машины для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="53ca4-255">In addition, you cannot move tooa new resource group a NIC that is attached tooa virtual machine for hello cluster.</span></span>

<span data-ttu-id="53ca4-256">При перемещении кластера HDInsight tooa новую подписку, необходимо сначала переместите другие ресурсы (например, учетная запись хранения hello).</span><span class="sxs-lookup"><span data-stu-id="53ca4-256">When moving an HDInsight cluster tooa new subscription, first move other resources (like hello storage account).</span></span> <span data-ttu-id="53ca4-257">Затем переместите кластера HDInsight hello сам по себе.</span><span class="sxs-lookup"><span data-stu-id="53ca4-257">Then, move hello HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="53ca4-258">Ограничения классического развертывания</span><span class="sxs-lookup"><span data-stu-id="53ca4-258">Classic deployment limitations</span></span>
<span data-ttu-id="53ca4-259">Hello параметры перемещения ресурсов, развернутые с помощью классической модели hello зависят от перемещаемой hello ресурсов в подписке или tooa новую подписку.</span><span class="sxs-lookup"><span data-stu-id="53ca4-259">hello options for moving resources deployed through hello classic model differ based on whether you are moving hello resources within a subscription or tooa new subscription.</span></span>

### <a name="same-subscription"></a><span data-ttu-id="53ca4-260">Та же подписка</span><span class="sxs-lookup"><span data-stu-id="53ca4-260">Same subscription</span></span>
<span data-ttu-id="53ca4-261">При перемещении ресурсов из одной группы tooanother ресурсов группы ресурсов в одной подписке, hello следующие ограничения применяются hello:</span><span class="sxs-lookup"><span data-stu-id="53ca4-261">When moving resources from one resource group tooanother resource group within hello same subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="53ca4-262">Нельзя перемещать виртуальные сети (классические).</span><span class="sxs-lookup"><span data-stu-id="53ca4-262">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="53ca4-263">Виртуальные машины (классические) должны быть перемещены hello облачной службе.</span><span class="sxs-lookup"><span data-stu-id="53ca4-263">Virtual machines (classic) must be moved with hello cloud service.</span></span>
* <span data-ttu-id="53ca4-264">Облачные службы могут перемещаться только в тех случаях, когда перемещения hello включает все виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="53ca4-264">Cloud service can only be moved when hello move includes all its virtual machines.</span></span>
* <span data-ttu-id="53ca4-265">Одновременно можно перемещать только одну облачную службу.</span><span class="sxs-lookup"><span data-stu-id="53ca4-265">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="53ca4-266">Одновременно можно перемещать только одну учетную запись хранения (классическую).</span><span class="sxs-lookup"><span data-stu-id="53ca4-266">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="53ca4-267">Учетная запись хранения (классические) не может быть перемещен в hello одной операции с виртуальной машины или облачной службы.</span><span class="sxs-lookup"><span data-stu-id="53ca4-267">Storage account (classic) cannot be moved in hello same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="53ca4-268">toomove классические ресурсы tooa группы ресурсов в hello той же подписке, используйте стандартный hello перемещении через hello [портала](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), или [API-интерфейса REST](#use-rest-api).</span><span class="sxs-lookup"><span data-stu-id="53ca4-268">toomove classic resources tooa new resource group within hello same subscription, use hello standard move operations through hello [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="53ca4-269">Вы используете hello и те же операции, как использовать для перемещения ресурсов диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="53ca4-269">You use hello same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="53ca4-270">Новая подписка</span><span class="sxs-lookup"><span data-stu-id="53ca4-270">New subscription</span></span>
<span data-ttu-id="53ca4-271">При перемещении ресурсов tooa новую подписку, применяются следующие ограничения hello.</span><span class="sxs-lookup"><span data-stu-id="53ca4-271">When moving resources tooa new subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="53ca4-272">Необходимо переместить все классические ресурсы в подписке hello в hello одной операции.</span><span class="sxs-lookup"><span data-stu-id="53ca4-272">All classic resources in hello subscription must be moved in hello same operation.</span></span>
* <span data-ttu-id="53ca4-273">Hello целевой подписки не должен содержать классические ресурсы.</span><span class="sxs-lookup"><span data-stu-id="53ca4-273">hello target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="53ca4-274">Перемещение Hello можно запросить только через отдельный API REST для классического переход.</span><span class="sxs-lookup"><span data-stu-id="53ca4-274">hello move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="53ca4-275">Hello стандартные команды перемещения диспетчер ресурсов не работают при перемещении классические ресурсы tooa новую подписку.</span><span class="sxs-lookup"><span data-stu-id="53ca4-275">hello standard Resource Manager move commands do not work when moving classic resources tooa new subscription.</span></span>

<span data-ttu-id="53ca4-276">toomove классические ресурсы tooa новую подписку, используйте hello REST операции, которые будут tooclassic определенных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="53ca4-276">toomove classic resources tooa new subscription, use hello REST operations that are specific tooclassic resources.</span></span> <span data-ttu-id="53ca4-277">toouse REST, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="53ca4-277">toouse REST, perform hello following steps:</span></span>

1. <span data-ttu-id="53ca4-278">Проверка, если исходная подписка hello могут участвовать в разных подписок переместить.</span><span class="sxs-lookup"><span data-stu-id="53ca4-278">Check if hello source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="53ca4-279">Используйте следующую операцию hello.</span><span class="sxs-lookup"><span data-stu-id="53ca4-279">Use hello following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="53ca4-280">В тексте запроса hello включают:</span><span class="sxs-lookup"><span data-stu-id="53ca4-280">In hello request body, include:</span></span>

  ```json
  {
    "role": "source"
  }
  ```

     <span data-ttu-id="53ca4-281">Hello ответ для операции проверки hello имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="53ca4-281">hello response for hello validation operation is in hello following format:</span></span>

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="53ca4-282">Флажок, если hello конечная подписка может участвовать в разных подписок переместить.</span><span class="sxs-lookup"><span data-stu-id="53ca4-282">Check if hello destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="53ca4-283">Используйте следующую операцию hello.</span><span class="sxs-lookup"><span data-stu-id="53ca4-283">Use hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="53ca4-284">В тексте запроса hello включают:</span><span class="sxs-lookup"><span data-stu-id="53ca4-284">In hello request body, include:</span></span>

  ```json
  {
    "role": "target"
  }
  ```

     <span data-ttu-id="53ca4-285">Hello ответа находится в том же формате, как проверка подписки источника hello hello.</span><span class="sxs-lookup"><span data-stu-id="53ca4-285">hello response is in hello same format as hello source subscription validation.</span></span>
3. <span data-ttu-id="53ca4-286">Если обе подписки проходят проверку, перемещение всех классических ресурсов из одной подписки tooanother подписки с hello следующую операцию:</span><span class="sxs-lookup"><span data-stu-id="53ca4-286">If both subscriptions pass validation, move all classic resources from one subscription tooanother subscription with hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="53ca4-287">В тексте запроса hello включают:</span><span class="sxs-lookup"><span data-stu-id="53ca4-287">In hello request body, include:</span></span>

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="53ca4-288">Hello операция может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="53ca4-288">hello operation may run for several minutes.</span></span>

## <a name="use-portal"></a><span data-ttu-id="53ca4-289">С помощью портала</span><span class="sxs-lookup"><span data-stu-id="53ca4-289">Use portal</span></span>
<span data-ttu-id="53ca4-290">ресурсы toomove выбрать группу ресурсов hello, содержащие эти ресурсы, а затем выберите hello **переместить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="53ca4-290">toomove resources, select hello resource group containing those resources, and then select hello **Move** button.</span></span>

![перемещение ресурсов](./media/resource-group-move-resources/select-move.png)

<span data-ttu-id="53ca4-292">Выберите, будут ли перемещении hello ресурсы tooa группы ресурсов или новую подписку.</span><span class="sxs-lookup"><span data-stu-id="53ca4-292">Select whether you are moving hello resources tooa new resource group or a new subscription.</span></span>

<span data-ttu-id="53ca4-293">Выберите toomove hello ресурсы и группы ресурсов целевой hello.</span><span class="sxs-lookup"><span data-stu-id="53ca4-293">Select hello resources toomove and hello destination resource group.</span></span> <span data-ttu-id="53ca4-294">Подтвердить необходимость tooupdate скрипты для этих ресурсов и выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="53ca4-294">Acknowledge that you need tooupdate scripts for these resources and select **OK**.</span></span> <span data-ttu-id="53ca4-295">Если вы выбрали hello Правка подписки на предыдущем шаге hello, необходимо выбрать hello конечная подписка.</span><span class="sxs-lookup"><span data-stu-id="53ca4-295">If you selected hello edit subscription icon in hello previous step, you must also select hello destination subscription.</span></span>

![выбор места назначения](./media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="53ca4-297">В **уведомления**, вы видите, hello перемещение выполняется операция.</span><span class="sxs-lookup"><span data-stu-id="53ca4-297">In **Notifications**, you see that hello move operation is running.</span></span>

![отображение состояния перемещения](./media/resource-group-move-resources/show-status.png)

<span data-ttu-id="53ca4-299">После ее завершения, получают уведомления hello результата.</span><span class="sxs-lookup"><span data-stu-id="53ca4-299">When it has completed, you are notified of hello result.</span></span>

![отображение результата перемещения](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="53ca4-301">Использование PowerShell</span><span class="sxs-lookup"><span data-stu-id="53ca4-301">Use PowerShell</span></span>
<span data-ttu-id="53ca4-302">toomove существующую группу ресурсов tooanother ресурсов или подписку, используйте hello `Move-AzureRmResource` команды.</span><span class="sxs-lookup"><span data-stu-id="53ca4-302">toomove existing resources tooanother resource group or subscription, use hello `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="53ca4-303">Hello в первом примере показан способ toomove один ресурс tooa группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="53ca4-303">hello first example shows how toomove one resource tooa new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="53ca4-304">Hello второй пример показывает, как toomove несколько ресурсов tooa новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="53ca4-304">hello second example shows how toomove multiple resources tooa new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="53ca4-305">toomove tooa новую подписку, добавьте значение hello `DestinationSubscriptionId` параметра.</span><span class="sxs-lookup"><span data-stu-id="53ca4-305">toomove tooa new subscription, include a value for hello `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="53ca4-306">Будет предложено ресурсов, указанных tooconfirm, что требуется toomove hello.</span><span class="sxs-lookup"><span data-stu-id="53ca4-306">You are asked tooconfirm that you want toomove hello specified resources.</span></span>

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="53ca4-307">Использование Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="53ca4-307">Use Azure CLI 2.0</span></span>
<span data-ttu-id="53ca4-308">toomove существующую группу ресурсов tooanother ресурсов или подписку, используйте hello `az resource move` команды.</span><span class="sxs-lookup"><span data-stu-id="53ca4-308">toomove existing resources tooanother resource group or subscription, use hello `az resource move` command.</span></span> <span data-ttu-id="53ca4-309">Укажите идентификаторы ресурсов toomove hello hello ресурса.</span><span class="sxs-lookup"><span data-stu-id="53ca4-309">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="53ca4-310">Идентификаторы ресурсов можно получить с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="53ca4-310">You can get resource IDs with hello following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="53ca4-311">Следующий пример Hello показано, как toomove хранилища учетной записи tooa новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="53ca4-311">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="53ca4-312">В hello `--ids` параметр, укажите разделенный пробелами список toomove идентификаторы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="53ca4-312">In hello `--ids` parameter, provide a space-separated list of hello resource IDs toomove.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="53ca4-313">toomove tooa новую подписку, укажите hello `--destination-subscription-id` параметра.</span><span class="sxs-lookup"><span data-stu-id="53ca4-313">toomove tooa new subscription, provide hello `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="53ca4-314">Использование Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="53ca4-314">Use Azure CLI 1.0</span></span>
<span data-ttu-id="53ca4-315">toomove существующую группу ресурсов tooanother ресурсов или подписку, используйте hello `azure resource move` команды.</span><span class="sxs-lookup"><span data-stu-id="53ca4-315">toomove existing resources tooanother resource group or subscription, use hello `azure resource move` command.</span></span> <span data-ttu-id="53ca4-316">Укажите идентификаторы ресурсов toomove hello hello ресурса.</span><span class="sxs-lookup"><span data-stu-id="53ca4-316">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="53ca4-317">Идентификаторы ресурсов можно получить с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="53ca4-317">You can get resource IDs with hello following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="53ca4-318">Выдаются hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="53ca4-318">Which returns hello following format:</span></span>

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

<span data-ttu-id="53ca4-319">Следующий пример Hello показано, как toomove хранилища учетной записи tooa новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="53ca4-319">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="53ca4-320">В hello `-i` параметр, укажите список разделенных запятыми toomove идентификаторы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="53ca4-320">In hello `-i` parameter, provide a comma-separated list of hello resource IDs toomove.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="53ca4-321">Будет предложено нужных toomove hello tooconfirm указанный ресурс.</span><span class="sxs-lookup"><span data-stu-id="53ca4-321">You are asked tooconfirm that you want toomove hello specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="53ca4-322">Использование REST API</span><span class="sxs-lookup"><span data-stu-id="53ca4-322">Use REST API</span></span>
<span data-ttu-id="53ca4-323">toomove существующие ресурсы tooanother группу ресурсов или подписку, запустите:</span><span class="sxs-lookup"><span data-stu-id="53ca4-323">toomove existing resources tooanother resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

<span data-ttu-id="53ca4-324">В тексте запроса hello укажите hello целевая группа ресурсов и ресурсов toomove hello.</span><span class="sxs-lookup"><span data-stu-id="53ca4-324">In hello request body, you specify hello target resource group and hello resources toomove.</span></span> <span data-ttu-id="53ca4-325">Дополнительные сведения об операции REST перемещения hello см. в разделе [перемещение ресурсов](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span><span class="sxs-lookup"><span data-stu-id="53ca4-325">For more information about hello move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="53ca4-326">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="53ca4-326">Next steps</span></span>
* <span data-ttu-id="53ca4-327">в разделе toolearn о командлетах PowerShell для управления подпиской, [с помощью Azure PowerShell с помощью диспетчера ресурсов](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="53ca4-327">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="53ca4-328">в разделе toolearn о командах Azure CLI для управления подпиской, [использование hello Azure CLI с помощью диспетчера ресурсов](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="53ca4-328">toolearn about Azure CLI commands for managing your subscription, see [Using hello Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="53ca4-329">toolearn портала возможности для управления подпиской, в разделе [использование ресурсов Azure портала toomanage hello](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="53ca4-329">toolearn about portal features for managing your subscription, see [Using hello Azure portal toomanage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="53ca4-330">toolearn о применении ресурсов tooyour логическую организацию, в разделе [использование теги tooorganize ресурсов](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="53ca4-330">toolearn about applying a logical organization tooyour resources, see [Using tags tooorganize your resources](resource-group-using-tags.md).</span></span>
