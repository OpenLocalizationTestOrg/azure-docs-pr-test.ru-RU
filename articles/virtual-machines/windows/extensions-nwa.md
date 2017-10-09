---
title: "aaaAzure расширение виртуальной машины агента Наблюдатель сети для Windows | Документы Microsoft"
description: "Развертывание hello агента Наблюдатель сети на виртуальной машине Windows, с помощью расширения виртуальной машины."
services: virtual-machines-windows
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 27e46af7-2150-45e8-b084-ba33de8c5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 21298706e462ff32c4d314f9a1ad127074ddf481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a>Расширение виртуальной машины агента Наблюдателя за сетями для Windows

## <a name="overview"></a>Обзор

[Наблюдатель за сетями Azure](https://review.docs.microsoft.com/en-us/azure/network-watcher/) — это служба мониторинга производительности, диагностики и анализа сети, позволяющая наблюдать за сетями Azure. Hello расширение виртуальной машины агента Наблюдатель сети является обязательным для некоторых функций hello Наблюдатель сети на виртуальных машинах Azure. Сюда входит запись сетевого трафика по запросу и другие дополнительные функциональные возможности.

Сведения этого документа hello поддерживается платформ и параметры развертывания для hello расширение агента Наблюдатель сети виртуальной машины для Windows.

## <a name="prerequisites"></a>Предварительные требования

### <a name="operating-system"></a>операционная система

Hello расширение Agent Наблюдатель сети для Windows, которые могут выполняться для Windows Server 2008 R2, 2012 и 2012 R2, 2016 освобождает. Обратите внимание, что hello Nano Server в настоящее время не поддерживается.

### <a name="internet-connectivity"></a>Подключение к Интернету

Некоторые функциональные возможности агента Наблюдатель сети hello требует hello целевой виртуальной машины подключенных toohello Интернета. Без hello возможность tooestablish исходящих подключений некоторых функций hello агента Наблюдатель сети может работать неправильно или становятся недоступными. Дополнительные сведения см. в разделе hello [документации Наблюдатель сети](../../network-watcher/network-watcher-monitoring-overview.md).

## <a name="extension-schema"></a>Схема расширения

Hello следующий JSON показана схема hello для hello расширение Agent Наблюдатель сети. Hello расширение не требуется ни в настоящее время поддерживает все параметры, предоставленные пользователем и зависит от конфигурации по умолчанию.

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentWindows",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a>Значения свойств

| Имя | Значение и пример |
| ---- | ---- |
| версия_API | 2015-06-15 |
| publisher | Microsoft.Azure.NetworkWatcher |
| type | NetworkWatcherAgentWindows |
| typeHandlerVersion | 1.4 |


## <a name="template-deployment"></a>Развертывание шаблона

Расширения виртуальной машины Azure можно развернуть с помощью шаблонов Azure Resource Manager. можно использовать схему JSON Hello, описанные в предыдущем разделе hello в hello toorun шаблона диспетчера ресурсов Azure расширение Agent Наблюдатель сети во время развертывания шаблона диспетчера ресурсов Azure.

## <a name="powershell-deployment"></a>Развертывание с помощью PowerShell

Hello `Set-AzureRmVMExtension` команду можно использовать toodeploy hello агента Наблюдатель сети виртуальной машины расширения tooan существующей виртуальной машины.

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a>Устранение неполадок и поддержка

### <a name="troubleshooting"></a>Устранение неполадок

Данные о состоянии hello развертываний расширения могут быть получены из hello портал Azure, а также с помощью модуля Azure PowerShell hello. Состояние развертывания hello toosee расширений для данной виртуальной Машины выполнения hello следующие команды, используя hello модуля Azure PowerShell.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

Модуль выполнения выходной журнал toofiles в hello следовать каталога:

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a>Поддержка

Если вам нужна дополнительная помощь в любой момент в этой статье, можно см. документации toohello руководство пользователя Наблюдатель сети или обратитесь в службу hello Azure экспертами hello [форумы MSDN Azure и переполнения стека](https://azure.microsoft.com/en-us/support/forums/). Кроме того, можно зарегистрировать обращение в службу поддержки Azure. Go toohello [сайт поддержки Azure](https://azure.microsoft.com/en-us/support/options/) и выбрать получение поддержки. Дополнительные сведения об использовании Azure поддерживает чтение hello [поддержки Microsoft Azure часто задаваемые вопросы о](https://azure.microsoft.com/en-us/support/faq/).
