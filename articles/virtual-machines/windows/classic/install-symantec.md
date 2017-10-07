---
title: "aaaInstall Symantec Endpoint Protection на виртуальной Машине Windows в Azure | Документы Microsoft"
description: "Узнайте, как tooinstall и настроить модуль безопасности hello Symantec Endpoint Protection на новый или существующей виртуальной Машине Azure hello классической модели развертывания."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: iainfou
ms.openlocfilehash: cb6083366185c26c9f43ff94d835cd90725de5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a>Как tooinstall и настройка Symantec Endpoint Protection на виртуальной Машине Windows
> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.

В этой статье показано, как tooinstall и настройки клиента hello Symantec Endpoint Protection на существующей виртуальной машины (VM) под управлением Windows Server. Этот полный клиент включает такие службы, как защита от вирусов и шпионских программ, брандмауэр и система предотвращения вторжений. Клиент Hello устанавливается как расширение безопасности с помощью hello агент виртуальной Машины.

Если у вас есть подписка от Symantec для решения в локальной среде, можно использовать его tooprotect виртуальных машин Azure. Если у вас еще нет подписки, можно зарегистрироваться для получения пробной подписки. Дополнительные сведения об этом решении см. в статье [Symantec Endpoint Protection на платформе Microsoft Azure][Symantec]. Эта страница также содержит ссылки toolicensing сведения и инструкции по установке клиента hello, если вы уже клиента Symantec.

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a>Установка Symantec Endpoint Protection на существующей виртуальной машине
Прежде чем начать, необходимо hello следующее:

* модуль Azure PowerShell Hello, версии 0.8.2 или более поздней версии на рабочем компьютере. Можно проверить версию hello Azure PowerShell, установленной с hello **Get-Module azure | format-table версии** команды. Инструкции и ссылки toohello последнюю версию, в разделе [как tooInstall и настройка Azure PowerShell][PS]. Вход с использованием подписки Azure tooyour `Add-AzureAccount`.
* Hello Здравствуйте, агент ВМ, работающий на виртуальной машине Azure.

Сначала проверьте, что hello агент виртуальной Машины уже установлена на виртуальной машине hello. Заполните hello имя облачной службы и имя виртуальной машины, а затем запустите следующие команды в командной строке Azure PowerShell администраторские hello. Замените все содержимое в кавычках hello, включая hello < и > символов.

> [!TIP]
> Если вы не знаете hello облачной службы и имена виртуальных машин, запустите **Get-AzureVM** toolist hello имена для всех виртуальных машин в текущей подписке.

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

Если hello **write-host** команда отображает **True**, hello установлен агент виртуальной Машины. Если отображается **False**, см. инструкции hello и toohello ссылку загрузить в Azure в блоге hello [агент ВМ и расширения — часть 2][Agent].

Если установлен агент ВМ hello, запустите следующие команды tooinstall hello Symantec Endpoint Protection.

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

tooverify, hello Symantec модуль безопасности был установлен и обновлен:

1. Войдите в систему виртуальной машины toohello. Инструкции см. в разделе [как tooLog на виртуальной машине под управлением Windows Server tooa][Logon].
2. Для Windows Server 2008 R2: щелкните **Пуск > Symantec Endpoint Protection**. Для Windows Server 2012 или Windows Server 2012 R2, hello начальном экране введите **Symantec**, а затем нажмите кнопку **Symantec Endpoint Protection**.
3. Из hello **состояние** вкладка hello **состояние Symantec Endpoint Protection** окна, установки обновлений и при необходимости перезагрузить.

## <a name="additional-resources"></a>Дополнительные ресурсы
[Как tooLog на tooa виртуальной машины под управлением Windows Server][Logon]

[Расширения и компоненты виртуальных машин Azure][Ext]

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
