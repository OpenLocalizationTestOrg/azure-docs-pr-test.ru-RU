---
title: "aaaCustom расширением сценария на виртуальной Машине Windows | Документы Microsoft"
description: "Автоматизировать задачи настройки виртуальной Машины Azure с помощью сценариев PowerShell toorun расширение пользовательского скрипта hello в удаленной виртуальной Машине Windows"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: ebb7340a-8f61-4d3c-a290-d7bf8de2d0bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: nepeters
ms.openlocfilehash: cf7bb895dd211f07fd010dc03b68cd77df1127b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows-using-hello-classic-deployment-model"></a>Пользовательский скрипт расширения для Windows с помощью hello классической модели развертывания

> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Узнайте, каким образом слишком[выполните следующие действия с помощью диспетчера ресурсов модели hello](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Hello настраиваемое расширение скриптов загружает и запускает сценарии на виртуальных машинах Azure. Это расширение можно использовать для настройки после развертывания, установки программного обеспечения и других задач настройки или управления. Скрипты можно загружается из хранилища Azure или GitHub, или предоставить toohello портал Azure во время выполнения модуля. Hello расширение пользовательского скрипта интегрируется с шаблоны Azure Resource Manager и также можно выполнить с помощью hello Azure CLI, PowerShell, портал Azure или hello API REST Azure виртуальной машины.

В этом документе описаны как с помощью настраиваемого расширения скриптов hello toouse hello модуля Azure PowerShell, шаблоны диспетчера ресурсов Azure и сведения об устранения неполадок в системах Windows.

## <a name="prerequisites"></a>Предварительные требования

### <a name="operating-system"></a>Операционная система

Hello настраиваемое расширение скриптов для Windows, которые могут выполняться для Windows Server 2008 R2, 2012 и 2012 R2, 2016 освобождает.

### <a name="script-location"></a>Расположение сценария

сценарий Hello должен toobe хранятся в хранилище Azure или любом другом месте, доступные через допустимый URL-адрес.

### <a name="internet-connectivity"></a>Подключение к Интернету

Hello пользовательский скрипт расширения для Windows требует hello целевой виртуальной машины подключенных toohello Интернета. 

## <a name="extension-schema"></a>Схема расширения

Hello следующий JSON показана схема hello для hello настраиваемого расширения скриптов. модуль Hello требует местоположение скрипта (хранилища Azure или другое местоположение с допустимый URL-адрес) и tooexecute команды. При использовании хранилища Azure в качестве исходного текста сценария hello, требуется ключ учетной записи и имени учетной записи хранилища Azure. Эти элементы следует рассматривать как конфиденциальные данные и указанные в конфигурацию защищенных параметров расширения hello. Данных параметр расширение защищенных виртуальных Машин Azure шифруется и расшифрованы только hello целевой виртуальной машине.

```json
{
    "name": "config-app",
    "type": "Microsoft.ClassicCompute/virtualMachines/extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-01",
    "properties": {
        "publisher": "Microsoft.Compute",
        "extension": "CustomScriptExtension",
        "version": "1.8",
        "parameters": {
            "public": {
                "fileUris": "[myScriptLocation]"
            },
            "private": {
                "commandToExecute": "[myExecutionString]"
            }
        }
    }
}
```

### <a name="property-values"></a>Значения свойств

| Имя | Значение и пример |
| ---- | ---- |
| версия_API | 2015-06-15 |
| publisher | Microsoft.Compute; |
| Расширение | CustomScriptExtension |
| typeHandlerVersion | 1.8 |
| fileUris (пример) | https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1 |
| commandToExecute (пример) | powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 |

## <a name="template-deployment"></a>Развертывание шаблона

Расширения виртуальной машины Azure можно развернуть с помощью шаблонов Azure Resource Manager. можно использовать схему JSON Hello, описанные в предыдущем разделе hello в hello toorun шаблона диспетчера ресурсов Azure настраиваемое расширение скриптов во время развертывания шаблона диспетчера ресурсов Azure. Образец шаблона, включает hello настраиваемое расширение скриптов можно найти здесь, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="powershell-deployment"></a>Развертывание с помощью PowerShell

Hello `Set-AzureVMCustomScriptExtension` команду можно использовать tooadd hello пользовательский сценарий расширения tooan существующей виртуальной машины. Дополнительные сведения см. в статье о [Set-AzureRmVMCustomScriptExtension](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a>Устранение неполадок и поддержка

### <a name="troubleshoot"></a>Устранение неполадок

Данные о состоянии hello развертываний расширения могут быть получены из hello портал Azure, а также с помощью модуля Azure PowerShell hello. Состояние развертывания hello toosee расширений для данной виртуальной Машины, запустите следующую команду hello.

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Выполнение модуля вывода нам регистрируется toofiles в следующий каталог hello целевой виртуальной машине hello.

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

сам скрипт Hello загружается в следующий каталог hello целевой виртуальной машине hello.

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a>Поддержка

Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello Azure экспертами hello [форумы MSDN Azure и переполнения стека](https://azure.microsoft.com/en-us/support/forums/). Кроме того, можно зарегистрировать обращение в службу поддержки Azure. Go toohello [сайт поддержки Azure](https://azure.microsoft.com/en-us/support/options/) и выбрать получение поддержки. Дополнительные сведения об использовании Azure поддерживает чтение hello [поддержки Microsoft Azure часто задаваемые вопросы о](https://azure.microsoft.com/en-us/support/faq/).
