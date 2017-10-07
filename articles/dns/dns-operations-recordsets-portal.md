---
title: "aaaManage DNS записи наборов и записей с помощью Azure DNS | Документы Microsoft"
description: "Azure DNS предоставляет hello возможность toomanage DNS-запись устанавливает и регистрирует при размещении вашего домена."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ed44a1-7bfe-454f-964e-922ad978264a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 2e62d017341589eaf8d1f8df2fe5db4b973381d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-hello-azure-portal"></a><span data-ttu-id="88743-103">Управление DNS-записи и наборы записей с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="88743-103">Manage DNS records and record sets by using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="88743-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="88743-104">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="88743-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="88743-105">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="88743-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="88743-106">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="88743-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="88743-107">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="88743-108">В этой статье показано, как наборы записей toomanage и записи для зоны DNS с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="88743-108">This article shows you how toomanage record sets and records for your DNS zone by using hello Azure portal.</span></span>

<span data-ttu-id="88743-109">Это важные toounderstand hello различие наборов записей DNS и отдельных записей DNS.</span><span class="sxs-lookup"><span data-stu-id="88743-109">It's important toounderstand hello difference between DNS record sets and individual DNS records.</span></span> <span data-ttu-id="88743-110">Набор записей — это совокупность записей в зоне, содержащих hello совпадают имя и являются hello того же типа.</span><span class="sxs-lookup"><span data-stu-id="88743-110">A record set is a collection of records in a zone that have hello same name and are hello same type.</span></span> <span data-ttu-id="88743-111">Дополнительные сведения см. в разделе [наборы записей DNS для создания и записи с помощью hello портал Azure](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="88743-111">For more information, see [Create DNS record sets and records by using hello Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="create-a-new-record-set-and-record"></a><span data-ttu-id="88743-112">Создание нового набора записей и записи</span><span class="sxs-lookup"><span data-stu-id="88743-112">Create a new record set and record</span></span>

<span data-ttu-id="88743-113">toocreate в hello портал Azure, набор записей. в разделе [Здравствуйте, создать DNS-записей с помощью портала Azure](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="88743-113">toocreate a record set in hello Azure portal, see [Create DNS records by using hello Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="view-a-record-set"></a><span data-ttu-id="88743-114">Просмотр набора записей</span><span class="sxs-lookup"><span data-stu-id="88743-114">View a record set</span></span>

1. <span data-ttu-id="88743-115">В hello портал Azure, перейдите toohello **зоны DNS** колонку.</span><span class="sxs-lookup"><span data-stu-id="88743-115">In hello Azure portal, go toohello **DNS zone** blade.</span></span>
2. <span data-ttu-id="88743-116">Поиск набора записей hello и выберите его.</span><span class="sxs-lookup"><span data-stu-id="88743-116">Search for hello record set and select it.</span></span> <span data-ttu-id="88743-117">При этом откроется hello свойств набора записей.</span><span class="sxs-lookup"><span data-stu-id="88743-117">This opens hello record set properties.</span></span>

    ![Поиск набора записей](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-tooa-record-set"></a><span data-ttu-id="88743-119">Добавление новых записей tooa набора записей</span><span class="sxs-lookup"><span data-stu-id="88743-119">Add a new record tooa record set</span></span>

<span data-ttu-id="88743-120">Можно добавить набор записей tooany записи too20.</span><span class="sxs-lookup"><span data-stu-id="88743-120">You can add up too20 records tooany record set.</span></span> <span data-ttu-id="88743-121">Набор записей не может содержать две одинаковые записи.</span><span class="sxs-lookup"><span data-stu-id="88743-121">A record set cannot contain two identical records.</span></span> <span data-ttu-id="88743-122">Пустой наборов записей (с нуля записи) могут быть созданы, но не отображаются в hello Azure DNS-серверами.</span><span class="sxs-lookup"><span data-stu-id="88743-122">Empty record sets (with zero records) can be created, but do not appear on hello Azure DNS name servers.</span></span> <span data-ttu-id="88743-123">Наборы записей типа CNAME могут содержать не более одной записи.</span><span class="sxs-lookup"><span data-stu-id="88743-123">Record sets of type CNAME can contain one record at most.</span></span>

1. <span data-ttu-id="88743-124">На hello **запись свойства** колонку для зоны DNS, щелкните запись hello задайте выполняться tooadd запись.</span><span class="sxs-lookup"><span data-stu-id="88743-124">On hello **Record set properties** blade for your DNS zone, click hello record set that you want tooadd a record to.</span></span>

    ![Выбор набора записей](./media/dns-operations-recordsets-portal/selectset500.png)

2. <span data-ttu-id="88743-126">Укажите набор свойств hello запись, заполнив поля hello.</span><span class="sxs-lookup"><span data-stu-id="88743-126">Specify hello record set properties by filling in hello fields.</span></span>

    ![Добавление записи](./media/dns-operations-recordsets-portal/addrecord500.png)

3. <span data-ttu-id="88743-128">Нажмите кнопку **Сохранить** на hello верхней части колонки toosave hello параметры.</span><span class="sxs-lookup"><span data-stu-id="88743-128">Click **Save** at hello top of hello blade toosave your settings.</span></span> <span data-ttu-id="88743-129">Затем закройте колонку hello.</span><span class="sxs-lookup"><span data-stu-id="88743-129">Then close hello blade.</span></span>
4. <span data-ttu-id="88743-130">В углу hello вы увидите, что Сохранение записи hello.</span><span class="sxs-lookup"><span data-stu-id="88743-130">In hello corner, you will see that hello record is saving.</span></span>

    ![Сохранение набора записей](./media/dns-operations-recordsets-portal/saving150.png)

<span data-ttu-id="88743-132">После сохранения записи hello hello значения на hello **зоны DNS** колонки будут отражать hello новой записи.</span><span class="sxs-lookup"><span data-stu-id="88743-132">After hello record has been saved, hello values on hello **DNS zone** blade will reflect hello new record.</span></span>

## <a name="update-a-record"></a><span data-ttu-id="88743-133">Изменение записи</span><span class="sxs-lookup"><span data-stu-id="88743-133">Update a record</span></span>

<span data-ttu-id="88743-134">При обновлении записи в существующий набор записей hello поля, которые можно обновить, зависят от типа hello записи вы работаете.</span><span class="sxs-lookup"><span data-stu-id="88743-134">When you update a record in an existing record set, hello fields you can update depend on hello type of record you're working with.</span></span>

1. <span data-ttu-id="88743-135">На hello **запись свойства** колонке набор записей, поиска записей hello.</span><span class="sxs-lookup"><span data-stu-id="88743-135">On hello **Record set properties** blade for your record set, search for hello record.</span></span>
2. <span data-ttu-id="88743-136">Измените запись hello.</span><span class="sxs-lookup"><span data-stu-id="88743-136">Modify hello record.</span></span> <span data-ttu-id="88743-137">При изменении записи, можно изменить доступные параметры записи hello hello.</span><span class="sxs-lookup"><span data-stu-id="88743-137">When you modify a record, you can change hello available settings for hello record.</span></span> <span data-ttu-id="88743-138">В следующем примере hello, hello **IP-адрес** выбрано поле и hello IP-адрес находится в процессе hello объекта изменяется.</span><span class="sxs-lookup"><span data-stu-id="88743-138">In hello following example, hello **IP address** field is selected, and hello IP address is in hello process of being modified.</span></span>

    ![Изменение набора записей](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. <span data-ttu-id="88743-140">Нажмите кнопку **Сохранить** на hello верхней части колонки toosave hello параметры.</span><span class="sxs-lookup"><span data-stu-id="88743-140">Click **Save** at hello top of hello blade toosave your settings.</span></span> <span data-ttu-id="88743-141">В верхнем правом углу hello вы увидите уведомление hello, сохранения записи hello.</span><span class="sxs-lookup"><span data-stu-id="88743-141">In hello upper right corner, you'll see hello notification that hello record has been saved.</span></span>

    ![Сохраненный набор записей](./media/dns-operations-recordsets-portal/saved150.png)

<span data-ttu-id="88743-143">После сохранения записи hello hello значения для записи hello установлены hello **зоны DNS** колонки будут отражать hello обновления записи.</span><span class="sxs-lookup"><span data-stu-id="88743-143">After hello record has been saved, hello values for hello record set on hello **DNS zone** blade will reflect hello updated record.</span></span>

## <a name="remove-a-record-from-a-record-set"></a><span data-ttu-id="88743-144">Удаление записи из набора записей</span><span class="sxs-lookup"><span data-stu-id="88743-144">Remove a record from a record set</span></span>

<span data-ttu-id="88743-145">Можно использовать hello Azure портала tooremove записи из набора записей.</span><span class="sxs-lookup"><span data-stu-id="88743-145">You can use hello Azure portal tooremove records from a record set.</span></span> <span data-ttu-id="88743-146">Обратите внимание, что при удалении hello последней записи из набора записей набора записей hello не удаляется.</span><span class="sxs-lookup"><span data-stu-id="88743-146">Note that removing hello last record from a record set does not delete hello record set.</span></span>

1. <span data-ttu-id="88743-147">На hello **запись свойства** колонке набор записей, поиска записей hello.</span><span class="sxs-lookup"><span data-stu-id="88743-147">On hello **Record set properties** blade for your record set, search for hello record.</span></span>
2. <span data-ttu-id="88743-148">Щелкните запись hello, что требуется tooremove.</span><span class="sxs-lookup"><span data-stu-id="88743-148">Click hello record that you want tooremove.</span></span> <span data-ttu-id="88743-149">Затем щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="88743-149">Then select **Remove**.</span></span>

    ![Удаление набора записей](./media/dns-operations-recordsets-portal/removerecord500.png)

3. <span data-ttu-id="88743-151">Нажмите кнопку **Сохранить** на hello верхней части колонки toosave hello параметры.</span><span class="sxs-lookup"><span data-stu-id="88743-151">Click **Save** at hello top of hello blade toosave your settings.</span></span>
4. <span data-ttu-id="88743-152">После удаления записи hello hello значения записи hello на hello **зоны DNS** колонки будут отражать удаления hello.</span><span class="sxs-lookup"><span data-stu-id="88743-152">After hello record has been removed, hello values for hello record on hello **DNS zone** blade will reflect hello removal.</span></span>

## <span data-ttu-id="88743-153"><a name="delete"></a>Удаление набора записей</span><span class="sxs-lookup"><span data-stu-id="88743-153"><a name="delete"></a>Delete a record set</span></span>

1. <span data-ttu-id="88743-154">На hello **запись свойства** колонке набор записей, нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="88743-154">On hello **Record set properties** blade for your record set, click **Delete**.</span></span>

    ![Удаление набора записей](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. <span data-ttu-id="88743-156">Появится сообщение, если требуется набор записей toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="88743-156">A message appears asking if you want toodelete hello record set.</span></span>
3. <span data-ttu-id="88743-157">Убедитесь, что запись hello совпадения имен hello требуется toodelete и нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="88743-157">Verify that hello name matches hello record set that you want toodelete, and then click **Yes**.</span></span>
4. <span data-ttu-id="88743-158">На hello **зоны DNS** колонки, убедитесь, что набор записей hello больше не отображается.</span><span class="sxs-lookup"><span data-stu-id="88743-158">On hello **DNS zone** blade, verify that hello record set is no longer visible.</span></span>

## <a name="work-with-ns-and-soa-records"></a><span data-ttu-id="88743-159">Работа с записями типа NS и SOA</span><span class="sxs-lookup"><span data-stu-id="88743-159">Work with NS and SOA records</span></span>

<span data-ttu-id="88743-160">Управление автоматически создаваемыми записями NS и SOA осуществляется иначе, чем другими типами записей.</span><span class="sxs-lookup"><span data-stu-id="88743-160">NS and SOA records that are automatically created are managed differently from other record types.</span></span>

### <a name="modify-soa-records"></a><span data-ttu-id="88743-161">Изменение записей типа SOA</span><span class="sxs-lookup"><span data-stu-id="88743-161">Modify SOA records</span></span>

<span data-ttu-id="88743-162">Не удается добавить или удаления записей из hello автоматически создается на вершине зоны hello начальной записи (имя = «@»).</span><span class="sxs-lookup"><span data-stu-id="88743-162">You cannot add or remove records from hello automatically created SOA record set at hello zone apex (name = "@").</span></span> <span data-ttu-id="88743-163">Однако вы можете изменить любые параметры hello в рамках hello начальной записи зоны (кроме «узел») и записи hello задать значение срока ЖИЗНИ.</span><span class="sxs-lookup"><span data-stu-id="88743-163">However, you can modify any of hello parameters within hello SOA record (except "Host") and hello record set TTL.</span></span>

### <a name="modify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="88743-164">Изменение записей NS в вершине зоны hello</span><span class="sxs-lookup"><span data-stu-id="88743-164">Modify NS records at hello zone apex</span></span>

<span data-ttu-id="88743-165">запись NS Hello на вершине зоны hello создается автоматически с каждой зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="88743-165">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="88743-166">Она содержит имена hello hello Azure имя серверов назначенного toohello зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="88743-166">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="88743-167">Можно добавить дополнительное имя серверов toothis NS: набор записей, toosupport совместное размещение домены с более чем одного поставщика DNS.</span><span class="sxs-lookup"><span data-stu-id="88743-167">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="88743-168">Можно также изменить hello TTL и метаданные для этого набора записей.</span><span class="sxs-lookup"><span data-stu-id="88743-168">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="88743-169">Тем не менее нельзя удалять или изменять hello предварительно заполненных Azure DNS-серверами.</span><span class="sxs-lookup"><span data-stu-id="88743-169">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="88743-170">Обратите внимание, что это применимо только toohello NS набора записей на вершине зоны hello.</span><span class="sxs-lookup"><span data-stu-id="88743-170">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="88743-171">Другие NS наборов записей в зоне (как в дочерних зонах используется toodelegate) можно изменять без ограничений.</span><span class="sxs-lookup"><span data-stu-id="88743-171">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

### <a name="delete-soa-or-ns-record-sets"></a><span data-ttu-id="88743-172">Удаление наборов записей типа SOA или NS</span><span class="sxs-lookup"><span data-stu-id="88743-172">Delete SOA or NS record sets</span></span>

<span data-ttu-id="88743-173">Не удается удалить hello SOA и NS наборов записей в вершине зоны hello (имя = «@»), создаются автоматически при создании зоны hello.</span><span class="sxs-lookup"><span data-stu-id="88743-173">You cannot delete hello SOA and NS record sets at hello zone apex (name = "@") that are created automatically when hello zone is created.</span></span> <span data-ttu-id="88743-174">Они удаляются автоматически при удалении hello зоны.</span><span class="sxs-lookup"><span data-stu-id="88743-174">They are deleted automatically when you delete hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88743-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="88743-175">Next steps</span></span>

* <span data-ttu-id="88743-176">Дополнительные сведения о Azure DNS см. в разделе hello [Обзор Azure DNS](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="88743-176">For more information about Azure DNS, see hello [Azure DNS overview](dns-overview.md).</span></span>
* <span data-ttu-id="88743-177">Дополнительные сведения об автоматизации DNS см. в разделе [зон DNS, создание и использование наборов записей hello .NET SDK](dns-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="88743-177">For more information about automating DNS, see [Creating DNS zones and record sets using hello .NET SDK](dns-sdk.md).</span></span>
* <span data-ttu-id="88743-178">Дополнительные сведения о записях обратной зоны DNS см. в статье [Основные сведения об обратной зоне DNS и ее поддержке в Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="88743-178">For more information about reverse DNS records, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>
