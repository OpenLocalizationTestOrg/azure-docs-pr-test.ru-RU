---
title: "Приступая к работе со службой DNS Azure с помощью портала Azure | Документация Майкрософт"
description: "Узнайте, как создать зону и запись DNS в службе DNS Azure. Это пошаговое руководство описывает создание первых зоны и записи DNS, а также управление ими с помощью портала Azure."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 93b24e3d9fbb3fbb3ea995271fd63d1e82eb9c9e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-the-azure-portal"></a><span data-ttu-id="4c0a8-104">Приступая к работе со службой DNS Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="4c0a8-104">Get started with Azure DNS using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c0a8-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="4c0a8-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="4c0a8-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c0a8-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="4c0a8-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4c0a8-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="4c0a8-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4c0a8-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="4c0a8-109">Эта статья поможет вам создать свою первую зону и первую запись DNS с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-109">This article walks you through the steps to create your first DNS zone and record using the Azure portal.</span></span> <span data-ttu-id="4c0a8-110">Эти действия также можно выполнить с помощью Azure PowerShell или кроссплатформенного интерфейса командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="4c0a8-110">You can also perform these steps using Azure PowerShell or the cross-platform Azure CLI.</span></span>

<span data-ttu-id="4c0a8-111">Зона DNS используется для размещения DNS-записей определенного домена.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="4c0a8-112">Чтобы разместить свой домен в Azure DNS, необходимо создать зону DNS для этого доменного имени.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="4c0a8-113">Каждая запись DNS для вашего домена создается внутри этой зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="4c0a8-114">Наконец, чтобы опубликовать зону DNS в Интернете, необходимо настроить серверы доменных имен для домена.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="4c0a8-115">Каждое из этих действий описано в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-115">Each of these steps is described in the following steps.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="4c0a8-116">Создание зоны DNS</span><span class="sxs-lookup"><span data-stu-id="4c0a8-116">Create a DNS zone</span></span>

1. <span data-ttu-id="4c0a8-117">Выполните вход на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-117">Sign in to the Azure portal</span></span>
2. <span data-ttu-id="4c0a8-118">В главном меню щелкните **Создать > Сети**, а затем щелкните **Зона DNS**, чтобы открыть колонку "Создать зону DNS".</span><span class="sxs-lookup"><span data-stu-id="4c0a8-118">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![Зона DNS](./media/dns-getstarted-portal/openzone650.png)

4. <span data-ttu-id="4c0a8-120">В колонке **Создание зоны DNS** введите следующие значения, а затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-120">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>


   | <span data-ttu-id="4c0a8-121">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="4c0a8-121">**Setting**</span></span> | <span data-ttu-id="4c0a8-122">**Значение**</span><span class="sxs-lookup"><span data-stu-id="4c0a8-122">**Value**</span></span> | <span data-ttu-id="4c0a8-123">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="4c0a8-123">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="4c0a8-124">**Имя**</span><span class="sxs-lookup"><span data-stu-id="4c0a8-124">**Name**</span></span>|<span data-ttu-id="4c0a8-125">contoso.com</span><span class="sxs-lookup"><span data-stu-id="4c0a8-125">contoso.com</span></span>|<span data-ttu-id="4c0a8-126">Имя зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-126">The name of the DNS zone</span></span>|
   |<span data-ttu-id="4c0a8-127">**Подписка**</span><span class="sxs-lookup"><span data-stu-id="4c0a8-127">**Subscription**</span></span>|<span data-ttu-id="4c0a8-128">[Ваша подписка]</span><span class="sxs-lookup"><span data-stu-id="4c0a8-128">[Your subscription]</span></span>|<span data-ttu-id="4c0a8-129">Выберите подписку для создания зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-129">Select a subscription to create the DNS zone in.</span></span>|
   |<span data-ttu-id="4c0a8-130">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="4c0a8-130">**Resource group**</span></span>|<span data-ttu-id="4c0a8-131">**Создать:** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="4c0a8-131">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="4c0a8-132">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-132">Create a resource group.</span></span> <span data-ttu-id="4c0a8-133">Имя группы ресурсов должно быть уникальным в пределах выбранной подписки.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-133">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="4c0a8-134">Дополнительные сведения о группах ресурсов см. в разделе [Группы ресурсов](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) статьи "Общие сведения об Azure Resource Manager".</span><span class="sxs-lookup"><span data-stu-id="4c0a8-134">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="4c0a8-135">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="4c0a8-135">**Location**</span></span>|<span data-ttu-id="4c0a8-136">Запад США</span><span class="sxs-lookup"><span data-stu-id="4c0a8-136">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="4c0a8-137">Этот параметр относится к расположению группы ресурсов и никак не влияет на расположение зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-137">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="4c0a8-138">Расположение зоны DNS всегда является "глобальным" и не отображается.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-138">The DNS zone location is always "global", and is not shown.</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="4c0a8-139">Создание записи DNS</span><span class="sxs-lookup"><span data-stu-id="4c0a8-139">Create a DNS record</span></span>

<span data-ttu-id="4c0a8-140">Следующий пример демонстрирует процесс создания записи типа A.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-140">The following example walks you through the process of creating new 'A' record.</span></span> <span data-ttu-id="4c0a8-141">Сведения о других типах записей и об изменении существующих записей см. в статье [Управление записями и наборами записей DNS с помощью портала Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4c0a8-141">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span> 

1. <span data-ttu-id="4c0a8-142">Создав зону DNS, на портале Azure в области **Избранное** щелкните **Все ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-142">With the DNS Zone created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="4c0a8-143">Щелкните зону DNS **contoso.com** в колонке "Все ресурсы".</span><span class="sxs-lookup"><span data-stu-id="4c0a8-143">Click the **contoso.com** DNS zone in the All resources blade.</span></span> <span data-ttu-id="4c0a8-144">Если выбранная подписка имеет несколько ресурсов, в поле **Фильтровать по имени...** введите **contoso.com**,</span><span class="sxs-lookup"><span data-stu-id="4c0a8-144">If the subscription you selected already has several resources in it, you can enter **contoso.com** in the **Filter by name…**</span></span> <span data-ttu-id="4c0a8-145">чтобы быстро получить доступ к необходимой зоне DNS.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-145">box to easily access the DNS Zone.</span></span>

1. <span data-ttu-id="4c0a8-146">В верхней части этой колонки **Зона DNS** щелкните **Набор записей**, чтобы открыть колонку **Добавление набора записей**.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-146">At the top of the **DNS zone** blade, select **+ Record set** to open the **Add record set** blade.</span></span>

1. <span data-ttu-id="4c0a8-147">В колонке **Добавление набора записей** введите приведенные ниже значения и щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-147">On the **Add record set** blade, enter the following values, and click **OK**.</span></span> <span data-ttu-id="4c0a8-148">В этом примере создается запись A.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-148">In this example, you are creating an A record.</span></span>

   |<span data-ttu-id="4c0a8-149">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="4c0a8-149">**Setting**</span></span> | <span data-ttu-id="4c0a8-150">**Значение**</span><span class="sxs-lookup"><span data-stu-id="4c0a8-150">**Value**</span></span> | <span data-ttu-id="4c0a8-151">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="4c0a8-151">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="4c0a8-152">**Имя**</span><span class="sxs-lookup"><span data-stu-id="4c0a8-152">**Name**</span></span>|<span data-ttu-id="4c0a8-153">www</span><span class="sxs-lookup"><span data-stu-id="4c0a8-153">www</span></span>|<span data-ttu-id="4c0a8-154">Имя записи.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-154">Name of the record</span></span>|
   |<span data-ttu-id="4c0a8-155">**Тип**</span><span class="sxs-lookup"><span data-stu-id="4c0a8-155">**Type**</span></span>|<span data-ttu-id="4c0a8-156">Файл ,</span><span class="sxs-lookup"><span data-stu-id="4c0a8-156">A</span></span>| <span data-ttu-id="4c0a8-157">Тип создаваемой записи DNS. Допустимые значения: A, AAAA, CNAME, MX, NS, SRV, TXT и PTR.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-157">Type of DNS record to create, acceptable values are A, AAAA, CNAME, MX, NS, SRV, TXT, and PTR.</span></span>  <span data-ttu-id="4c0a8-158">Дополнительные сведения о типах записей см. в статье [Обзор зон и записей DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="4c0a8-158">For more information about record types, visit [Overview of DNS zones and records](dns-zones-records.md)</span></span>|
   |<span data-ttu-id="4c0a8-159">**Срок жизни**</span><span class="sxs-lookup"><span data-stu-id="4c0a8-159">**TTL**</span></span>|<span data-ttu-id="4c0a8-160">1</span><span class="sxs-lookup"><span data-stu-id="4c0a8-160">1</span></span>|<span data-ttu-id="4c0a8-161">Срок жизни DNS-запроса.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-161">Time-to-live of the DNS request.</span></span>|
   |<span data-ttu-id="4c0a8-162">**Единица срока жизни**</span><span class="sxs-lookup"><span data-stu-id="4c0a8-162">**TTL unit**</span></span>|<span data-ttu-id="4c0a8-163">Часы</span><span class="sxs-lookup"><span data-stu-id="4c0a8-163">Hours</span></span>|<span data-ttu-id="4c0a8-164">Измерение времени для значения срока жизни.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-164">Measurement of time for TTL value.</span></span>|
   |<span data-ttu-id="4c0a8-165">**IP-адрес**</span><span class="sxs-lookup"><span data-stu-id="4c0a8-165">**IP address**</span></span>|<span data-ttu-id="4c0a8-166">ipAddressValue</span><span class="sxs-lookup"><span data-stu-id="4c0a8-166">ipAddressValue</span></span>| <span data-ttu-id="4c0a8-167">Это значение является IP-адресом, который разрешает запись DNS.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-167">This value is the IP address that the DNS record resolves.</span></span>|

## <a name="view-records"></a><span data-ttu-id="4c0a8-168">Просмотр записей</span><span class="sxs-lookup"><span data-stu-id="4c0a8-168">View records</span></span>

<span data-ttu-id="4c0a8-169">В нижней части колонки "Зона DNS" отображаются записи для зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-169">In the lower part of the DNS zone blade, you can see the records for the DNS zone.</span></span> <span data-ttu-id="4c0a8-170">Должны отобразиться записи типа DNS и SOA по умолчанию, которые создаются в каждой зоне, а также все новые записи, созданные вами.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-170">You should see the default DNS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

![зона](./media/dns-getstarted-portal/viewzone500.png)


## <a name="update-name-servers"></a><span data-ttu-id="4c0a8-172">Обновление серверов доменных имен</span><span class="sxs-lookup"><span data-stu-id="4c0a8-172">Update name servers</span></span>

<span data-ttu-id="4c0a8-173">Когда вы убедитесь, что зона и записи DNS настроены правильно, необходимо настроить доменное имя для использования серверов доменных имен службы DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-173">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="4c0a8-174">Это позволит другим пользователям в Интернете находить ваши записи DNS.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-174">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="4c0a8-175">Серверы доменных имен для вашей зоны перечислены на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-175">The name servers for your zone are given in the Azure portal:</span></span>

![зона](./media/dns-getstarted-portal/viewzonens500.png)

<span data-ttu-id="4c0a8-177">Эти серверы доменных имен необходимо настроить с помощью регистратора доменных имен (у которого было приобретено доменное имя).</span><span class="sxs-lookup"><span data-stu-id="4c0a8-177">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="4c0a8-178">Регистратор предлагает вам вариант настройки серверов доменных имен для домена.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-178">Your registrar offers the option to set up the name servers for the domain.</span></span> <span data-ttu-id="4c0a8-179">Дополнительные сведения см. в статье [Делегирование домена в Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="4c0a8-179">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="4c0a8-180">Удаление всех ресурсов</span><span class="sxs-lookup"><span data-stu-id="4c0a8-180">Delete all resources</span></span>

<span data-ttu-id="4c0a8-181">Чтобы удалить все ресурсы, созданные в этой статье, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4c0a8-181">To delete all resources created in this article, complete the following steps:</span></span>

1. <span data-ttu-id="4c0a8-182">На портале Azure в области **Избранное** щелкните **Все ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-182">In the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="4c0a8-183">Щелкните группу ресурсов **MyResourceGroup** в колонке "Все ресурсы".</span><span class="sxs-lookup"><span data-stu-id="4c0a8-183">Click the **MyResourceGroup** resource group in the All resources blade.</span></span> <span data-ttu-id="4c0a8-184">Если выбранная подписка имеет несколько ресурсов, в поле **Фильтровать по имени...** введите **MyResourceGroup**,</span><span class="sxs-lookup"><span data-stu-id="4c0a8-184">If the subscription you selected already has several resources in it, you can enter **MyResourceGroup** in the **Filter by name…**</span></span> <span data-ttu-id="4c0a8-185">чтобы быстро получить доступ к необходимой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-185">box to easily access the resource group.</span></span>
1. <span data-ttu-id="4c0a8-186">В колонке **MyResourceGroup** нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-186">In the **MyResourceGroup** blade, click the **Delete** button.</span></span>
1. <span data-ttu-id="4c0a8-187">На портале появится запрос на ввод имени группы ресурсов для подтверждения удаления.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-187">The portal requires you to type the name of the resource group to confirm that you want to delete it.</span></span> <span data-ttu-id="4c0a8-188">Выберите **Удаление**, введите *MyResourceGroup* в качестве имени группы ресурсов, а затем щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-188">Click **Delete**, Type *MyResourceGroup* for the resource group name, then click **Delete**.</span></span> <span data-ttu-id="4c0a8-189">При удалении группы ресурсов удаляются все расположенные в ней ресурсы. Поэтому перед удалением группы ресурсов всегда проверяйте ее содержимое.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-189">Deleting a resource group deletes all resources within the resource group, so always be sure to confirm the contents of a resource group before deleting it.</span></span> <span data-ttu-id="4c0a8-190">Сначала портал удаляет все ресурсы, содержащиеся в группе ресурсов, а затем удаляет и саму группу.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-190">The portal deletes all resources contained within the resource group, then deletes the resource group itself.</span></span> <span data-ttu-id="4c0a8-191">Этот процесс занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="4c0a8-191">This process takes several minutes.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4c0a8-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4c0a8-192">Next steps</span></span>

<span data-ttu-id="4c0a8-193">Дополнительные сведения о службе DNS Azure см. в статье [Обзор Azure DNS](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4c0a8-193">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="4c0a8-194">Дополнительные сведения об управлении записями DNS в службе DNS Azure см. в статье [Управление записями и наборами записей DNS с помощью портала Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4c0a8-194">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

