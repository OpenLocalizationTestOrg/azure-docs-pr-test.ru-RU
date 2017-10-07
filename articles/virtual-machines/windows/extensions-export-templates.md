---
title: "aaaExporting групп ресурсов Azure, содержащего расширения ВМ | Документы Microsoft"
description: "Экспорт шаблонов Resource Manager, которые включают расширения виртуальной машины."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: cdbc2030988a19fe68429e8733dc60536c264abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a>Экспорт групп ресурсов, которые содержат расширения виртуальной машины

Вы можете экспортировать группы ресурсов Azure в новый шаблон Resource Manager, а затем развернуть этот шаблон. Hello в процессе экспорта интерпретирует существующих ресурсов и создает шаблона диспетчера ресурсов, при развертывании приводит аналогичные группы ресурсов. При использовании параметра экспорта hello группы ресурсов для группы ресурсов, содержащий расширения виртуальных машин, несколько элементов необходимость toobe считается например совместимости расширений и защищенные параметры.

Этот документ описывает, как работает hello группы ресурсов в процессе экспорта относительно расширения виртуальных машин, включая список поддерживаемых модулей и сведения об обработке защищенным данным.

## <a name="supported-virtual-machine-extensions"></a>Поддерживаемые расширения виртуальной машины

Доступно много разных расширений виртуальной машины. Не все расширения можно экспортировать в виде шаблона диспетчера ресурсов с помощью функции «Сценарий автоматизации» hello. Если расширение виртуальной машины не поддерживается, он должен вручную помещаются обратно в экспортированный шаблон hello toobe.

Hello следующие расширения можно экспортировать с помощью функции скрипта автоматизации hello.

| Добавочный номер ||||
|---|---|---|---|
| Резервное копирование Acronis | Агент Datadog для Windows | Исправления для ОС Linux | Моментальные снимки виртуальной машины Linux
| Резервное копирование Acronis для Linux | Расширение Docker | Агент Puppet |
| Сведения о BG | Расширение DSC | Site 24x7 для Apm Insight |
| Агент BMC CTM для Linux | Dynatrace для Linux | Site 24x7 для сервера Linux |
| Агент BMC CTM для Windows | Dynatrace для Windows | Site 24x7 для сервера Windows Server |
| Клиент Chef | Защитник приложений HPE Security | Trend Micro DSA |
| Custom Script | Защита от вредоносных программ IaaS | Trend Micro DSA для Linux |
| Расширение пользовательских сценариев | Диагностика IaaS | VM Access для Linux |
| Custom Script для Linux | Клиент Chef для Linux | VM Access для Linux |
| Агент Datadog для Linux | Диагностика Linux | Моментальный снимок виртуальной машины |

## <a name="export-hello-resource-group"></a>Экспорт hello группы ресурсов

tooexport группу ресурсов в повторно используемый шаблон завершения hello, следующие шаги:

1. Войдите в toohello портал Azure
2. Щелкните hello в главном меню, группы ресурсов
3. Выберите из списка hello hello целевой группы ресурсов
4. В колонке hello группы ресурсов щелкните сценарий автоматизации

![Экспорт шаблона](./media/extensions-export-templates/template-export.png)

Hello сценариев автоматизации Azure Resource Manager создает шаблона диспетчера ресурсов, файл параметров и несколько примеров сценариев развертывания, таких как Azure CLI и PowerShell. На этом этапе hello экспортированный шаблон можно загрузить с помощью кнопки загрузки hello, добавляется новый библиотека шаблонов toohello шаблона или повторно развернуть с помощью hello кнопка "Развертывание".

## <a name="configure-protected-settings"></a>Настройка защищенных конфигураций

Многие расширения виртуальной машины Azure поддерживают использование защищенных конфигураций, при котором шифруются конфиденциальные данные, например учетные данные и строки конфигурации. Защищенные параметры не экспортируются вместе с сценарий автоматизации hello. При необходимости, защищенные параметры требуют toobe повторно hello экспортированный шаблон.

### <a name="step-1---remove-template-parameter"></a>Шаг 1. Удаление параметра шаблона

При создании tooprovide hello, который экспортируется группы ресурсов, один шаблон параметра toohello значение экспортированы защищенных параметров. Этот параметр можно удалить. параметр tooremove hello, просмотрите список параметров hello и удалить параметр hello, выполняющее аналогичный пример toothis JSON.

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a>Шаг 2. Получение свойств защищенных конфигураций

Поскольку каждого защищенного параметра имеет набор обязательных свойств, список этих свойств должны toobe сбора. Каждый параметр hello защищенные параметры конфигурации можно найти в hello [схемы диспетчера ресурсов Azure на GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json). Эта схема включает только hello наборов параметров для расширений hello, перечисленные в разделе Обзор hello этого документа. 

Из в репозитории схемы hello, поиск hello требуемого расширения, в этом примере `IaaSDiagnostics`. Один раз hello расширения `protectedSettings` обнаружен объект, запишите каждого параметра. В приведенном примере hello hello `IaasDiagnostic` модуль, hello требует параметры `storageAccountName`, `storageAccountKey`, и `storageAccountEndPoint`.

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-hello-protected-configuration"></a>Шаг 3. повторно создать конфигурацию защищенных hello

В случае hello экспортированный шаблон — поиск `protectedSettings` и замените экспортированного защищенных установки hello объекта новый, который включает параметры hello необходимые расширения и значение для каждого из них.

В приведенном примере hello hello `IaasDiagnostic` расширения, новая конфигурация защищенного параметр hello выглядит следующим образом hello в следующем примере:

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

Hello окончательным расширением ресурсов выглядит примерно toohello следующий пример JSON:

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

При использовании значений свойств tooprovide параметры шаблона, они должны toobe создан. При создании параметров шаблона для защищенного задание значений убедитесь, что hello toouse `SecureString` параметра типа, чтобы защищаются конфиденциальные значения. Дополнительную информацию об использовании параметров см. в статье [Создание шаблонов Azure Resource Manager](../../resource-group-authoring-templates.md).

В приведенном примере hello hello `IaasDiagnostic` расширения, будут создаваться hello следующие параметры в разделе параметров hello hello шаблона диспетчера ресурсов.

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

На этом этапе hello шаблона могут быть развернуты с любой метод развертывания шаблона.
