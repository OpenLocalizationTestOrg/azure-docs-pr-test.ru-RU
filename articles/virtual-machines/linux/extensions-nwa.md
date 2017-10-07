---
title: "aaaAzure расширение агента Наблюдатель сети виртуальной машины для Linux | Документы Microsoft"
description: "Развертывание hello агента Наблюдатель сети на виртуальной машине Linux с помощью расширения виртуальной машины."
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a>Расширение виртуальной машины агента Наблюдателя за сетями для Linux

## <a name="overview"></a>Обзор

[Наблюдатель за сетями Azure](https://review.docs.microsoft.com/en-us/azure/network-watcher/) — это служба мониторинга производительности, диагностики и анализа сети, позволяющая наблюдать за сетями Azure. Hello расширение виртуальной машины агента Наблюдатель сети является обязательным для некоторых функций hello Наблюдатель сети на виртуальных машинах Azure. Сюда входит запись сетевого трафика по запросу и другие дополнительные функциональные возможности.

Этот документ сведения hello платформ и параметры развертывания hello расширение агента Наблюдатель сети виртуальной машины для Linux поддерживает.

## <a name="prerequisites"></a>Предварительные требования

### <a name="operating-system"></a>операционная система

Hello расширение Agent Наблюдатель сети можно выполнять на этих дистрибутивов Linux:

| Дистрибутив | Version (версия) |
|---|---|
| Ubuntu | 16.04 LTS, 14.04 LTS и 12.04 LTS |
| Debian | 7 и 8 |
| RedHat | 6.x и 7.x |
| Oracle Linux | 7x |
| SUSE | 11 и 12 |
| openSUSE | 7.0 |
| CentOS | 7.0 |

Обратите внимание, что CoreOS в данный момент не поддерживается.

### <a name="internet-connectivity"></a>Подключение к Интернету

Некоторые функциональные возможности агента Наблюдатель сети hello требует hello целевой виртуальной машины подключенных toohello Интернета. Без hello возможность tooestablish исходящих подключений некоторых функций hello агента Наблюдатель сети может работать неправильно или становятся недоступными. Дополнительные сведения см. в разделе hello [документации Наблюдатель сети](https://review.docs.microsoft.com/en-us/azure/network-watcher/).

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
        "type": "NetworkWatcherAgentLinux",
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
| type | NetworkWatcherAgentLinux |
| typeHandlerVersion | 1.4 |

## <a name="template-deployment"></a>Развертывание шаблона

Расширения виртуальной машины Azure можно развернуть с помощью шаблонов Azure Resource Manager. можно использовать схему JSON Hello, описанные в предыдущем разделе hello в hello toorun шаблона диспетчера ресурсов Azure расширение Agent Наблюдатель сети во время развертывания шаблона диспетчера ресурсов Azure.

## <a name="azure-cli-deployment"></a>Развертывание с помощью Azure CLI

Hello Azure CLI можно используется toodeploy hello сетевых наблюдателей агента ВМ расширения tooan существующей виртуальной машины.

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a>Устранение неполадок и поддержка

### <a name="troubleshooting"></a>Устранение неполадок

Данные о состоянии hello развертываний расширения могут быть получены из hello портал Azure, а также с помощью hello Azure CLI. Состояние развертывания hello toosee расширений для данной виртуальной Машины, запустите следующие команды, используя hello hello Azure CLI.

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

Модуль выполнения выходной журнал toofiles в hello следовать каталога:

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a>Поддержка

Если вам нужна дополнительная помощь в любой момент в этой статье, можно см. документации toohello Наблюдатель сети или обратитесь в службу hello Azure экспертами hello [форумы MSDN Azure и переполнения стека](https://azure.microsoft.com/en-us/support/forums/). Кроме того, можно зарегистрировать обращение в службу поддержки Azure. Go toohello [сайт поддержки Azure](https://azure.microsoft.com/en-us/support/options/) и выбрать получение поддержки. Дополнительные сведения об использовании Azure поддерживает чтение hello [поддержки Microsoft Azure часто задаваемые вопросы о](https://azure.microsoft.com/en-us/support/faq/).
