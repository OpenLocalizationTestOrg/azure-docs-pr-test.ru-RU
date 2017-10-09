---
title: "aaaReset hello пароль или настройки удаленного рабочего стола на виртуальной Машине Windows в Azure | Документы Microsoft"
description: "Узнайте, как hello tooreset пароля учетной записи или службы удаленного рабочего стола на виртуальной Машине Windows созданного с помощью hello классического развертывания модели с помощью портала Azure или Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 1721a91fc6c89b46df74e76dfcf918b1c4c77a4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a><span data-ttu-id="1e736-103">Как службы удаленного рабочего стола tooreset hello или ее пароля входа в систему на виртуальной машине Windows, созданного с помощью hello классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="1e736-103">How tooreset hello Remote Desktop service or its login password in a Windows VM created using hello Classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1e736-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1e736-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1e736-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="1e736-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="1e736-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1e736-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="1e736-107">Вы также можете [выполните следующие действия для виртуальных машин, созданных с помощью модели развертывания диспетчера ресурсов hello](../reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="1e736-107">You can also [perform these steps for VMs created with hello Resource Manager deployment model](../reset-rdp.md).</span></span>

<span data-ttu-id="1e736-108">Если не удается подключиться tooa Windows виртуальной машины (VM), можно сбросить пароль локального администратора hello или сбросить настройки службы удаленного рабочего стола hello.</span><span class="sxs-lookup"><span data-stu-id="1e736-108">If you can't connect tooa Windows virtual machine (VM), you can reset hello local administrator password or reset hello Remote Desktop service configuration.</span></span> <span data-ttu-id="1e736-109">Можно использовать либо hello Azure portal или hello расширение доступа виртуальной Машины в Azure PowerShell tooreset hello пароль.</span><span class="sxs-lookup"><span data-stu-id="1e736-109">You can use either hello Azure portal or hello VM Access extension in Azure PowerShell tooreset hello password.</span></span>

## <a name="ways-tooreset-configuration-or-credentials"></a><span data-ttu-id="1e736-110">Способы настройки tooreset или учетные данные</span><span class="sxs-lookup"><span data-stu-id="1e736-110">Ways tooreset configuration or credentials</span></span>
<span data-ttu-id="1e736-111">В зависимости от ваших потребностей службы удаленных рабочих столов и учетные данные можно сбросить несколькими разными способами:</span><span class="sxs-lookup"><span data-stu-id="1e736-111">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="1e736-112">Сбросить с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="1e736-112">Reset using hello Azure portal</span></span>](#azure-portal)
- <span data-ttu-id="1e736-113">[сброс с помощью Azure PowerShell](#vmaccess-extension-and-powershell).</span><span class="sxs-lookup"><span data-stu-id="1e736-113">[Reset using Azure PowerShell](#vmaccess-extension-and-powershell)</span></span>

## <a name="azure-portal"></a><span data-ttu-id="1e736-114">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="1e736-114">Azure portal</span></span>
<span data-ttu-id="1e736-115">Можно использовать hello [портал Azure](https://portal.azure.com) tooreset hello службы удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="1e736-115">You can use hello [Azure portal](https://portal.azure.com) tooreset hello Remote Desktop service.</span></span> <span data-ttu-id="1e736-116">tooexpand hello портала выберите hello три строки в верхнем левом углу hello и нажмите кнопку **виртуальные машины (классические)**:</span><span class="sxs-lookup"><span data-stu-id="1e736-116">tooexpand hello portal menu, click hello three bars in hello upper left corner and then click **Virtual machines (classic)**:</span></span>

![Выбор виртуальной машины Azure](./media/reset-rdp/Portal-Select-Classic-VM.png)

<span data-ttu-id="1e736-118">Выберите виртуальную машину Windows и нажмите кнопку **удаленный сброс...** . hello появится следующее диалоговое окно настройки удаленного рабочего стола tooreset hello:</span><span class="sxs-lookup"><span data-stu-id="1e736-118">Select your Windows virtual machine and then click **Reset Remote...**. hello following dialog appears tooreset hello Remote Desktop configuration:</span></span>

![Страница "Сброс конфигурации удаленного рабочего стола"](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

<span data-ttu-id="1e736-120">Можно также сбросить hello имя пользователя и пароль учетной записи локального администратора hello.</span><span class="sxs-lookup"><span data-stu-id="1e736-120">You can also reset hello username and password of hello local administrator account.</span></span> <span data-ttu-id="1e736-121">В виртуальной машине щелкните **Поддержка и устранение неполадок** > **Сбросить пароль**.</span><span class="sxs-lookup"><span data-stu-id="1e736-121">From your VM, click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="1e736-122">отображается колонке сброса пароля Hello.</span><span class="sxs-lookup"><span data-stu-id="1e736-122">hello password reset blade is displayed:</span></span>

![Страница "Сброс пароля"](./media/reset-rdp/Portal-PW-Reset-Windows.png)

<span data-ttu-id="1e736-124">После ввода hello новое имя пользователя и пароль, щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1e736-124">After you enter hello new user name and password, click **Save**.</span></span>

## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="1e736-125">Расширение VMAccess и PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e736-125">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="1e736-126">Убедитесь, что установлен агент виртуальной Машины на виртуальной машине hello приветствия.</span><span class="sxs-lookup"><span data-stu-id="1e736-126">Make sure hello VM Agent is installed on hello virtual machine.</span></span> <span data-ttu-id="1e736-127">расширение VMAccess Hello не toobe установить, прежде чем его можно использовать, при условии, что доступен hello агент виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="1e736-127">hello VMAccess extension doesn't need toobe installed before you can use it, as long as hello VM Agent is available.</span></span> <span data-ttu-id="1e736-128">Убедитесь, что приветствия уже установлен агент ВМ, используя следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="1e736-128">Verify that hello VM Agent is already installed by using hello following command.</span></span> <span data-ttu-id="1e736-129">(Замените «myCloudService» и «myVM» hello имена облачной службы и ВМ, соответственно.</span><span class="sxs-lookup"><span data-stu-id="1e736-129">(Replace "myCloudService" and "myVM" by hello names of your cloud service and your VM, respectively.</span></span> <span data-ttu-id="1e736-130">Чтобы найти эти имена, выполните команду `Get-AzureVM` без параметров.)</span><span class="sxs-lookup"><span data-stu-id="1e736-130">You can learn these names by running `Get-AzureVM` without any parameters.)</span></span>

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="1e736-131">Если hello **write-host** команда отображает **True**, hello установлен агент виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="1e736-131">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="1e736-132">Если отображается **False**, см. инструкции hello и toohello ссылку загрузить в hello [агент ВМ и расширения — часть 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) блога Azure.</span><span class="sxs-lookup"><span data-stu-id="1e736-132">If it displays **False**, see hello instructions and a link toohello download in hello [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blog post.</span></span>

<span data-ttu-id="1e736-133">Если вы создали hello виртуальной машины с помощью портала hello, проверьте ли `$vm.GetInstance().ProvisionGuestAgent` возвращает **True**.</span><span class="sxs-lookup"><span data-stu-id="1e736-133">If you created hello virtual machine by using hello portal, check whether `$vm.GetInstance().ProvisionGuestAgent` returns **True**.</span></span> <span data-ttu-id="1e736-134">Если нет, укажите это значение с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="1e736-134">If not, you can set it by using this command:</span></span>

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

<span data-ttu-id="1e736-135">Эта команда запрещает hello следующая ошибка при запуске hello **Set-AzureVMExtension** в hello дальнейшие действия: «Подготовка гостевой агент должен быть включен hello объекта виртуальной Машины перед установкой расширения Access ВМ IaaS.»</span><span class="sxs-lookup"><span data-stu-id="1e736-135">This command prevents hello following error when you're running hello **Set-AzureVMExtension** command in hello next steps: “Provision Guest Agent must be enabled on hello VM object before setting IaaS VM Access Extension.”</span></span>

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="1e736-136">**Сброс пароля учетной записи локального администратора hello**</span><span class="sxs-lookup"><span data-stu-id="1e736-136">**Reset hello local administrator account password**</span></span>
<span data-ttu-id="1e736-137">Создание учетных данных входа в систему с Привет текущее имя учетной записи локального администратора и новый пароль, а затем запустите hello `Set-AzureVMAccessExtension` следующим образом.</span><span class="sxs-lookup"><span data-stu-id="1e736-137">Create a sign-in credential with hello current local administrator account name and a new password, and then run hello `Set-AzureVMAccessExtension` as follows.</span></span>

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

<span data-ttu-id="1e736-138">Если ввести имя, отличное от текущего счета hello hello расширения VMAccess имени учетной записи локального администратора hello, назначает учетной записи toothat пароль hello и выдает выхода удаленного рабочего стола. При отключении учетной записи локального администратора hello hello расширение VMAccess позволяет ему.</span><span class="sxs-lookup"><span data-stu-id="1e736-138">If you type a different name than hello current account, hello VMAccess extension renames hello local administrator account, assigns hello password toothat account, and issues a Remote Desktop sign-out. If hello local administrator account is disabled, hello VMAccess extension enables it.</span></span>

<span data-ttu-id="1e736-139">Эти команды также сбросить настройки службы удаленного рабочего стола hello.</span><span class="sxs-lookup"><span data-stu-id="1e736-139">These commands also reset hello Remote Desktop service configuration.</span></span>

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="1e736-140">**Сброс конфигурации службы удаленного рабочего стола hello**</span><span class="sxs-lookup"><span data-stu-id="1e736-140">**Reset hello Remote Desktop service configuration**</span></span>
<span data-ttu-id="1e736-141">tooreset hello удаленного рабочего стола конфигурации службы, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1e736-141">tooreset hello Remote Desktop service configuration, run hello following command:</span></span>

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

<span data-ttu-id="1e736-142">Hello расширения VMAccess выполняет две команды на виртуальной машине hello:</span><span class="sxs-lookup"><span data-stu-id="1e736-142">hello VMAccess extension runs two commands on hello virtual machine:</span></span>

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

<span data-ttu-id="1e736-143">Эта команда включает hello встроенного брандмауэра Windows группы, которая позволяет входящий трафик удаленного рабочего стола, который использует TCP-порт 3389.</span><span class="sxs-lookup"><span data-stu-id="1e736-143">This command enables hello built-in Windows Firewall group that allows incoming Remote Desktop traffic, which uses TCP port 3389.</span></span>

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

<span data-ttu-id="1e736-144">Эта команда задает hello fDenyTSConnections реестра значение too0, включение подключений удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="1e736-144">This command sets hello fDenyTSConnections registry value too0, enabling Remote Desktop connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e736-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1e736-145">Next steps</span></span>
<span data-ttu-id="1e736-146">Если hello расширение виртуальной Машины Azure не отвечает, не удается tooreset hello пароль, можно [сброса hello локальный пароль Windows автономной](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1e736-146">If hello Azure VM access extension does not respond and you are unable tooreset hello password, you can [reset hello local Windows password offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="1e736-147">Этот метод является более сложную процедуру и требует tooconnect hello виртуальный жесткий диск hello проблемный ВМ tooanother виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="1e736-147">This method is a more advanced process and requires you tooconnect hello virtual hard disk of hello problematic VM tooanother VM.</span></span> <span data-ttu-id="1e736-148">Hello шагов, описанных в этой статье, сначала выполните и попытку метод reset hello автономного пароль в качестве последнего средства.</span><span class="sxs-lookup"><span data-stu-id="1e736-148">Follow hello steps documented in this article first, and only attempt hello offline password reset method as a last resort.</span></span>

[<span data-ttu-id="1e736-149">Расширения и компоненты виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="1e736-149">Azure VM extensions and features</span></span>](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="1e736-150">Подключение tooan виртуальной машины Azure с помощью протокола удаленного рабочего СТОЛА или SSH</span><span class="sxs-lookup"><span data-stu-id="1e736-150">Connect tooan Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="1e736-151">Устранение неполадок удаленного рабочего стола подключений tooa на основе Windows Azure виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="1e736-151">Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine</span></span>](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

