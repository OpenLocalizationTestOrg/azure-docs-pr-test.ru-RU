---
title: "Выполнение пользовательских сценариев на виртуальных машинах Linux в Azure | Документация Майкрософт"
description: "Автоматизируйте задачи настройки виртуальных машин Linux с помощью расширения пользовательских сценариев"
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cf17ab2b-8d7e-4078-b6df-955c6d5071c2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 1dde64aac72c11ccfccf4fdb676279692befaadd
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="using-the-azure-custom-script-extension-with-linux-virtual-machines"></a>Использование расширения пользовательских сценариев Azure на виртуальных машинах Linux
Расширение пользовательских сценариев загружает и запускает сценарии на виртуальных машинах Azure. Это расширение можно использовать для настройки после развертывания, установки программного обеспечения и других задач настройки или управления. Сценарии можно загрузить из службы хранилища Azure или другого расположения, доступного из Интернета, или передать во время выполнения расширения. Расширение пользовательских сценариев интегрируется с шаблонами Azure Resource Manager, а также его можно запустить с помощью интерфейса командной строки Azure, PowerShell, портала Azure или API REST виртуальной машины Azure.

В этом документе объясняется, как использовать расширение пользовательских сценариев с помощью командной строки Azure и шаблона Azure Resource Manager, а также подробно описываются действия по устранению неполадок в системах Linux.

## <a name="extension-configuration"></a>Конфигурация расширения
В конфигурации расширения пользовательских сценариев указываются такие параметры, как расположение сценария и команда для его выполнения. Эту конфигурацию можно хранить в файлах конфигурации, указать в командной строке или в шаблоне Azure Resource Manager. Конфиденциальные данные можно хранить в зашифрованном виде в защищенной конфигурации, которая расшифровывается только внутри виртуальной машины. Защищенную конфигурацию можно использовать для команд, которые содержат секретные данные, например пароли.

### <a name="public-configuration"></a>Открытая конфигурация
Схема.

**Примечание**. В именах свойств учитывается регистр. Используйте имена как показано ниже, чтобы избежать проблем с развертыванием.

* **commandToExecute**— (обязательный, строка) сценарий точки входа
* **fileUris**— (необязательный, строковый массив) URL-адреса файлов для загрузки.
* **timestamp** — (необязательный, целое число) используется только для повторного запуска скрипта при изменении значения этого поля.

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a>Защищенная конфигурация
Схема.

**Примечание**. В именах свойств учитывается регистр. Используйте имена как показано ниже, чтобы избежать проблем с развертыванием.

* **commandToExecute**— (необязательный, строка) сценарий точки входа. Используйте это поле, если команда содержит секретные данные, например пароли.
* **storageAccountName**— (необязательный, строка) имя учетной записи хранения. Если указаны учетные данные, все значения fileUris должны иметь формат URL-адресов для BLOB-объектов Azure.
* **storageAccountKey**— (необязательный, строка) ключ доступа для учетной записи хранения.

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a>Инфраструктура CLI Azure
Если вы запускаете расширение пользовательских сценариев из интерфейса командной строки Azure, создайте файл или файлы конфигурации, содержащие по меньшей мере универсальный код ресурса (URI) файла и команду выполнения сценария.

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

При необходимости можно указать параметры в команде в виде форматированной строки JSON. Это позволяет задать конфигурацию прямо во время выполнения, не используя отдельный файл конфигурации.

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a>Примеры использования интерфейса командной строки Azure

**Пример 1** — открытая конфигурация с файлом сценария.

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

Команда интерфейса командной строки Azure:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

**Пример 2** — открытая конфигурация без файла сценария.

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

Команда интерфейса командной строки Azure:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

**Пример 3** — используется файл открытой конфигурации для указания универсального кода ресурса (URI) файла сценария и файл защищенной конфигурации для указания выполняемой команды.

Файл открытой конфигурации:

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

Файл защищенной конфигурации:  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

Команда интерфейса командной строки Azure:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a>Шаблон Resource Manager
Расширение пользовательских сценариев Azure может выполняться во время развертывания виртуальной машины с использованием шаблона Resource Manager. Для этого добавьте правильно составленный объект JSON в шаблон развертывания.

### <a name="resource-manager-examples"></a>Примеры использования Resource Manager
**Пример 1** — открытая конфигурация.

```json
{
    "name": "scriptextensiondemo",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-15",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', parameters('scriptextensiondemoName'))]"
    ],
    "tags": {
        "displayName": "scriptextensiondemo"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
      "settings": {
        "fileUris": [
          "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
        ],
        "commandToExecute": "sh hello.sh"
      }
    }
}
```

**Пример 2** — команда выполнения в защищенной конфигурации.

```json
{
  "name": "config-app",
  "type": "extensions",
  "location": "[resourceGroup().location]",
  "apiVersion": "2015-06-15",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
      ]              
    },
    "protectedSettings": {
      "commandToExecute": "sh hello.sh <password>"
    }
  }
}
```

Готовый пример демонстрационной версии музыкального магазина .NET Core см. [здесь](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).

## <a name="troubleshooting"></a>Устранение неполадок
Расширение пользовательских сценариев при выполнении создает или загружает сценарий в каталог, как показано в примере ниже. Выходные данные команды также сохраняются в этот каталог в файлах `stdout` и `stderr`.

```bash
/var/lib/waagent/custom-script/download/0/
```

Расширение сценариев Azure создает журнал, который можно найти здесь.

```bash
/var/log/azure/custom-script/handler.log
```

Состояние выполнения для расширения пользовательских сценариев также можно получить с помощью интерфейса командной строки Azure.

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

Выходные данные выглядят так:

```azurecli
info:    Executing command vm extension get
+ Looking up the VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a>Дальнейшие действия
Сведения о других расширениях сценариев для виртуальной машины см. в статье [Обзор расширений и компонентов виртуальной машины](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

