---
title: "Пример сценария Azure PowerShell. Масштабирование веб-приложения вручную | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для масштабирования веб-приложения вручную."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: de5d4285-9c7d-4735-a695-288264047375
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: e99dfc02b6ab4123cd5f95997285dca5cb686380
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="scale-a-web-app-manually"></a>Масштабирование веб-приложения вручную

В этой статье вы узнаете, как создать группу ресурсов, план службы приложений и веб-приложение. Затем вы выполните масштабирование плана службы приложений от одного экземпляра до нескольких.

При необходимости установите Azure PowerShell с помощью инструкции, приведенной в [руководстве Azure PowerShell](/powershell/azure/overview), а затем выполните команду `Login-AzureRmAccount`, чтобы создать подключение к Azure.

## <a name="sample-script"></a>Пример скрипта

[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Масштабирование веб-приложения вручную")]

## <a name="clean-up-deployment"></a>Очистка развертывания 

Выполнив пример сценария, вы можете удалить группу ресурсов, веб-приложение и все связанные ресурсы, используя следующую команду.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует следующие команды. Для каждой команды в таблице приведены ссылки на соответствующую документацию.

| Команда | Примечания |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Создает группу ресурсов, в которой хранятся все ресурсы. |
| [New-AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | Создает план службы приложений. |
| [New-AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | Создает веб-приложение. |
| [Set-AzureRmWebApp](/powershell/module/azurerm.websites/set-azurermwebapp) | Изменяет конфигурацию веб-приложения. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о модуле Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).

Дополнительные примеры сценариев Azure PowerShell для веб-приложений службы приложений Azure доступны [здесь](../app-service-powershell-samples.md).
