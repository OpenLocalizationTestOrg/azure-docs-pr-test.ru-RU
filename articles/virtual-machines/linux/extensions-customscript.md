---
title: "пользовательские сценарии aaaRun на виртуальных машинах Linux в Azure | Документы Microsoft"
description: "Автоматизировать настройку виртуальных Машин Linux с помощью hello настраиваемое расширение скриптов"
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
ms.openlocfilehash: f2c273a5fbd4cd1695aea48fa4bd08e691511e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-custom-script-extension-with-linux-virtual-machines"></a>С помощью hello Azure настраиваемое расширение скриптов с виртуальных машин Linux
Hello настраиваемое расширение скриптов загружает и запускает сценарии на виртуальных машинах Azure. Это расширение можно использовать для настройки после развертывания, установки программного обеспечения и других задач настройки или управления. Скрипты можно загружается из хранилища Azure или другое доступное расположение в Интернете, или предоставить toohello расширения времени выполнения. Hello расширение пользовательского скрипта интегрируется с шаблоны Azure Resource Manager и также можно выполнить с помощью hello Azure CLI, PowerShell, портал Azure или hello API REST Azure виртуальной машины.

Этот документ описывает, каким образом toouse hello настраиваемое расширение скриптов из hello Azure CLI и шаблона Azure Resource Manager, а также сведения об устранения неполадок в системах Linux.

## <a name="extension-configuration"></a>Конфигурация расширения
Конфигурация настраиваемого расширения скриптов Hello указывает расположение скрипта и запустите toobe команда hello. Эта конфигурация могут храниться в файлах конфигурации, указанные в командной строке hello, или в шаблон диспетчера ресурсов Azure. Конфиденциальные данные могут храниться в защищенной конфигурации, которая шифруются и расшифровываются только hello виртуальной машине. Защищенная конфигурация Hello удобен для команды выполнения hello содержит секретные данные, например пароля.

### <a name="public-configuration"></a>Открытая конфигурация
Схема.

**Примечание**. В именах свойств учитывается регистр. Используйте имена hello, как показано ниже tooavoid проблем развертывания.

* **commandToExecute**: (обязательно, string) hello tooexecute сценария точки входа
* **fileUris**: загружаются hello URL-адреса для toobe файлов (необязательный, массив строк).
* **Отметка времени** (необязательный, целое число) использовать это поле только tootrigger повторить hello скрипта, изменив значение этого поля.

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a>Защищенная конфигурация
Схема.

**Примечание**. В именах свойств учитывается регистр. Используйте имена hello, как показано ниже tooavoid проблем развертывания.

* **commandToExecute**: (необязательный, string) hello tooexecute сценария точки входа. Используйте это поле, если команда содержит секретные данные, например пароли.
* **storageAccountName**: (необязательный, string) hello имя учетной записи хранения. Если указаны учетные данные, все значения fileUris должны иметь формат URL-адресов для BLOB-объектов Azure.
* **storageAccountKey**: (необязательный, string) hello ключа доступа учетной записи хранения.

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a>Инфраструктура CLI Azure
При использовании hello Azure CLI toorun hello настраиваемое расширение скриптов, создайте файл конфигурации или файлов, содержащих uri файла минимального hello и hello команды выполнения скрипта.

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

При необходимости hello можно задать параметры в команде hello как строка в формате JSON. Это позволяет toobe hello конфигурации, заданные во время выполнения и без отдельный файл конфигурации.

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

**Пример 3** — файл открытой конфигурации файла скрипта используется toospecify hello URI, который файл защищенной конфигурации используется toospecify hello команда toobe выполнена.

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
Hello Azure настраиваемое расширение скриптов может выполняться во время развертывания виртуальной машины с помощью шаблона диспетчера ресурсов. Таким образом, toodo добавить шаблон развертывания toohello правильно отформатированную JSON.

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

Разделе hello .net Core Music Store Демонстрация полный пример - [Демонстрация хранилища Музыка](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).

## <a name="troubleshooting"></a>Устранение неполадок
При запуске hello настраиваемое расширение скриптов hello скрипт создается или загружать их в аналогичные toohello каталог, следующий пример. выходные данные команды Hello также сохраняется в этот каталог в `stdout` и `stderr` файла.

```bash
/var/lib/waagent/custom-script/download/0/
```

Hello расширение сценария Azure создает журнал, который можно найти здесь.

```bash
/var/log/azure/custom-script/handler.log
```

также можно получить состояние выполнения Hello hello настраиваемое расширение скриптов с hello Azure CLI.

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

Hello вывод выглядит следующим образом после текста hello.

```azurecli
info:    Executing command vm extension get
+ Looking up hello VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a>Дальнейшие действия
Сведения о других расширениях сценариев для виртуальной машины см. в статье [Обзор расширений и компонентов виртуальной машины](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

