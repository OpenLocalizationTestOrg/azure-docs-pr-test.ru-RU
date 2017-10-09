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
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a>Как службы удаленного рабочего стола tooreset hello или ее пароля входа в систему на виртуальной машине Windows, созданного с помощью hello классической модели развертывания
> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Вы также можете [выполните следующие действия для виртуальных машин, созданных с помощью модели развертывания диспетчера ресурсов hello](../reset-rdp.md).

Если не удается подключиться tooa Windows виртуальной машины (VM), можно сбросить пароль локального администратора hello или сбросить настройки службы удаленного рабочего стола hello. Можно использовать либо hello Azure portal или hello расширение доступа виртуальной Машины в Azure PowerShell tooreset hello пароль.

## <a name="ways-tooreset-configuration-or-credentials"></a>Способы настройки tooreset или учетные данные
В зависимости от ваших потребностей службы удаленных рабочих столов и учетные данные можно сбросить несколькими разными способами:

- [Сбросить с помощью портала Azure hello](#azure-portal)
- [сброс с помощью Azure PowerShell](#vmaccess-extension-and-powershell).

## <a name="azure-portal"></a>Портал Azure
Можно использовать hello [портал Azure](https://portal.azure.com) tooreset hello службы удаленного рабочего стола. tooexpand hello портала выберите hello три строки в верхнем левом углу hello и нажмите кнопку **виртуальные машины (классические)**:

![Выбор виртуальной машины Azure](./media/reset-rdp/Portal-Select-Classic-VM.png)

Выберите виртуальную машину Windows и нажмите кнопку **удаленный сброс...** . hello появится следующее диалоговое окно настройки удаленного рабочего стола tooreset hello:

![Страница "Сброс конфигурации удаленного рабочего стола"](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

Можно также сбросить hello имя пользователя и пароль учетной записи локального администратора hello. В виртуальной машине щелкните **Поддержка и устранение неполадок** > **Сбросить пароль**. отображается колонке сброса пароля Hello.

![Страница "Сброс пароля"](./media/reset-rdp/Portal-PW-Reset-Windows.png)

После ввода hello новое имя пользователя и пароль, щелкните **Сохранить**.

## <a name="vmaccess-extension-and-powershell"></a>Расширение VMAccess и PowerShell
Убедитесь, что установлен агент виртуальной Машины на виртуальной машине hello приветствия. расширение VMAccess Hello не toobe установить, прежде чем его можно использовать, при условии, что доступен hello агент виртуальной Машины. Убедитесь, что приветствия уже установлен агент ВМ, используя следующую команду hello. (Замените «myCloudService» и «myVM» hello имена облачной службы и ВМ, соответственно. Чтобы найти эти имена, выполните команду `Get-AzureVM` без параметров.)

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

Если hello **write-host** команда отображает **True**, hello установлен агент виртуальной Машины. Если отображается **False**, см. инструкции hello и toohello ссылку загрузить в hello [агент ВМ и расширения — часть 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) блога Azure.

Если вы создали hello виртуальной машины с помощью портала hello, проверьте ли `$vm.GetInstance().ProvisionGuestAgent` возвращает **True**. Если нет, укажите это значение с помощью следующей команды:

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

Эта команда запрещает hello следующая ошибка при запуске hello **Set-AzureVMExtension** в hello дальнейшие действия: «Подготовка гостевой агент должен быть включен hello объекта виртуальной Машины перед установкой расширения Access ВМ IaaS.»

### <a name="reset-hello-local-administrator-account-password"></a>**Сброс пароля учетной записи локального администратора hello**
Создание учетных данных входа в систему с Привет текущее имя учетной записи локального администратора и новый пароль, а затем запустите hello `Set-AzureVMAccessExtension` следующим образом.

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

Если ввести имя, отличное от текущего счета hello hello расширения VMAccess имени учетной записи локального администратора hello, назначает учетной записи toothat пароль hello и выдает выхода удаленного рабочего стола. При отключении учетной записи локального администратора hello hello расширение VMAccess позволяет ему.

Эти команды также сбросить настройки службы удаленного рабочего стола hello.

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Сброс конфигурации службы удаленного рабочего стола hello**
tooreset hello удаленного рабочего стола конфигурации службы, запустите hello следующую команду:

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

Hello расширения VMAccess выполняет две команды на виртуальной машине hello:

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

Эта команда включает hello встроенного брандмауэра Windows группы, которая позволяет входящий трафик удаленного рабочего стола, который использует TCP-порт 3389.

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

Эта команда задает hello fDenyTSConnections реестра значение too0, включение подключений удаленного рабочего стола.

## <a name="next-steps"></a>Дальнейшие действия
Если hello расширение виртуальной Машины Azure не отвечает, не удается tooreset hello пароль, можно [сброса hello локальный пароль Windows автономной](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Этот метод является более сложную процедуру и требует tooconnect hello виртуальный жесткий диск hello проблемный ВМ tooanother виртуальной Машины. Hello шагов, описанных в этой статье, сначала выполните и попытку метод reset hello автономного пароль в качестве последнего средства.

[Расширения и компоненты виртуальных машин Azure](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Подключение tooan виртуальной машины Azure с помощью протокола удаленного рабочего СТОЛА или SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[Устранение неполадок удаленного рабочего стола подключений tooa на основе Windows Azure виртуальные машины](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

