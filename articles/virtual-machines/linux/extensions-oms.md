---
title: "aaaOMS расширение виртуальной машины Azure для Linux | Документы Microsoft"
description: "Разверните агент OMS hello на виртуальной машине Linux с помощью расширения виртуальной машины."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a>Расширение виртуальной машины OMS для Linux

## <a name="overview"></a>Обзор

Operations Management Suite (OMS) предоставляет возможности мониторинга, оповещений и внесения исправлений в соответствии с оповещениями для облачных и локальных ресурсов. расширение виртуальной машины агента OMS для Linux Hello публикации и поддерживается корпорацией Майкрософт. расширение Hello устанавливает агент OMS hello на виртуальных машинах Azure и регистрирует виртуальных машин в существующую рабочую область OMS. Этот документ сведения hello платформы, конфигурации и параметры развертывания hello расширение виртуальной машины OMS для Linux поддерживает.

## <a name="prerequisites"></a>Предварительные требования

### <a name="operating-system"></a>операционная система

для этих дистрибутивов Linux, можно запустить Hello расширение OMS Agent.

| Дистрибутив | Version (версия) |
|---|---|
| CentOS Linux | 5, 6 и 7 |
| Oracle Linux | 5, 6 и 7 |
| Сервер Red Hat Enterprise Linux | 5, 6 и 7 |
| Debian GNU/Linux | 6, 7 и 8 |
| Ubuntu | 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS |
| SUSE Linux Enterprise Server | 11 и 12 |

### <a name="internet-connectivity"></a>Подключение к Интернету

Hello расширение агента OMS для Linux требует hello целевой виртуальной машины подключенных toohello Интернета. 

## <a name="extension-schema"></a>Схема расширения

Hello следующий JSON показана схема hello для hello расширение OMS Agent. расширения Hello требуются hello ключ рабочей области идентификатора и рабочей области из рабочей области OMS целевой hello; Эти значения можно найти на портале OMS hello. Так как ключ рабочей области hello должны рассматриваться как конфиденциальные данные, его должны храниться в защищенном Настройка конфигурации. Данных параметр расширение защищенных виртуальных Машин Azure шифруется и расшифрованы только hello целевой виртуальной машине. Обратите внимание, что в **workspaceId** и **workspaceKey** учитывается регистр знаков.

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a>Значения свойств

| Имя | Значение и пример |
| ---- | ---- |
| версия_API | 2015-06-15 |
| publisher | Microsoft.EnterpriseCloud.Monitoring |
| type | OmsAgentForLinux |
| typeHandlerVersion | 1.4 |
| workspaceID (пример) | 6f680a37-00c6-41c7-a93f-1437e3462574 |
| workspaceKey (пример) | z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ== |


## <a name="template-deployment"></a>Развертывание шаблона

Расширения виртуальной машины Azure можно развернуть с помощью шаблонов Azure Resource Manager. Шаблоны представляют собой идеальный при развертывании одного или нескольких виртуальных машин, требующих после настройки развертывания, например tooOMS адаптации. Образец шаблона диспетчера ресурсов, включает в себя расширение виртуальной Машины агента OMS hello можно найти на hello [Azure быстрого запуска коллекции](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm). 

Hello конфигурации JSON для расширения виртуальной машины может быть вложена в ресурс виртуальной машины hello или помещается в корень hello или шаблон JSON диспетчера ресурсов верхнего уровня. Размещение Hello конфигурации JSON hello влияет значение hello hello ресурсов именем и типом. Дополнительные сведения см. в разделе [Указание имени и типа дочернего ресурса в шаблоне Resource Manager](../../azure-resource-manager/resource-manager-template-child-resource.md). 

Hello в примере предполагается, что расширение OMS hello вложен в hello ресурса виртуальной машины. При вложении hello расширения ресурса, hello JSON помещается в hello `"resources": []` объекта hello виртуальной машины.

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

При помещении hello расширения JSON в корне hello hello шаблона, имя ресурса hello ссылка toohello родительской виртуальной машиной и тип hello отражает hello вложенных конфигурации.  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a>Развертывание с помощью Azure CLI

Hello Azure CLI можно используется toodeploy hello ВМ агента OMS расширения tooan существующей виртуальной машины. Замените ключ hello OMS и OMS код из рабочей области OMS. 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a>Устранение неполадок и поддержка

### <a name="troubleshoot"></a>Устранение неполадок

Данные о состоянии hello развертываний расширения могут быть получены из hello портал Azure, а также с помощью hello Azure CLI. Состояние развертывания hello toosee расширений для данной виртуальной Машины, запустите следующие команды, используя hello hello Azure CLI.

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

Модуль выполнения выходных данных журнал toohello следующие файл:

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a>Коды ошибок и их описание

| Код ошибки | Значение | Возможное действие |
| :---: | --- | --- |
| 10 | Виртуальная машина уже подключенных tooan рабочей области OMS | tooconnect рабочей области для toohello hello виртуальной Машины указан в схеме расширения hello, задать stopOnMultipleConnections toofalse в общие параметры настройки или удалите это свойство. Счет для этой виртуальной машины выставляется за каждую рабочую область, к которой она подключена. |
| 11 | Недопустимый конфигурации указано toohello расширения | Выполните hello в предыдущих примерах tooset все значения свойств, необходимых для развертывания. |
| 12 | Диспетчер пакетов dpkg Hello заблокирован | Убедитесь, что все dpkg операции обновления на компьютере hello завершена и повторите попытку. |
| 20 | Преждевременный вызов операции включения | [Обновление hello Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello последней доступной версии. |
| 51 | Это расширение не поддерживается в операционной системе виртуальной Машины hello | |
| 55 | Не удается подключиться к службе Microsoft Operations Management Suite toohello | Проверьте, что hello система имеет доступ к Интернету или что предоставлено допустимое HTTP-прокси. Кроме того Проверьте правильность hello кода hello рабочей области. |

Дополнительные сведения об устранении неполадок можно найти на hello [руководство по устранению неполадок агента OMS для Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).

### <a name="support"></a>Поддержка

Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello Azure экспертами hello [форумы MSDN Azure и переполнения стека](https://azure.microsoft.com/en-us/support/forums/). Кроме того, можно зарегистрировать обращение в службу поддержки Azure. Go toohello [сайт поддержки Azure](https://azure.microsoft.com/en-us/support/options/) и выбрать получение поддержки. Дополнительные сведения об использовании Azure поддерживает чтение hello [поддержки Microsoft Azure часто задаваемые вопросы о](https://azure.microsoft.com/en-us/support/faq/).
