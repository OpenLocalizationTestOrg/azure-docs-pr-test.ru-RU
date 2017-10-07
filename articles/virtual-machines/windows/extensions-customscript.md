---
title: "aaaAzure пользовательский скрипт расширения для Windows | Документы Microsoft"
description: "Автоматизации задач настройки виртуальной Машины Windows с помощью расширения пользовательский сценарий hello"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f4181fee-7a9d-4a1c-b517-52956f5b7fa1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/16/2017
ms.author: nepeters
ms.openlocfilehash: 97e065242e9fed116ee20b074f4e302a0cd10585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows"></a>Расширение Custom Script в ОС Windows

Hello настраиваемое расширение скриптов загружает и запускает сценарии на виртуальных машинах Azure. Это расширение можно использовать для настройки после развертывания, установки программного обеспечения и других задач настройки или управления. Скрипты можно загружается из хранилища Azure или GitHub, или предоставить toohello портал Azure во время выполнения модуля. Hello расширение пользовательского скрипта интегрируется с шаблоны Azure Resource Manager и также можно выполнить с помощью hello Azure CLI, PowerShell, портал Azure или hello API REST Azure виртуальной машины.

В этом документе описаны как с помощью настраиваемого расширения скриптов hello toouse hello модуля Azure PowerShell, шаблоны диспетчера ресурсов Azure и сведения об устранения неполадок в системах Windows.

## <a name="prerequisites"></a>Предварительные требования

### <a name="operating-system"></a>Операционная система

Hello настраиваемое расширение скриптов для Windows, которые могут выполняться для Windows Server 2008 R2, 2012 и 2012 R2, 2016 освобождает.

### <a name="script-location"></a>Расположение сценария

сценарий Hello должен toobe хранятся в хранилище больших двоичных объектов Azure или любом другом месте, доступные через допустимый URL-адрес.

### <a name="internet-connectivity"></a>Подключение к Интернету

Hello пользовательский скрипт расширения для Windows требует hello целевой виртуальной машины подключенных toohello Интернета. 

## <a name="extension-schema"></a>Схема расширения

Hello следующий JSON показана схема hello для hello настраиваемого расширения скриптов. модуль Hello требует местоположение скрипта (хранилища Azure или другое местоположение с допустимый URL-адрес) и tooexecute команды. При использовании хранилища Azure в качестве исходного текста сценария hello, требуется ключ учетной записи и имени учетной записи хранилища Azure. Эти элементы следует рассматривать как конфиденциальные данные и указанные в конфигурацию защищенных параметров расширения hello. Данных параметр расширение защищенных виртуальных Машин Azure шифруется и расшифрованы только hello целевой виртуальной машине.

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
        "typeHandlerVersion": "1.9",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "script location"
            ]
        },
        "protectedSettings": {
            "commandToExecute": "myExecutionCommand",
            "storageAccountName": "myStorageAccountName",
            "storageAccountKey": "myStorageAccountKey"
        }
    }
}
```

### <a name="property-values"></a>Значения свойств

| Имя | Значение и пример |
| ---- | ---- |
| версия_API | 2015-06-15 |
| publisher | Microsoft.Compute; |
| type | extensions |
| typeHandlerVersion | 1.9 |
| fileUris (пример) | https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1 |
| commandToExecute (пример) | powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 |
| storageAccountName (пример) | examplestorageacct |
| storageAccountKey (пример) | TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg== |

**Примечание**. В именах свойств учитывается регистр. Используйте имена hello, см. выше проблем развертывания tooavoid.

## <a name="template-deployment"></a>Развертывание шаблона

Расширения виртуальной машины Azure можно развернуть с помощью шаблонов Azure Resource Manager. можно использовать схему JSON Hello, описанные в предыдущем разделе hello в hello toorun шаблона диспетчера ресурсов Azure настраиваемое расширение скриптов во время развертывания шаблона диспетчера ресурсов Azure. Образец шаблона, включает hello настраиваемое расширение скриптов можно найти здесь, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="powershell-deployment"></a>Развертывание с помощью PowerShell

Hello `Set-AzureRmVMCustomScriptExtension` команду можно использовать tooadd hello пользовательский сценарий расширения tooan существующей виртуальной машины. Дополнительные сведения см. в статье о [Set-AzureRmVMCustomScriptExtension](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a>Устранение неполадок и поддержка

### <a name="troubleshoot"></a>Устранение неполадок

Данные о состоянии hello развертываний расширения могут быть получены из hello портал Azure, а также с помощью модуля Azure PowerShell hello. Состояние развертывания hello toosee расширений для данной виртуальной Машины, запустите следующую команду hello.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Модуль выполнения выходных данных зарегистрированного toofiles вложенной hello следовать directory hello целевой виртуальной машине.
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

файлы загружаются в следующий каталог hello целевой виртуальной машине hello указанный Hello.
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
где `<n>` имеет десятичное целое число, которое может измениться между выполнениями hello расширения.  Hello `1.*` значение соответствует фактическую, текущий hello `typeHandlerVersion` значение hello расширения.  Например, может быть действительных папках hello `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.  

При выполнении hello `commandToExecute` команды расширения hello задаст этот каталог (например, `...\Downloads\2`) как hello текущий рабочий каталог. Это включает использование hello относительные пути toolocate hello файлов загружены через hello `fileURIs` свойство. Приведенной ниже таблице hello, примеры.

Поскольку со временем может меняться hello загрузки абсолютный путь, будет лучше tooopt для относительных скрипт или путей к файлам в hello `commandToExecute` строки, когда это возможно. Например:
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

Сведения о пути после первого сегмента URI hello сохраняется для файлов загружены через hello `fileUris` списка свойств.  Как показано в следующей таблице hello, загруженные файлы сопоставляются в подкаталогах загрузки tooreflect структура hello hello `fileUris` значения.  

#### <a name="examples-of-downloaded-files"></a>Примеры скачанных файлов

| Универсальный код ресурса (URI) в fileUris | Относительное расположение скачанных файлов | Абсолютное расположение скачанных файлов* |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

\*Как выше, абсолютные пути hello изменит за время жизни hello hello виртуальной Машины, но не в пределах одного выполнения расширение CustomScript hello.

### <a name="support"></a>Поддержка

Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello Azure экспертами hello [форумы MSDN Azure и переполнения стека] (https://azure.microsoft.com/en-us/support/forums/). Кроме того, можно зарегистрировать обращение в службу поддержки Azure. Go toohello [сайт поддержки Azure](https://azure.microsoft.com/en-us/support/options/) и выбрать получение поддержки. Дополнительные сведения об использовании Azure поддерживает чтение hello [поддержки Microsoft Azure часто задаваемые вопросы о](https://azure.microsoft.com/en-us/support/faq/).
