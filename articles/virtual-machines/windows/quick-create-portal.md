---
title: "Краткое руководство по Azure. Создание виртуальной машины Windows с помощью портала | Документация Майкрософт"
description: "Краткое руководство по Azure. Создание виртуальной машины Windows с помощью портала."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 31ac18add9c3fd956e0d37b1e0c1a510265c22e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-windows-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="2faf6-103">Создание виртуальной машины Windows с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="2faf6-103">Create a Windows virtual machine with the Azure portal</span></span>

<span data-ttu-id="2faf6-104">Виртуальные машины Azure можно создать на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2faf6-104">Azure virtual machines can be created through the Azure portal.</span></span> <span data-ttu-id="2faf6-105">В этом случае для создания и настройки виртуальных машин и всех связанных ресурсов Azure используется пользовательский интерфейс на основе браузера.</span><span class="sxs-lookup"><span data-stu-id="2faf6-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="2faf6-106">В этом кратком руководстве содержатся пошаговые инструкции по созданию виртуальной машины и установке веб-сервера на этой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="2faf6-106">This Quickstart steps through creating a virtual machine and installing a webserver on the VM.</span></span>

<span data-ttu-id="2faf6-107">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) , прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="2faf6-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="2faf6-108">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="2faf6-108">Log in to Azure</span></span>

<span data-ttu-id="2faf6-109">Войдите на портал Azure по адресу http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="2faf6-109">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="2faf6-110">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="2faf6-110">Create virtual machine</span></span>

1. <span data-ttu-id="2faf6-111">Щелкните **Создать** в верхнем левом углу портала Azure.</span><span class="sxs-lookup"><span data-stu-id="2faf6-111">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="2faf6-112">Выберите **Вычисления**, а затем — **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="2faf6-112">Select **Compute**, and then select **Windows Server 2016 Datacenter**.</span></span> 

3. <span data-ttu-id="2faf6-113">Введите сведения о виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="2faf6-113">Enter the virtual machine information.</span></span> <span data-ttu-id="2faf6-114">Имя пользователя и пароль понадобятся для входа на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="2faf6-114">The user name and password entered here is used to log in to the virtual machine.</span></span> <span data-ttu-id="2faf6-115">По завершении нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2faf6-115">When complete, click **OK**.</span></span>

    ![Ввод основных сведений о виртуальной машине в колонке портала](./media/quick-create-portal/create-windows-vm-portal-basic-blade.png)  

4. <span data-ttu-id="2faf6-117">Выберите размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2faf6-117">Select a size for the VM.</span></span> <span data-ttu-id="2faf6-118">Чтобы просмотреть дополнительные размеры, выберите **Просмотреть все** или измените фильтр **Supported disk type** (Поддерживаемые типы диска).</span><span class="sxs-lookup"><span data-stu-id="2faf6-118">To see more sizes, select **View all** or change the **Supported disk type** filter.</span></span> 

    ![Снимок экрана, на котором показаны размеры виртуальных машин](./media/quick-create-portal/create-windows-vm-portal-sizes.png)  

5. <span data-ttu-id="2faf6-120">В колонке параметров оставьте значения по умолчанию и нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="2faf6-120">On the settings blade, keep the defaults and click **OK**.</span></span>

6. <span data-ttu-id="2faf6-121">На странице сводки нажмите кнопку **OК**, чтобы начать развертывание виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2faf6-121">On the summary page, click **Ok** to start the virtual machine deployment.</span></span>

7. <span data-ttu-id="2faf6-122">Виртуальная машина будет закреплена на панели мониторинга портала Azure.</span><span class="sxs-lookup"><span data-stu-id="2faf6-122">The VM will be pinned to the Azure portal dashboard.</span></span> <span data-ttu-id="2faf6-123">По завершении развертывания автоматически откроется колонка со сводными сведениями о виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="2faf6-123">Once the deployment has completed, the VM summary blade automatically opens.</span></span>


## <a name="connect-to-virtual-machine"></a><span data-ttu-id="2faf6-124">Подключение к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="2faf6-124">Connect to virtual machine</span></span>

<span data-ttu-id="2faf6-125">Создайте подключение удаленного рабочего стола к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="2faf6-125">Create a remote desktop connection to the virtual machine.</span></span>

1. <span data-ttu-id="2faf6-126">Нажмите кнопку **Подключиться** в свойствах виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2faf6-126">Click the **Connect** button on the virtual machine properties.</span></span> <span data-ttu-id="2faf6-127">Будет создан и скачан файл протокола удаленного рабочего стола (RDP-файл).</span><span class="sxs-lookup"><span data-stu-id="2faf6-127">A Remote Desktop Protocol file (.rdp file) is created and downloaded.</span></span>

    ![Портал 9](./media/quick-create-portal/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="2faf6-129">Чтобы подключиться к виртуальной машине, откройте скачанный RDP-файл.</span><span class="sxs-lookup"><span data-stu-id="2faf6-129">To connect to your VM, open the downloaded RDP file.</span></span> <span data-ttu-id="2faf6-130">При появлении запроса нажмите кнопку **Подключиться**.</span><span class="sxs-lookup"><span data-stu-id="2faf6-130">If prompted, click **Connect**.</span></span> <span data-ttu-id="2faf6-131">На компьютере Mac вам понадобится клиент RDP, например [Remote Desktop Client](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) из Mac App Store.</span><span class="sxs-lookup"><span data-stu-id="2faf6-131">On a Mac, you need an RDP client such as this [Remote Desktop Client](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) from the Mac App Store.</span></span>

3. <span data-ttu-id="2faf6-132">Введите имя пользователя и пароль, указанные при создании виртуальной машины, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2faf6-132">Enter the user name and password you specified when creating the virtual machine, then click **Ok**.</span></span>

4. <span data-ttu-id="2faf6-133">При входе в систему может появиться предупреждение о сертификате.</span><span class="sxs-lookup"><span data-stu-id="2faf6-133">You may receive a certificate warning during the sign-in process.</span></span> <span data-ttu-id="2faf6-134">Чтобы продолжить процесс подключения, нажмите кнопку **Да** или **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="2faf6-134">Click **Yes** or **Continue** to proceed with the connection.</span></span>


## <a name="install-iis-using-powershell"></a><span data-ttu-id="2faf6-135">Установка IIS с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="2faf6-135">Install IIS using PowerShell</span></span>

<span data-ttu-id="2faf6-136">На виртуальной машине запустите сеанс PowerShell и выполните следующую команду, чтобы установить службы IIS.</span><span class="sxs-lookup"><span data-stu-id="2faf6-136">On the virtual machine, start a PowerShell session and run the following command to install IIS.</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="2faf6-137">После этого завершите сеанс RDP и вернитесь на страницу свойств виртуальной машины на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2faf6-137">When done, exit the RDP session and return the VM properties in the Azure portal.</span></span>

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="2faf6-138">Открытие порта 80 для веб-трафика</span><span class="sxs-lookup"><span data-stu-id="2faf6-138">Open port 80 for web traffic</span></span> 

<span data-ttu-id="2faf6-139">Группа безопасности сети (NSG) защищает входящий и исходящий трафик.</span><span class="sxs-lookup"><span data-stu-id="2faf6-139">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="2faf6-140">При создании виртуальной машины на портале Azure правило для входящего трафика создается через порт 3389 для подключений RDP.</span><span class="sxs-lookup"><span data-stu-id="2faf6-140">When a VM is created from the Azure portal, an inbound rule is created on port 3389 for RDP connections.</span></span> <span data-ttu-id="2faf6-141">Так как на этой виртуальной машине размещается веб-сервер, необходимо создать правило NSG для порта 80.</span><span class="sxs-lookup"><span data-stu-id="2faf6-141">Because this VM hosts a webserver, an NSG rule needs to be created for port 80.</span></span>

1. <span data-ttu-id="2faf6-142">На виртуальной машине щелкните имя **группы ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="2faf6-142">On the virtual machine, click the name of the **Resource group**.</span></span>
2. <span data-ttu-id="2faf6-143">Выберите **группу безопасности сети**.</span><span class="sxs-lookup"><span data-stu-id="2faf6-143">Select the **network security group**.</span></span> <span data-ttu-id="2faf6-144">NSG можно определить с помощью столбца **Тип**.</span><span class="sxs-lookup"><span data-stu-id="2faf6-144">The NSG can be identified using the **Type** column.</span></span> 
3. <span data-ttu-id="2faf6-145">В меню слева в разделе параметров щелкните **Правила безопасности для входящего трафика**.</span><span class="sxs-lookup"><span data-stu-id="2faf6-145">On the left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="2faf6-146">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2faf6-146">Click on **Add**.</span></span>
5. <span data-ttu-id="2faf6-147">В поле **Имя** введите **http**.</span><span class="sxs-lookup"><span data-stu-id="2faf6-147">In **Name**, type **http**.</span></span> <span data-ttu-id="2faf6-148">Убедитесь, что для параметра **Диапазон портов** задано значение 80, а для параметра **Действие** — значение **Разрешить**.</span><span class="sxs-lookup"><span data-stu-id="2faf6-148">Make sure **Port range** is set to 80 and **Action** is set to **Allow**.</span></span> 
6. <span data-ttu-id="2faf6-149">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2faf6-149">Click **OK**.</span></span>


## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="2faf6-150">Просмотр страницы приветствия IIS</span><span class="sxs-lookup"><span data-stu-id="2faf6-150">View the IIS welcome page</span></span>

<span data-ttu-id="2faf6-151">Установив службы IIS и открыв порт 80 для виртуальной машины, вы можете получить доступ к веб-серверу через Интернет.</span><span class="sxs-lookup"><span data-stu-id="2faf6-151">With IIS installed, and port 80 open to your VM, the webserver can now be accessed from the internet.</span></span> <span data-ttu-id="2faf6-152">Откройте веб-браузер и введите общедоступный IP-адрес виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2faf6-152">Open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="2faf6-153">Общедоступный IP-адрес можно найти в колонке "Виртуальная машина" на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2faf6-153">the public IP address can be found on the VM blade in the Azure portal.</span></span>

![Сайт IIS по умолчанию](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="2faf6-155">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="2faf6-155">Clean up resources</span></span>

<span data-ttu-id="2faf6-156">Ставшие ненужными группу ресурсов, виртуальную машину и все связанные ресурсы можно удалить, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="2faf6-156">When no longer needed, delete the resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="2faf6-157">Для этого выберите группу ресурсов в колонке виртуальной машины и нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="2faf6-157">To do so, select the resource group from the virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2faf6-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2faf6-158">Next steps</span></span>

<span data-ttu-id="2faf6-159">Из этого краткого руководства вы узнали о том, как развернуть простую виртуальную машину, о правилах группы безопасности сети и об установке веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="2faf6-159">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="2faf6-160">Дополнительные сведения о виртуальных машинах Azure см. в руководстве по работе с виртуальными машинами Windows.</span><span class="sxs-lookup"><span data-stu-id="2faf6-160">To learn more about Azure virtual machines, continue to the tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2faf6-161">Создание виртуальных машин Windows и управление ими с помощью модуля Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2faf6-161">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
