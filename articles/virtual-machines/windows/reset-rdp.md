---
title: "aaaReset hello пароль или настройки удаленного рабочего стола на виртуальной Машине Windows | Документы Microsoft"
description: "Узнайте, как tooreset пароля учетной записи или службы удаленного рабочего стола на виртуальной Машине Windows с помощью hello портал Azure или Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 45c69812-d3e4-48de-a98d-39a0f5675777
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 5258df7196621f0adb50debd08dd248922a966de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a><span data-ttu-id="d21a0-103">Как tooreset hello службы удаленного рабочего стола или ее пароля входа в систему на виртуальной машине Windows</span><span class="sxs-lookup"><span data-stu-id="d21a0-103">How tooreset hello Remote Desktop service or its login password in a Windows VM</span></span>
<span data-ttu-id="d21a0-104">Если не удается подключиться tooa Windows виртуальной машины (VM), можно сбросить пароль локального администратора hello или сбросить настройки службы удаленного рабочего стола hello.</span><span class="sxs-lookup"><span data-stu-id="d21a0-104">If you can't connect tooa Windows virtual machine (VM), you can reset hello local administrator password or reset hello Remote Desktop service configuration.</span></span> <span data-ttu-id="d21a0-105">Можно использовать либо hello Azure portal или hello расширение доступа виртуальной Машины в Azure PowerShell tooreset hello пароль.</span><span class="sxs-lookup"><span data-stu-id="d21a0-105">You can use either hello Azure portal or hello VM Access extension in Azure PowerShell tooreset hello password.</span></span> <span data-ttu-id="d21a0-106">При использовании PowerShell убедитесь, что hello [последний модуль PowerShell устанавливается и настраивается](/powershell/azure/overview) и вошел в tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="d21a0-106">If you are using PowerShell, make sure that you have hello [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in tooyour Azure subscription.</span></span> <span data-ttu-id="d21a0-107">Вы также можете [выполните следующие действия для виртуальных машин, созданных с помощью hello классической модели развертывания](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="d21a0-107">You can also [perform these steps for VMs created with hello Classic deployment model](reset-rdp.md).</span></span>

## <a name="ways-tooreset-configuration-or-credentials"></a><span data-ttu-id="d21a0-108">Способы настройки tooreset или учетные данные</span><span class="sxs-lookup"><span data-stu-id="d21a0-108">Ways tooreset configuration or credentials</span></span>
<span data-ttu-id="d21a0-109">В зависимости от ваших потребностей службы удаленных рабочих столов и учетные данные можно сбросить несколькими разными способами:</span><span class="sxs-lookup"><span data-stu-id="d21a0-109">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="d21a0-110">Сбросить с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="d21a0-110">Reset using hello Azure portal</span></span>](#azure-portal)
- <span data-ttu-id="d21a0-111">[сброс с помощью Azure PowerShell](#vmaccess-extension-and-powershell).</span><span class="sxs-lookup"><span data-stu-id="d21a0-111">[Reset using Azure PowerShell](#vmaccess-extension-and-powershell)</span></span>

## <a name="azure-portal"></a><span data-ttu-id="d21a0-112">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="d21a0-112">Azure portal</span></span>
<span data-ttu-id="d21a0-113">tooexpand hello портала выберите hello три строки в верхнем левом углу hello и нажмите кнопку **виртуальные машины**:</span><span class="sxs-lookup"><span data-stu-id="d21a0-113">tooexpand hello portal menu, click hello three bars in hello upper left corner and then click **Virtual machines**:</span></span>

![Выбор виртуальной машины Azure](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="d21a0-115">**Сброс пароля учетной записи локального администратора hello**</span><span class="sxs-lookup"><span data-stu-id="d21a0-115">**Reset hello local administrator account password**</span></span>

<span data-ttu-id="d21a0-116">Выберите виртуальную машину Windows, а затем щелкните **Поддержка и устранение неполадок** > **Сбросить пароль**.</span><span class="sxs-lookup"><span data-stu-id="d21a0-116">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="d21a0-117">отображается колонке сброса пароля Hello.</span><span class="sxs-lookup"><span data-stu-id="d21a0-117">hello password reset blade is displayed:</span></span>

![Страница "Сброс пароля"](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

<span data-ttu-id="d21a0-119">Введите имя пользователя hello и новый пароль, затем щелкните **обновление**.</span><span class="sxs-lookup"><span data-stu-id="d21a0-119">Enter hello username and a new password, then click **Update**.</span></span> <span data-ttu-id="d21a0-120">Повторите попытку подключения tooyour виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d21a0-120">Try connecting tooyour VM again.</span></span>

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="d21a0-121">**Сброс конфигурации службы удаленного рабочего стола hello**</span><span class="sxs-lookup"><span data-stu-id="d21a0-121">**Reset hello Remote Desktop service configuration**</span></span>

<span data-ttu-id="d21a0-122">Выберите виртуальную машину Windows, а затем щелкните **Поддержка и устранение неполадок** > **Сбросить пароль**.</span><span class="sxs-lookup"><span data-stu-id="d21a0-122">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="d21a0-123">Откроется колонка сброса пароля Hello.</span><span class="sxs-lookup"><span data-stu-id="d21a0-123">hello password reset blade is displayed.</span></span> 

![Сброс конфигурации удаленного рабочего стола](./media/reset-rdp/Portal-RM-RDP-Reset.png)

<span data-ttu-id="d21a0-125">Выберите **сброса конфигурации только** hello раскрывающееся меню, а затем щелкните **обновление**.</span><span class="sxs-lookup"><span data-stu-id="d21a0-125">Select **Reset configuration only** from hello drop-down menu, then click **Update**.</span></span> <span data-ttu-id="d21a0-126">Повторите попытку подключения tooyour виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d21a0-126">Try connecting tooyour VM again.</span></span>


## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="d21a0-127">Расширение VMAccess и PowerShell</span><span class="sxs-lookup"><span data-stu-id="d21a0-127">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="d21a0-128">Убедитесь, что имеется hello [последний модуль PowerShell устанавливается и настраивается](/powershell/azure/overview) и вошли в подписку Azure совместно с hello tooyour `Login-AzureRmAccount` командлета.</span><span class="sxs-lookup"><span data-stu-id="d21a0-128">Make sure that you have hello [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in tooyour Azure subscription with hello `Login-AzureRmAccount` cmdlet.</span></span>

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="d21a0-129">**Сброс пароля учетной записи локального администратора hello**</span><span class="sxs-lookup"><span data-stu-id="d21a0-129">**Reset hello local administrator account password**</span></span>
<span data-ttu-id="d21a0-130">Сброс hello администратора пароль или имя пользователя с hello [AzureRmVMAccessExtension набор](/powershell/module/azurerm.compute/set-azurermvmaccessextension) командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d21a0-130">Reset hello administrator password or user name with hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="d21a0-131">Создайте учетные данные следующим образом.</span><span class="sxs-lookup"><span data-stu-id="d21a0-131">Create your account credentials as follows:</span></span>

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> <span data-ttu-id="d21a0-132">Если ввести имя, отличное от hello текущей учетной записи локального администратора на виртуальной Машине, hello расширения VMAccess имени учетной записи локального администратора hello, назначает учетной записи toothat указанный пароль и выдает событие выхода из системы удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="d21a0-132">If you type a different name than hello current local administrator account on your VM, hello VMAccess extension renames hello local administrator account, assigns your specified password toothat account, and issues a Remote Desktop logoff event.</span></span> <span data-ttu-id="d21a0-133">При отключении hello учетной записи локального администратора на виртуальной Машине hello расширение VMAccess позволяет ему.</span><span class="sxs-lookup"><span data-stu-id="d21a0-133">If hello local administrator account on your VM is disabled, hello VMAccess extension enables it.</span></span>

<span data-ttu-id="d21a0-134">Следующий пример обновляет Hello hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup` toohello учетные данные, указанные.</span><span class="sxs-lookup"><span data-stu-id="d21a0-134">hello following example updates hello VM named `myVM` in hello resource group named `myResourceGroup` toohello credentials specified.</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="d21a0-135">**Сброс конфигурации службы удаленного рабочего стола hello**</span><span class="sxs-lookup"><span data-stu-id="d21a0-135">**Reset hello Remote Desktop service configuration**</span></span>
<span data-ttu-id="d21a0-136">Сброс tooyour удаленного доступа виртуальной Машины с hello [AzureRmVMAccessExtension набор](/powershell/module/azurerm.compute/set-azurermvmaccessextension) командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d21a0-136">Reset remote access tooyour VM with hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="d21a0-137">Hello следующий пример сбрасывает hello доступа расширения с именем `myVMAccess` на Виртуальную машину с именем hello `myVM` в hello `myResourceGroup` группа ресурсов:</span><span class="sxs-lookup"><span data-stu-id="d21a0-137">hello following example resets hello access extension named `myVMAccess` on hello VM named `myVM` in hello `myResourceGroup` resource group:</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> <span data-ttu-id="d21a0-138">В любой момент на виртуальной машине может быть только один агент доступа.</span><span class="sxs-lookup"><span data-stu-id="d21a0-138">At any point, a VM can have only a single VM access agent.</span></span> <span data-ttu-id="d21a0-139">Свойства агента доступа VM hello tooset успешно, hello `-ForceRerun` параметр может быть использован.</span><span class="sxs-lookup"><span data-stu-id="d21a0-139">tooset hello VM access agent properties successfully, hello `-ForceRerun` option can be used.</span></span> <span data-ttu-id="d21a0-140">При использовании `-ForceRerun`, убедитесь, что toouse hello одно имя для доступа агента ВМ hello в любой предыдущей команды.</span><span class="sxs-lookup"><span data-stu-id="d21a0-140">When using `-ForceRerun`, make sure toouse hello same name for hello VM access agent as used in any previous commands.</span></span>

<span data-ttu-id="d21a0-141">Если вы по-прежнему не удается удаленно подключиться tooyour виртуальной машины, см. Дополнительные действия tootry на [Устранение неполадок удаленного рабочего стола подключений tooa Windows Azure виртуальной машины под управлением](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d21a0-141">If you still can't connect remotely tooyour virtual machine, see more steps tootry at [Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="next-steps"></a><span data-ttu-id="d21a0-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d21a0-142">Next steps</span></span>
<span data-ttu-id="d21a0-143">Если hello расширение виртуальной Машины Azure не отвечает, не удается tooreset hello пароль, можно [сброса hello локальный пароль Windows автономной](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d21a0-143">If hello Azure VM access extension does not respond and you are unable tooreset hello password, you can [reset hello local Windows password offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="d21a0-144">Этот метод является более сложную процедуру и требует tooconnect hello виртуальный жесткий диск hello проблемный ВМ tooanother виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d21a0-144">This method is a more advanced process and requires you tooconnect hello virtual hard disk of hello problematic VM tooanother VM.</span></span> <span data-ttu-id="d21a0-145">Hello шагов, описанных в этой статье, сначала выполните и попытку метод reset hello автономного пароль в качестве последнего средства.</span><span class="sxs-lookup"><span data-stu-id="d21a0-145">Follow hello steps documented in this article first, and only attempt hello offline password reset method as a last resort.</span></span>

[<span data-ttu-id="d21a0-146">Расширения и компоненты виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="d21a0-146">Azure VM extensions and features</span></span>](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="d21a0-147">Подключение tooan виртуальной машины Azure с помощью протокола удаленного рабочего СТОЛА или SSH</span><span class="sxs-lookup"><span data-stu-id="d21a0-147">Connect tooan Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="d21a0-148">Устранение неполадок удаленного рабочего стола подключений tooa на основе Windows Azure виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="d21a0-148">Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine</span></span>](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

