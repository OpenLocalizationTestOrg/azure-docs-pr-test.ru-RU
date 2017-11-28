---
title: "aaaConfigure частных IP-адресов для виртуальных машин - портал Azure | Документы Microsoft"
description: "Узнайте, как tooconfigure частных IP-адресов для виртуальных машин с помощью hello портал Azure."
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
ms.openlocfilehash: 474161303cdf8cb98e16ffd7cef6b74debdbc49a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-portal"></a><span data-ttu-id="39ddc-103">Настройка частного IP-адреса для виртуальной машины с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="39ddc-103">Configure private IP addresses for a virtual machine using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="39ddc-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="39ddc-104">Azure portal</span></span>](virtual-networks-static-private-ip-arm-pportal.md)
> * [<span data-ttu-id="39ddc-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="39ddc-105">PowerShell</span></span>](virtual-networks-static-private-ip-arm-ps.md)
> * [<span data-ttu-id="39ddc-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="39ddc-106">Azure CLI</span></span>](virtual-networks-static-private-ip-arm-cli.md)
> * [<span data-ttu-id="39ddc-107">Портал Azure (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="39ddc-107">Azure portal (Classic)</span></span>](virtual-networks-static-private-ip-classic-pportal.md)
> * [<span data-ttu-id="39ddc-108">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="39ddc-108">PowerShell (Classic)</span></span>](virtual-networks-static-private-ip-classic-ps.md)
> * [<span data-ttu-id="39ddc-109">Интерфейс командной строки Azure (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="39ddc-109">Azure CLI (Classic)</span></span>](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="39ddc-110">В этой статье рассматриваются hello модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="39ddc-110">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="39ddc-111">Вы также можете [управление статический частный IP-адрес в hello классической модели развертывания](virtual-networks-static-private-ip-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="39ddc-111">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="39ddc-112">следующие действия Образец Hello ожидать простой среде уже создан.</span><span class="sxs-lookup"><span data-stu-id="39ddc-112">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="39ddc-113">Требуется toorun hello действия, показанной в этом документе, вначале построить hello тестовой среде, описанной в [создании виртуальной сети](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="39ddc-113">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-pportal.md).</span></span>

## <a name="how-toocreate-a-vm-for-testing-static-private-ip-addresses"></a><span data-ttu-id="39ddc-114">Каким образом соответствие toocreate ВМ для тестирования статических частных IP-адресов</span><span class="sxs-lookup"><span data-stu-id="39ddc-114">How toocreate a VM for testing static private IP addresses</span></span>
<span data-ttu-id="39ddc-115">Нельзя задать статический частный IP-адрес во время создания виртуальной Машины в режим развертывания диспетчера ресурсов hello hello, используя hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="39ddc-115">You cannot set a static private IP address during hello creation of a VM in hello Resource Manager deployment mode by using hello Azure portal.</span></span> <span data-ttu-id="39ddc-116">Необходимо сначала создать hello виртуальной Машины, последующей задан его частного IP toobe статический.</span><span class="sxs-lookup"><span data-stu-id="39ddc-116">You must create hello VM first, tehn set its private IP toobe static.</span></span>

<span data-ttu-id="39ddc-117">Виртуальную машину с именем toocreate *DNS01* в hello *переднего плана* подсети виртуальной сети с именем *TestVNet*, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="39ddc-117">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet*, follow hello steps below.</span></span>

1. <span data-ttu-id="39ddc-118">В браузере перейдите toohttp://portal.azure.com и при необходимости выполните вход с помощью учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="39ddc-118">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="39ddc-119">Нажмите кнопку **NEW** > **вычислений** > **Windows Server 2012 R2 Datacenter**, обратите внимание, что hello **выберите модель развертывания** представлен список уже **диспетчера ресурсов**, а затем нажмите кнопку **создать**, как показано в приведенном ниже рисунке hello.</span><span class="sxs-lookup"><span data-stu-id="39ddc-119">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Resource Manager**, and then click **Create**, as seen in hello figure below.</span></span>
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. <span data-ttu-id="39ddc-121">В hello **основы** колонки, введите имя hello создан toobe ВМ hello (*DNS01* в нашем сценарии), hello учетной записи локального администратора и пароль, как показано на следующем рисунке hello.</span><span class="sxs-lookup"><span data-stu-id="39ddc-121">In hello **Basics** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password, as seen in hello figure below.</span></span>
   
    ![Колонка «Основные»](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. <span data-ttu-id="39ddc-123">Убедитесь, что hello **расположение** выбранный *центральной части США*, нажмите кнопку **выбрать существующий** под **группы ресурсов**, нажмите кнопку **Группы ресурсов** еще раз, нажмите кнопку *TestRG*, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="39ddc-123">Make sure hello **Location** selected is *Central US*, then click **Select existing** under **Resource group**, then click **Resource group** again, then click *TestRG*, and then click **OK**.</span></span>
   
    ![Колонка «Основные»](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. <span data-ttu-id="39ddc-125">В hello **выберите размер** колонке выберите **A1 Standard**, а затем нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="39ddc-125">In hello **Choose a size** blade, select **A1 Standard**, and then click **Select**.</span></span>
   
    ![Колонка «Выбор размера»](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. <span data-ttu-id="39ddc-127">В **параметры** колонки, убедитесь, что hello следующие свойства задаются задаются со значениями hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="39ddc-127">In teh **Settings** blade, make sure hello following properties are set are set with hello values below, and then click **OK**.</span></span>
   
    <span data-ttu-id="39ddc-128">-**Учетная запись**: *vnetstorage*</span><span class="sxs-lookup"><span data-stu-id="39ddc-128">-**Storage account**: *vnetstorage*</span></span>
   
   * <span data-ttu-id="39ddc-129">**Сеть**: *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="39ddc-129">**Network**: *TestVNet*</span></span>
   * <span data-ttu-id="39ddc-130">**Подсеть**: *FrontEnd*</span><span class="sxs-lookup"><span data-stu-id="39ddc-130">**Subnet**: *FrontEnd*</span></span>
     
     ![Колонка «Выбор размера»](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. <span data-ttu-id="39ddc-132">В hello **Сводка** колонка, щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="39ddc-132">In hello **Summary** blade, click **OK**.</span></span> <span data-ttu-id="39ddc-133">Обратите внимание hello Плитка ниже отображаются в панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="39ddc-133">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="39ddc-135">Как статических частных IP-tooretrieve адресов сведения для виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="39ddc-135">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="39ddc-136">tooview hello статических частных IP-адресе для hello виртуальных Машин, созданных с hello указанную выше процедуру, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="39ddc-136">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="39ddc-137">На портале Azure Azure hello, нажмите кнопку **ПРОСМОТРЕТЬ все** > **виртуальные машины** > **DNS01** > **все Параметры** > **сетевых интерфейсов** и выберите только сетевой интерфейс hello в списке.</span><span class="sxs-lookup"><span data-stu-id="39ddc-137">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines** > **DNS01** > **All settings** > **Network interfaces** and then click on hello only network interface listed.</span></span>
   
    ![Элемент «Развертывание виртуальной машины»](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. <span data-ttu-id="39ddc-139">В hello **сетевой интерфейс** колонке нажмите кнопку **все параметры** > **IP-адреса** и hello уведомление **назначения** и **IP-адрес** значения.</span><span class="sxs-lookup"><span data-stu-id="39ddc-139">In hello **Network interface** blade, click **All settings** > **IP addresses** and notice hello **Assignment** and **IP address** values.</span></span>
   
    ![Элемент «Развертывание виртуальной машины»](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="39ddc-141">Как tooadd статический частных IP-адрес решения tooan существующей виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="39ddc-141">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="39ddc-142">tooadd статические частного IP адрес toohello виртуальной Машины, созданной с помощью hello указанную выше процедуру, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="39ddc-142">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="39ddc-143">Из hello **IP-адреса** колонки, показанном выше, нажмите кнопку **статических** под **назначения**.</span><span class="sxs-lookup"><span data-stu-id="39ddc-143">From hello **IP addresses** blade shown above, click **Static** under **Assignment**.</span></span>
2. <span data-ttu-id="39ddc-144">Введите *192.168.1.101* в поле **IP-адрес**, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="39ddc-144">Type *192.168.1.101* for **IP address**, and then click **Save**.</span></span>
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> <span data-ttu-id="39ddc-146">Если после нажатия кнопки **Сохранить** Обратите внимание, что назначение hello по-прежнему задано слишком**динамическое**, это означает, что IP-адрес hello, вы ввели уже используется.</span><span class="sxs-lookup"><span data-stu-id="39ddc-146">If after clicking **Save** you notice that hello assignment is still set too**Dynamic**, it means that hello IP address you typed is already in use.</span></span> <span data-ttu-id="39ddc-147">Попробуйте другой IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="39ddc-147">Try a different IP address.</span></span>
> 
> 

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="39ddc-148">Как tooremove статических частных IP-адресов из виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="39ddc-148">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="39ddc-149">tooremove hello статический частный IP-адрес из приветствия созданную виртуальную Машину, выполните даст hello.</span><span class="sxs-lookup"><span data-stu-id="39ddc-149">tooremove hello static private IP address from hello VM created above, complete hello following step:</span></span>

<span data-ttu-id="39ddc-150">Из hello **IP-адреса** колонки, показанном выше, нажмите кнопку **динамическое** под **назначения**и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="39ddc-150">From hello **IP addresses** blade shown above, click **Dynamic** under **Assignment**, and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39ddc-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="39ddc-151">Next steps</span></span>
* <span data-ttu-id="39ddc-152">Ознакомьтесь с информацией о [зарезервированных общедоступных IP-адресах](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="39ddc-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="39ddc-153">Узнайте об [общедоступных IP-адресах уровня экземпляра (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="39ddc-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="39ddc-154">Обратитесь к hello [зарезервированные интерфейсы REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="39ddc-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

