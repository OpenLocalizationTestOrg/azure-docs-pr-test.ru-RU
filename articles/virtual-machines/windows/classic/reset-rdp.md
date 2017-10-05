---
title: "Сброс пароля или конфигурации удаленного рабочего стола для виртуальной машины Windows в Azure | Документация Майкрософт"
description: "Узнайте, как с помощью портала Azure или Azure PowerShell сбросить пароль учетной записи или конфигурацию службы удаленного рабочего стола для виртуальной машины Windows, созданной с использованием классической модели развертывания."
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
ms.openlocfilehash: 43e5cf1ab3bc3121d7e3915ea0785998e0ee2fc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-the-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-the-classic-deployment-model"></a><span data-ttu-id="c559f-103">Сброс службы удаленного рабочего стола или ее пароля для входа в систему на виртуальной машине Windows, созданной с использованием классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="c559f-103">How to reset the Remote Desktop service or its login password in a Windows VM created using the Classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c559f-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c559f-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c559f-105">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="c559f-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="c559f-106">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c559f-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="c559f-107">Вы также можете [выполнить эти шаги на виртуальных машинах, созданных на основе модели развертывания с помощью Resource Manager](../reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="c559f-107">You can also [perform these steps for VMs created with the Resource Manager deployment model](../reset-rdp.md).</span></span>

<span data-ttu-id="c559f-108">Если не удается подключиться к виртуальной машине Windows, можно сбросить пароль локального администратора или конфигурацию службы удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="c559f-108">If you can't connect to a Windows virtual machine (VM), you can reset the local administrator password or reset the Remote Desktop service configuration.</span></span> <span data-ttu-id="c559f-109">Для сброса пароля можно использовать портал Azure или расширение VMAccess в Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c559f-109">You can use either the Azure portal or the VM Access extension in Azure PowerShell to reset the password.</span></span>

## <a name="ways-to-reset-configuration-or-credentials"></a><span data-ttu-id="c559f-110">Способы сброса конфигурации или учетных данных</span><span class="sxs-lookup"><span data-stu-id="c559f-110">Ways to reset configuration or credentials</span></span>
<span data-ttu-id="c559f-111">В зависимости от ваших потребностей службы удаленных рабочих столов и учетные данные можно сбросить несколькими разными способами:</span><span class="sxs-lookup"><span data-stu-id="c559f-111">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- <span data-ttu-id="c559f-112">[сброс с помощью портала Azure](#azure-portal);</span><span class="sxs-lookup"><span data-stu-id="c559f-112">[Reset using the Azure portal](#azure-portal)</span></span>
- <span data-ttu-id="c559f-113">[сброс с помощью Azure PowerShell](#vmaccess-extension-and-powershell).</span><span class="sxs-lookup"><span data-stu-id="c559f-113">[Reset using Azure PowerShell](#vmaccess-extension-and-powershell)</span></span>

## <a name="azure-portal"></a><span data-ttu-id="c559f-114">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="c559f-114">Azure portal</span></span>
<span data-ttu-id="c559f-115">Сброс службы удаленного рабочего стола можно выполнить с помощью [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c559f-115">You can use the [Azure portal](https://portal.azure.com) to reset the Remote Desktop service.</span></span> <span data-ttu-id="c559f-116">Чтобы развернуть меню портала, щелкните три полосы в левом верхнем углу и выберите **Виртуальные машины (классика)**.</span><span class="sxs-lookup"><span data-stu-id="c559f-116">To expand the portal menu, click the three bars in the upper left corner and then click **Virtual machines (classic)**:</span></span>

![Выбор виртуальной машины Azure](./media/reset-rdp/Portal-Select-Classic-VM.png)

<span data-ttu-id="c559f-118">Выберите виртуальную машину Windows и щелкните **Сброс удаленной конфигурации (новый портал)**.</span><span class="sxs-lookup"><span data-stu-id="c559f-118">Select your Windows virtual machine and then click **Reset Remote...**.</span></span> <span data-ttu-id="c559f-119">Отобразится диалоговое окно сброса конфигурации удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="c559f-119">The following dialog appears to reset the Remote Desktop configuration:</span></span>

![Страница "Сброс конфигурации удаленного рабочего стола"](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

<span data-ttu-id="c559f-121">Можно также сбросить имя и пароль учетной записи локального администратора.</span><span class="sxs-lookup"><span data-stu-id="c559f-121">You can also reset the username and password of the local administrator account.</span></span> <span data-ttu-id="c559f-122">В виртуальной машине щелкните **Поддержка и устранение неполадок** > **Сбросить пароль**.</span><span class="sxs-lookup"><span data-stu-id="c559f-122">From your VM, click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="c559f-123">Отобразится колонка сброса пароля.</span><span class="sxs-lookup"><span data-stu-id="c559f-123">The password reset blade is displayed:</span></span>

![Страница "Сброс пароля"](./media/reset-rdp/Portal-PW-Reset-Windows.png)

<span data-ttu-id="c559f-125">Введите новое имя пользователя и пароль, затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c559f-125">After you enter the new user name and password, click **Save**.</span></span>

## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="c559f-126">Расширение VMAccess и PowerShell</span><span class="sxs-lookup"><span data-stu-id="c559f-126">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="c559f-127">Убедитесь, что агент ВМ установлен на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c559f-127">Make sure the VM Agent is installed on the virtual machine.</span></span> <span data-ttu-id="c559f-128">Для использования расширения VMAccess его не обязательно нужно устанавливать, если доступен агент ВМ.</span><span class="sxs-lookup"><span data-stu-id="c559f-128">The VMAccess extension doesn't need to be installed before you can use it, as long as the VM Agent is available.</span></span> <span data-ttu-id="c559f-129">Убедитесь, что агент VM уже установлен на виртуальной машине, используя следующую команду.</span><span class="sxs-lookup"><span data-stu-id="c559f-129">Verify that the VM Agent is already installed by using the following command.</span></span> <span data-ttu-id="c559f-130">(Замените myCloudService и myVM именами облачной службы и виртуальной машины соответственно.</span><span class="sxs-lookup"><span data-stu-id="c559f-130">(Replace "myCloudService" and "myVM" by the names of your cloud service and your VM, respectively.</span></span> <span data-ttu-id="c559f-131">Чтобы найти эти имена, выполните команду `Get-AzureVM` без параметров.)</span><span class="sxs-lookup"><span data-stu-id="c559f-131">You can learn these names by running `Get-AzureVM` without any parameters.)</span></span>

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="c559f-132">Если команда **write-host** отображает значение **True**, агент ВМ установлен.</span><span class="sxs-lookup"><span data-stu-id="c559f-132">If the **write-host** command displays **True**, the VM Agent is installed.</span></span> <span data-ttu-id="c559f-133">Если она отображает значение **False**, соответствующие инструкции и ссылку для скачивания можно найти в записи блога Azure [Агент виртуальной машины и расширения — часть 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) .</span><span class="sxs-lookup"><span data-stu-id="c559f-133">If it displays **False**, see the instructions and a link to the download in the [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blog post.</span></span>

<span data-ttu-id="c559f-134">Если вы создали виртуальную машину с помощью портала, проверьте, возвращает ли `$vm.GetInstance().ProvisionGuestAgent` значение **True**.</span><span class="sxs-lookup"><span data-stu-id="c559f-134">If you created the virtual machine by using the portal, check whether `$vm.GetInstance().ProvisionGuestAgent` returns **True**.</span></span> <span data-ttu-id="c559f-135">Если нет, укажите это значение с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="c559f-135">If not, you can set it by using this command:</span></span>

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

<span data-ttu-id="c559f-136">Если выполнить эту команду, то во время выполнения команды **Set-AzureVMExtension** на следующих шагах не появится сообщение о том, что перед настройкой расширения виртуальной машины IaaS требуется включить гостевой агент подготовки в объекте виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c559f-136">This command prevents the following error when you're running the **Set-AzureVMExtension** command in the next steps: “Provision Guest Agent must be enabled on the VM object before setting IaaS VM Access Extension.”</span></span>

### <a name="reset-the-local-administrator-account-password"></a><span data-ttu-id="c559f-137">**Сброс пароля учетной записи локального администратора**</span><span class="sxs-lookup"><span data-stu-id="c559f-137">**Reset the local administrator account password**</span></span>
<span data-ttu-id="c559f-138">Создайте учетные данные для входа с именем учетной записи текущего локального администратора и новым паролем, а затем выполните команду `Set-AzureVMAccessExtension` .</span><span class="sxs-lookup"><span data-stu-id="c559f-138">Create a sign-in credential with the current local administrator account name and a new password, and then run the `Set-AzureVMAccessExtension` as follows.</span></span>

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

<span data-ttu-id="c559f-139">Если вы укажете другое имя для учетной записи, расширение VMAccess переименует учетную запись локального администратора, назначит пароль этой учетной записи и закроет удаленный рабочий стол.</span><span class="sxs-lookup"><span data-stu-id="c559f-139">If you type a different name than the current account, the VMAccess extension renames the local administrator account, assigns the password to that account, and issues a Remote Desktop sign-out.</span></span> <span data-ttu-id="c559f-140">Если учетная запись локального администратора отключена, расширение VMAccess включит ее.</span><span class="sxs-lookup"><span data-stu-id="c559f-140">If the local administrator account is disabled, the VMAccess extension enables it.</span></span>

<span data-ttu-id="c559f-141">Эти команды также сбрасывают конфигурацию службы удаленных рабочих столов.</span><span class="sxs-lookup"><span data-stu-id="c559f-141">These commands also reset the Remote Desktop service configuration.</span></span>

### <a name="reset-the-remote-desktop-service-configuration"></a><span data-ttu-id="c559f-142">**Сброс конфигурации службы удаленных рабочих столов**</span><span class="sxs-lookup"><span data-stu-id="c559f-142">**Reset the Remote Desktop service configuration**</span></span>
<span data-ttu-id="c559f-143">Чтобы сбросить конфигурацию службы удаленных рабочих столов, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="c559f-143">To reset the Remote Desktop service configuration, run the following command:</span></span>

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

<span data-ttu-id="c559f-144">Расширение VMAccess запустит эти две команды на виртуальной машине:</span><span class="sxs-lookup"><span data-stu-id="c559f-144">The VMAccess extension runs two commands on the virtual machine:</span></span>

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

<span data-ttu-id="c559f-145">Эта команда включает встроенную группу брандмауэра Windows, которая разрешает входящий трафик удаленного рабочего стола через TCP-порт 3389.</span><span class="sxs-lookup"><span data-stu-id="c559f-145">This command enables the built-in Windows Firewall group that allows incoming Remote Desktop traffic, which uses TCP port 3389.</span></span>

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

<span data-ttu-id="c559f-146">Эта команда задает значение реестра fDenyTSConnections равным 0, включая подключения удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="c559f-146">This command sets the fDenyTSConnections registry value to 0, enabling Remote Desktop connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c559f-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c559f-147">Next steps</span></span>
<span data-ttu-id="c559f-148">Если расширение доступа к виртуальной машине Azure не отвечает и сбросить пароль не удается, вы можете [сбросить локальный пароль Windows в автономном режиме](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c559f-148">If the Azure VM access extension does not respond and you are unable to reset the password, you can [reset the local Windows password offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="c559f-149">Этот метод является более сложным процессом и требует подключения виртуального жесткого диска проблемной виртуальной машины к другой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c559f-149">This method is a more advanced process and requires you to connect the virtual hard disk of the problematic VM to another VM.</span></span> <span data-ttu-id="c559f-150">Сначала выполните действия, описанные в этой статье, и только потом попробуйте сбросить пароль в автономном режиме в качестве последнего средства.</span><span class="sxs-lookup"><span data-stu-id="c559f-150">Follow the steps documented in this article first, and only attempt the offline password reset method as a last resort.</span></span>

[<span data-ttu-id="c559f-151">Расширения и компоненты виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="c559f-151">Azure VM extensions and features</span></span>](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="c559f-152">Подключение к виртуальной машине Azure с помощью RDP или SSH</span><span class="sxs-lookup"><span data-stu-id="c559f-152">Connect to an Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="c559f-153">Устранение неполадок с подключением к удаленному рабочему столу виртуальной машины Windows в службе Azure</span><span class="sxs-lookup"><span data-stu-id="c559f-153">Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine</span></span>](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

