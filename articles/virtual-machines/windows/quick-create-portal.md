---
title: "Быстрый запуск - aaaAzure создания портала ВМ Windows | Документы Microsoft"
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
ms.openlocfilehash: 5646ad51244db6d214c0121d1f7cc45c59f9a78b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="aa846-103">Создание виртуальной машины Windows с hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="aa846-103">Create a Windows virtual machine with hello Azure portal</span></span>

<span data-ttu-id="aa846-104">Виртуальные машины Azure могут создаваться через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="aa846-104">Azure virtual machines can be created through hello Azure portal.</span></span> <span data-ttu-id="aa846-105">В этом случае для создания и настройки виртуальных машин и всех связанных ресурсов Azure используется пользовательский интерфейс на основе браузера.</span><span class="sxs-lookup"><span data-stu-id="aa846-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="aa846-106">Это краткое руководство пошаговые инструкции для создания виртуальной машины и установка веб-сервере, на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="aa846-106">This Quickstart steps through creating a virtual machine and installing a webserver on hello VM.</span></span>

<span data-ttu-id="aa846-107">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="aa846-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="aa846-108">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="aa846-108">Log in tooAzure</span></span>

<span data-ttu-id="aa846-109">Войдите в систему toohello портал Azure по адресу http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="aa846-109">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="aa846-110">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="aa846-110">Create virtual machine</span></span>

1. <span data-ttu-id="aa846-111">Нажмите кнопку hello **New** кнопка найдена в верхнем левом углу hello hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="aa846-111">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="aa846-112">Выберите **Вычисления**, а затем — **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="aa846-112">Select **Compute**, and then select **Windows Server 2016 Datacenter**.</span></span> 

3. <span data-ttu-id="aa846-113">Введите сведения о виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="aa846-113">Enter hello virtual machine information.</span></span> <span data-ttu-id="aa846-114">Hello имя пользователя и пароль, введенный здесь — используется toolog toohello виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="aa846-114">hello user name and password entered here is used toolog in toohello virtual machine.</span></span> <span data-ttu-id="aa846-115">По завершении нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="aa846-115">When complete, click **OK**.</span></span>

    ![Ввести основные сведения о ВМ в колонке портала hello](./media/quick-create-portal/create-windows-vm-portal-basic-blade.png)  

4. <span data-ttu-id="aa846-117">Выберите размер виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="aa846-117">Select a size for hello VM.</span></span> <span data-ttu-id="aa846-118">Выберите дополнительные размеры toosee **просмотреть все** или изменить hello **поддерживается тип диска** фильтра.</span><span class="sxs-lookup"><span data-stu-id="aa846-118">toosee more sizes, select **View all** or change hello **Supported disk type** filter.</span></span> 

    ![Снимок экрана, на котором показаны размеры виртуальных машин](./media/quick-create-portal/create-windows-vm-portal-sizes.png)  

5. <span data-ttu-id="aa846-120">В колонке параметров hello, оставьте значения по умолчанию hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="aa846-120">On hello settings blade, keep hello defaults and click **OK**.</span></span>

6. <span data-ttu-id="aa846-121">На странице сводки hello щелкните **ОК** развертывания виртуальной машины toostart hello.</span><span class="sxs-lookup"><span data-stu-id="aa846-121">On hello summary page, click **Ok** toostart hello virtual machine deployment.</span></span>

7. <span data-ttu-id="aa846-122">Hello виртуальной Машины будет закрепленных toohello Azure панели мониторинга портала.</span><span class="sxs-lookup"><span data-stu-id="aa846-122">hello VM will be pinned toohello Azure portal dashboard.</span></span> <span data-ttu-id="aa846-123">После завершения развертывания hello, автоматически откроется Сводка колонки hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="aa846-123">Once hello deployment has completed, hello VM summary blade automatically opens.</span></span>


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="aa846-124">Подключиться к компьютеру toovirtual</span><span class="sxs-lookup"><span data-stu-id="aa846-124">Connect toovirtual machine</span></span>

<span data-ttu-id="aa846-125">Создание виртуальной машины toohello подключения удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="aa846-125">Create a remote desktop connection toohello virtual machine.</span></span>

1. <span data-ttu-id="aa846-126">Нажмите кнопку hello **Connect** кнопку на hello свойства виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="aa846-126">Click hello **Connect** button on hello virtual machine properties.</span></span> <span data-ttu-id="aa846-127">Будет создан и скачан файл протокола удаленного рабочего стола (RDP-файл).</span><span class="sxs-lookup"><span data-stu-id="aa846-127">A Remote Desktop Protocol file (.rdp file) is created and downloaded.</span></span>

    ![Портал 9](./media/quick-create-portal/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="aa846-129">tooconnect tooyour виртуальной Машины, откройте hello загрузить RDP-файл.</span><span class="sxs-lookup"><span data-stu-id="aa846-129">tooconnect tooyour VM, open hello downloaded RDP file.</span></span> <span data-ttu-id="aa846-130">При появлении запроса нажмите кнопку **Подключиться**.</span><span class="sxs-lookup"><span data-stu-id="aa846-130">If prompted, click **Connect**.</span></span> <span data-ttu-id="aa846-131">На компьютере Mac, необходимо клиентом RDP, такие как это [клиент удаленного рабочего стола](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) из hello Mac App Store.</span><span class="sxs-lookup"><span data-stu-id="aa846-131">On a Mac, you need an RDP client such as this [Remote Desktop Client](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) from hello Mac App Store.</span></span>

3. <span data-ttu-id="aa846-132">Введите hello имя пользователя и пароль, указанный при создании hello виртуальную машину, затем щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="aa846-132">Enter hello user name and password you specified when creating hello virtual machine, then click **Ok**.</span></span>

4. <span data-ttu-id="aa846-133">Может появиться предупреждение сертификата во время процесса входа hello.</span><span class="sxs-lookup"><span data-stu-id="aa846-133">You may receive a certificate warning during hello sign-in process.</span></span> <span data-ttu-id="aa846-134">Нажмите кнопку **Да** или **Продолжить** tooproceed с подключением hello.</span><span class="sxs-lookup"><span data-stu-id="aa846-134">Click **Yes** or **Continue** tooproceed with hello connection.</span></span>


## <a name="install-iis-using-powershell"></a><span data-ttu-id="aa846-135">Установка IIS с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa846-135">Install IIS using PowerShell</span></span>

<span data-ttu-id="aa846-136">На виртуальной машине hello запустите сеанс PowerShell и выполните hello, следующая команда tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="aa846-136">On hello virtual machine, start a PowerShell session and run hello following command tooinstall IIS.</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="aa846-137">После этого завершите сеанс RDP hello и возвращает свойства виртуальной Машины hello hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="aa846-137">When done, exit hello RDP session and return hello VM properties in hello Azure portal.</span></span>

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="aa846-138">Открытие порта 80 для веб-трафика</span><span class="sxs-lookup"><span data-stu-id="aa846-138">Open port 80 for web traffic</span></span> 

<span data-ttu-id="aa846-139">Группа безопасности сети (NSG) защищает входящий и исходящий трафик.</span><span class="sxs-lookup"><span data-stu-id="aa846-139">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="aa846-140">При создании виртуальной Машины из портала Azure hello входящее правило создается на порт 3389 для подключений по протоколу RDP.</span><span class="sxs-lookup"><span data-stu-id="aa846-140">When a VM is created from hello Azure portal, an inbound rule is created on port 3389 for RDP connections.</span></span> <span data-ttu-id="aa846-141">Поскольку эта виртуальная машина размещается веб-сервере, правило NSG должен toobe, созданное для порта 80.</span><span class="sxs-lookup"><span data-stu-id="aa846-141">Because this VM hosts a webserver, an NSG rule needs toobe created for port 80.</span></span>

1. <span data-ttu-id="aa846-142">На виртуальной машине hello, щелкните имя hello hello **группы ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="aa846-142">On hello virtual machine, click hello name of hello **Resource group**.</span></span>
2. <span data-ttu-id="aa846-143">Выберите hello **сетевой группы безопасности**.</span><span class="sxs-lookup"><span data-stu-id="aa846-143">Select hello **network security group**.</span></span> <span data-ttu-id="aa846-144">Hello NSG можно определить с помощью hello **тип** столбца.</span><span class="sxs-lookup"><span data-stu-id="aa846-144">hello NSG can be identified using hello **Type** column.</span></span> 
3. <span data-ttu-id="aa846-145">Hello слева в разделе Параметры меню **безопасности правила для входящих подключений**.</span><span class="sxs-lookup"><span data-stu-id="aa846-145">On hello left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="aa846-146">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="aa846-146">Click on **Add**.</span></span>
5. <span data-ttu-id="aa846-147">В поле **Имя** введите **http**.</span><span class="sxs-lookup"><span data-stu-id="aa846-147">In **Name**, type **http**.</span></span> <span data-ttu-id="aa846-148">Убедитесь, что **диапазон портов** задано too80 и **действия** задано слишком**Разрешить**.</span><span class="sxs-lookup"><span data-stu-id="aa846-148">Make sure **Port range** is set too80 and **Action** is set too**Allow**.</span></span> 
6. <span data-ttu-id="aa846-149">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="aa846-149">Click **OK**.</span></span>


## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="aa846-150">Представление hello страницу приветствия IIS</span><span class="sxs-lookup"><span data-stu-id="aa846-150">View hello IIS welcome page</span></span>

<span data-ttu-id="aa846-151">Со службами IIS установлены и порт 80 откройте tooyour виртуальных Машин, веб-сервер hello, теперь доступны из hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="aa846-151">With IIS installed, and port 80 open tooyour VM, hello webserver can now be accessed from hello internet.</span></span> <span data-ttu-id="aa846-152">Откройте веб-браузер и введите hello общедоступный IP-адрес hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="aa846-152">Open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="aa846-153">Hello общедоступный IP-адрес можно найти на колонки виртуальной Машины hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="aa846-153">hello public IP address can be found on hello VM blade in hello Azure portal.</span></span>

![Сайт IIS по умолчанию](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="aa846-155">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="aa846-155">Clean up resources</span></span>

<span data-ttu-id="aa846-156">Когда больше не нужен, удалите hello группы ресурсов, виртуальные машины и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="aa846-156">When no longer needed, delete hello resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="aa846-157">toodo таким образом, выберите группу ресурсов hello hello колонке виртуальной машины и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="aa846-157">toodo so, select hello resource group from hello virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa846-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aa846-158">Next steps</span></span>

<span data-ttu-id="aa846-159">Из этого краткого руководства вы узнали о том, как развернуть простую виртуальную машину, о правилах группы безопасности сети и об установке веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="aa846-159">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="aa846-160">toolearn Дополнительные сведения о виртуальных машинах Azure, продолжить toohello учебника для виртуальных машин Windows.</span><span class="sxs-lookup"><span data-stu-id="aa846-160">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aa846-161">Создание виртуальных машин Windows и управление ими с помощью модуля Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa846-161">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
