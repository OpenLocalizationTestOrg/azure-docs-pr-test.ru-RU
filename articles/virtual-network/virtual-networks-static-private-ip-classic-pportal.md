---
title: "aaaConfigure частных IP-адресов для виртуальных машин (обычная) — портал Azure | Документы Microsoft"
description: "Узнайте, как tooconfigure частных IP-адресов для виртуальных машин (классические) с помощью hello портал Azure."
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
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a><span data-ttu-id="dc0b6-103">Настройка частного IP-адреса для виртуальной машины при помощи hello портал Azure (классические)</span><span class="sxs-lookup"><span data-stu-id="dc0b6-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="dc0b6-104">В этой статье рассматриваются hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="dc0b6-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="dc0b6-105">Вы также можете [управление статический частный IP-адрес в модели развертывания диспетчера ресурсов hello](virtual-networks-static-private-ip-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="dc0b6-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="dc0b6-106">следующие действия Образец Hello ожидать простой среде уже создан.</span><span class="sxs-lookup"><span data-stu-id="dc0b6-106">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="dc0b6-107">Требуется toorun hello действия, показанной в этом документе, вначале построить hello тестовой среде, описанной в [создании виртуальной сети](virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="dc0b6-107">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-pportal.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="dc0b6-108">Как toospecify статических частных IP-адресов при создании виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="dc0b6-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="dc0b6-109">toocreate Виртуальную машину с именем *DNS01* в hello *переднего плана* подсети виртуальной сети с именем *TestVNet* с статических частного IP-адреса *192.168.1.101*, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="dc0b6-109">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="dc0b6-110">В браузере перейдите toohttp://portal.azure.com и при необходимости выполните вход с помощью учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="dc0b6-110">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="dc0b6-111">Нажмите кнопку **NEW** > **вычислений** > **Windows Server 2012 R2 Datacenter**, обратите внимание, что hello **выберите модель развертывания** представлен список уже **классический**, а затем нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="dc0b6-111">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Classic**, and then click **Create**.</span></span>
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. <span data-ttu-id="dc0b6-113">В hello **Создание ВМ** колонки, введите имя hello создан toobe ВМ hello (*DNS01* в нашем сценарии), hello учетной записи локального администратора и пароль.</span><span class="sxs-lookup"><span data-stu-id="dc0b6-113">In hello **Create VM** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password.</span></span>
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. <span data-ttu-id="dc0b6-115">Щелкните **Необязательная конфигурация** > **Сеть** > **Виртуальная сеть**, а затем — **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="dc0b6-115">Click **Optional Configuration** > **Network** > **Virtual Network**, and then click **TestVNet**.</span></span> <span data-ttu-id="dc0b6-116">Если **TestVNet** недоступно, убедитесь, что вы используете hello *центральной части США* расположение и созданы hello тестовой среды, описанные в начале этой статьи hello.</span><span class="sxs-lookup"><span data-stu-id="dc0b6-116">If **TestVNet** is not available, make sure you are using hello *Central US* location and have created hello test environment described at hello beginning of this article.</span></span>
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. <span data-ttu-id="dc0b6-118">В hello **сети** колонки, убедитесь, что hello подсети выбранного в данный момент является *переднего плана*, нажмите кнопку **IP-адреса**в разделе **назначения IP-адресов** щелкните **статических**, а затем введите *192.168.1.101* для **IP-адрес** как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="dc0b6-118">In hello **Network** blade, make sure hello subnet currently selected is *FrontEnd*, then click **IP addresses**, under **IP address assignment** click **Static**, and then enter *192.168.1.101* for **IP Address** as seen below.</span></span>
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. <span data-ttu-id="dc0b6-120">Нажмите кнопку **ОК** в hello **IP-адреса** колонке нажмите кнопку **ОК** в hello **сети** и, при необходимости щелкните **ОК**в hello **необязательная конфигурация** колонку.</span><span class="sxs-lookup"><span data-stu-id="dc0b6-120">Click **OK** in hello **IP addresses** blade, then click **OK** in hello **Network** blade, and click **OK** in hello **Optional config** blade.</span></span>
7. <span data-ttu-id="dc0b6-121">В hello **Создание ВМ** колонка, щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="dc0b6-121">In hello **Create VM** blade, click **Create**.</span></span> <span data-ttu-id="dc0b6-122">Обратите внимание hello Плитка ниже отображаются в панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="dc0b6-122">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="dc0b6-124">Как статических частных IP-tooretrieve адресов сведения для виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="dc0b6-124">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="dc0b6-125">tooview hello статических частных IP-адресе для hello виртуальных Машин, созданных с hello указанную выше процедуру, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="dc0b6-125">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="dc0b6-126">На портале Azure Azure hello, нажмите кнопку **ПРОСМОТРЕТЬ все** > **виртуальные машины (классические)** > **DNS01**  >   **Все параметры** > **IP-адреса** и обратите внимание, hello назначения IP-адресов и IP-адрес, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="dc0b6-126">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines (classic)** > **DNS01** > **All settings** > **IP addresses** and notice hello IP address assignment and IP address as seen below.</span></span>
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="dc0b6-128">Как tooremove статических частных IP-адресов из виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="dc0b6-128">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="dc0b6-129">tooremove hello статический частный IP-адрес из приветствия созданную виртуальную Машину, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="dc0b6-129">tooremove hello static private IP address from hello VM created above, follow hello steps below.</span></span>

1. <span data-ttu-id="dc0b6-130">Из hello **IP-адресов** колонки, показанном выше, нажмите кнопку **динамическое** toohello справа от **назначения IP-адресов**, нажмите кнопку **Сохранить**, а затем Нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="dc0b6-130">From hello **IP addresses** blade shown above, click **Dynamic** toohello right of **IP address assignment**, then click **Save**, and then click **Yes**.</span></span>
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="dc0b6-132">Как tooadd статический частных IP-адрес решения tooan существующей виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="dc0b6-132">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="dc0b6-133">tooadd статические частного IP адрес toohello виртуальной Машины, созданной с помощью hello указанную выше процедуру, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="dc0b6-133">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="dc0b6-134">Из hello **IP-адреса** колонки, показанном выше, нажмите кнопку **статических** toohello справа от **назначения IP-адресов**.</span><span class="sxs-lookup"><span data-stu-id="dc0b6-134">From hello **IP addresses** blade shown above, click **Static** toohello right of **IP address assignment**.</span></span>
2. <span data-ttu-id="dc0b6-135">Введите *192.168.1.101* в поле **IP-адрес**, нажмите кнопку **Сохранить**, а затем — **Да**.</span><span class="sxs-lookup"><span data-stu-id="dc0b6-135">Type *192.168.1.101* for **IP address**, then click **Save**, and then click **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc0b6-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dc0b6-136">Next steps</span></span>
* <span data-ttu-id="dc0b6-137">Ознакомьтесь с информацией о [зарезервированных общедоступных IP-адресах](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="dc0b6-137">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="dc0b6-138">Узнайте об [общедоступных IP-адресах уровня экземпляра (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="dc0b6-138">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="dc0b6-139">Обратитесь к hello [зарезервированные интерфейсы REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc0b6-139">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

