---
title: "Установка IIS на вашу первую виртуальную машину Windows | Документация Майкрософт"
description: "Поэкспериментируйте со своей первой виртуальной машиной Windows, установив на нее IIS и открыв порт 80 с помощью портала Azure."
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6334ea45-db6b-4e08-abb5-1f98927ebc34
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cynthn
ms.openlocfilehash: b11ce1eab0c26a802c31bc418cdf725cbc4fba30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a><span data-ttu-id="43ef0-103">Эксперимент с установкой роли на виртуальной машине Windows</span><span class="sxs-lookup"><span data-stu-id="43ef0-103">Experiment with installing a role on your Windows VM</span></span>
<span data-ttu-id="43ef0-104">После создания и запуска своей первой виртуальной машины можно перейти к установке программного обеспечения и служб.</span><span class="sxs-lookup"><span data-stu-id="43ef0-104">Once you have your first virtual machine (VM) up and running, you can move on to installing software and services.</span></span> <span data-ttu-id="43ef0-105">В этом учебнике мы установим службы IIS на виртуальную машину Windows Server с помощью диспетчера сервера.</span><span class="sxs-lookup"><span data-stu-id="43ef0-105">For this tutorial, we are going to use Server Manager on the Windows Server VM to install IIS.</span></span> <span data-ttu-id="43ef0-106">Затем мы создадим группу безопасности сети с помощью портала Azure, чтобы открыть порт 80 для трафика IIS.</span><span class="sxs-lookup"><span data-stu-id="43ef0-106">Then, we will create a Network Security Group (NSG) using the Azure portal to open port 80 to IIS traffic.</span></span> 

<span data-ttu-id="43ef0-107">Если вы еще не создали свою первую виртуальную машину, то вам следует вернуться к разделу [Создание первой виртуальной машины Windows на портале Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), прежде чем продолжить работу с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="43ef0-107">If you haven't already created your first VM, you should go back to [Create your first Windows virtual machine in the Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before continuing with this tutorial.</span></span>

## <a name="make-sure-the-vm-is-running"></a><span data-ttu-id="43ef0-108">Проверка состояния виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="43ef0-108">Make sure the VM is running</span></span>
1. <span data-ttu-id="43ef0-109">Откройте [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="43ef0-109">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="43ef0-110">В главном меню щелкните **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-110">On the hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="43ef0-111">Затем выберите виртуальную машину из списка.</span><span class="sxs-lookup"><span data-stu-id="43ef0-111">Select the virtual machine from the list.</span></span>
3. <span data-ttu-id="43ef0-112">Если состояние — **Остановлена (освобождена)**, то нажмите кнопку **Запустить** в колонке **Основные компоненты** виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="43ef0-112">If the status is **Stopped (Deallocated)**, click the **Start** button on the **Essentials** blade of the VM.</span></span> <span data-ttu-id="43ef0-113">Если состояние — **Работает**, то можно перейти к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="43ef0-113">If the status is **Running**, you can move on to the next step.</span></span>

## <a name="connect-to-the-virtual-machine-and-sign-in"></a><span data-ttu-id="43ef0-114">Подключение к виртуальной машине и вход в нее</span><span class="sxs-lookup"><span data-stu-id="43ef0-114">Connect to the virtual machine and sign in</span></span>
1. <span data-ttu-id="43ef0-115">В главном меню щелкните **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-115">On the hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="43ef0-116">Затем выберите виртуальную машину из списка.</span><span class="sxs-lookup"><span data-stu-id="43ef0-116">Select the virtual machine from the list.</span></span>
2. <span data-ttu-id="43ef0-117">В колонке виртуальной машины щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-117">On the blade for the virtual machine, click **Connect**.</span></span> <span data-ttu-id="43ef0-118">В результате этого будет создан и скачан RDP-файл в виде ярлыка, с помощью которого можно подключиться к компьютеру.</span><span class="sxs-lookup"><span data-stu-id="43ef0-118">This creates and downloads a Remote Desktop Protocol file (.rdp file) that is like a shortcut to connect to your machine.</span></span> <span data-ttu-id="43ef0-119">Этот файл можно сохранить на рабочем столе для быстрого доступа.</span><span class="sxs-lookup"><span data-stu-id="43ef0-119">You might want to save the file to your desktop for easy access.</span></span> <span data-ttu-id="43ef0-120">**Откройте** этот файл, чтобы подключиться к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="43ef0-120">**Open** this file to connect to your VM.</span></span>
   
    ![Снимок экрана портала Azure: подключение к виртуальной машине](./media/hero-role/connect.png)
3. <span data-ttu-id="43ef0-122">Появится предупреждение, что издатель RDP-файла неизвестен.</span><span class="sxs-lookup"><span data-stu-id="43ef0-122">You get a warning that the .rdp is from an unknown publisher.</span></span> <span data-ttu-id="43ef0-123">Это нормально.</span><span class="sxs-lookup"><span data-stu-id="43ef0-123">This is normal.</span></span> <span data-ttu-id="43ef0-124">Чтобы продолжить, в окне удаленного рабочего стола нажмите кнопку **Подключить** .</span><span class="sxs-lookup"><span data-stu-id="43ef0-124">In the Remote Desktop window, click **Connect** to continue.</span></span>
   
    ![Снимок экрана с предупреждением о неизвестном издателе](./media/hero-role/rdp-warn.png)
4. <span data-ttu-id="43ef0-126">В окне "Безопасность Windows" введите имя пользователя и пароль локальной учетной записи, созданной при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="43ef0-126">In the Windows Security window, type the username and password for the local account that you created when you created the VM.</span></span> <span data-ttu-id="43ef0-127">Введите имя пользователя в формате *имя_ВМ*&#92;*имя_пользователя*, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-127">The username is entered as *vmname*&#92;*username*, then click **OK**.</span></span>
   
    ![Снимок экрана: ввод имени виртуальной машины, имени пользователя и пароля](./media/hero-role/credentials.png)
5. <span data-ttu-id="43ef0-129">Вы получите предупреждение о том, что сертификат невозможно проверить.</span><span class="sxs-lookup"><span data-stu-id="43ef0-129">You get a warning that the certificate cannot be verified.</span></span> <span data-ttu-id="43ef0-130">Это нормально.</span><span class="sxs-lookup"><span data-stu-id="43ef0-130">This is normal.</span></span> <span data-ttu-id="43ef0-131">Щелкните **Да** для проверки удостоверения виртуальной машины и завершения входа в систему.</span><span class="sxs-lookup"><span data-stu-id="43ef0-131">Click **Yes** to verify the identity of the virtual machine and finish logging on.</span></span>
   
   ![Снимок экрана с сообщением о проверке удостоверения виртуальной машины](./media/hero-role/cert-warning.png)

<span data-ttu-id="43ef0-133">Если при попытке подключения возникает ошибка, см. статью [Устранение неполадок с подключением к удаленному рабочему столу на виртуальной машине Azure под управлением Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="43ef0-133">If you run in to trouble when you try to connect, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="install-iis-on-your-vm"></a><span data-ttu-id="43ef0-134">Установка служб IIS на виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="43ef0-134">Install IIS on your VM</span></span>
<span data-ttu-id="43ef0-135">Войдя на виртуальную машину, мы в порядке эксперимента установим роль сервера.</span><span class="sxs-lookup"><span data-stu-id="43ef0-135">Now that you are logged in to the VM, we will install a server role so that you can experiment more.</span></span>

1. <span data-ttu-id="43ef0-136">Откройте **диспетчер серверов** , если он еще не открыт.</span><span class="sxs-lookup"><span data-stu-id="43ef0-136">Open **Server Manager** if it isn't already open.</span></span> <span data-ttu-id="43ef0-137">Откройте меню **Пуск** и выберите **Диспетчер сервера**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-137">Click the **Start** menu, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="43ef0-138">В окне **Диспетчере сервера** выберите **Локальный сервер** в области слева.</span><span class="sxs-lookup"><span data-stu-id="43ef0-138">In **Server Manager**, select **Local Server** from the left pane.</span></span> 
3. <span data-ttu-id="43ef0-139">В меню выберите **Управление** > **Добавить роли и компоненты**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-139">In the menu, select **Manage** > **Add Roles and Features**.</span></span>
4. <span data-ttu-id="43ef0-140">В мастере добавления ролей и компонентов на странице выбора **типа установки** щелкните **Установка ролей или компонентов** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-140">In the Add Roles and Features Wizard, on the **Installation Type** page, choose **Role-based or feature-based installation**, and then click **Next**.</span></span>
   
    ![Снимок экрана: вкладка "Тип установки" в мастере добавления ролей и компонентов](./media/hero-role/role-wizard.png)
5. <span data-ttu-id="43ef0-142">Выберите виртуальную машину в пуле серверов и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-142">Select the VM from the server pool and click **Next**.</span></span>
6. <span data-ttu-id="43ef0-143">На странице **Роли сервера** выберите **Веб-сервер (IIS)**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-143">On the **Server Roles** page, select **Web Server (IIS)**.</span></span>
   
    ![Снимок экрана: вкладка "Роли сервера" в мастере добавления ролей и компонентов](./media/hero-role/add-iis.png)
7. <span data-ttu-id="43ef0-145">Во всплывающем окне добавления компонентов, необходимых для IIS, установите флажок **Включить средства управления**, а затем щелкните **Добавить компоненты**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-145">In the pop-up about adding features needed for IIS, make sure that **Include management tools** is selected and then click **Add Features**.</span></span> <span data-ttu-id="43ef0-146">Закрыв всплывающее окно, нажмите кнопку **Далее** в мастере.</span><span class="sxs-lookup"><span data-stu-id="43ef0-146">When the pop-up closes, click **Next** in the wizard.</span></span>
   
    ![Снимок экрана: всплывающее окно для подтверждения добавления роли IIS](./media/hero-role/confirm-add-feature.png)
8. <span data-ttu-id="43ef0-148">На странице компонентов щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-148">On the features page, click **Next**.</span></span>
9. <span data-ttu-id="43ef0-149">На странице **Роль веб-сервера (IIS)** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-149">On the **Web Server Role (IIS)** page, click **Next**.</span></span> 
10. <span data-ttu-id="43ef0-150">На странице **Службы ролей** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-150">On the **Role Services** page, click **Next**.</span></span> 
11. <span data-ttu-id="43ef0-151">На странице **подтверждения** нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-151">On the **Confirmation** page, click **Install**.</span></span> 
12. <span data-ttu-id="43ef0-152">После завершения установки нажмите кнопку **Закрыть** в мастере.</span><span class="sxs-lookup"><span data-stu-id="43ef0-152">When the installation is complete, click **Close** on the wizard.</span></span>

## <a name="open-port-80"></a><span data-ttu-id="43ef0-153">Открытие порта 80</span><span class="sxs-lookup"><span data-stu-id="43ef0-153">Open port 80</span></span>
<span data-ttu-id="43ef0-154">Чтобы виртуальная машина могла принимать входящий трафик через порт 80, в группу безопасности сети необходимо добавить правило для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="43ef0-154">In order for your VM to accept inbound traffic over port 80, you need to add an inbound rule to the network security group.</span></span> 

1. <span data-ttu-id="43ef0-155">Откройте [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="43ef0-155">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="43ef0-156">В разделе **Виртуальные машины** выберите созданную виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="43ef0-156">In **Virtual machines** select the VM that you created.</span></span>
3. <span data-ttu-id="43ef0-157">В разделе параметров виртуальных машин выберите **Сетевые интерфейсы** , а затем выберите существующий сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="43ef0-157">In the virtual machines settings, select **Network interfaces** and then select the existing network interface.</span></span>
   
    ![Снимок экрана: настройка виртуальной машины для сетевых интерфейсов](./media/hero-role/network-interface.png)
4. <span data-ttu-id="43ef0-159">В разделе **Основные компоненты** для сетевого интерфейса щелкните **Группа безопасности сети**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-159">In **Essentials** for the network interface, click the **Network security group**.</span></span>
   
    ![Снимок экрана: раздел "Основные компоненты" для сетевых интерфейсов](./media/hero-role/select-nsg.png)
5. <span data-ttu-id="43ef0-161">В колонке **Основные компоненты** для группы безопасности сети должно быть указано одно существующее правило по умолчанию для входящего трафика **default-allow-rdp**, разрешающее вход на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="43ef0-161">In the **Essentials** blade for the NSG, you should have one existing default inbound rule for **default-allow-rdp** which allows you to log in to the VM.</span></span> <span data-ttu-id="43ef0-162">Добавьте еще одно правило для входящего трафика, разрешающее трафик IIS.</span><span class="sxs-lookup"><span data-stu-id="43ef0-162">You will add another inbound rule to allow IIS traffic.</span></span> <span data-ttu-id="43ef0-163">Щелкните **Правило безопасности для входящего трафика**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-163">Click **Inbound security rule**.</span></span>
   
    ![Снимок экрана: раздел "Основные компоненты" для группы безопасности сети](./media/hero-role/inbound.png)
6. <span data-ttu-id="43ef0-165">В разделе **Правила безопасности для входящего трафика** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-165">In **Inbound security rules**, click **Add**.</span></span>
   
    ![Снимок экрана: кнопка для добавления правила безопасности](./media/hero-role/add-rule.png)
7. <span data-ttu-id="43ef0-167">В разделе **Правила безопасности для входящего трафика** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-167">In **Inbound security rules**, click **Add**.</span></span> <span data-ttu-id="43ef0-168">Введите **80** для диапазона портов и убедитесь, что установлен переключатель **Разрешить**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-168">Type **80** in the port range and make sure **Allow** is selected.</span></span> <span data-ttu-id="43ef0-169">Когда все будет готово, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-169">When you are done, click **OK**.</span></span>
   
    ![Снимок экрана: кнопка для добавления правила безопасности](./media/hero-role/port-80.png)

<span data-ttu-id="43ef0-171">Дополнительные сведения о группах безопасности сети, а также о правилах для входящего и исходящего трафика см. в статье [Открытие портов для виртуальной машины в Azure с помощью портала Azure](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="43ef0-171">For more information about NSGs, inbound and outbound rules, see [Allow external access to your VM using the Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="connect-to-the-default-iis-website"></a><span data-ttu-id="43ef0-172">Подключение к веб-сайту IIS по умолчанию</span><span class="sxs-lookup"><span data-stu-id="43ef0-172">Connect to the default IIS website</span></span>
1. <span data-ttu-id="43ef0-173">На портале Azure щелкните **Виртуальные машины** и выберите нужную виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="43ef0-173">In the Azure portal, click **Virtual machines** and then select your VM.</span></span>
2. <span data-ttu-id="43ef0-174">В колонке **Основные компоненты** скопируйте **общедоступный IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="43ef0-174">In the **Essentials** blade, copy your **Public IP address**.</span></span>
   
    ![Снимок экрана: расположение общедоступного IP-адреса виртуальной машины](./media/hero-role/ipaddress.png)
3. <span data-ttu-id="43ef0-176">Откройте браузер, введите в адресную строку общедоступный IP-адрес в формате http://<publicIPaddress> и нажмите клавишу **ВВОД**, чтобы перейти по этому адресу.</span><span class="sxs-lookup"><span data-stu-id="43ef0-176">Open a browser and in the address bar, type in your public IP address like this: http://<publicIPaddress> and click **Enter** to go to that address.</span></span>
4. <span data-ttu-id="43ef0-177">В браузере должна открыться веб-страница службы IIS по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="43ef0-177">Your browser should open the default IIS web page.</span></span> <span data-ttu-id="43ef0-178">Она имеет следующий вид.</span><span class="sxs-lookup"><span data-stu-id="43ef0-178">It looks something like this:</span></span>
   
    ![Снимок экрана: вид страницы IIS по умолчанию в браузере](./media/hero-role/iis-default.png)

## <a name="next-steps"></a><span data-ttu-id="43ef0-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="43ef0-180">Next steps</span></span>
* <span data-ttu-id="43ef0-181">Вы также можете попробовать [подключить диск данных](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="43ef0-181">You can also experiment with [attaching a data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to your virtual machine.</span></span> <span data-ttu-id="43ef0-182">Диски данных предоставляют дополнительное хранилище для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="43ef0-182">Data disks provide more storage for your virtual machine.</span></span>

