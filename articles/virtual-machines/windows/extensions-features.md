---
title: "aaaVirtual машины расширения и компоненты для Windows в Azure | Документы Microsoft"
description: "Узнайте о расширениях, доступных для виртуальных машин Azure и сгруппированных по предоставляемым функциям или улучшениям."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 999d63ee-890e-432e-9391-25b3fc6cde28
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/06/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 61ccfd696b38e9be1026d836d5796c2346fd650f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a>Обзор расширений и компонентов виртуальной машины под управлением Windows

Расширения виртуальных машин Azure — это небольшие приложения, которые выполняют задачи настройки и автоматизации после развертывания виртуальных машин Azure. Например, если виртуальная машина требует установки программного обеспечения защиты от вирусов и конфигурации Docker, расширение ВМ может быть используется toocomplete этих задач. Расширений ВМ Azure можно выполнять с помощью hello Azure CLI PowerShell шаблоны диспетчера ресурсов Azure и hello портал Azure. Расширения можно использовать при развертывании новой виртуальной машины или запускать на любой из существующих систем.

В этом документе Обзор расширений виртуальной машины, предварительные условия для использования расширения виртуальных машин, а также рекомендации о предоставлении toodetect, управление и удаление расширений виртуальной машины. Этот документ содержит только обобщенные сведения, так как существует множество расширений виртуальной машины с разными параметрами настройки. Сведения о различных модулей можно найти в каждое расширение отдельных toohello определенного документа.

## <a name="use-cases-and-samples"></a>Варианты использования и примеры

Существует много разных расширений виртуальной машины Azure, каждое из которых используется в определенных случаях. Вот некоторые варианты использования:

- Применение требуемого состояния PowerShell конфигураций tooa виртуальной машины с помощью расширения hello DSC для Windows. Подробнее см. [Общие сведения об обработчике расширения Desired State Configuration в Azure](extensions-dsc-overview.md);
- Настройте наблюдение за виртуальной машины с помощью расширения виртуальной Машине агент наблюдения Microsoft hello. Дополнительные сведения см. в разделе [tooLog виртуальных машин подключение Azure Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).
- Настройка мониторинга инфраструктуры Azure с hello Datadog расширения. Дополнительные сведения см. в разделе hello [Datadog блог](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).
- настройка виртуальной машины Azure с помощью Chef. Подробнее см. [Автоматизация развертывания виртуальной машины Azure с помощью Chef](chef-automation.md);

Кроме расширения tooprocess, расширение пользовательского скрипта доступен для виртуальных машин Windows и Linux. расширение пользовательского скрипта для Windows Hello позволяет любой toobe сценария PowerShell, выполните на виртуальной машине. Это полезно при разработке развертывания Azure, требующего дополнительной настройки, которую не могут выполнить собственные средства Azure. Подробнее см. [Использование расширений пользовательских сценариев для виртуальной машины Windows с шаблонами Azure Resource Manager](extensions-customscript.md).


## <a name="prerequisites"></a>Предварительные требования

Каждое расширение виртуальной машины может иметь собственный набор необходимых компонентов. К примеру hello расширение ВМ Docker обладает необходимым условием поддерживаемые ОС Linux. Требования отдельных расширений, описаны в документации конкретного расширения hello.

### <a name="azure-vm-agent"></a>Агент виртуальной машины Azure
агент ВМ Azure Hello управляет взаимодействием между виртуальной машины Azure и Azure fabric controller hello. агент виртуальной Машины Hello отвечает за многие аспекты работы развертывания и управления Azure виртуальные машины, включая выполнение расширений ВМ. агент ВМ Azure Hello предустановлен на Azure Marketplace образов и могут быть установлены на поддерживаемых операционных системах.

Сведения о поддерживаемых операционных системах и инструкции по установке см. в статье [Обзор агента и расширений виртуальной машины](agent-user-guide.md).

## <a name="discover-vm-extensions"></a>Поиск расширений ВМ
Существует множество различных расширений ВМ, которые можно использовать с виртуальными машинами Azure. toosee полный список, запустите следующую команду с модулем PowerShell диспетчера ресурсов Azure hello hello. Убедитесь, что расположение требуемого hello toospecify при запуске этой команды.

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a>Запуск расширений ВМ

Расширения виртуальных машин Azure может выполняться на существующих виртуальных машин, что полезно при необходимости изменения конфигурации toomake или восстановить подключение на уже развернутой виртуальной Машины. Также расширения можно использовать при развертывании с помощью шаблонов Azure Resource Manager. С помощью расширений с помощью шаблонов диспетчера ресурсов, можно включить toobe виртуальных машин Azure развертывания и настройки без необходимости вмешательства после развертывания hello.

Hello следующие методы можно использовать toorun расширение для существующей виртуальной машины.

### <a name="powershell"></a>PowerShell

Есть несколько команд PowerShell, позволяющих выполнять отдельные модули. toosee список, запустите следующие команды PowerShell hello.

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

Это обеспечивает аналогичную toohello следующие выходные данные:

```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Set-AzureRmVMAccessExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMADDomainExtension                     2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMAEMExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBackupExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBginfoExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMChefExtension                         2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMCustomScriptExtension                 2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiagnosticsExtension                  2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiskEncryptionExtension               2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDscExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMExtension                             2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMSqlServerExtension                    2.2.0      AzureRM.Compute
```

Hello следующий пример использует hello пользовательский сценарий расширения toodownload сценарий из репозитория GitHub hello целевой виртуальной машине и затем запустите скрипт hello. Дополнительные сведения о hello расширение пользовательского скрипта см. в разделе [Обзор расширения пользовательский сценарий](extensions-customscript.md).

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

В этом примере hello расширение виртуальной Машины — используется tooreset hello административный пароль Windows виртуальной машины. Дополнительные сведения о hello расширение виртуальной Машины в разделе [сброс службы удаленного рабочего стола на виртуальной машине Windows](reset-rdp.md).

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

Hello `Set-AzureRmVMExtension` команды можно использовать toostart любое расширение виртуальной Машины. Дополнительные сведения см. в разделе hello [AzureRmVMExtension набор ссылок](https://msdn.microsoft.com/en-us/library/mt603745.aspx).


### <a name="azure-portal"></a>Портал Azure

Расширение виртуальной Машины может быть применен tooan существующей виртуальной машины через портал Azure hello. toodo таким образом, выберите виртуальную машину hello нужны toouse, выберите **расширения**и нажмите кнопку **добавить**. Вы увидите список доступных расширений. Выберите hello требуется, и следуйте указаниям мастера hello в hello.

Hello следующем рисунке показана установка hello hello модуль защиты от вредоносных программ Майкрософт от hello портал Azure.

![Установка расширения защиты от вредоносных программ](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a>Шаблоны диспетчера ресурсов Azure

Расширения ВМ может быть добавлено tooan шаблона диспетчера ресурсов Azure и выполняться hello развертывания шаблона hello. Развертывание расширений с помощью шаблона позволяет создать полностью настроенные развертывания Azure. Например приветствия следующий JSON берется из шаблона диспетчера ресурсов, который развертывает набор с балансировкой нагрузки виртуальные машины и базы данных Azure SQL, а затем устанавливает приложение .NET Core на каждой виртуальной Машине. Установка программного обеспечения hello обеспечивает Hello расширения виртуальной Машины.

Дополнительные сведения см. в разделе hello [полного шаблона диспетчера ресурсов](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

Дополнительные сведения см. в статье [Создание шаблонов Azure Resource Manager с помощью расширений виртуальной машины Windows](template-description.md#extensions).

## <a name="secure-vm-extension-data"></a>Защита данных в расширениях ВМ

При работе с расширением ВМ, может быть необходимо tooinclude конфиденциальные сведения, например учетные данные, имена учетных записей хранилища и ключи доступа к учетной записи хранения. Множество расширений ВМ включают защищенной конфигурации, который шифрует данные и только расшифровывает его целевой виртуальной машине hello. Каждое расширение имеет собственную схему защищенной конфигурации, которая описывается в документации по этим расширениям.

Привет, в следующем примере показан экземпляр hello расширение пользовательского скрипта для Windows. Обратите внимание, что команды, hello tooexecute включает в себя набор учетных данных. В этом примере команда tooexecute hello не будут зашифрованы.


```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ],
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

Защитить строку hello выполнения путем перемещения hello **tooexecute команда** toohello свойство **защищенных** конфигурации.

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

## <a name="troubleshoot-vm-extensions"></a>Устранение неполадок с расширениями ВМ

Связанные с каждым расширением виртуальной машины неполадки устраняются определенным образом. Для экземпляра когда вы используете расширение пользовательского скрипта hello, сведения о выполнении скрипта можно найти локально на hello виртуальной машины, на котором был выполнен hello расширения. Действия по устранению неполадок для конкретных расширений описаны в документации по соответствующим расширениям.

следующие шаги по устранению неполадок Hello применяются tooall расширения виртуальных машин.

### <a name="view-extension-status"></a>Просмотр состояния расширения

После завершения выполнения расширения виртуальной машины от виртуальной машины, используйте hello следующие состояния расширения tooreturn команды PowerShell. Замените в примере имена-параметры собственными значениями. Hello `Name` принимает имя hello, данное расширение toohello во время выполнения.

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Hello вывод выглядит следующим образом следующие hello.

```json
ResourceGroupName       : myResourceGroup
VMName                  : myVM
Name                    : myExtensionName
Location                : westus
Etag                    : null
Publisher               : Microsoft.Azure.Extensions
ExtensionType           : DockerExtension
TypeHandlerVersion      : 1.0
Id                      : /subscriptions/mySubscriptionIS/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM/extensions/myExtensionName
PublicSettings          :
ProtectedSettings       :
ProvisioningState       : Succeeded
Statuses                :
SubStatuses             :
AutoUpgradeMinorVersion : False
ForceUpdateTag          :
```

Состояние выполнения расширения можно найти также в hello портал Azure. состояние hello tooview расширение, выберите hello виртуальной машины, выберите **расширения**, и выберите hello нужное расширение.

### <a name="rerun-vm-extensions"></a>Повторный запуск расширений виртуальной машины

Возможны ситуации, в которых расширение виртуальной машины должен toobe повторно. Это можно сделать, удалив расширение hello и повторно запустив hello расширения с помощью метода выполнения по своему усмотрению. tooremove расширение, запустите следующую команду с помощью модуля Azure PowerShell hello hello. Замените в примере имена-параметры собственными значениями.

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Расширения можно также удалить с помощью портала Azure hello. toodo так:

1. Выберите виртуальную машину.
2. Выберите **Расширения**.
3. Выберите расширение требуемого hello.
4. Выберите **Удалить**.

## <a name="common-vm-extensions-reference"></a>Справочники по распространенным расширениям виртуальной машины
| Имя расширения | Описание | Дополнительные сведения |
| --- | --- | --- |
| Расширение Custom Script в ОС Windows |Выполняет сценарии на виртуальных машинах Azure. |[Расширение Custom Script в ОС Windows](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Расширение DSC в ОС Windows |Расширение PowerShell DSC (настройка требуемого состояния) |[Общие сведения об обработчике расширения Desired State Configuration в Azure](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Расширение системы диагностики Azure |Управляет системой диагностики Azure |[Расширение системы диагностики Azure](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| Расширение Azure VM Access |Управляет пользователями и учетными данными. |[Расширение VM Access для Linux](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
