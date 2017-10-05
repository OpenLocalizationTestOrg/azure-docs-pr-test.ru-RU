---
title: "Создание прослушивателя для групп доступности SQL Server в службе виртуальных машин Azure | Документация Майкрософт"
description: "Пошаговые инструкции по созданию прослушивателя для группы доступности AlwaysOn для SQL Server в службе виртуальных машин Azure."
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: d1f291e9-9af2-41ba-9d29-9541e3adcfcf
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/01/2017
ms.author: mikeray
ms.openlocfilehash: 09fed7e785708d4afe64905de973becc188181d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-load-balancer-for-an-always-on-availability-group-in-azure"></a><span data-ttu-id="dd11e-103">Настройка подсистемы балансировки нагрузки для группы доступности AlwaysOn в Azure</span><span class="sxs-lookup"><span data-stu-id="dd11e-103">Configure a load balancer for an Always On availability group in Azure</span></span>
<span data-ttu-id="dd11e-104">В этой статье описывается, как создать подсистему балансировки нагрузки для группы доступности AlwaysOn для SQL Server на виртуальных машинах Azure, развернутых с помощью модели Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dd11e-104">This article explains how to create a load balancer for a SQL Server Always On availability group in Azure virtual machines that are running with Azure Resource Manager.</span></span> <span data-ttu-id="dd11e-105">Группе доступности нужен балансировщик нагрузки, если экземпляры SQL Server находятся на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="dd11e-105">An availability group requires a load balancer when the SQL Server instances are on Azure virtual machines.</span></span> <span data-ttu-id="dd11e-106">Балансировщик нагрузки хранит IP-адрес для прослушивателя группы доступности.</span><span class="sxs-lookup"><span data-stu-id="dd11e-106">The load balancer stores the IP address for the availability group listener.</span></span> <span data-ttu-id="dd11e-107">Если группа доступности распространяется на несколько регионов, для каждого из них нужен отдельный балансировщик.</span><span class="sxs-lookup"><span data-stu-id="dd11e-107">If an availability group spans multiple regions, each region needs a load balancer.</span></span>

<span data-ttu-id="dd11e-108">Для этого необходимо развернуть группу доступности SQL Server на виртуальных машинах Azure с использованием модели Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dd11e-108">To complete this task, you need to have a SQL Server availability group deployed on Azure virtual machines that are running with Resource Manager.</span></span> <span data-ttu-id="dd11e-109">Обе виртуальные машины SQL Server должны принадлежать к одной и той же группе доступности.</span><span class="sxs-lookup"><span data-stu-id="dd11e-109">Both SQL Server virtual machines must belong to the same availability set.</span></span> <span data-ttu-id="dd11e-110">Вы можете использовать [шаблон Майкрософт](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), чтобы автоматически создать группу доступности в Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dd11e-110">You can use the [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) to automatically create the availability group in Resource Manager.</span></span> <span data-ttu-id="dd11e-111">Этот шаблон также автоматически создает внутреннюю подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="dd11e-111">This template automatically creates an internal load balancer for you.</span></span> 

<span data-ttu-id="dd11e-112">При необходимости [группу доступности можно настроить вручную](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="dd11e-112">If you prefer, you can [manually configure an availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="dd11e-113">Здесь предполагается, что группы доступности уже настроены.</span><span class="sxs-lookup"><span data-stu-id="dd11e-113">This article requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="dd11e-114">Связанные разделы включают:</span><span class="sxs-lookup"><span data-stu-id="dd11e-114">Related topics include:</span></span>

* [<span data-ttu-id="dd11e-115">Введение в группы доступности AlwaysOn SQL Server на виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="dd11e-115">Configure Always On availability groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="dd11e-116">Настройка подключения между виртуальными сетями с помощью Azure Resource Manager и PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd11e-116">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

<span data-ttu-id="dd11e-117">Последовательно выполнив все действия этой статьи, вы создадите и настроите подсистему балансировки нагрузки на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="dd11e-117">By walking through this article, you create and configure a load balancer in the Azure portal.</span></span> <span data-ttu-id="dd11e-118">По завершении процесса вы настроите в кластере IP-адрес подсистемы балансировки нагрузки для прослушивателя группы доступности.</span><span class="sxs-lookup"><span data-stu-id="dd11e-118">After the process is complete, you configure the cluster to use the IP address from the load balancer for the availability group listener.</span></span>

## <a name="create-and-configure-the-load-balancer-in-the-azure-portal"></a><span data-ttu-id="dd11e-119">Создание и настройка балансировщика нагрузки на портале Azure</span><span class="sxs-lookup"><span data-stu-id="dd11e-119">Create and configure the load balancer in the Azure portal</span></span>
<span data-ttu-id="dd11e-120">В этом разделе мы сделаем следующее:</span><span class="sxs-lookup"><span data-stu-id="dd11e-120">In this portion of the task, do the following:</span></span>

1. <span data-ttu-id="dd11e-121">Создадим подсистему балансировки нагрузки и настроим IP-адрес на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="dd11e-121">In the Azure portal, create the load balancer and configure the IP address.</span></span>
2. <span data-ttu-id="dd11e-122">Настроим серверный пул.</span><span class="sxs-lookup"><span data-stu-id="dd11e-122">Configure the back-end pool.</span></span>
3. <span data-ttu-id="dd11e-123">Создадим пробу.</span><span class="sxs-lookup"><span data-stu-id="dd11e-123">Create the probe.</span></span> 
4. <span data-ttu-id="dd11e-124">Настройте правила балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="dd11e-124">Set the load balancing rules.</span></span>

> [!NOTE]
> <span data-ttu-id="dd11e-125">Если экземпляры SQL Server расположены в нескольких группах ресурсов и регионах, необходимо выполнить все эти действия дважды — по одному разу в каждой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="dd11e-125">If the SQL Server instances are in multiple resource groups and regions, perform each step twice, once in each resource group.</span></span>
> 
> 

### <a name="step-1-create-the-load-balancer-and-configure-the-ip-address"></a><span data-ttu-id="dd11e-126">Шаг 1. Создание подсистемы балансировки нагрузки и настройка IP-адреса</span><span class="sxs-lookup"><span data-stu-id="dd11e-126">Step 1: Create the load balancer and configure the IP address</span></span>
<span data-ttu-id="dd11e-127">Сначала создайте подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="dd11e-127">First, create the load balancer.</span></span> 

1. <span data-ttu-id="dd11e-128">На портале Azure откройте группу ресурсов, в которой содержатся виртуальные машины SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dd11e-128">In the Azure portal, open the resource group that contains the SQL Server virtual machines.</span></span> 

2. <span data-ttu-id="dd11e-129">В колонке группы ресурсов щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-129">In the resource group, click **Add**.</span></span>

3. <span data-ttu-id="dd11e-130">Выполните поиск по запросу **подсистема балансировки нагрузки** и в результатах поиска выберите **Подсистема балансировки нагрузки**, опубликованную корпорацией **Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-130">Search for **load balancer** and then, in the search results, select **Load Balancer**, which is published by **Microsoft**.</span></span>

4. <span data-ttu-id="dd11e-131">В колонке **Балансировщик нагрузки** щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-131">On the **Load Balancer** blade, click **Create**.</span></span>

5. <span data-ttu-id="dd11e-132">В диалоговом окне **Создание подсистемы балансировки нагрузки** настройте подсистему балансировки нагрузки, задав следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="dd11e-132">In the **Create load balancer** dialog box, configure the load balancer as follows:</span></span>

   | <span data-ttu-id="dd11e-133">Настройка</span><span class="sxs-lookup"><span data-stu-id="dd11e-133">Setting</span></span> | <span data-ttu-id="dd11e-134">Значение</span><span class="sxs-lookup"><span data-stu-id="dd11e-134">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="dd11e-135">**Имя**</span><span class="sxs-lookup"><span data-stu-id="dd11e-135">**Name**</span></span> |<span data-ttu-id="dd11e-136">Текст, представляющий имя балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="dd11e-136">A text name representing the load balancer.</span></span> <span data-ttu-id="dd11e-137">Например, **sqlLB**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-137">For example, **sqlLB**.</span></span> |
   | <span data-ttu-id="dd11e-138">**Тип**</span><span class="sxs-lookup"><span data-stu-id="dd11e-138">**Type**</span></span> |<span data-ttu-id="dd11e-139">**Внутренний.** Большинство реализаций используют внутреннюю подсистему балансировки нагрузки, которая позволяет приложениям, работающим в одной и той же виртуальной сети, подключаться к группе доступности.</span><span class="sxs-lookup"><span data-stu-id="dd11e-139">**Internal**: Most implementations use an internal load balancer, which allows applications within the same virtual network to connect to the availability group.</span></span>  </br> <span data-ttu-id="dd11e-140">**Внешний.** Позволяет приложениям подключаться к группе доступности через общедоступное интернет-подключение.</span><span class="sxs-lookup"><span data-stu-id="dd11e-140">**External**: Allows applications to connect to the availability group through a public Internet connection.</span></span> |
   | <span data-ttu-id="dd11e-141">**Виртуальная сеть**</span><span class="sxs-lookup"><span data-stu-id="dd11e-141">**Virtual network**</span></span> |<span data-ttu-id="dd11e-142">Выберите виртуальную сеть, в которой расположены экземпляры SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dd11e-142">Select the virtual network that the SQL Server intances are in.</span></span> |
   | <span data-ttu-id="dd11e-143">**Подсеть**</span><span class="sxs-lookup"><span data-stu-id="dd11e-143">**Subnet**</span></span> |<span data-ttu-id="dd11e-144">Выберите подсеть, в которой расположены экземпляры SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dd11e-144">Select the subnet that the SQL Server instances are in.</span></span> |
   | <span data-ttu-id="dd11e-145">**Назначение IP-адресов**</span><span class="sxs-lookup"><span data-stu-id="dd11e-145">**IP address assignment**</span></span> |<span data-ttu-id="dd11e-146">**Статическое**</span><span class="sxs-lookup"><span data-stu-id="dd11e-146">**Static**</span></span> |
   | <span data-ttu-id="dd11e-147">**Частный IP-адрес**</span><span class="sxs-lookup"><span data-stu-id="dd11e-147">**Private IP address**</span></span> |<span data-ttu-id="dd11e-148">Укажите свободный IP-адрес из нужной подсети.</span><span class="sxs-lookup"><span data-stu-id="dd11e-148">Specify an available IP address from the subnet.</span></span> <span data-ttu-id="dd11e-149">Используйте этот IP-адрес при создании прослушивателя в кластере.</span><span class="sxs-lookup"><span data-stu-id="dd11e-149">Use this IP address when you create a listener on the cluster.</span></span> <span data-ttu-id="dd11e-150">Далее вам понадобится использовать этот адрес для переменной `$ILBIP` в скрипте PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dd11e-150">In a PowerShell script, later in this article, use this address for the `$ILBIP` variable.</span></span> |
   | <span data-ttu-id="dd11e-151">**Подписка**</span><span class="sxs-lookup"><span data-stu-id="dd11e-151">**Subscription**</span></span> |<span data-ttu-id="dd11e-152">Это поле может появиться, если у вас несколько подписок.</span><span class="sxs-lookup"><span data-stu-id="dd11e-152">If you have multiple subscriptions, this field might appear.</span></span> <span data-ttu-id="dd11e-153">Выберите подписку, которую требуется связать с этим ресурсом.</span><span class="sxs-lookup"><span data-stu-id="dd11e-153">Select the subscription that you want to associate with this resource.</span></span> <span data-ttu-id="dd11e-154">Обычно это подписка, с которой связаны все ресурсы группы доступности.</span><span class="sxs-lookup"><span data-stu-id="dd11e-154">It is normally the same subscription as all the resources for the availability group.</span></span> |
   | <span data-ttu-id="dd11e-155">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="dd11e-155">**Resource group**</span></span> |<span data-ttu-id="dd11e-156">Выберите группу ресурсов, в которой расположены экземпляры SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dd11e-156">Select the resource group that the SQL Server instances are in.</span></span> |
   | <span data-ttu-id="dd11e-157">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="dd11e-157">**Location**</span></span> |<span data-ttu-id="dd11e-158">Выберите расположение Azure, в котором расположены экземпляры SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dd11e-158">Select the Azure location that the SQL Server instances are in.</span></span> |

6. <span data-ttu-id="dd11e-159">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-159">Click **Create**.</span></span> 

<span data-ttu-id="dd11e-160">Azure создаст подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="dd11e-160">Azure creates the load balancer.</span></span> <span data-ttu-id="dd11e-161">Балансировщик нагрузки относится к конкретной сети, подсети, группе ресурсов и расположению.</span><span class="sxs-lookup"><span data-stu-id="dd11e-161">The load balancer belongs to a specific network, subnet, resource group, and location.</span></span> <span data-ttu-id="dd11e-162">После создания подсистемы балансировки нагрузки проверьте ее параметры в Azure.</span><span class="sxs-lookup"><span data-stu-id="dd11e-162">After Azure completes the task, verify the load balancer settings in Azure.</span></span> 

### <a name="step-2-configure-the-back-end-pool"></a><span data-ttu-id="dd11e-163">Шаг 2. Настройка серверного пула</span><span class="sxs-lookup"><span data-stu-id="dd11e-163">Step 2: Configure the back-end pool</span></span>
<span data-ttu-id="dd11e-164">В Azure серверный пул адресов называется просто *серверным пулом*.</span><span class="sxs-lookup"><span data-stu-id="dd11e-164">Azure calls the back-end address pool *backend pool*.</span></span> <span data-ttu-id="dd11e-165">В нашем случае это адреса двух экземпляров SQL Server в группе доступности.</span><span class="sxs-lookup"><span data-stu-id="dd11e-165">In this case, the back-end pool is the addresses of the two SQL Server instances in your availability group.</span></span> 

1. <span data-ttu-id="dd11e-166">В группе ресурсов щелкните созданную подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="dd11e-166">In your resource group, click the load balancer that you created.</span></span> 

2. <span data-ttu-id="dd11e-167">В колонке **Параметры** щелкните **Серверные пулы**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-167">On **Settings**, click **Backend pools**.</span></span>

3. <span data-ttu-id="dd11e-168">На вкладке **Серверные пулы** щелкните **Добавить**, чтобы создать серверный пул адресов.</span><span class="sxs-lookup"><span data-stu-id="dd11e-168">On **Backend pools**, click **Add** to create a back-end address pool.</span></span> 

4. <span data-ttu-id="dd11e-169">В колонке **Добавление серверного пула** в поле **Имя** введите имя серверного пула.</span><span class="sxs-lookup"><span data-stu-id="dd11e-169">On **Add backend pool**, under **Name**, type a name for the back-end pool.</span></span>

5. <span data-ttu-id="dd11e-170">В разделе **Виртуальные машины** щелкните **Добавить виртуальную машину**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-170">Under **Virtual machines**, click **Add a virtual machine**.</span></span> 

6. <span data-ttu-id="dd11e-171">В разделе **Выбор виртуальных машин** щелкните **Выберите группу доступности** и укажите группу доступности, к которой принадлежат виртуальные машины SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dd11e-171">Under **Choose virtual machines**, click **Choose an availability set**, and then specify the availability set that the SQL Server virtual machines belong to.</span></span>

7. <span data-ttu-id="dd11e-172">Выбрав группу доступности, щелкните **Выберите виртуальные машины**. Выберите две виртуальные машины, на которых размещены экземпляры SQL Server в группе доступности, а затем щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-172">After you have chosen the availability set, click **Choose the virtual machines**, select the two virtual machines that host the SQL Server instances in the availability group, and then click **Select**.</span></span> 

8. <span data-ttu-id="dd11e-173">Нажмите кнопку **ОК**, чтобы закрыть колонки **Выбор виртуальных машин** и **Добавить внутренний пул**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-173">Click **OK** to close the blades for **Choose virtual machines**, and **Add backend pool**.</span></span> 

<span data-ttu-id="dd11e-174">После этого Azure обновит параметры для серверного пула адресов.</span><span class="sxs-lookup"><span data-stu-id="dd11e-174">Azure updates the settings for the back-end address pool.</span></span> <span data-ttu-id="dd11e-175">Теперь в вашей группе доступности есть пул из двух экземпляров SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dd11e-175">Now your availability set has a pool of two SQL Server instances.</span></span>

### <a name="step-3-create-a-probe"></a><span data-ttu-id="dd11e-176">Шаг 3. Создание пробы</span><span class="sxs-lookup"><span data-stu-id="dd11e-176">Step 3: Create a probe</span></span>
<span data-ttu-id="dd11e-177">Проба определяет, как Azure будет проверять, какому из экземпляров SQL Server в данный момент принадлежит прослушиватель группы доступности.</span><span class="sxs-lookup"><span data-stu-id="dd11e-177">The probe defines how Azure verifies which of the SQL Server instances currently owns the availability group listener.</span></span> <span data-ttu-id="dd11e-178">Azure проверяет службу по IP-адресу и порту, которые вы указываете при создании пробы.</span><span class="sxs-lookup"><span data-stu-id="dd11e-178">Azure probes the service based on the IP address on a port that you define when you create the probe.</span></span>

1. <span data-ttu-id="dd11e-179">В колонке **Параметры** для подсистемы балансировки нагрузки щелкните **Health probes** (Пробы работоспособности).</span><span class="sxs-lookup"><span data-stu-id="dd11e-179">On the load balancer **Settings** blade, click **Health probes**.</span></span> 

2. <span data-ttu-id="dd11e-180">В колонке **Health probes** (Пробы работоспособности) щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-180">On the **Health probes** blade, click **Add**.</span></span>

3. <span data-ttu-id="dd11e-181">Настройте пробу в колонке **Добавление пробы** .</span><span class="sxs-lookup"><span data-stu-id="dd11e-181">Configure the probe on the **Add probe** blade.</span></span> <span data-ttu-id="dd11e-182">Для настройки пробы используйте следующие значения:</span><span class="sxs-lookup"><span data-stu-id="dd11e-182">Use the following values to configure the probe:</span></span>

   | <span data-ttu-id="dd11e-183">Настройка</span><span class="sxs-lookup"><span data-stu-id="dd11e-183">Setting</span></span> | <span data-ttu-id="dd11e-184">Значение</span><span class="sxs-lookup"><span data-stu-id="dd11e-184">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="dd11e-185">**Имя**</span><span class="sxs-lookup"><span data-stu-id="dd11e-185">**Name**</span></span> |<span data-ttu-id="dd11e-186">Текст, представляющий имя пробы.</span><span class="sxs-lookup"><span data-stu-id="dd11e-186">A text name representing the probe.</span></span> <span data-ttu-id="dd11e-187">Например, **SQLAlwaysOnEndPointProbe**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-187">For example, **SQLAlwaysOnEndPointProbe**.</span></span> |
   | <span data-ttu-id="dd11e-188">**Протокол**</span><span class="sxs-lookup"><span data-stu-id="dd11e-188">**Protocol**</span></span> |<span data-ttu-id="dd11e-189">**TCP**</span><span class="sxs-lookup"><span data-stu-id="dd11e-189">**TCP**</span></span> |
   | <span data-ttu-id="dd11e-190">**Порт**</span><span class="sxs-lookup"><span data-stu-id="dd11e-190">**Port**</span></span> |<span data-ttu-id="dd11e-191">Вы можете использовать любой доступный порт.</span><span class="sxs-lookup"><span data-stu-id="dd11e-191">You can use any available port.</span></span> <span data-ttu-id="dd11e-192">Например, *59999*.</span><span class="sxs-lookup"><span data-stu-id="dd11e-192">For example, *59999*.</span></span> |
   | <span data-ttu-id="dd11e-193">**Интервал**</span><span class="sxs-lookup"><span data-stu-id="dd11e-193">**Interval**</span></span> |<span data-ttu-id="dd11e-194">*5*</span><span class="sxs-lookup"><span data-stu-id="dd11e-194">*5*</span></span> |
   | <span data-ttu-id="dd11e-195">**Пороговое значение сбоя**</span><span class="sxs-lookup"><span data-stu-id="dd11e-195">**Unhealthy threshold**</span></span> |<span data-ttu-id="dd11e-196">*2*</span><span class="sxs-lookup"><span data-stu-id="dd11e-196">*2*</span></span> |

4.  <span data-ttu-id="dd11e-197">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-197">Click **OK**.</span></span> 

> [!NOTE]
> <span data-ttu-id="dd11e-198">Указанный порт должен быть открыт в брандмауэре обоих экземпляров SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dd11e-198">Make sure that the port you specify is open on the firewall of both SQL Server instances.</span></span> <span data-ttu-id="dd11e-199">Для обоих экземпляров требуется правило для входящего трафика используемого TCP-порта.</span><span class="sxs-lookup"><span data-stu-id="dd11e-199">Both instances require an inbound rule for the TCP port that you use.</span></span> <span data-ttu-id="dd11e-200">Дополнительные сведения см. в статье [Добавление и изменение правила брандмауэра](http://technet.microsoft.com/library/cc753558.aspx).</span><span class="sxs-lookup"><span data-stu-id="dd11e-200">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span> 
> 
> 

<span data-ttu-id="dd11e-201">Azure создаст пробу и с ее помощью будет проверять, в каком экземпляре SQL Server есть прослушиватель для группы доступности.</span><span class="sxs-lookup"><span data-stu-id="dd11e-201">Azure creates the probe and then uses it to test which SQL Server instance has the listener for the availability group.</span></span>

### <a name="step-4-set-the-load-balancing-rules"></a><span data-ttu-id="dd11e-202">Шаг 4. Настройка правил балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="dd11e-202">Step 4: Set the load balancing rules</span></span>
<span data-ttu-id="dd11e-203">Правила балансировки нагрузки определяют способ направления трафика подсистемой балансировки нагрузки в экземплярах SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dd11e-203">The load balancing rules configure how the load balancer routes traffic to the SQL Server instances.</span></span> <span data-ttu-id="dd11e-204">Для этой подсистемы балансировки нагрузки включите прямой ответ от сервера, так как одновременно только один из двух экземпляров SQL Server может содержать ресурс прослушивателя группы доступности.</span><span class="sxs-lookup"><span data-stu-id="dd11e-204">For this load balancer, you enable direct server return because only one of the two SQL Server instances owns the availability group listener resource at a time.</span></span>

1. <span data-ttu-id="dd11e-205">В колонке **Параметры** для балансировщика нагрузки щелкните **Правила балансировки нагрузки**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-205">On the load balancer **Settings** blade, click **Load balancing rules**.</span></span> 

2. <span data-ttu-id="dd11e-206">В колонке **Правила балансировки нагрузки** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-206">On the **Load balancing rules** blade, click **Add**.</span></span>

3. <span data-ttu-id="dd11e-207">В колонке **Add load balancing rules** (Добавление правил балансировки нагрузки) настройте правило балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="dd11e-207">On the **Add load balancing rules** blade, configure the load balancing rule.</span></span> <span data-ttu-id="dd11e-208">Используйте следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="dd11e-208">Use the following settings:</span></span> 

   | <span data-ttu-id="dd11e-209">Настройка</span><span class="sxs-lookup"><span data-stu-id="dd11e-209">Setting</span></span> | <span data-ttu-id="dd11e-210">Значение</span><span class="sxs-lookup"><span data-stu-id="dd11e-210">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="dd11e-211">**Имя**</span><span class="sxs-lookup"><span data-stu-id="dd11e-211">**Name**</span></span> |<span data-ttu-id="dd11e-212">Текст, представляющий имя правила балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="dd11e-212">A text name representing the load balancing rules.</span></span> <span data-ttu-id="dd11e-213">Например, **SQLAlwaysOnEndPointListener**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-213">For example, **SQLAlwaysOnEndPointListener**.</span></span> |
   | <span data-ttu-id="dd11e-214">**Протокол**</span><span class="sxs-lookup"><span data-stu-id="dd11e-214">**Protocol**</span></span> |<span data-ttu-id="dd11e-215">**TCP**</span><span class="sxs-lookup"><span data-stu-id="dd11e-215">**TCP**</span></span> |
   | <span data-ttu-id="dd11e-216">**Порт**</span><span class="sxs-lookup"><span data-stu-id="dd11e-216">**Port**</span></span> |<span data-ttu-id="dd11e-217">*1433*</span><span class="sxs-lookup"><span data-stu-id="dd11e-217">*1433*</span></span> |
   | <span data-ttu-id="dd11e-218">**Серверный порт**</span><span class="sxs-lookup"><span data-stu-id="dd11e-218">**Backend Port**</span></span> |<span data-ttu-id="dd11e-219">*1433*. Это значение игнорируется, поскольку правило использует **плавающий IP-адрес (прямой ответ от сервера)**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-219">*1433*. This value is ignored because this rule uses **Floating IP (direct server return)**.</span></span> |
   | <span data-ttu-id="dd11e-220">**Проба**</span><span class="sxs-lookup"><span data-stu-id="dd11e-220">**Probe**</span></span> |<span data-ttu-id="dd11e-221">Используйте имя пробы, созданной для этого балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="dd11e-221">Use the name of the probe that you created for this load balancer.</span></span> |
   | <span data-ttu-id="dd11e-222">**Сохранение сеанса**</span><span class="sxs-lookup"><span data-stu-id="dd11e-222">**Session persistence**</span></span> |<span data-ttu-id="dd11e-223">**None**</span><span class="sxs-lookup"><span data-stu-id="dd11e-223">**None**</span></span> |
   | <span data-ttu-id="dd11e-224">**Время ожидания простоя (в минутах)**</span><span class="sxs-lookup"><span data-stu-id="dd11e-224">**Idle timeout (minutes)**</span></span> |<span data-ttu-id="dd11e-225">*4*</span><span class="sxs-lookup"><span data-stu-id="dd11e-225">*4*</span></span> |
   | <span data-ttu-id="dd11e-226">**Плавающий IP-адрес (прямой ответ от сервера)**</span><span class="sxs-lookup"><span data-stu-id="dd11e-226">**Floating IP (direct server return)**</span></span> |<span data-ttu-id="dd11e-227">**Включено**</span><span class="sxs-lookup"><span data-stu-id="dd11e-227">**Enabled**</span></span> |

   > [!NOTE]
   > <span data-ttu-id="dd11e-228">Возможно, потребуется прокрутить колонку вниз, чтобы просмотреть все параметры.</span><span class="sxs-lookup"><span data-stu-id="dd11e-228">You might have to scroll down the blade to view all the settings.</span></span>
   > 

4. <span data-ttu-id="dd11e-229">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-229">Click **OK**.</span></span> 
5. <span data-ttu-id="dd11e-230">Azure настроит правило балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="dd11e-230">Azure configures the load balancing rule.</span></span> <span data-ttu-id="dd11e-231">Теперь подсистема балансировки нагрузки настроена для маршрутизации трафика в экземпляр SQL Server, на котором размещается прослушиватель для группы доступности.</span><span class="sxs-lookup"><span data-stu-id="dd11e-231">Now the load balancer is configured to route traffic to the SQL Server instance that hosts the listener for the availability group.</span></span> 

<span data-ttu-id="dd11e-232">На этом этапе группа ресурсов содержит подсистему балансировки нагрузки, через которую происходит подключение к обеим виртуальным машинам SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dd11e-232">At this point, the resource group has a load balancer that connects to both SQL Server machines.</span></span> <span data-ttu-id="dd11e-233">Подсистема балансировки нагрузки также содержит IP-адрес прослушивателя группы доступности AlwaysOn для SQL Server. Таким образом, любая виртуальная машина может отвечать на запросы для групп доступности.</span><span class="sxs-lookup"><span data-stu-id="dd11e-233">The load balancer also contains an IP address for the SQL Server Always On availability group listener, so that either machine can respond to requests for the availability groups.</span></span>

> [!NOTE]
> <span data-ttu-id="dd11e-234">Если экземпляры SQL Server находятся в разных регионах, повторите эти действия еще раз в другом регионе.</span><span class="sxs-lookup"><span data-stu-id="dd11e-234">If your SQL Server instances are in two separate regions, repeat the steps in the other region.</span></span> <span data-ttu-id="dd11e-235">Балансировщик нагрузки необходим для каждого региона.</span><span class="sxs-lookup"><span data-stu-id="dd11e-235">Each region requires a load balancer.</span></span> 
> 
> 

## <a name="configure-the-cluster-to-use-the-load-balancer-ip-address"></a><span data-ttu-id="dd11e-236">Настройка использования IP-адреса балансировщика нагрузки для кластера</span><span class="sxs-lookup"><span data-stu-id="dd11e-236">Configure the cluster to use the load balancer IP address</span></span>
<span data-ttu-id="dd11e-237">Теперь необходимо настроить прослушиватель в кластере и подключить его.</span><span class="sxs-lookup"><span data-stu-id="dd11e-237">The next step is to configure the listener on the cluster, and bring the listener online.</span></span> <span data-ttu-id="dd11e-238">Выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="dd11e-238">Do the following:</span></span> 

1. <span data-ttu-id="dd11e-239">Создайте прослушиватель группы доступности в отказоустойчивом кластере.</span><span class="sxs-lookup"><span data-stu-id="dd11e-239">Create the availability group listener on the failover cluster.</span></span> 

2. <span data-ttu-id="dd11e-240">Подключите прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="dd11e-240">Bring the listener online.</span></span>

### <a name="step-5-create-the-availability-group-listener-on-the-failover-cluster"></a><span data-ttu-id="dd11e-241">Шаг 5. Создание прослушивателя группы доступности в отказоустойчивом кластере</span><span class="sxs-lookup"><span data-stu-id="dd11e-241">Step 5: Create the availability group listener on the failover cluster</span></span>
<span data-ttu-id="dd11e-242">На этом шаге вручную создается прослушиватель группы доступности в диспетчере отказоустойчивости кластеров и службе SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="dd11e-242">In this step, you manually create the availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

### <a name="verify-the-configuration-of-the-listener"></a><span data-ttu-id="dd11e-243">Проверка конфигурации прослушивателя</span><span class="sxs-lookup"><span data-stu-id="dd11e-243">Verify the configuration of the listener</span></span>

<span data-ttu-id="dd11e-244">Если ресурсы и зависимости кластера настроены правильно, вы увидите прослушиватель в SQL Server Management Studios.</span><span class="sxs-lookup"><span data-stu-id="dd11e-244">If the cluster resources and dependencies are correctly configured, you should be able to view the listener in SQL Server Management Studio.</span></span> <span data-ttu-id="dd11e-245">Чтобы задать порт прослушивателя, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="dd11e-245">To set the listener port, do the following:</span></span>

1. <span data-ttu-id="dd11e-246">Запустите SQL Server Management Studio и подключитесь к основной реплике.</span><span class="sxs-lookup"><span data-stu-id="dd11e-246">Start SQL Server Management Studio, and then connect to the primary replica.</span></span>

2. <span data-ttu-id="dd11e-247">Перейдите в раздел **Высокий уровень доступности AlwaysOn** > **Группы доступности** > **Прослушиватели группы доступности**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-247">Go to **AlwaysOn High Availability** > **Availability Groups** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="dd11e-248">Теперь вы увидите имя прослушивателя, созданного в диспетчере отказоустойчивости кластеров.</span><span class="sxs-lookup"><span data-stu-id="dd11e-248">You should now see the listener name that you created in Failover Cluster Manager.</span></span> 

3. <span data-ttu-id="dd11e-249">Щелкните правой кнопкой мыши имя прослушивателя и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-249">Right-click the listener name, and then click **Properties**.</span></span>

4. <span data-ttu-id="dd11e-250">В поле **Порт** укажите номер порта для прослушивателя группы доступности с помощью использованного ранее параметра $EndpointPort (по умолчанию использовалось значение 1433) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-250">In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort you used earlier (1433 was the default), and then click **OK**.</span></span>

<span data-ttu-id="dd11e-251">Теперь у вас есть группа доступности на виртуальных машинах Azure, работающих в режиме Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dd11e-251">You now have an availability group in Azure virtual machines running in Resource Manager mode.</span></span> 

## <a name="test-the-connection-to-the-listener"></a><span data-ttu-id="dd11e-252">Проверка подключения к прослушивателю</span><span class="sxs-lookup"><span data-stu-id="dd11e-252">Test the connection to the listener</span></span>
<span data-ttu-id="dd11e-253">Чтобы проверить подключение, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="dd11e-253">Test the connection by doing the following:</span></span>

1. <span data-ttu-id="dd11e-254">Подключитесь по протоколу RDP к экземпляру SQL Server, который находится в той же виртуальной сети, но не содержит реплику.</span><span class="sxs-lookup"><span data-stu-id="dd11e-254">RDP to a SQL Server instance that is in the same virtual network, but does not own the replica.</span></span> <span data-ttu-id="dd11e-255">Этот сервер может быть другим экземпляром SQL Server в кластере.</span><span class="sxs-lookup"><span data-stu-id="dd11e-255">This server can be the other SQL Server instance in the cluster.</span></span>

2. <span data-ttu-id="dd11e-256">Для проверки подключения используйте служебную программу **sqlcmd** .</span><span class="sxs-lookup"><span data-stu-id="dd11e-256">Use **sqlcmd** utility to test the connection.</span></span> <span data-ttu-id="dd11e-257">Например, в следующем сценарии **sqlcmd** подключается к основной реплике через прослушиватель с использованием аутентификации Windows.</span><span class="sxs-lookup"><span data-stu-id="dd11e-257">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span></span>
   
        sqlcmd -S <listenerName> -E

<span data-ttu-id="dd11e-258">SQLCMD автоматически подключается к экземпляру SQL Server, на котором размещена основная реплика.</span><span class="sxs-lookup"><span data-stu-id="dd11e-258">The SQLCMD connection automatically connects to the SQL Server instance that hosts the primary replica.</span></span> 

## <a name="create-an-ip-address-for-an-additional-availability-group"></a><span data-ttu-id="dd11e-259">Создание IP-адреса для дополнительной группы доступности</span><span class="sxs-lookup"><span data-stu-id="dd11e-259">Create an IP address for an additional availability group</span></span>

<span data-ttu-id="dd11e-260">Каждая группа доступности использует отдельный прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="dd11e-260">Each availability group uses a separate listener.</span></span> <span data-ttu-id="dd11e-261">У каждого прослушивателя имеется собственный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="dd11e-261">Each listener has its own IP address.</span></span> <span data-ttu-id="dd11e-262">Используйте одну подсистему балансировки нагрузки для обслуживания IP-адреса для дополнительных прослушивателей.</span><span class="sxs-lookup"><span data-stu-id="dd11e-262">Use the same load balancer to hold the IP address for additional listeners.</span></span> <span data-ttu-id="dd11e-263">После создания группы доступности добавьте IP-адрес в подсистему балансировки нагрузки, а затем настройте прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="dd11e-263">After you create an availability group, add the IP address to the load balancer, and then configure the listener.</span></span>

<span data-ttu-id="dd11e-264">Чтобы добавить IP-адрес в подсистему балансировки нагрузки с помощью портала Azure, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="dd11e-264">To add an IP address to a load balancer with the Azure portal, do the following:</span></span>

1. <span data-ttu-id="dd11e-265">На портале Azure откройте группу ресурсов, содержащую подсистему балансировки нагрузки, и щелкните эту подсистему.</span><span class="sxs-lookup"><span data-stu-id="dd11e-265">In the Azure portal, open the resource group that contains the load balancer, and then click the load balancer.</span></span> 

2. <span data-ttu-id="dd11e-266">В разделе **Параметры** щелкните **Пул внешних IP-адресов**, а затем щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-266">Under **SETTINGS**, click **Frontend IP pool**, and then click **Add**.</span></span> 

3. <span data-ttu-id="dd11e-267">В разделе **Добавить внешний IP-адрес** укажите имя внешнего интерфейса.</span><span class="sxs-lookup"><span data-stu-id="dd11e-267">Under **Add frontend IP address**, assign a name for the front end.</span></span> 

4. <span data-ttu-id="dd11e-268">Убедитесь, что указаны те же **виртуальная сеть** и **подсеть**, что и для экземпляров SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dd11e-268">Verify that the **Virtual network** and the **Subnet** are the same as the SQL Server instances.</span></span>

5. <span data-ttu-id="dd11e-269">Задайте IP-адрес для прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="dd11e-269">Set the IP address for the listener.</span></span> 
   
   >[!TIP]
   ><span data-ttu-id="dd11e-270">Можно задать статический IP-адрес, который в настоящее время не используется в подсети.</span><span class="sxs-lookup"><span data-stu-id="dd11e-270">You can set the IP address to static and type an address that is not currently used in the subnet.</span></span> <span data-ttu-id="dd11e-271">Кроме того, можно задать динамический IP-адрес и сохранить новый пул внешних IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="dd11e-271">Alternatively, you can set the IP address to dynamic and save the new front-end IP pool.</span></span> <span data-ttu-id="dd11e-272">При этом портал Azure автоматически назначит пулу доступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="dd11e-272">When you do so, the Azure portal automatically assigns an available IP address to the pool.</span></span> <span data-ttu-id="dd11e-273">Затем можно будет повторно открыть пул внешних IP-адресов и изменить этот адрес на статический.</span><span class="sxs-lookup"><span data-stu-id="dd11e-273">You can then reopen the front-end IP pool and change the assignment to static.</span></span> 

6. <span data-ttu-id="dd11e-274">Сохраните IP-адрес прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="dd11e-274">Save the IP address for the listener.</span></span> 

7. <span data-ttu-id="dd11e-275">Добавьте пробу работоспособности, используя следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="dd11e-275">Add a health probe by using the following settings:</span></span>

   |<span data-ttu-id="dd11e-276">Настройка</span><span class="sxs-lookup"><span data-stu-id="dd11e-276">Setting</span></span> |<span data-ttu-id="dd11e-277">Значение</span><span class="sxs-lookup"><span data-stu-id="dd11e-277">Value</span></span>
   |:-----|:----
   |<span data-ttu-id="dd11e-278">**Имя**</span><span class="sxs-lookup"><span data-stu-id="dd11e-278">**Name**</span></span> |<span data-ttu-id="dd11e-279">Имя для идентификации пробы.</span><span class="sxs-lookup"><span data-stu-id="dd11e-279">A name to identify the probe.</span></span>
   |<span data-ttu-id="dd11e-280">**Протокол**</span><span class="sxs-lookup"><span data-stu-id="dd11e-280">**Protocol**</span></span> |<span data-ttu-id="dd11e-281">TCP</span><span class="sxs-lookup"><span data-stu-id="dd11e-281">TCP</span></span>
   |<span data-ttu-id="dd11e-282">**Порт**</span><span class="sxs-lookup"><span data-stu-id="dd11e-282">**Port**</span></span> |<span data-ttu-id="dd11e-283">Неиспользуемый TCP-порт, который должен быть доступен для всех виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="dd11e-283">An unused TCP port, which must be available on all virtual machines.</span></span> <span data-ttu-id="dd11e-284">Он не должен использоваться для других целей.</span><span class="sxs-lookup"><span data-stu-id="dd11e-284">It cannot be used for any other purpose.</span></span> <span data-ttu-id="dd11e-285">Два прослушивателя не могут использовать один и тот же порт пробы.</span><span class="sxs-lookup"><span data-stu-id="dd11e-285">No two listeners can use the same probe port.</span></span> 
   |<span data-ttu-id="dd11e-286">**Интервал**</span><span class="sxs-lookup"><span data-stu-id="dd11e-286">**Interval**</span></span> |<span data-ttu-id="dd11e-287">Промежуток времени между повторными попытками выполнения пробы.</span><span class="sxs-lookup"><span data-stu-id="dd11e-287">The amount of time between probe attempts.</span></span> <span data-ttu-id="dd11e-288">Используйте значение по умолчанию (5).</span><span class="sxs-lookup"><span data-stu-id="dd11e-288">Use the default (5).</span></span>
   |<span data-ttu-id="dd11e-289">**Пороговое значение сбоя**</span><span class="sxs-lookup"><span data-stu-id="dd11e-289">**Unhealthy threshold**</span></span> |<span data-ttu-id="dd11e-290">Количество последовательных нарушений пороговых значений, после которого виртуальная машина считается неработоспособной.</span><span class="sxs-lookup"><span data-stu-id="dd11e-290">The number of consecutive thresholds that should fail before a virtual machine is considered unhealthy.</span></span>

8. <span data-ttu-id="dd11e-291">Нажмите кнопку **ОК**, чтобы сохранить пробу.</span><span class="sxs-lookup"><span data-stu-id="dd11e-291">Click **OK** to save the probe.</span></span> 

9. <span data-ttu-id="dd11e-292">Создайте правило балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="dd11e-292">Create a load balancing rule.</span></span> <span data-ttu-id="dd11e-293">Выберите **Правила балансировки нагрузки**, затем щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-293">Click **Load balancing rules**, and then click **Add**.</span></span>

10. <span data-ttu-id="dd11e-294">Настройте новое правило балансировки нагрузки, используя следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="dd11e-294">Configure the new load balancing rule by using the following settings:</span></span>

   |<span data-ttu-id="dd11e-295">Настройка</span><span class="sxs-lookup"><span data-stu-id="dd11e-295">Setting</span></span> |<span data-ttu-id="dd11e-296">Значение</span><span class="sxs-lookup"><span data-stu-id="dd11e-296">Value</span></span>
   |:-----|:----
   |<span data-ttu-id="dd11e-297">**Имя**</span><span class="sxs-lookup"><span data-stu-id="dd11e-297">**Name**</span></span> |<span data-ttu-id="dd11e-298">Имя для идентификации правила балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="dd11e-298">A name to identify the load balancing rule.</span></span> 
   |<span data-ttu-id="dd11e-299">**Frontend IP address** (Интерфейсный IP-адрес)</span><span class="sxs-lookup"><span data-stu-id="dd11e-299">**Frontend IP address**</span></span> |<span data-ttu-id="dd11e-300">Выберите IP-адрес, который вы создали.</span><span class="sxs-lookup"><span data-stu-id="dd11e-300">Select the IP address you created.</span></span> 
   |<span data-ttu-id="dd11e-301">**Протокол**</span><span class="sxs-lookup"><span data-stu-id="dd11e-301">**Protocol**</span></span> |<span data-ttu-id="dd11e-302">TCP</span><span class="sxs-lookup"><span data-stu-id="dd11e-302">TCP</span></span>
   |<span data-ttu-id="dd11e-303">**Порт**</span><span class="sxs-lookup"><span data-stu-id="dd11e-303">**Port**</span></span> |<span data-ttu-id="dd11e-304">Укажите порт, используемый экземплярами SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dd11e-304">Use the port that the SQL Server instances are using.</span></span> <span data-ttu-id="dd11e-305">Экземпляр по умолчанию использует порт 1433, если только вы не изменили его.</span><span class="sxs-lookup"><span data-stu-id="dd11e-305">A default instance uses port 1433, unless you changed it.</span></span> 
   |<span data-ttu-id="dd11e-306">**Внутренний порт**</span><span class="sxs-lookup"><span data-stu-id="dd11e-306">**Backend port**</span></span> |<span data-ttu-id="dd11e-307">Укажите то же значение, что и для параметра **Порт**.</span><span class="sxs-lookup"><span data-stu-id="dd11e-307">Use the same value as **Port**.</span></span>
   |<span data-ttu-id="dd11e-308">**Внутренний пул**</span><span class="sxs-lookup"><span data-stu-id="dd11e-308">**Backend pool**</span></span> |<span data-ttu-id="dd11e-309">Пул, содержащий виртуальные машины с экземплярами SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dd11e-309">The pool that contains the virtual machines with the SQL Server instances.</span></span> 
   |<span data-ttu-id="dd11e-310">**Зонд работоспособности**</span><span class="sxs-lookup"><span data-stu-id="dd11e-310">**Health probe**</span></span> |<span data-ttu-id="dd11e-311">Выберите пробу, которую вы создали.</span><span class="sxs-lookup"><span data-stu-id="dd11e-311">Choose the probe you created.</span></span>
   |<span data-ttu-id="dd11e-312">**Сохранение сеанса**</span><span class="sxs-lookup"><span data-stu-id="dd11e-312">**Session persistence**</span></span> |<span data-ttu-id="dd11e-313">None</span><span class="sxs-lookup"><span data-stu-id="dd11e-313">None</span></span>
   |<span data-ttu-id="dd11e-314">**Время ожидания простоя (в минутах)**</span><span class="sxs-lookup"><span data-stu-id="dd11e-314">**Idle timeout (minutes)**</span></span> |<span data-ttu-id="dd11e-315">Оставьте значение по умолчанию (4).</span><span class="sxs-lookup"><span data-stu-id="dd11e-315">Default (4)</span></span>
   |<span data-ttu-id="dd11e-316">**Плавающий IP-адрес (прямой ответ от сервера)**</span><span class="sxs-lookup"><span data-stu-id="dd11e-316">**Floating IP (direct server return)**</span></span> | <span data-ttu-id="dd11e-317">Включено</span><span class="sxs-lookup"><span data-stu-id="dd11e-317">Enabled</span></span>

### <a name="configure-the-availability-group-to-use-the-new-ip-address"></a><span data-ttu-id="dd11e-318">Настройка группы доступности для использования нового IP-адреса</span><span class="sxs-lookup"><span data-stu-id="dd11e-318">Configure the availability group to use the new IP address</span></span>

<span data-ttu-id="dd11e-319">Чтобы завершить настройку кластера, повторите действия, которые были выполнены при создании первой группы доступности.</span><span class="sxs-lookup"><span data-stu-id="dd11e-319">To finish configuring the cluster, repeat the steps that you followed when you made the first availability group.</span></span> <span data-ttu-id="dd11e-320">То есть настройте [кластер для использования нового IP-адреса](#configure-the-cluster-to-use-the-load-balancer-ip-address).</span><span class="sxs-lookup"><span data-stu-id="dd11e-320">That is, configure the [cluster to use the new IP address](#configure-the-cluster-to-use-the-load-balancer-ip-address).</span></span> 

<span data-ttu-id="dd11e-321">После добавления IP-адреса для прослушивателя можно настроить дополнительную группу доступности, сделав следующее:</span><span class="sxs-lookup"><span data-stu-id="dd11e-321">After you have added an IP address for the listener, configure the additional availability group by doing the following:</span></span> 

1. <span data-ttu-id="dd11e-322">Убедитесь, что порт пробы для нового IP-адреса открыт на обеих виртуальных машинах SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dd11e-322">Verify that the probe port for the new IP address is open on both SQL Server virtual machines.</span></span> 

2. <span data-ttu-id="dd11e-323">[Создайте точку доступа клиента в диспетчере кластеров.](#addcap)</span><span class="sxs-lookup"><span data-stu-id="dd11e-323">[In Cluster Manager, add the client access point](#addcap).</span></span>

3. <span data-ttu-id="dd11e-324">[Настройте ресурс IP-адреса для группы доступности](#congroup).</span><span class="sxs-lookup"><span data-stu-id="dd11e-324">[Configure the IP resource for the availability group](#congroup).</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="dd11e-325">При создании IP-адрес используйте IP-адрес, добавленный в подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="dd11e-325">When you create the IP address, use the IP address that you added to the load balancer.</span></span>  

4. <span data-ttu-id="dd11e-326">[Сделайте так, чтобы ресурс группы доступности SQL Server зависел от точки доступа клиента.](#dependencyGroup)</span><span class="sxs-lookup"><span data-stu-id="dd11e-326">[Make the SQL Server availability group resource dependent on the client access point](#dependencyGroup).</span></span>

5. <span data-ttu-id="dd11e-327">[Сделайте так, чтобы ресурс точки доступа клиента зависел от IP-адреса](#listname).</span><span class="sxs-lookup"><span data-stu-id="dd11e-327">[Make the client access point resource dependent on the IP address](#listname).</span></span>
 
6. <span data-ttu-id="dd11e-328">[Настройте параметры кластера в PowerShell](#setparam).</span><span class="sxs-lookup"><span data-stu-id="dd11e-328">[Set the cluster parameters in PowerShell](#setparam).</span></span>

<span data-ttu-id="dd11e-329">Настроив группу доступности для использования нового IP-адреса, настройте подключение к прослушивателю.</span><span class="sxs-lookup"><span data-stu-id="dd11e-329">After you configure the availability group to use the new IP address, configure the connection to the listener.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="dd11e-330">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dd11e-330">Next steps</span></span>

- [<span data-ttu-id="dd11e-331">Настройка группы доступности AlwaysOn на виртуальных машинах Azure в разных регионах</span><span class="sxs-lookup"><span data-stu-id="dd11e-331">Configure a SQL Server Always On availability group on Azure virtual machines in different regions</span></span>](virtual-machines-windows-portal-sql-availability-group-dr.md)
