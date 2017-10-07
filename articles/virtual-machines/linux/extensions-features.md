---
title: "aaaVirtual машины расширения и компоненты для Linux | Документы Microsoft"
description: "Узнайте о расширениях, доступных для виртуальных машин Azure и сгруппированных по предоставляемым функциям или улучшениям."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 52f5d0ec-8f75-49e7-9e15-88d46b420e63
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: e0d2ce794c76815ccc6743e8788ee5d9d931e9a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a>Обзор расширений и компонентов виртуальных машин под управлением Linux

Расширения виртуальных машин Azure — это небольшие приложения, которые выполняют задачи настройки и автоматизации после развертывания виртуальных машин Azure. Например, если виртуальная машина требует установки программного обеспечения защиты от вирусов и конфигурации Docker, расширение ВМ может быть используется toocomplete этих задач. Расширений ВМ Azure можно выполнить с помощью hello Azure CLI PowerShell шаблоны диспетчера ресурсов Azure и hello портал Azure. Расширения могут предоставляться в рамках нового развертывания виртуальной машины и работать в любой из существующих систем.

Этот документ предоставляет обзор расширений ВМ, предварительные условия для использования расширений ВМ Azure и руководство о предоставлении toodetect, управление и удаление расширений ВМ. Этот документ содержит только обобщенные сведения, так как существует множество расширений виртуальной машины с разными параметрами настройки. Сведения о различных модулей можно найти в каждое расширение отдельных toohello определенного документа.

## <a name="use-cases-and-samples"></a>Варианты использования и примеры

Существует несколько разных расширений ВМ Azure, которые используются в определенных сценариях. Ниже приведены некоторые примеры.

- Примените требуемого состояния PowerShell конфигураций tooa виртуальной машины с помощью hello расширение DSC для Linux. Подробнее см. [Общие сведения об обработчике расширения Desired State Configuration в Azure](https://github.com/Azure/azure-linux-extensions/tree/master/DSC);
- Настройте наблюдение за виртуальную машину с hello расширения виртуальной Машины агента наблюдения Майкрософт. Дополнительные сведения см. в разделе [как toomonitor ВМ Linux](tutorial-monitoring.md).
- Настройка мониторинга инфраструктуры Azure с hello Datadog расширения. Дополнительные сведения см. в разделе hello [Datadog блог](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).
- Настройка узла Docker на виртуальной машине Azure с помощью расширения виртуальной Машины Docker hello. Дополнительные сведения см. в статье [Использование расширения виртуальной машины Docker для развертывания среды](dockerextension.md).

Кроме расширения tooprocess, расширение пользовательского скрипта доступен для виртуальных машин Windows и Linux. Hello расширение пользовательского скрипта для Linux позволяет любой скрипт toobe Bash, выполните на виртуальной машине. Пользовательские сценарии могут пригодиться при проектировании развертывания Azure, для которого требуется дополнительная настройка, ее невозможно выполнить собственными средствами Azure. Дополнительные сведения см. в статье [Использование расширения пользовательских сценариев Azure на виртуальных машинах Linux](extensions-customscript.md).


## <a name="prerequisites"></a>Предварительные требования

Для каждого расширения ВМ могут существовать свои требования. К примеру hello расширение ВМ Docker обладает необходимым условием поддерживаемые ОС Linux. Требования отдельных расширений, описаны в документации конкретного расширения hello.

### <a name="azure-vm-agent"></a>Агент виртуальной машины Azure

агент ВМ Azure Hello управляет взаимодействиями между виртуальной машины Azure и Azure fabric controller hello. агент виртуальной Машины Hello отвечает за многие аспекты работы развертывания и управления Azure виртуальные машины, включая выполнение расширений ВМ. агент ВМ Azure Hello предустановлен на Azure Marketplace образов и можно установить вручную на поддерживаемых операционных системах.

Сведения о поддерживаемых операционных системах и инструкции по установке см. в статье [Обзор агента и расширений виртуальной машины](../windows/classic/agents-and-extensions.md).

## <a name="discover-vm-extensions"></a>Поиск расширений ВМ

Существует множество различных расширений ВМ, которые можно использовать с виртуальными машинами Azure. toosee полный список запуска hello следующую команду с hello Azure CLI, заменив пути hello hello местом по своему усмотрению.

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a>Запуск расширений ВМ

Расширения виртуальных машин Azure может выполняться на существующих виртуальных машин, которые могут быть полезны при необходимости изменения конфигурации toomake или восстановить подключение на уже развернутой виртуальной Машины. Также расширения можно использовать при развертывании с помощью шаблонов Azure Resource Manager. Используя расширения вместе с шаблонами Resource Manager, можно так развернуть и настроить виртуальные машины Azure, чтобы не после развертывания не требовались дополнительные действия.

Hello следующие методы можно использовать toorun расширение для существующей виртуальной машины.

### <a name="azure-cli"></a>Инфраструктура CLI Azure

Расширения виртуальных машин Azure, выполняемых над существующей виртуальной машины с помощью hello `az vm extension set` команды. В этом примере выполняется расширение пользовательского скрипта hello от виртуальной машины.

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

Здравствуйте, сценарий создает выходные данные примерно toohello следующий текст:

```azurecli
info:    Executing command vm extension set
+ Looking up hello VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a>Портал Azure

Расширения ВМ может быть применен tooan существующей виртуальной машины через портал Azure hello. toodo таким образом, выбрать hello виртуальную машину, выберите **расширения**и нажмите кнопку **добавить**. Выберите расширение hello из hello список доступных расширений и выполните инструкции мастера hello hello.

Hello следующем рисунке показана установка hello hello расширения Linux пользовательский сценарий из hello портал Azure.

![Установка расширения пользовательских сценариев](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a>Шаблоны диспетчера ресурсов Azure

Расширения ВМ может быть добавлено tooan шаблона диспетчера ресурсов Azure и выполняться hello развертывания шаблона hello. Развертывая расширение вместе с шаблоном, можно создать полностью настроенное развертывание Azure. Например следующий JSON hello берется из шаблона диспетчера ресурсов. шаблон Hello развертывает набор с балансировкой нагрузки виртуальные машины и базы данных Azure SQL, а затем устанавливает приложение .NET Core на каждой виртуальной Машине. Установка программного обеспечения hello обеспечивает Hello расширения виртуальной Машины.

Дополнительные сведения см. в разделе hello полного [шаблона диспетчера ресурсов](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
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
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
    }
}
```

Дополнительные сведения см. в статье [Создание шаблонов Azure Resource Manager](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).

## <a name="secure-vm-extension-data"></a>Защита данных в расширениях ВМ

При работе с расширением ВМ, может быть необходимо tooinclude конфиденциальные сведения, например учетные данные, имена учетных записей хранилища и ключи доступа к учетной записи хранения. Множество расширений ВМ включают защищенной конфигурации, который шифрует данные и только расшифровывает его целевой виртуальной машине hello. Каждое расширение имеет собственную схему защищенной конфигурации, которая описывается в документации по этим расширениям.

Привет, в следующем примере показан экземпляр hello расширение пользовательского скрипта для Linux. Обратите внимание, что команды, hello tooexecute включает в себя набор учетных данных. В этом примере команда tooexecute hello не будут зашифрованы.


```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
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
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ],
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

Перемещение hello **tooexecute команда** toohello свойство **защищенных** конфигурации защищает строку hello выполнения.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
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
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

## <a name="troubleshoot-vm-extensions"></a>Устранение неполадок с расширениями ВМ

Каждое расширение ВМ, возможно, устранение неполадок расширения toohello определенного действия. Например когда вы используете расширение пользовательского скрипта hello, сведения о выполнении скрипта можно найти локально на hello виртуальной машины, на котором был выполнен hello расширения. Действия по устранению неполадок для конкретных расширений описаны в документации по соответствующим расширениям.

следующие шаги по устранению неполадок Hello применяются tooall расширения виртуальных машин.

### <a name="view-extension-status"></a>Просмотр состояния расширения

После завершения выполнения расширения виртуальной машины от виртуальной машины, используйте следующие состояния расширения tooreturn команды Azure CLI hello. Замените в примере имена-параметры собственными значениями.

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

Hello вывод выглядит следующим образом после текста hello.

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

Состояние выполнения расширения можно найти также в hello портал Azure. состояние hello tooview расширение, выберите hello виртуальной машины, выберите **расширения**, и выберите hello нужное расширение.

### <a name="rerun-a-vm-extension"></a>Повторный запуск расширения ВМ

Возможны ситуации, в которых расширение виртуальной машины должен toobe повторно. Можно повторно запустить расширение, удалив и повторно запустив hello расширения с помощью метода выполнения по своему усмотрению. tooremove расширение, запустите следующую команду с hello Azure CLI hello. Замените в примере имена-параметры собственными значениями.

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

Расширение можно удалить с помощью инструкций из портала Azure hello hello.

1. Выберите виртуальную машину.
2. Выберите **Расширения**.
3. Выберите расширение требуемого hello.
4. Выберите **Удалить**.

## <a name="common-vm-extension-reference"></a>Справочные материалы для всех расширений ВМ
| Имя расширения | Описание | Дополнительные сведения |
| --- | --- | --- |
| Расширение пользовательских сценариев для Linux |Выполняет сценарии на виртуальных машинах Azure. |[Расширение пользовательских сценариев для Linux](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| Расширение Docker |Установите hello Docker daemon toosupport удаленных команд Docker. |[Расширение виртуальной машины Docker](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| Расширение для доступа к виртуальной машине |Восстановить tooan доступа к виртуальной машине Azure |[Расширение для доступа к виртуальной машине](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| Расширение системы диагностики Azure |Управляет системой диагностики Azure. |[Расширение системы диагностики Azure](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| Расширение Azure VM Access |Управляет пользователями и учетными данными. |[Расширение VM Access для Linux](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
