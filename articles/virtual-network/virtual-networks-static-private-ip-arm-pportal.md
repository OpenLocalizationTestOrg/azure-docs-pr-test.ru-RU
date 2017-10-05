---
title: "Настройка частных IP-адресов для виртуальных машин с помощью портала Azure | Документация Майкрософт"
description: "Узнайте, как настроить частные IP-адреса для виртуальных машин с помощью портала Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 672462fad715758e50680fa5bade4b1f9d50e6e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-portal"></a><span data-ttu-id="c1e40-103">Настройка частных IP-адресов для виртуальной машины с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="c1e40-103">Configure private IP addresses for a virtual machine using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c1e40-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="c1e40-104">Azure portal</span></span>](virtual-networks-static-private-ip-arm-pportal.md)
> * [<span data-ttu-id="c1e40-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1e40-105">PowerShell</span></span>](virtual-networks-static-private-ip-arm-ps.md)
> * [<span data-ttu-id="c1e40-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="c1e40-106">Azure CLI</span></span>](virtual-networks-static-private-ip-arm-cli.md)
> * [<span data-ttu-id="c1e40-107">Портал Azure (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="c1e40-107">Azure portal (Classic)</span></span>](virtual-networks-static-private-ip-classic-pportal.md)
> * [<span data-ttu-id="c1e40-108">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="c1e40-108">PowerShell (Classic)</span></span>](virtual-networks-static-private-ip-classic-ps.md)
> * [<span data-ttu-id="c1e40-109">Интерфейс командной строки Azure (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="c1e40-109">Azure CLI (Classic)</span></span>](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="c1e40-110">В этой статье описывается модель развертывания с использованием менеджера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c1e40-110">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="c1e40-111">Кроме того, вы можете [управлять статическим частным IP-адресом в классической модели развертывания](virtual-networks-static-private-ip-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="c1e40-111">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="c1e40-112">Для выполнения приведенных ниже примеров действий требуется созданная простая среда.</span><span class="sxs-lookup"><span data-stu-id="c1e40-112">The sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="c1e40-113">Чтобы выполнять действия в соответствии с указаниями, представленными в этом документе, сначала постройте тестовую среду, как описано в статье [Создание виртуальной сети](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="c1e40-113">If you want to run the steps as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-pportal.md).</span></span>

## <a name="how-to-create-a-vm-for-testing-static-private-ip-addresses"></a><span data-ttu-id="c1e40-114">Как создать виртуальную машину для тестирования статических частных IP-адресов</span><span class="sxs-lookup"><span data-stu-id="c1e40-114">How to create a VM for testing static private IP addresses</span></span>
<span data-ttu-id="c1e40-115">Невозможно задать статический частный IP-адрес во время создания виртуальной машины в режиме развертывания диспетчера ресурсов с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="c1e40-115">You cannot set a static private IP address during the creation of a VM in the Resource Manager deployment mode by using the Azure portal.</span></span> <span data-ttu-id="c1e40-116">Сначала необходимо создать виртуальную машину, а затем указать, что ее статический IP-адрес является частным.</span><span class="sxs-lookup"><span data-stu-id="c1e40-116">You must create the VM first, tehn set its private IP to be static.</span></span>

<span data-ttu-id="c1e40-117">Чтобы создать виртуальную машину *DNS01* в подсети *FrontEnd* виртуальной сети *TestVNet*, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c1e40-117">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet*, follow the steps below.</span></span>

1. <span data-ttu-id="c1e40-118">В браузере откройте адрес http://portal.azure.com и войдите с помощью учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="c1e40-118">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="c1e40-119">Щелкните **Создать** > **Вычисление** > **Windows Server 2012 R2 Datacenter**. Обратите внимание на то, что в списке **Выберите модель развертывания** уже указан параметр **Resource Manager**, и нажмите кнопку **Создать** (см. рисунок ниже).</span><span class="sxs-lookup"><span data-stu-id="c1e40-119">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that the **Select a deployment model** list already shows **Resource Manager**, and then click **Create**, as seen in the figure below.</span></span>
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. <span data-ttu-id="c1e40-121">В колонке **Основные** введите имя создаваемой виртуальной машины (в нашем случае это*DNS01* ), учетную запись локального администратора и пароль, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="c1e40-121">In the **Basics** blade, enter the name of the VM to be created (*DNS01* in our scenario), the local administrator account, and password, as seen in the figure below.</span></span>
   
    ![Колонка «Основные»](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. <span data-ttu-id="c1e40-123">В качестве **расположения** выберите *Центральная часть США*, щелкните **Выбрать существующую** в разделе **Группа ресурсов**, а затем еще раз щелкните **Группа ресурсов**, выберите *TestRG* и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c1e40-123">Make sure the **Location** selected is *Central US*, then click **Select existing** under **Resource group**, then click **Resource group** again, then click *TestRG*, and then click **OK**.</span></span>
   
    ![Колонка «Основные»](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. <span data-ttu-id="c1e40-125">В колонке **Выбор размера** выберите **A1 Standard**, а затем щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c1e40-125">In the **Choose a size** blade, select **A1 Standard**, and then click **Select**.</span></span>
   
    ![Колонка «Выбор размера»](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. <span data-ttu-id="c1e40-127">Задайте в колонке **Параметры** значения свойств, указанные ниже, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c1e40-127">In teh **Settings** blade, make sure the following properties are set are set with the values below, and then click **OK**.</span></span>
   
    <span data-ttu-id="c1e40-128">-**Учетная запись**: *vnetstorage*</span><span class="sxs-lookup"><span data-stu-id="c1e40-128">-**Storage account**: *vnetstorage*</span></span>
   
   * <span data-ttu-id="c1e40-129">**Сеть**: *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="c1e40-129">**Network**: *TestVNet*</span></span>
   * <span data-ttu-id="c1e40-130">**Подсеть**: *FrontEnd*</span><span class="sxs-lookup"><span data-stu-id="c1e40-130">**Subnet**: *FrontEnd*</span></span>
     
     ![Колонка «Выбор размера»](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. <span data-ttu-id="c1e40-132">В колонке **Сводка** нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c1e40-132">In the **Summary** blade, click **OK**.</span></span> <span data-ttu-id="c1e40-133">Ниже обратите внимание на элемент, отображенный в панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="c1e40-133">Notice the tile below displayed in your dashboard.</span></span>
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="c1e40-135">Как получить информацию о статическом частном IP-адресе виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c1e40-135">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="c1e40-136">Чтобы просмотреть информацию о статическом частном IP-адресе виртуальной машины, созданной с помощью описанные выше действий, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="c1e40-136">To view the static private IP address information for the VM created with the steps above, execute the steps below.</span></span>

1. <span data-ttu-id="c1e40-137">На портале Azure щелкните **Просмотреть все** > **Виртуальные машины** > **DNS01** > **Все параметры** > **Сетевые интерфейсы**, а затем щелкните единственный сетевой интерфейс в списке.</span><span class="sxs-lookup"><span data-stu-id="c1e40-137">From the Azure Azure portal, click **BROWSE ALL** > **Virtual machines** > **DNS01** > **All settings** > **Network interfaces** and then click on the only network interface listed.</span></span>
   
    ![Элемент «Развертывание виртуальной машины»](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. <span data-ttu-id="c1e40-139">В колонке **Сетевой интерфейс** щелкните **Все параметры** > **IP-адреса** и посмотрите на значения **Назначение** и **IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="c1e40-139">In the **Network interface** blade, click **All settings** > **IP addresses** and notice the **Assignment** and **IP address** values.</span></span>
   
    ![Элемент «Развертывание виртуальной машины»](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-to-add-a-static-private-ip-address-to-an-existing-vm"></a><span data-ttu-id="c1e40-141">Как добавить статический частный IP-адрес для существующей виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c1e40-141">How to add a static private IP address to an existing VM</span></span>
<span data-ttu-id="c1e40-142">Чтобы добавить статический частный IP-адрес для виртуальной машины, созданной с помощью действий, описанных выше, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="c1e40-142">To add a static private IP address to the VM created using the steps above, follow the steps below:</span></span>

1. <span data-ttu-id="c1e40-143">В колонке **IP-адреса**, показанной выше, в разделе **Назначение** щелкните **Статический**.</span><span class="sxs-lookup"><span data-stu-id="c1e40-143">From the **IP addresses** blade shown above, click **Static** under **Assignment**.</span></span>
2. <span data-ttu-id="c1e40-144">Введите *192.168.1.101* в поле **IP-адрес**, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c1e40-144">Type *192.168.1.101* for **IP address**, and then click **Save**.</span></span>
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> <span data-ttu-id="c1e40-146">Если после нажатия кнопки **Сохранить** назначение по-прежнему остается **динамическим**, это означает, что введенный IP-адрес уже используется.</span><span class="sxs-lookup"><span data-stu-id="c1e40-146">If after clicking **Save** you notice that the assignment is still set to **Dynamic**, it means that the IP address you typed is already in use.</span></span> <span data-ttu-id="c1e40-147">Попробуйте другой IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c1e40-147">Try a different IP address.</span></span>
> 
> 

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="c1e40-148">Как удалить статический частный IP-адрес виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c1e40-148">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="c1e40-149">Чтобы удалить статический частный IP-адрес виртуальной машины, созданной ранее, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="c1e40-149">To remove the static private IP address from the VM created above, complete the following step:</span></span>

<span data-ttu-id="c1e40-150">В колонке **IP-адреса**, показанной выше, в разделе **Назначение** щелкните **Динамический** и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c1e40-150">From the **IP addresses** blade shown above, click **Dynamic** under **Assignment**, and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1e40-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c1e40-151">Next steps</span></span>
* <span data-ttu-id="c1e40-152">Ознакомьтесь с информацией о [зарезервированных общедоступных IP-адресах](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="c1e40-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="c1e40-153">Узнайте об [общедоступных IP-адресах уровня экземпляра (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="c1e40-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="c1e40-154">Ознакомьтесь с информацией о [REST API зарезервированных IP-адресов](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="c1e40-154">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

