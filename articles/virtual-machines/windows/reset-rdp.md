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
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a>Как tooreset hello службы удаленного рабочего стола или ее пароля входа в систему на виртуальной машине Windows
Если не удается подключиться tooa Windows виртуальной машины (VM), можно сбросить пароль локального администратора hello или сбросить настройки службы удаленного рабочего стола hello. Можно использовать либо hello Azure portal или hello расширение доступа виртуальной Машины в Azure PowerShell tooreset hello пароль. При использовании PowerShell убедитесь, что hello [последний модуль PowerShell устанавливается и настраивается](/powershell/azure/overview) и вошел в tooyour подписки Azure. Вы также можете [выполните следующие действия для виртуальных машин, созданных с помощью hello классической модели развертывания](reset-rdp.md).

## <a name="ways-tooreset-configuration-or-credentials"></a>Способы настройки tooreset или учетные данные
В зависимости от ваших потребностей службы удаленных рабочих столов и учетные данные можно сбросить несколькими разными способами:

- [Сбросить с помощью портала Azure hello](#azure-portal)
- [сброс с помощью Azure PowerShell](#vmaccess-extension-and-powershell).

## <a name="azure-portal"></a>Портал Azure
tooexpand hello портала выберите hello три строки в верхнем левом углу hello и нажмите кнопку **виртуальные машины**:

![Выбор виртуальной машины Azure](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-hello-local-administrator-account-password"></a>**Сброс пароля учетной записи локального администратора hello**

Выберите виртуальную машину Windows, а затем щелкните **Поддержка и устранение неполадок** > **Сбросить пароль**. отображается колонке сброса пароля Hello.

![Страница "Сброс пароля"](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

Введите имя пользователя hello и новый пароль, затем щелкните **обновление**. Повторите попытку подключения tooyour виртуальной Машины.

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Сброс конфигурации службы удаленного рабочего стола hello**

Выберите виртуальную машину Windows, а затем щелкните **Поддержка и устранение неполадок** > **Сбросить пароль**. Откроется колонка сброса пароля Hello. 

![Сброс конфигурации удаленного рабочего стола](./media/reset-rdp/Portal-RM-RDP-Reset.png)

Выберите **сброса конфигурации только** hello раскрывающееся меню, а затем щелкните **обновление**. Повторите попытку подключения tooyour виртуальной Машины.


## <a name="vmaccess-extension-and-powershell"></a>Расширение VMAccess и PowerShell
Убедитесь, что имеется hello [последний модуль PowerShell устанавливается и настраивается](/powershell/azure/overview) и вошли в подписку Azure совместно с hello tooyour `Login-AzureRmAccount` командлета.

### <a name="reset-hello-local-administrator-account-password"></a>**Сброс пароля учетной записи локального администратора hello**
Сброс hello администратора пароль или имя пользователя с hello [AzureRmVMAccessExtension набор](/powershell/module/azurerm.compute/set-azurermvmaccessextension) командлета PowerShell. Создайте учетные данные следующим образом.

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> Если ввести имя, отличное от hello текущей учетной записи локального администратора на виртуальной Машине, hello расширения VMAccess имени учетной записи локального администратора hello, назначает учетной записи toothat указанный пароль и выдает событие выхода из системы удаленного рабочего стола. При отключении hello учетной записи локального администратора на виртуальной Машине hello расширение VMAccess позволяет ему.

Следующий пример обновляет Hello hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup` toohello учетные данные, указанные.

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Сброс конфигурации службы удаленного рабочего стола hello**
Сброс tooyour удаленного доступа виртуальной Машины с hello [AzureRmVMAccessExtension набор](/powershell/module/azurerm.compute/set-azurermvmaccessextension) командлета PowerShell. Hello следующий пример сбрасывает hello доступа расширения с именем `myVMAccess` на Виртуальную машину с именем hello `myVM` в hello `myResourceGroup` группа ресурсов:

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> В любой момент на виртуальной машине может быть только один агент доступа. Свойства агента доступа VM hello tooset успешно, hello `-ForceRerun` параметр может быть использован. При использовании `-ForceRerun`, убедитесь, что toouse hello одно имя для доступа агента ВМ hello в любой предыдущей команды.

Если вы по-прежнему не удается удаленно подключиться tooyour виртуальной машины, см. Дополнительные действия tootry на [Устранение неполадок удаленного рабочего стола подключений tooa Windows Azure виртуальной машины под управлением](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


## <a name="next-steps"></a>Дальнейшие действия
Если hello расширение виртуальной Машины Azure не отвечает, не удается tooreset hello пароль, можно [сброса hello локальный пароль Windows автономной](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Этот метод является более сложную процедуру и требует tooconnect hello виртуальный жесткий диск hello проблемный ВМ tooanother виртуальной Машины. Hello шагов, описанных в этой статье, сначала выполните и попытку метод reset hello автономного пароль в качестве последнего средства.

[Расширения и компоненты виртуальных машин Azure](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Подключение tooan виртуальной машины Azure с помощью протокола удаленного рабочего СТОЛА или SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[Устранение неполадок удаленного рабочего стола подключений tooa на основе Windows Azure виртуальные машины](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

