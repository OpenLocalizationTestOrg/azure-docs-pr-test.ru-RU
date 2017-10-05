---
title: "Настройка частных IP-адресов для (классических) виртуальных машин с помощью портала Azure | Документация Майкрософт"
description: "Узнайте, как настроить частные IP-адреса для (классических) виртуальных машин с помощью портала Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bde6de3495c2909b63b1f85e420a4ff5e7ac2c1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-the-azure-portal"></a><span data-ttu-id="1a2bb-103">Настройка частных IP-адресов для (классической) виртуальной машины с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="1a2bb-103">Configure private IP addresses for a virtual machine (Classic) using the Azure portal</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="1a2bb-104">В этой статье рассматривается классическая модель развертывания.</span><span class="sxs-lookup"><span data-stu-id="1a2bb-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="1a2bb-105">Кроме того, вы можете [управлять статическим частным IP-адресом в модели развертывания для диспетчера ресурсов](virtual-networks-static-private-ip-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="1a2bb-105">You can also [manage a static private IP address in the Resource Manager deployment model](virtual-networks-static-private-ip-arm-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="1a2bb-106">Для выполнения приведенных ниже примеров действий требуется созданная простая среда.</span><span class="sxs-lookup"><span data-stu-id="1a2bb-106">The sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="1a2bb-107">Чтобы выполнять действия в соответствии с указаниями, представленными в этом документе, сначала постройте тестовую среду, как описано в статье [Создание виртуальной сети](virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="1a2bb-107">If you want to run the steps as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-classic-pportal.md).</span></span>

## <a name="how-to-specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="1a2bb-108">Указание статического частного IP-адреса при создании виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="1a2bb-108">How to specify a static private IP address when creating a VM</span></span>
<span data-ttu-id="1a2bb-109">Чтобы создать виртуальную машину с именем *DNS01* в подсети *FrontEnd* виртуальной сети *TestVNet* со статическим частным IP-адресом *192.168.1.101*, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1a2bb-109">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="1a2bb-110">В браузере откройте адрес http://portal.azure.com и войдите с помощью учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="1a2bb-110">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="1a2bb-111">Щелкните **Создать** > **Вычисление** > **Windows Server 2012 R2 Datacenter**. Обратите внимание на то, что в списке **Выберите модель развертывания** уже указан параметр **Классический**, и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1a2bb-111">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that the **Select a deployment model** list already shows **Classic**, and then click **Create**.</span></span>
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. <span data-ttu-id="1a2bb-113">В колонке **Создать VM** введите имя создаваемой виртуальной машины (в нашем случае это*DNS01* ), учетную запись локального администратора и пароль.</span><span class="sxs-lookup"><span data-stu-id="1a2bb-113">In the **Create VM** blade, enter the name of the VM to be created (*DNS01* in our scenario), the local administrator account, and password.</span></span>
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. <span data-ttu-id="1a2bb-115">Щелкните **Необязательная конфигурация** > **Сеть** > **Виртуальная сеть**, а затем — **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="1a2bb-115">Click **Optional Configuration** > **Network** > **Virtual Network**, and then click **TestVNet**.</span></span> <span data-ttu-id="1a2bb-116">Если сеть **TestVNet** недоступна, убедитесь, что вы используете расположение *Центральная часть США* и создали тестовую среду, описанную в начале этой статьи.</span><span class="sxs-lookup"><span data-stu-id="1a2bb-116">If **TestVNet** is not available, make sure you are using the *Central US* location and have created the test environment described at the beginning of this article.</span></span>
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. <span data-ttu-id="1a2bb-118">В колонке **Сеть** выберите подсеть *FrontEnd* и щелкните **IP-адреса**. В разделе **Назначение IP-адресов** щелкните **Статический** и введите *192.168.1.101* в поле **IP-адрес**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="1a2bb-118">In the **Network** blade, make sure the subnet currently selected is *FrontEnd*, then click **IP addresses**, under **IP address assignment** click **Static**, and then enter *192.168.1.101* for **IP Address** as seen below.</span></span>
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. <span data-ttu-id="1a2bb-120">Нажмите кнопку **ОК** в колонке **IP-адреса**, затем нажмите кнопку **ОК** в колонке **Сеть**. После этого нажмите кнопку **ОК** в колонке **Необязательная конфигурация**.</span><span class="sxs-lookup"><span data-stu-id="1a2bb-120">Click **OK** in the **IP addresses** blade, then click **OK** in the **Network** blade, and click **OK** in the **Optional config** blade.</span></span>
7. <span data-ttu-id="1a2bb-121">В колонке **Создать виртуальную машину** щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1a2bb-121">In the **Create VM** blade, click **Create**.</span></span> <span data-ttu-id="1a2bb-122">Ниже обратите внимание на элемент, отображенный в панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="1a2bb-122">Notice the tile below displayed in your dashboard.</span></span>
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="1a2bb-124">Как получить информацию о статическом частном IP-адресе виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="1a2bb-124">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="1a2bb-125">Чтобы просмотреть информацию о статическом частном IP-адресе виртуальной машины, созданной с помощью описанные выше действий, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="1a2bb-125">To view the static private IP address information for the VM created with the steps above, execute the steps below.</span></span>

1. <span data-ttu-id="1a2bb-126">На портале Azure щелкните **Просмотреть все** > **Виртуальные машины (классические)** > **DNS01** > **Все параметры** > **IP-адреса** и обратите внимание на назначение IP-адресов и сам IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="1a2bb-126">From the Azure Azure portal, click **BROWSE ALL** > **Virtual machines (classic)** > **DNS01** > **All settings** > **IP addresses** and notice the IP address assignment and IP address as seen below.</span></span>
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="1a2bb-128">Как удалить статический частный IP-адрес виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="1a2bb-128">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="1a2bb-129">Чтобы удалить статический частный IP-адрес виртуальной машины, созданной ранее, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="1a2bb-129">To remove the static private IP address from the VM created above, follow the steps below.</span></span>

1. <span data-ttu-id="1a2bb-130">В колонке **IP-адреса**, показанной ранее, щелкните **Динамический** справа от элемента **Назначение IP-адресов**, нажмите кнопку **Сохранить**, а затем — **Да**.</span><span class="sxs-lookup"><span data-stu-id="1a2bb-130">From the **IP addresses** blade shown above, click **Dynamic** to the right of **IP address assignment**, then click **Save**, and then click **Yes**.</span></span>
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-to-add-a-static-private-ip-address-to-an-existing-vm"></a><span data-ttu-id="1a2bb-132">Как добавить статический частный IP-адрес для существующей виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="1a2bb-132">How to add a static private IP address to an existing VM</span></span>
<span data-ttu-id="1a2bb-133">Чтобы добавить статический частный IP-адрес для виртуальной машины, созданной с помощью действий, описанных выше, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="1a2bb-133">To add a static private IP address to the VM created using the steps above, follow the steps below:</span></span>

1. <span data-ttu-id="1a2bb-134">В колонке **IP-адреса**, показанной выше, справа от элемента **Назначение IP-адресов** щелкните **Статический**.</span><span class="sxs-lookup"><span data-stu-id="1a2bb-134">From the **IP addresses** blade shown above, click **Static** to the right of **IP address assignment**.</span></span>
2. <span data-ttu-id="1a2bb-135">Введите *192.168.1.101* в поле **IP-адрес**, нажмите кнопку **Сохранить**, а затем — **Да**.</span><span class="sxs-lookup"><span data-stu-id="1a2bb-135">Type *192.168.1.101* for **IP address**, then click **Save**, and then click **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a2bb-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1a2bb-136">Next steps</span></span>
* <span data-ttu-id="1a2bb-137">Ознакомьтесь с информацией о [зарезервированных общедоступных IP-адресах](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="1a2bb-137">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="1a2bb-138">Узнайте об [общедоступных IP-адресах уровня экземпляра (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="1a2bb-138">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="1a2bb-139">Ознакомьтесь с информацией о [REST API зарезервированных IP-адресов](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="1a2bb-139">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

