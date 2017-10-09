---
title: "aaaConnect tooa виртуальной машины SQL Server (диспетчер ресурсов) | Документы Microsoft"
description: "Узнайте, как tooconnect tooSQL Server работает на виртуальной машине в Azure. В этом разделе использует hello классической модели развертывания. сценарии Hello отличаться в зависимости от конфигурации сети hello и расположению hello hello клиента."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: 7b127c14c37b9a72c19ed17f8b1dad61c7bc2d38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-resource-manager"></a><span data-ttu-id="b4969-105">Подключение tooa виртуальной машины SQL Server в Azure (диспетчера ресурсов)</span><span class="sxs-lookup"><span data-stu-id="b4969-105">Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b4969-106">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="b4969-106">Resource Manager</span></span>](virtual-machines-windows-sql-connect.md)
> * [<span data-ttu-id="b4969-107">Классический</span><span class="sxs-lookup"><span data-stu-id="b4969-107">Classic</span></span>](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="b4969-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="b4969-108">Overview</span></span>

<span data-ttu-id="b4969-109">В этом разделе описывается, как tooconnect tooyour SQL Server экземпляр запущен на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="b4969-109">This topic describes how tooconnect tooyour SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="b4969-110">Сначала рассматриваются некоторые [общие сценарии подключения](#connection-scenarios), а затем предоставляются [подробные инструкции по настройке подключений SQL Server на виртуальной машине Azure](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="b4969-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="b4969-111">Если вы предпочитаете полное пошаговое руководство по подготовке и подключению, то см. статью [Подготовка виртуальной машины SQL Server на портале Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="b4969-111">If you would rather have a full walk-through of both provisioning and connectivity, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="b4969-112">Сценарии подключения</span><span class="sxs-lookup"><span data-stu-id="b4969-112">Connection scenarios</span></span>

<span data-ttu-id="b4969-113">способ Hello клиент подключается tooSQL сервер, работающий на виртуальной машине отличается в зависимости от расположения hello hello клиента и конфигурации сети hello.</span><span class="sxs-lookup"><span data-stu-id="b4969-113">hello way a client connects tooSQL Server running on a Virtual Machine differs depending on hello location of hello client and hello networking configuration.</span></span>

<span data-ttu-id="b4969-114">Подготовка к работе виртуальную Машину SQL Server в hello портал Azure, у вас есть параметр hello определения типа hello **подключения SQL**.</span><span class="sxs-lookup"><span data-stu-id="b4969-114">If you provision a SQL Server VM in hello Azure portal, you have hello option of specifying hello type of **SQL connectivity**.</span></span>

![Общедоступное подключение SQL во время подготовки](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

<span data-ttu-id="b4969-116">Варианты подключения:</span><span class="sxs-lookup"><span data-stu-id="b4969-116">Your options for connectivity include:</span></span>

| <span data-ttu-id="b4969-117">Параметр</span><span class="sxs-lookup"><span data-stu-id="b4969-117">Option</span></span> | <span data-ttu-id="b4969-118">Описание</span><span class="sxs-lookup"><span data-stu-id="b4969-118">Description</span></span> |
|---|---|
| <span data-ttu-id="b4969-119">**Общедоступное**</span><span class="sxs-lookup"><span data-stu-id="b4969-119">**Public**</span></span> | <span data-ttu-id="b4969-120">Подключение tooSQL сервера через hello Интернета</span><span class="sxs-lookup"><span data-stu-id="b4969-120">Connect tooSQL Server over hello internet</span></span> |
| <span data-ttu-id="b4969-121">**Частное**</span><span class="sxs-lookup"><span data-stu-id="b4969-121">**Private**</span></span> | <span data-ttu-id="b4969-122">Подключение tooSQL сервера в hello одной виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="b4969-122">Connect tooSQL Server in hello same virtual network</span></span> |
| <span data-ttu-id="b4969-123">**Локальное**</span><span class="sxs-lookup"><span data-stu-id="b4969-123">**Local**</span></span> | <span data-ttu-id="b4969-124">Подключение tooSQL Server локально на hello одной виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="b4969-124">Connect tooSQL Server locally on hello same virtual machine</span></span> | 

<span data-ttu-id="b4969-125">Hello ниже разделы содержат определение hello **открытый** и **закрытый** параметры более подробно.</span><span class="sxs-lookup"><span data-stu-id="b4969-125">hello following sections explain hello **Public** and **Private** options in more detail.</span></span>

## <a name="connect-toosql-server-over-hello-internet"></a><span data-ttu-id="b4969-126">Подключение tooSQL сервера через Интернет hello</span><span class="sxs-lookup"><span data-stu-id="b4969-126">Connect tooSQL Server over hello Internet</span></span>

<span data-ttu-id="b4969-127">Tooconnect tooyour SQL Server database engine от hello Интернет, установите **открытый** для hello **подключения SQL** типа hello портала во время инициализации.</span><span class="sxs-lookup"><span data-stu-id="b4969-127">If you want tooconnect tooyour SQL Server database engine from hello Internet, select **Public** for hello **SQL connectivity** type in hello portal during provisioning.</span></span> <span data-ttu-id="b4969-128">Hello портал автоматически hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b4969-128">hello portal automatically does hello following steps:</span></span>

* <span data-ttu-id="b4969-129">Включает hello протокол TCP/IP для SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b4969-129">Enables hello TCP/IP protocol for SQL Server.</span></span>
* <span data-ttu-id="b4969-130">Настраивает hello tooopen правила брандмауэра SQL Server TCP-порт (по умолчанию 1433).</span><span class="sxs-lookup"><span data-stu-id="b4969-130">Configures a firewall rule tooopen hello SQL Server TCP port (default 1433).</span></span>
* <span data-ttu-id="b4969-131">включение аутентификации SQL Server, требуемой для предоставления общего доступа;</span><span class="sxs-lookup"><span data-stu-id="b4969-131">Enables SQL Server Authentication, required for public access.</span></span>
* <span data-ttu-id="b4969-132">Настраивает hello сетевой группы безопасности на hello ВМ tooall TCP-трафика на hello порт SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b4969-132">Configures hello network security group on hello VM tooall TCP traffic on hello SQL Server port.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4969-133">выпуски Express и Hello образы виртуальных машин для SQL Server Developer Привет автоматически не включайте hello TCP/IP-протокол.</span><span class="sxs-lookup"><span data-stu-id="b4969-133">hello virtual machine images for hello SQL Server Developer and Express editions do not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="b4969-134">В выпусках Developer и Express, необходимо использовать диспетчер конфигурации SQL Server слишком[вручную включить протокол hello TCP/IP](#manualtcp) после создания hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b4969-134">For Developer and Express editions, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#manualtcp) after creating hello VM.</span></span>

<span data-ttu-id="b4969-135">Любой клиент с доступом в Интернет может подключаться toohello экземпляр SQL Server, указав hello общедоступный IP-адрес виртуальной машины hello или любую метку DNS toothat IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="b4969-135">Any client with internet access can connect toohello SQL Server instance by specifying either hello public IP address of hello virtual machine or any DNS label assigned toothat IP address.</span></span> <span data-ttu-id="b4969-136">Если hello порт SQL Server — 1433, не обязательно toospecify его в строке подключения hello.</span><span class="sxs-lookup"><span data-stu-id="b4969-136">If hello SQL Server port is 1433, you do not need toospecify it in hello connection string.</span></span> <span data-ttu-id="b4969-137">Привет, следующая строка подключения подключается tooa виртуальной Машине SQL с именем DNS из `sqlvmlabel.eastus.cloudapp.azure.com` с использованием проверки подлинности SQL (можно также использовать hello общедоступный IP-адрес).</span><span class="sxs-lookup"><span data-stu-id="b4969-137">hello following connection string connects tooa SQL VM with a DNS label of `sqlvmlabel.eastus.cloudapp.azure.com` using SQL Authentication (you could also use hello public IP address).</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

<span data-ttu-id="b4969-138">Несмотря на то, что это позволяет подключения клиентов через Интернет Здравствуйте, это не означает, что любой пользователь может подключиться tooyour SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b4969-138">Although this enables connectivity for clients over hello internet, this does not imply that anyone can connect tooyour SQL Server.</span></span> <span data-ttu-id="b4969-139">Внешним клиентам иметь toohello правильное имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="b4969-139">Outside clients have toohello correct username and password.</span></span> <span data-ttu-id="b4969-140">Тем не менее для обеспечения дополнительной безопасности можно избежать hello известный порт 1433.</span><span class="sxs-lookup"><span data-stu-id="b4969-140">However, for additional security, you can avoid hello well-known port 1433.</span></span> <span data-ttu-id="b4969-141">Например если вы настроили toolisten SQL Server для порта 1500 и установленное правильную брандмауэра и правил группы безопасности сети, удалось подключиться путем добавления имени сервера номеров toohello hello порта.</span><span class="sxs-lookup"><span data-stu-id="b4969-141">For example, if you configured SQL Server toolisten on port 1500 and established proper firewall and network security group rules, you could connect by appending hello port number toohello Server name.</span></span> <span data-ttu-id="b4969-142">Hello следующий пример изменяет предыдущий hello, добавив собственный номер порта, **1500**, toohello имя сервера:</span><span class="sxs-lookup"><span data-stu-id="b4969-142">hello following example alters hello previous one by adding a custom port number, **1500**, toohello server name:</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> <span data-ttu-id="b4969-143">При выполнении запроса SQL Server на виртуальной машине через hello Интернета, все данные, исходящие из hello Azure центра обработки данных — тема toonormal [Ценообразование на исходящую передачу данных](https://azure.microsoft.com/pricing/details/data-transfers/).</span><span class="sxs-lookup"><span data-stu-id="b4969-143">When you query SQL Server in a VM over hello internet, all outgoing data from hello Azure datacenter is subject toonormal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).</span></span>

## <a name="connect-toosql-server-within-a-virtual-network"></a><span data-ttu-id="b4969-144">Подключение tooSQL Server в виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="b4969-144">Connect tooSQL Server within a virtual network</span></span>

<span data-ttu-id="b4969-145">При выборе **закрытый** для hello **подключения SQL** типа hello портала Azure настраивает большая часть параметров hello идентичные слишком**открытый**.</span><span class="sxs-lookup"><span data-stu-id="b4969-145">When you choose **Private** for hello **SQL connectivity** type in hello portal, Azure configures most of hello settings identical too**Public**.</span></span> <span data-ttu-id="b4969-146">Единственным отличием Hello является не tooallow сетевой безопасности группы правил за пределами трафик через порт SQL Server hello (по умолчанию 1433).</span><span class="sxs-lookup"><span data-stu-id="b4969-146">hello one difference is that there is no network security group rule tooallow outside traffic on hello SQL Server port (default 1433).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4969-147">выпуски Express и Hello образы виртуальных машин для SQL Server Developer Привет автоматически не включайте hello TCP/IP-протокол.</span><span class="sxs-lookup"><span data-stu-id="b4969-147">hello virtual machine images for hello SQL Server Developer and Express editions do not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="b4969-148">В выпусках Developer и Express, необходимо использовать диспетчер конфигурации SQL Server слишком[вручную включить протокол hello TCP/IP](#manualtcp) после создания hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b4969-148">For Developer and Express editions, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#manualtcp) after creating hello VM.</span></span>

<span data-ttu-id="b4969-149">Частное подключение часто используется в сочетании с [виртуальной сетью](../../../virtual-network/virtual-networks-overview.md), что позволяет реализовать несколько сценариев.</span><span class="sxs-lookup"><span data-stu-id="b4969-149">Private connectivity is often used in conjunction with [Virtual Network](../../../virtual-network/virtual-networks-overview.md), which enables several scenarios.</span></span> <span data-ttu-id="b4969-150">Можно подключить виртуальные машины в одной виртуальной сети, даже если эти виртуальные машины существует в разных группах ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="b4969-150">You can connect VMs in hello same virtual network, even if those VMs exist in different resource groups.</span></span> <span data-ttu-id="b4969-151">Если используется [VPN типа «сеть-сеть»](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), можно создать гибридную архитектуру, обеспечивающую подключение виртуальных машин к локальным сетям и компьютерам.</span><span class="sxs-lookup"><span data-stu-id="b4969-151">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="b4969-152">Виртуальные сети включите вы toojoin домена tooa виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="b4969-152">Virtual networks also enable     you toojoin your Azure VMs tooa domain.</span></span> <span data-ttu-id="b4969-153">Это hello единственным способом toouse проверку подлинности Windows tooSQL сервера.</span><span class="sxs-lookup"><span data-stu-id="b4969-153">This is hello only way toouse Windows Authentication tooSQL Server.</span></span> <span data-ttu-id="b4969-154">Hello другие варианты подключения требуется проверка подлинности SQL с именами пользователей и пароли.</span><span class="sxs-lookup"><span data-stu-id="b4969-154">hello other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="b4969-155">Предположим, что вы настроили DNS в виртуальной сети, можно подключиться tooyour экземпляр SQL Server, указав имя компьютера виртуальной Машины SQL Server hello в строке подключения hello.</span><span class="sxs-lookup"><span data-stu-id="b4969-155">Assuming that you have configured DNS in your virtual network, you can connect tooyour SQL Server instance by specifying hello SQL Server VM computer name in hello connection string.</span></span> <span data-ttu-id="b4969-156">Следующий пример также Hello предполагается, что также настроена проверка подлинности Windows и предоставлены пользователю, hello, экземпляр SQL Server toohello доступа.</span><span class="sxs-lookup"><span data-stu-id="b4969-156">hello following example also assumes that Windows Authentication has also been configured and that hello user has been granted access toohello SQL Server instance.</span></span>

```
Server=mysqlvm;Integrated Security=true
```

## <span data-ttu-id="b4969-157"><a id="change"></a> Изменение параметров подключения к SQL</span><span class="sxs-lookup"><span data-stu-id="b4969-157"><a id="change"></a> Change SQL connectivity settings</span></span>

<span data-ttu-id="b4969-158">Можно изменить параметры подключения к hello для виртуальной машины SQL Server в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b4969-158">You can change hello connectivity settings for your SQL Server virtual machine in hello Azure portal.</span></span>

1. <span data-ttu-id="b4969-159">В hello портал Azure, выберите **виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="b4969-159">In hello Azure portal, select **Virtual Machines**.</span></span>

2. <span data-ttu-id="b4969-160">Выберите виртуальную машину SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b4969-160">Select your SQL Server VM.</span></span>

3. <span data-ttu-id="b4969-161">В разделе **Параметры** щелкните **Конфигурация SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="b4969-161">Under **Settings**, click **SQL Server configuration**.</span></span>

4. <span data-ttu-id="b4969-162">Изменение hello **уровня подключения SQL** tooyour требуется настройка.</span><span class="sxs-lookup"><span data-stu-id="b4969-162">Change hello **SQL connectivity level** tooyour required setting.</span></span> <span data-ttu-id="b4969-163">При необходимости можно использовать этот hello toochange области порт SQL Server или параметры проверки подлинности SQL hello.</span><span class="sxs-lookup"><span data-stu-id="b4969-163">You can optionally use this area toochange hello SQL Server port or hello SQL Authentication settings.</span></span>

   ![Изменение параметров подключения к SQL](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. <span data-ttu-id="b4969-165">Подождите несколько минут для обновления toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="b4969-165">Wait several minutes for hello update toocomplete.</span></span>

   ![Уведомление об обновлении виртуальной машины SQL](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <span data-ttu-id="b4969-167"><a id="manualtcp"></a> Включение TCP/IP для выпусков Developer и Express</span><span class="sxs-lookup"><span data-stu-id="b4969-167"><a id="manualtcp"></a> Enable TCP/IP for Developer and Express editions</span></span>

<span data-ttu-id="b4969-168">При изменении параметров подключения к SQL Server, Azure не происходит автоматического включения hello TCP/IP-протокола для разработчиков SQL Server и выпусках Express.</span><span class="sxs-lookup"><span data-stu-id="b4969-168">When changing SQL Server connectivity settings, Azure does not automatically enable hello TCP/IP protocol for SQL Server Developer and Express editions.</span></span> <span data-ttu-id="b4969-169">описанные действия Hello, как включить toomanually TCP/IP, чтобы удаленно подключиться по IP-адресу.</span><span class="sxs-lookup"><span data-stu-id="b4969-169">hello steps below explain how toomanually enable TCP/IP so that you can connect remotely by IP address.</span></span>

<span data-ttu-id="b4969-170">Сначала подключите toohello машины SQL Server с помощью удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="b4969-170">First, connect toohello SQL Server machine with remote desktop.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

<span data-ttu-id="b4969-171">Затем включите протокол hello TCP/IP с **диспетчер конфигурации SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="b4969-171">Next, enable hello TCP/IP protocol with **SQL Server Configuration Manager**.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a><span data-ttu-id="b4969-172">Подключение с помощью SSMS</span><span class="sxs-lookup"><span data-stu-id="b4969-172">Connect with SSMS</span></span>

<span data-ttu-id="b4969-173">Hello следующее Показать, как toocreate необязательно DNS метка для ВМ Azure и подключитесь с помощью SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="b4969-173">hello following steps show how toocreate an optional DNS Label for your Azure VM and then connect with SQL Server Management Studio (SSMS).</span></span>

[!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="b4969-174">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b4969-174">Next Steps</span></span>

<span data-ttu-id="b4969-175">инструкции подготовки toosee вместе с следующее подключение. в разделе [подготовки виртуальной машины SQL Server в Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="b4969-175">toosee provisioning instructions along with these connectivity steps, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

<span data-ttu-id="b4969-176">Другие разделы, посвященные toorunning SQL Server в виртуальных машинах Azure, см. в разделе [SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b4969-176">For other topics related toorunning SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
