---
title: "службы IIS на первой виртуальной Машине Windows aaaInstall | Документы Microsoft"
description: "Поэкспериментируйте с первой виртуальной машине, установка служб IIS и открыв порт 80 с использованием hello портал Azure."
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
ms.openlocfilehash: 7cfed6197df058c4569d111ee88961da7c6fe0b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a><span data-ttu-id="8fe29-103">Эксперимент с установкой роли на виртуальной машине Windows</span><span class="sxs-lookup"><span data-stu-id="8fe29-103">Experiment with installing a role on your Windows VM</span></span>
<span data-ttu-id="8fe29-104">После создания вашего первого виртуальной машины (VM вверх) и выполнения можно переместить на tooinstalling программного обеспечения и служб.</span><span class="sxs-lookup"><span data-stu-id="8fe29-104">Once you have your first virtual machine (VM) up and running, you can move on tooinstalling software and services.</span></span> <span data-ttu-id="8fe29-105">В этом учебнике мы будем toouse диспетчера серверов на tooinstall hello виртуальной Машины Windows Server IIS.</span><span class="sxs-lookup"><span data-stu-id="8fe29-105">For this tutorial, we are going toouse Server Manager on hello Windows Server VM tooinstall IIS.</span></span> <span data-ttu-id="8fe29-106">Затем мы создадим hello Azure портала tooopen порт 80 tooIIS трафик с помощью группы безопасности сети (NSG).</span><span class="sxs-lookup"><span data-stu-id="8fe29-106">Then, we will create a Network Security Group (NSG) using hello Azure portal tooopen port 80 tooIIS traffic.</span></span> 

<span data-ttu-id="8fe29-107">Если вы уже не создавали первой ВМ, вы должны вернуться назад слишком[создания первой виртуальной машине Windows в hello портал Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) перед продолжением работы с учебником.</span><span class="sxs-lookup"><span data-stu-id="8fe29-107">If you haven't already created your first VM, you should go back too[Create your first Windows virtual machine in hello Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before continuing with this tutorial.</span></span>

## <a name="make-sure-hello-vm-is-running"></a><span data-ttu-id="8fe29-108">Убедитесь, что Виртуальная машина запущена приветствия</span><span class="sxs-lookup"><span data-stu-id="8fe29-108">Make sure hello VM is running</span></span>
1. <span data-ttu-id="8fe29-109">Откройте hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8fe29-109">Open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8fe29-110">Hello концентратора меню **виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="8fe29-110">On hello hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="8fe29-111">Выберите виртуальную машину hello из списка hello.</span><span class="sxs-lookup"><span data-stu-id="8fe29-111">Select hello virtual machine from hello list.</span></span>
3. <span data-ttu-id="8fe29-112">Если состояние hello **остановлена (освобождена)**, нажмите кнопку hello **запустить** кнопку на hello **Essentials** колонке hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8fe29-112">If hello status is **Stopped (Deallocated)**, click hello **Start** button on hello **Essentials** blade of hello VM.</span></span> <span data-ttu-id="8fe29-113">Если состояние hello **под управлением**, можно переместить на следующем шаге toohello.</span><span class="sxs-lookup"><span data-stu-id="8fe29-113">If hello status is **Running**, you can move on toohello next step.</span></span>

## <a name="connect-toohello-virtual-machine-and-sign-in"></a><span data-ttu-id="8fe29-114">Подключите toohello виртуальную машину и выполните вход</span><span class="sxs-lookup"><span data-stu-id="8fe29-114">Connect toohello virtual machine and sign in</span></span>
1. <span data-ttu-id="8fe29-115">Hello концентратора меню **виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="8fe29-115">On hello hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="8fe29-116">Выберите виртуальную машину hello из списка hello.</span><span class="sxs-lookup"><span data-stu-id="8fe29-116">Select hello virtual machine from hello list.</span></span>
2. <span data-ttu-id="8fe29-117">В колонке hello для hello виртуальной машины, нажмите кнопку **Connect**.</span><span class="sxs-lookup"><span data-stu-id="8fe29-117">On hello blade for hello virtual machine, click **Connect**.</span></span> <span data-ttu-id="8fe29-118">Это создает и загружает файл протокола удаленного рабочего стола (RDP-файл), похожая на машине tooyour tooconnect ярлык.</span><span class="sxs-lookup"><span data-stu-id="8fe29-118">This creates and downloads a Remote Desktop Protocol file (.rdp file) that is like a shortcut tooconnect tooyour machine.</span></span> <span data-ttu-id="8fe29-119">Файл tooyour toosave hello desktop можно легко получить доступ.</span><span class="sxs-lookup"><span data-stu-id="8fe29-119">You might want toosave hello file tooyour desktop for easy access.</span></span> <span data-ttu-id="8fe29-120">**Откройте** tooyour tooconnect этот файл виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8fe29-120">**Open** this file tooconnect tooyour VM.</span></span>
   
    ![Снимок экрана: hello Azure портала отображение как tooconnect tooyour виртуальной Машины](./media/hero-role/connect.png)
3. <span data-ttu-id="8fe29-122">Вы получаете предупреждение, .rdp hello — от неизвестного издателя.</span><span class="sxs-lookup"><span data-stu-id="8fe29-122">You get a warning that hello .rdp is from an unknown publisher.</span></span> <span data-ttu-id="8fe29-123">Это нормально.</span><span class="sxs-lookup"><span data-stu-id="8fe29-123">This is normal.</span></span> <span data-ttu-id="8fe29-124">В окне приветствия удаленного рабочего стола, щелкните **Connect** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="8fe29-124">In hello Remote Desktop window, click **Connect** toocontinue.</span></span>
   
    ![Снимок экрана с предупреждением о неизвестном издателе](./media/hero-role/rdp-warn.png)
4. <span data-ttu-id="8fe29-126">В окне Безопасность Windows hello типа hello пользователя и пароль для hello учетная запись, созданная при создании hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8fe29-126">In hello Windows Security window, type hello username and password for hello local account that you created when you created hello VM.</span></span> <span data-ttu-id="8fe29-127">имя пользователя Hello вводится как *vmname*&#92; *имя пользователя*, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8fe29-127">hello username is entered as *vmname*&#92;*username*, then click **OK**.</span></span>
   
    ![Снимок экрана: Введите имя виртуальной Машины hello, имя пользователя и пароль](./media/hero-role/credentials.png)
5. <span data-ttu-id="8fe29-129">Вы получаете предупреждение не удалось проверить этот сертификат hello.</span><span class="sxs-lookup"><span data-stu-id="8fe29-129">You get a warning that hello certificate cannot be verified.</span></span> <span data-ttu-id="8fe29-130">Это нормально.</span><span class="sxs-lookup"><span data-stu-id="8fe29-130">This is normal.</span></span> <span data-ttu-id="8fe29-131">Нажмите кнопку **Да** tooverify hello идентификатор hello виртуальной машины и завершения входа в систему.</span><span class="sxs-lookup"><span data-stu-id="8fe29-131">Click **Yes** tooverify hello identity of hello virtual machine and finish logging on.</span></span>
   
   ![Снимок экрана, показывающий сообщение граничат служат hello удостоверением hello виртуальной Машины](./media/hero-role/cert-warning.png)

<span data-ttu-id="8fe29-133">Если вы запустите tootrouble при попытке tooconnect, [tooa подключений удаленного рабочего стола на устранение неполадок виртуальной машины на основе Windows Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8fe29-133">If you run in tootrouble when you try tooconnect, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="install-iis-on-your-vm"></a><span data-ttu-id="8fe29-134">Установка служб IIS на виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="8fe29-134">Install IIS on your VM</span></span>
<span data-ttu-id="8fe29-135">Теперь, когда вы вошли в toohello ВМ, мы установим роли сервера, можно поэкспериментировать.</span><span class="sxs-lookup"><span data-stu-id="8fe29-135">Now that you are logged in toohello VM, we will install a server role so that you can experiment more.</span></span>

1. <span data-ttu-id="8fe29-136">Откройте **диспетчер серверов** , если он еще не открыт.</span><span class="sxs-lookup"><span data-stu-id="8fe29-136">Open **Server Manager** if it isn't already open.</span></span> <span data-ttu-id="8fe29-137">Нажмите кнопку hello **запустить** меню, а затем нажмите **диспетчера сервера**.</span><span class="sxs-lookup"><span data-stu-id="8fe29-137">Click hello **Start** menu, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="8fe29-138">В **диспетчера сервера**выберите **локального сервера** hello левой панели.</span><span class="sxs-lookup"><span data-stu-id="8fe29-138">In **Server Manager**, select **Local Server** from hello left pane.</span></span> 
3. <span data-ttu-id="8fe29-139">Выберите в меню hello **управление** > **Добавить роли и компоненты**.</span><span class="sxs-lookup"><span data-stu-id="8fe29-139">In hello menu, select **Manage** > **Add Roles and Features**.</span></span>
4. <span data-ttu-id="8fe29-140">В hello Добавить роли и функции мастера на hello **тип установки** выберите **Установка ролей или компонентов**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8fe29-140">In hello Add Roles and Features Wizard, on hello **Installation Type** page, choose **Role-based or feature-based installation**, and then click **Next**.</span></span>
   
    ![Отображение приветствия мастера добавления ролей и компонентов вкладки для типа установки](./media/hero-role/role-wizard.png)
5. <span data-ttu-id="8fe29-142">Выберите пул серверов hello hello виртуальной Машины и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8fe29-142">Select hello VM from hello server pool and click **Next**.</span></span>
6. <span data-ttu-id="8fe29-143">На hello **ролей сервера** выберите **веб-сервер (IIS)**.</span><span class="sxs-lookup"><span data-stu-id="8fe29-143">On hello **Server Roles** page, select **Web Server (IIS)**.</span></span>
   
    ![Отображение приветствия мастера добавления ролей и компонентов вкладки для ролей сервера](./media/hero-role/add-iis.png)
7. <span data-ttu-id="8fe29-145">Убедитесь, что в hello всплывающих о добавлении возможности, необходимые для служб IIS, **включить средства управления** выбран, а затем нажмите кнопку **добавить компоненты**.</span><span class="sxs-lookup"><span data-stu-id="8fe29-145">In hello pop-up about adding features needed for IIS, make sure that **Include management tools** is selected and then click **Add Features**.</span></span> <span data-ttu-id="8fe29-146">После закрытия всплывающего hello, нажмите кнопку **Далее** приветствия мастера.</span><span class="sxs-lookup"><span data-stu-id="8fe29-146">When hello pop-up closes, click **Next** in hello wizard.</span></span>
   
    ![Снимок экрана, показывающий всплывающих tooconfirm Добавление роли IIS hello](./media/hero-role/confirm-add-feature.png)
8. <span data-ttu-id="8fe29-148">На странице функции hello щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8fe29-148">On hello features page, click **Next**.</span></span>
9. <span data-ttu-id="8fe29-149">На hello **роль веб-сервера (IIS)** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8fe29-149">On hello **Web Server Role (IIS)** page, click **Next**.</span></span> 
10. <span data-ttu-id="8fe29-150">На hello **служб ролей** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8fe29-150">On hello **Role Services** page, click **Next**.</span></span> 
11. <span data-ttu-id="8fe29-151">На hello **Подтверждение** щелкните **установить**.</span><span class="sxs-lookup"><span data-stu-id="8fe29-151">On hello **Confirmation** page, click **Install**.</span></span> 
12. <span data-ttu-id="8fe29-152">По завершении установки hello щелкните **закрыть** на приветствия мастера.</span><span class="sxs-lookup"><span data-stu-id="8fe29-152">When hello installation is complete, click **Close** on hello wizard.</span></span>

## <a name="open-port-80"></a><span data-ttu-id="8fe29-153">Открытие порта 80</span><span class="sxs-lookup"><span data-stu-id="8fe29-153">Open port 80</span></span>
<span data-ttu-id="8fe29-154">В порядке для вашей виртуальной Машины tooaccept входящий трафик через порт 80, необходимо tooadd правило для входящего трафика toohello сетевой группы безопасности.</span><span class="sxs-lookup"><span data-stu-id="8fe29-154">In order for your VM tooaccept inbound traffic over port 80, you need tooadd an inbound rule toohello network security group.</span></span> 

1. <span data-ttu-id="8fe29-155">Откройте hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8fe29-155">Open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8fe29-156">В **виртуальные машины** Здравствуйте, выберите созданную ВМ.</span><span class="sxs-lookup"><span data-stu-id="8fe29-156">In **Virtual machines** select hello VM that you created.</span></span>
3. <span data-ttu-id="8fe29-157">В параметрах hello виртуальные машины, выберите **сетевых интерфейсов** и затем выберите hello существующего сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="8fe29-157">In hello virtual machines settings, select **Network interfaces** and then select hello existing network interface.</span></span>
   
    ![Снимок экрана приветствия виртуальной машины для hello сетевых интерфейсов](./media/hero-role/network-interface.png)
4. <span data-ttu-id="8fe29-159">В **Essentials** для hello сетевого интерфейса, нажмите кнопку hello **сетевой группы безопасности**.</span><span class="sxs-lookup"><span data-stu-id="8fe29-159">In **Essentials** for hello network interface, click hello **Network security group**.</span></span>
   
    ![Снимок экрана, показывающий hello Essentials раздел для hello сетевого интерфейса](./media/hero-role/select-nsg.png)
5. <span data-ttu-id="8fe29-161">В hello **Essentials** колонке hello NSG, должны иметь один существующее значение по умолчанию правило для входящего трафика **разрешить rdp по умолчанию** позволяющее toolog в toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8fe29-161">In hello **Essentials** blade for hello NSG, you should have one existing default inbound rule for **default-allow-rdp** which allows you toolog in toohello VM.</span></span> <span data-ttu-id="8fe29-162">Вы добавите трафика IIS tooallow другое правило для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="8fe29-162">You will add another inbound rule tooallow IIS traffic.</span></span> <span data-ttu-id="8fe29-163">Щелкните **Правило безопасности для входящего трафика**.</span><span class="sxs-lookup"><span data-stu-id="8fe29-163">Click **Inbound security rule**.</span></span>
   
    ![Снимок экрана, показывающий hello Essentials раздел для hello NSG](./media/hero-role/inbound.png)
6. <span data-ttu-id="8fe29-165">В разделе **Правила безопасности для входящего трафика** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8fe29-165">In **Inbound security rules**, click **Add**.</span></span>
   
    ![Снимок экрана, показывающий tooadd кнопку hello правило безопасности](./media/hero-role/add-rule.png)
7. <span data-ttu-id="8fe29-167">В разделе **Правила безопасности для входящего трафика** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8fe29-167">In **Inbound security rules**, click **Add**.</span></span> <span data-ttu-id="8fe29-168">Тип **80** в hello диапазон портов и убедитесь, что **Разрешить** выбран.</span><span class="sxs-lookup"><span data-stu-id="8fe29-168">Type **80** in hello port range and make sure **Allow** is selected.</span></span> <span data-ttu-id="8fe29-169">Когда все будет готово, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8fe29-169">When you are done, click **OK**.</span></span>
   
    ![Снимок экрана, показывающий tooadd кнопку hello правило безопасности](./media/hero-role/port-80.png)

<span data-ttu-id="8fe29-171">Дополнительные сведения о Nsg, входящие и исходящие правила, в разделе [разрешить внешний доступ tooyour виртуальной Машины с помощью hello портал Azure](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="8fe29-171">For more information about NSGs, inbound and outbound rules, see [Allow external access tooyour VM using hello Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="connect-toohello-default-iis-website"></a><span data-ttu-id="8fe29-172">Подключение веб-сайт IIS по умолчанию toohello</span><span class="sxs-lookup"><span data-stu-id="8fe29-172">Connect toohello default IIS website</span></span>
1. <span data-ttu-id="8fe29-173">В hello портал Azure, щелкните **виртуальные машины** , а затем выберите виртуальную Машину.</span><span class="sxs-lookup"><span data-stu-id="8fe29-173">In hello Azure portal, click **Virtual machines** and then select your VM.</span></span>
2. <span data-ttu-id="8fe29-174">В hello **Essentials** колонки, скопируйте вашей **общедоступный IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="8fe29-174">In hello **Essentials** blade, copy your **Public IP address**.</span></span>
   
    ![Снимок экрана, показывающий, где toofind hello общедоступный IP-адрес виртуальной машины](./media/hero-role/ipaddress.png)
3. <span data-ttu-id="8fe29-176">Откройте браузер и введите в адресной строке hello, в открытый IP-адреса следующим образом: http://<publicIPaddress> и нажмите кнопку **ввод** toogo toothat адрес.</span><span class="sxs-lookup"><span data-stu-id="8fe29-176">Open a browser and in hello address bar, type in your public IP address like this: http://<publicIPaddress> and click **Enter** toogo toothat address.</span></span>
4. <span data-ttu-id="8fe29-177">Браузер должен открыться hello по умолчанию службы IIS веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="8fe29-177">Your browser should open hello default IIS web page.</span></span> <span data-ttu-id="8fe29-178">Она имеет следующий вид.</span><span class="sxs-lookup"><span data-stu-id="8fe29-178">It looks something like this:</span></span>
   
    ![Снимок экрана, показывающий, какая страница IIS по умолчанию hello выглядит в браузере](./media/hero-role/iis-default.png)

## <a name="next-steps"></a><span data-ttu-id="8fe29-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8fe29-180">Next steps</span></span>
* <span data-ttu-id="8fe29-181">Также можно поэкспериментировать с [при подключении диска данных](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8fe29-181">You can also experiment with [attaching a data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour virtual machine.</span></span> <span data-ttu-id="8fe29-182">Диски данных предоставляют дополнительное хранилище для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8fe29-182">Data disks provide more storage for your virtual machine.</span></span>

